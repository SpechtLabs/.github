# .github

The SpechtLabs organization's default community health files and its
profile page.

GitHub uses the files here for every SpechtLabs repository that doesn't have
its own copy:

- [`CONTRIBUTING.md`](./CONTRIBUTING.md): how to set up the tools, and how
  pull requests become commits and releases.
- [`SECURITY.md`](./SECURITY.md): how to report a vulnerability.
- [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md)
- [`.github/ISSUE_TEMPLATE/`](./.github/ISSUE_TEMPLATE) and
  [`.github/pull_request_template.md`](./.github/pull_request_template.md):
  the issue forms and the pull request template.

A repository that adds its own copy of any of these, or its own
`.github/ISSUE_TEMPLATE` directory, replaces the default entirely; GitHub
doesn't merge the two.

[`profile/README.md`](./profile/README.md) is the page shown on
<https://github.com/SpechtLabs>.

The workflow in `.github/workflows/` lints this repository only; GitHub never
runs an organization's `.github` workflows in its other repositories.
