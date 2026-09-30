<p align="center">
  <img src="https://raw.githubusercontent.com/swack-tools/.github/main/profile/assets/banner.svg" alt="swack-tools: Understand files. Build better tools. Cybersecurity, threat intelligence, and AI engineering." width="100%">
</p>

# Security engineering meets practical AI

Tools by [@swackhamer](https://github.com/swackhamer), a developer focused on **cybersecurity, cyber threat intelligence, and AI engineering**. From extracting file metadata to extending AI assistants, these open source projects turn hands-on engineering problems into tools other people can use.

[Explore OxiDex](https://oxidex.net/) · [Browse AI plugins](https://ai.swacktech.com/) · [See all repositories](https://github.com/orgs/swack-tools/repositories)

## File metadata for security workflows

**Understanding a file starts with understanding what's inside it.**

**[OxiDex](https://github.com/swack-tools/oxidex)** is a Rust implementation of ExifTool for metadata extraction and manipulation. It grew out of a security engineering need: a Rust alternative for processing untrusted files in [STRELKA](https://github.com/target/strelka) scanning workflows, with memory safety, throughput, and maintainable parsers as design priorities.

- **Built for integration:** a command-line tool and Rust library, with JSON output for analysis pipelines.
- **Built for investigation:** metadata extraction across images, documents, audio, video, and other file formats.
- **Built with evidence:** comparisons against ExifTool and an [AI development harness](https://github.com/swack-tools/oxidex/blob/main/docs/AI_HARNESS.md) that puts candidate parser changes through builds, comparisons, review, and tests.

[Documentation](https://oxidex.net/) · [Source](https://github.com/swack-tools/oxidex) · [Releases](https://github.com/swack-tools/oxidex/releases) · [Rust API](https://docs.rs/oxidex)

## AI plugins for useful, repeatable work

Plugins for **Claude and Codex** support development workflows and connected applications. The [plugin marketplace](https://ai.swacktech.com/) brings installation guides, capabilities, and downloads together.

| Project | What it does |
| --- | --- |
| **[Vale](https://github.com/swack-tools/vale-ai-plugin)** | Brings documentation checks into AI coding workflows with Vale, Google style rules, automatic hooks, and writing and review skills. [Guide](https://vale.swacktech.com/) |
| **[Token Max](https://github.com/swack-tools/token-max-ai-plugin)** | Audits token use in AI sessions and projects, then supplies actionable findings and fix prompts. The audit leaves code and settings unchanged. [Guide](https://token-max.swacktech.com/) |
| **[Trakt MCP](https://github.com/swack-tools/trakt-ai-plugin)** | Connects AI assistants to personal viewing history, recommendations, lists, and calendars through the Model Context Protocol (MCP), with explicit authorization for account changes. [Guide](https://trakt.swacktech.com/) |

## Protocols, devices, and the systems underneath

The same curiosity extends to reverse engineering and native applications: understand the protocol, expose useful information, and make the system easier to control.

| Project | What it explores |
| --- | --- |
| **[tuya-re](https://github.com/swack-tools/tuya-re)** | Tuya protocol reverse engineering and local device control over Bluetooth LE and the LAN, including protocol framing, cryptography, and sessions. After credential setup, control stays local. |
| **[Battery Monitor](https://github.com/swack-tools/battery-info-mac)** | A native Swift macOS app for battery health, USB-C power delivery, and thermal diagnostics, with a menu bar interface and signed, notarized releases. |

## Explore, contribute, connect

Try a tool, report a reproducible bug, improve the docs, or contribute a focused change. Start with the relevant repository's README and development instructions; the [OxiDex contribution notes](https://github.com/swack-tools/oxidex#contributing) are one place to begin.

For security concerns, check the affected repository's **Security** tab and follow its reporting guidance. Use private vulnerability reporting where the project offers it.

**Interested in file analysis, threat intelligence tooling, or AI developer workflows?** Explore the repositories and find the developer behind them at [@swackhamer](https://github.com/swackhamer).
