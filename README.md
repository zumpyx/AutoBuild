# AutoBuild

Automated build repository for C# .NET 4.8 tools commonly used in security research and red team operations. Compiled binaries are published to the [`NET4.8`](../../tree/NET4.8) branch on every successful build.

## Branches

| Branch | Description |
|--------|-------------|
| `main` | Source configuration, build scripts, and status tracking |
| `NET4.8` | Compiled .NET 4.8 binaries (AnyCPU / x86 / x64) |

## Tools

See [`config.json`](config.json) for the full list of configured tools.

Each tool is compiled for three CPU targets:

| Suffix | Platform |
|--------|----------|
| `<Tool>.any.exe` | AnyCPU (JIT selects 32/64-bit at runtime) |
| `<Tool>.x86.exe` | Forced 32-bit |
| `<Tool>.x64.exe` | Forced 64-bit |

## Build Status

See [`status.json`](status.json) for per-tool build status, or visit the [`NET4.8`](../../tree/NET4.8) branch README for a rendered table.

## Triggering a Build

Builds run automatically:

- Every **Monday at 02:00 UTC** (weekly scheduled run)
- On every **push to `main`** that modifies `config.json`
- Manually via **Actions → Build .NET 4.8 Tools → Run workflow**

## Adding a New Tool

1. Add an entry to [`config.json`](config.json):

```json
{
    "name": "MyTool",
    "repository": "https://github.com/author/MyTool.git",
    "branch": null,
    "enabled": true
}
```

Set `"branch"` to a branch name (e.g. `"dev"`) to clone a specific branch instead of the repository's default branch. Use `null` to always clone the default branch.

2. Push to `main` — the workflow will pick it up automatically.

## License

This repository contains only build automation scripts. Each tool retains its original license. Refer to each tool's upstream repository for licensing details.
