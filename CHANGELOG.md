# Changelog

QuaRex's releases. QuaRex began from GoRex 0.18.0, whose changelog is in
GoRex's repository (si-mods/gorex) and in this one's first commit.

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
