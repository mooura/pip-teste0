# PiPManager

Advanced Picture-in-Picture manager for Firefox with automatic video restoration, intelligent playlist navigation, and multi-slot layout management.

## Project Overview

PiPManager is a dual-component solution:

1. **Firefox Extension** – Intercepts and manages Picture-in-Picture windows, supports multi-slot layouts, tab occupancy detection, and automatic playlist navigation.
2. **.NET 8 WPF Host App** – Native Windows companion that provides persistent PiP window management, system tray integration, and overlay controls.

## Branch Structure

| Branch | Purpose | Status |
|--------|---------|--------|
| `main` | Project overview and documentation | Stable |
| `fix4-rc6` | Stable PiPManager release with tab occupancy features | Release Candidate |
| `pip12h4-hotfix8` | Development version with advanced AutoReturn | Development |

## Quick Start

### Firefox Extension

1. Open Firefox and navigate to `about:debugging#/runtime/this-firefox`
2. Click **Load Temporary Add-on** and select `manifest.json` from the extension directory
3. Alternatively install from the [Releases](../../releases) page

### Windows Host App (.NET 8 WPF)

1. Download the latest installer from [Releases](../../releases)
2. Run `PiPManager-Setup.exe`
3. The app starts in the system tray automatically

### Build from Source

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed build and deployment instructions.

## Version History

See [VERSIONS.md](./VERSIONS.md) for the full version history across all branches.

## License

MIT
