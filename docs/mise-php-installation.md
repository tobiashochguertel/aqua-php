# PHP Installation with mise - Documentation

This document describes how PHP was set up using `mise` with prebuilt binaries instead of compiling from source.

## Background

The standard ways to install PHP with mise have drawbacks:
- **asdf backend**: Compiles PHP from source (slow, dependency hell)
- **vfox backend**: Also compiles from source, outdated versions
- **No native/core PHP support** in mise

## Recommended Solution: `ubi` Backend

The **ubi** (Universal Binary Installer) backend is the recommended approach for PHP. It downloads prebuilt static PHP binaries from [rodrigodotdev/php](https://github.com/rodrigodotdev/php).

### Installation

```bash
mise use "ubi:rodrigodotdev/php@8.4.15"
```

### Verify

```bash
mise x -- php -v
# PHP 8.4.15 (cli) (built: Nov 28 2025 05:07:18) (NTS clang 17.0.0)
```

### mise.toml Configuration

```toml
[tools]
"ubi:rodrigodotdev/php" = "8.4.15"
```

### Available Versions

Check available versions:
```bash
mise ls-remote "ubi:rodrigodotdev/php"
```

Current series available:
- 8.4.x (latest: 8.4.15)
- 8.3.x
- 8.2.x
- 8.1.x

## Why `ubi` Backend?

According to mise documentation, the preferred backends for new tools are:

1. **aqua** - offers the most features and security (SLSA verification)
2. **ubi** - Universal Binary Installer, for tools available on GitHub/GitLab

Since PHP is not in the main aqua registry, `ubi` is the best choice because:
- ✅ Downloads prebuilt static binaries (no compilation)
- ✅ Fast installation (~30 seconds)
- ✅ Cross-platform (Linux, macOS, Windows)
- ✅ Multiple architectures (x86_64, aarch64)
- ✅ Zero dependencies (static binaries)

## Plugin Types Explained

### Backend Plugins vs Tool Plugins

From [mise documentation](https://mise.jdx.dev/plugins.html):

**Backend Plugins** (Preferred):
- Use backends like `aqua`, `ubi`, `github`, `npm`, `pipx`
- No custom plugin code needed
- Just specify the repository and version
- Example: `mise use ubi:rodrigodotdev/php@8.4.15`

**Tool Plugins** (Legacy):
- Custom Lua scripts that define how to download/install tools
- Located in `~/.local/share/mise/plugins/`
- More complex, requires maintenance
- Example: Our old `php-bin` plugin

**Recommendation**: Use backend plugins (`ubi`, `aqua`) whenever possible. Only create tool plugins for tools with unique installation requirements.

## Supported Platforms

| Platform | Architecture | Status |
|----------|--------------|--------|
| Linux | x86_64 | ✅ |
| Linux | aarch64 | ✅ |
| macOS | x86_64 (Intel) | ✅ |
| macOS | aarch64 (Apple Silicon) | ✅ |
| Windows | x64 | ✅ |

## Included Extensions

The static PHP binaries include common extensions:
- bcmath, curl, openssl, mysqli, pdo_mysql
- pgsql, pdo_pgsql, sqlite3, pdo_sqlite
- opcache, mbstring, soap, sockets, pcntl
- json, xml, dom, simplexml, xmlreader, xmlwriter
- zip, zlib, gd, exif, fileinfo, filter, hash
- and more...

## Alternative: Custom Aqua Registry

We also created an aqua registry at [tobiashochguertel/aqua-php](https://github.com/tobiashochguertel/aqua-php) for reference. However, mise's aqua backend currently only supports the main aqua registry, so `ubi` is the practical choice.

## Troubleshooting

### PHP command not found after installation

Run `mise activate` or use `mise x -- php` to execute PHP:
```bash
mise x -- php -v
```

### Check installed versions

```bash
mise ls
```

### Reinstall PHP

```bash
mise uninstall "ubi:rodrigodotdev/php"
mise use "ubi:rodrigodotdev/php@8.4.15"
```

## References

- [mise documentation](https://mise.jdx.dev/)
- [mise ubi backend](https://mise.jdx.dev/dev-tools/backends/ubi.html)
- [mise backends overview](https://mise.jdx.dev/dev-tools/backends/)
- [mise plugins](https://mise.jdx.dev/plugins.html)
- [rodrigodotdev/php](https://github.com/rodrigodotdev/php) - PHP binaries source
- [static-php-cli](https://github.com/crazywhalecc/static-php-cli) - Binary builder
