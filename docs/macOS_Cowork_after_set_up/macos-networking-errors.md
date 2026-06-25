# Fix: Workspace Connection and Sandbox Errors — macOS

You successfully launched Claude Cowork, but your workspace disconnected, threw a virtual machine error, or failed to load plugins. Because Cowork runs inside a local macOS virtualization sandbox, it requires a stable workspace disk image and clear network pathways. If your Mac runs low on storage, a security extension blocks a network request, or the session image becomes corrupted, the workspace will crash or fail to load.

Find your error below.

---

## Which error are you seeing?

### 🔴 "CLI output was not valid JSON" or "sandbox-helper: host share not mounted"

The workspace session image has become corrupted or locked, preventing Cowork from mounting your project folders.

👉 [Jump to Fix 1](#fix-1-corrupted-workspace-session-image)

---

### 🔴 "sandboxVirtualization error: VM failed to start" or "ENOSPC: no space left on device"

The virtualization sandbox cannot boot — usually because your Mac has run out of disk space.

👉 [Jump to Fix 2](#fix-2-vm-failed-to-start)

---

### 🔴 Plugin Marketplace fails to load, shows a DNS error, or returns HTTP 404

Cowork cannot reach the plugin server — usually due to a network filter or browser extension blocking the request.

👉 [Jump to Fix 3](#fix-3-plugin-marketplace-fails-to-load)

---

## Fix 1 — Corrupted Workspace Session Image

**Error:** `"CLI output was not valid JSON"` or `"sandbox-helper: host share not mounted"`

The workspace session image (`sessiondata.img`) has become corrupted or is stuck in a hung state. This prevents Cowork's internal file-sharing engine from mounting your Mac project folders into the workspace environment.

!!! warning "The \"Reinstall workspace\" button will not fix this"
    Claude Desktop has a built-in **Reinstall workspace** button, and it is the natural first thing to try — but it will not resolve this error. By design, this button explicitly preserves `sessiondata.img` and `rootfs.img.zst`, the two files most likely to be corrupted. Clicking it will appear to reinstall without actually clearing the problem. Skip the button and follow the steps below instead.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

The fix renames the corrupted session image to a backup file. Cowork will then automatically generate a fresh, clean image on next launch.

**Step 1 — Quit Claude Desktop**

Press **Command + Q** while Claude is the active app to quit it fully. Alternatively, right-click the Claude icon in the Dock and select **Quit**.

**Step 2 — Open Terminal**

Press **Command + Space** to open Spotlight, type `Terminal`, and press **Enter**.

**Step 3 — Rename the corrupted session image**

Run this command exactly as written:

```bash
mv ~/Library/Application\ Support/Claude/vm_bundles/claudevm.bundle/sessiondata.img ~/Library/Application\ Support/Claude/vm_bundles/claudevm.bundle/sessiondata.img.bak
```

This renames the corrupted image rather than deleting it, keeping it as a safety backup.

**Step 4 — Relaunch Claude Desktop**

Open Claude Desktop. It will detect the missing session image and automatically generate a fresh one.

✅ **Error gone? You're done.**

❌ **Still seeing the error?**

If Claude Desktop cannot generate a new session image, the next step is to clear any remaining corrupted app data.

👉 [Fix: Personal Mac troubleshooting](../getting_set_up_macOS/macos-personal-mac-fixes.md)

If that does not resolve it, contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

The Terminal steps above apply to work Macs as well. However, if your employer's security software restricts file operations in your Library folder, the `mv` command may return a permissions error.

If that happens, your IT department will need to temporarily lift the restriction so the corrupted image can be cleared.

!!! note "For IT departments"
    Claude Cowork stores its workspace session image at:
    `~/Library/Application Support/Claude/vm_bundles/claudevm.bundle/sessiondata.img`

    This is a per-user path in the user's local Library. The fix requires the user to rename or delete this file so Cowork can regenerate it. If your MDM or security policy restricts writes to `~/Library/Application Support/`, a temporary exception for this path is needed.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

## Fix 2 — VM Failed to Start

**Error:** `"sandboxVirtualization error: VM failed to start"` or `"ENOSPC: no space left on device"`

The macOS virtualization sandbox cannot boot. This almost always happens when your Mac has fallen below 10GB of free disk space — Cowork needs this headroom to run the workspace environment. It can also occur if your macOS version is no longer supported.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

**Step 1 — Check your available storage**

Click the **Apple menu** → **System Settings** → **General** → **Storage**.

Verify you have at least **10GB of free space**. If not, delete large files or applications before continuing.

**Step 2 — Verify your macOS version**

Click the **Apple menu** → **About This Mac**.

Cowork requires **macOS Sonoma (14.0) or later**. If your version is older, go to **System Settings → General → Software Update** and install available updates.

**Step 3 — Restart your Mac**

Restarting clears temporary locked files that may be consuming disk space or blocking the virtualization engine.

**Step 4 — Relaunch Claude Desktop and try opening Cowork**

✅ **Workspace launched? You're done.**

❌ **Still failing to start?**

If you have at least 10GB free and a supported macOS version but the VM still won't start, check that your Mac's hardware meets Cowork's requirements.

👉 [macOS universal requirements](../getting_set_up_macOS/macos-universal-requirements.md)

---

#### 🏢 Work Mac (managed by your employer)

The steps above apply to work Macs. However, if your Mac's storage is heavily managed — for example, if large folders are redirected to a network share — you may not have full visibility into what is consuming local disk space.

If clearing space is outside your control, contact your IT department and ask them to verify that at least 10GB of local disk space is available for Cowork's use.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

## Fix 3 — Plugin Marketplace Fails to Load

**Symptoms — any of these may appear:**

- The Plugin Marketplace shows a blank screen or spins indefinitely
- A DNS error or HTTP 404 appears when trying to reach `plugins.claude.ai`
- Plugins fail to install even after the page loads

Cowork's Plugin Marketplace requires a clear network path to `plugins.claude.ai`. This can be blocked by browser extensions that inject scripts into web pages, or by macOS network filters that intercept outbound connections.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

**Work through these steps in order. After each step, relaunch the Plugin Marketplace and check whether it loads. Stop as soon as it works.**

**Step 1 — Disable browser extensions temporarily**

If you are accessing the Plugin Marketplace through a web browser, disable any extensions that modify or intercept page content — particularly coupon finders, ad blockers, or script injectors. Then refresh the page.

**Step 2 — Check for macOS network filters**

If the marketplace is showing a 404 error inside the Claude Desktop app itself, a macOS-level network filter may be blocking `plugins.claude.ai`. Common culprits include:

- **Little Snitch** — check its rules for any block on `plugins.claude.ai` or `claude.ai` domains
- **LuLu** — check for a pending connection alert or an active block rule for Claude Desktop
- **Custom VPN DNS profiles** — if you have a VPN active with custom DNS settings, try disconnecting and retrying

Temporarily disable any of the above and test whether the Marketplace loads.

**Step 3 — Quit and relaunch Claude Desktop**

Press **Command + Q** to fully quit Claude Desktop, then reopen it. This flushes the app's internal DNS cache.

✅ **Marketplace loading? You're done.**

❌ **Still not loading?**

If none of the above resolves it, the issue may be on Anthropic's side or specific to your network configuration. Contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

Corporate firewalls and web proxies may block `plugins.claude.ai` at the network level. This is not something you can fix yourself — your IT department needs to whitelist the domain.

!!! note "For IT departments"
    Claude Cowork's Plugin Marketplace requires outbound HTTPS access to `plugins.claude.ai`. If your corporate firewall, proxy, or DNS filter is blocking this domain, Claude Desktop will show a DNS error or HTTP 404 in the Plugin Marketplace panel. The fix is to add `plugins.claude.ai` to your network allowlist.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
