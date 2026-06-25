# Known Server Bugs and OS Limits — Windows

You have hit an error, searched for a fix, and landed here. The good news is: you can stop troubleshooting. The issues on this page are either confirmed Anthropic server-side bugs or hard Windows OS limitations. No PowerShell command, cache clear, or reinstall will resolve them — they require a fix on Anthropic's end, or they reflect a fundamental limit of your Windows edition.

This page exists purely to save you time.

---

## Which issue applies to you?

### 🔴 You're on Windows Home and Cowork cannot connect to the workspace

WinNAT — the networking component Cowork requires — is not included in Windows 10 Home or Windows 11 Home.

👉 [Jump to Issue 1](#issue-1-windows-home-winnat-not-available)

---

### 🔴 Gmail, Google Drive, or Google Calendar connector won't authenticate

Anthropic's hosted Google connectors are missing a required OAuth scope. This is an Anthropic server-side bug, not a problem with your Google account.

👉 [Jump to Issue 2](#issue-2-google-mcp-connectors-oauth-scope-missing)

---

### 🔴 Office add-in shows "Redirect-URI", "Schema validation", or "Extra inputs" error

These are server-side API contract failures that happen before the add-in reaches your local Office installation.

👉 [Jump to Issue 3](#issue-3-office-add-in-api-contract-errors)

---

## Issue 1 — Windows Home: WinNAT Not Available

**Error:** Cowork cannot reach the API / workspace fails to connect / "API Unreachable"

Cowork's workspace runs as a virtual machine on your computer. On Windows, that VM requires a networking component called **WinNAT** to access the internet. Microsoft does not include WinNAT in any version of Windows 10 Home or Windows 11 Home — it is only available in Windows Pro, Enterprise, and Education editions.

!!! warning "PowerShell commands will not help here"
    If you have arrived here after trying PowerShell networking commands from other troubleshooting guides, those commands fail because the underlying networking modules do not exist on Windows Home. This is not a configuration problem you can work around — it is a fundamental OS limitation.

**How to confirm you are on Windows Home**

Press **Win + I** → **System** → **About** → scroll to **Windows specifications** → check the **Edition** field.

If it says **Windows 10 Home** or **Windows 11 Home**, this issue applies to you. If it says Pro, Enterprise, or Education, return to [networking troubleshooting](windows-networking-errors.md) — WinNAT is not your problem.

**Your options**

- **Upgrade to Windows Pro** — On a personal computer you own, you can purchase the upgrade through **Settings → System → Activation → Upgrade your edition of Windows**. On a work computer, contact your IT department.
- **Use Claude on the web** — Claude's full chat interface at [claude.ai](https://claude.ai) does not require Cowork or WinNAT to function. You can use Claude normally in any browser, on any edition of Windows.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Issue 2 — Google MCP Connectors: OAuth Scope Missing

**Error:** The Gmail, Google Drive, or Google Calendar connector authentication fails silently, loops back to the sign-in screen, or returns an authorization error

Anthropic's hosted MCP connectors for Google services require an OAuth token that includes the scope `user:mcp_servers`. The current version of Claude Desktop is sending an OAuth request that is missing this scope. The authentication request is rejected before your Google credentials are ever evaluated.

**This is not a problem with your Google account.** None of the following will resolve it:

- Re-authenticating or signing out and back in
- Revoking and re-granting Google app permissions
- Signing in with a different Google account
- Clearing your browser cache or Windows credential store

The request is being rejected by Anthropic's servers, not by Google.

**What you can do**

Report it to Anthropic so the impact is registered — the more users who file a report, the faster a fix is prioritized. Use Claude.ai in your browser in the meantime.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Issue 3 — Office Add-in API Contract Errors

**Errors:** `"Redirect-URI mismatch"`, `"Schema validation failed"`, or `"Extra inputs"` when signing in to or using the Claude add-in in Excel or PowerPoint

These three errors are server-side API contract failures. They occur at the moment the add-in calls Anthropic's API — before the request ever reaches your local Office installation:

- **Redirect-URI** — Anthropic's servers are rejecting the OAuth login callback path
- **Schema validation** — The add-in's request does not match the schema Anthropic's API currently expects
- **Extra inputs** — The request body contains fields the API does not recognize or allow

**None of these can be fixed locally.** Do not attempt to:

- Clear your Office add-in cache
- Reinstall the Claude add-in
- Modify your Windows credential store

These steps address local state. The requests are being rejected on Anthropic's side before they reach your machine.

**What you can do**

Report it to Anthropic to put it on record. As a working alternative, [Excel Online and PowerPoint Online](https://office.com) are not affected by this bug — the browser-based Office apps work reliably with Claude.ai.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Reporting to Anthropic

Filing a support report is valuable even when there is no local fix — it registers the real-world impact and directly influences how Anthropic prioritizes these issues.

**Personal account (Claude Pro or Max)**

Submit a ticket through Anthropic's Help Center. Include your Windows edition, the exact error message, and the steps you have already tried.

👉 [How to contact Anthropic support](../support/getting-support.md)

**Work account (Team or Enterprise plan)**

Contact your organization's Anthropic account administrator or your IT helpdesk. They have access to Anthropic's dedicated enterprise support channels and can escalate directly.

👉 [IT email template: Known Issues](../support/IT_support_email.md)

**While you wait**

Claude's full chat interface at [claude.ai](https://claude.ai) does not require the Cowork virtual machine and works in any browser on any edition of Windows.

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
