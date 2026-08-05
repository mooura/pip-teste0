# fix4-rc6 – Stable Release Candidate

**Version:** 4.0.0-rc6  
**Status:** Release Candidate – production ready

## Key Features

### Tab Occupancy Detection
- Detects when a tab already owns a PiP slot before opening a new window
- Prevents duplicate PiP windows for the same tab
- `TabOccupancyManager` API available for host-app integration

### Multi-Slot Layout Management
- Up to 4 simultaneous PiP slots, each independently positionable
- Slot assignment persists across tab navigation
- Layout presets: `2x1`, `2x2`, `1+3` sidebar

### Playlist Navigation
- Automatic next/previous video detection via DOM mutation observers
- Works with YouTube, Twitch, and generic `<video>` playlists

### WPF Host App
- .NET 8 WPF, system-tray icon with quick-access menu
- Overlay controls (play/pause, seek, volume) rendered over PiP windows
- Named-pipe IPC with the Firefox extension

## Versions

| Component | Version | Date | Notes |
|-----------|---------|------|-------|
| Firefox Extension | 4.0.0-rc6 | 2026-07-01 | Tab occupancy detection, multi-slot layout |
| WPF Host App | 4.0.0-rc6 | 2026-07-01 | .NET 8, system-tray integration |

## Changelog

- **4.0.0-rc6** – Final RC: tab occupancy bug fixes, improved overlay rendering, named-pipe stability
- **4.0.0-rc5** – Tab occupancy feature complete, multi-slot layout stable
- **4.0.0-rc4** – Multi-slot layout engine refactor; slot persistence added
- **4.0.0-rc3** – Initial tab occupancy API integration with `TabOccupancyManager`
- **4.0.0-rc2** – Playlist navigation improvements; YouTube/Twitch compatibility
- **4.0.0-rc1** – Initial release candidate based on v3.x stable

## Build & Deploy

```bash
# Clone this branch
git clone -b fix4-rc6 https://github.com/mooura/pip-teste0.git

# Build WPF host (Windows)
dotnet publish ./src/PiPManager/PiPManager.csproj \
  -c Release -r win-x64 --self-contained true \
  -p:PublishSingleFile=true -o ./dist/wpf

# Package Firefox extension
web-ext build --source-dir ./extension --artifacts-dir ./dist/extension
```

## Testing

```bash
# Tab occupancy tests
dotnet test ./src/PiPManager.Tests -c Release --filter "Category=TabOccupancy"

# Full test suite
dotnet test ./src/PiPManager.Tests -c Release
```

## Migration from v3.x

1. Uninstall the v3.x extension and WPF app
2. Install the new extension from this branch
3. Run the new WPF installer
4. Previous slot configurations are not compatible; reconfigure slots in the tray menu
