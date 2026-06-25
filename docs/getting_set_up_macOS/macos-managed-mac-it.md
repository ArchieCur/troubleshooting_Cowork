# Fix: Managed Mac — Contact IT

If your Mac was issued by your employer, corporate security policies are most likely blocking Cowork from running its background environment. This is not something you can fix yourself.

There are two common causes on managed Macs — share both with your IT department so they can check for either.

---

## What's likely blocking Cowork

### MDM or EDR software

Corporate Macs often use **Mobile Device Management (MDM)** profiles or **Endpoint Detection and Response (EDR)** software. These tools routinely block applications from using Apple's built-in virtualization framework — which is exactly what Cowork relies on.

Your IT department will need to **whitelist the Claude application** so it is permitted to launch background virtualization processes.

### Corporate VPN or firewall

Corporate VPNs and strict firewalls often block the internal network communication between your Mac and Cowork's background Linux virtual machine. Your IT department will need to adjust **network split-tunneling rules** so the application can communicate properly.

---

## Contact your IT department

A pre-written email template is below. Copy it, fill in your details, and send it to your IT helpdesk.

!!! note "Tip for faster results"
    If your organization uses a helpdesk ticketing system, submit a ticket in addition to sending this email. Having a ticket number ensures your request is tracked and doesn't get lost in an inbox.

---

**Subject:** Technical Assistance Request: Enabling Virtualization Permissions for Claude Desktop (macOS)

Hello IT Support Team,

I am attempting to run the system readiness checker for the **Claude Cowork** feature inside the official Claude Desktop app on my managed Mac. The initialization process is failing and I believe our corporate security policies may be blocking it.

Could you please assist me with the following:

**1. Application Whitelisting**

Please check if our Mobile Device Management (MDM) or Endpoint Detection and Response (EDR) software is blocking Claude from launching background virtualization processes. Claude Cowork uses Apple's native **Virtualization.framework** to run a local, sandboxed environment.

**2. Network and Firewall Rules**

Please verify if our local firewall or corporate VPN client is restricting internal network communications between the host Mac and Cowork's local virtualization ports.

**My details:**

- Name: [Your name]
- Device name: [Your Mac's name — find this under Apple menu → System Settings → General → About → Name]
- macOS version: [e.g., macOS Sequoia 15.4 — find this under Apple menu → About This Mac]

Please let me know if you need any logs or further system information to help whitelist or configure the app.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

## While you wait for IT

If you need to use Claude in the meantime, Claude's full chat interface is available at **claude.ai** in any web browser and does not require Cowork or any local setup.

👉 [Back to macOS Checker Errors hub](macos-checker-errors.md)

---

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0 · June 2026*
