---
title: "badlogic/cchistory: Extract and compare system prompts and tools from different Claude Code versions"
source: "https://github.com/badlogic/cchistory"
author:
  - "[[badlogic]]"
published:
created: 2025-12-04
description: "Extract and compare system prompts and tools from different Claude Code versions - badlogic/cchistory"
tags:
  - "clippings"
---
**[cchistory](https://github.com/badlogic/cchistory)** Public

Extract and compare system prompts and tools from different Claude Code versions

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/badlogic/cchistory?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/tree/main/.github">.github</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/tree/main/.github">.github</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/dc7e9017bd8d2b3853de8a90f819c80e22ee353c">Create FUNDING.yml</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/tree/main/.husky">.husky</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/tree/main/.husky">.husky</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/60ccd58d194bc874ddd6bffd8d3e9207dfb0467f">Add husky pre-commit hook for biome formatting and TypeScript checking</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/tree/main/src">src</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/tree/main/src">src</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/ddacee8343dc9dade7042c1de8233d1138aba9f1">Fix capturing pairs with system prompts</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/ffad7561e7229aa5a452b6b6afbada9cc6ad67ec">Extract pure functions and add comprehensive test suite</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/README.md">README.md</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/README.md">README.md</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/1466439fa420aed407255a54fef4038f8f80ec71">Add custom binary support and argument passing (</a><a href="https://github.com/badlogic/cchistory/issues/3">#3</a><a href="https://github.com/badlogic/cchistory/commit/1466439fa420aed407255a54fef4038f8f80ec71">)</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/biome.json">biome.json</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/biome.json">biome.json</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/e22dc122f127691ba4efab5440f10f0c0d542c10">Fix all TypeScript and linting errors, rename prompts.ts to cchistory.ts</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/package-lock.json">package-lock.json</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/package-lock.json">package-lock.json</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/cdf2f25b54bcec005acd37fc191594607d66694f">1.1.11</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/package.json">package.json</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/package.json">package.json</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/cdf2f25b54bcec005acd37fc191594607d66694f">1.1.11</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/tsconfig.json">tsconfig.json</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/tsconfig.json">tsconfig.json</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/1c19c6daf3ecf7316d29d921ffa7988ec8a8589d">Update package.json scripts and biome configuration</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/badlogic/cchistory/blob/main/vitest.config.ts">vitest.config.ts</a></p></td><td colspan="1"><p><a href="https://github.com/badlogic/cchistory/blob/main/vitest.config.ts">vitest.config.ts</a></p></td><td><p><a href="https://github.com/badlogic/cchistory/commit/ffad7561e7229aa5a452b6b6afbada9cc6ad67ec">Extract pure functions and add comprehensive test suite</a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

## cchistory

Extract and compare system prompts and tools from different Claude Code versions.

## Prerequisites

- You must be logged in to Claude Code (authentication required for all modes)
- Claude Code installation is optional if using `--binary-path` with a custom binary
- Note: Each version tested will send a single haiku request to Claude, which may incur costs if you're on a pay-per-token plan instead of Claude Max

## Installation

```
npm install -g @mariozechner/cchistory
```

## Usage

```
cchistory [version] [--latest] [--binary-path <path>] [--claude-args "<args>"]
```

### Options

- `version` - NPM version of Claude Code to extract (e.g., `1.0.0`)
- `--latest` - Extract all versions from the specified version to the latest published version
- `--binary-path <path>` - Use a custom/local Claude Code binary instead of downloading from npm
- `--claude-args "<args>"` - Pass additional arguments to Claude Code during execution
- `--version`, `-v` - Show cchistory version
- `--help`, `-h` - Show help message

### Examples

```
# Extract prompts from a single version
cchistory 1.0.0

# Extract prompts from version 1.0.0 to latest
cchistory 1.0.0 --latest

# Test a custom/local build of Claude Code
cchistory --binary-path /path/to/custom/cli.js

# Test with additional Claude Code arguments
cchistory 1.0.0 --claude-args "--mcp-config /path/to/config.json"

# Combine custom binary with custom arguments
cchistory --binary-path ./build/cli.js --claude-args "--verbose"

# Pass system prompt modifiers to any version
cchistory 1.5.0 --claude-args "--append-system-prompt"
```
1. Downloads the specified Claude Code version from npm
2. Patches the version check to prevent auto-updates
3. Runs the patched version with claude-trace to intercept API requests
4. Sends a single test haiku request to trigger an API call
5. Extracts the system prompt, user message format, and available tools from the intercepted request
6. Saves the results to `prompts-{version}.md`
1. Uses the specified binary directly (skips download and patching)
2. Runs it with claude-trace to intercept API requests
3. Sends a single test haiku request to trigger an API call
4. Extracts the system prompt, user message format, and available tools from the intercepted request
5. Saves the results to `prompts-custom-{timestamp}.md`

Existing prompt files are automatically skipped to avoid redundant downloads and API calls.

## Output Format

Each `prompts-{version}.md` file contains:

- **User Message**: The format of user messages sent to Claude
- **System Prompt**: The system instructions Claude receives
- **Tools**: Available tools with their descriptions and input schemas (excluding MCP tools)

## Advanced Usage

The `--binary-path` flag is particularly useful for:

- Testing local modifications to Claude Code before publishing
- Comparing development builds against released versions
- Debugging prompt or tool changes in your fork
```
# Test your local development build
cchistory --binary-path /path/to/your/fork/cli.js

# Compare with a released version
cchistory 1.0.0
# Now you have both prompts-1.0.0.md and prompts-custom-*.md to compare
```

The `--claude-args` flag allows you to test Claude Code with different configurations:

```
# Test with MCP server configuration
cchistory 1.5.0 --claude-args "--mcp-config ~/.config/claude/mcp.json"

# Test with verbose logging
cchistory --binary-path ./build/cli.js --claude-args "--verbose"

# Combine multiple flags
cchistory 1.0.0 --claude-args "--debug --no-cache"
```

**Note**: Arguments are parsed safely using shell-quote to prevent command injection. Shell operators and control characters are filtered out.

### Debugging

Enable debug output to see detailed information about the extraction process:

```
DEBUG=1 cchistory 1.0.0
```

This will show:

- All API requests found in the claude-trace log
- Model names and tool counts for each request
- Full stack traces for any errors

### Security Notes

- All shell commands use proper escaping via the `shell-quote` library
- The `--claude-args` parameter filters out shell operators for safety
- Version patching only modifies the version check function (no other code changes)
- Custom binaries are executed directly without modification

## Releases

[9 tags](https://github.com/badlogic/cchistory/tags)

## Sponsor this project

[**badlogic** Mario Zechner](https://github.com/badlogic)

[Sponsor](https://github.com/sponsors/badlogic)

[Learn more about GitHub Sponsors](https://github.com/sponsors)

## Packages

No packages published  

## Languages

- [TypeScript 80.3%](https://github.com/badlogic/cchistory/search?l=typescript)
- [JavaScript 18.8%](https://github.com/badlogic/cchistory/search?l=javascript)
- [Shell 0.9%](https://github.com/badlogic/cchistory/search?l=shell)