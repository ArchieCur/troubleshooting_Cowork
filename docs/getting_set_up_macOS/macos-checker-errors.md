# macOS Cowork Readiness Checker — Errors

You ran the Cowork Readiness Checker on your Mac and something came back with a red X or a warning. You're in the right place.

Before troubleshooting any specific error, start with the universal requirements check — most failures on macOS trace back to one of a small number of root causes.

---

## Start here — universal requirements

Before anything else, confirm your Mac meets the baseline requirements for Cowork. This takes about 5 minutes and resolves the majority of readiness failures.

👉 [Check universal requirements first](macos-universal-requirements.md)

---

## Which situation applies to you?

### 🏠 Personal Mac (you own and manage it)

If you own your Mac and control its settings, you have everything you need to resolve most readiness errors yourself.

Common causes include Gatekeeper blocking background scripts, missing folder permissions, corrupted app data, or a stuck background service.

👉 [Fix: Personal Mac troubleshooting](macos-personal-mac-fixes.md)

---

### 🏢 Work Mac (managed by your employer)

If your Mac was issued by your employer, corporate security policies are most likely blocking Cowork from running its background environment. This is not something you can fix yourself — your IT department needs to assist.

Common causes include MDM or EDR software blocking Apple's Virtualization.framework, or corporate VPN and firewall rules blocking internal network communication.

👉 [Fix: Managed Mac — contact IT](macos-managed-mac-it.md)

---

!!! note "Not sure which situation applies to you?"
    A quick way to tell: if you needed permission from your employer to install software, or if you've never been asked for an admin password on this machine, it's likely a managed work Mac. If you set it up yourself and manage your own settings, it's a personal Mac.  

    *ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.0 · June 2026*
