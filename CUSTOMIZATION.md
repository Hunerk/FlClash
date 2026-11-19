# FlClash 0.9.4 customization notes

This file records the user-requested UI and Android build customizations. Keep it updated when making future changes.

## Floating bottom dock (悬浮底栏)

- Dock height: `52.5 dp`.
- Overall width: `Transform.scale(scaleX: 0.95)`; scales the dock itself by 5%, centered. It must NOT use the available screen width as the scale baseline or shrink the page/screen layout.
- Dock horizontal padding: `3.72 dp`.
- Edge margin: `12 dp`.
- Shadow room: `8 dp`.
- Maximum item extent: `60.078 dp`.
- Minimum resting selection-lens width: `78.12 dp`.
- Menu text labels are hidden; menu glyph icons remain visible. Accessibility semantics retain each destination label.
- Icon size: previously `20.46 dp`; now `22.51 dp` (approximately +10%).
- Selected lens / indicator frame: width and height are both scaled to `85%` of the previous calculated dimensions (15% smaller).
- The same 85% lens geometry is used while the user holds and drags across menu items, so the animated switching/drag frame is also smaller. Keep the lens visual and its glass/content clipping based on the same rectangle.
- Current horizontal dock scale remains 95%; do not confuse this with the 85% lens size.

## Standard NavigationBar (普通底栏, separate from the floating dock)

- Height: changed from `80 dp` to `48 dp`.
- Selected indicator size: changed from `64 x 32 dp` to `64 x 26 dp`.
- Icon/label column spacing: changed from `4 dp` to `1 dp`.
- Label text moved upward by `2 dp` using `Transform.translate(offset: Offset(0, -2))`.
- These settings apply to the standard `NavigationBar`, not the floating dock.

## Android app identity and build

- Android launcher/app display name: `FlClash` (not Nightly).
- App release line: `dev`; app version: `0.9.4`.
- ARM64 APK output name: `FlClash-dev-0.9.4-android-arm64.apk`.
- GitHub Actions artifact name: `FlClash-dev-0.9.4-android-arm64`.
- Build command pins the package version using `--tag v0.9.4` to avoid automatic `nightly.DATE.COMMIT` suffixes.
- Target: Android ARM64 (`arm64-v8a`).
- CI toolchain currently configured as Flutter `3.50.0`, Go `1.27.1`, NDK `r28c`.

## Future change checklist

- Keep floating dock and standard NavigationBar changes separate.
- When changing the dock width, scale the dock widget itself, not the full screen or available width.
- When changing the selection frame, update the shared lens rectangle so the normal selected state and long-press/drag animation stay consistent.
- Preserve the exact artifact naming above unless the user requests another version/name.
