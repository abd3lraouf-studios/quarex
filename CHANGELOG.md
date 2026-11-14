# Changelog

QuaRex's releases. QuaRex began from GoRex 0.18.0, whose changelog is in
GoRex's repository (si-mods/gorex).

## 0.6.0

* Arabic and Hebrew in the terminal read right to left, an Arabic word's letters joined and its tashkeel in its places, in bold, italic, underlined, struck or colored text too, even when only part of a word is, while tables, prompts and copied text keep their order. Settings › Terminal › Right-to-left text turns it off for a program that reverses such text itself.
* Split Right, Split Down and New Tab ask where and with what in one picker: your projects beside what opens in them (profiles, bookmarks, shells, WSL, SSH hosts, pages), each program with its own mark. The search field keeps the keyboard: Tab switches columns, Alt+1–9 picks a project, Alt+O adds a folder, and ? shows every key.
* QuaRex reaches a machine over SSH as well as Tailscale, by whichever route is ready first. Settings › Machines shows the route a machine uses and lets you set its SSH host or choose one route, and Add Remote Host… lists the hosts of your SSH configuration.
* On Windows, MSYS2's zsh, bash and fish start as MSYS2's own launcher starts them, so Oh My Zsh and powerlevel10k load as on the Mac. Settings › Profiles › Default shell chooses what new tabs and panes start. Every WSL distribution and Windows Terminal profile shows once, the default distribution first.
* Tint with Theme (Settings › Appearance) colors every window from the terminal theme, Settings too: the background, panels, text, hover and the accent, kept readable whatever the theme. A space's color stays its accent.
* A trackpad scroll past the top of the scrollback no longer shakes the rows.
* A Settings switch redrawn during an animation no longer crashes QuaRex.
* Two notices that come at the same moment no longer replace each other.
* Screen readers tell the Add Remote Host sheet's Add buttons apart: Add by address, Add SSH host, and Add beside each SSH host.

## 0.5.0

* While QuaRex is not in front, notices are QuaRex’s own cards that float over every app, one per session. A permission’s card has Allow and Deny. A Quake pane’s card drops in at the top of Quake’s screen (Settings › Quake › Peek from the top). Settings › Notifications chooses cards or the system’s notices and lists recent ones.
* Claude Code, Codex, Gemini CLI, OpenCode and Pi report whether they are working, waiting for you or done through their own hooks, which `quarex skill setup` installs. QuaRex knows an agent waits for a permission even when it prints nothing.
* The Quake hotkey drops on the pane that needs you most. Stay While Working keeps Quake down while an agent works. Open in the Folder You Are In opens Quake in the folder of the File Explorer or editor window in front. With several screens, Quake keeps a height per screen.
* A link or a file you open from QuaRex comes up in front of it, and of the Quake terminal, even when the browser was already running.
* The focus comet between panes lands on the cursor an agent draws itself.
* On Windows, the Quake terminal stays down while a screen capture tool’s selector (Shutr, Snipping Tool, ShareX, Greenshot) is in front, so it can be captured.

## 0.4.1

* An update asks once whether to restart. Installing it, in the background too, never restarts your sessions or opens a second dialog. On Windows, Restart QuaRex says that running programs and their scrollback end, then reopens your tabs and folders on the new session server.
* The updater's windows stay above a pinned Quake terminal.

## 0.4.0

* Each desktop Settings pane has an illustrated header and subtitle tuned for light and dark appearances. Visual indicators show server and permission states, with details available on hover and through assistive technology.
* Settings headings and controls move again, and the Server pane shows live connections with a typing prompt and readouts that count up. Settings search finds more controls and moves keyboard focus to the selected result.
* Settings stays above pinned Quake. Returning to Settings restores keyboard input there, and opening Quake before its first terminal is ready creates a single tab.
* On macOS, the menu bar item opens its menu on the display where you click it.
* Sessions, notes and layouts recover from interrupted saves. A rejected tab close preserves its notes.
* Remote control requires explicit LAN access and rejects untrusted browser origins.
* Cancelling a download before it is saved discards the partial file, even if the final bytes have already arrived.

## 0.3.0

### Features

* **settings:** Settings look and work as macOS 26's: the page's title in the title bar, capsule switches, segmented controls with icons, pop-up buttons, and pages that fill a wide window. Every page is reworded: short, plain, and a hint only where the label can't say it
* **settings:** Appearance picks the color scheme, the interface style (Classic or Glass) and the app icon from pictures, on QuaRex's own field of glyphs
* **settings:** theme cards show each theme's text, QuaRex's prompt in its green, its cursor and all sixteen of its colors
* **settings:** the Server page is a stage: the machine lights up in its server's state, its name decodes, the devices attached orbit it with live connections, and the numbers that matter count up on frosted glass
* **settings:** Integrations show each agent's skill and session hook, with Let agents name sessions, and the text agents read as a session starts
* **agents:** agents label their session after their task when you let them, OpenCode and Pi too, which learn it from QuaRex's skill
* **app:** six app icons, Default, Bright, Twilight, Aurora, Ember and Glacier, on macOS, Windows, Linux and iOS
* **app:** as a split or a close moves the focus, the cursor flies to the pane that takes it

### Fixes

* **quake:** notifications from the quake terminal show again once it is hidden
* **cli:** `quarex rename` takes flags after the name, as `quarex rename -s ID NAME --json`
* **settings:** rows no longer show twice their padding

## 0.2.0

### Features

* **welcome:** a walkthrough greets the first launch, on a stage over the whole window: it types and runs `quarex init`, then takes you through the look, the agents' skill and Full Disk Access, your keys migrated by an agent, and the keys worth knowing. It fits every window, from a small one to a 4K screen
* **app:** the Cinematic motion style, the default: things come into focus, panes rise into place, a space opens on a ripple of glyphs, Settings' titles are typed and decode, and new tabs' names decode
* **settings:** a Permissions page shows each macOS permission's state live, with Grant…, Ask… or Open, and a guide that walks you through System Settings in eleven languages; programs in QuaRex can ask for the microphone, the camera and the rest
* **settings:** a Server page controls the session server: restart it, update it keeping every program, end its sessions, turn Remote Control on or off, see the clients attached, open its log or copy a debug report
* **settings:** more of what Rex's Settings have: notifications per kind of news with sounds and the Dock badge, notices in the window, the agents' skill and hooks per agent, Developer Mode with an API console, a global key to show or hide QuaRex, tinting, compact panes, headers on hover, pinch to zoom, three app icons, a theme for light and dark, Ghostty and iTerm2 theme import and a theme editor
* **terminal:** Insert Path (⌃⌘I) browses the pane's machine and types a path at the cursor, with the paths used last
* **terminal:** Display P3, a forced cursor style, the blink's speed, smooth scrolling, rounded selections, the selection in QuaRex red with a flash on copy, Force Theme Palette for Text, and the cursor is a bar by default
* **updates:** About has the update channel, Stable or Preview, and automatic checks and downloads
* **windows:** QuaRex installs with a setup wizard, for all users in Program Files or for you alone. The setup closes a running QuaRex first, an install for all users replaces your own, and it updates itself with an administrator's approval
* **launcher:** a split's picker opens in the half its pane will take, and blurs into place
* **app:** a folder group's bar drags the panes under it, as a pane's header would
* **quake:** Settings › Quake › Resize from the Window's Edges, on by default

### Fixes

* **quake:** on macOS the quake terminal slides in from above its screen and back out, as its Slide styles say: macOS kept it under the menu bar, where it only zoomed in and out
* **quake:** resizing stays on the quake terminal's screen and keeps what it shows; the grabber keeps the spot under the pointer and snaps to presets with no jump
* **windows:** a server the installer started finds pwsh, oh-my-posh and zoxide for its sessions, instead of falling back to Windows PowerShell

## 0.1.5

### Changes

* **updates:** QuaRex updates from [github.com/abd3lraouf-studios/quarex](https://github.com/abd3lraouf-studios/quarex), where its source and its releases are now public. Installs of 0.1.4 and before, which read their updates from `abd3lraouf-studios/quarex-releases`, move there with this update; nothing else changes for them

### Fixes

* **app:** a terminal belongs to the group of the folder its shell is in now, so a `cd` takes it out of its group and into the group of the folder it went to; a zoomed group whose focused terminal leaves it gives the tab back its panes

## 0.1.4

### Features

* **app:** terminals opened in one folder, side by side in a tab, form a group of that folder: a box in the folder's color under a bar with its name, path, Git branch, what its terminals are doing and how many there are. The bar zooms the group, splits in its folder, renames it, sets its color, copies its path and closes its terminals; the palette has Zoom Group, Next and Previous Pane in Group and Close Folder Group. A pane dragged next to its folder's panes joins the group
* **app:** the file manager's menu of a folder has Open in QuaRex (a tab in that folder) and Open in Quake Terminal; Settings › General turns them off, and the uninstall removes them
* **tray:** the tray's menu is in groups, each item with an icon of its own
* **windows:** menus are compact, as Windows 11's own, and a checked item in a menu with icons shows its check in place of its icon

### Fixes

* **quake:** dragging the grabber up to make the quake terminal small no longer puts it away when let go: it stops at the smallest height and stays down
* **quake:** on Windows another window, the taskbar's too, comes over the quake terminal, which stayed on top of every app the taskbar, Start or Alt-Tab opened
* **linux:** on Sway, Hyprland and KDE a click on another window takes the keyboard from the quake terminal, which now goes under the windows
* **terminal:** a double click selects a Windows path whole, its drive letter included, and a word, URL or path that a soft wrap splits across rows
* **menus:** a menu shows a separator only between two groups of items, never two in a row or one at an end

## 0.1.3

### Fixes

* **windows:** the installer is a Windows Installer package, `quarex-setup-0.1.3-amd64.msi` and `-arm64.msi`, built by the release itself: it runs no script of its own, so Microsoft Defender no longer mistakes it for a trojan as it did 0.1.2's first `.exe`. It installs for your user where the `.exe` did, takes over an install the `.exe` made, and `install.ps1` runs it with `msiexec`
* **settings:** on macOS the tray icon's switch and its hint say Show in the Menu Bar, where the icon lives; searching for "tray" still finds it
* **rex api:** a second QuaRex server on the same data directory, as one left running from another install, no longer writes over the listening gateway's status, so Settings stops saying "Not listening" while the local network listener serves

## 0.1.2

### Features

* **pairing:** pairing over the local network asks for a pairing code: the machine that pairs shows six digits (Settings › Remote, or `quarex remote pair start`), and Pair, on the other machine, takes them. Both prove they know the code without sending it (CPace), so neither the code nor the address crosses the network in clear, a device that does not know the code gets nothing, and one that answers in the machine's name is found out. A machine still on 0.1.1 does not answer one on 0.1.2: update both
* **remotectl:** `find` lists the servers of the local network, and `pairlan` pairs with one by its code
* **config:** a Rex `init.lua` loads: the `rex` table, Rex's action names (`client.tab.new`, `pane.balance`, `client.mode.enter`…), `require` beside the file, and a bad call, key or action skipped with its file and line while the rest loads. Keys can run Lua functions; `bindings()`, `modes()`, unbinding one binding, a whole mode or the app's own shortcut; keys a mode blocks; Escape leaves a mode; `meta`, `win` and physical keys (`ctrl+[KeyA]`)
* **config:** custom actions take `category`, `keywords`, `repeats`, object and array arguments and a JSON Schema, get `ctx.session_id` and `block_id`, and return a result; `quarex.exec`, `exec.start`, `json`, `log` and `client.queue`. The configuration hears the terminal's `bell`, `title_changed`, `pwd_changed`, `process_changed` and `child_exited`
* **actions:** split left, up and best fit, focus the next and previous pane, move (swap) a pane, close other panes and tabs, send a key, copy the pane's ID, copy and paste, rename a pane, go to a tab, move a tab back and forward, full screen, copy the config path, Install QuaRex for Agents
* **cli:** `quarex do` runs Lua scripts against the server's API, as `rex do` (`rex.call`, `rex.session.*`, `rex.on`, `rex.wait`, timers, `--all`, `--for`, `--action`), and actions by name; `actions`, `keymap`, `send-key`, `kill`, `whoami`, `api list|describe|call`, `completion`, `server start|stop|status|logs`; `split --left --up --ratio --label`, `ls -q`, `send -`, `capture --trim`
* **app:** the window shows the key mode it is in, and the keys of a sequence typed so far
* **rex api:** `desktop_notification` and `progress_report` events; `server.config_reload` reloads the Lua file
* **status:** a program that only reports its progress (OSC 9;4) shows as working, or failed, on its tab, its pane and the iPhone's inbox, as one that reports its status does; and the answer to the status protocol's query lists the states and kinds QuaRex takes

### Fixes

* **pairing:** a Mac finds the machines of its network though it has ports with no cable or a bridge, where it found none; a Windows PC no longer tells its virtual adapters' addresses
* **ios:** the Add button of a computer found on the network keeps its width
* **server:** a client told it is attached is the one whose terminal answers the program from then
* **status:** a program that asks whether the terminal knows the status protocol (OSC 7501) gets that answer before the device attributes', always; it could come second, and the program then reported nothing. A progress with a sign (`+40`) is none, and messages lose more characters that show nothing
* **app:** Reload Config reloads the Lua file too
* **windows:** the installer is a Windows Installer package, `quarex-setup-0.1.2-amd64.msi` and `-arm64.msi`, in place of the NSIS `.exe` that Microsoft Defender quarantined as `Trojan:Win32/Bearfoos.B!ml`, a false positive: the release's `.exe` files were replaced by packages of the same app. It installs where the `.exe` did, takes over its install, and `install.ps1` runs it with `msiexec`

## 0.1.1

### Features

* **pairing:** desktops pair over the local network, with no address to paste: Add Remote Host lists the machines found On this network, and Pair asks for the address, then pairs as with one pasted (the request, the fingerprint, the approval there)
* **ios:** the iPhone app finds the QuaRex servers of the local network, in Settings › Remote Hosts › On This Network, and a host added so follows its machine to a new address

### Fixes

* **pairing:** a look at the network that fails no longer closes the Add Remote Host sheet with a crash
* **app:** the installed app may start at login again, on macOS, Windows and Linux

## 0.1.0

### Features

* **app:** GoRex is QuaRex: its own name, identifier (dev.abd3lraouf.quarex), icon, data directory and command (quarex), which takes GoRex's settings, keys and remote access the first time it runs
* **quake:** a terminal that drops down from the top of the screen at a key that can be any, on the screen of the pointer or one of the user's, with spaces of its own, a tray menu, and windows of QuaRex's that come over it as any app's do
* **terminal:** iTerm2's menu of a selection, a link and a command, shell integration (OSC 133) for PowerShell, zsh and bash, Copy Mode, annotations, snippets, and prompts that draw again as a pane narrows
* **panes:** drag a pane or a tab between windows, the quake terminal's too, or out into a window of its own on any screen; splits start in their pane's directory
* **spaces:** quake spaces wear a badge; the spaces list draws each tab's splits and previews a space under the pointer
* **settings:** a search; pages that keep related settings together, with iOS-style tiles; the scrollback, the clipboard, contrast and padding; Restore Defaults; export and import
* **icons:** Font Awesome Pro throughout

### Changes

* **env:** the environment variables are QUAREX_*, and GOREX_* still read; sessions export both
* **module:** the Go module is github.com/abd3lraouf-studios/quarex
