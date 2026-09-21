# Set up FreeCAD MCP for Codex

This skill supplies modeling instructions. The connection requires two separate components from [neka-nat/freecad-mcp](https://github.com/neka-nat/freecad-mcp): an addon running inside FreeCAD and a bridge that Codex launches as an MCP server. These instructions were checked on 2026-09-21; consult the linked upstream documentation if installation details change.

## 1. Install the prerequisites

Install [FreeCAD](https://www.freecad.org/downloads.php), [uv](https://docs.astral.sh/uv/getting-started/installation/), and Git if using the source checkout below. The bridge requires Python 3.12 or newer; uv can manage its interpreter separately from FreeCAD's bundled Python. Do not install the bridge into FreeCAD's bundled interpreter.

## 2. Install and start the FreeCAD addon

Clone the upstream repository:

```sh
git clone https://github.com/neka-nat/freecad-mcp.git
```

In FreeCAD, open **View → Panels → Python console** and find your user module directory:

```python
import os
print(os.path.join(FreeCAD.getUserAppDataDir(), "Mod"))
```

Create that directory if needed, then copy the checkout's `addon/FreeCADMCP` folder into it. The resulting structure must contain `Mod/FreeCADMCP/InitGui.py`; do not copy the entire checkout there or introduce another nested `FreeCADMCP` directory.

Restart FreeCAD, select the **MCP Addon** workbench, and click **Start RPC Server**. Keep FreeCAD running. The default local endpoint uses port **9875** for XML-RPC. It is not an HTTP/SSE MCP URL to paste into Codex.

See the upstream [installation instructions](https://github.com/neka-nat/freecad-mcp/blob/main/docs/installation.md) for platform details.

## 3. Register the bridge in Codex

Use the Codex CLI:

```sh
codex mcp add freecad -- uvx freecad-mcp
codex mcp list
```

Alternatively, merge this table into your user `~/.codex/config.toml` (on Windows, `%USERPROFILE%\.codex\config.toml`):

```toml
[mcp_servers.freecad]
command = "uvx"
args = ["freecad-mcp"]
```

Use one registration method and preserve other settings. Restart the Codex app if it has not picked up the change. If a desktop app cannot find `uvx`, use the full path to its executable for `command`.

### Alternative: run the bridge from the checkout

For development or a pinned upstream checkout, run `uv sync` and `uv run freecad-mcp --help` inside that checkout. Replace the configuration above with:

```toml
[mcp_servers.freecad]
command = "uv"
args = ["--directory", "/absolute/path/to/freecad-mcp", "run", "freecad-mcp"]
```

On Windows, forward slashes in the TOML path work, for example `C:/src/freecad-mcp`. Choose your actual checkout location. Keep the addon and bridge versions compatible when updating.

The official [Codex MCP documentation](https://learn.chatgpt.com/docs/extend/mcp?surface=cli) describes registration and configuration options.

## 4. Verify the complete connection

Ask Codex to list open FreeCAD documents without modifying them. An empty list is a valid response when no documents are open. Merely seeing the server in `codex mcp list` does not verify the addon connection. If exposed by your version, `get_rpc_status` provides another diagnostic.

Then install this skill using the [repository instructions](../README.md#install). A simple first task is to create and save a new document containing a 10 mm cube. Use a new document rather than replacing an existing project.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| MCP Addon workbench missing | Verify the folder nesting, restart FreeCAD, and inspect its Report view for addon import errors. |
| Codex cannot start the bridge | Check the executable path and run `uvx freecad-mcp --help` in a terminal. GUI applications can have a different PATH. |
| Connection refused | Start the RPC server in the running FreeCAD instance and check the configured host/port. A listening port alone is not an end-to-end test. |
| A long modeling call times out | Do not submit the mutation again immediately. Inspect status and completed artifacts first; the GUI operation may still be running. |
| Headless execution unavailable | Check the upstream `--freecadcmd` option and executable detection. Headless execution occurs on the bridge machine, which must have access to the input/output paths. |

For deliberate long builds, Codex supports `tool_timeout_sec` in the server table. This client budget is separate from the execution tool's own timeout and FreeCAD dispatch limits. Increasing it does not repair a stalled geometry operation. Prefer isolated headless builds for expensive geometry where supported, and avoid GUI calls in those builds. See upstream [execution behavior](https://github.com/neka-nat/freecad-mcp/blob/main/docs/execution.md) and [configuration](https://github.com/neka-nat/freecad-mcp/blob/main/docs/configuration.md).

Local use needs no publicly exposed port. Upstream also provides an optional addon auto-start setting after the manual connection works.
