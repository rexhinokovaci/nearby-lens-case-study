# Nearby Lens: case study

**Detects camera-equipped smart glasses nearby, over Bluetooth LE.** Native apps for iOS, watchOS, Android and Wear OS.

[Website](https://nearby-glasses-alert.pages.dev) · Platforms: iOS · watchOS · Android · Wear OS

> Source code is private. This repo documents what was built and how. Ask for a live walkthrough of the real codebase.

## The problem

Smart glasses with cameras, such as Ray-Ban Meta, Oakley Meta and Snap Spectacles, look like normal glasses. People want to know when one might be recording nearby, without needing special hardware.

## What I built

- **Passive BLE scanning** that scores nearby devices by manufacturer ID, service UUID and name signals, then alerts when confidence passes a threshold.
- **Three sensitivity modes** (strict, balanced, relaxed), each tuning minimum confidence and signal strength.
- **Over-the-air detection rules.** New devices are added by publishing a versioned rules file, with no app-store release needed.
- **Background reliability.** Foreground service, resume after reboot, a scan watchdog and retry with backoff.
- **Wrist alerts** on Apple Watch and Wear OS, plus a home-screen widget and a quick-settings tile.
- **Privacy by default.** Device identifiers are hashed and detection history stays on the phone.

## Results

- Shipped natively on four platforms from one detection model.
- Rule updates go live in minutes instead of waiting for store review.

## Lessons learned

- **Score, don't match.** BLE signals are noisy, so a weighted confidence score with user-selectable sensitivity works better than a yes/no device match.
- **Ship detection rules as data.** Moving rules out of the app binary turned a store-review cycle into a deploy that takes minutes. Validating that file before it's published matters as much as testing code.
- **Background behavior is platform-specific.** Reliable background scanning needed native code on each platform, plus explicit handling of reboots, scan stalls and OS battery optimization.
- **Be honest about limits.** Passive BLE can't prove a camera is recording, so the app presents likelihood, not proof.

## FAQ

### Can Nearby Lens prove that someone is recording me?

No. It detects nearby devices that advertise like camera-equipped smart glasses and reports how likely a match is. Devices that don't advertise, or that randomize their identifiers, may be missed. See [known limits](docs/architecture.md#known-limits-stated-honestly).

### Does the app send my data to a server?

No. There is no tracking backend: detection runs on the device, identifiers are hashed, and detection history stays on the phone. The app fetches the versioned detection rules from the edge and caches them.

### How are new smart glasses models added?

By publishing a new version of the rules file to Cloudflare. Apps pick it up over the air and cache it for offline use, with no App Store or Google Play release needed.

### Why native apps instead of a cross-platform framework?

Background Bluetooth LE behaves differently on iOS, watchOS, Android and Wear OS, and needs native control to stay reliable without draining the battery.

### Can you build a Bluetooth, wearable or privacy-first app for my business?

Yes. I'm a mobile app developer and DevOps engineer based in Tirana, Albania, building native iOS, Android, watchOS and Wear OS apps for clients across the Balkans and Europe. [Email me about your project](mailto:kovacirexhino@gmail.com?subject=Project%20inquiry).

## Read more

- [Architecture and key decisions](docs/architecture.md)
- [Delivery pipeline and stack](docs/engineering.md)

## Related case studies

- [Word game engine](https://github.com/rexhinokovaci/word-game-engine-case-study): one real-time multiplayer engine shipped as 7 localized games
- [Kush Jam Unë?](https://github.com/rexhinokovaci/kush-jam-une-case-study): Albanian party game with live content, subscriptions and ads
- [Balkans Quiz](https://github.com/rexhinokovaci/balkans-quiz-case-study): per-country trivia apps with Apple Watch, widgets and an automated question pipeline

## About the author

**Rexhino Kovaci** is a DevOps engineer, mobile app developer and AI engineer based in Tirana, Albania, and the founder of [Modex Apps](https://modex.al). He has 5+ years in DevOps, including work as a DevOps Engineer at Lufthansa Industry Solutions on Volkswagen AG projects, and holds Microsoft DevOps Engineer Expert, Azure Administrator Associate, Azure Developer Associate, HashiCorp Terraform Associate and New Relic Full-Stack Observability certifications. He builds for clients across the Balkans and Europe.

---

**Want something like this built for your business?** I build mobile apps, web apps and AI products end to end. [Email me about your project](mailto:kovacirexhino@gmail.com?subject=Project%20inquiry) · [Full profile](https://github.com/rexhinokovaci)

<sub>This case study is licensed under [CC BY 4.0](LICENSE). Product names and trademarks belong to their owners.</sub>
