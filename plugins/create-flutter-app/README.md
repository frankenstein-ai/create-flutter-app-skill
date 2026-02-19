# create-flutter-app

A [Claude Code](https://claude.ai/code) plugin that scaffolds production-ready Flutter mobile apps targeting iOS and Android.

## Installation

```
/plugin marketplace add frankenstein-ai/agent-skills
/plugin install frankenstein-ai/create-flutter-app
```

## Usage

```
/create-flutter-app my_app
```

This will create a new Flutter project in the current directory with sensible defaults applied.

## What It Does

1. Runs `flutter create --platforms=ios,android` to scaffold the project
2. Fixes Dart dot-shorthand syntax issues in generated templates (Flutter 3.38+)
3. Sets iOS deployment target to 16.0
4. Cleans up `pubspec.yaml` (removes boilerplate comments, sets Dart SDK constraint)
5. Verifies Android configuration (Kotlin version, Flutter-managed SDK versions)
6. Creates a `CLAUDE.md` with build commands and architecture notes
7. Initializes a git repository with an initial commit

## Configuration Defaults

| Setting | Value |
|---|---|
| Platforms | iOS, Android only |
| iOS deployment target | 16.0 |
| Dart SDK | `>=3.5.0 <4.0.0` |
| Android Kotlin | 2.2.20 |
| Android Gradle Plugin | 8.11.1 |
| Java compatibility | 17 |
| Android SDK versions | Flutter-managed |

## Requirements

- [Flutter SDK](https://docs.flutter.dev/get-started/install) installed and on your PATH
- Xcode 15+ (for iOS development)
- Android Studio or Android SDK (for Android development)

## License

MIT
