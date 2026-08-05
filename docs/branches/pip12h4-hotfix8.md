# pip12h4-hotfix8 – Development Branch

**Version:** 12.4.0-hotfix8  
**Status:** Development – not for production use

## Key Features

### Advanced AutoReturn
- Automatically returns video to PiP when tab focus moves away
- Configurable delay (0–5000 ms) exposed in the WPF settings UI
- Crash-safe: hotfix8 fixes a crash on rapid tab switching
- Session persistence: AutoReturn state survives browser restarts

### Multi-Window Orchestration
- Coordinates multiple PiP windows across monitors
- Window-specific volume and playback-rate controls
- Cross-window focus arbitration

### WebExtension Manifest V3
- Fully migrated from Manifest V2
- Service worker replaces background page
- Declarative Net Request replaces webRequest blocking

### Enhanced Overlay
- Redesigned overlay with hardware-accelerated rendering
- Picture-in-Picture thumbnail preview on hover
- Configurable opacity and corner radius

## Versions

| Component | Version | Date | Notes |
|-----------|---------|------|-------|
| Firefox Extension | 12.4.0-hotfix8 | 2026-08-01 | Advanced AutoReturn, session persistence |
| WPF Host App | 12.4.0-hotfix8 | 2026-08-01 | .NET 8, enhanced overlay |

## Changelog

- **12.4.0-hotfix8** – AutoReturn crash fix on rapid tab switch
- **12.4.0-hotfix7** – AutoReturn delay config exposed in WPF settings UI
- **12.4.0-hotfix6** – Session persistence across browser restarts
- **12.4.0-hotfix5** – AutoReturn heuristic improvements (focus debounce)
- **12.4.0-hotfix4** – Service-worker lifecycle fixes
- **12.4.0-hotfix3** – Declarative Net Request rule set updates
- **12.4.0-hotfix2** – Enhanced overlay rendering performance
- **12.4.0-hotfix1** – Cross-window focus arbitration fix
- **12.4.0** – Advanced AutoReturn engine introduced
- **12.3.0** – Multi-window orchestration
- **12.2.0** – WebExtension Manifest V3 migration
- **12.1.0** – Enhanced overlay with hardware acceleration

## Build & Deploy

```bash
# Clone this branch
git clone -b pip12h4-hotfix8 https://github.com/mooura/pip-teste0.git

# Build WPF host (Windows)
dotnet publish ./src/PiPManager/PiPManager.csproj \
  -c Release -r win-x64 --self-contained true \
  -p:PublishSingleFile=true -o ./dist/wpf

# Package Firefox extension
web-ext build --source-dir ./extension --artifacts-dir ./dist/extension
```

## Testing

```bash
# AutoReturn regression suite
dotnet test ./src/PiPManager.Tests -c Release --filter "Category=AutoReturn"

# Full test suite
dotnet test ./src/PiPManager.Tests -c Release
```

## Known Issues

- AutoReturn may misfire on single-page apps that manipulate `history.pushState` aggressively – tracked in issue #47
- Enhanced overlay corner radius has no effect on Windows 10 builds older than 1903
