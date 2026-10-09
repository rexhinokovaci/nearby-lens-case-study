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

## Read more

- [Architecture and key decisions](docs/architecture.md)
- [Delivery pipeline and stack](docs/engineering.md)

---

**Want something like this built for your business?** I build mobile apps, web apps and AI products end to end. [Email me about your project](mailto:kovacirexhino@gmail.com?subject=Project%20inquiry) · [Full profile](https://github.com/rexhinokovaci)
