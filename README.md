# ToolingTools Plugins

The shared marketplace catalog for ToolingTools developer plugins:

- [SimView](https://github.com/toolingtools/simview) — local iOS Simulator preview, inspection, input, and annotation.
- [Metro MCP](https://github.com/steve228uk/metro-mcp) — React Native and Expo runtime debugging through Metro/CDP.

This repository is intentionally catalog-only. It contains the Codex and Claude Code marketplace indexes, not plugin source, compiled binaries, or release archives. Each plugin is fetched from npm so its source repository and release cadence remain independent.

## Install in Codex

From GitHub:

```sh
codex plugin marketplace add toolingtools/plugins
codex plugin add simview@toolingtools
codex plugin add metro-mcp@toolingtools
```

From a local checkout:

```sh
codex plugin marketplace add /path/to/plugins
codex plugin add simview@toolingtools
codex plugin add metro-mcp@toolingtools
```

## Install in Claude Code

From GitHub:

```text
/plugin marketplace add toolingtools/plugins
/plugin install simview@toolingtools
/plugin install metro-mcp@toolingtools
```

The equivalent non-interactive commands are:

```sh
claude plugin marketplace add toolingtools/plugins
claude plugin install simview@toolingtools
claude plugin install metro-mcp@toolingtools
```

## Release contract

The npm package named by each marketplace entry must contain the plugin manifest and runtime files required by both clients:

- `.codex-plugin/plugin.json` for Codex.
- `.claude-plugin/plugin.json` for Claude Code.
- `.mcp.json` and any skills or assets referenced by those manifests.
- Built runtime files required by the package's MCP server.

Metro MCP is currently published as `metro-mcp` and should continue to be released from [its source repository](https://github.com/steve228uk/metro-mcp). SimView is listed as `simview` and resolves to the scoped npm package `@toolingtools/simview`.

After publishing a new package version, refresh the marketplace and reinstall or update the plugin in the relevant client. Do not commit release binaries or package archives to this repository.

## Validate

Run the catalog-only checks from the repository root:

```sh
./scripts/validate-catalogs
```

The same check runs in CI for every pull request and push to `main`.
