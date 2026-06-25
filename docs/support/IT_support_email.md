# IT Email Templates for reporting errors to Internal IT

If your computer is managed by your employer, use this pre-written email templates to request the changes needed for Cowork to run.

**Instructions:**

1. Copy the template below
2. Fill in the bracketed fields with your information
3. Send it to your IT helpdesk or IT administrator

---

## Tier 1- Networking & Plugins

**Your symptoms may include:** "API Unreachable" errors, invalid JSON output, or Plugin Marketplace DNS failures.

**Additional information to include:**

- The exact error message shown in the Plugin Marketplace or API response
- Whether the issue happens on all networks or only on specific ones (e.g., home Wi-Fi vs. office network vs. mobile hotspot)
- Whether you are using a VPN — and if so, which one
- Whether the issue started after a specific update or change to your system  
- If possible gather relevant logs using this procedure [Gathering Relevant Logs](support-info-to-gather.md)

---

**Subject:** Request: Networking & Plugins for Claude Cowork

Hi [IT Team / Name],

I am receiving this error message [error message from Plugin Marketplace or API response]

I receive this error on these networks [home Wi-Fi vs. office network vs. mobile hotspot]  

This issue started after [include if it was after an update or change in the system]  

I am [using/ not] using a VPN. If using a VPN give VPN name.

I have tried these troubleshooting steps [copy the steps you used from the troubleshooting guide]  

My machine details:
- Name: [Your name]
- Device name / hostname: [Your computer name — find this under Settings → System → About → Device name]
- Operating system: [e.g., Windows 11 Pro, version 24H2 or macOS]

These are the relevant logs: [Paste any Relevant logs you have collected]


Please let me know if you need any additional information.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

## Tier 2- Scheduled Tasks & Storage

**Your symptoms may include:** Tasks failing silently or UNC path errors.

**Additional information to include:**

- The exact task that is failing and what it was set up to do
- Whether your documents or storage are on a different drive than your Windows installation (e.g., files on D:\ when Windows is on C:\)
- Whether your organization uses folder redirection via Group Policy
- Whether the failure happens when your computer is in sleep or focus mode  
- If possible gather relevant logs using this procedure [Gathering Relevant Logs](support-info-to-gather.md)

---

**Subject:** Request: Scheduled Tasks & Storage for Claude Cowork

Hi [IT Team / Name],

I am running [name of the exact task], it was set up to [name the process it was set up to do] and it is [failing silently or giving me UNC path errors]

My documents are [on the same as or a different drive than] my Windows installation.  

I believe we [are using folder redirection via Group Policy or are not using folder redirection via Group Policy]

The failure happens when [computer is in sleep or focus mode or is not in computer is in sleep or focus mode]  

I have tried these troubleshooting steps [copy the steps you used from the troubleshooting guide]  

My machine details:
- Name: [Your name]
- Device name / hostname: [Your computer name — find this under Settings → System → About → Device name]
- Operating system: [e.g., Windows 11 Pro, version 24H2 or macOS]

These are the relevant logs: [Paste any Relevant logs you have collected]


Please let me know if you need any additional information.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

## Connectors & Add-ins

**Your symptoms may include:** Missing MCP tools or Office Add-in authentication failures.

**Additional information to include:**

- Which connector or add-in is affected
- Whether the issue appeared after a Claude Desktop or Office update
- Whether the problem occurs in the CLI version of Claude, the Desktop app, or both
- Any authentication error messages shown during login or token refresh  
- If possible gather relevant logs using this procedure [Gathering Relevant Logs](support-info-to-gather.md)

---

**Subject:** Request: Connectors & Add-ins for Claude Cowork

Hi [IT Team / Name],

I am using [name connector or add-in], and it is not working. I am receiving this [authentication error messages shown during login or token refresh]

This appeared [after a Claude Desktop or Office update or both] 

I have tried these troubleshooting steps [copy the steps you used from the troubleshooting guide]  

My machine details:
- Name: [Your name]
- Device name / hostname: [Your computer name — find this under Settings → System → About → Device name]
- Operating system: [e.g., Windows 11 Pro, version 24H2 or macOS]

These are the relevant logs: [Paste any Relevant logs you have collected]


Please let me know if you need any additional information.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

## Known issues (not user fixable)

**Your symptoms may include:** Issues that persist after all troubleshooting steps, or problems that match known Anthropic server-side bugs.

!!! note "What this tier means"
    Some issues are caused by bugs on Anthropic's side — not your computer. These include things like missing OAuth scopes, AppleScript bugs in compiled binaries, or Windows Home limitations. If your troubleshooting guide directed you here, your ticket is important — it helps Anthropic's engineering team track and prioritize these fixes.

**Additional information to include:**

- Confirmation that you have completed all steps in the relevant troubleshooting guide
- The name of the troubleshooting guide you followed
- Whether the issue is reproducible — does it happen every time, or intermittently?
- Any workarounds you have found, even partial ones 
- If possible gather relevant logs using this procedure [Gathering Relevant Logs](support-info-to-gather.md) 

---

**Subject:** Request: Support for Claude Cowork

Hi [IT Team / Name],

I am having problems with Claude Cowork.  

This is the problem I am having [describe your problem as best as you can]

I have tried these troubleshooting steps [copy the steps you used from the troubleshooting guide]  

[Report if the error is reproducible or if it is intermittent]  

[Report if you have found any workarounds, even if they are partial]

My machine details:
- Name: [Your name]
- Device name / hostname: [Your computer name — find this under Settings → System → About → Device name]
- Operating system: [e.g., Windows 11 Pro, version 24H2 or macOS]

These are the relevant logs: [Paste any Relevant logs you have collected]

Please let me know if you need any additional information.

Thank you,
[Your name]
[Your department]
[Your contact information]

---

!!! note "Tip for faster results"
    If your organization uses a helpdesk ticketing system, submit a ticket in addition to sending this email. Having a ticket number ensures your request is tracked and doesn't get lost in an inbox.  

    *ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.0 · June 2026*
