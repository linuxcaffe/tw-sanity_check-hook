# tw-sanity-check

Reviews and fixes common Taskwarrior inconsistencies interactively.

## Usage

```
tw-sanity-check           # Status: issue counts per condition
tw-sanity-check all       # Interactive review of all conditions
tw-sanity-check <name>    # Interactive review of one condition
```

Or via the `tw` wrapper:

```
tw checkup                # Status
tw checkup all            # Review all
```

## Conditions (default sanity.rc)

| Name | Description |
|------|-------------|
| `late-due` | Tasks past their due date |
| `late-sched` | Tasks with scheduled date in the past |
| `wait-after-due` | Wait date is after due (task hidden past due) |
| `until-before-due` | Until date is before due (task expires before due) |
| `wait-after-sched` | Wait date is after scheduled |
| `sched-after-due` | Scheduled date is after due |
| `orphans` | Blocked tasks whose dependency is no longer pending |
| `diag-check` | Issues reported by `task diag` |

## Interactive review

Each task is displayed with its dates and metadata. The fix prompt is
pre-filled with a suggested command (editable via readline):

```
  [12] Overdue report
       due:2026-02-01 (32d ago)
  (1/3  s=skip  d=done  q=quit)

  Fix > task 12 due:2026-03-15
```

- **Enter** (or edit and Enter) — run the command; advance if successful
- **s** — skip this task
- **d** — mark done
- **q** — quit the session

## Configuration

Edit `~/.task/config/sanity.rc` to add, remove, or customise conditions:

```ini
condition.NAME.description = Short description for status view
condition.NAME.filter       = +PENDING +OVERDUE
condition.NAME.msg          = Longer message shown during review
condition.NAME.sort         = due+          # optional; field± syntax
condition.NAME.action       = due:<due+7d>  # optional; pre-filled fix fragment
condition.NAME.type         = orphans       # optional; orphans | diag
```

Action templates support date arithmetic: `<due+7d>`, `<scheduled-2w>`, etc.

## Installation

```bash
bash sanity-check.install
```

Installs `tw-sanity-check` to `~/.task/scripts/` and `sanity.rc` to
`~/.task/config/`. Adds an `include` line to `~/.taskrc`.

## Files

| File | Installed to |
|------|-------------|
| `tw-sanity-check` | `~/.task/scripts/` |
| `sanity.rc` | `~/.task/config/` |

## Version

0.1.0 — Designed by linuxcaffe, implemented by Claude Code
