# What to Gather Before Contacting Support

Before opening a ticket with Anthropic or your IT team, collect the information below. Having this ready means faster resolution — support staff won't need to follow up asking for details you could have included upfront.

---

## Part 1 — Universal information (all tiers)

Every support ticket should include these regardless of which problem you're experiencing.

---

### Your error message

Copy the exact error message from the troubleshooting guide or directly from the Cowork error screen. Exact wording matters — don't paraphrase it.

---

### Steps you have already tried

Copy the relevant steps from the troubleshooting guide you followed. This prevents support staff from asking you to repeat things you've already done.

---

### Your Claude Desktop app version

=== "Windows"
    1. Click your **profile name or avatar** in the bottom-left corner of the Claude Desktop app
    2. Select **Settings**
    3. Go to the **General** tab under "Desktop app"
    4. Scroll down — your app version is listed there

=== "macOS"
    1. Open the **Claude Desktop app**
    2. Click **Claude** in the top menu bar (next to the Apple logo)
    3. Select **About Claude** to view your version number

---

### Your operating system

=== "Windows"
    1. Open the **Start menu**
    2. Go to **Settings → System → About**
    3. Scroll down to **Windows specifications**
    4. Note your **Edition**, **Version**, and **OS Build**

=== "macOS"
    1. Click the **Apple icon** in the top-left corner of your screen
    2. Select **About This Mac**
    3. Note the macOS name and version number displayed

---

### Relevant logs

Logs give Anthropic's engineers and IT support the technical detail needed to diagnose what went wrong.

=== "Windows — Event Viewer"
    1. Click the **Start menu** or search bar and type `Event Viewer` — open it
    2. In the left panel, click the arrow next to **Windows Logs** to expand it
    3. Click **Application**
    4. In the middle pane, find and click the **Claude Desktop** or **Cowork** log entry
    5. Read the details in the bottom pane
    6. **To export:** Hold **Ctrl** and click to select multiple log entries → right-click your selection → choose **Save Selected Events** → save as a text or CSV file to attach to your ticket

=== "macOS — Console.app"
    1. Press **Command + Spacebar** to open Spotlight, type `Console` and open it — or find it in **Applications → Utilities**
    2. In the left sidebar, look at the **Reports** section
    3. Click **Crash Reports**, **Spin Reports**, or **Log Reports**
    4. Click the **Claude Desktop** or **Cowork** report to read its details in the bottom pane
    5. **To export:** Right-click the report in the sidebar → choose **Reveal in Finder** → attach the raw file to your ticket

---

## Part 2 — Tier-specific information

Find your tier below and include this additional information in your ticket.

---

### Tier 1 — Networking & Plugins

**Your symptoms may include:** "API Unreachable" errors, invalid JSON output, or Plugin Marketplace DNS failures.

**Additional information to include:**

- The exact error message shown in the Plugin Marketplace or API response
- Whether the issue happens on all networks or only on specific ones (e.g., home Wi-Fi vs. office network vs. mobile hotspot)
- Whether you are using a VPN — and if so, which one
- Whether the issue started after a specific update or change to your system

---

### Tier 2 — Scheduled Tasks & Storage

**Your symptoms may include:** Tasks failing silently or UNC path errors.

**Additional information to include:**

- The exact task that is failing and what it was set up to do
- Whether your documents or storage are on a different drive than your Windows installation (e.g., files on D:\ when Windows is on C:\)
- Whether your organization uses folder redirection via Group Policy
- Whether the failure happens when your computer is in sleep or focus mode

---

### Tier 3 — Connectors & Add-ins

**Your symptoms may include:** Missing MCP tools or Office Add-in authentication failures.

**Additional information to include:**

- Which connector or add-in is affected
- Whether the issue appeared after a Claude Desktop or Office update
- Whether the problem occurs in the CLI version of Claude, the Desktop app, or both
- Any authentication error messages shown during login or token refresh

---

### Tier 4 — Known issues (not user fixable)

**Your symptoms may include:** Issues that persist after all troubleshooting steps, or problems that match known Anthropic server-side bugs.

!!! note "What this tier means"
    Some issues are caused by bugs on Anthropic's side — not your computer. These include things like missing OAuth scopes, AppleScript bugs in compiled binaries, or Windows Home limitations. If your troubleshooting guide directed you here, your ticket is important — it helps Anthropic's engineering team track and prioritize these fixes.

**Additional information to include:**

- Confirmation that you have completed all steps in the relevant troubleshooting guide
- The name of the troubleshooting guide you followed
- Whether the issue is reproducible — does it happen every time, or intermittently?
- Any workarounds you have found, even partial ones

---

## Ready to open your ticket?

👉 [How to reach Anthropic support](getting-support.md)

---

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0 · June 2026*
