# Git Commit Message Skill

An AI agent skill that generates concise, informative Git commit messages following the Conventional Commits specification with Gitmojis.

## Installation

Install this skill using the skills CLI:

```bash
npx skills add nelwincatalogo/git-commit-message
```

## Usage

This skill helps AI agents generate well-structured commit messages based on your code changes. When you ask your AI agent to create a commit message, it will:

1. Analyze your git changes (staged and unstaged)
2. Determine the type of change (feat, fix, refactor, etc.)
3. Select an appropriate Gitmoji
4. Generate a commit message following Conventional Commits format

## Example

Ask your AI agent: "Create a commit message for my changes"

It will generate something like:

```
✨ feat(auth): implement magic link login

- Introduces passwordless authentication using magic links
- Improves UX by removing password requirements
- Adds `/auth/magic-link` endpoint
```

## Commit Types

- `feat` - New feature for users
- `fix` - Bug fix
- `refactor` - Code change that's neither fix nor feature
- `perf` - Performance improvement
- `style` - UI/formatting changes (no logic change)
- `test` - Adding/updating tests
- `docs` - Documentation only
- `chore` - Build process, dependencies, maintenance
- `ci` - CI configuration changes
- `build` - Build system or dependency changes
- `revert` - Reverting previous commit

## Gitmojis

This skill includes a comprehensive Gitmoji reference table with 50+ emojis for different scenarios, from new features (✨) to breaking changes (💥).

## License

MIT
