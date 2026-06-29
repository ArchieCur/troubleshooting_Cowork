# Fix: Scheduled Tasks Failing or Not Firing — Windows

You set up a scheduled task in Cowork, but it failed to create, silently stopped running, or triggered an error. Because Cowork tasks rely on strict Windows file linking rules and local background processes, your scheduled work can break if your storage is split across multiple drives, your Documents folder is synced to the cloud or a network share, or your computer goes to sleep at the wrong time.

Find your error below.

!!! note "New to PowerShell?"
    Some fixes on this page require PowerShell. If you've never used it before, [start here for a quick, friendly primer](new-to-powershell.md) before you begin.

---

## Which error are you seeing?

### 🔴 "EXDEV: cross-device link not permitted" — or tasks fail silently on creation

Cowork cannot create the file link it needs because your app and your Documents folder are on different drives.

👉 [Jump to Fix 1](#fix-1-cross-device-link-error)

---

### 🔴 "Failed to create scheduled task. You can try again."

Cowork cannot reach its task storage folder because your Documents folder is synced to the cloud or redirected to a network location.

👉 [Jump to Fix 2](#fix-2-task-creation-fails)

---

### 🔴 Task was created but did not run at the scheduled time

Cowork's background scheduler missed its trigger — usually because the computer slept, the app was closed, or the Cowork tab lost focus.

👉 [Jump to Fix 3](#fix-3-task-did-not-run-at-scheduled-time)

---

## Fix 1 — Cross-Device Link Error

**Error:** `"EXDEV: cross-device link not permitted"` or tasks fail silently when you try to create them

Cowork uses a Windows feature called a hard link to connect tasks to your workspace. Hard links cannot cross from one drive to another. This error appears when Windows is set to save new apps to your D: drive (or another secondary drive) instead of your primary C: drive, putting Claude Desktop on a different drive from your Documents folder.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

**Work through these steps in order. Stop as soon as scheduled tasks work.**

**Step 1 — Open Storage Settings**

Go to **Settings** → **System** → **Storage** → **Advanced storage settings** → **Where new content is saved**.

**Step 2 — Change the app installation drive to C:**

Find the **"New apps will save to"** dropdown and change it to your **C:** drive.

**Step 3 — Uninstall Claude Desktop**

Go to **Settings** → **Apps** → **Installed apps**, find **Claude**, and click **Uninstall**.

**Step 4 — Reinstall Claude Desktop**

Download and install the latest version of Claude Desktop. It will now install to the correct drive.

**Step 5 — Try creating a scheduled task again**

✅ **Task created successfully? You're done.**

❌ **Still failing?**

If the error persists after reinstalling, your Documents folder may be synced or redirected rather than stored locally — this is a separate issue covered in Fix 2.

👉 [Jump to Fix 2](#fix-2-task-creation-fails)

---

#### 🏢 Work computer (managed by your employer)

Your IT department may control where applications are installed on your machine. If the **"New apps will save to"** setting is greyed out and cannot be changed, your IT department has locked this setting via Group Policy.

Contact your IT department and ask them to allow Claude Desktop to install on the C: drive, or to install it on your behalf.

👉 [IT email template: Scheduled Tasks & Storage](../support/IT_support_email.md)

---

## Fix 2 — Task Creation Fails

**Error:** `"Failed to create scheduled task. You can try again."`

Cowork saves scheduled task data to a fixed path inside your Documents folder (`~/Documents/Claude/Scheduled/`). If that folder is synced to a cloud service or redirected to a corporate network location, the local scheduler cannot write to it — and task creation fails.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

The most common cause on personal computers is **OneDrive syncing your Documents folder**, which is the Windows default on many machines. The fix is to restore Documents to a real local folder by turning off OneDrive backup for that folder only. This is safe and reversible — your existing files stay on your device.

**Step 1 — Open OneDrive Settings**

Right-click the **OneDrive cloud icon** in the Windows System Tray (near the clock) and select **Settings**.

**Step 2 — Go to Sync and backup**

Select the **Sync and backup** tab → click **Manage backup**.

**Step 3 — Turn off Documents backup**

Find **Documents** in the list and toggle it **Off**.

**Step 4 — Keep your files on this device**

When OneDrive asks what to do with your existing files, select **Keep files on this device**. Your files remain exactly where they are — OneDrive simply stops managing the folder going forward.

**Step 5 — Try creating a scheduled task again**

✅ **Task created successfully? You're done.**

❌ **Still failing?**

If your Documents folder is not synced to OneDrive but the error persists, check whether it has a cloud or network icon in File Explorer. If so, another sync tool (Google Drive, Dropbox, or a corporate tool) may be managing it — that tool's backup settings will need to be adjusted the same way.

---

#### 🏢 Work computer (managed by your employer)

!!! warning "This cannot be fixed locally"
    If your employer uses Group Policy to redirect your Documents folder to a corporate network share or a managed OneDrive, this is a known limitation of Cowork. The task storage path is hardcoded and cannot be changed or bypassed by the user.

    **To use scheduled tasks, you need a computer where the Documents folder is stored locally on the main drive.**

Your options are:

- **Contact IT** and ask whether the Documents folder redirection policy can be adjusted on your device, or whether a local exception is possible.
- **Use a personal computer** for Cowork sessions that require scheduled tasks.

👉 [IT email template: Scheduled Tasks & Storage](../support/IT_support_email.md)

---

## Fix 3 — Task Did Not Run at Scheduled Time

**Symptom:** You created a scheduled task and it appeared to set up correctly, but it did not run at the time you specified.

Cowork's scheduler depends on a local background process running on your machine. If your computer sleeps, the app closes, or the Cowork tab loses focus before the scheduled time, the trigger will be missed.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

Work through each check below. After each change, reschedule and test the task.

**Check 1 — Keep Claude Desktop open and running**

Cowork's scheduler only runs while Claude Desktop is open. The app must remain open in the background during the scheduled time — do not close it or let it fully quit.

**Check 2 — Prevent your computer from sleeping**

1. Go to **Settings** → **System** → **Power & Sleep**
2. Under **Sleep**, set **"When plugged in, PC goes to sleep after"** to **Never**
3. If you are on a laptop, also set **"When on battery power, PC goes to sleep after"** to a duration longer than your task's scheduled window

**Check 3 — Keep the Cowork tab in focus**

!!! note "Known bug"
    There is a known issue where scheduled tasks may not fire unless the Cowork tab is the actively focused view on your screen at the time the task is set to run. Before stepping away from your computer, click into the Cowork tab to ensure it has focus.

**Check 4 — Verify your timezone**

Confirm the task was not accidentally scheduled in UTC rather than your local timezone. Check the scheduled time shown in Cowork against your local clock.

✅ **Task running correctly? You're done.**

❌ **Tasks still not firing while the app is active?**

If you have confirmed the app is open, the computer is awake, and the Cowork tab is focused — but tasks still silently fail to run — Cowork's background scheduler may be in a stuck state that requires Anthropic's support team to investigate.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work computer (managed by your employer)

The checks above apply to work computers as well. However, note that corporate power management policies may override your sleep settings — if your computer is forced to sleep by an IT policy, the local Power & Sleep settings cannot override it.

If you believe a corporate power policy is causing missed tasks, contact your IT department and ask whether an exception can be made for your device.

👉 [IT email template: Scheduled Tasks & Storage](../support/IT_support_email.md)

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
