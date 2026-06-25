# Is Your Computer Ready for Claude Cowork?

Claude Cowork requires specific local hardware and software to function as an autonomous AI agent, alongside cloud-side operational limits.

These programs will check your system:

## macOS

<https://claude.ai/api/desktop/darwin/universal/cowork-readiness-check/latest/redirect>

The primary requirements include:

- **Hardware:** Mac with Apple Silicon (M1/M2/M3/M4) is required, with at least 8GB of RAM recommended. Intel chips not supported.
- **OS:** macOS Sonoma or later.

## Windows ARM64

<https://claude.ai/api/desktop/win32/arm64/cowork-readiness-check/latest/redirect>

The primary requirements include:

- **Hardware:** Intel Core i7 / Core Ultra 7 (12th-Gen or newer) or AMD Ryzen 7 / Ryzen 9
- **OS:** Windows 11 Pro

## Windows x64

<https://claude.ai/api/desktop/win32/x64/cowork-readiness-check/latest/redirect>

The primary requirements include:

- **Hardware:** Intel Core i7 / Core Ultra 7 (12th-Gen or newer) or AMD Ryzen 7 / Ryzen 9
- **OS:** Windows 10 1809+ or Windows 11 Pro or Enterprise, 64-bit

---

## System Requirements Summary

| | **Chat-only Minimum** | **Cowork Minimum** |
|---|---|---|
| RAM | 8GB | 16GB+ (Cowork), 2GB (Claude Desktop) |
| Disk | 1GB for the app | 5GB+ for Cowork's VM image + project work-trees |
| Processor | Negligible — runs in web browser | Intel Core i7 / Core Ultra 7 (12th-Gen or newer) or AMD Ryzen 7 / Ryzen 9; Apple Silicon (M1/M2/M3/M4) — Intel chips not supported |
| Storage | Negligible — runs in web browser | 256GB SSD minimum, 512GB recommended |
| Network | Outbound HTTPS to `api.anthropic.com` | Same, plus OAuth callbacks on `localhost` for Connectors |
| Account | Free for Chat-only | Cowork requires Pro, Max, Team, or Enterprise |
| Node.js | Not required | Required for MCP servers |

---

## Supported Operating Systems

| **Operating System** | **Version** | **Notes** |
|---|---|---|
| macOS | macOS Sonoma (14.0) or later | All Cowork features supported on supported Mac hardware |
| Windows | Windows 10 1809+ or Windows 11, 64-bit | Cowork requires Virtual Machine Platform and Windows Hypervisor Platform. Older Windows 10 builds or Home edition may pass the basic OS check but still fail the VM step — they are missing required features. |
| Linux | ⚠️ Not officially supported | Only claude.ai and Claude Projects; no Cowork |
| ChromeOS | ⚠️ Not officially supported | Only claude.ai supported; no Cowork |

---

## Known Issues, Limitations & Workarounds

| Issue | Notes |
|---|---|
| **Old laptops with 4–8GB RAM and spinning hard drives** | Not recommended |
| **Windows Home** | ⚠️ Not supported. May work on newer builds with Virtual Machine Platform enabled, but not guaranteed. |
| **Mac with Intel Chips** | ⚠️ Not supported |
| **Windows 10 machines that can't upgrade to 11** | ⚠️ Windows 10 no longer receives security updates |
| **Chromebooks** | ⚠️ Not supported — cannot run Claude Desktop or Node.js natively |
| **VPNs** | VPN software creates routing conflicts with Cowork's internal VM networking. ⚠️ Workaround required. |
| **Biggest Bottlenecks** | RAM and disk speed — SSD and minimum 16GB RAM recommended |

---

## How to Check Your System

### Windows (ARM64 and x64)

1. Click **Start** or use the search bar — type **"about"** or **"about your PC"**
2. Open **About your PC**

**System > About** will display:

- For ARM devices, Device Info will report: `ARM64-based process`, `ARM64` or `ARM64EC`
  - Processor examples: Qualcomm / Microsoft SQ1 / SQ2 / SQ3 / Snapdragon X Elite
- **Processor** — e.g., `Intel(R) Core(TM) i7-4790S CPU @ 3.20GHz`
- **Installed RAM** — e.g., `32.0 GB`
- **Storage** — e.g., `118 GB of 932 GB used`
- **Edition** — e.g., `Windows 11 Pro`
- **Version** — e.g., `25H2`

### macOS

1. Click the **Apple menu** (top-left)
2. Select **About This Mac**

This shows your macOS version, processor/chip type, and memory.

#### Compatible macOS Versions

| **macOS Version** | **Release Status** | **Succeeded By** |
|---|---|---|
| **macOS Sonoma (14)** | Released 2023 | macOS Sequoia (15) |
| **macOS Sequoia (15)** | Released Sept 16, 2024 | macOS Tahoe (26) |
| **macOS Tahoe (26)** | Released Sept 15, 2025 | macOS Golden Gate (27) |
| **macOS Golden Gate (27)** | Announced June 8, 2026 (WWDC); releasing late 2026 — Cowork has not yet been tested on Golden Gate | — |

---
*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.0 · June 2026*

