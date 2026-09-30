# Contributing to swack-tools

Thanks for your interest. These are the default contribution guidelines for
repositories in the [swack-tools](https://github.com/swack-tools) organization.
A repository's own README or `CONTRIBUTING.md` takes precedence where it
differs.

## Before you start

- **Bugs:** open an issue on the affected repository with the tool version, your
  platform, and a reproducible example. Sanitize any sample files or logs.
- **Larger changes:** open an issue first to discuss the approach. Focused pull
  requests are easier to review than broad ones.
- **Security issues:** do not open a public issue. Follow the
  [security policy](SECURITY.md).

## Making a change

1. Fork the repository and create a branch from `main`.
2. Keep each pull request to one logical change, with tests where the project
   has them.
3. Run the repository's checks before opening the pull request. Examples:

   | Repository | Checks |
   | --- | --- |
   | [OxiDex](https://github.com/swack-tools/oxidex) | `cargo fmt`, `cargo clippy`, `cargo test` (see the [contributing guide](https://oxidex.net/contributing/)) |
   | [tuya-re](https://github.com/swack-tools/tuya-re) | `uv run pytest`, `uv run ruff check src tests` |
   | [Vale AI plugin](https://github.com/swack-tools/vale-ai-plugin) | `python3 scripts/validate_plugin.py` |

4. Describe what changed and why in the pull request. Link the issue it
   addresses.

## Ground rules

- Never commit credentials, device keys, API tokens, or personal data,
  including in tests, fixtures, or commit messages.
- Keep claims in documentation grounded: if a number or capability is not
  measured, say so rather than estimating.
- Licenses are set per repository (for example GPL-3.0 for OxiDex, MIT for the
  Vale AI plugin). By contributing, you agree that your contribution is licensed
  under the license of the repository you contribute to.

## Getting help

Open an issue on the relevant repository. Questions about the organization as a
whole can go to the [.github](https://github.com/swack-tools/.github) repository.
