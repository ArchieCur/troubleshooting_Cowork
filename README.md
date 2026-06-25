# Claude Cowork Troubleshooting Guide

An open-source troubleshooting guide for [Claude Cowork](https://claude.ai) — Anthropic's AI-powered virtual workspace tool — written for non-developer knowledge workers who hit errors that the official documentation does not address.

This guide covers both Windows and macOS, organized by error tier: from networking and storage fixes a user can apply themselves, through known Anthropic server-side bugs where the right action is to stop troubleshooting and file a report.

**Published site:** https://archiecur.github.io/troubleshooting_Cowork/

---

## Who This Is For

- **Individual users** on Claude Pro or Max who encountered a Cowork error and want to fix it without opening a support ticket
- **IT administrators** managing Claude Cowork for a team or enterprise, who need verified fix steps and email templates for helpdesk escalation
- **L&D and knowledge management professionals** evaluating Cowork for organizational rollout

This guide assumes no developer background. Every fix is written in plain language with step-by-step instructions, branched for personal and work-managed computers.

---

## Using This Guide

Start with the error you're seeing and your platform (Windows or macOS). Each section follows a hub-and-spoke model: a symptom index routes you to a specific fix page. If a fix page can't resolve your issue, it will tell you so directly and route you to the appropriate support path rather than leaving you looping through steps that won't work.

**Section structure:**

| Section | Content |
|---|---|
| Getting Set Up | Pre-installation readiness, setup errors, IT prerequisites |
| After Set Up — Tier 1 | Networking, session file corruption, plugin marketplace failures |
| After Set Up — Tier 2 | Scheduled tasks, storage path conflicts |
| After Set Up — Tier 3 | MCP connectors, OAuth persistence, Office add-in bugs |
| After Set Up — Tier 4 | Known dead ends — confirmed bugs or OS limits that require Anthropic to fix |
| Support | How to contact Anthropic, IT email templates, pre-ticket checklist |

---

## How This Was Built

This guide was produced through a structured human + multi-AI workflow, with each contributor doing the work that matched their specific strengths.

### The Team

| Contributor | Phase | Contribution |
|---|---|---|
| **ArchieCur** | All phases | Original multi-source research across Anthropic documentation, GitHub, Microsoft Learn, forums, newsletters, blogs, and social posts; project direction; scope and audience decisions; technical validation; human judgment on tone throughout |
| **Claude Sonnet 4.6** (Anthropic) | Phases 1–2 | Co-created all Section 1 (Getting Set Up) files; conducted GitHub error pattern research to surface post-setup Cowork errors; co-developed the foundational error taxonomy that structured Section 2 |
| **Gemini 3.1 Pro** (Google) | Phase 3 | Organized combined research into the 4-tier structure; identified omissions; drafted all specification handoff files defining scope and fix logic for each tier and platform |
| **Claude Code** (Anthropic) | Phase 4 | Wrote all Section 2 documentation files and the spec format guide; identified spec gaps; applied formatting conventions consistently across all files; asked clarifying questions before writing each file |
| **Microsoft Copilot** | Throughout | Verified Windows and macOS error messages, confirmed tool behavior, validated PowerShell commands and file paths |
| **Anthropic Support** | Throughout | Confirmed Cowork-specific behaviors, validated Anthropic-side bug status, verified documented feature availability |

### The Workflow

The project moved through four distinct phases, each building on the last.

**Phase 1 — Original Research**

ArchieCur conducted independent multi-source research to surface known problems with Cowork on Windows and macOS, drawing from Anthropic documentation, GitHub issues, Microsoft Learn, community forums, newsletters, blogs, and social posts. This foundational research is what the entire guide rests on.

**Phase 2 — Section 1 and Error Surface Research**

ArchieCur and Claude Sonnet 4.6 worked together to organize the setup-phase research into the Section 1 documentation files — Getting Set Up for Windows and macOS, plus the readiness checker. The team then turned to post-setup errors: Sonnet 4.6 focused on GitHub issues to identify error patterns, while ArchieCur continued researching documentation, community sources, and firsthand reports. The combined findings formed the error taxonomy that Section 2 is built on.

**Phase 3 — Organization and Architecture**

ArchieCur brought the combined error research to Gemini 3.1 Pro, which organized the material into the 4-tier structure, identified gaps, and produced the specification handoff files that defined scope and fix logic for each tier and platform.

**Phase 4 — Section 2 Documentation**

Claude Code joined the project to write the Section 2 documentation files from Gemini's specifications. Before writing each file, Claude Code read the spec, returned clarifying questions, and received answers — often with Copilot or Anthropic Support providing verification. Claude Code also wrote the spec format guide that standardized Gemini's output across all tiers, and applied formatting conventions consistently throughout (personal/work branching, admonition style, checkpoint format, footer, support links).

This four-phase structure kept human judgment at the center of every decision while using each collaborator for what they do best: ArchieCur for research depth and audience knowledge, Sonnet 4.6 for pattern recognition and co-authoring, Gemini for architecture and organization, Claude Code for precise and consistent execution, Copilot and Anthropic Support for factual verification.

### A Note on the Working Files

Two folders were maintained locally throughout this project but are not included in this repository:

- **`handoffs/`** — contains all specification files Gemini drafted, the spec format guide used to standardize Gemini's output, and the project roadmap. These files show the complete workflow from first spec to final file.
- **`research-notes/`** — contains Copilot and Anthropic Support verification outputs used to confirm technical details before they were written into the guide.

These folders are excluded from the public repo to keep the repository focused on the troubleshooting content itself. Anyone designing a similar human + multi-AI documentation workflow is welcome to reach out — the methodology is intended to be replicable.

---

## Contributing and Reporting Issues

Found an error, an outdated fix, or a symptom this guide doesn't cover?

- **Open a GitHub Issue** with the platform, error message, and a description of what's wrong or missing
- **Pull requests** with corrections or additions are welcome — please follow the existing file and formatting conventions

This guide will become outdated as Anthropic updates Claude Cowork. Community corrections are essential to keeping it accurate.

---

*Created by ArchieCur in collaboration with Claude Code (Anthropic) and Gemini 3.1 Pro (Google) · Content verified by Microsoft Copilot and Anthropic Support · Open source under [MIT License](LICENSE)*
