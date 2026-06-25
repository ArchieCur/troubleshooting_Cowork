# Fix: Scheduled Tasks Failing or Not Firing — macOS

You set up a scheduled task in Cowork, but it failed to create, missed its scheduled time, or threw a cryptic "VirtioFS mount error." Because Cowork tasks rely on local background processes and a specific folder path inside your Documents folder, your scheduled work can break if macOS privacy settings block access to your files, or if your Mac goes to sleep before the task runs.

Find your error below.

---

## Which error are you seeing?

### 🔴 "VirtioFS mount error" — or tasks fail instantly when you try to create them

macOS privacy settings may be blocking Claude Desktop from accessing your Documents folder.

👉 [Jump to Fix 1](#fix-1-documents-folder-permission-denied)

---

### 🔴 Task was created but did not run at the scheduled time

Cowork's background scheduler missed its trigger — usually because the Mac slept, the app was closed, or the Cowork tab lost focus.

👉 [Jump to Fix 2](#fix-2-task-did-not-run-at-scheduled-time)

---

## Fix 1 — Documents Folder Permission Denied

**Error:** `"VirtioFS mount error"` or tasks fail instantly on creation

Cowork saves scheduled task data to a fixed path inside your Mac's Documents folder (`~/Documents/Claude/Scheduled/`). Apple's privacy system — called TCC (Transparency, Consent, and Control) — may have silently blocked Claude Desktop from reading or writing to your Documents folder. When access is blocked, the internal file-sharing system (VirtioFS) crashes, causing this error.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

**Step 1 — Open System Settings**

Click the **Apple menu** (top-left corner of your screen) → **System Settings**.

**Step 2 — Go to Privacy & Security → Files and Folders**

In the left sidebar, click **Privacy & Security**. Scroll down and click **Files and Folders**.

**Step 3 — Grant Claude access to your Documents folder**

Find **Claude** in the list of applications. Click the arrow to expand it, then make sure the toggle next to **Documents Folder** is turned **on**.

!!! note "Claude not in the list?"
    If Claude doesn't appear in Files and Folders, it hasn't requested Documents access yet. Try creating a scheduled task first — macOS should prompt you to allow access. If no prompt appears, try removing Claude Desktop and reinstalling it, which resets its permission request.

**Step 4 — Restart Claude Desktop**

Press **Command + Q** while Claude is the active app to quit it fully, then reopen it.

**Step 5 — Try creating a scheduled task again**

✅ **Task created successfully? You're done.**

❌ **Still seeing the error?**

If the toggle was already on or re-enabling it didn't help, the issue may be deeper than a simple permission toggle. Contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

On a Mac managed by your employer, your IT department controls application permissions through Mobile Device Management (MDM). The **Files and Folders** toggle for Claude may not appear at all, or may be greyed out and cannot be changed by you.

Your IT department needs to whitelist Claude Desktop's access to the local Documents folder in your MDM configuration.

!!! note "For IT departments"
    Claude Cowork requires read and write access to `~/Documents/Claude/Scheduled/` to create and manage scheduled tasks. This access is governed by macOS TCC. On a managed Mac, Claude Desktop's entitlement to access the Documents folder must be explicitly granted via your MDM profile (e.g., Jamf, Mosyle, or Kandji) using a Privacy Preferences Policy Control (PPPC) payload.

👉 [IT email template: Scheduled Tasks & Storage](../support/IT_support_email.md)

---

## Fix 2 — Task Did Not Run at Scheduled Time

**Symptom:** You created a scheduled task and it appeared to set up correctly, but it did not run at the time you specified.

Cowork's scheduler depends on a local background process running on your Mac. If your Mac sleeps, the app closes, or the Cowork tab loses focus before the scheduled time, the trigger will be missed.

---

### Is this your personal Mac or a work Mac?

#### 🏠 Personal Mac

Work through each check below. After each change, reschedule and test the task.

**Check 1 — Keep Claude Desktop open and running**

Cowork's scheduler only runs while Claude Desktop is open. The app must remain running in the background during the scheduled time — do not close it or quit it before the task fires.

**Check 2 — Prevent your Mac from sleeping**

!!! warning "Battery and power impact"
    Preventing sleep keeps your Mac running at full power. As Apple notes: *"Keep in mind that delaying, preventing, or allowing disruption of sleep may increase power consumption."* If you are on a laptop, plug your Mac into power before leaving it awake for a scheduled task.

Choose the path that matches your macOS version:

**macOS Sonoma (14) and later — Battery path:**

1. Go to **System Settings** → **Battery** → **Options**
2. Turn on **"Prevent automatic sleeping on power adapter when the display is off"**

**macOS Sequoia (15) and Tahoe (26) — alternative Displays path:**

1. Go to **System Settings** → **Displays** → **Advanced**
2. Turn on **"Prevent automatic sleeping on power adapter when the display is off"**

!!! note
    On Sequoia and Tahoe, both paths control the same setting. Use whichever you find first.

**Check 3 — Keep the Cowork tab in focus**

!!! note "Known bug"
    There is a known issue where scheduled tasks may not fire unless the Cowork tab is the actively focused view on your screen at the time the task is set to run. Before stepping away from your Mac, click into the Cowork tab to make sure it has focus.

**Check 4 — Verify your timezone**

Confirm the task was not accidentally scheduled in UTC rather than your local timezone. Check the scheduled time shown in Cowork against your Mac's clock.

✅ **Task running correctly? You're done.**

❌ **Tasks still not firing while the app is active?**

If your Mac is awake, Claude Desktop is open, and the Cowork tab is focused — but tasks still silently fail to run — Cowork's background scheduler may be in a stuck state that requires Anthropic's support team to investigate.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work Mac (managed by your employer)

The checks above apply to work Macs as well. However, your IT department may enforce a corporate sleep or power policy that overrides your System Settings — if your Mac is required to sleep after a set period of inactivity, you cannot override that locally.

If you believe a corporate power policy is causing missed tasks, contact your IT department and ask whether a sleep exception can be made for your device during scheduled task windows.

👉 [IT email template: Scheduled Tasks & Storage](../support/IT_support_email.md)

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
