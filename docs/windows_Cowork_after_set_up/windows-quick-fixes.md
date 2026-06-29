# ⚡ Quick Cowork Fixes 

Before trying advanced troubleshooting steps, start with these simple fixes. They resolve many Cowork startup issues without touching BIOS, PowerShell, or system settings.

---

## 1. Quit Cowork Completely
Closing the window does not fully stop Cowork — the VM may still be running in the background.

**Fix:**  
Right‑click the Cowork tray icon → **Quit Cowork**, wait 5 seconds, then relaunch.

**Why it helps:**  
Clears stuck VM sessions, stale mounts, and hung processes.

---

## 2. Restart CoworkVMService (GUI Only)
You can restart the service without using PowerShell.

**Fix:**  
1. Press **Ctrl + Shift + Esc**  
2. Go to **Services**  
3. Find **CoworkVMService**  
4. Right‑click → **Restart**

**Why it helps:**  
Resets the VM, virtiofs, Plan9 mounts, and HCS handles.

---

## 3. Close All WSL Terminals
WSL keeps the hypervisor active even when minimized.

**Fix:**  
Close all:
- Windows Terminal  
- PowerShell  
- CMD  
- VS Code Remote WSL sessions  

**Why it helps:**  
Releases WSL’s VM so Cowork can start its own.

---

## 4. Quit VS Code (Especially Remote WSL)
VS Code Remote WSL silently keeps WSL running.

**Fix:**  
Fully quit VS Code before launching Cowork.

**Why it helps:**  
Prevents WSL from reserving Hyper‑V resources.

---

## 5. Quit Virtualization Apps
These apps auto‑start and reserve virtualization resources:

- Docker Desktop  
- VirtualBox  
- VMware Workstation  
- QEMU  
- Android emulators (BlueStacks, LDPlayer, Nox)

**Fix:**  
Quit these apps before launching Cowork.

**Why it helps:**  
Prevents hypervisor conflicts and VM resource contention.

---

## 6. Disconnect VPN / Tunneling Apps
VPNs create virtual network adapters that block Hyper‑V networking.

Common offenders:
- Tailscale  
- ZeroTier  
- NordVPN  
- ExpressVPN  
- Cisco AnyConnect  
- GlobalProtect  
- Cloudflare WARP  

**Fix:**  
Disconnect or quit the VPN app, then relaunch Cowork.

**Why it helps:**  
Allows Cowork’s VM to obtain an IP address and create its NAT network.

---

## 7. Reboot After Windows Updates
Windows updates often leave Hyper‑V or HNS in a partially updated state.

**Fix:**  
Restart your PC, then launch Cowork before opening other apps.

**Why it helps:**  
Resets Hyper‑V, HNS, WinNAT, and VM state files.

---

## 8. Close Other Running VMs
Hyper‑V allows only one VM to reserve certain resources at a time.

**Fix:**  
Close any running VM from:
- Hyper‑V Manager  
- VirtualBox  
- VMware  

**Why it helps:**  
Ensures Cowork’s VM can start cleanly.

---

## 9. Log Out and Back In
A fast way to reset user‑session virtualization handles.

**Fix:**  
Sign out → sign back in → launch Cowork.

**Why it helps:**  
Clears stale HCS handles and locked VHDX files.

---

## 10. Ensure Only One Cowork Instance Is Running
Launching Cowork twice can cause mount failures.

**Fix:**  
Quit all Cowork windows, then relaunch a single instance.  

**Why it helps:**  
Prevents duplicate VM initialization attempts.

---
*Windows Quick Fixes- Claude Cowork Troubleshooting Guide Created by ArchieCur in collaboration with Copilot (Microsoft) version 1.0.0 June 2026*

---

