# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build & Run Commands

```bash
flutter pub get                    # Install dependencies
flutter run                        # Run on any device (auto-select)
flutter run -d ios                 # Run on iOS simulator
flutter run -d android             # Run on Android emulator
flutter run -d all                 # Run on all connected devices
flutter analyze                    # Run Dart static analysis
flutter test                       # Run tests
flutter test test/widget_test.dart # Run a single test file
flutter clean && flutter pub get   # Clean rebuild
```

## Architecture

All Dart source is in `lib/` (flat structure, no subdirectories).

## Platform Requirements

- iOS: deployment target 16.0, Xcode 15+
- Android: Kotlin 2.2.20, Gradle 8.11.1, Flutter-managed SDK versions
- Dart SDK: `>=3.5.0 <4.0.0`
