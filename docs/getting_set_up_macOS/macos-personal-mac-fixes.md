# Fix: Personal Mac Troubleshooting

You've confirmed your Mac meets the universal requirements but the Cowork Readiness Checker is still failing. If you own and manage your own Mac, work through the fixes below in order.

**After each fix, run the Cowork Readiness Checker again. Stop as soon as the errors are gone.**

---

## Fix 1 — Approve Gatekeeper blocks

Apple's built-in security feature, **Gatekeeper**, may be silently blocking the background scripts Cowork needs to run. This is one of the most common causes of readiness failures on personal Macs.

**Symptoms — any of these may appear:**

- A dialog saying *"Apple cannot check it for malicious software"* or *"the developer cannot be verified"*
- The app opens briefly and then quits silently
- No error message — just a bounce in the Dock and nothing happens

**Fix:**

1. Open **System Settings**
2. Go to **Privacy & Security**
3. Scroll down to the **Security** section
4. If you see a message about Claude being blocked, click **Allow Anyway**
5. You may be asked to enter your Mac's admin password

**Run the Cowork Readiness Checker again.**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Fix 2.**

---

## Fix 2 — Check folder permissions

macOS strictly controls which applications can access your files and folders. If Cowork can't connect to your workspace, it may be missing the folder access permissions it needs.

**Fix:**

1. Open **System Settings**
2. Go to **Privacy & Security → Files and Folders**
3. Find **Claude** in the list
4. Make sure all toggles next to Claude are switched **ON**

**Run the Cowork Readiness Checker again.**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Fix 3.**

---

## Fix 3 — Clear corrupted app data

!!! warning "For more confident Mac users"
    This fix involves navigating to a hidden system folder. If you're not comfortable doing this, skip to Fix 4 and come back to this one with help from a technically confident friend or colleague if needed.

A corrupted cache can cause Cowork's setup script to fail or the app to spin endlessly without launching.

**Fix:**

1. Fully quit Claude — press **Command + Q** while Claude is the active app, or right-click the Claude icon in the Dock and select **Quit**
2. Open **Finder**
3. Hold the **Option** key on your keyboard
4. Click **Go** in the menu bar at the top of your screen — you will see a hidden **Library** option appear
5. Click **Library**
6. Navigate to **Application Support → Claude**
7. Delete the cache folders inside

**Run the Cowork Readiness Checker again.**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Fix 4.**

---

## Fix 4 — Force restart the background service

If the Cowork virtual machine is stuck and refusing to boot, you can force-stop the stuck processes and restart them. This is done using the macOS Terminal.

!!! warning "For more confident Mac users"
    Terminal is a text-based tool that sends direct commands to your Mac. You only need to type exactly what is shown below — do not modify the commands.

**Fix:**

1. Press **Command + Spacebar** to open Spotlight
2. Type `Terminal` and open it
3. Type the following command exactly and press **Enter:**

```
pkill -9 -f "claude"
```

4. Wait a few seconds, then type the following command and press **Enter:**

```
open -a "Claude"
```

5. Claude will relaunch with a fresh background service

**Run the Cowork Readiness Checker again.**

✅ **Errors gone? You're done — ready to install Cowork!**

---

## Still not working?

If you've worked through all four fixes and the readiness checker is still failing, the issue may be related to corporate security policies — even if you believe this is a personal Mac. Some security software installed by a previous employer or bundled with other applications can behave like managed device policies.

👉 [Fix: Managed Mac — contact IT](macos-managed-mac-it.md)

👉 [Back to macOS Checker Errors hub](macos-checker-errors.md)

---

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0 · June 2026*
