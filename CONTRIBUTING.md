# Contributing

This is the independently maintained [hiadamhere/MAUI-Designer](https://github.com/hiadamhere/MAUI-Designer)
fork of [GMPrakhar/MAUI-Designer](https://github.com/GMPrakhar/MAUI-Designer).
Preserve upstream attribution and read [AGENTS.md](AGENTS.md) for the shared
engineering standards.

## Review and commits

- Keep each branch and commit focused on one reviewable change. Use descriptive
  commit messages explaining the resulting behavior or correction.
- Inspect `git status`, `git diff --check`, and the full diff before staging.
  Stage explicit paths, then inspect `git diff --cached` before committing.
- Include the problem, resulting behavior, validation evidence, and material
  limitations in a pull request. Add screenshots when they help review UI changes.
- Address review findings and rerun checks affected by subsequent changes.
- Do not force-push shared branches, rewrite upstream history, or include unrelated
  generated files, machine settings, credentials, or private automation material.

For agent work in the maintainer's checkout, the initial review happens locally
before commits unless local commits are explicitly authorized. Pushing, opening
PRs, merging, tagging, deployment, and publication each require authorization for
the reviewed scope. Test results alone do not authorize publication.

## Branch and release flow

1. Create feature branches from `develop` and merge completed work back into `develop`.
2. Test the integrated `develop` branch.
3. After explicit approval, open a pull request from `develop` to `main`.
4. Merge the pull request only after its required checks pass.
5. Create `native-v*` and `vsix-v*` release tags from the resulting `main` commit.

Do not commit feature work directly to `main`, create a release tag from
`develop`, or publish release artifacts before the `develop` changes have been
approved and promoted through a pull request.

Both release workflows verify that their tagged commit is reachable from
`origin/main` before building or publishing an artifact.

Review the workflows before an approved push: the Pages workflow responds to
`main` and `master`, and the release workflows respond to release tags. The VSIX
workflow can also publish through a manual dispatch with a tag. These triggers
are part of the publication scope to review.

## Validation

Use the checked-in dependency files and CI workflows as the source for tooling
versions. Keep lockfiles reproducible; do not delete them to work around a failed
install. Run the checks for each affected component and any shared integration.

### Web designer

From the repository root, using the Node.js version selected by
[web CI](.github/workflows/ci.yml):

```sh
npm ci
npm run build
npm run test:headless
npx playwright install chromium
npm run e2e
```

The unit suite requires Chrome; the end-to-end suite uses Playwright Chromium.
For UI changes, also run `npm start` and exercise the affected designer interactions.
There is currently no configured lint script; do not report compilation as linting.

### Visual Studio extension

```sh
dotnet test extension/MauiDesigner.Core.sln --configuration Release
```

This covers core tests and the VSIX source compile check. Packaging, installation,
and embedded-window interactions require separate Windows/Visual Studio validation;
see [extension/README.md](extension/README.md).

### Native Windows designer

Use Windows, the .NET 10 SDK, and the MAUI Windows workload as described in the
[native app guide](maui-designer-native/README.md). From the repository root:

```sh
dotnet test maui-designer-native/MAUIDesigner.Fresh.Core.Tests/MAUIDesigner.Fresh.Core.Tests.csproj -c Release
dotnet test maui-designer-native/MAUIDesigner.Fresh.App.Tests/MAUIDesigner.Fresh.App.Tests.csproj -c Release -r win-x64 -p:PublishReadyToRun=false
dotnet build maui-designer-native/MAUIDesigner.Fresh.App/MAUIDesigner.Fresh.App.csproj -c Release
```

For UI changes, launch the native app and inspect the affected interactions.
Report unavailable prerequisites and checks not run explicitly.

### Documentation

Check relative links, referenced paths, examples, and `git diff --check`.
Documentation-only changes do not need application test runs unless they also
change executable behavior.
