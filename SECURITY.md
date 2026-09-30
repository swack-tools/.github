# Security policy

This is the default security policy for repositories in the
[swack-tools](https://github.com/swack-tools) organization. A repository that
ships its own `SECURITY.md` takes precedence over this file.

## Reporting a vulnerability

Please report vulnerabilities privately. Do not open a public issue or pull
request that contains exploit details, credentials, device keys, tokens, or
personal data.

1. **Private vulnerability reporting (preferred).** Open the affected
   repository's **Security** tab and choose **Report a vulnerability**. This is
   enabled for [OxiDex](https://github.com/swack-tools/oxidex/security/advisories/new),
   [tuya-re](https://github.com/swack-tools/tuya-re/security/advisories/new),
   and the macOS tools
   ([battery-info-mac](https://github.com/swack-tools/battery-info-mac/security/advisories/new),
   [ram-monitor-mac](https://github.com/swack-tools/ram-monitor-mac/security/advisories/new)).
2. **By email.** If the repository does not offer private reporting, or you cannot
   use it, email **security@swacktech.com**.

Include a minimal reproduction, the affected version or commit, the impact you
observed, and a safe way to reach you. Avoid sending live secrets or
unnecessary personal data.

## What to expect

Reports are handled on a best-effort basis by a single maintainer. No response
time or fix time is guaranteed. Confirmed issues are fixed in the affected
repository and, where appropriate, noted in its release notes, or in a GitHub
security advisory. Please allow time for a fix before disclosing publicly.

## Scope

All public repositories under `swack-tools`. Third-party components these
projects build on (for example ExifTool, Vale, or Trakt) should be reported to
their own maintainers.
