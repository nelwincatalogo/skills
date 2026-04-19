---
name: git-commit-message
description: Generate concise, informative Git commit messages following Conventional Commits specification with Gitmojis. Use when the user wants to create a git commit message, needs help writing commit messages based on their changes, or asks for commit message suggestions for staged/unstaged files.
---

# Git Commit Message Generator

Generate commit messages based on code changes following Conventional Commits specification with Gitmojis.

## Workflow

1. **Gather Context** - Run git commands to understand the changes
2. **Analyze Changes** - Determine the purpose and type of changes
3. **Generate Message** - Create commit message following the format

## Step 1: Gather Context

Run these git commands to understand the changes:

```bash
git status --short
git --no-pager diff --staged
git --no-pager diff
```

## Step 2: Analyze the Diffs

Read through all diffs (staged and unstaged) to identify:
- **Purpose**: Adding feature? Fixing bug? Refactoring? Improving performance?
- **Scope**: Which part of codebase is affected (api, auth, ui, config, etc.)
- **Impact**: Any breaking changes?

## Step 3: Select Commit Type

| Type | Use When |
|------|----------|
| `feat` | New feature for users |
| `fix` | Bug fix |
| `refactor` | Code change that's neither fix nor feature |
| `perf` | Performance improvement |
| `style` | UI/formatting changes (no logic change) |
| `test` | Adding/updating tests |
| `docs` | Documentation only |
| `chore` | Build process, dependencies, maintenance |
| `ci` | CI configuration changes |
| `build` | Build system or dependency changes |
| `revert` | Reverting previous commit |

## Step 4: Choose Gitmoji

| Gitmoji | Code | Type | Use Case |
|:-------:|:-----|:----:|----------|
| ✨ | `:sparkles:` | `feat` | New feature |
| 🐛 | `:bug:` | `fix` | Bug fix |
| 🚑️ | `:ambulance:` | `fix` | Critical hotfix |
| ⚡️ | `:zap:` | `perf` | Performance improvement |
| 🚀 | `:rocket:` | `chore` | Deploy stuff |
| ♻️ | `:recycle:` | `refactor` | Refactor code |
| 🎨 | `:art:` | `refactor`, `style` | Improve structure/format |
| 🔥 | `:fire:` | `refactor`, `chore` | Remove code/files |
| 💄 | `:lipstick:` | `style` | Add/update UI and style files |
| 📝 | `:memo:` | `docs` | Add/update documentation |
| 💡 | `:bulb:` | `docs` | Add/update comments |
| 📄 | `:page_facing_up:` | `docs` | Add/update license |
| 👥 | `:busts_in_silhouette:` | `docs` | Add/update contributor(s) |
| ✅ | `:white_check_mark:` | `test` | Add/update/pass tests |
| 🤡 | `:clown_face:` | `test` | Mock things |
| 🧪 | `:test_tube:` | `test` | Add a failing test |
| 🔧 | `:wrench:` | `chore` | Add/update configuration files |
| 🔨 | `:hammer:` | `chore` | Add/update development scripts |
| 📦️ | `:package:` | `build` | Add/update compiled files or packages |
| ➕ | `:heavy_plus_sign:` | `build` | Add a dependency |
| ➖ | `:heavy_minus_sign:` | `build` | Remove a dependency |
| ⬆️ | `:arrow_up:` | `build`, `ci` | Upgrade dependencies |
| ⬇️ | `:arrow_down:` | `build`, `ci` | Downgrade dependencies |
| 📌 | `:pushpin:` | `build` | Pin dependencies to specific versions |
| 💚 | `:green_heart:` | `ci` | Fix CI Build |
| 👷 | `:construction_worker:` | `ci` | Add/update CI build system |
| 🚨 | `:rotating_light:` | `style` | Fix compiler/linter warnings |
| 🔒 | `:lock:` | `feat`, `fix` | Fix security or privacy issues |
| 🔐 | `:closed_lock_with_key:` | `feat`, `fix` | Add/update secrets |
| ♿️ | `:wheelchair:` | `feat`, `fix` | Improve accessibility |
| 🚚 | `:truck:` | `chore`, `refactor` | Move/rename resources |
| 🎉 | `:tada:` | `feat` | Begin a project |
| 💥 | `:boom:` | **Any** | Breaking changes |
| 🌐 | `:globe_with_meridians:` | `feat` | Internationalization and localization |
| 📱 | `:iphone:` | `feat` | Work on responsive design |
| 🍱 | `:bento:` | `feat` | Add/update assets |
| 💫 | `:dizzy:` | `feat` | Add/update animations and transitions |
| 🛂 | `:passport_control:` | `feat` | Authorization, roles, permissions |
| 🧑‍💻 | `:technologist:` | `feat` | Improve developer experience |
| ✈️ | `:airplane:` | `feat` | Improve offline support |
| 🦖 | `:t-rex:` | `feat` | Backwards compatibility |
| 🚸 | `:children_crossing:` | `feat` | Improve user experience/usability |
| 🏗️ | `:building_construction:` | `refactor` | Make architectural changes |
| 🗑️ | `:wastebasket:` | `refactor` | Deprecate code |
| ⚰️ | `:coffin:` | `refactor` | Remove dead code |
| ✏️ | `:pencil2:` | `fix` | Fix typos |
| 🩹 | `:adhesive_bandage:` | `fix` | Simple fix for non-critical issue |
| 🥅 | `:goal_net:` | `fix` | Catch errors |
| 👽️ | `:alien:` | `fix` | Update code due to external API changes |
| 🗃️ | `:card_file_box:` | `chore` | Database related changes |
| 🔊 | `:loud_sound:` | `chore` | Add/update logs |
| 🔇 | `:mute:` | `chore` | Remove logs |
| 🏷️ | `:label:` | `chore` | Add/update types |
| 🌱 | `:seedling:` | `chore` | Add/update seed files |
| 🩺 | `:stethoscope:` | `chore` | Add/update healthcheck |
| 🧱 | `:bricks:` | `chore` | Infrastructure related changes |
| 🙈 | `:see_no_evil:` | `chore` | Add/update .gitignore file |
| ⏪️ | `:rewind:` | `revert` | Revert changes |
| 🔀 | `:twisted_rightwards_arrows:` | `chore` | Merge branches |
| 🚧 | `:construction:` | - | Work in progress |
| 📈 | `:chart_with_upwards_trend:` | `feat` | Add/update analytics |
| 🔖 | `:bookmark:` | `chore` | Release / Version tags |

## Step 5: Craft the Message

**Format:** `<gitmoji> type(scope): description`

**Subject Line Rules:**
- Use imperative mood ("add", "fix", "change" NOT "added", "fixed")
- Keep under 50 characters
- Do NOT end with a period

**Body Rules (for significant changes):**
- Separate subject from body with blank line
- Explain the **"why"**, not the "how"
- Use bullet points (`-` or `*`)
- For breaking changes: Start paragraph with `BREAKING CHANGE:`

## Output Format

Commit message only, no explanations.

**Example:**

```
✨ feat(auth): implement magic link login

- Introduces passwordless authentication using magic links
- Improves UX by removing password requirements
- Adds `/auth/magic-link` endpoint

BREAKING CHANGE: `loginWithPassword` is deprecated, use `loginWithMagicLink`
```

## Important Notes

- Don't create commit_message.txt files
- Consider both staged AND unstaged changes
- Output ONLY the commit message, no explanations
- Don't commit unless explicitly asked
