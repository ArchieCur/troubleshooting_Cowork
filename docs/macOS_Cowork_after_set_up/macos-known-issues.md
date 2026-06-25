# Known Server Bugs and OS Limits — macOS

You have hit an error, searched for a fix, and landed here. The good news is: you can stop troubleshooting. The issues on this page are either confirmed Anthropic server-side bugs, broken code in Anthropic's compiled application binaries, or hard Mac hardware limitations. No Terminal command, cache clear, or reinstall will resolve them — they require a fix from Anthropic, or they reflect a fundamental limit of your Mac's hardware.

This page exists purely to save you time.

---

## Which issue applies to you?

### 🔴 You have an Intel Mac and Cowork fails the readiness check or won't launch

Apple Intelligence virtualization requires Apple Silicon (M1 or later). Intel Macs cannot run the Cowork workspace environment.

👉 [Jump to Issue 1](#issue-1-intel-mac-hardware-not-supported)

---

### 🔴 Gmail, Google Drive, or Google Calendar connector won't authenticate

Anthropic's hosted Google connectors are missing a required OAuth scope. This is an Anthropic server-side bug, not a problem with your Google account.

👉 [Jump to Issue 2](#issue-2-google-mcp-connectors-oauth-scope-missing)

---

### 🔴 Word or PowerPoint tools fail — `get_slide_content`, `replace_text`, or `open_document` errors

AppleScript syntax errors embedded in Anthropic's compiled application binary make these tools fail on every call. This cannot be fixed by the user.

👉 [Jump to Issue 3](#issue-3-word-and-powerpoint-applescript-binary-bugs)

---

### 🔴 Office add-in shows "Redirect-URI", "Schema validation", or "Extra inputs" error

These are server-side API contract failures that happen before the add-in reaches your local Office installation.

👉 [Jump to Issue 4](#issue-4-office-add-in-api-contract-errors)

---

## Issue 1 — Intel Mac: Hardware Not Supported

**Error:** The readiness checker permanently fails / Cowork workspace fails to launch

Cowork's workspace environment runs as a virtual machine using Apple's Virtualization.framework. This framework requires an **Apple Silicon** processor (M1, M2, M3, or M4). Intel-based Macs do not have the required hardware architecture — there is no software update, settings change, or workaround that enables Cowork on an Intel chip.

**How to confirm your Mac's processor**

Click the **Apple menu ()** → **About This Mac**.

- If you see **Chip: Apple M1** (or M2, M3, M4) → your Mac is Apple Silicon. This issue does not apply to you — return to troubleshooting.
- If you see **Processor: Intel** → this issue applies. No further troubleshooting is needed.

!!! warning "Terminal scripts will not help here"
    If you have come across guides suggesting you run Terminal commands to bypass the readiness checker or force a Cowork installation, do not attempt them. The virtualization hardware simply does not exist on your Mac and no script can substitute for it.

**Your options**

- **Use Claude on the web** — Claude's full chat interface at [claude.ai](https://claude.ai) does not require Cowork, Apple Silicon, or any local virtualization. It works in any browser on any Mac.
- **Request a hardware upgrade** — If you are using a work Mac, contact your IT department about whether an Apple Silicon replacement is available.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Issue 2 — Google MCP Connectors: OAuth Scope Missing

**Error:** The Gmail, Google Drive, or Google Calendar connector authentication fails silently, loops back to the sign-in screen, or returns an authorization error

Anthropic's hosted MCP connectors for Google services require an OAuth token that includes the scope `user:mcp_servers`. The current version of Claude Desktop is sending an OAuth request that is missing this scope. The authentication request is rejected before your Google credentials are ever evaluated.

**This is not a problem with your Google account.** None of the following will resolve it:

- Re-authenticating or signing out and back in
- Revoking and re-granting Google app permissions
- Signing in with a different Google account
- Clearing the `~/.claude/mcp-needs-auth-cache.json` file

The request is being rejected by Anthropic's servers, not by Google.

**What you can do**

Report it to Anthropic so the impact is registered — the more users who file a report, the faster a fix is prioritized. Use Claude.ai in your browser in the meantime.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Issue 3 — Word and PowerPoint: AppleScript Binary Bugs

**Errors:** `get_slide_content` fails every time / `replace_text` fails every time / `open_document` reports success but nothing happens in Word or PowerPoint

The built-in Word and PowerPoint MCP connectors in Claude Desktop for macOS contain AppleScript syntax errors embedded directly in the application's compiled `Bun.js` binary. These errors cause three specific tools to fail on every call:

| Tool | What fails |
|---|---|
| `get_slide_content` | Fails 100% of the time — AppleScript syntax error in the binary |
| `replace_text` | Fails 100% of the time — AppleScript syntax error in the binary |
| `open_document` | Reports success, but the VM-to-Mac file path translation fails silently |

**This cannot be fixed by any local action.** Because the bugs are compiled into the application binary Anthropic ships with Claude Desktop, the script is not a file you can edit, patch, or replace. The fix requires Anthropic to correct the syntax errors and release an updated version of Claude Desktop for macOS.

Do not attempt to:

- Reinstall Word or PowerPoint
- Edit AppleScript files in your Applications folder
- Clear macOS script caches or permissions

None of these touch the compiled binary where the errors live.

**What you can do in the meantime**

Use Claude.ai in your browser to generate or edit document content, then manually apply the changes in Word or PowerPoint. It is slower than a working connector, but it is the only reliable path until Anthropic ships a fix.

Report it to Anthropic to put the bug on record.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Issue 4 — Office Add-in API Contract Errors

**Errors:** `"Redirect-URI mismatch"`, `"Schema validation failed"`, or `"Extra inputs"` when signing in to or using the Claude add-in in Excel or PowerPoint

These three errors are server-side API contract failures. They occur at the moment the add-in calls Anthropic's API — before the request ever reaches your local Office installation:

- **Redirect-URI** — Anthropic's servers are rejecting the OAuth login callback path
- **Schema validation** — The add-in's request does not match the schema Anthropic's API currently expects
- **Extra inputs** — The request body contains fields the API does not recognize or allow

**None of these can be fixed locally.** Do not attempt to:

- Clear your Office add-in cache at `~/Library/Containers/com.Microsoft.OsfWebHost/Data/`
- Reinstall the Claude add-in
- Sign out and back in to Microsoft Office

These steps address local state. The requests are being rejected on Anthropic's side before they reach your machine.

**What you can do**

Report it to Anthropic to put it on record. As a working alternative, [Excel Online and PowerPoint Online](https://office.com) are not affected by this bug — the browser-based Office apps work reliably with Claude.ai.

👉 [How to contact Anthropic support](../support/getting-support.md)

---

## Reporting to Anthropic

Filing a support report is valuable even when there is no local fix — it registers the real-world impact and directly influences how Anthropic prioritizes these issues.

**Personal account (Claude Pro or Max)**

Submit a ticket through Anthropic's Help Center. Include your Mac's chip type, your macOS version, the exact error message or tool name you're seeing, and the steps you have already tried.

👉 [How to contact Anthropic support](../support/getting-support.md)

**Work account (Team or Enterprise plan)**

Contact your organization's Anthropic account administrator or your IT helpdesk. They have access to Anthropic's dedicated enterprise support channels and can escalate directly.

👉 [IT email template: Known Issues](../support/IT_support_email.md)

**While you wait**

Claude's full chat interface at [claude.ai](https://claude.ai) does not require the Cowork virtual machine and works in any browser on any Mac — including Intel Macs.

---

*ArchieCur created in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · v1.0.0 · June 2026*
