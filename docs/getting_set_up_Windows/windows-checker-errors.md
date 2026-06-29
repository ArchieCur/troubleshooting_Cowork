# Windows Cowork Readiness Checker — Errors

You ran the Cowork Readiness Checker and something came back with a red X or a warning. You're in the right place.

Find your error below and follow the link to the fix.

---

## Which error are you seeing?

### 🔴 Red X next to "Hardware Virtualization" or "Virtual Machine Platform"

This is the most common result and is usually a quick fix — a feature just needs to be switched on in Windows.

👉 [Fix: Virtual Machine Platform is turned off](fix-virtual-machine-platform.md)

---

### 🔴 Red X that won't go away — or messages saying:

- *"hypervisor not running"*
- *"missing vmcompute / HNS / vfpext"*
- *"WDAC policy present"*

These errors mean the virtual machine feature is turned on, but something else is blocking it from starting. There are a few possible causes and you'll work through them one at a time.

👉 [Fix: Hypervisor not running](fix-hypervisor-not-running.md)

---

### 🔴 Warning about "Application control policy" or "WDAC policy"

This warning appears on computers managed by an employer. It means a security policy is preventing Cowork from running — this is not something you can fix yourself.

👉 [Fix: Application control policy (WDAC)](fix-wdac-policy.md)

---

### 🔴 Warning about "VM service logon right" or "Access Denied"

This warning also appears on employer-managed computers. It means Windows blocked the checker from reading a security setting.

👉 [Fix: VM service logon / Access Denied](fix-access-denied.md)

---  

## Legacy Errors — Resolved

**Legacy Issue: “yukonSilver not supported”**
Early versions of Claude Cowork used an outdated platform‑detection system that misidentified some Windows devices as “yukonSilver,” an internal codename for Windows ARM64.

This caused false “unsupported platform” errors on fully supported Windows 10/11 Pro x64 systems.

**Status:** This issue has been fully resolved by an update to the readiness checker.

**Legacy Issue: Windows Home not supported — now confirmed**

**Status:** This issue has been fully resolved by an update to the readiness checker.

---  

## Need to contact IT?

If your computer is managed by your employer, you may need to send your IT department a request. Pre-written email templates are available here:

👉 [IT email templates for Cowork virtualization errors](windows-it-email-templates.md)  

---

## Known Windows systems that won't work with Cowork

**Windows 11 Home users:** If you are on Windows 11 Home, the Readiness Checker may have incorrectly reported that your system is ready — this is a known issue caused by the way Windows reports its version internally. Windows 11 Home is not a supported configuration for Cowork.  

**Windows 10 users:** Cowork requires Windows 10 build 17763 or higher (released October 2018). To check your build, go to Settings → System → About and look at the OS Build number. If your build is lower than 17763, Windows Update may be able to bring you current — but if your hardware is too old to upgrade, Cowork will not be supported.

---

!!! note "Not sure which error you have?"
    Take a screenshot of your readiness checker results and compare it to the descriptions above. If you're still unsure, the [Fix: Hypervisor not running](fix-hypervisor-not-running.md) page covers the most common layered causes and walks you through them step by step.  

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.1 · June 2026*
