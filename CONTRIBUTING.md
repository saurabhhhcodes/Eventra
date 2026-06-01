# Contributing to Eventra

Thank you for contributing to Eventra.

This guide explains how to set up your environment, propose changes, and open high-quality pull requests.

## Code of Conduct

Please read and follow [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

We expect all collaboration to be respectful, inclusive, and constructive.

## Before You Start

Read these docs first:

- [Architecture and Roles](docs/ARCHITECTURE_AND_ROLES.md)
- [Environment Setup Guide](docs/ENV_SETUP_GUIDE.md)
- [Frontend Onboarding](docs/frontend-onboarding.md)

These cover project structure, permissions, and local setup patterns used in this repository.

## Prerequisites

- Node.js `>=22.x`
- npm `>=9.6.4`
- Git

## Local Setup

1. Fork the repository on GitHub.
2. Clone your fork and install dependencies:

```bash
git clone https://github.com/<your-username>/Eventra.git
cd Eventra
npm install
```

3. Copy environment variables:

```bash
cp .env.example .env
```

4. Start development server:

```bash
npm run dev
```

The app runs on `http://localhost:3000`.

## Development Workflow

1. Sync your fork with upstream.
2. Create a focused branch:

```bash
git checkout -b feature/short-description
```

3. Make your changes in small, reviewable commits.
4. Run quality checks locally:

```bash
npm run lint
npm test
```

5. Run E2E tests when your change affects key flows:

```bash
npm run test:e2e
```

6. Push your branch and open a pull request.

## Coding Standards

- Prefer functional React components and hooks.
- Keep components modular and reusable.
- Reuse existing utilities/hooks before creating new ones.
- Keep naming explicit and consistent with nearby code.
- Update docs when behavior or setup changes.
- Use ESLint and Prettier conventions used in the repo.

## Testing Expectations

- Add or update tests for meaningful behavior changes.
- Cover edge cases for bug fixes.
- Keep test names clear and behavior-focused.
- Do not merge changes that break lint or tests.

## Storybook Component Testing Standards

Storybook is the fastest way to review isolated UI states before they reach a route-level page. Eventra already keeps Storybook configuration in `.storybook/` and component stories near the related component, such as `src/components/Button.stories.jsx` and the shared `src/components/common/*.stories.jsx` examples.

### When to Add or Update Stories

Add or update a Storybook story whenever your PR changes a reusable UI component, shared layout state, empty/loading/error state, or interaction pattern that can be reviewed without a backend request. A good story should make the intended UI state obvious to reviewers and future contributors.

Prioritize stories for:

- reusable components in `src/components/`
- loading, empty, error, success, and permission states
- responsive variants that can break on mobile
- accessibility-sensitive controls such as buttons, dialogs, forms, dropdowns, and navigation
- visual regressions that are hard to catch from unit tests alone

### Story File Conventions

- Place stories next to the component or inside the matching shared component folder.
- Name files as `ComponentName.stories.jsx`.
- Use a clear `title`, for example `Components/Button` or `Components/Common/Loading`.
- Export small named stories such as `Default`, `Loading`, `Error`, `Empty`, `Mobile`, or `WithLongContent`.
- Keep story data realistic but safe. Do not include real user tokens, private emails, API keys, or production secrets.
- Prefer props and mock data over network calls. Stories should render deterministically.

### Required Story States

For each changed reusable component, cover the states that reviewers need to trust the UI:

- default state with normal content
- long text or crowded content state when layout can wrap
- disabled or loading state when the component supports it
- error or empty state when the component represents fallback UI
- keyboard and accessibility-relevant state for controls, modals, menus, and forms

If a component has only one valid state, mention that in the PR description so reviewers know the smaller story surface is intentional.

### Accessibility and Interaction Checks

Before opening a PR, review the story in Storybook and check:

- interactive elements have visible focus states
- icon-only buttons have accessible names
- text has enough contrast against the background
- content does not overflow at narrow viewport widths
- controls work with keyboard navigation where applicable
- animations do not hide content from review screenshots

Use the Storybook a11y addon when available and fix warnings caused by your change. If an existing warning is outside your PR scope, document it clearly in the PR.

### Local Storybook Commands

Run the Storybook workflow when your PR touches reusable UI:

```bash
npm run storybook
```

For CI-style validation of the static Storybook build:

```bash
npm run build-storybook
```

If Storybook cannot run locally because of an environment or dependency issue, include the error and the fallback checks you ran in the PR description.

### PR Review Checklist for UI Stories

Before requesting review, confirm:

- the story file name and title match the component location
- changed visual states are represented in stories
- mock data is local, deterministic, and non-sensitive
- the story renders without relying on live APIs
- `npm run build-storybook` passes, or the blocker is documented
- screenshots are attached when the change is visual and reviewer-facing

These standards keep Eventra's component library easier to review, safer to refactor, and friendlier for new GSSoC contributors.

## Commit Message Guidelines

Use Conventional Commit style where possible:

- `feat:` new feature
- `fix:` bug fix
- `docs:` documentation-only changes
- `refactor:` internal cleanup without behavior changes
- `test:` test additions/updates
- `chore:` tooling or maintenance

Examples:

- `feat: add event search badge filter`
- `fix: prevent stale state update in event details`
- `docs: update env setup notes for SSE`

## Pull Request Guidelines

Include these in your PR:

- What changed
- Why it changed
- Related issue (for example: `Closes #123`)
- Test evidence (commands run, screenshots if UI changes)

Before requesting review:

- Rebase or merge latest default branch changes (currently `master`)
- Resolve merge conflicts
- Ensure lint/tests pass locally
- Keep PR scope focused

## Issue Assignment Policy

This repository runs an automation workflow that unassigns stale issues.

- Threshold is 7 days by default.
- If you are assigned an issue, open a draft PR within that window to keep assignment active.
- If you need more time, comment on the issue and request reassignment.

Reference workflow:
- [.github/workflows/auto-unassign-stale-issues.yml](.github/workflows/auto-unassign-stale-issues.yml)

## Automated PR Labels

PR labels are applied automatically by workflows:

- Type labels: `.github/workflows/type-labeler.yml` (`type:*`)
- Quality labels: `.github/workflows/quality-labeler.yml` (`quality:*`)
- Difficulty labels: `.github/workflows/difficulty.yml` (`level:*`)

You do not need to set these manually.

## Getting Help

- Open an issue for bugs or feature requests.
- Use GitHub Discussions (if enabled) for questions and ideas.
- For project-specific clarifications, tag maintainers in the PR or issue thread.

## Security

Do not commit secrets, tokens, or private keys.

If you discover a security issue, follow [SECURITY.md](SECURITY.md).
