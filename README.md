# aqua-php

Aqua registry package for PHP prebuilt static binaries.

This package provides PHP CLI binaries via the [aqua](https://aquaproj.github.io/) package manager, using prebuilt static binaries from [rodrigodotdev/php](https://github.com/rodrigodotdev/php).

## Usage with mise

Add to your `mise.toml`:

```toml
[tools]
"aqua:tobiashochguertel/aqua-php/php" = "8.4.15"
```

Or install via command line:

```bash
mise use "aqua:tobiashochguertel/aqua-php/php@8.4.15"
php -v
```

## Usage with aqua directly

Add to your `aqua.yaml`:

```yaml
registries:
  - type: standard
    ref: v4.232.1
  - name: php
    type: github_content
    repo_owner: tobiashochguertel
    repo_name: aqua-php
    ref: main
    path: registry.yaml

packages:
  - name: php
    registry: php
    version: "8.4.15"
```

## Available Versions

PHP versions are automatically synced from [rodrigodotdev/php](https://github.com/rodrigodotdev/php):

- 8.4.x series (latest: 8.4.15)
- 8.3.x series
- 8.2.x series
- 8.1.x series

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

## Building from Source

The binaries are built using [static-php-cli](https://github.com/crazywhalecc/static-php-cli) and distributed via [rodrigodotdev/php](https://github.com/rodrigodotdev/php).

## License

MIT License
