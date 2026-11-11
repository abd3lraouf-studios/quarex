# QuaRex guide

What QuaRex does, its keys, its settings, and remote access, in detail.
Installing it is in the [README](../README.md).

## What it does

- **Tabs and split panes.** Every pane is a card over the window's gradient,
  with its program's icon, name and directory in its header, and buttons to
  split right, split down, zoom and close. Drag the gaps between panes to
  resize them (double-click resets a split to half).
- **Pick the machine and the terminal.** Split Right, Split Down and New
  Tab (their keys, the panes' buttons, the title bar's +, the palette) ask
  which machine the new pane runs on, this one or any connected host, and
  what it runs there: the machine's shells (PowerShell, Command Prompt, Git
  Bash, WSL distributions, zsh, bash, fish…), Windows Terminal's profiles,
  your own profiles, the SSH hosts of its `~/.ssh/config`, or on this
  machine a browser or a note. It opens on the machine and the terminal
  you opened last (marked Recent), else the focused pane's; ← → switch the
  machine, ↑ ↓ the terminal, typing filters, Enter opens, and Delete or a
  row's eye button hides a row you never use (the footer shows the hidden
  ones again, as Settings › Terminal does). One tab holds panes of several
  machines, each pane's header saying its machine, and the title bar's
  machine chip follows the focused pane, its panel listing every machine
  with New Tab and Split buttons. Settings › Terminal turns the picker off
  (Split then opens the focused pane's terminal at once), hides Windows
  Terminal's profiles or the SSH hosts, and edits your profiles: a name, a
  command line, a starting directory, and the machines it is offered on.
- **SSH by the best route.** An SSH host of this machine (its
  `~/.ssh/config`) opens on the local network where the host answers
  there, and over Tailscale where it does not, as away from home: QuaRex is
  the connection's ProxyCommand (`quarex ssh-route`), which races the routes
  with the local network a moment ahead, and ssh keeps your user, keys and
  known hosts. The Tailscale route is the tailnet device whose name the
  host's alias or `HostName` matches (`mac.local` finds `mac` or `mac-1`),
  or one you pick in Settings › Terminal › SSH Routes, where Local network
  only turns it off. A connection that drops, as when you leave the local
  network, connects again by itself by the route open then, after one
  second and then up to sixteen; leaving the shell closes the pane as ever.
  A host with its own ProxyCommand or ProxyJump is left to it.
- **Move panes and tabs anywhere.** As iTerm2 moves a session, a pane's
  menu moves it, its program running, to a window of its own (Move Pane to
  New Window, also a command), into another window as a tab of its own or
  beside its pane, or into a space no window shows; a tab's menu moves the
  whole tab the same ways. The quake terminal is one of the windows: a pane
  or tab goes into it, and one that comes out is a standalone window's.
  Each pane's header has a button that moves it to a new window, which
  then takes tabs and splits as any (Settings › Appearance › Panes).
- **Focus follows the mouse.** Moving the pointer into a split gives it
  the keyboard, as iTerm2's Focus Follows Mouse; keys that move between
  panes still hold while the pointer rests, and a selection dragged across
  panes moves nothing. Settings › Appearance › Focus a Pane switches to
  Click.
- **The terminal's menu, as iTerm2's.** A right click in a terminal shows
  a menu with an icon on each item. On a link: Open Link or Open File,
  Show in File Explorer (Reveal in Finder), Copy Link. On a selection:
  Open Selection (a URL or a file), Search Google for "…" (the engine is a
  setting: Google, DuckDuckGo, Bing, Kagi, Startpage or a URL of your own),
  Send Email to an address, a number in hexadecimal or decimal and a Unix
  time as a date (choosing one copies it), Copy Base64-Encoded and
  Base64-Decoded, Send Selection To another pane, and Save Selection as
  Snippet. Then Copy, Paste, Select All, Clear Buffer, Paste Snippet, Clear
  Scrollback, Find…, new windows, tabs and splits, Move and Swap With Pane,
  Save Contents…, Rename, Broadcast Input to Tab, Lock Pane, Close,
  Restart and Bury (the pane goes, still running, to a Buried space).
  Settings › Terminal sets the search engine, lists the snippets to rename
  or delete, and can keep the terminal's short menu instead.
- **Shell integration, as iTerm2's.** The shells QuaRex starts (PowerShell,
  zsh and bash) mark their prompts, commands and output (OSC 133). A right
  click then offers Copy Command, Copy Output, Copy Command and Output,
  Select Output and Re-run Command, for the command under the pointer or
  the last one, and Previous and Next Prompt (Command+Up and Down on macOS,
  Control+Shift+Up and Down elsewhere); the palette has them too. Settings ›
  Terminal › Shell Integration turns the marks off.
- **Copy Mode, Copy with Styles and annotations.** Copy Mode (⇧⌘C, or
  Control+Shift+X) selects with the keyboard: arrows or h j k l, Home and
  End, Page Up and Down, g and G move; v starts a selection; y copies;
  Escape leaves. Copy with Styles copies a selection with its colors, as
  HTML. Annotate Selection… pins a note to text: a line under it and a dot
  whose tooltip is the note follow it as output scrolls; a click on the dot,
  or the menu's Annotations, edits or removes it.
- **Quake terminal.** Press F12 in any app and a QuaRex terminal drops down
  from the top of the screen, over full-screen apps too, on the screen the
  pointer is on; press it again, or go elsewhere, and it goes back up. It
  shows a space of its own (Quake), whose tabs, splits and machines the
  standalone windows leave alone, and it keeps QuaRex running in the
  background with its tray icon, which shows it with a click and has New
  Window, Settings… and Quit in its menu. Settings › Quake picks the key
  (F9 to F12, Ctrl+` or Alt+`, Ctrl+Space…), the height (30 % to the whole
  screen), the screen, whether it hides as QuaRex loses the focus, the tray
  icon, and starting at login, which the installed app turns on the first
  time, its windows staying closed till you ask for one. On Windows QuaRex
  reads the key from the keyboard itself, as Windows keeps F12 from hot keys
  for its debugger, so F12 works with no change to the system; an app run as
  administrator keeps the key while it is in front. On a Mac keyboard F12
  takes fn, unless the function keys work as standard keys.
  Its title bar has no label: its controls, where a window has its own,
  tell it apart. A pin keeps it down as you switch apps (lit while it
  does); a small screen glyph, its top band as high as the quake terminal,
  opens a panel with the key and whether it works, the heights drawn as
  screens, the screen it drops on (Follow the Pointer, Primary, or a map
  of your displays as they stand), the pin and its settings; the hide
  button carries the key. A grabber at its bottom edge resizes it live,
  snapping near the presets; a double click gives it the whole screen and
  back; pushed up, it stops at the smallest height.
- **Browser panes.** New Browser Tab, or Split with Browser, opens a pane
  that shows a web page in the system's web view: an address field, back,
  forward and reload in its header, and the page's title on its tab. The
  page lives while its tab does, and opens again at its URL when QuaRex
  starts. A browser pane belongs to this machine, so a remote tab takes
  none, and Find searches terminals alone. Only http and https pages
  open; a page is untrusted, so it reaches no QuaRex code, asks for no
  permission, opens no window of its own and downloads nothing.
- **Note panes.** New Note Tab, or Split with Note, opens a pane that is a
  sticky note: free text you type in place, named by its first line. The
  layout keeps the text, so it is there when QuaRex starts. A note pane
  belongs to this machine, so a remote tab takes none, peers and the API
  never see it, and Find searches terminals alone. With a note focused, the
  text-size keys (`⌘+`, `⌘−`, `⌘0`) resize its text, a note at a time, and the
  eye button or `⌘E` shows it as rendered Markdown (links open in the browser,
  images show their descriptions); the pencil button or `⌘E` edits again. On
  Windows and Linux the key is `Ctrl+Shift+M`, and a terminal keeps it unless
  a note has the focus.
- **Persistent sessions.** Shells run in a session server, a background
  process of the same binary (`QuaRex -server`). Quit QuaRex and everything
  keeps running; open it again and every tab, split and pane comes back as
  it was, programs still running. The server keeps each session's screen in
  a headless libghostty-vt emulator and sends a snapshot on attach, so
  full-screen programs (lazygit, vim, htop…) come back exactly. A server
  restarted (`quarex server restart`, or the app on Windows replacing an
  older one once asked) brings its sessions back as new shells at their
  panes' directories; Quit and End All ends them. How the server keeps
  the screens: docs/session-server.md.
- **Kitty graphics.** Images sent by file path are read where the program
  runs, including on a remote host, and are shown in-band; a window that
  attaches again replays them.
- **Find and links.** Cmd+F searches the focused pane's screen and
  scrollback, with the match count and next/previous; Escape closes it.
  Command-click (Control-click elsewhere) opens URLs through the system,
  and file paths relative to the pane's program.
- **Spaces.** Like a Rex session, a space is a set of tabs of its own, with a
  name such as `icy-ridge` and a color of its own, and each window shows
  one. The space chip in the title bar, or atop the sidebar, lists the
  spaces with their tabs and the window that shows them, and makes,
  renames and closes them; so do the Space menu and the command palette,
  whose Change Space… finds one by its name. New Window opens a window of
  a new space, and Move Tab to New Window moves a tab to one. Choosing a
  space another window shows brings that window to the front. Closing a
  window keeps its space, its programs running; Close Space asks, then
  ends its terminals. QuaRex opens again the windows open when it quit,
  each on its space; terminals that no space has, as after a crash, get
  tabs in the first.
- **Single instance.** QuaRex runs once: opened again, it brings the
  window used last to the front, or opens one. The installed app and
  `mygo dev`'s QuaRex Dev each run once, apart, and an app given a
  `QUAREX_DIR` of its own runs beside them.
- **Program activity.** The server watches each terminal's foreground
  process (`tcgetpgrp`, `sysctl`, `proc_pidinfo`; on Windows, the shell's
  newest child, its command line and directory): headers and tabs name the
  program (`Node`, `Git Changes` for lazygit, `Codex`, `SSH host`…) and its
  working directory, a green dot shows a program printing, and an orange dot
  marks a pane whose program finished or rang the bell out of sight. When
  the window is in the background, a long command finishing posts a
  notification. A session's most urgent program status shows in the
  session picker and the sidebar, and rootshell sees it as the pane's and
  tab's `agent_status`.
- **Agent skill and hooks.** `quarex skill setup` finds Claude Code, Codex,
  OpenCode and Pi, installs a `quarex` skill into each, and adds a
  session-start hook to Claude Code and Codex that tells the agent its
  session and pane and how to drive QuaRex from the command line. It adds
  only its own hook and leaves other settings, hooks and skills as they
  were; `quarex skill status` says what is installed, and `quarex skill
  remove` removes only what it added. `--project` keeps the skill in the
  repository, and `--dry-run` reports first.

- **Tab icons** stack the tiles of a tab's programs, the focused pane's in
  front, as Rex does. Tabs reorder by dragging, rename by double-click, and
  have a context menu.
- **Vertical tabs.** Settings ▸ Appearance places the tabs above the panes,
  or in a sidebar on the left or the right side of the window. Drag the
  sidebar's inner edge to resize it (double-click resets it), and Toggle
  Sidebar (⌃⌘S) hides and shows it. "Show pane headers" off hides the
  panes' headers while the sidebar shows on the left; they always show
  when it is hidden or on the right, as in Rex.
- **Pane animations.** Panes spring into place when they move, split or
  zoom, and new or closing panes pop in and out. Settings ▸ Appearance ▸
  Animation style chooses Snappy, Natural or Off, which also sets how the
  sidebar shows and hides. While the system's Reduce Motion is on,
  animations stay off.
- **Infinite canvas (experimental).** Settings ▸ Appearance ▸ Experimental
  ▸ Infinite canvas lays every tab out as free boxes on an endless plane,
  each pane where it showed. Scroll or drag the empty plane to pan, or
  hold Space over it and drag anywhere; pinch, or hold Ctrl or Cmd and
  scroll, to zoom (25% to 200%), and Reset Canvas View in the palette goes
  back to the start. Right-click the empty plane for a new terminal,
  browser or note there. Move and resize a box by its header and edges; a
  split puts a box of the same size right of or below the focused one. A box keeps its size as the window resizes or the canvas
  zooms, so its terminal keeps its columns and rows. Turning it off docks
  every box back into the tab's splits. It may change or go away.
- **Host chip** with the machine's name and model; its popover shows the
  chip, memory, OS and the session server, and a remote host that is not
  connected with a button to Settings › Remote (Add Remote Host… while
  none is saved).
- **Command palette** (⇧⌘P, Ctrl+Shift+P, or the ⌘ button): every command, and every pane
  to jump to, fuzzy-matched.
- Light and dark appearances (View ▸ Appearance), text size (⌘+ ⌘− ⌘0),
  JetBrains Mono embedded, and the Nerd Fonts' icons (Symbols Nerd Font
  Mono) after it, as Ghostty has them: the icons of prompts such as
  oh-my-posh, Starship or Powerlevel10k, and of `ls` and editors, draw
  in any font, with no Nerd Font installed.
- English. The messages live in `locales/en.json`; a language added
  beside it brings back Settings ▸ General ▸ Language.

## Shortcuts

| macOS | Windows, Linux | |
|---|---|---|
| ⌘T | Ctrl+Shift+T | New tab (asks which machine and terminal) |
| ⌘D / ⇧⌘D | Alt+D / Alt+Shift+D | Split right / down (asks which machine and terminal) |
| F12 | F12 | Show or hide the quake terminal, from any app |
| ⌘W / ⇧⌘W | Ctrl+Shift+W | Close pane / tab |
| ⇧⌘↩ | Ctrl+Shift+Enter | Zoom the pane |
| ⌥⌘ arrows | Alt+arrows | Focus the pane in that direction |
| ⌃⌘ arrows | Alt+Shift+arrows | Move the nearest divider |
| ⌃⌘= | | Equalize panes |
| ⌘1…⌘9, ⇧⌘[ ⇧⌘], ⌃Tab | Ctrl+Shift+1…9, Ctrl+PageUp/PageDown, Ctrl+Tab | Switch tabs |
| ⇧⌘R | Ctrl+Shift+R | Rename tab |
| ⌘N | Ctrl+Shift+N | New window, of a new session |
| ⇧⌘N | | New session |
| ⇧⌘O | Ctrl+Shift+O | Change session |
| ⌃⌘] ⌃⌘[ | Ctrl+Shift+PageDown/PageUp | Next / previous session |
| ⌘J | Ctrl+Shift+J | Jump to the pane that needs you |
| ⇧⌘J | | List what needs you, by state, across windows and hosts |
| ⌃⌘S | Ctrl+Shift+S | Hide or show the tabs' sidebar |
| ⇧⌘P, ⌘P | Ctrl+Shift+P | Command palette |
| ⌘K | Ctrl+Shift+K | Clear |
| ⌘+ ⌘− ⌘0 | Ctrl+= Ctrl+- Ctrl+0 | Text size |
| ⌥⌘Q | | Quit and end all sessions |

Elsewhere than on macOS, Control and a letter are the terminal's (Ctrl+C,
Ctrl+D, Ctrl+W…), so QuaRex's shortcuts take Shift too, as copying and
pasting do (Ctrl+Shift+C, Ctrl+Shift+V), and none take Control and Alt,
which type characters (AltGr) on many keyboards.

With nothing selected, ⌘C (Ctrl+Shift+C elsewhere) goes on to the
program, as in Ghostty: a program that selects with the mouse, as Codex
CLI, copies its own selection.

### Settings

Settings… (⌘, on macOS, Ctrl+, elsewhere; the gear in the title bar or at
the sidebar's foot, the app menu on macOS and the Shell menu elsewhere, and
the command palette) opens a window of its own with a sidebar of sections: Appearance (light,
dark or system; tab placement; pane headers; animation style; text size;
language), Terminal (font, cursor style and blink, copy on
selection; what Split and New Tab ask, and your profiles), Quake (see
[Quake terminal](#what-it-does)), Theme (any of Ghostty's themes, or follow the config),
Keyboard (QuaRex's shortcuts, read only), Remote (see
[Remote access](#remote-access) and [Remote hosts](#remote-hosts)),
Network (see [Remote hosts](#remote-hosts) and [System Tailscale](#system-tailscale-desktop))
and About (version, Check for Updates…).
The choices go to `settings.json`, as do the sidebar's width and whether
it is hidden.

Remote turns the server's remote access on and off, and manages it:
whether allowed clients share the sessions open here, pairing a new device (Start pairing opens a five-minute window; each
request shows its name and fingerprint, to Approve or Reject), the list
of allowed clients (revoke one, or add one by name and public key), this
machine's own key and its fingerprint, and, while listening, the address,
hidden until you show it, with Copy and Regenerate (which asks first). The
page asks the server every two seconds while it shows. Its Remote Hosts
group is the other side: the machines this one connects to (see
[Remote hosts](#remote-hosts)).

Precedence: what you set in Settings, over Ghostty's config, over QuaRex's
defaults. "Reload Ghostty Config" reads the config again but never
replaces a choice made in Settings; "Use Ghostty config" (Terminal)
forgets the font, cursor, and copy-on-selection choices, and Theme's
"Follow Ghostty config" the theme's. A theme chosen in Settings also
replaces the config's `background`, `foreground`, `palette`, and the other
colors, which belonged to its own theme. Font, theme, copy on selection,
and the cursor apply to open panes at once.

### Ghostty configuration

QuaRex reads Ghostty's config: `$XDG_CONFIG_HOME/ghostty/config.ghostty`
(`config`), else `%LOCALAPPDATA%` on Windows or `~/.config`; on macOS also
`~/Library/Application Support/com.mitchellh.ghostty/`. `config-file`
includes work. `QUAREX_GHOSTTY_CONFIG` names one file instead.

Supported: `font-family`, `font-size`, `font-feature`, `font-thicken`,
`adjust-cell-height` (percent), `theme` (also `light:…,dark:…`),
`background`, `foreground`, `cursor-color`, `cursor-text`,
`selection-background`, `selection-foreground`, `palette` (0–15),
`cursor-style`, `cursor-style-blink`, `scrollback-limit`,
`macos-option-as-alt`, `copy-on-select` (`clipboard`; `true` is
Linux's selection clipboard, so it copies nothing), `right-click-action`,
`minimum-contrast`, `clipboard-read`, `clipboard-write`,
`window-padding-x`, `window-padding-y`, `window-padding-color`,
`image-storage-limit`, `search-background`, `search-foreground`,
`search-selected-background`, `search-selected-foreground`, `keybind`.
`keybind` takes `clear`, `performable:`,
and the actions unbind, ignore, copy_to_clipboard, paste_from_clipboard,
select_all, clear_screen, increase_font_size, decrease_font_size,
reset_font_size, and scroll_page_up, scroll_page_down, scroll_to_top,
scroll_to_bottom; `global:`, `all:`, and `unconsumed:` binds, sequences
(`a>b`), and other actions are skipped. QuaRex's own shortcuts come
before keybinds. A text size set with ⌘+ ⌘− wins over `font-size`;
⌘0 goes back to it. With a theme or background, panes draw its
background, and unless View ▸ Appearance names one, the window turns
dark or light by it, as Ghostty's `window-theme = auto` does (not with
`light:…,dark:…`, which follows the system). "Reload Ghostty Config"
(command palette, View menu) applies fonts, themes, `copy-on-select`,
and `minimum-contrast` to open panes; the other options apply to new
panes.

`minimum-contrast` is 3 unless Ghostty's config or Settings ▸ Terminal
(`minimumContrast` in settings.json) sets it: text closer than that to
its background, colors programs set too (ANSI, 256 and RGB), turns
lighter or darker in its hue, in local and remote panes alike. 1 turns
the correction off. Unset, Ghostty's is 1, so QuaRex corrects colors
where Ghostty would not.

Options QuaRex maps fully: the colors and fonts above, `cursor-style`,
`cursor-style-blink`, `scrollback-limit`, `macos-option-as-alt`,
`copy-on-select`, `right-click-action`, `minimum-contrast`,
`clipboard-read` (allow, ask or deny), `clipboard-write` (allow or
deny; ask is treated as deny), the first value of `window-padding-x`
and `window-padding-y` (the library has one width and one height),
`window-padding-color`, `image-storage-limit` (0 refuses images), and
the supported `keybind`s. Options it reads but leaves out, as the library
has no mapping: `background-opacity`, `background-blur`,
`mouse-hide-while-typing`, `scroll-multiplier`, `window-padding-balance`,
and window decorations. Other options are ignored, and `quarex config check`
lists the Ghostty options it ignores.

## Remote access

### System Tailscale (desktop)

On macOS and Linux, QuaRex uses an existing, running system Tailscale
client to discover QuaRex hosts and connect to their terminals. Devices
with the same Tailscale user in the same tailnet appear in Remote Hosts
once they have a compatible QuaRex server and Tailscale policy allows
TCP port 7464. Click Connect on a host to open or reattach to a session.
The server only listens on its Tailscale interface and checks each
connection's device identity with the local Tailscale client.

Turn **Tailscale discovery and connections** on in Settings → Remote, or
use `quarex remote tailscale on`. The mode is off by default and waits
when Tailscale is unavailable. `quarex remote status --json` reports the
local mode and the hosts it has discovered. The existing **Share open
terminals** setting controls access to sessions created by other clients.

### Tailcat

The session server can also listen on a
[tailcat](https://github.com/tailscale/tailcat) address: Tailscale's data
plane without its control plane, so WireGuard end to end, through a DERP
relay or directly, with no Tailscale account. Remote access is off by
default. Each machine has a client key (`remote-client.json`), and the
server serves the keys of its allowlist only: it reads the key of every
connection, and closes those of other keys at once, saying first that
they are not allowed (so that a client tells a refusal from a network
that dropped). With an empty
allowlist nobody gets in. The server keeps its keys (`remote.json`, mode
0600), so its address stays the same; regenerating them makes a new one,
and the old address stops working.

Pairing adds a client without copying its key by hand:

1. On the server, turn remote access on and Start pairing: a window
   opens for five minutes.
2. On the client, ask to pair with the server's address and a name
   (`remotectl pair ADDRESS alice-laptop`). It prints a fingerprint, as
   `01234567-cdef`.
3. The request shows on the server with its name and fingerprint.
   Approve it only if the fingerprint is the one the client printed:
   anyone with the address can ask too.

While the window is open, a client not allowed may ask to pair and
nothing else; at most 8 requests wait, one per key, and they are
forgotten when the window closes. They are never saved.

On one local network there is no address to copy. A server with remote
access on tells the network it is there (Bonjour, `_quarex-pair._tcp`:
its computer's name and system, never its address), and Settings › Remote
› Remote Hosts → Add Remote Host… lists it under On this network. While
its pairing window is open the server shows a pairing code, six digits
(the Remote page's pairing card, or `quarex remote pair start`). Pair,
on the other machine, asks for that code and gives it to the server for
its address. Both ends prove they know the code without sending it (a
PAKE, CPace), and the address comes back under the key they then share:
nothing that crosses the network tells the code or the address; a
device that does not know the code gets nothing, and has eight guesses
at a million before the window must be opened again, with another code;
and a device that answers in the server's name without the code is
found out, and not paired with. The request, the fingerprint and the
approval then follow as above.

What to know before turning it on:

- The address is a secret: it holds the server's key and the WireGuard
  pre-shared key. Do not paste it where others read it. QuaRex never logs
  it, nor any key.
- The allowlist is what keeps others out. A leaked address alone gets
  nobody in, but it lets anyone ask to pair while a window is open:
  compare fingerprints, and regenerate a leaked address anyway.
- An allowed key means running commands as this user: a client may
  start any program with any environment. From a shell there it can
  reach the local socket, and so change the layout, remote access, and
  sharing itself. Trust it as you would an SSH key.
- Share open terminals (Settings › Remote, off by default, kept in
  `remote.json`) decides what else a client sees. Off, each client lists,
  attaches to, resizes and kills only the sessions it created; the others
  (this machine's window's, other clients') are refused. On, every allowed
  client sees and uses every session. Turning it off detaches clients
  from the sessions they did not create. The server remembers which key
  created a session, in memory, and keeps it across an in-place upgrade;
  a session survives a revoke and approval of the same key as its own.
  Local connections always see every session. A session a client opens
  here gets a tab in this window too, last among this machine's tabs and
  without taking the focus, rather than running unseen.
- Over the connection itself, a remote client may list, create, kill,
  resize and attach to sessions only, and read what the machine is and
  which shells it has (`host.info`: its shells, Windows Terminal profiles
  and SSH host aliases, never an address, a user or a key, as the hello
  says already). It may not shut the server down,
  read or set the window layout, or see or change remote access
  (`remote.*`, pairing included): those are for the local socket only.
- Every connection is limited: a line of requests of at most 1 MiB, a
  terminal of 1 to 1000 columns and rows, and 8 kills at once.

### The coordinator

Pairing every machine with every other does not scale, so a
coordinator can turn remote access into a network, the way Tailscale
does: each machine joins **once** with a network key held by a small
always-on service (`gcoord`, see docs/coord.md), which keeps the
directory of members and their addresses. Every member then trusts and
finds every other member through it, without pairing windows or
addresses copied by hand; the terminal traffic itself still goes peer
to peer over tailcat, and the coordinator down does not break machines
that already know each other. Whoever holds the network key may run
commands on every machine in it, so it is treated like the addresses
themselves: never logged, never written anywhere wider than the
member's own state.

Joining is manual, for any coordinator a user runs themselves: in
Settings › Remote (remote access on), paste the join URL the
coordinator printed and its network key (`remotectl join URL KEY
[NAME]` does the same without the app). The server then asks the
coordinator every half minute: members come and go with its directory,
their addresses become this machine's remote hosts by themselves
(Settings › Remote › Remote Hosts shows them without Remove, for the directory,
not a hand, decides), and a member removed there — `gcoord kick` on
the coordinator, or Remove on the network card — loses its
connections on every machine within its next ask. Leaving the network
(Leave, or `remotectl leave`) drops the members and tells the
coordinator best effort. Pairing stays for those who run no
coordinator; a machine in a network never needs it.

### Remote hosts

Remote clients pair by name and keep their key and created/last-seen
times; a client's hello names its principal, `quarex clients` lists the
live attachments with their principal and age, and `quarex ls` shows the
principal that owns each session. Settings › Remote
Hosts can share this window's layout read-only, and each allowed client
can be given all sessions, and the layout with them, or only the
sessions it opened; the shared layout is filtered to sessions that client
may use; panes it may not use are shown as unavailable placeholders, and
panes of other hosts are left out; `quarex -S HOST layout`
reads it and `events` follows changes.

A session attached by several clients takes the size of the one the
user's focus is on, if that machine had input in the last minute; see
docs/session-size.md.

For a Linux service shared by several paired clients, see
docs/shared-server.md. Per-user isolation and
PAM login are a separate proposal: docs/login-server-rfc.md.

Settings › Remote › Remote Hosts connects this machine to other machines' session
servers, whose sessions then open in tabs of the window beside its own.
Add Remote Host… asks for the host's address (the one its Settings ›
Remote shows; the field hides it), a name for it, and the name this
machine pairs as (the computer's name, at first):

1. On the host, turn remote access on and Start pairing.
2. On this machine, Add Remote Host… with its address. A host that allows
   this machine already is saved at once; otherwise QuaRex asks to pair
   and shows this machine's fingerprint.
3. On the host, approve the request that shows the same fingerprint. The
   sheet tries again every three seconds and saves the host once it is
   let in.

The hosts are kept in `hosts.json` beside the settings, readable by the
user only, and not in `settings.json`: their addresses are secrets, which
QuaRex never logs nor shows. Each host's row shows its state (Connecting,
Connected, Reconnecting (attempt N), or why it is not connected) with
Retry, which tries at once, and Remove. Removing a host closes its tabs
and its panes in tabs of several machines, and leaves its sessions
running on the remote server.

QuaRex keeps a connection to each host and connects again when it drops,
waiting longer after each failure, up to 30 seconds. New Tab opens on the
active tab's host, and a split on its pane's; New Tab on a host (the
command palette, or the + of a host's name in the sidebar) picks one, and
Split Right on a host or Split Down on a host (the command palette) puts a
pane of that machine beside the focused pane of any machine. A tab may so
hold panes of several machines: each pane's header names its machine, the
tab shows the icons of the others, and the sidebar lists it under this
machine when a pane of it runs here, else under its first pane's host.
Panes and tabs drag between tabs of any machines; a tab dropped on another
machine's tab asks to teleport there, or to add its panes to that tab,
where they keep running on their own machine.
Closing a tab or a pane ends its session on its host, once connected
again if it is not now. With hosts saved, the sidebar lists
the tabs under their host's name, this machine's first, and tabs above
show a host's name on its tabs. A pane whose host is away keeps its
screen under "Reconnecting to …", drops what is typed meanwhile, and
attaches again by itself; one whose session ended there closes. The
window's layout keeps the host of each pane, so a host's tabs come back
when QuaRex opens again, attached once the host answers. Sessions the host
lists that no tab shows (opened in the host's own window, or by another
client, while the host shares its sessions) open last among the host's:
one tab for each session, or, while the host shares its layout, one tab
for each tab that layout shows, with its splits, so two panes side by
side there are not two tabs here; a tab closed here ends its session as
any other and does not come back. When the host stops sharing, the tabs
of sessions this machine did not create close here and their sessions go
on there.
`go run ./tools/remotectl pair ADDRESS NAME` asks to pair from a machine
without the app.

### Teleport

Teleport to… (the pane's menu, or Teleport to a host in the command
palette) moves a pane's work to a connected host: the Git work tree's
commits, changes and untracked files, Claude Code's or omp's conversation, and the
scrollback. The host makes a work tree of its clone of the repo,
`.gorex/teleport/<id>` on a branch `teleport/<id>`, or, for work coming
back to a directory it left untouched, takes it there again; and starts
`claude --resume` or `omp --resume` there, or a shell; the pane then shows that session, in
a tab of the host's, and its own session ends. Only a shell at its prompt
or Claude Code or omp waiting for the user can go, from this machine;
`quarex teleport PANE HOST` does the same from the command line. Dragging
a tab of one pane onto another host's tabs, or its name in the sidebar,
asks to teleport it there. See docs/teleport.md.

## Importing a Rex session

QuaRex reads a Rex server and makes the same shape here: a Rex session
becomes a space, a window a tab, and a block a pane. Each pane runs
`quarex rex-mirror`, which draws what the Rex block shows and sends what
is typed there to it, so the two show the same program.

```sh
quarex rex-import --session work            # one session, by label or ID
quarex rex-import                           # every session
quarex rex-import --shell                   # shells, not mirrors
quarex rex-import --resize                  # mirrors give their blocks the pane's size
```

The window imports without a terminal: **Space ▸ Import from Rex**, or the
command palette's *Import from Rex*, mirrors every session the record does
not have yet and says how many it made in a notification; a failure opens a
dialog. The Rex server defaults to `$REX_SERVER`, else `rex/server.sock` in
the platform's data directory; `--rex` names another. What a run imported
is recorded in `rex-import.json` in QuaRex's data directory, so a second run
leaves those sessions alone. The QuaRex window must be open: it makes the
spaces, tabs and panes.

A mirror is a view with input. The data stream starts with a snapshot in
Ghostty's binary format, which only a Ghostty terminal restores, so the
mirror draws the screen from the escape sequences Rex renders (`format`
vt), reads past the snapshot by its record format, and passes the
program's output on as it comes; Rex's own APC messages are dropped. Keys
go to the block as text. What the block's program prints reaches the pane
as it would reach a terminal itself: the mirror does not filter its
escapes otherwise, as a terminal multiplexer would not.

A tab keeps its window's label only when a person gave it one; Rex's own
labels, such as `Window 2b63efe2`, are left out, and the tab follows its
block's title, as the Rex window does. The tab's tile is the program the
block runs — Claude Code, omp, a shell — which the mirror reports through
the program status protocol (OSC 7501) along with the status Rex keeps for
it, so a working or finished block shows as it does in Rex.

A mirror's pane is a terminal of QuaRex's, so what the Rex program writes
reaches it, escape sequences and all. A layout's exact shape is not kept:
the blocks are made in layout order, each split beside the one before, so a
nested split's panes can sit in different halves than Rex put them, and
ratios are not kept.

## rootshell

[rootshell](https://github.com/kitknox/rootshell), on iOS and the Mac,
shows this machine's tabs over SSH as it shows herdr's in its full control
mode: QuaRex plays herdr. `tools/rootshell/herdr`, installed on the host,
runs `QuaRex control` in herdr's place, a bridge to the server of the QuaRex
already open. The layout stays the desktop's: rootshell shows it, and
changes it through the QuaRex window. Setup on macOS and Windows hosts, the steps in
rootshell, limits and troubleshooting: docs/rootshell.md.

## Rex's iPhone app

Rex's own apps, the iPhone one among them, connect to QuaRex as to a Rex
server: the QuaRex server serves Rex's API (revision 11), on the local
network to the networks you allow (Settings › Remote), and on the tailnet
through a Tailscale device of its own. A space is
a Rex session, a tab a window, a pane a block, and a floating pane a
floating layer; terminals stream as Ghostty snapshots, as Rex's do. Setup,
pairing, what differs from a Rex server, and troubleshooting:
docs/rex-api.md.
