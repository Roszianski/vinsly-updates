# Vinsly Updates

This public repository hosts the auto-update manifest for Vinsly Desktop.

## Update Endpoint

```
https://raw.githubusercontent.com/Roszianski/Vinsly-Updates/main/latest.json
```

## How It Works

1. **Build & Sign**: Private repo builds and cryptographically signs installers
2. **Release**: GitHub Actions creates a release with signed binaries
3. **Generate Manifest**: Workflow generates `latest.json` with download URLs
4. **Publish**: Manifest is automatically pushed to this public repo
5. **Update Check**: Vinsly Desktop periodically checks this URL for updates

## Setup Instructions

### One-Time Setup

1. **Create GitHub Token**
   - Go to: https://github.com/settings/tokens/new?description=Vinsly%20Updates%20Publisher&scopes=public_repo
   - Click "Generate token"
   - Copy the token

2. **Add Token to Private Repo**
   - Go to: https://github.com/Roszianski/Vinsly-Desktop/settings/secrets/actions/new
   - Name: `VINSLY_UPDATES_TOKEN`
   - Paste the token
   - Click "Add secret"

### Creating a Release

Push a version tag to trigger the automated workflow:

```bash
git tag v1.0.0
git push origin v1.0.0
```

The workflow will automatically:
- Build for macOS (Intel & Apple Silicon) and Windows
- Sign all installers with Tauri signing keys
- Create GitHub Release
- Update this repository's `latest.json`

## Files

- `latest.json` - Auto-update manifest (updated by GitHub Actions)
- `README.md` - This file
