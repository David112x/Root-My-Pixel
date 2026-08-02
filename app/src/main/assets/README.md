# App Assets

This directory contains bundled payload files shipped inside the APK.

## Required files

### profiles.json
The device profile feed. Maps each supported Pixel firmware to its asset paths.

### explores/*.so
Pre-compiled exploit payloads (CVE-2026-43499 APP_PAYLOAD variant) for each
target. Built from the payloads/ directory with:
```
make TARGET=frankel-CP2A.260605.012 ANDROID_NDK_HOME=...
```

The output `cve-2026-43499-app.release.so` goes into `app/src/main/assets/exploits/<target>.so`.

### ksud/*.bin
ReSukiSU late-load binaries (ksud) for each KMI. Download from official
ReSukiSU releases and rename to `ksud-android14-6.1`, `ksud-android15-6.6`, etc.

## Adding a new target

1. Add the target profile to `profiles.json`
2. Build the exploit .so for that target via the payloads/ Makefile
3. Copy the .so to `exploits/<profileId>.so`
4. Ensure a matching `ksud/<kmi>` binary exists
