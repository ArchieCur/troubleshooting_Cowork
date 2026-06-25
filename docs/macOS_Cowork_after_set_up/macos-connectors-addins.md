# Fix: Connectors, Plugins, and Office Add-ins — macOS

You launched a Cowork session on your Mac, but your connected tools are missing, the MCP registry throws a red error banner, your custom connectors refuse to authenticate, or your Microsoft 365 add-ins have disappeared. Because Claude Desktop updates automatically in the background, the internal tool registry can fall out of sync with your workspace. Additionally, macOS caching bugs can cause Cowork to silently forget your OAuth logins or drop plugins when you restart the application.

Find your error below.

---

## Which error are you seeing?

### 🔴 "Could not connect to MCP server mcp-registry" or "Could not load connectors directory"

A background update caused the internal tool registry to lose sync with your workspace.

👉 [Jump to Fix 1](#fix-1-mcp-registry-out-of-sync)

---

### 🔴 Custom MCP connector silently fails to connect — or forgets your login after every restart

A caching bug in the `~/.claude` directory is preventing OAuth tokens from persisting.

👉 [Jump to Fix 2](#fix-2-custom-mcp-connector-wont-authenticate)

---

### 🔴 Plugins disappear from the Cowork tab every time you restart the app

Plugins installed through the visual marketplace are not persisting between app restarts.

👉 [Jump to Fix 3](#fix-3-plugins-disappear-after-restarting)

---

### 🔴 Excel or PowerPoint add-in disappeared — or shows an error when clicked

A known Cowork bug is removing or corrupting Microsoft 365 add-ins after each session.

👉 [Jump to Fix 4](#fix-4-office-add-in-disappears-after-cowork-session)

---

## Fix 1 — MCP Registry Out of Sync

**Error:** `"Could not connect to MCP server mcp-registry"` or `"Could not load connectors directory"`

A background auto-update to Claude Desktop caused the internal tool registry to fall out of sync with your workspace. All of your MCP tools become invisible to Cowork — even though they are still installed and functioning.

!!! warning "Do not use rm -rf to delete the vm_bundles folder"
    Some online sources suggest running `rm -rf` on the `vm_bundles` folder to fix this issue. **Do not do this.** That folder contains your active Cowork workspace state, including ongoing terminal sessions, uncommitted tasks, and local plugin data. Deleting it causes immediate and permanent loss of that data. The steps below rename the folders as backups instead, which is safe and reversible.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

**Step 1 — Quit Claude Desktop**

Press **Command + Q** while Claude is the active app to quit it fully.

**Step 2 — Open Terminal**

Press **Command + Space**, type `Terminal`, and press **Enter**.

**Step 3 — Rename the out-of-sync registry folders**

Run both commands as written. This renames the folders to backup copies rather than deleting them.

```bash
mv ~/Library/Application\ Support/Claude/vm_bundles ~/Library/Application\ Support/Claude/vm_bundles.bak
mv ~/Library/Application\ Support/Claude/claude-code-vm ~/Library/Application\ Support/Claude/claude-code-vm.bak
```

!!! note "If you see a 'cannot move' error"
    A backup from a previous run of this fix may already exist. Run the following to remove the old backups first, then repeat the commands above:
    ```bash
    rm -rf ~/Library/Application\ Support/Claude/vm_bundles.bak
    rm -rf ~/Library/Application\ Support/Claude/claude-code-vm.bak
    ```

**Step 4 — Relaunch Claude Desktop**

Claude Desktop will detect the missing folders and provision a fresh workspace, then reconnect to the MCP registry.

✅ **MCP tools back? You're done.**

❌ **Registry banner gone but tools still won't authenticate?**

This may be a known Anthropic server-side issue. Contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

The Terminal steps above apply to work Macs. However, if your employer's security software restricts access to your Library folder, the `mv` commands may return a permissions error. Contact your IT department if that happens.

!!! note "For IT departments"
    Claude Cowork's MCP tool registry is stored in two folders:
    - `~/Library/Application Support/Claude/vm_bundles`
    - `~/Library/Application Support/Claude/claude-code-vm`

    Renaming both folders (not deleting) and relaunching Claude Desktop forces a clean registry rebuild. If MDM or endpoint security software restricts writes to `~/Library/Application Support/`, a temporary exception for these paths is needed.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

## Fix 2 — Custom MCP Connector Won't Authenticate

**Symptom:** A custom MCP connector's **Connect** button silently fails when clicked, or the connector loses its login every time Claude Desktop restarts.

A caching bug prevents custom MCP connector OAuth tokens from persisting across app restarts. The local cache file (`mcp-needs-auth-cache.json`) does not properly track authentication state for custom (non-Anthropic-managed) connectors.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

**Step 1 — Quit Claude Desktop**

Press **Command + Q** while Claude is the active app.

**Step 2 — Open Terminal**

Press **Command + Space**, type `Terminal`, and press **Enter**.

**Step 3 — Clear the corrupted authentication cache**

```bash
rm ~/.claude/mcp-needs-auth-cache.json
```

This file is automatically recreated when Claude Desktop relaunches — deleting it is safe.

**Step 4 — Relaunch Claude Desktop and authenticate again**

Open Claude Desktop and try connecting the MCP connector again.

✅ **Connector authenticating? You're done.**

❌ **Connector still failing?**

!!! warning "For more confident Mac users"
    If clearing the cache did not help, the OAuth entry for your connector may need to be removed manually from a hidden credentials file. This involves opening a JSON file and deleting a specific entry. Only attempt this if you are comfortable editing plain-text files — an incorrectly edited file will break all saved credentials.

    1. In Terminal, open the credentials file in your default text editor:
       ```bash
       open -e ~/.claude/.credentials.json
       ```
    2. Find the `mcpOAuth` section and delete only the entry for the broken connector
    3. Save the file and close the editor
    4. Relaunch Claude Desktop and authenticate the connector again

If editing the credentials file does not resolve it, or if you are not comfortable doing so, contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

Custom MCP connector authentication issues on managed Macs may also be caused by MDM-enforced network policies blocking the OAuth callback URL. If the connector's authorization page opens in a browser but the authentication never completes, your corporate firewall or proxy may be intercepting the OAuth redirect.

Contact your IT department and ask them to allow OAuth callback traffic for the connector's registered redirect URI.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

## Fix 3 — Plugins Disappear After Restarting

**Symptom:** Plugins you installed through the Cowork marketplace tab are gone the next time you open Claude Desktop.

!!! warning "This is a known sync bug"
    Cowork's visual plugin marketplace and the underlying Claude Code command-line tool maintain separate, unsynchronized installation states. Plugins installed through the visual "Personal" marketplace tab are currently not persisted between app restarts.

There is no permanent fix for this yet. Two workarounds are available.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

**Workaround 1 — Reinstall from the marketplace tab each session**

Each time you open Claude Desktop, go to the Cowork marketplace tab and reinstall the plugins you need. This takes seconds but must be repeated every session.

**Workaround 2 — Use a personal marketplace with ZIP upload**

A more durable option: create your own personal marketplace and upload your plugins as `.zip` files through the admin UI. Plugins added this way are not subject to the restart sync bug.

This is a documented Anthropic feature — see the [Claude Desktop Extensions guide](https://www.anthropic.com/engineering/desktop-extensions) for how to set up a personal marketplace and use the manual upload option.

!!! note
    The ZIP upload approach requires initial setup time but eliminates the need to reinstall after every restart. It is the recommended path if you rely on specific plugins regularly.

✅ **Plugins staying put? You're done.**

❌ **Still disappearing?**

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

If your organization manages Claude Desktop centrally, individual plugin installation may be restricted. Contact your Anthropic account administrator to ask whether plugins can be deployed to your workspace from the organizational marketplace.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

## Fix 4 — Office Add-in Disappears After Cowork Session

**Symptoms — any of these may appear after a Cowork session ends:**

- The Claude add-in has disappeared from the PowerPoint ribbon entirely
- The Claude add-in is visible in Excel but clicking it produces an error or does nothing
- An error says `"Microsoft 365 has been configured to prevent individual acquisition"`

!!! warning "This is a confirmed, reproducible Cowork bug"
    Cowork's macOS virtualization layer interferes with Microsoft Office Web Add-in registration. After a Cowork session closes, it removes the Claude add-in manifest from PowerPoint and corrupts the execution context for Excel's add-in. This happens on every session and affects any new Office file, not just files Cowork touched.

    **There is no permanent local fix.** The add-ins must be re-enabled after each Cowork session until Anthropic resolves this at the application level.

    **What does not fix this:** Reinstalling Office, reinstalling Claude Desktop, using a different Microsoft 365 account, or creating a new macOS user profile.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

Work through these steps in order. Stop as soon as the add-in is working again.

**Step 1 — Sign out and back in to Microsoft Office**

Open Excel or PowerPoint → click your profile picture or name in the top-right corner → **Sign out**. Then sign back in. This sometimes resolves manifest errors without any further steps.

**Step 2 — Clear the Office Web Add-in host cache**

!!! warning "For more confident Mac users"
    This step involves deleting files from hidden system folders. If you are not comfortable doing this, skip to Step 3.

    Open Terminal and run:
    ```bash
    rm -rf ~/Library/Containers/com.Microsoft.OsfWebHost/Data/*
    ```
    Then fully quit and relaunch Excel or PowerPoint.

**Step 3 — Reinstall the add-in from Get Add-ins**

1. Open Excel or PowerPoint
2. Go to **Insert** → **Get Add-ins**
3. Search for **Claude** and reinstall or re-enable it
4. Sign in when prompted

This step must be repeated after each Cowork session.

**Step 4 — Use Office Online as a working alternative**

Excel Online and PowerPoint Online at [office.com](https://office.com) are not affected by this bug. If you need the Claude add-in while using Cowork, the browser-based Office apps work reliably and require no reinstallation.

✅ **Add-in working again? You're done — but expect to repeat Step 3 after each session.**

❌ **Seeing a "Schema validation", "Redirect-URI", or "Extra inputs" error when signing in to the add-in?**

These are server-side API errors that cannot be fixed locally. See the known issues page for a full explanation and your options.

👉 [Known server bugs and OS limits — macOS](macos-known-issues.md)

---

#### 🏢 Work Mac (managed by your employer)

If your organization controls Microsoft 365 add-in deployment, you will not be able to reinstall the Claude add-in yourself using Get Add-ins. Your IT department or Microsoft 365 administrator needs to re-deploy the add-in from the Microsoft 365 Admin Center.

!!! note "For IT departments"
    This is a confirmed bug in Claude Cowork on macOS. After each Cowork session, the Claude Web Add-in manifest for PowerPoint is removed and the Excel add-in's execution context is corrupted. The only confirmed workaround is to re-deploy the Claude add-in from the Microsoft 365 Admin Center after each affected session. Microsoft moderators also recommend clearing `~/Library/Containers/com.Microsoft.OsfWebHost/Data/` on the affected device as a supplementary step. This is being tracked as an Anthropic engineering issue.

    **Office Online (office.com) is not affected** and can be used in the meantime.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
