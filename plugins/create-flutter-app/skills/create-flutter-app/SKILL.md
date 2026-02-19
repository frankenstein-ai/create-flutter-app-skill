---
name: create-flutter-app
description: Create a new Flutter mobile app with up-to-date defaults for iOS and Android. Use when the user asks to create, scaffold, or initialize a new Flutter project.
disable-model-invocation: true
argument-hint: [project-name]
allowed-tools: Bash(flutter *), Bash(git *), Read, Edit, Write, Grep, Glob
---

Create a new Flutter mobile app named **$ARGUMENTS** using the following conventions and version defaults. Follow every step in order.

## Version Defaults (as of early 2026 — update when Flutter stable advances)

| Tool | Version |
|---|---|
| Flutter stable | latest (`flutter upgrade` to ensure) |
| Dart SDK constraint | `>=3.5.0 <4.0.0` |
| iOS deployment target | `16.0` |
| Android Kotlin | `2.2.20` (via settings.gradle.kts) |
| Android Gradle Plugin | `8.11.1` |
| Java compatibility | `17` |
| Android SDK | Flutter-managed (`flutter.minSdkVersion`, `flutter.targetSdkVersion`, `flutter.compileSdkVersion`) |

## Current Flutter Environment
`flutter --version 2>/dev/null || echo "FLUTTER_NOT_INSTALLED"`

If the output above shows `FLUTTER_NOT_INSTALLED`, stop and tell the user to install Flutter first (https://docs.flutter.dev/get-started/install).

## Steps

### 1. Determine project location

Ask the user where to create the project if not specified. Default to the current working directory.

### 2. Scaffold the project

Run:
```bash
flutter create --platforms=ios,android <project_name>
```

Do NOT include web, macOS, linux, or windows platforms unless explicitly requested.

### 3. Fix dot-shorthands in generated template

Flutter 3.38+ generates `lib/main.dart` using Dart's experimental "dot-shorthands" syntax (e.g., `.fromSeed(...)` instead of `ColorScheme.fromSeed(...)`, `.center` instead of `MainAxisAlignment.center`). This syntax requires an experimental flag and won't compile by default.

Read `lib/main.dart` and replace all dot-shorthand usages with their fully-qualified forms:
- `.fromSeed(` → `ColorScheme.fromSeed(`
- `mainAxisAlignment: .center` → `mainAxisAlignment: MainAxisAlignment.center`
- Any other `.shorthand` patterns where the type is omitted

Also scan `test/widget_test.dart` for the same issue and fix if needed.

### 4. Update iOS deployment target

In `ios/Runner.xcodeproj/project.pbxproj`, use the Edit tool to update all occurrences of `IPHONEOS_DEPLOYMENT_TARGET` to `16.0`.

Note: The new Flutter template does NOT generate a Podfile by default (uses Swift Package Manager). Do not create one unless a CocoaPods dependency requires it.

### 5. Clean up pubspec.yaml

Replace the generated `pubspec.yaml` using the template at
[templates/pubspec.yaml](templates/pubspec.yaml). Substitute `<project_name>`
and `<short description>` with actual values.

- Set `sdk: '>=3.5.0 <4.0.0'`
- Remove all boilerplate comments
- Keep `cupertino_icons`, `flutter_lints`, `flutter_test`
- Keep `uses-material-design: true`

### 6. Verify Android configuration

The new Flutter template uses `.gradle.kts` files. Check `android/settings.gradle.kts` for the Kotlin version. If it differs from `2.2.20`, update it. The `android/app/build.gradle.kts` should use Flutter-managed SDK versions — do NOT hardcode `minSdk`, `targetSdk`, or `compileSdk`.

### 7. Create CLAUDE.md

Create a `CLAUDE.md` in the project root using the template at
[templates/CLAUDE.md](templates/CLAUDE.md).

### 8. Initialize git

```bash
git init
git add .
git commit -m "Initial Flutter project setup for <project_name>

Blank Flutter app targeting iOS and Android only.

Configuration:
- iOS deployment target: 16.0
- Android: Kotlin 2.2.20, Gradle 8.11.1, Flutter-managed SDK versions
- Dart SDK: >=3.5.0 <4.0.0
- flutter_lints for static analysis

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>"
```

### 9. Confirm completion

Report back:
- Full path of the created project
- iOS deployment target applied
- Kotlin version in use
- Any deviations from the defaults above and why
- Next steps: `cd <project_name> && flutter run -d ios`

## Error Handling

- If `flutter create` fails, verify Flutter is installed (`flutter doctor`)
- If iOS config files are missing, the user may need to install Xcode first
- If Android config uses `.gradle` instead of `.gradle.kts`, the Flutter version may be outdated — advise `flutter upgrade`
