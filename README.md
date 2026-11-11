# Omni Provider (`provider`)

# About

**`provider`** is the official default remote provider repository (`omni`, v0.1.0) for the [Omni Shell Framework](../omni/README.md). It acts as the central registry and catalog mapping official Omni **tools** and **contexts** to their respective Git repository URLs, local paths, and descriptions.

## Cataloged Tools

| Tool | Repository URL | Description |
| :--- | :--- | :--- |
| [`debug`](../debug/README.md) | `https://github.com/omnishell/debug.git` | Operating system debugger (`/proc` process manager, log viewer, and system inspector) |
| [`g`](../g/README.md) | `https://github.com/omnishell/g.git` | Interactive Git workflow manager (`fzf` + `vimdiff` staging, history editing, branches, tags, conflicts) |
| [`hardware`](../hardware/README.md) | `https://github.com/omnishell/hardware.git` | Hardware manager for multi-monitor (`xrandr`) and Wi-Fi (`nmcli`) configuration |
| [`otp`](../otp/README.md) | `https://github.com/omnishell/otp.git` | Multi-factor authentication (TOTP/OTP) code generator and secret manager |
| [`preprint`](../preprint/README.md) | `https://github.com/omnishell/preprint.git` | Academic preprint and publication manager for arXiv, Zenodo, HAL, and ORCID |
| [`py`](../py/README.md) | `https://github.com/omnishell/py.git` | Python environment, project, library, lockfile, build, and PyPI publishing manager |
| [`social`](../social/README.md) | `https://github.com/omnishell/social.git` | Social media content, template, and LinkedIn API publishing manager |
| [`web`](../web/README.md) | `https://github.com/omnishell/web.git` | Web browsers, hierarchical bookmarks, protocols, and search engines manager |
| [`wiki`](../wiki/README.md) | `https://github.com/omnishell/wiki.git` | Static site and personal wiki generator with LaTeX, SVG diagrams, and incremental builds |

## Cataloged Contexts

| Context | Repository URL | Description |
| :--- | :--- | :--- |
| [`contexts`](../contexts/README.md) | `https://github.com/omnishell/contexts.git` | Core Omni contexts collection |

---

# Install

## Default Registration in Omni

The `omni` provider is pre-registered out of the box when you initialize Omni (`PROVIDERS_REMOTE[omni]="https://github.com/omnishell/provider.git"`). To clone and install the provider catalog into `~/.omni/providers/omni`:

```bash
omni providers install omni
```

## Custom Registration (Remote or Local)

To register this repository manually as a remote provider:

```bash
omni providers set omni --type remote -u https://github.com/omnishell/provider.git
omni providers install omni
```

Or to register a local checkout of this repository for development:

```bash
omni providers set omni --type local -d /path/to/omni/provider
```

---

# Usage

## Inspecting and Syncing the Provider

```bash
# List registered providers
omni providers ls

# Inspect all tools and contexts exposed by the `omni` provider
omni providers get omni

# Pull the latest catalog updates from GitHub
omni providers sync omni
```

## Installing and Using Tools from the Provider

```bash
# List all tools available in the `omni` provider
omni tools ls -p omni

# Install and enable a tool in the active environment (automatically clones on first use)
omni tools use g --provider omni
omni tools use py --provider omni
omni tools use wiki --provider omni

# Enable a tool for a specific environment
omni tools use debug -e work --provider omni

# Run a tool from the provider without permanently adding it to the environment
omni tools call otp -p omni
```

## Using Contexts from the Provider

```bash
# List all contexts available in the `omni` provider
omni contexts ls -p omni

# Activate a context in the current environment
omni contexts use contexts -p omni
```

## Provider Specification (`init`)

The provider entrypoint file (`init`) defines the following associative arrays and metadata variables consumed by Omni's provider loader:

- `PROVIDER_NAME`: Provider identifier (`"omni"`)
- `PROVIDER_DESCRIPTION`: Human-readable summary (`"Core omni tools and contexts"`)
- `PROVIDER_VERSION`: Provider catalog version (`"0.1.0"`)
- `PROVIDER_TOOLS_URL[<tool>]`: Remote Git repository URL for `<tool>`
- `PROVIDER_TOOLS_PATH[<tool>]`: Optional local filesystem path for `<tool>`
- `PROVIDER_TOOLS_DESC[<tool>]`: Short description of `<tool>`
- `PROVIDER_CONTEXTS_URL[<context>]`: Remote Git repository URL for `<context>`
- `PROVIDER_CONTEXTS_PATH[<context>]`: Optional local filesystem path for `<context>`
- `PROVIDER_CONTEXTS_DESC[<context>]`: Short description of `<context>`
