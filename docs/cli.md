# quarex command line

`quarex` is the same binary as the app. From a terminal it drives sessions
without opening a window; with no arguments it starts the app.

`-S HOST` before a command uses a saved remote host from `hosts.json`, by
its name or its alias, or an address, instead of this machine's server. A
saved host is reached by its routes, as the window reaches it: Tailscale
(its address) first, then SSH (its SSH host, through `quarex ssh-bridge`
there); one kept to a route uses that one alone. Local-only commands (`hosts`,
`remote`, `server`, `update`) and window-only commands (`split`, `close`) do
not apply remotely. `action` applies remotely when the host turns Remote
Control on; `layout` reads a host's layout when it turns Share Layout on.

Every local terminal QuaRex opens gets:

- `QUAREX_SESSION`, the session the terminal belongs to, which commands
  use when `-s` is not given.
- `QUAREX_BIN_DIR`, and that directory at the front of `PATH`, where a
  `quarex` shim (and a `gorex` one, as GoRex named it) points at the app binary.
- `QUAREX_SERVER`, the server's socket.
- A pane made by the app also gets `QUAREX_PANE`, and `QUAREX_HOST` for a
  remote host's pane or `QUAREX_CLIENT` for a local one. A pane the server
  made for a client with no window open gets `QUAREX_CLIENT` only.

A session a remote client created does not get the shim: its shell is
already reachable from another machine, and the shim would make this
machine's local socket look local. It still gets `QUAREX_SESSION`.

## Opening a folder

```sh
quarex --open DIR...        # a tab in DIR, in the window focused last (a new window when none is open)
quarex --open-quake DIR...  # a tab in DIR, in the quake terminal, which drops down
```

These are the app's own arguments: a QuaRex that runs already takes them
from the new launch and opens the tabs, and one that starts opens them once
it has started (with `--open-quake` alone, only the quake terminal shows,
its windows waiting as at login). A relative `DIR` is under the current
directory, and a file opens its folder.

The installed app puts them in the file manager's menu of a folder, as
Open in QuaRex and Open in Quake Terminal (the second while the quake
terminal is on); Settings › General turns them off.

- **Windows:** File Explorer's menu of a folder, of the inside of one and
  of a drive, under `HKEY_CURRENT_USER\Software\Classes` (`Directory`,
  `Directory\Background` and `Drive`, verbs `QuaRex.open` and
  `QuaRex.quake`). Windows 11 lists them under Show more options, as it
  does every app's that is not an MSIX package. Uninstalling removes them
  (`mygo.json`'s `windows.removeKeys`).
- **macOS:** Finder's Quick Actions, `~/Library/Services/Open in
  QuaRex.workflow` and `Open in Quake Terminal.workflow`, for a folder or a
  file in one. Finder shows no Quick Actions for a click on the empty
  inside of a folder: right-click a file in it, which opens its folder.
- **Linux:** GNOME Files' Scripts menu (`~/.local/share/nautilus/scripts`),
  or with nautilus-python an extension that adds the items to the menu of a
  folder and of the inside of one; Nemo's actions; Dolphin's service menu
  (`~/.local/share/kio/servicemenus`).

## Commands

```sh
quarex ls [--json]
quarex clients [--json]
quarex [-S HOST] layout [--json]
quarex new [--dir DIR] [--shell SHELL] [--json] [-- COMMAND...]
quarex split [-s SESSION] [--down] [--dir DIR] [--shell SHELL] [-- COMMAND...]
quarex [-S HOST] shells [--json]
quarex close [-s SESSION] [--tab]
quarex rename [-s SESSION] NAME
quarex send [-s SESSION] [--enter] [--json] TEXT...
quarex capture [-s SESSION] [--history BYTES] [--raw] [--json]
quarex wait [-s SESSION] [--json] (--exit | --idle | --status STATE | --contains TEXT) [--timeout D]
quarex run [--json] [--dir DIR] -- COMMAND...
quarex events
quarex hosts [ls] [--json]
quarex skill show|setup|status|remove [--agent NAME] [--project] [--dry-run] [--json]
quarex remote status [--json] | remote control on|off
quarex server restart | upgrade
quarex update
quarex config path | config check [FILE] | config reload
quarex action run [-s SESSION] [--json] ACTION [KEY=VALUE...]
quarex float [new|toggle|hide-all|raise|lower|cycle|move|resize|dock] [-s SESSION] [--json] [KEY=VALUE...]
quarex teleport [--json] PANE HOST
quarex rex-import [--rex SOCKET] [--session LABEL|ID] [--shell] [--resize] [--json]
quarex rex-mirror --session ID --block ID [--label LABEL] [--socket PATH] [--resize]
quarex version [--json]
```

Targets are a full session ID, a workspace, tab or pane label, a position
in `ls` (1 is the first), or the end of an ID (at least four characters).
`-b` chooses a pane label, `-w` a tab label; `-b` wins over `-w`, which
wins over `-s`. An ambiguous target exits 3. `rename` gives a pane a label.

- `new` creates a session and prints its ID.
- `shells` lists the shells of the server's machine, the default one
  first, and its Windows Terminal profiles: their IDs, names and commands.
  `--shell` on `new` and `split` takes one by its ID or name (`pwsh`,
  `git-bash`, `wsl:Ubuntu`, `zsh`), or a program's path, and starts it as
  the default shell starts (PowerShell keeps its directory in step, a shell
  of Unix is a login shell); a command after `--` wins over it. The pane
  keeps it: a restart, or the server starting the layout's sessions again,
  starts the same shell.
- The app's actions `tab.new`, `pane.split.right` and `pane.split.down`
  (`quarex action run`, Lua's `quarex.invoke`, a keymap binding's `args`)
  take `host` (a saved host's name or id, or `local`), `profile` (a row of
  the picker: its id as `shell:pwsh`, `profile:ID`, `ssh:m4`, `browser` or
  `note`, the id's last part, or its title), `shell` (the same, or a
  program's command line) and `dir`. With none, the user's own key opens
  the picker of machines and terminals; a script or a client never sees
  it, and opens the focused pane's terminal on its machine.
  `quarex action run pane.split.right host=office-mac shell=zsh` splits the
  focused pane with zsh on the host office-mac. `quake.toggle` shows or
  hides the quake terminal.
- `send` types without attaching; `--enter` presses Return.
- `capture` prints the screen as text, or the escape sequences with
  `--raw`.
- `wait --exit` exits with the program's status; the other conditions
  exit 0, and a timeout exits 1. `--timeout 0` (the default) waits forever.
- `run` creates a session, runs the command, prints what the screen shows
  when it ends, and exits with the program's status.
- `split` changes the layout; the command after `--` runs in the new
  pane, or a shell does. The session server makes the change, and an
  open window shows it at once, a closed one as it opens. `close` and
  `rename` work the same way.
- `events` prints each layout or session change as one JSON line; with a
  host that shares its layout, it subscribes to that host's layout too.
- `clients` prints the principal, peer key, whether it is remote, through a
  kept connection, and how many seconds it has been attached.
- `hosts` lists saved remote hosts, each by its name and the alias it was
  given in QuaRex, if any, its routes (`tailscale`, `ssh`) and its SSH
  host; addresses stay hidden. A host of SSH alone is listed too.
- `remote status` shows the local server's remote access without its
  address; `remote control on|off` lets paired clients run app actions
  through the window. It applies to every paired client and every member
  of a joined network, and persists even while remote access is off.
  Destructive actions stay refused.
- `server restart` stops the local server, and the next one starts the
  sessions of the layout again, as one after a crash does: new shells at
  the directories their panes were in, with the same ids, so the windows
  attach to them; what the old ones printed is gone. Quit and End All
  still ends sessions. It starts no server itself: the open app
  reconnects and starts the next one, else the next `quarex` command or
  the next launch does, which brings the sessions back; until then none
  runs. Run inside a pane, it tells of the new shell first, then ends
  with the pane. It exits 0 when it is done, 1 when the server is too old
  to bring its sessions back (quit it once with Quit and End All, or kill
  it), and 4 when no server runs or the server did not stop.
- `server upgrade` hands the local server over to the executable you
  invoked on macOS or Linux. Shell processes and their output survive
  while clients reconnect. The executable's modification time must be
  newer than the server's, as for an app-initiated upgrade. The exact
  build already running is a no-op; an older build, or a different path
  with the same modification time, is refused.
- `update` checks the signed release feed for the Linux per-user install.
  It installs the update without opening a window and hands over the
  running server when there is one. Use the same `QUAREX_DIR` as the
  server if you set one. On macOS use Check for Updates in the app.
- `rex-import` reads a Rex server and makes its sessions in QuaRex: a space
  per session, a tab per window, a pane per block. Each pane runs this
  program's `rex-mirror`, which draws the Rex block and types into it, or
  runs a shell in its directory with `--shell`; `--resize` lets a mirror
  give the block the pane's size. Sessions already imported are recorded
  in `rex-import.json` in the data directory and left alone.
- `rex-mirror` is what those panes run; it needs the QuaRex window open for
  the import, not to mirror.
- The window's **Space ▸ Import from Rex**, and the palette's *Import from
  Rex*, do what `rex-import` does with mirrors, for every session not
  recorded yet.
- `action run` runs a built-in action by its ID, through the window.
  Values after the action are strings; the CLI does not guess types.
- `float` floats or docks panes through the window: `new` opens a floating
  terminal, `dock` puts the focused float back among the tiled panes, and
  the other subcommands name the `float.*` actions.
- `teleport` moves a pane of this machine to a host
  (teleport.md), named as `-S` names one: by its name as
  Remote Hosts shows it, or its address. It prints the new session's ID
  there, and has the server show the pane as that session, with or
  without a window; with no tab showing the pane, its session ends and
  the new one waits on the host; when the server cannot show the new
  session, as of a host the window does not know, both stay and it exits
  1.

`quarex rexapi` is not a command of this line: it serves Rex's API to Rex
clients from the server the app already runs. The server runs that
gateway itself while the local network listener or built-in Tailscale is
on; `quarex rexapi` alone runs one of its own, for development.
`quarex rexapi lan on --allow-unauthenticated`, `quarex rexapi lan off|status`, `quarex rexapi lan listen HOST:PORT` and
`quarex rexapi lan allow|deny NETWORK` set the listener on the local
network; `quarex rexapi tailscale on|off|login|logout|rename|status`,
`quarex rexapi pair` and `quarex rexapi call METHOD [JSON]` talk to the
gateway. See rex-api.md.

Exit codes: 0 ok, 1 failed, 2 usage, 3 no such session or target, 4
server unreachable. A signal exits 130. `run` and `wait --exit` return the
program's own status, which can collide with 1–4; the rest return the
codes above. `wait --json`, `run --json` and `action run --json` print a
JSON object while keeping the same exit status.

## Agents

A local session's shell already has `quarex` on `PATH`, so an agent can run:

```sh
quarex new --dir /tmp/demo
quarex send -s <id> --enter 'make test'
quarex wait -s <id> --contains FAIL --timeout 120s
quarex capture -s <id>
```

### The skill and its hooks

`quarex skill setup` installs a `quarex` skill that points at the guide the
installed binary prints, so upgrading QuaRex updates what agents are told.
It finds Claude Code (`~/.claude`), Codex (`~/.codex`), Gemini CLI
(`~/.gemini`, or `$GEMINI_CLI_HOME/.gemini`), OpenCode
(`~/.config/opencode`, or `$XDG_CONFIG_HOME/opencode`), and Pi
(`~/.pi/agent`, or `$PI_CODING_AGENT_DIR`). A named `--agent` is set up
even when its directory is absent; an unknown one is an error.

The skill goes into Claude Code's own `skills/quarex` directory and into
the shared `~/.agents/skills/quarex` directory that Codex, Gemini CLI,
OpenCode and Pi read. With no agent found, only the shared skill is written.

Claude Code, Codex and Gemini CLI also get a session-start hook, added to
`~/.claude/settings.json`, `~/.codex/hooks.json` and
`~/.gemini/settings.json`. The hook runs
`quarex __internal session-start --agent NAME`, which prints the session,
pane and connection for the agent's context, and labels the pane when
`--pane-naming` is on. Only QuaRex's own hook is added or removed:
every other setting and hook is left as it was, and a settings file that
is not valid JSON is reported as a conflict instead of rewritten.

Setup also makes each agent report its state to the pane it runs in, so
QuaRex knows the agent is working, waiting for the user or done even when
it prints no OSC 7501 report itself (kind `status` in setup and status).
Claude Code, Codex and Gemini CLI get one hook per event in the same
settings file; OpenCode gets a plugin, `~/.config/opencode/plugins/quarex.js`,
and Pi an extension, `~/.pi/agent/extensions/quarex.js` (kind `plugin`).
Each runs `quarex __internal agent-event --agent NAME --event EVENT` with
the event's JSON on stdin; it sends the server a `status.report` request
with an OSC 7501 body (`app=NAME`) for the session in `$QUAREX_SESSION`,
prints nothing and always exits 0, and does nothing outside QuaRex.

| Agent | working | blocked | done / idle / error | cleared |
| --- | --- | --- | --- | --- |
| Claude Code | UserPromptSubmit, PreToolUse, PostToolUse(Failure), ElicitationResult | PermissionRequest and Notification `permission_prompt` (permission); AskUserQuestion, Elicitation and other notifications (question); `auth_storage_failure`, StopFailure `authentication_failed`/`billing_error` (auth) | Stop (done, its last message); Notification `idle_prompt` (idle); StopFailure (error) | SessionEnd |
| Codex | UserPromptSubmit, PreToolUse, PostToolUse | PermissionRequest (permission) | Stop (done); Interrupt (idle); `notify` `agent-turn-complete` (done) | SessionEnd |
| Gemini CLI | BeforeAgent, BeforeTool, AfterTool | Notification `ToolPermission` (permission); the ask_user tool (question) | AfterAgent (done) | SessionEnd |
| OpenCode | `session.status` busy/retry, `session.execution.started`, a reply | `permission.asked` (permission); `question.asked`, `form.created` (question) | `session.idle`, `session.execution.succeeded` (done); `session.error`, `session.execution.failed` (error); an abort (idle) | `session.deleted` |
| Pi | `agent_start`, tool calls, `ui_prompt_end` | `ui_prompt_start` (confirm: permission, else question) | `agent_settled` (done, or idle when aborted) | `session_shutdown` |

Subagents' events (Claude Code's SubagentStop, OpenCode's child sessions)
are left out, so the pane shows the main agent.

- `quarex skill status` reports each agent and whether its skill and hook
  are missing, current, outdated or in conflict. `--json` has the same
  information for scripts.
- `quarex skill remove` removes QuaRex's skill and hook from every known
  agent, including agents no longer installed, and cleans up the skill
  and Pi/omp extension older builds wrote. It never removes a file QuaRex
  did not write.
- `quarex skill setup --dry-run` reports without changing anything;
  `--force` replaces a `quarex` skill the user wrote.
- `--project` writes into the current repository instead: the shared
  `.agents/skills/quarex`, or with `--agent claude`, `.claude/skills/quarex`
  and its hooks in `.claude/settings.local.json`. Codex and Gemini CLI
  project hooks, and the OpenCode and Pi plugins, are skipped: Codex asks
  the user to trust the project and each hook, and Gemini CLI's and the
  plugins' project files are shared with the repository; set those up for
  the account instead.
- `quarex skill show` prints the same guide the skill tells agents to read.
  `quarex __internal skill`, `quarex __internal session-start` and
  `quarex __internal agent-event` are the commands the installed files run and are not part of the documented
  command line.

Host add/remove and remote `split`/`close` are not part of this slice.
