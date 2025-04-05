<!--
Copyright (c) Ansible Project
GNU General Public License v3.0+ (see LICENSES/GPL-3.0-or-later.txt or https://www.gnu.org/licenses/gpl-3.0.txt)
SPDX-License-Identifier: GPL-3.0-or-later
-->

# GitHub Action for running nox

[![Linting](https://github.com/ansible-community/github-action-run-nox/actions/workflows/linting.yml/badge.svg)](https://github.com/ansible-community/github-action-run-nox/actions/workflows/linting.yml)
[![REUSE status](https://api.reuse.software/badge/github.com/ansible-community/github-action-run-nox)](https://api.reuse.software/info/github.com/ansible-community/github-action-run-nox)

A composite GitHub Action that allows to build an Ansible collection artifact in GitHub Actions CI/CD workflows.

This action is covered by the [Ansible Code of Conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html).

## Usage

To use the action, add the following step to your workflow file (for example `.github/workflows/nox.yml`):

```yaml
- name: Check out your collection repository
  uses: actions/checkout@v4
  with:
    working-directory: my-code

- name: Install nox
  uses: wntrblm/nox@2025.02.09
  with:
    python-versions: "3.11, 3.12, 3.13"

- name: Lint
  uses: ansible-community/github-action-run-nox@main
  with:
    sessions: lint
    pythons: 3.13
    working-directory: my-code
```

## Options

The follow options can be provided to this GitHub Action.

### `sessions`

Which nox session(s) to run. If left empty, all sessions marked as default will be run.
Can be a space-separated list of sessions.

Example: `formatters codeqa`.

**(DEFAULT: `""`)**

### `pythons`

Which version(s) of Python to force. Should be a space-separated list of Python versions.

Example: `3.11 3.12 3.13`.

**(DEFAULT: `""`)**

### `working-directory`

The directory in which all commands should be run.

**(DEFAULT: `.`)**

### `codecov`

Whether code coverage is collected by the session(s) and should be uploaded.
If set to `true`, the [codecov/codecov-action](https://github.com/codecov/codecov-action) action will be used to upload code coverage.

**(DEFAULT: `false`)**

### `codecov-session`

If a special nox session should be run to collect/analyze code coverage. This is done as an extra step.

**(DEFAULT: `""`)**

### `codecov-name`

If a name should be supplied to codecov. If not specified, will fall back to `sessions`.

**(DEFAULT: `""`)**

### `codecov-token`

Should be provided with the value of `secrets.CODECOV_TOKEN` if `codecov=true`.

**(DEFAULT: `""`)**

## License

This action is primarily licensed and distributed as a whole under the GNU General Public License v3.0 or later.

See [LICENSES/GPL-3.0-or-later.txt](https://github.com/ansible-community/github-action-build-collection/blob/main/COPYING) for the full text.

All files have a machine readable `SDPX-License-Identifier:` comment denoting its respective license(s) or an equivalent entry in an accompanying `.license` file. This conforms to the [REUSE specification](https://reuse.software/spec/).
