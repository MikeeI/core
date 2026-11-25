# AI Agent Guidelines for ownCloud Core

This file provides context for AI coding agents (Claude Code, GitHub Copilot, Cursor, etc.) working in this repository.

## Repository Overview
- **Product family:** Classic (OC10)
- **Primary language(s):** PHP, JavaScript
- **Build system:** Composer, Make, npm/Yarn
- **Test framework:** PHPUnit, JavaScript tests (Node), Acceptance tests (Behat)
- **CI system:** GitHub Actions

## Fork & Upstream Contribution Intent

- Official upstream: [owncloud/core](https://github.com/owncloud/core).
- This checkout is the [MikeeI/core](https://github.com/MikeeI/core) fork, not an independently owned product.
- The canonical upstream branch is `master` at `upstream/master`.
- The fork supports evidence-backed upstream issues, comments, and pull requests.
- `ISSUES.md` provides the compact finding overview and global ID allocator.
- `issues/ISSUE-NNN.md` owns the complete durable record for one root cause.
- `FORMAT.md` owns research, drafting, implementation authorization, approval, and publication rules.
- Prefer small, well-scoped corrections with clear maintainer or user value.
- Never choose `Authorized-Work` or `Publication-Target` on the user's behalf.
- Keep fork-only context, ledgers, configuration, and personal commits out of upstream contribution diffs.
- Apply `skill-fork-contribution-tracking` for ledger, lifecycle, branch, and upstream handoff work.
- Apply `skill-maintainer-communication` before external issues, pull requests, reviews, comments, or discussions.
- Apply `skill-semantic-compression-3` when authoring or restructuring tracking content.

## Branch Roles

- `master` mirrors `upstream/master` and remains free of fork-only context and source changes.
- `personal` owns this fork's fork-specific `AGENTS.md` sections, `FORMAT.md`, `ISSUES.md`, and `issues/` tracking state.
- Each upstream contribution uses a separate branch based on the current `upstream/master`.
- Contribution branches contain only the authorized source change and its focused verification.
- Rebase contribution branches before pushing and never create merge commits.
- Every commit must be GPG-signed and carry a DCO sign-off with `git commit -S -s`.
- Publication to official upstream requires approval of the exact current draft and target.

## Project Ownership Map

- `lib/` owns the core PHP library and private and public APIs.
- `core/` owns the Classic web application, login, file list, and core UI behavior.
- `apps/` owns bundled applications.
- `ocs/`, `ocs-provider/`, and `ocm-provider/` own OCS and Open Cloud Mesh provider endpoints.
- `config/` owns configuration samples and defaults.
- `tests/` owns unit, JavaScript, integration, and Behat acceptance tests.
- `build/`, `Makefile`, Composer manifests, and Yarn configuration own build automation and dependencies.
- `l10n/` owns translations, which must be submitted through Transifex rather than pull requests.

## Finding and Contribution Ledger

- At the start of every agent session, read `ISSUES.md` before repository work.
- `ISSUES.md` owns the global `Next finding ID` allocator and compact cross-finding overview.
- Each `issues/ISSUE-NNN.md` owns one finding's state, evidence, drafts, and next action.
- `FORMAT.md` is authoritative for research, drafting, implementation boundaries, and publication format.
- Search existing findings and upstream work before creating a new record.
- New findings start with `State: Investigating`, `Authorized-Work: Not-Selected`, and `Publication-Target: Not-Selected`.
- The user selects `Authorized-Work` for each finding and publication requires approval of the exact draft and target.
- Run the read-only validator bundled with `skill-fork-contribution-tracking` after every ledger mutation.
- Keep fork-only `AGENTS.md` sections, `FORMAT.md`, `ISSUES.md`, and `issues/` out of every upstream contribution diff.
- Do not record security vulnerabilities in public issue records; use https://security.owncloud.com.
- Keep security findings in the local, git-excluded dossier `security/`; never in the contribution ledger, never in a pushed commit, and never in an upstream contribution diff.

## Architecture & Key Paths
- `lib/` - Core PHP library (private and public APIs)
- `core/` - Core app (login, file list, etc.)
- `apps/` - Bundled apps
- `config/` - Configuration samples and defaults
- `ocs/` - OCS API endpoints
- `ocs-provider/` - OCS provider discovery
- `ocm-provider/` - Open Cloud Mesh provider
- `build/` - Build scripts and tools
- `l10n/` - Translations
- `tests/` - Test suites (unit, integration, acceptance)
- `Makefile` - Build and test automation
- `composer.json` - PHP dependencies
- `phpcs.xml` - PHP_CodeSniffer configuration
- `phpstan.neon` - PHPStan configuration
- `CHANGELOG.md` - Release history
- `console.php` - CLI entry point
- `occ` - ownCloud console CLI tool
- `cron.php` - Background job runner
- `index.php` - Web entry point

## Development Conventions
- **Branching:** master
- **Commit messages:** DCO sign-off required (`git commit -s`). Must follow [Conventional Commits](https://www.conventionalcommits.org/) format.
- **Code style:** PHP_CodeSniffer (phpcs.xml), ownCloud coding standard
- **PR process:** Open a PR against master. All CI checks must pass.

## Build & Test Commands
```bash
# Build (install all dependencies)
make

# Test (PHP unit)
make test-php-unit

# Test (JavaScript)
make test-js

# Test (acceptance - API)
make test-acceptance-api

# Test (acceptance - CLI)
make test-acceptance-cli

# Test (acceptance - Web User Interface)
make test-acceptance-webui

# Lint (PHP)
make test-php-style

# Fix code style
make test-php-style-fix
```

## Important Constraints
- All code contributions must be compatible with the **AGPL-3.0** license
- Do not introduce new **copyleft-licensed dependencies** (GPL, AGPL, LGPL, MPL) without explicit discussion in an issue first. This is especially important for repos migrating to Apache 2.0.
- Do not introduce new dependencies without discussion in an issue first
- Conventional Commits are enforced by CI
- Translations must be submitted via Transifex, not as PRs
- This is a large, complex codebase with many interdependencies


## OSPO Policy Constraints

### GitHub Actions
- **Only** use actions owned by `owncloud`, created by GitHub (`actions/*`), verified on the GitHub Marketplace, or verified by the ownCloud Maintainers.
- Pin all actions to their full commit SHA (not tags): `uses: actions/checkout@<SHA> # vX.Y.Z`
- Never introduce actions from unverified third parties.

### Dependency Management
- Dependabot is configured for automated dependency updates.
- Review and merge Dependabot PRs as part of regular maintenance.
- Do not introduce new dependencies without discussion in an issue first.

### Git Workflow
- **Rebase policy**: Always rebase; never create merge commits. Use `git pull --rebase` and `git rebase` before pushing.
- **Signed commits**: All commits **must** be PGP/GPG signed (`git commit -S -s`).
- **DCO sign-off**: Every commit needs a `Signed-off-by` line (`git commit -s`).
- **Conventional Commits & Squash Merge**: Use the [Conventional Commits](https://www.conventionalcommits.org/) format where the repository enforces it. Many repos use squash merge, where the PR title becomes the commit message on the default branch — apply Conventional Commits format to PR titles as well. A reusable GitHub Actions workflow enforces this.

## Context for AI Agents
- Match existing code style
- Do not refactor unrelated code in the same PR
- Write tests for new functionality
- Keep PRs focused and atomic
- Use Conventional Commits format for all commit messages
- Be aware of the public API surface (OCP namespace) - breaking changes require careful consideration
- The `lib/private/` directory contains internal APIs; `lib/public/` contains the stable public API
