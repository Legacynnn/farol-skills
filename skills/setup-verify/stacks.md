# Runtime probes by surface

Pick the first probe whose tools exist on this machine; prove it; record only what was proven. Each probe lists launch, observe, stop.

## Web app (Next, Vite, Remix, Astro, plain)

1. **Chrome MCP** (`claude-in-chrome` or `mcp__claude-in-chrome__*`): launch the dev server in the background, wait for the URL to answer (`curl -sf <url> >/dev/null`), then navigate, screenshot, read console, snapshot the DOM. Resize the window to 320px for the narrow state.
2. **Playwright** (`npx playwright` present or installable): a one-file script that opens the URL, sets viewport, screenshots to `.scratch/verify/<name>.png`, dumps console errors.
3. **Fallback**: `curl` the route for status and key markup; note the gap.

## API / server

- Launch the server; probe with `curl -sf` or the project's HTTP client against one real endpoint per change; assert status and a body field with `jq`. Read the server log for errors.

## CLI

- Run the binary against a fixture in `.scratch/verify/fixtures/`; assert exit code and stdout with `diff` against an expected file. Golden files are the evidence.

## Library

- Static loops only; the runtime loop is one consumer test that imports the public entry point.

## Electron

- Launch with remote debugging: `<app cmd> --remote-debugging-port=9222`; attach Chrome MCP or Playwright (`chromium.connectOverCDP('http://localhost:9222')`) to the renderer; screenshot and read console. Main-process evidence is the app log.

## Tauri

1. **Tauri MCP** (`mcp___hypothesi_tauri-mcp-server__*`): `get_setup_instructions` once, then `driver_session`, `webview_screenshot`, `webview_dom_snapshot`, `read_logs`, `ipc_execute_command` for backend state.
2. **Fallback**: run `tauri dev`, treat the webview as a web app at its dev URL, read the Rust log.

## Expo / React Native

1. **iOS simulator**: `xcrun simctl boot "<device>"`, `npx expo run:ios` or `expo start --ios`; screenshot with `xcrun simctl io booted screenshot .scratch/verify/<name>.png`; logs with `xcrun simctl spawn booted log stream --predicate 'process == "<app>"'`. Deep-link to a screen with `xcrun simctl openurl booted <scheme>://<route>`.
2. **Android emulator**: `emulator -avd <name>`, `adb wait-for-device`, `npx expo run:android`; screenshot `adb exec-out screencap -p > .scratch/verify/<name>.png`; logs `adb logcat -s ReactNativeJS`.
3. **Expo web** as a fallback for layout only, via the web probe; note that native behaviour is not covered.

## Native iOS (Xcode)

- `xcodebuild -scheme <s> -destination 'platform=iOS Simulator,name=<d>' build test`; screenshots via `xcrun simctl io booted screenshot`; UI tests are the runtime loop.

## Native Android

- `./gradlew test`, `./gradlew connectedAndroidTest` on a running emulator; `adb` screenshot and logcat as above.

## Browser extension

- Load unpacked via Playwright `chromium.launchPersistentContext` with `--load-extension=<dist>`; drive a page that triggers it; screenshot and read the service-worker console.

## Desktop via accessibility (any app on this Mac)

- `computer-use` skill when present: list windows, read the accessibility tree, screenshot. Slowest probe; use only when nothing above applies.
