# Fix: Hypervisor Not Running

You've already turned on **Virtual Machine Platform** and **Windows Hypervisor Platform** in Windows Features — but the Cowork Readiness Checker is still showing errors like:

- *"hypervisor not running"*
- *"missing vmcompute / HNS / vfpext"*
- *"WDAC policy present"*

This means the virtual machine feature is turned on, but something else on your computer is blocking it from starting. There are a few possible causes.

**Work through the steps below in order.** After each step, restart your computer and run the Cowork Readiness Checker again. Stop as soon as the errors are gone — you don't need to do every step.

---

## Step 1 — Check Memory Integrity (Core Isolation)

This is the **#1 cause** of "hypervisor not running" on personal PCs. Memory Integrity is a Windows security feature that, when turned on, can prevent the virtualization services Cowork needs from starting.

**1. Open the Start menu**

Type `Windows Security` and open it.  

![Windows Security](../assets/hypervisor_not_running/windows_security.png)  

**2. Go to Device Security**  

![Device Security](../assets/hypervisor_not_running/device_security.png)  

Select **Device Security** → click **Core isolation details**.  

![Core Isolation](../assets/hypervisor_not_running/core_isolation.png)  

**3. Check Memory Integrity**  

![Memory Integrity](../assets/hypervisor_not_running/memory_integrity.png)  

- If Memory Integrity is **ON → turn it OFF**
- If Memory Integrity is **OFF → leave it off and skip to Step 2**

**4. Restart your computer**  

![Restart](../assets/fix_access_denied/restart.png) 

**5. Run the Cowork Readiness Checker again**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Step 2.**

---

## Step 2 — Check Reputation-Based Protection (Smart App Control)

Windows security settings can sometimes act as a "bouncer" that blocks Cowork's virtualization services from being approved to run.   
This step temporarily relaxes those restrictions so you can test whether they are the cause.

**1. Open the Start menu**

Type `App & browser control` and open it.  

![App and Browser Control](../assets/hypervisor_not_running/app_browser_control.png) 

**2. Go to Reputation-based protection settings** 

Click **Reputation-based protection settings**.  
 
![Reputation Protection](../assets/hypervisor_not_running/reputation.png) 


**3. Temporarily turn OFF these three settings:**

- **Check apps and files**  

![Check apps and files](../assets/hypervisor_not_running/check_apps_and_files.png) 

- **SmartScreen for Microsoft Edge**  

![SmartScreen](../assets/hypervisor_not_running/SmartScreen.png) 

- **Potentially unwanted app blocking**  

![Potentially Unwanted](../assets/hypervisor_not_running/potentially_unwanted.png) 

!!! note "You can turn these back on later"
    These are temporary changes for testing. Once Cowork is running, you can turn them back on.

**If you see a message saying these are controlled by Smart App Control and can't be changed:**

- Go back one screen  

![Go back](../assets/hypervisor_not_running/go_back.png)

Select **Smart App Control settings**

![SmartApp Control](../assets/hypervisor_not_running/smart_app_settings.png) 

- Click the radio button to turn Smart App Control **Off**  

![SmartApp Off](../assets/hypervisor_not_running/smart_app_off.png) 

- Click **Yes** in the pop-up that appears 

- Then return to **Reputation-based protection settings** and **turn off the three items listed in Step 2- #3 above**  


**4. Check Exploit Protection**

While still in App & browser control:

- Go back one screen

![Go back](../assets/hypervisor_not_running/go_back.png)

- Scroll down to **Exploit protection** → click **Exploit protection settings** 

![Exploitation Protection](../assets/hypervisor_not_running/exploit_protection.png) 
 
- Select the **System settings** tab  

![Exploitation system settings](../assets/hypervisor_not_running/system_settings.png) 

- Scroll to **Control flow guard (CFG)**  

![Control Flow Guard](../assets/hypervisor_not_running/control_flow_guard.png) 

- Make sure it is set to **Use default (On)**  

**5. Restart your computer**  

![Restart](../assets/fix_access_denied/restart.png) 

**6. Run the Cowork Readiness Checker again**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Step 3.**

---

## Step 3 — Check if Virtualization is Enabled in Task Manager

Before going into your computer's hardware settings, this quick check tells you whether virtualization is switched off at the hardware level.

**1. Right-click on an empty area of your taskbar**

Select **Task Manager**.  

![Task Manager](../assets/hypervisor_not_running/task_manager.png) 

**2. Click Performance → then CPU** 
 
![Performance](../assets/hypervisor_not_running/performance.png) 

![CPU](../assets/hypervisor_not_running/cpu.png) 

At the bottom of the screen, look for **Virtualization**.  

![Virtualization](../assets/hypervisor_not_running/virtualization.png) 

You will see one of these:

| What it says | What it means |
|---|---|
| **Virtualization: Enabled** | Your hardware is fine — skip to Step 4 (antivirus check) |
| **Virtualization: Disabled** | You need to enable it in BIOS — continue to Step 3a below |
| **Virtualization: Not supported** | Your processor does not support virtualization. This is rare on modern PCs. |

---

### Step 3a — Enable Virtualization in BIOS/UEFI

!!! warning "Read this before you start"
    The BIOS controls low-level hardware settings. You should only change the virtualization option — do not adjust anything else. If your PC is less than 5 years old, virtualization is likely already enabled and you can skip this step.

**How to get into BIOS/UEFI:**

**1. Open Settings**

Type `Settings` in the search bar and click **Open**  

![Settings](../assets/hypervisor_not_running/Settings_open.png) 

**2. Go to Recovery**

Scroll to **Recovery** and click on it.  

![Recovery](../assets/hypervisor_not_running/recovery.png) 

**3. Click "Restart now" under Advanced startup**  

![Restart Now](../assets/hypervisor_not_running/advanced_startup.png) 

Your computer will restart into a menu screen. 

**4. In the menu select:**  

Computer manufactures have menu screens with different appearances. You will look for these specific items in the menu- 

- **Troubleshoot**
- **Advanced options**
- **UEFI Firmware Settings**
- **Restart**

**What to look for once you're in BIOS/UEFI:**

Look for a setting with one of these names — they all mean the same thing:

- Intel Virtualization Technology
- Intel VT-x
- AMD-V
- SVM Mode
- Virtualization Support
- Virtual Machine Support

**What to do:**

- Set it to **Enabled**
- Save and exit — usually by pressing **F10**
There may be on screen instruction showing how to exit.

**What NOT to touch:**

| Setting | Leave it alone |
|---|---|
| Secure Boot | ⬜ Do not change |
| TPM | ⬜ Do not change |
| Boot order | ⬜ Do not change |
| Overclocking | ⬜ Do not change |
| C-states | ⬜ Do not change |
| Anything mentioning voltage or frequency | ⬜ Do not change |

**After saving and restarting:**

Open Task Manager → Performance → CPU and confirm it now says **Virtualization: Enabled**.

Then run the **Cowork Readiness Checker** again.

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Step 4.**

---

## Step 4 — Check for Antivirus Interference

Some antivirus programs block the hypervisor from starting in order to "protect" your system. This step temporarily disables that protection so you can test whether your antivirus is the cause.

**1. Open the Start menu**

Type `Windows Security` and open it.  

![Windows Security](../assets/hypervisor_not_running/windows_security.png) 

**2. Go to Virus & threat protection**  

![Virus and Threat protection](../assets/hypervisor_not_running/Virus_threat.png) 

Select **Virus & threat protection** → scroll to **Virus & threat protection settings** → click **Manage settings**.  

![Virus and Threat protection Settings](../assets/hypervisor_not_running/virus_threat_settings.png) 

**3. Temporarily turn OFF:**

- **Real-time protection**  

![Realtime protection](../assets/hypervisor_not_running/Realtime_protection.png) 

- **Tamper protection** (if present)  

![Tamper Protection](../assets/hypervisor_not_running/Tamper_protection.png) 

!!! note "You can turn these back on after testing"
    If turning these off fixes the problem, you'll want to turn them back on and then look into your antivirus settings for a way to whitelist Cowork specifically.

**4. Restart your computer**  

![Restart](../assets/fix_access_denied/restart.png) 

**5. Run the Cowork Readiness Checker again**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Step 5.**

---

## Step 5 — Check Device Encryption

Device Encryption can sometimes reserve the hypervisor in a way that prevents Cowork from using it.  

Claude Cowork runs a small virtual machine. On some Windows systems, Device Encryption or BitLocker can reserve the Windows hypervisor, preventing Cowork’s VM from starting.  

This issue is documented across multiple Cowork troubleshooting reports and aligns with Microsoft’s own guidance about BitLocker’s interaction with Hyper V.

!!! Note      Windows 11 Home users: If you are on Windows 11 Home, the Readiness Checker may have incorrectly reported that your system is ready — this is a known issue caused by the way Windows reports its version internally. Windows 11 Home is not a supported configuration for Cowork. This has been reported as being corrected in a Readiness Checker update.
 
!!! Note      Windows 10 users: Cowork requires Windows 10 build 17763 or higher (released October 2018). To check your build, go to Settings → System → About and look at the OS Build number. If your build is lower than 17763, Windows Update may be able to bring you current — but if your hardware is too old to upgrade, Cowork will not be supported.

**1. Open Settings**  

**2. Go to Privacy & security**   

![Privacy and Security](../assets/hypervisor_not_running/privacy_security.png) 
   
- Select **Device Security**  

![Device Security](../assets/hypervisor_not_running/device_securityA.png) 

- If you see **Device Encryption, turn it OFF and restart**. or  

- If you see **BitLocker Drive Encryption, suspend or turn it OFF and restart**

![BitLocker Off](../assets/hypervisor_not_running/bit_locker_off.png) 


**3. Run the Cowork Readiness Checker again**

✅ **Errors gone? You're done — ready to install Cowork!**

❌ **Still seeing errors? Continue to Step 6.**

---

## Step 6 — Check Windows Update

In rare cases, the hypervisor fails to start because of a missing Windows update.

**1. Open Settings → Windows Update**  

![Windows Update](../assets/hypervisor_not_running/windows_update.png) 

**2. Click Check for updates**  

![Check for updates](../assets/hypervisor_not_running/check_for_updates.png) 

**3. Install all available updates**

**4. Restart your computer**  

![Restart](../assets/fix_access_denied/restart.png) 


**5. Run the Cowork Readiness Checker again**

✅ **Errors gone? You're done — ready to install Cowork!**

---

## Still not working?

If you've worked through all six steps and the errors are still there, the issue may be related to an application control policy on your computer. This is uncommon on personal PCs but can happen if you have certain security software installed.

👉 [Fix: Application control policy (WDAC)](fix-wdac-policy.md)

If your computer is managed by your employer, your IT department will need to assist.

👉 [IT email templates for Cowork virtualization errors](windows-it-email-templates.md)  

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.0 · June 2026*
