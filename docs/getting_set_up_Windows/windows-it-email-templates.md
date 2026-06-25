# IT Email Templates for Cowork Virtualization Errors

If your computer is managed by your employer, use these pre-written email templates to request the changes needed for Cowork to run.

**Instructions:**

1. Copy the appropriate template below
2. Fill in the bracketed fields with your information
3. Send it to your IT helpdesk or IT administrator

---

## Application control policy exception

Use this template if the Cowork Readiness Checker flagged a warning about an **application control policy**, **WDAC policy**, or **AppLocker policy**.

---

**Subject:** Request: Application Control Policy Exception for Claude Cowork

Hi [IT Team / Name],

I am requesting an exception to our application control policy to allow **Claude Cowork** to run on my machine.

Claude Cowork is an AI productivity tool made by Anthropic. It requires the following to function:

- Permission to run its virtualization service (`vmcompute`) and associated components (`HNS`, `vfpext`)
- An exemption from any WDAC or AppLocker policy that blocks unsigned or non-whitelisted virtualization components

**My machine details:**

- Name: [Your name]
- Device name / hostname: [Your computer name — find this under Settings → System → About → Device name]
- Operating system: [e.g., Windows 11 Pro, version 24H2]

**Reference:** Anthropic's Cowork architecture documentation confirms that Cowork uses Windows Hyper-V based virtualization on Windows devices to provide isolated code execution environments.

Please let me know if you need any additional information.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

## VM service logon rights

Use this template if the Cowork Readiness Checker flagged a warning about **"VM service logon right"** or an **"Access Denied"** error.

---

**Subject:** Request: VM Service Logon Rights for Claude Cowork

Hi [IT Team / Name],

I am requesting that the appropriate VM service logon rights be granted on my machine to allow **Claude Cowork** to run.

The Cowork Readiness Checker has flagged that the following virtualization services do not have the required **"Log on as a service"** user right on my device:

- `vmcompute` (Hyper-V Host Compute Service)
- `hns` (Host Network Service)

These services are required for Cowork to create and manage its isolated virtual machine environment.

**My machine details:**

- Name: [Your name]
- Device name / hostname: [Your computer name — find this under Settings → System → About → Device name]
- Operating system: [e.g., Windows 11 Pro, version 24H2]

**What's needed:** Please grant **"Log on as a service"** rights to the service accounts associated with `vmcompute` and `hns` via Local Security Policy or Group Policy on my device.

Please let me know if you need any additional information.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

!!! note "Tip for faster results"
    If your organization uses a helpdesk ticketing system, submit a ticket in addition to sending this email. Having a ticket number ensures your request is tracked and doesn't get lost in an inbox.  

    *ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.0 · June 2026*
