# Deployment Guide

This guide covers building and deploying both the Firefox extension and the .NET 8 WPF host application for all branches.

---

## Prerequisites

| Tool | Version | Purpose |
|------|---------|---------|
| .NET SDK | 8.x | WPF host app |
| Node.js | 20+ | Extension tooling |
| web-ext | 8.x | Firefox extension packaging |
| Visual Studio | 2022 | Windows WPF development |
| Windows | 10/11 | WPF target platform |

---

## Building the Firefox Extension

```bash
# Install tooling
npm install -g web-ext

# Lint
web-ext lint --source-dir ./extension

# Build unsigned ZIP for testing
web-ext build --source-dir ./extension --artifacts-dir ./dist/extension

# Sign for distribution (requires AMO API key)
web-ext sign --source-dir ./extension \
  --api-key $AMO_API_KEY \
  --api-secret $AMO_API_SECRET \
  --artifacts-dir ./dist/extension
```

---

## Building the WPF Host App (.NET 8)

```bash
# Restore dependencies
dotnet restore ./src/PiPManager.sln

# Build (Release)
dotnet build ./src/PiPManager.sln -c Release

# Publish self-contained Windows x64 executable
dotnet publish ./src/PiPManager/PiPManager.csproj \
  -c Release \
  -r win-x64 \
  --self-contained true \
  -p:PublishSingleFile=true \
  -o ./dist/wpf
```

---

## Branch-Specific Notes

### `fix4-rc6` (Stable RC)

- Use configuration `Release` for the WPF app.
- Extension version must match `4.0.0-rc6` in `manifest.json`.
- Run smoke tests against tab occupancy feature before release.

```bash
dotnet test ./src/PiPManager.Tests -c Release --filter "Category=TabOccupancy"
```

### `pip12h4-hotfix8` (Development)

- Use configuration `Release` for the WPF app.
- Extension version must match `12.4.0-hotfix8` in `manifest.json`.
- Run AutoReturn regression suite:

```bash
dotnet test ./src/PiPManager.Tests -c Release --filter "Category=AutoReturn"
```

---

## GitHub Actions CI/CD

Automated builds run on every push via `.github/workflows/build.yml`.

Artifacts are published to the workflow run and, on tagged commits, to GitHub Releases.

| Trigger | Action |
|---------|--------|
| Push to any branch | Build + lint |
| Tag `v*` | Build + package + GitHub Release |

---

## Release Checklist

- [ ] Update `VERSIONS.md` with release date and notes
- [ ] Bump version in `manifest.json` (extension) and `.csproj` (WPF)
- [ ] Tag the commit: `git tag -a vX.Y.Z -m "Release X.Y.Z"`
- [ ] Push the tag: `git push origin vX.Y.Z`
- [ ] GitHub Actions will build and create the release automatically
- [ ] Attach signed extension `.xpi` to the GitHub Release
