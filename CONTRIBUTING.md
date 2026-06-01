# 🤝 Contributing to Eventra 🎉

Thank you for your interest in contributing to **Eventra** — a modern event management platform built for **builders**, **communities**, and **creators**.  
We’re thrilled to have you on board! 🚀

This guide will help you understand how to contribute effectively, maintain high-quality standards, and collaborate seamlessly with our community.

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [Ways to Contribute](#-ways-to-contribute)
- [Development Workflow](#-development-workflow)
- [Code Standards](#-code-standards)
- [Storybook Component Testing Standards](#-storybook-component-testing-standards)
- [Frontend Guidelines](#-frontend-guidelines)
- [Backend Guidelines](#-backend-guidelines)
- [Commit Message Guidelines](#-commit-message-guidelines)
- [Pull Request Process](#-pull-request-process)
- [Getting Help](#-getting-help)

---

## 📜 Code of Conduct

At **Eventra**, we believe that collaboration thrives in a respectful, inclusive, and supportive community.  
Our goal is to ensure that every contributor feels valued and safe while participating in this project.

Before contributing, please take a moment to read our full [**Code of Conduct**](CODE_OF_CONDUCT.md).  
By participating, you agree to uphold these principles and help us maintain a positive environment for everyone.

**Key principles:**

- 💬 **Be respectful:** Treat everyone with kindness and empathy.
- 🤝 **Be inclusive:** Embrace diversity and welcome new voices.
- 🌱 **Be constructive:** Offer helpful feedback and focus on solutions.
- 🛡️ **Be professional:** Avoid harassment, personal attacks, or discriminatory behavior.

Together, we can make **Eventra** a safe and inspiring space for all contributors. ✨

---

## 🌟 Ways to Contribute

You can help improve Eventra in several ways:

- **Reporting Bugs** – Open an issue with detailed reproduction steps.
- **Suggesting Features** – Share ideas that can make Eventra even better.
- **Improving Documentation** – Fix typos, add missing explanations, or improve clarity.
- **Code Contributions** – Add new features, fix bugs, or improve existing code.
- **UI/UX Enhancements** – Improve the design, animations, and user experience.

---

## 🏗️ Understanding Eventra Architecture

**Before you start coding**, take a few minutes to understand how Eventra works:

📖 **[Architecture & Roles Guide](docs/ARCHITECTURE_AND_ROLES.md)** provides:
- 🧬 Complete system architecture overview
- 👥 Role-Based Access Control (RBAC) with 5 roles
- 🎟️ Event lifecycle stages
- 🔐 Authentication & route protection
- 📍 Contributor code map showing where to implement features
- 💡 Common tasks and where to find relevant code

**Key Topics for Contributors:**
- **Adding a new permission?** → See [RBAC Section](docs/ARCHITECTURE_AND_ROLES.md#-role-based-access-control-rbac)
- **Changing event workflow?** → See [Event Lifecycle](docs/ARCHITECTURE_AND_ROLES.md#-event-lifecycle-system)
- **Implementing hackathon features?** → See [Hackathon Hub](docs/ARCHITECTURE_AND_ROLES.md#-hackathon-hub-workflow)
- **Confused about auth?** → See [Authentication Flow](docs/ARCHITECTURE_AND_ROLES.md#-route-protection--authentication-flow)
- **Want to contribute to a specific area?** → See [Contributor Code Map](docs/ARCHITECTURE_AND_ROLES.md#-contributor-notes--code-map)

---

## 🛠️ Development Workflow

1. **Fork the Repository**
   ```bash
   git fork https://github.com/SandeepVashishtha/Eventra.git
   cd Eventra
   ```
2. Create a Feature Branch

```bash
git checkout -b feature/amazing-feature
```

3. Make Your Changes
   Follow the code standards and test your changes locally.
4. Commit Your Changes

```bash
git commit -m "feat: add amazing feature"
```

5. Push to Your Branch

```bash
git push origin feature/amazing-feature
```

6. Open a Pull Request
   Submit a PR with a clear description of your changes.

## 🧩 Code Standards

Maintaining consistent coding standards ensures readability, maintainability, and collaboration across **Eventra**.

---

### 🎨 Frontend Standards

- Use **functional components** with **React Hooks** for state and lifecycle management.
- Follow modern **React best practices**, including component composition and context usage.
- Keep components **small, reusable, and modular**.
- Maintain a consistent **UI/UX design**, ensuring accessibility and responsiveness across devices.
- Store configuration and constants separately (e.g., `src/config`) to maintain clean code.
- Use **ESLint + Prettier** to enforce consistent code style and formatting.

## 🧪 Testing

Proper testing ensures that our features are reliable and maintainable. Please follow these guidelines:

- Write **unit** and **integration tests** for all new features and critical fixes.
- Test thoroughly before submitting your PR to ensure everything works as expected.
- Use descriptive test names and cover edge cases whenever possible.
- Ensure tests pass consistently in both local and CI environments.

---

## 📚 Storybook Component Testing Standards

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
- keyboard/a11y-relevant state for controls, modals, menus, and forms

If a component has only one valid state, mention that in the PR description so reviewers know the smaller story surface is intentional.

### Accessibility and Interaction Checks

Before opening a PR, review the story in Storybook and check:

- interactive elements have visible focus states
- icon-only buttons have accessible names
- text has enough contrast against the background
- content does not overflow at narrow viewport widths
- controls work with keyboard navigation where applicable
- animations do not hide content from review screenshots

Use the Storybook a11y addon when available and fix warnings that are caused by your change. If an existing warning is outside your PR scope, document it clearly in the PR.

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

---

## 📖 Documentation

Good documentation helps other contributors understand and use your code effectively:

- Update the **README** or project documentation for any new features or changes.
- Add **inline comments** where necessary to clarify complex logic.
- Keep documentation concise, clear, and up to date with code changes.

---

## 🎨 Frontend Guidelines

### 🛠 Tech Stack

- **React** 18.2.0
- **React Router DOM** for routing
- **Framer Motion** for animations

### 💻 Code Style

- Use **ESLint** + **Prettier** for consistent formatting.
- Store API configurations in `src/config/api.js`.
- Write modular, reusable components with proper naming conventions.

### 🌐 Environment

- Configure environment variables using a `.env` file.
- Refer to `.env.example` for required variables and structure.

---

## Commit Message Guidelines

We follow conventional commits:

- feat: – New feature
- fix: – Bug fix
- docs: – Documentation only changes
- style: – Code style changes (formatting, missing semicolons, etc.)
- refactor: – Code changes that neither fix a bug nor add a feature
- test: – Adding or updating tests
- chore: – Maintenance tasks

### 💡 Examples of Commit Messages

Here are some practical examples following our **Conventional Commits** guidelines:

- `feat: add leaderboard component` – Introduces a new feature.
- `fix: resolve API CORS issue` – Fixes a bug in the API handling.
- `docs: update contributing guidelines` – Updates documentation without affecting code.
- `style: format dashboard layout using Prettier` – Adjusts code style or formatting.
- `refactor: simplify event creation logic` – Refactors code without adding features or fixing bugs.
- `test: add integration tests for event routes` – Adds or updates tests.
- `chore: update dependencies and clean up scripts` – Routine maintenance tasks.

> ✅ Using these clear and descriptive messages keeps the git history readable and makes collaboration easier.

## 🚀 Pull Request Process

Submitting a pull request (PR) is how you share your awesome work with the **Eventra** community!  
To make the review process smooth and efficient, please follow these steps:

1. **Sync your branch**
   - Ensure your feature or fix branch is up to date with the latest `main` branch.
   - Resolve any merge conflicts before opening your PR.

2. **Describe your changes clearly**  
   In your PR description, please include:
   - 🧩 **Problem Solved:** What issue or feature does this address?
   - 💡 **Approach:** How did you solve it? Mention tools, libraries, or patterns used.
   - 🔗 **Related Issues:** Reference any related issues (e.g., `Closes #123`).
   - 🧪 **Testing:** Describe how you tested your changes and include screenshots if applicable.

3. **Run all tests and checks**
   - Ensure that all unit, integration, and lint tests pass.
   - If new functionality is added, write appropriate tests.

4. **Follow coding conventions**
   - Use consistent formatting, naming, and structure as defined in our [Code Standards](#-code-standards).

5. **Request a review**
   - Assign at least one maintainer or tag a reviewer in your PR.
   - Be open to feedback and make revisions as needed.

6. **Wait for approval & merge**
   - Once approved, your PR will be merged by a maintainer. 🎉

---

## 💬 Getting Help

Need assistance or want to discuss ideas? We’re here to help!

- 🐞 **Issues:** Report bugs or request features.
- 💭 **Discussions:** Share ideas, ask questions, or connect with contributors.
- 📧 **Contact Maintainers:** For sensitive matters, reach out privately through the contact listed in the repository.

---

## 🎉 Final Note

Thank you for contributing to **Eventra**!  
Your time, ideas, and code make this project better for everyone.  
Together, we’re building a **modern, open, and collaborative event management platform** for the community. 🚀💙
