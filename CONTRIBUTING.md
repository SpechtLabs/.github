# Contributing to SpechtLabs projects

Thanks for helping out. This guide applies to every SpechtLabs repository
that doesn't ship a `CONTRIBUTING.md` of its own; where a repository has its
own guide or contributor docs, those come first.

Please read the [Code of Conduct](./CODE_OF_CONDUCT.md) before you take part,
and report security problems as [SECURITY.md](./SECURITY.md) describes, never
in a public issue.

## Set up the tools

Every repository pins its tools (Go, Node, Rust, linters, release tooling) to
exact versions in `.mise.toml`, and CI installs the same versions from it. Install
[mise](https://mise.jdx.dev), then, from the repository root:

```sh
mise trust
mise install
mise tasks        # what the repository can build, test and check
```

You don't need anything installed globally beyond mise itself.

## Before you open a pull request

```sh
mise run check
```

`check` is the definition of done: it runs every gate CI runs on a pull
request (linters, formatting checks, tests, builds), so a green `check`
locally means a green CI run. `mise run fmt`, where a repository has it,
fixes what the formatters can fix.

Repositories with Go code lint with golangci-lint and the
[golint-sl](https://github.com/SpechtLabs/golint-sl) plugin, built into a
local `custom-gcl` binary by `mise run lint`. Fix what it reports; if a rule
really doesn't fit, add a narrow exclusion to `.golangci.yaml` with a comment
that says why, rather than disabling the linter.

Dependencies are kept current by Renovate. Bump one by hand only when your
change needs the newer version.

## Branches

Start from `main` and name the branch after the kind of change, using the
Conventional Commit type as the prefix: `feat/signup-form`,
`fix/login-redirect`, `docs/install-guide`, `ci/cache-go-build`. The
`feat` and `fix` prefixes also label the pull request as an enhancement or a
bug. The commits on your branch can be as granular as you like; they are
squashed on merge.

## The pull request is the commit

Pull requests are squash-merged. The merge commit takes the **PR title as its
subject** and the **PR description as its body**, and
[release-please](https://github.com/googleapis/release-please) builds the
changelog and picks the next version from that commit. Write both for the
history, not for the reviewer of the day.

**The title** is a [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0/)
header; repositories with release automation check it on every pull
request:

```text
feat(cli): add a generate-config subcommand
fix(auth): keep the redirect target after an OAuth2 login
docs: explain the configuration file's lookup order
chore(deps): update module golang.org/x/net to v0.40.0
```

Choose the type by what users of the project see:

- `feat` adds something users can use, and `fix` repairs something they could
  hit. Both cut a release and get a changelog entry.
- `docs`, `ci`, `build`, `chore`, `refactor`, `test` and `style` don't cut a
  release and stay out of the changelog. Use them for tooling, CI and
  internal work, even when the change is large.
- `perf` and `revert` get a changelog entry too.

A breaking change adds `!` after the type or scope (`feat(api)!: ...`) and
ends the description with a `BREAKING CHANGE:` paragraph that says what
breaks and how to migrate. Before 1.0 a breaking change bumps the minor
version; afterwards, the major.

**The description** says what was wrong or missing, what you changed, and
why this way. A short code excerpt helps when the change is about code.
Leave out headings, checklists and anything that only matters during review:
it all ends up in the commit. Put `Closes #123` at the end to close an issue.

One trap: release-please reads any line that starts like `identifier(`, such
as `assert("x",` or `fix(` at the very beginning of a line, as a commit
footer, fails to parse the message, and silently drops the commit from the
changelog and the version bump. Indent such lines, or put a word in front of
them. The same pull request check catches it.

## Reporting bugs and asking for features

Open an issue in the repository the problem is in and pick the matching
template. For a bug, the version you run and the exact command or
configuration that triggers it save the most time.

## Questions

If something here is unclear or doesn't match what a repository actually
does, open an issue. That is a bug in this guide.
