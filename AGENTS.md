# Repository engineering standards

These instructions apply throughout the repository. Read [CONTRIBUTING.md](CONTRIBUTING.md)
and the relevant component README before editing. Resolve API and tooling questions
from the checked-in dependency versions, configuration, and implementation.

## Scope and ownership

- Confirm the checkout, branch, status, and requested scope before making changes.
- Preserve unrelated edits and untracked files. Do not reset, clean, or overwrite
  another contributor's work.
- Work on a focused branch from `develop`. Do not commit directly to `develop` or
  `main`. Preserve upstream history and attribution.
- For maintainer-directed agent work, present local changes for review before
  committing unless local commits have explicitly been authorized. Obtain explicit
  approval before pushing, opening a pull request, merging, tagging, deploying, or
  publishing. Approval covers the reviewed scope; later changes need renewed review.
- Do not launch additional agents unless the maintainer requests delegation.

## Code quality

- Make the smallest cohesive change that solves the problem. Keep unrelated
  refactors, dependency updates, generated output, and formatting out of the diff.
- Follow `.editorconfig` and the conventions of the component being changed.
  Prefer clear names and simple control flow. Explain non-obvious constraints.
- Keep domain and document operations separate from UI and host integration.
  Introduce abstractions for concrete needs, with explicit ownership and contracts.
- Validate data at file, protocol, persistence, and user-input boundaries. Handle
  errors explicitly; preserve a valid document when an edit or import fails.
- Preserve XAML round-trip data, namespaces, unknown constructs, and undo/redo
  semantics. Test compatibility boundaries when changing parsing or serialization.
- Keep asynchronous work observable and cancellable where appropriate; release
  subscriptions, event handlers, streams, and native resources with their owners.
- Respect UI thread affinity. In the Visual Studio extension, use the owning
  `AsyncPackage`'s `JoinableTaskFactory` for work tied to package lifetime and retain
  the existing threading analyzers.
- Preserve keyboard access, focus behavior, accessible labels, and test selectors
  when changing UI. Check interactions at relevant viewport sizes and DPI settings.
- Never silence a failing check or weaken assertions just to obtain a passing run.
  Fix the cause or report the limitation with evidence.

## Validation and reporting

- Use the commands in [CONTRIBUTING.md](CONTRIBUTING.md). Check available tooling
  before claiming a build or runtime scenario is supported locally.
- Add regression coverage for bug fixes and meaningful behavior coverage for new
  features. Exercise failure paths and boundary cases, not just implementation details.
- For UI changes, inspect the running affected application as well as automated
  results. A compile check does not establish visual or interaction correctness.
- For documentation-only edits, check the diff, links, paths, and command accuracy;
  application tests are needed only if executable behavior is affected.
- Report what changed, why, the exact validation performed and its outcome, and
  any checks not run. Distinguish compilation, tests, runtime checks, and publication.
- Inspect the complete diff and staged files before a commit. Stage explicit paths.
  Do not force-add ignored content or rewrite shared history.

## Public contribution boundary

- The public checkout must contain the source, documentation, configuration, and
  tooling needed to build, test, and maintain the application from a fresh clone.
- Personal automation must remain optional. Do not make builds or CI depend on
  private prompts, skills, services, local paths, or unpublished orchestration.
- Do not commit credentials, machine-local configuration, transcripts, or private
  planning and orchestration material. Review generated docs, logs, screenshots,
  commit messages, and PR text for unintended disclosure as well as source files.
- Publish reusable agent skills only when explicitly selected for inclusion,
  reviewed for disclosure and licensing, and useful to public contributors.
- Preserve license files and applicable attribution when modifying inherited work.
