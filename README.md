# .github

Shared GitHub files for the repositories of [mazzsva](https://github.com/mazzsva).

## Xcode workflow

`.github/workflows/xcode.yml` lints, builds, and tests an Xcode project or a Swift package. Each repository calls it from its own `ci.yml`:

```yaml
jobs:
  xcode:
    name: Xcode
    uses: mazzsva/.github/.github/workflows/xcode.yml@v1.0.0
    with:
      scheme: Lexicon
      platform: iOS
      lint-paths: Lexicon LexiconTests
```

| Input | Default | Use |
|---|---|---|
| `scheme` | | The scheme to build and test |
| `platform` | | `iOS` tests on the iPhone 18 Pro simulator, and `macOS` tests on My Mac |
| `lint-paths` | | The paths that `swift format` lints |
| `metal-toolchain` | `false` | Installs the Metal Toolchain before the build |
| `integration-tests` | `false` | Runs `scripts/test-integration.sh` on the Firebase emulators |
| `example-project` | | The project of an example app to build |
| `example-scheme` | | The scheme of the example app |

- **Build once:** The unit tests and the integration tests run on one build.
- **Warnings:** A warning in the repository's own files fails the run. A warning in a package does not.
- **Packages:** xcodebuild uses only the versions in `Package.resolved`. A cache keeps them, and the run saves it right after it resolves the packages, so a later failure does not lose it.

## Pull request template

GitHub uses `.github/pull_request_template.md` for each repository that has no template of its own.

## Versions

Each repository pins a version, such as `v1.0.0`. Dependabot opens a pull request in each repository for a new version, so each repository tests the change before it uses it.

Copyright © 2026 Lorenzo Mazzarotto
