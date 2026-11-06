# FrizzBank QA

This repository is used to run and maintain quality-assurance checks for a
Flutter banking UI component library. The library provides reusable banking
widgets; this repository's tests check their behavior, accessibility,
localization, visual consistency, and design-token integrity.

The checks are automated evidence about this codebase. They are not an
independent audit and do not certify an application that uses the library.

## Run the QA checks

Install Flutter 3.44.4 (stable), then run these commands from the repository
root:

```shell
flutter pub get
dart format --output=none --set-exit-if-changed .
flutter analyze
dart run tool/generate_tokens.dart --check
flutter test --coverage
```

CI runs the same formatting, analysis, token-integrity, and test checks on
pushes and pull requests to `main`. It also builds the example app for web.
To run that build locally:

```shell
cd example
flutter pub get
flutter build web -t lib/screenshot_harness.dart --release --no-web-resources-cdn --no-tree-shake-icons
```

## What is covered

- Widget and model behavior across the banking UI components.
- Accessibility semantics, contrast, tap targets, reduced motion, and privacy
  masking. See the [Accessibility Conformance Report](doc/enterprise/acr/ACR.md)
  and its [machine-readable OpenACR source](doc/enterprise/acr/openacr.yaml).
- Theme and visual regression behavior across the built-in presets, light and
  dark modes, and left-to-right and right-to-left layouts.
- Design-token synchronization between the platform-neutral token data and
  generated Dart values.
- Dependency and supply-chain checks run by GitHub Actions.

Tests and reports describe the repository state at the time they were run.
Review the workflows and test sources before relying on any result, and run
the host application's own QA checks as well.

## Repository layout

- `lib/` — Flutter package source.
- `test/` — unit, widget, accessibility, and regression tests.
- `example/` — sample app and screenshot harness.
- `tokens/` — source design tokens and theme exports.
- `doc/enterprise/acr/` — accessibility conformance report and OpenACR data.
- `.github/workflows/` — CI and supply-chain workflows.

## Package

The package name remains `bank_ui_kit` so existing Dart imports and tests keep
working. See [`pubspec.yaml`](pubspec.yaml) for package metadata and
dependencies.

## License

The project is licensed under [GNU GPL version 3 or later](LICENSE).
Originally MIT-licensed material retains its applicable copyright and
permission notice in [`LICENSE-MIT`](LICENSE-MIT). Repository attribution is
summarized in [`NOTICE`](NOTICE).

## Create a clean GitHub repository

Create an empty repository at
[maureenobiekwe/frizz-bank](https://github.com/maureenobiekwe/frizz-bank)
without initializing it with a README, license, or `.gitignore`. To publish
the current files with a fresh Git history, make a clean copy that excludes
the existing `.git` directory, then run:

```powershell
robocopy . ..\frizz-bank-clean /E /XD .git
cd ..\frizz-bank-clean
git init -b main
git config user.name "Maureen Obiekwe"
git config user.email "YOUR_GITHUB_NOREPLY_EMAIL"
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/maureenobiekwe/frizz-bank.git
git push -u origin main
```

Replace `YOUR_GITHUB_NOREPLY_EMAIL` with the email shown in your GitHub
settings. GitHub will then show the new initial commit and its author, rather
than the old repository's commit history. Removing Git history does not remove
copyright or license obligations for code already included here.
