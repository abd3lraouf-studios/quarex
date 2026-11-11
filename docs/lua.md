# Lua configuration

QuaRex reads `~/.config/quarex/init.lua` (GoRex's `~/.config/gorex/init.lua`
while only that one exists), or `QUAREX_CONFIG`. Its functions are the
`quarex` table; `rex` and `gorex`, the same table, keep Rex's and GoRex's
configurations working. The file is read when the app starts and by
`quarex config reload`. As in Rex, a bad call (`quarex.bind({ "cmd+k" },
…)`) is skipped and reported with its file and line, and so are a key that
does not read and an action no one has; the rest of the file loads. Only a
mistake Lua cannot get past, a syntax error, keeps the previous keymap and
actions. `quarex config check` prints the file's bindings, actions and
modes, and its mistakes.

`require("keys")` loads `keys.lua` beside the file (`a.b` is `a/b.lua` or
`a/b/init.lua`), once.

Rex's action names work too: `client.tab.new` is `tab.new`, `pane.balance`
`pane.equalize`, `client.mode.enter` `mode.enter`, and so on
(`rexActions` in `internal/app/rexcompat.go`).

## Keybindings

```lua
quarex.bind("ctrl+b>c", "tab.new")
quarex.bind("cmd+shift+l", "scratch")
quarex.unbind("ctrl+b>c")
```

Keys can be sequences joined by `>`; modifiers are `cmd` (`command`,
`super`, `meta`, `win`), `ctrl` (`control`), `alt` (`opt`, `option`) and
`shift`. Named keys include `enter`, `escape`, `tab`, `space`,
`backspace`, `delete`, arrows, `home`, `end`, `pageup`, `pagedown`, and
`f1`–`f12`; a key by its place, whatever the layout, is its W3C code in
brackets: `ctrl+[KeyA]`, `cmd+[Digit1]`.

`quarex.unbind("cmd+t")` also takes the app's own shortcut off the key,
which then reaches the terminal; `quarex.unbind("cmd+t", "tab.new")` only
when that is what it does.

A key can run a function. It returns `true` to take the key; else the
function bound to the key before it runs, and the last passes the key to
the terminal:

```lua
quarex.bind("ctrl+shift+n", function(ctx, ev)
  quarex.invoke("tab.new")
  return true
end)
```

`quarex.bindings()` lists the bindings made so far, each `{ key, mode,
action, args, source }` (`source` is `init.lua:3`), or those a filter
matches: `quarex.bindings{ action = "tab.new" }`. Passing one to
`quarex.unbind` removes just it. `quarex.modes()` lists the modes.

## Modes

```lua
quarex.mode("resize", { exclusive = true, once = true })
quarex.bind("cmd+r", "mode.enter", { name = "resize" })
quarex.bind("resize/left", "pane.resize.left")
quarex.bind("resize/right", "pane.resize.right")
```

`exclusive` ignores bindings outside the mode; `once` leaves the mode
after its next action. `mode.exit` and `mode.exit_all` leave explicitly,
and Escape leaves the current mode unless the mode binds it. While a
mode is active, the window shows its name at the bottom, and the keys of
a sequence typed so far until it runs or gives up (`keyhint.go`). A binding's
mode is written before the key: `resize/left`; a mode's binding comes
before one of the same key outside it. `quarex.unbind("resize/left")`
blocks the key in the mode (it does nothing there, though bound outside);
`quarex.unbind{ mode = "resize" }` removes the whole mode.

## Actions

```lua
quarex.action{
  name = "scratch",
  title = "Open Scratch Tab",
  args = { dir = "string", ratio = "number?" },
  run = function(ctx, args)
    quarex.invoke("tab.new", { dir = args.dir })
  end,
}
quarex.bind("cmd+shift+j", "scratch", { dir = "/tmp" })
```

Custom actions appear in the palette and in `quarex action run`. Argument
types are `string`, `number`, `integer`, `boolean`, `object`, `array` and
`any`; a trailing `?` makes one optional. An `args` table with a `type`
is a JSON Schema, used as written, and an action that declares no `args`
takes any. `category`, `keywords` and `repeats` are kept as Rex has them.

`run(ctx, args)` gets `ctx.origin` (`key`, `palette` or `api`),
`ctx.session_id` (the window's workspace) and `ctx.block_id` (the
focused pane's session). What it returns is the action's result, which
`quarex action run` prints as JSON; `nil` or `true` is none. An error it
raises fails the action.

- `quarex.invoke(name, args)` runs another action, built-in or custom, and
  returns its result, or `nil` and the error.
- `quarex.client.queue(name, args)` runs one of the app's actions after
  `run` returns, in order; none when `run` fails.
- `quarex.exec(argv, { cwd, env, stdin, timeout })` runs a command and
  returns `{ ok, code, stdout, stderr }`, or `nil` and the error;
  `quarex.exec.start(argv, opts)` starts one and returns `{ pid }`. An
  action has 30 seconds, and runs on the app's thread: the window waits
  for a command it runs. `config check` runs none.
- `quarex.json.encode(v)`, `quarex.json.decode(s)`, and `quarex.log(...)`,
  which writes to the app's log with the file and line.

## Events

```lua
quarex.on("program_status_changed", function(ev)
  if ev.state == "blocked" then
    quarex.invoke("app.settings")
  end
end)
```

`program_status_changed` runs when a pane's program reports a new or
changed status (`OSC 7501`), or when a record goes away (`ev.state ==
"clear"`). A pane's terminal also sends `bell`, `title_changed` (`title`),
`pwd_changed` (`pwd`), `process_changed` (`program`) and `child_exited`
(`exit_code`), each with `session`, `pane`, `program` and `dir`. A handler
may name them as Rex does, `terminal.bell` or
`com.superlogical.terminal.bell`. Fields are `session`, `pane`, `state`, `id`, `kind`, `title`,
`msg`, `last_msg` (the last message a working report carried), `app`,
`progress`, `program` and `dir`. Events run on the app's
thread after the poll that saw the change.

## App overrides

The app keeps its own overrides apart from Lua, in `shortcuts.json` beside
the settings:

```json
{"bindings":[{"key":"cmd+shift+j","action":"tab.new","args":{"dir":"/tmp"}}]}
```

They load after the Lua file, so they win over it. A binding whose key is
a menu shortcut takes that shortcut over: the menu item no longer answers
it, and the key reaches the terminal and the keymap (unless an exclusive
mode is active).

## Reload

```sh
quarex config check
quarex config reload
```

## Scripts

`quarex do` runs a Lua script against the server, as Rex's `rex do`:

```sh
quarex do ./layout.lua branch=main      # a file: it ends in .lua or has a slash
quarex do -e 'return rex.call("session.list")' --json
quarex do - < script.lua
quarex do dev_layout file=app.log       # anything else is an action by name
quarex do init.lua --action dev_layout file=app.log
```

The script runs in the `quarex` process, not the app. Its API calls go
to the Rex API gateway (`rexapi.sock`). When no gateway runs, `quarex do`
serves one of its own until the script ends. A script started in a
QuaRex pane acts on that pane's session and block; `-s` and `-b` name
others.

- `rex.args`, `rex.session_id`, `rex.block_id`. `key=value` pairs are typed
  by how they are written (`n=2` is a number). `--args` takes JSON,
  `@FILE` or `-`.
- `rex.call(method, args)`, and `rex.session.<method>{...}`, which fills
  in `session_id`. `rex.block.call(creator, method, args)` calls
  `block.method` and fills in `block_id`. Each returns its result, or
  `nil` and the error. `quarex api list` lists the methods.
- `rex.layout.block{ flavor, options }`, `rex.layout.horizontal(ratio, a,
  b)` and `rex.layout.vertical(...)` build the layouts `new_window`
  takes.
- `rex.action{...}` defines an action. `rex.invoke` runs it, or asks the
  app to run an action the script does not define, and
  `rex.client.queue` runs one of the app's at once.
- `rex.on(event, fn)` keeps the script listening after its last line.
  Events are named as Rex names them: `terminal.pwd_changed` or
  `com.superlogical.terminal.pwd_changed` for a block's, `block_event`
  for every block's, `window_created` for a session's. Without `--all`
  the script hears only its own session. `rex.wait(event, filter,
  timeout)`, `rex.sleep(s)`, `rex.after(s, fn)`, `rex.every(s, fn)` and
  `rex.stop(code)` work as in Rex. `--for 10m` stops listening after that
  long, and `--fail-fast` stops at the first handler that fails. Ctrl-C
  exits with status 130.
- `rex.exec.start` returns a handle: `h:wait([s])`, `h:write(data)` (with
  `stdin = true`), `h:close_stdin()`, `h:kill([signal])`, `h:running()`,
  `h.pid`. Output callbacks are not supported; the output is in what
  `h:wait` returns.
- `io.popen` and `os.execute` are not available, here or in the
  configuration; `rex.exec` runs commands.
- `rex.servers()` is empty and `rex.server(label)` fails: a script calls
  this machine's server only.

`quarex actions` lists every action with its arguments and Rex's names
of it. `quarex keymap` lists the keys bound and the file and line that
bound each, then the modes.
