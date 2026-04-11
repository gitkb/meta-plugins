# meta-plugins

Official plugin registry for [meta](https://github.com/gitkb/meta).

## What is this?

This is a thin registry that maps short plugin names to GitHub repositories. When you run `meta plugin install docker`, meta looks up the plugin in this registry and installs it from the corresponding GitHub repository.

## Registry Structure

```
plugins/
├── docker        # Contains: someuser/meta-docker
├── npm           # Contains: anotheruser/meta-npm
└── k8s           # Contains: k8s-org/meta-k8s
```

Each file in `plugins/` contains a single line with a GitHub shorthand like `user/repo` or `user/repo@v1.0.0`.

## Using the Registry

### Install a plugin by name

```bash
meta plugin install docker
```

This resolves `docker` → `someuser/meta-docker` → downloads from GitHub releases.

### Search for plugins

```bash
meta plugin search <query>
```

## Publishing Your Plugin

### Requirements

1. Your plugin must follow [GitHub Releases naming conventions](https://github.com/gitkb/meta/blob/main/docs/plugin-distribution.md#github-releases)
2. Release assets must be named: `meta-{name}-{platform}.tar.gz`
3. Supported platforms: `darwin-arm64`, `darwin-x64`, `linux-x64`, `linux-arm64`, `windows-x64`
4. Your plugin must respond to `--meta-plugin-info` and return valid JSON

### Submission Process

1. Fork this repository
2. Create a new file in `plugins/` with your plugin's short name
3. Add your GitHub shorthand (e.g., `yourusername/meta-yourplugin`)
4. Submit a pull request
5. CI will validate your plugin:
   - Checks that the GitHub repo exists
   - Verifies releases follow naming conventions
   - Downloads and validates plugin binary
6. Once CI passes, a maintainer will merge your PR

### Example

To register `meta-docker` from `someuser/meta-docker`:

```bash
# Create file
echo "someuser/meta-docker" > plugins/docker

# Commit and push
git add plugins/docker
git commit -m "Add docker plugin"
git push
```

Then create a pull request.

## CI Validation

The `.github/workflows/validate-plugin.yml` workflow automatically validates:

- GitHub repository exists and is accessible
- Latest release has correctly named assets for all platforms
- Plugin binary responds to `--meta-plugin-info`
- Plugin name doesn't conflict with existing plugins

## Support

- [Documentation](https://github.com/gitkb/meta)
- [Report issues](https://github.com/gitkb/meta/issues)
- [Plugin development guide](https://github.com/gitkb/meta/blob/main/docs/plugins.md)
