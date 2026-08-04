# Using These Skills

This repo is meant to make finance skills easy to inspect, install, update, and reuse.

## Choosing A Skill

Start with `DIRECTORY.md`. Pick the narrowest skill that matches the work:

- Use `cash-reconciliation-reporting` before `cfo-cash-dashboard` when cash has not yet been reconciled.
- Use `cfo-cash-dashboard` only after a reconciliation pack exists.
- Use `cash-flow-model-builder` for a simple first-pass 13-week forecast.
- Use `monthly-financial-review` for a guided MFR process and final HTML deck.
- Use `forensic-finance-investigation` when the numbers need skeptical cross-file investigation.
- Use `self-improving-finance` when improving the finance operating system itself. Its source folder is `skills/self-improving-finance-skill-pack/`.
- Use `cfo-board-prep` for board, lender, investor, audit committee, or finance committee preparation.
- Use `cfo-brain`, `cfo-memory`, `cfo-audit-trail`, and `cfo-quality-gate` as standalone CFO stack skills when that layer is needed directly.
- Use `born2cycle-monthly-snapshot` only for the governed Born2Cycle monthly snapshot.

## Installing Or Moving A Skill

Use the packaged bundle when the target environment accepts `.skill` files:

```text
packages/<skill-name>.skill
```

Use the extracted source when editing or reviewing:

```text
skills/<skill-name>/SKILL.md
```

If the skill has `assets/`, `templates/`, `resources/`, or `examples/`, keep those files with the `SKILL.md`. They are part of the skill, not optional notes.

Some CFO stack skills are source-only folders without a packaged `.skill` archive. Use their `skills/<skill-name>/SKILL.md` as the install source unless a packaged bundle is added later.

## Updating A Skill

1. Edit the extracted source under `skills/<skill-name>/`.
2. Update `DIRECTORY.md` if the skill's use case, inputs, outputs, or controls changed.
3. Rebuild the `.skill` package only after the source folder is correct.
4. Replace the matching file in `packages/`.
5. Verify the package inventory against the extracted folder before committing.

## Quality Rules

- Do not hardcode client data into generic skills.
- Keep governed templates unchanged unless the update is intentional.
- Preserve validation gates, source-of-truth rules, and stop-and-report policies.
- Treat example files as examples, not factual memory.
- Check for secrets before committing.

## Rebuilding A Package

Preserve the existing archive layout for each package. Check it first:

```sh
unzip -Z1 packages/cash-reconciliation-reporting.skill
```

Build to a new archive, inspect it, then replace the package. Do not update an existing zip in place; stale deleted files can remain inside the archive.

Most packages preserve a root folder inside the archive. For those, rebuild from the `skills/` parent:

```sh
pkg="$(mktemp /tmp/cash-reconciliation-reporting.XXXXXX.skill)"
cd skills
zip -qr "$pkg" cash-reconciliation-reporting/
cd ..
unzip -Z1 "$pkg"
mv "$pkg" packages/cash-reconciliation-reporting.skill
```

Current package layouts:

| Package | Rebuild pattern |
| --- | --- |
| `born2cycle-monthly-snapshot.skill` | root folder from `skills/born2cycle-monthly-snapshot/` |
| `cash-flow-model-builder.skill` | root folder from `skills/cash-flow-model-builder/` |
| `cash-reconciliation-reporting.skill` | root folder from `skills/cash-reconciliation-reporting/` |
| `cfo-cash-dashboard.skill` | root folder from `skills/cfo-cash-dashboard/` |
| `forensic-finance-investigation.skill` | rootless archive containing only `SKILL.md` |
| `monthly-financial-review.skill` | stage source under root folder `monthly-financial-review-skill/` before zipping |
| `self-improving-finance-skill-pack.zip` | ordinary zip package with root folder `self-improving-finance-skill-pack/` |

Rootless forensic rebuild:

```sh
pkg="$(mktemp /tmp/forensic-finance-investigation.XXXXXX.skill)"
cd skills/forensic-finance-investigation
zip -qr "$pkg" SKILL.md
cd ../..
unzip -Z1 "$pkg"
mv "$pkg" packages/forensic-finance-investigation.skill
```

Monthly financial review rebuild:

```sh
stage="$(mktemp -d /tmp/monthly-financial-review.XXXXXX)"
mkdir "$stage/monthly-financial-review-skill"
cp -R skills/monthly-financial-review/. "$stage/monthly-financial-review-skill/"
pkg="$(mktemp /tmp/monthly-financial-review.XXXXXX.skill)"
cd "$stage"
zip -qr "$pkg" monthly-financial-review-skill/
cd -
unzip -Z1 "$pkg"
mv "$pkg" packages/monthly-financial-review.skill
```

After rebuilding, compare the package inventory to the extracted folder before committing:

```sh
unzip -Z1 packages/<skill-name>.skill
find skills/<matching-source-folder> -type f | sort
```
