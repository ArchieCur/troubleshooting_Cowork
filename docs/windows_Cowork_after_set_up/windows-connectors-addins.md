# Fix: Connectors, Plugins, and Office Add-ins — Windows

You launched a Cowork session, but your connected tools are missing, the MCP registry throws a red error banner, or your Excel and PowerPoint add-ins have crashed or disappeared. Because Claude Desktop updates automatically in the background, the internal tool registry can fall out of sync with your workspace. Additionally, Cowork's visual plugin marketplace and the command-line tool track installations separately, which can cause plugins to disappear when you restart the app.

Find your error below.

!!! note "New to PowerShell?"
    Some fixes on this page require PowerShell. If you've never used it before, [start here for a quick, friendly primer](new-to-powershell.md) before you begin.

---

## Which error are you seeing?

### 🔴 "Could not connect to MCP server mcp-registry" or "Could not load connectors directory"

A background update caused the internal tool registry to lose sync with your workspace.

👉 [Jump to Fix 1](#fix-1-mcp-registry-out-of-sync)

---

### 🔴 Excel or PowerPoint add-in disappeared — or shows "Microsoft 365 has been configured to prevent individual acquisition"

A known Cowork bug is removing or breaking the Microsoft 365 Claude add-ins after each session.

👉 [Jump to Fix 2](#fix-2-office-add-in-disappears-after-cowork-session)

---

### 🔴 Plugins disappear from the Cowork tab every time you restart the app

Plugins installed through the visual marketplace are not persisting between app restarts.

👉 [Jump to Fix 3](#fix-3-plugins-disappear-after-restarting)

---

## Fix 1 — MCP Registry Out of Sync

**Error:** `"Could not connect to MCP server mcp-registry"` or `"Could not load connectors directory"`

A background auto-update to Claude Desktop caused the internal tool registry to fall out of sync with your workspace. Because this registry handles tool discovery, all of your MCP tools become invisible to Cowork — even though they are technically still installed and functioning.

!!! warning "Do not use Remove-Item to delete the vm_bundles folder"
    Some online sources suggest running `Remove-Item -Recurse -Force` on the `vm_bundles` folder to fix this issue. **Do not do this.** That folder contains your active Cowork workspace state, including ongoing terminal sessions, uncommitted tasks, and local plugin data. Deleting it causes immediate and permanent loss of that data. The steps below rename the folder as a backup instead, which is safe and reversible.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

**Step 1 — Exit Claude Desktop completely**

Right-click the Claude icon in the Windows System Tray (near the clock) → **Exit**.

**Step 2 — Open PowerShell**

Click Start, type `powershell`, and click **Windows PowerShell**. Standard (non-administrator) PowerShell is sufficient for this fix.

**Step 3 — Rename the out-of-sync registry folders**

Run both commands as written. This renames the folders to backup copies rather than deleting them, so nothing is permanently lost.

```powershell
Rename-Item -Path "$env:APPDATA\Claude\vm_bundles" -NewName "vm_bundles.bak" -ErrorAction SilentlyContinue
Rename-Item -Path "$env:APPDATA\Claude\claude-code-vm" -NewName "claude-code-vm.bak" -ErrorAction SilentlyContinue
```

!!! note "If you see a 'destination already exists' error"
    A backup from a previous run of this fix is still in place. Open File Explorer, navigate to `%APPDATA%\Claude`, and delete the existing `vm_bundles.bak` and `claude-code-vm.bak` folders. Then run the commands above again.

**Step 4 — Reopen Claude Desktop**

Claude Desktop will detect the missing folders and re-download a fresh workspace bundle, then reconnect to the MCP registry.

✅ **MCP tools back? You're done.**

❌ **Registry banner gone but tools still won't authenticate?**

This may be a known Anthropic server-side issue with OAuth scopes. Contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work computer (managed by your employer)

The PowerShell steps above apply to work computers as well. Standard PowerShell access (non-administrator) is enough for this fix since it only touches your personal AppData folder.

If the rename fails because your AppData folder has been redirected to a network location by a Group Policy, your IT department will need to locate and rename the folders at the redirected path.

!!! note "For IT departments"
    Claude Cowork's MCP tool registry is stored in two folders:
    - `%APPDATA%\Claude\vm_bundles`
    - `%APPDATA%\Claude\claude-code-vm`

    If AppData has been redirected via Group Policy, these folders will be at the redirected network path rather than the local path above. Renaming both folders (not deleting) and relaunching Claude Desktop forces a clean registry rebuild.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

## Fix 2 — Office Add-in Disappears After Cowork Session

**Symptoms — any of these may appear after a Cowork session ends:**

- The Claude add-in disappears from the PowerPoint ribbon entirely
- The Claude add-in remains visible in Excel but clicking it produces an execution policy error
- An error says `"Microsoft 365 has been configured to prevent individual acquisition"`

!!! warning "This is a confirmed, reproducible Cowork bug"
    Cowork's Windows virtualization layer interferes with Microsoft Office Web Add-in registration. After a Cowork session closes, it removes or corrupts the Claude add-in manifests for PowerPoint and Excel. This happens on every session and affects any new Office file, not just files Cowork touched.

    **There is no permanent local fix.** The add-ins must be re-enabled manually after each Cowork session until Anthropic resolves this at the application level.

    **What does not fix this:** Reinstalling Office, reinstalling Claude Desktop, or clearing general app caches alone will not prevent the bug from recurring.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

**Workaround — Re-enable the add-in before each session**

1. Open Excel or PowerPoint
2. Go to **Insert** → **Get Add-ins**
3. Search for **Claude** and reinstall or re-enable it
4. Sign in when prompted

This needs to be repeated after each Cowork session until Anthropic fixes the underlying bug.

**Alternative — Use Office Online**

Excel Online and PowerPoint Online at office.com are not affected by this bug. If you need the Claude add-in while Cowork is active, using the browser-based Office apps is a reliable workaround that requires no re-installation.

✅ **Add-in working again? You're done — but expect to repeat this after each session.**

❌ **Seeing a "Schema validation", "Redirect-URI", or "Extra inputs" error when trying to sign in to the add-in?**

These are server-side API errors that cannot be fixed locally. See the known issues page for a full explanation and your options.

👉 [Known server bugs and OS limits — Windows](windows-known-issues.md)

---

#### 🏢 Work computer (managed by your employer)

The error `"Microsoft 365 has been configured to prevent individual acquisition"` means your IT department has locked down add-in installation from the public Microsoft store. You cannot install or reinstall the Claude add-in yourself.

Your options are:

- **Contact IT** and ask them to re-deploy the Claude Microsoft 365 add-in to your device from the Microsoft 365 Admin Center — this is the only confirmed workaround for managed environments.
- **Use Office Online** (office.com) — the browser-based Excel and PowerPoint are not affected by this bug and do not require IT intervention.

!!! note "For IT departments"
    This is a confirmed bug in Claude Cowork on Windows. After each Cowork session, the Claude Web Add-in manifest for PowerPoint is removed and the Excel add-in manifest is corrupted, causing an execution policy failure. The only confirmed workaround is to re-deploy the add-in from the Microsoft 365 Admin Center after each affected session. This is being tracked as an Anthropic engineering issue.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

## Fix 3 — Plugins Disappear After Restarting

**Symptom:** Plugins you installed through the Cowork marketplace tab are gone the next time you open Claude Desktop.

!!! warning "This is a known sync bug"
    Cowork's visual plugin marketplace and the underlying Claude Code command-line tool maintain separate, unsynchronized installation states. Plugins installed through the visual "Personal" marketplace tab are currently not persisted between app restarts.

There is no permanent fix for this yet. Two workarounds are available depending on your setup.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

**Workaround 1 — Reinstall from the marketplace tab each session**

The quickest option: each time you open Claude Desktop, go to the Cowork marketplace tab and reinstall the plugins you need. This takes seconds but must be repeated every session.

**Workaround 2 — Use a personal marketplace with ZIP upload**

This is a more durable option that avoids the sync issue entirely. Instead of using the shared marketplace, you create your own personal marketplace and upload your plugins as `.zip` files through the admin UI. Plugins added this way are not subject to the restart sync bug.

This feature is documented by Anthropic — see the [Claude Desktop Extensions guide](https://www.anthropic.com/engineering/desktop-extensions) for how to set up a personal marketplace and use the manual upload option.

!!! note
    The ZIP upload approach requires initial setup time but eliminates the need to reinstall after every restart. It is the recommended path if you rely on specific plugins regularly.

✅ **Plugins staying put? You're done.**

❌ **Plugins still disappearing even after the ZIP upload workaround?**

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work computer (managed by your employer)

If your organization manages Claude Desktop centrally, individual plugin installation may be restricted. Contact your Anthropic account administrator to ask whether plugins can be deployed to your workspace from the organizational marketplace.

If you do have access to install plugins yourself, both workarounds above apply.

👉 [IT email template: Connectors & Add-ins](../support/IT_support_email.md)

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
