# Upload a Release Asset

A GitHub Action to upload assets to an existing release in your repository.

## Features

- Upload assets to existing releases
- Support for multiple file uploads via glob patterns
- Automatic file size and type detection

## Usage

### Basic Usage

```yaml
- name: Upload Release Asset
  uses: owjs3901/upload-release-asset@v1
  with:
    upload_url: ${{ steps.create_release.outputs.upload_url }}
    asset_path: 'dist/*.zip'
    token: ${{ secrets.GITHUB_TOKEN }}
```

### Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `upload_url` | The URL for uploading assets to the release | ✅ | - |
| `asset_path` | The path to the asset you want to upload (supports glob patterns) | ✅ | - |
| `token` | The token to use to authenticate with the GitHub API | ❌ | `${{ github.token }}` |

### Examples

#### Single File Upload

```yaml
- name: Upload Release Asset
  uses: owjs3901/upload-release-asset@v1
  with:
    upload_url: ${{ steps.create_release.outputs.upload_url }}
    asset_path: 'dist/app.zip'
    token: ${{ secrets.GITHUB_TOKEN }}
```

#### Multiple File Upload (Glob Pattern)

```yaml
- name: Upload Release Assets
  uses: owjs3901/upload-release-asset@v1
  with:
    upload_url: ${{ steps.create_release.outputs.upload_url }}
    asset_path: 'dist/*.{zip,tar.gz}'
    token: ${{ secrets.GITHUB_TOKEN }}
```

#### Upload with Release Creation

```yaml
- name: Create Release
  id: create_release
  uses: actions/create-release@v1
  with:
    tag_name: ${{ github.ref }}
    release_name: Release ${{ github.ref }}
    body: |
      Release notes here
    draft: false
    prerelease: false

- name: Upload Release Asset
  uses: owjs3901/upload-release-asset@v1
  with:
    upload_url: ${{ steps.create_release.outputs.upload_url }}
    asset_path: 'dist/*.zip'
```

## Development

### Build

```bash
bun run build
```

### Lint

```bash
bun run lint
bun run lint:fix
```

## License

Apache-2.0

## Author

JeongMin Oh (owjs3901)