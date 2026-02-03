# Contributing to meta-plugins

Thank you for contributing a plugin to the meta registry!

## Before You Submit

1. **Create your plugin** following the [plugin development guide](https://github.com/harmony-labs/meta/blob/main/docs/plugins.md)
2. **Publish GitHub releases** with platform-specific binaries
3. **Test locally** with `meta plugin install user/your-plugin`

## Release Requirements

Your plugin repository must have GitHub releases with correctly named assets:

### Asset Naming Convention

```
meta-{plugin-name}-{platform}.tar.gz
```

### Supported Platforms

- `darwin-arm64` (macOS Apple Silicon)
- `darwin-x64` (macOS Intel)
- `linux-x64` (Linux x86_64)
- `linux-arm64` (Linux ARM64)
- `windows-x64` (Windows x86_64)

### Example Release

For a plugin called `meta-docker`:

```
Releases v1.0.0
├── meta-docker-darwin-arm64.tar.gz
├── meta-docker-darwin-x64.tar.gz
├── meta-docker-linux-x64.tar.gz
├── meta-docker-linux-arm64.tar.gz
└── meta-docker-windows-x64.tar.gz
```

Each archive should contain the plugin binary (e.g., `meta-docker`).

## Submission Steps

### 1. Fork and Clone

```bash
git clone git@github.com:YOUR_USERNAME/meta-plugins.git
cd meta-plugins
```

### 2. Add Your Plugin

```bash
# Choose a short, memorable name
echo "your-github-username/meta-your-plugin" > plugins/your-plugin
```

### 3. Test Format

```bash
# Verify the file contains valid GitHub shorthand
cat plugins/your-plugin
# Should output: your-github-username/meta-your-plugin
```

### 4. Commit and Push

```bash
git add plugins/your-plugin
git commit -m "Add your-plugin to registry"
git push origin main
```

### 5. Create Pull Request

- Go to https://github.com/harmony-labs/meta-plugins
- Click "New pull request"
- Choose your fork and branch
- Title: "Add {plugin-name} plugin"
- Description: Brief explanation of what your plugin does

## CI Validation

Your PR will be automatically validated:

1. **Format check** - GitHub shorthand is valid
2. **Repository check** - GitHub repo exists and is accessible
3. **Release check** - Latest release has correctly named assets
4. **Conflict check** - Plugin name doesn't conflict

If CI fails, check the error message and update your PR.

## After Merge

Once merged, users can install your plugin:

```bash
meta plugin install your-plugin
```

## Plugin Quality Guidelines

- **Respond to `--meta-plugin-info`** - Return valid JSON with plugin metadata
- **Follow semantic versioning** - Use tags like `v1.0.0`, `v1.2.3`
- **Document in README** - Explain what your plugin does and how to use it
- **Include examples** - Show common use cases
- **Keep binaries small** - Strip debug symbols, use release builds

## Questions?

- [Open an issue](https://github.com/harmony-labs/meta/issues)
- [Check the docs](https://github.com/harmony-labs/meta)
- [Plugin development guide](https://github.com/harmony-labs/meta/blob/main/docs/plugins.md)
