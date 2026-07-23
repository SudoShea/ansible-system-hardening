# Changelog

All notable changes to the `ansible-system-hardening` project will be documented in this file.

## [1.0.1] - 2026-07-24
### Fixed
- Refactored `site.yml` tasks to replace `ignore_errors` with explicit `failed_when: false` handling.
- Corrected YAML syntax formatting and document markers in `site.yml`.

### Added
- Added `requirements.yml` to track external Ansible collection dependencies (`community.general` and `ansible.posix`).
- Integrated automated CI/CD pipeline using GitHub Actions and `ansible-lint`.

## [1.0.0] - 2026-05-10
### Added
- Initial release of automated system hardening and firewall management playbooks.
