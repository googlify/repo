# Team Git Workflow Rules

Follow these steps for every task to avoid merge conflicts and keep our repo clean.

## 1. Pull from `feature` branch before you start work

Always sync first so you start from the latest code:

```
git checkout feature
git pull origin feature
git checkout -b your-branch-name
```

## 2. Keep your branch short-lived

Push your work and open a PR to `feature` branch as soon as it's ready.

## 3. Follow the team's commit/merge message format

Use the agreed format for every commit and merge message, so history stays consistent and easy to follow.

**Structure of Commit Message:**

```
<type>(<scope>): <short summary>

<optional body>

<optional footer>
```

**Common types:**

- `feat` – a new feature
- `fix` – a bug fix
- `docs` – documentation only changes
- `style` – formatting, no code logic change
- `refactor` – code change that neither fixes a bug nor adds a feature
- `test` – adding or fixing tests
- `chore` – build process, tooling, dependency updates

**Rules:**

1. Keep the summary line short (ideally under 50 chars, 72 max).
2. Use the imperative mood — "Add login validation", not "Added" or "Adds".
3. One logical change per commit.
4. Explain _why_, not just _what_, in the body when the reasoning isn't obvious at summary.
5. Separate summary and body with a blank line.

**Example:**

```
feat(search): add filter for direct flights only

Users had to scroll through connecting flights to find direct
ones. Added a toggle in the search filters panel to show only
non-stop results.


feat(search): add multi-city flight search option

feat(booking): allow date range selection for hotel stays

feat(payment): add Apple Pay as checkout option (TRAVEL-214)

feat(notifications): send booking confirmation email after payment success
```

```
fix(pricing): correct fare total when adding infant passenger

Infant fares were being calculated using the adult tax rate,
inflating the total price by ~15%. Now applies the correct
infant tax bracket from the fare rules API.


fix(booking): prevent seat selection after payment is submitted

A race condition allowed users to change their seat via the
back button after payment had already processed, causing a
mismatch between the ticket and the boarding pass.

```

```
refactor(search): extract fare comparison logic into separate module

Fare comparison logic was duplicated across the search results
page and the price alert feature. Consolidating it into one
module makes future fare rule changes easier to maintain.

refactor(checkout): simplify passenger form validation

```

```
chore(deps): upgrade duffle flight API client to v3.2

BREAKING CHANGE: response format for multi-city search changed
from array to object keyed by segment ID. Updated all callers
accordingly.
```

```
docs(api): document baggage allowance query parameters

```

```
test(pricing): add test cases for round-trip fare with layover taxes

Covers previously untested edge case where layover country
adds its own departure tax on top of the base fare.
```

## 4. Notify before touching shared or a coworker's files

If you need to change a shared file or something someone else is working on, post a heads-up on the team communication channel first. This prevents two people editing the same area at the same time.

## 5. Use the agreed PR template when requesting a merge

Fill in the team's PR template completely before requesting a merge, so reviewers have what they need and nothing gets missed.

## 6. Pull from `feature` into your branch again before opening your PR

If your branch has been open more than a day, pull the latest `feature` into it again before requesting a merge — don't rely only on step 1:

```
git checkout your-branch-name
git pull origin feature
```

## 7. Resolve conflicts locally, not in the GitHub web UI

If a conflict comes up after pull request, fix it in your own editor, test it, then push — safer than resolving directly on GitHub.

## 8. Don't run the formatter/linter on code that isn't yours

Only format the files or lines you actually changed. Running a formatter across the whole file or project reformats other people's code too, creating noise in the diff and near-guaranteed conflicts with their work.

---

## High-Risk Files (extra caution / notify before editing)

These files are common conflict hotspots — treat step 4 (notify before editing shared files) as mandatory for these:

**Config & environment**

- Tool/IDE config (`.eslintrc`, `tsconfig.json`)
- Environment/config files (`.env`, `config.yml`)
- CI/CD pipeline files (`.github/workflows/*.yml` )

**Dependency & build files**

- Lock files (`package-lock.json`)
- Build/dependency manifests (`package.json`)

**Database & schema**

- Database entity/model files, especially schema definitions
- Migration files
- ORM mapping files

**Documentation & metadata**

- `README.md`, `CHANGELOG.md`

## Quick checklist before requesting a merge

- [ ] Pulled latest `feature` before starting
- [ ] Branch is short-lived and up to date with `feature`
- [ ] Commit/merge messages follow team format
- [ ] Notified team before touching shared files
- [ ] PR template filled out completely
- [ ] Formatter/linter only run on your own changed files
