# Tank 300 — Yandex Music AutoPlay skip fix

Fix for **double next/previous track** when using steering-wheel media buttons on **Tank 300 / GWM V3** head units.

## What was wrong

The HU firmware often sends a duplicate media-button signal. Track skip was handled by the **Media3** session (`androidx.media3.session`), not the older `MediaSessionCompat` callback path — so earlier debounce attempts there did nothing.

## What this patch does

Adds a **1000 ms debounce** in Media3 session callback:

- File: `androidx/media3/session/u.smali`
- Methods: `extends()` (skip next), `finally()` (skip previous)
- Duplicate presses within 1 second are ignored

Also keeps related debounce on the legacy path (`a79$g`, `xz8`) as a safety net.

## Install

1. Uninstall the previous Yandex Music Auto / autoPlay build if the signing key differs.
2. Install the APK from [Releases](https://github.com/virtusjit/tank300-alfa-devil-autoplay-skip-fix/releases).

Signed with a debug keystore (`*-aligned-debugSigned.apk`).

## Credits

- Base mod: **[Яндекс Музыка для ГУ на Андроид (autoPlay)](https://4pda.to/forum/index.php?showtopic=1116072)** by **Alfa_devil**  
  Build used: `Yandex.Music_07.06.26_autoPlay_basic.apk` (2026.06.07 build 5544)
- Earlier foundation mentioned by Alfa_devil: mod by **Vildanoff**
- This fork: Tank 300 steering-wheel double-skip fix

## Disclaimer

Unofficial modification. Not affiliated with Yandex. Requires a valid Yandex Music subscription. Use at your own risk.
