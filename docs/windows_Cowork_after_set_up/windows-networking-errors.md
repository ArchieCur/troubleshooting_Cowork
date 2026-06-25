# Fix: Workspace Connection and Sandbox Errors — Windows

You successfully launched Claude Cowork, but during your session the workspace disconnected, threw a network timeout, or crashed with an unexpected file-sharing error. Because Cowork operates inside an isolated local virtual environment on Windows, it relies on persistent system network routing and stable disk images. If a VPN reconnects, Windows updates background settings, or a file handle locks up, the sandbox will lose contact with Claude.

Find your error below.

---

## Which error are you seeing?

### 🔴 "The Claude API cannot be reached from Claude's workspace"

The private network Cowork uses to reach the Anthropic API has lost its DNS configuration or routing rule.

👉 [Jump to Fix 1](#fix-1-api-cannot-be-reached)

---

### 🔴 "CLI output was not valid JSON" or "sandbox-helper: host share not mounted"

Cowork's workspace session file has become corrupted or locked.

👉 [Jump to Fix 2](#fix-2-corrupted-workspace-session-file)

---

### 🔴 Cowork hangs on "Starting…" — Docker Desktop or WSL is also running

A conflict between Cowork and developer virtualization tools is blocking the workspace from launching.

👉 [Jump to Fix 3](#fix-3-docker-and-wsl-conflicts)

---

## Fix 1 — API Cannot Be Reached

**Error:** `"The Claude API cannot be reached from Claude's workspace"`

The private virtual network adapter assigned to Cowork (`vEthernet (cowork-vm-nat)`) has lost its DNS configuration, or Windows has silently cleared the network address translation (WinNAT) rule required to bridge the virtual machine to your internet connection.

!!! warning "Windows Home users"
    The commands in this fix use Windows networking tools that are not available on Windows Home. If you are on Windows Home, this fix cannot be completed. Windows Home is not a supported configuration for Cowork.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

**Work through these steps in order. After each step, reopen Claude Desktop and try launching Cowork. Stop as soon as the error is gone.**

**Step 1 — Exit Claude Desktop**

Right-click the Claude icon in the Windows System Tray (near the clock) → **Exit**.

**Step 2 — Open PowerShell as Administrator**

Click Start, type `powershell`, right-click **Windows PowerShell**, and select **Run as administrator**.

**Step 3 — Assign a stable DNS route to the Cowork adapter**

```powershell
$alias='vEthernet (cowork-vm-nat)'
Set-DnsClientServerAddress -InterfaceAlias $alias -ServerAddresses @('1.1.1.1','8.8.8.8')
Clear-DnsClientCache
```

**Step 4 — Recreate the missing network routing rule**

```powershell
New-NetNat -Name cowork-vm-nat -InternalIPInterfaceAddressPrefix 172.16.0.0/24
```

**Step 5 — Restart the Cowork service**

```powershell
Restart-Service CoworkVMService -Force
```

**Step 6 — Reopen Claude Desktop**

Launch a Cowork session.

✅ **Error gone? You're done.**

❌ **Still seeing the error?**

If this error comes back every time your computer wakes from sleep or reconnects to a VPN, the VPN is overwriting the NAT rule on reconnect. This is not something you can permanently fix yourself — the VPN's split-tunneling rules need to be adjusted by IT.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

#### 🏢 Work computer (managed by your employer)

Your IT department controls network routing on this machine. If your computer connects to a corporate VPN, it is most likely overwriting the NAT rules Cowork needs each time it reconnects.

This is not something you can fix yourself. Your IT department needs to configure VPN split-tunneling to allow Cowork's internal network traffic to pass through.

!!! note "For IT departments"
    Cowork's virtual network adapter (`vEthernet (cowork-vm-nat)`) requires a persistent NAT rule (`172.16.0.0/24`) and DNS assignment (`1.1.1.1`, `8.8.8.8`) to reach `api.anthropic.com`. Corporate VPN clients may clear these rules on reconnect. The resolution is to configure split-tunneling to exclude Cowork's internal subnet (`172.16.0.0/24`) from VPN routing.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

## Fix 2 — Corrupted Workspace Session File

**Error:** `"CLI output was not valid JSON"` or `"sandbox-helper: host share not mounted at /mnt/.virtiofs-root/shared"`

The persistent workspace state file (`sessiondata.vhdx`) has entered a corrupted or locked state. This prevents Cowork's internal file-sharing service (VirtioFS) from connecting your project folders to the workspace execution layer.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

The fix below stops the Cowork service, locates the corrupted session file, renames it as a safety backup, and restarts the service so Claude automatically generates a clean replacement.

**Step 1 — Close Claude Desktop**

Right-click the Claude icon in the Windows System Tray → **Exit**.

If Claude is unresponsive, open Task Manager (`Ctrl + Shift + Esc`), find **Claude**, and click **End Task**.

**Step 2 — Open PowerShell as Administrator**

Click Start, type `powershell`, right-click **Windows PowerShell**, and select **Run as administrator**.

**Step 3 — Stop the service, locate the session file, and rename it**

Run this entire block as written. It handles both standard and Microsoft Store installations automatically.

```powershell
Stop-Service CoworkVMService -Force
$bundle = (Get-Item "$env:LOCALAPPDATA\Packages\Claude_*\LocalCache\Roaming\Claude\vm_bundles\claudevm.bundle" -ErrorAction SilentlyContinue).FullName
if (-not $bundle) { $bundle = "$env:APPDATA\Claude\vm_bundles\claudevm.bundle" }
$session = Join-Path $bundle 'sessiondata.vhdx'
Rename-Item -Path $session -NewName "sessiondata.vhdx.bak"
Start-Service CoworkVMService
```

**Step 4 — Reopen Claude Desktop**

Launch a Cowork session. Claude will detect the missing session file and automatically generate a fresh one.

✅ **Error gone? You're done.**

❌ **Still seeing the error?**

If Claude Desktop cannot generate a new session file, the issue is likely beyond what you can resolve yourself.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

#### 🏢 Work computer (managed by your employer)

Your IT department may have configured folder redirection, which moves your AppData folder to a network location. If this is the case, the session file will not be at its expected path and the script above will fail to find it.

Contact your IT department and share the following:

!!! note "For IT departments"
    Claude Cowork stores its VM session file at one of two locations depending on installation type:

    - Microsoft Store: `%LOCALAPPDATA%\Packages\Claude_*\LocalCache\Roaming\Claude\vm_bundles\claudevm.bundle\sessiondata.vhdx`
    - Standard install: `%APPDATA%\Claude\vm_bundles\claudevm.bundle\sessiondata.vhdx`

    If AppData has been redirected to a network location via Group Policy, the file may be inaccessible or locked. The fix is to locate `sessiondata.vhdx` at the redirected path and rename or delete it so Claude can generate a fresh copy on next launch.

If your organization is on a **Team or Enterprise plan**, contact your Anthropic account administrator or internal IT helpdesk — they have access to Anthropic's enterprise support channel.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

## Fix 3 — Docker and WSL Conflicts

**Symptoms — any of these may appear:**

- Cowork hangs on **Starting…** without launching
- Error messages: `"VM service not running"`, `"Plan9 mount failed"`, or `"virtiofs mount failed"`
- Docker Desktop is running at the same time as Cowork
- WSL distributions (Ubuntu, Debian, etc.) are active in the background

Docker Desktop and WSL2 use the same Windows virtualization layer as Cowork. When they run simultaneously, Windows tries to manage competing virtualization resources — and Cowork loses.

---

### Is this your personal computer or a work computer?

#### 🏠 Personal computer

**Work through these steps in order. After each step, try launching Cowork. Stop as soon as it loads successfully.**

**Step 1 — Fully close Cowork and Docker Desktop**

1. Right-click the Claude icon in the taskbar → **Quit**
2. Right-click the Docker whale icon in the taskbar → **Quit Docker Desktop**
3. Wait 10–15 seconds for Docker's background services to fully stop

**Step 2 — Shut down all WSL instances**

Open **PowerShell as Administrator** and run:

```powershell
wsl --shutdown
```

This stops all running WSL2 distributions and releases the virtualization resources they were holding.

**Step 3 — Restart the Cowork service**

In the same Administrator PowerShell window, run:

```powershell
Restart-Service CoworkVMService
```

If the service is stuck in **Starting** or **Stopping**, force-reset it:

```powershell
Stop-Service CoworkVMService -Force
Start-Service CoworkVMService
```

**Step 4 — Start Cowork before Docker Desktop**

1. Open Claude Desktop and launch a Cowork session
2. Wait for the workspace to fully load before opening anything else
3. Only after Cowork is running, relaunch Docker Desktop if you need it

✅ **Cowork launched? You're done.**

❌ **Still not launching?**

If Cowork still fails after completing all steps, try unregistering WSL distributions you no longer use — they may be claiming network resources Cowork needs even when idle:

```powershell
wsl --list
wsl --unregister <DistributionName>
```

If the problem persists after removing unused distributions, contact Anthropic support.

👉 [How to contact Anthropic support](../support/getting-support.md)

!!! note "Prevent this from happening again"
    The startup order matters — Cowork must claim the virtualization layer first:

    - **Always start Cowork before Docker Desktop**
    - Turn off Docker's auto-start: Docker Desktop → Settings → General → uncheck **"Start Docker Desktop when you log in"**
    - Avoid running heavy WSL workloads while Cowork is active
    - Close VPN or tunneling tools (Tailscale, ZeroTier) before starting Cowork

---

#### 🏢 Work computer (managed by your employer)

Docker Desktop and WSL tools on a managed work computer are typically deployed and controlled by IT. Contact your IT department to:

- Disable Docker Desktop's auto-start at login
- Confirm whether your company's Docker or WSL deployment is compatible with Cowork's virtualization requirements

If your organization is on a **Team or Enterprise plan**, contact your Anthropic account administrator or internal IT helpdesk.

👉 [IT email template: Networking & Plugins](../support/IT_support_email.md)

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
