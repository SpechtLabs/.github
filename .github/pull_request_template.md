<!--
This pull request is squash-merged: its title becomes the commit subject and
this description the commit body, and release-please builds the changelog
and the next version from them. CONTRIBUTING.md has the details.

Title: a Conventional Commit header, e.g. `fix(cli): keep --output when
--config is set`. feat and fix cut a release; docs, ci, build, chore,
refactor, test and style don't.

Description: what was wrong or missing, what changed, and why this way.
Add a short code excerpt where it helps. No headings or checklists: they
end up in the commit.

- No line may start like `identifier(` (e.g. `assert("x",`): release-please
  reads it as a footer and silently drops the commit. Indent it, or put a
  word in front.
- A breaking change: `!` in the title (`feat(api)!: ...`) and a final
  paragraph starting with `BREAKING CHANGE:` that says how to migrate.
- `Closes #123` at the end closes an issue.

Delete this comment before you open the pull request; everything in the
description lands in the commit message.
-->
