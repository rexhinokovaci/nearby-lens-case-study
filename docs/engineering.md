# How it ships

- **CI on every change.** Build and tests for the Android, Wear OS, iOS and watchOS targets.
- **Gated rules deploys.** The rules file is validated before it's published to the edge. A bad rules file never reaches devices.
- **Release hygiene.** Signing keys live outside git, and store builds come from tagged commits.
- **Store compliance.** Permission prompts explain why Bluetooth is needed, and the foreground service type is declared for connected devices.
- **Battery awareness.** Warns when OS battery optimization would stop background scanning.

## Stack

Kotlin · Jetpack Compose · Swift · SwiftUI · Wear OS · watchOS · Bluetooth LE · Cloudflare Pages & Workers · GitHub Actions
