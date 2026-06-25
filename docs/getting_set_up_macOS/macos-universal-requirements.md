# macOS Universal Requirements — Check These First

Before troubleshooting any specific error, work through this checklist. The majority of macOS Cowork readiness failures trace back to one of these five things.

**Work through each check in order.** After any change, run the Cowork Readiness Checker again before continuing.

---

## Check 1 — Verify your processor

Claude Cowork requires **Apple Silicon** — an M1, M2, M3, or M4 chip. Intel-based Macs are not supported and the readiness checker will permanently fail on them.

**How to check:**

1. Click the **Apple menu** (top-left corner of your screen)
2. Select **About This Mac**
3. Look for **Chip** or **Processor**

| What it says | What it means |
|---|---|
| Apple M1, M2, M3, or M4 | ✅ Your chip is supported |
| Intel Core i5 / i7 / i9 | ❌ This Mac cannot run Cowork |

!!! warning "Intel Mac"
    If your Mac has an Intel processor, no software update or settings change will enable Cowork. This is a hardware limitation. Cowork requires Apple Silicon.

---

## Check 2 — Verify your macOS version

Cowork requires **macOS Sonoma (14.0) or later**.

**How to check:**

1. Click the **Apple menu**
2. Select **About This Mac**
3. Look at the macOS version listed at the top

| What it says | What it means |
|---|---|
| macOS Sonoma (14.x) | ✅ Supported |
| macOS Sequoia (15.x) | ✅ Supported |
| macOS Tahoe (26.x) | ✅ Supported |
| macOS Ventura (13.x) or earlier | ❌ Needs to be updated |

**To update macOS:**

Go to **System Settings → General → Software Update** and install any available updates.

!!! note "macOS Tahoe and Golden Gate"
    Cowork has been tested on macOS Sonoma, Sequoia, and Tahoe. macOS Golden Gate was announced at WWDC June 2026 and has not yet been tested with Cowork.

---

## Check 3 — Verify available storage

Cowork's virtual machine requires at least **10GB of free disk space** to run securely.

**How to check:**

1. Click the **Apple menu**
2. Select **About This Mac**
3. Click the **Storage** tab

If free space is below 10GB, delete files or move them to external storage before proceeding.

---

## Check 4 — Verify available memory

Cowork requires a minimum of **8GB of RAM**. If your Mac's memory is maxed out by other applications, the virtual machine may fail to start.

**How to check:**

1. Press **Command + Spacebar** to open Spotlight
2. Type `Activity Monitor` and open it
3. Click the **Memory** tab
4. Look at the **Memory Pressure** indicator at the bottom

| Memory Pressure color | What it means |
|---|---|
| 🟢 Green | ✅ Sufficient memory available |
| 🟡 Yellow | ⚠️ Memory is under moderate pressure — close some apps |
| 🔴 Red | ❌ Memory is critically low — close heavy apps before running Cowork |

**To close heavy applications:**

Press **Command + Option + Escape**, select the app using the most memory, and click **Force Quit**.

Restart your Mac after clearing memory to refresh system resources.

---

## Check 5 — Move Claude Desktop to your Applications folder

This is a commonly missed step. If you downloaded Claude Desktop and ran it directly from your **Downloads** folder without moving it first, macOS will trigger a security feature that breaks Cowork's local sandbox.

**Claude Desktop must be in your Applications folder.**

**How to move it:**

1. Open **Finder**
2. Click **Downloads** in the sidebar
3. Locate the **Claude** app
4. Open a second Finder window and click **Applications** in the sidebar
5. Drag the Claude app from Downloads into Applications
6. Open Applications and double-click Claude to launch it — macOS may ask for your admin password, click **Open** to proceed
7. Once confirmed, delete the original file from Downloads to keep things tidy

!!! note "Why does this matter?"
    Running an app directly from Downloads triggers a macOS security feature called Gatekeeper quarantine. This silently blocks the background processes Cowork needs to run — without always showing a clear error message.

---

## All five checks done — still seeing errors?

If your Mac meets all the requirements above and the readiness checker is still failing, the next step depends on whether this is a personal Mac or a work Mac.

👉 [Fix: Personal Mac troubleshooting](macos-personal-mac-fixes.md)

👉 [Fix: Managed Mac — contact IT](macos-managed-mac-it.md)

---

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0 · June 2026*
