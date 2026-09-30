<p align="center">
  <a href="https://github.com/orgs/swack-tools/repositories"><img src="https://raw.githubusercontent.com/swack-tools/.github/main/profile/assets/banner.svg" alt="swack-tools: Understand files. Build better tools." width="100%"></a>
</p>

# swack-tools: memory-safe file analysis and AI plugins

Allen ([@swackhamer](https://github.com/swackhamer)) builds tools for cybersecurity and cyber threat intelligence and has recently focused on AI development. The flagship is **[OxiDex](https://github.com/swack-tools/oxidex)**, a memory-safe Rust reimplementation of ExifTool for pipelines that scan untrusted files. Around it: Claude and Codex plugins, a from-scratch Tuya protocol implementation, and macOS utilities explicit about what runs as root. Written in Rust, Python, and Swift.

[OxiDex docs](https://oxidex.net/) · [Plugin marketplace](https://ai.swacktech.com/) · [All repositories](https://github.com/orgs/swack-tools/repositories)

## File analysis: OxiDex

File scanners such as [Strelka](https://github.com/target/strelka) shell out to ExifTool: Strelka routes Office, PDF, LNK, SWF, and image files to `ScanExiftool`, which runs `exiftool -j` and parses the JSON. ExifTool has publicly documented vulnerabilities, including [CVE-2021-22204](https://nvd.nist.gov/vuln/detail/CVE-2021-22204) (code execution from a crafted DjVu image; fixed in 12.24 and listed in CISA's Known Exploited Vulnerabilities Catalog) and [CVE-2022-23935](https://nvd.nist.gov/vuln/detail/CVE-2022-23935) (command injection through a crafted filename; fixed in 12.38). OxiDex was written to replace that step: a memory-safe extractor for untrusted input, with ExifTool-compatible arguments and `-j` output, and parsers meant to be read, tested, and extended.

Measured: 16,684 tag definitions; 77.5% extraction conformance against ExifTool 13.59 across 126 format families ([coverage report](https://oxidex.net/reference/tag-coverage-analysis)); 3.7-9.7x faster than Perl ExifTool on the [project's published benchmarks](https://oxidex.net/performance/benchmarks). GPL-3.0 licensed.

- **Built for triage:** PE executables (imports, exports, [Rich header](https://oxidex.net/features/pe-rich-header), version info, and Authenticode signer details read without validating the signature), ELF and Mach-O binaries, LNK shortcuts, PCAP/PCAP-NG captures, ZIP/RAR archives, and [Office documents](https://github.com/swack-tools/oxidex/blob/main/docs/features/OFFICE_FORENSIC_METADATA.md) (authorship and revision metadata); optional [Magika](https://github.com/google/magika) content-based type detection.
- **Built to deploy:** an ExifTool-compatible command-line tool (`-j`, `--csv`, recursive `-r`); static musl Linux binaries (x86_64, arm64); Developer ID-signed and notarized macOS builds; a Windows build; a multi-arch [Docker image](https://hub.docker.com/r/swackhamer/oxidex); a Rust library ([API reference](https://oxidex.net/reference/api-reference)); a C ABI with a cbindgen-generated header ([FFI reference](https://oxidex.net/reference/ffi-api)); and a reference Python binding.
- **Built to be verified:** `unsafe` kept out of the format parsers; libFuzzer [fuzz harnesses](https://github.com/swack-tools/oxidex/tree/main/fuzz) for PDF, MP4, FLAC, and MP3; `cargo audit` inside the required Lint & Audit status check; SHA-pinned GitHub Actions; pinned ExifTool (`.exiftool-version`) as CI's differential-test oracle.
- **Built with an autonomous AI harness:** ["the fleet"](https://oxidex.net/AI_HARNESS) runs parallel LLM workers in separate git worktrees to patch parsers for tags that ExifTool reports and OxiDex misses. Each candidate must pass an ordered gate stack (apply, build, re-comparison against ExifTool, structural and gap-count gates, targeted tests, duplicate check, reviewer model, full test suite) before commit. Results: 67 tag gaps closed with per-commit evidence across 13 formats; figures that could not be measured are labeled *not measured*. Where ExifTool's tag tables hold the answer, OxiDex [extracts that data mechanically](https://oxidex.net/TRANSCRIPTION) (27,747 entries in 1.3 seconds) rather than spending roughly 112 model calls per delivered tag.

## AI plugins for Claude and Codex

Each plugin ships to Claude and Codex from one source tree. Together: 12 skills, 3 lifecycle hooks, and a 15-tool remote MCP server, installable from the [ai-plugin-marketplace](https://github.com/swack-tools/ai-plugin-marketplace) repository.

| Project | What it does |
| --- | --- |
| **[Vale&nbsp;AI&nbsp;plugin](https://github.com/swack-tools/vale-ai-plugin)**<br><sub>[Guide](https://vale.swacktech.com/)</sub> | [Vale](https://vale.sh/) with bundled Google style rules: three lifecycle hooks, four prose skills, and a checker that never edits files. CI smoke-tests it against real Claude Code and Codex clients. |
| **[Token&nbsp;Max](https://github.com/swack-tools/token-max-ai-plugin)**<br><sub>[Guide](https://token-max.swacktech.com/)&nbsp;·&nbsp;[Evidence](https://token-max.swacktech.com/review.html)</sub> | Report-only token audit of sessions and projects; it installs no hooks. Every finding is labeled *measured*, *estimated*, or *hypothesis*; actionable ones include a copyable fix prompt. |
| **[Trakt&nbsp;MCP](https://github.com/swack-tools/trakt-ai-plugin)**<br><sub>[Guide](https://trakt.swacktech.com/)&nbsp;·&nbsp;[CI&nbsp;security](https://github.com/swack-tools/trakt-ai-plugin/blob/main/CI_SECURITY.md)</sub> | Rust MCP server on Cloudflare Workers for Trakt history, recommendations, lists, and calendars. It runs its own OAuth 2.0 authorization server (S256 PKCE for public clients, `trakt:read`/`trakt:write` scopes); refresh cannot raise scope; every write needs write scope plus `confirmed: true`. Its CI runs CodeQL, OSV Scanner, and dependency audits on SHA-pinned GitHub Actions, plus a branch-protection check. |

## Protocols and macOS tools

| Project | What it does |
| --- | --- |
| **[tuya-re](https://github.com/swack-tools/tuya-re)**<br><sub>[Protocol notes](https://github.com/swack-tools/tuya-re#how-the-pieces-fit)</sub> | From-scratch Python implementation of Tuya's BLE v3 and LAN v3.3/v3.4 protocols, with framing verified against byte-exact golden vectors. Its SECURITY.md classifies every credential and documents rotation; CI runs gitleaks over the full history. After a one-time credential pull, commands never leave the LAN. |
| **[Battery&nbsp;Monitor](https://github.com/swack-tools/battery-info-mac)**<br><sub>[Releases](https://github.com/swack-tools/battery-info-mac/releases)</sub> | Swift menu bar app for battery health, USB-C Power Delivery, and thermal diagnostics. An optional root LaunchDaemon helper runs the privileged collectors; the UI never runs as root. Signed, notarized DMGs with SHA-256 checksums. |
| **[ram-monitor](https://github.com/swack-tools/ram-monitor-mac)**<br><sub>[Releases](https://github.com/swack-tools/ram-monitor-mac/releases)</sub> | Rust root LaunchDaemon that terminates the largest processes when used memory crosses a configurable threshold. Allowlist of critical daemons, dry-run mode, and signed, notarized, checksummed releases with documented `codesign`/`spctl` verification. |

## Get involved

- **Use a tool:** download an OxiDex [prebuilt binary](https://github.com/swack-tools/oxidex/releases) and run `oxidex -j sample.pdf`; install the plugins from the [plugin marketplace](https://ai.swacktech.com/).
- **Ask a question or report a bug:** open an issue on the relevant repository (for example, [OxiDex issues](https://github.com/swack-tools/oxidex/issues)); for bugs, include a reproducible example.
- **Contribute:** open an issue before anything beyond a focused fix, then follow the org [contributing guide](https://github.com/swack-tools/.github/blob/main/CONTRIBUTING.md) and [OxiDex's contributing guide](https://oxidex.net/contributing/).
- **Report a vulnerability:** OxiDex ([report privately](https://github.com/swack-tools/oxidex/security/advisories/new)), tuya-re, and the macOS tools accept private vulnerability reports; the org [security policy](https://github.com/swack-tools/.github/blob/main/SECURITY.md) covers the rest.
