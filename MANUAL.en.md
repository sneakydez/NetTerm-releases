# NetTerm manual

NetTerm is a terminal client for Windows to connect to routers, switches, servers and
Raspberry Pi over **SSH, Telnet, SFTP and FTP**, with buttons that send commands or passwords with one click.

## 1. Install and open

1. Download `NetTerm.exe` from https://github.com/sneakydez/NetTerm-releases/releases/latest
2. Save it wherever you like (Desktop, `Documents\NetTerm`…). **No installation needed.**
3. Open it with a double-click.
4. If Windows shows **"Windows protected your PC"**, click **More info → Run anyway**.
   It appears because the program is not digitally signed yet.

The first time it takes a few seconds to open while Windows scans it.

## 2. First steps

1. Click **＋ New session**.
2. Choose the protocol (**SSH**, **Telnet**, **SFTP** or **FTP**). The port is filled in automatically.
3. Enter a **name**, the **host** (IP or name) and, if you want, the **user** and **password**.
4. Click **Save and connect**.

To connect later: **double-click** the session in the left panel.

## 3. The screen

| Area | What it is for |
|---|---|
| Sessions panel (left) | Your saved sessions, grouped and searchable |
| `☰` (top left) | Show or hide the sessions panel (`Ctrl+B`) |
| Tabs | One per connection. The dot shows the status: green connected, yellow connecting, red disconnected. **Drag them** to change the order (`Ctrl+Tab` follows that order) |
| `🔍` | Search and filter in the terminal (`Ctrl+Shift+F`) |
| `📡` | Multi-send: type into several sessions at once |
| `▥` | Split screen: see 1, 2 or 4 terminals |
| `⚙` | Preferences (`Ctrl+,`) |
| `?` | This manual (`F1`) |
| Buttons bar | Your command and password buttons |
| Bottom bar | Active session, user, host and status; NetTerm version |

## 4. Sessions

- **Groups:** enter a group when creating the session (for example "Head office") and they will appear grouped.
- **Search:** type part of the name, IP or group in "Search session…".
- **Edit, duplicate or delete:** right-click the session, or the pencil ✎ when hovering over it.
- **Theme per session:** in the session form, choose its own theme. For example, "Production (red)" for
  critical devices, so you don't get the wrong window.
- **SSH private key:** in the form, "Private key" → "Browse…".

### If the password is wrong

NetTerm asks for the password in the terminal itself (what you type is not shown). Type it and press `Enter`.
If it works, a notice offers to **save it** in the session. `Esc` cancels.

> After several failed attempts, many servers (OpenSSH, routers) **block your IP for a few minutes**.
> If you see "The server closed the connection", wait and try again.

### Reconnect

If you close a session or the device closes it (`exit`, idle timeout), press `Enter` in its tab, or right-click the
tab → **Reconnect**.

If the connection **drops** (device reboot, network or VPN outage), an SSH or Telnet session **reconnects by itself**:
it makes attempts further and further apart (up to one every 30 s) for 15 minutes. `Enter` tries right away and `Esc`
cancels. If the password fails, it stops trying and asks you for it, so your user doesn't get locked out. No command is
repeated and the log continues in the same file. Set the minutes, or turn it off, in Preferences → Terminal.

The **keepalive** (every 60 s, also in Preferences → Terminal) stops a firewall from cutting an idle session and helps
notice a drop sooner. It doesn't prevent an idle timeout configured on the device itself.

## 5. Working in the terminal

- **Copy:** select the text with the mouse; it is copied automatically. Also `Ctrl+Shift+C`.
- **Paste:** right-click, `Ctrl+Shift+V` or `Ctrl+V`. If the text has **several lines**, NetTerm first shows you
  the complete configuration, with line numbers, and asks whether to paste it (like MobaXterm): each
  line runs as a command. Adjust it in Preferences → Terminal → "Ask before pasting".
- **Context menu:** `Ctrl` + right-click (or set the right-click to always open the menu, see
  Preferences → Terminal). Options: Copy, Paste, **Highlight** the word, Select all, Clear screen.
- `Ctrl+C`, `Ctrl+Z`, `Tab`, arrows… work as in any terminal.
- Right-click a **tab**: Reconnect, Open log, Clear screen, Close.

### Search and filter in the terminal

Click `🔍` or press `Ctrl+Shift+F` (if you have selected text, it searches for it directly).

- **Search:** type the word. All matches are marked in yellow and the current one in orange; the
  counter shows "3 of 27". `Enter` goes to the next, `Shift+Enter` to the previous, `Esc` closes.
- **Options:** `Aa` matches case, `ab` whole words only and `.*` uses a regular expression
  (for example `et-0/0/[0-3] +up +down` to see the interfaces that are down).
- **Filter lines:** shows **only the lines containing the word**, like a `| include`, but on what
  you already have on screen, without running the command again. Ideal for reviewing a long configuration.
  - **With the word / Without the word:** include or exclude (like `| exclude`).
  - **Context:** also shows 1, 3 or 5 lines around each match (in grey).
  - Click a line to go to it in the terminal. **Copy** copies the result; **Refresh** reads
    the terminal again if new output has arrived.

`Ctrl+F` without `Shift` is not used for searching because device CLIs use it to move the cursor.

### SFTP and FTP

SFTP/FTP sessions open a **file explorer**: your PC on the left and the device on the right, with the console below.

- **Navigate:** double-click a folder, `↑` to go up, or type the path and press `Enter`.
- **Select:** click, `Ctrl`+click, `Shift`+click or `Ctrl+A`.
- **Copy:** drag from one panel to the other, use the `→` and `←` buttons or double-click a file. Folders are copied with their
  contents. If something already exists at the destination, NetTerm asks before overwriting. Progress shows at the bottom, with **Cancel**.
- **Other actions (right-click):** new folder, rename, delete, copy path. Also `F2`, `Del`, `F5` and `Backspace`.
  Delete and rename only work on the remote device; nothing on your PC is deleted from here.
- `✕` hides the explorer and `📁` shows it again.
- For safety, downloads skip links and names that aren't valid on Windows, and NetTerm tells you how many.

If you prefer typing, the console is still there. Type `help` to see the commands:

| Command | What it does |
|---|---|
| `ls [path]` | List the remote directory |
| `cd <path>` / `pwd` | Change directory / see where you are |
| `get <remote> [local]` | Download (by default to your Downloads folder) |
| `put <local> [remote]` | Upload a file |
| `mkdir`, `rmdir`, `rm`, `mv` | Create, delete, rename |
| `lcd`, `lls`, `lpwd` | Local folder |

## 6. Custom buttons

Click **＋ Button** in the buttons bar.

Tip: a command can use **what you have selected**. Write `{sel}` in it (`show interfaces {sel} terse`) or press **Insert {sel}**.
Double-click an interface in the terminal, press the button and it is sent with that interface. It works with a single line;
with nothing selected, NetTerm warns you and sends nothing. It also works in the key editor and with multi-send.

- **Commands:** one or several lines; they are sent in order with the delay you choose (useful for
  `terminal length 0` + `show running-config`).
- **Password:** sends a saved password (for example the `enable` one) without it ever showing on screen.
- **Press Enter at the end:** check it so it runs directly.
- **Keyboard shortcut:** click the "Shortcut" field and press the combination (`Ctrl+Alt+1`, `F5`, `Ctrl+→`…).
  `Ctrl`+letter is not allowed because the terminal needs it (`Ctrl+C`, `Ctrl+D`…). Arrows, Home, End,
  PgUp, PgDn and Insert need `Ctrl` or `Alt`. `Del` removes the shortcut.
- **Color:** to tell them apart at a glance.

Right-click a button to **edit, move or delete it**. The button applies to the active tab
(or to all marked tabs if multi-send is on).

### Key editor

To assign texts to keys without creating buttons (like SecureCRT's "Keymap Editor"):
**Preferences → Keys**.

1. Choose the modifiers (`Ctrl`, `Alt`, `Shift`) and click a key on the on-screen keyboard. You can also
   click the keyboard and press the real combination.
2. Enter the text it should send, for example `show interfaces diagnostics optics et-0/0/0`. It can have
   several lines.
3. Check "Press Enter at the end" if you want it to run directly, and click **Assign**.

The on-screen keyboard is complete, with the navigation block and numeric keypad. `Del`, `Enter` and the symbol keys also
work, with `Ctrl` or `Alt`. Click `Ctrl`, `Alt` or `Shift` to turn them on. Dimmed keys (`Esc`, `Win`, `Caps Lock`…) can't be
assigned, and neither can shortcuts Windows takes for itself (`Alt+Tab`, `Alt+F4`…).

Keyboard colors: blue = assigned; green = a button's shortcut; blue stripe = assigned with other modifiers;
dimmed = used by NetTerm. Below is the list of assigned keys to edit or remove them.

## 7. Split screen

Click `▥` and choose:

| Layout | Shortcut |
|---|---|
| One terminal | `Ctrl+Shift+1` |
| Two, side by side | `Ctrl+Shift+2` |
| Two, top and bottom | `Ctrl+Shift+3` |
| Four | `Ctrl+Shift+4` |

- The selected panel has a **blue border**. Click a panel to select it.
- Click a **tab** to show it in the selected panel (or in a free slot).
- Each panel shows the session name and status at the top.

## 8. Multi-send (typing into several sessions at once)

1. Open the sessions (for example, all the switches on a floor).
2. Click `📡` (or `Ctrl+Shift+M`). An **orange bar** appears and all SSH/Telnet sessions are marked ☑.
3. Unmark the ones you don't want with the ☑ on their tab ("Mark all" / "None" in the orange bar).
4. Type in any marked session: **what you type reaches all the marked ones**. Buttons too.
5. Click **Turn off** (or `📡` again) when finished.

> ⚠ Be careful with configuration changes: they apply to all marked sessions at once.
> Combine it with the split screen to see how each device responds.

## 9. Word highlighting

Routers and switches don't send colors, so NetTerm adds them. By default:

| What | Color |
|---|---|
| `up`, `active`, `connected`, `established`… | Bold green |
| `down`, `err-disabled`, `failed`, `error`… | Bold red |
| `administratively down`, `admin-down`, `%Warning`… | Orange |
| IPv4 and IPv6 addresses | Cyan |
| MAC addresses (`0050.56c0.0001`, `aa:bb:cc:dd:ee:ff`) | Purple |
| Aggregated / trunk interfaces (`ae3`, `BE3.9`, `Port-channel10`, `Eth-Trunk0`, `BAGG1`, `lag1`, `Trk1`…) | Bold gold |
| 100G and 400G interfaces (`et-0/0/0`, `Hu0/0/0/1`, `HundredGigE…`, `100GE…`, `HGE1/0/49`) | Pink |
| 10G interfaces (`xe-0/1/4`, `TenGigE…`, `Te1/1/1`, `XGigabitEthernet…`, `XGE1/0/1`) | Turquoise |
| Other interfaces (`ge-0/0/1`, `Gi0/1`, `lo0`, `GE1/0/1`, `1/1/1`…) | Blue |

**Highlight a word on the spot:** right-click the word in the terminal (or `Ctrl`+right-click) →
**🎨 Highlight**. Choose a template or create a new one. It applies to whatever arrives from that moment on.

**Preferences → Highlighting:**

- **Style templates:** text color, background (∅ = no background), **B** bold, *I* italic, U underline.
- **Rules:** what each template applies to.
  - *Words:* exact words separated by commas (`up, active, connected`). `UP` does not color `BACKUP`.
  - *Contains:* like Words, but also inside other words: `MPLS` colors `MPLS_VPN_SLAES`.
  - *Pattern:* IPv4, IPv6, MAC or an **interface type**: trunks/aggregated, 100G-400G, 40G-25G, 10G, 1G,
    management/logical, or any interface. This way you can give each type the color you want.
  - *Regex:* regular expression (for example `VLAN\d+`). If it is badly written, the field turns red.
  - `Aa` = ignore case. `▲▼` = priority: if two rules match, the one on top wins.
- **Restore** goes back to the default rules.

## 10. Preferences (`⚙` or `Ctrl+,`)

Changes are saved automatically. The **🌐 language** (Español, English) is chosen at the top of this window.

- **Terminal:** 13 themes, font and size, line height, weight, cursor, custom colors,
  on-screen history, right-click behavior, paste warning, keepalive, automatic reconnection and **ask before closing NetTerm**
  (by default, if there are open sessions; so it doesn't close by accident). If the open session has its own
  theme, you choose whether the theme applies to "All sessions" or "This session only".
- **Layout:** buttons top, bottom, left or right; style and size; sessions panel left,
  right or hidden; list, compact or cards.
- **Logs:** turn on or off and choose the folder.
- **Highlighting:** see section 9.
- **Keys:** key editor (section 6).
- **Updates:** check for updates when opening and "Check for updates now".

### On-screen history

How many lines you can scroll back with the mouse wheel: from 1,000 to 1,000,000. Each line uses memory
(with 1,000,000 lines, up to ~1.5 GB **per tab**). To keep **everything without limit**, use the logs.

## 11. Session logs

With logs on (the default), each connection is saved to a text file with the **date and time on
every line**, for example `raspi_2026-10-23_18-30-00.log`.

- Default folder: `Documents\NetTerm Logs` (change it in Preferences → Logs).
- Open a session's log: right-click its tab → **Open log**.

## 12. Import and export

`⋯` button next to "New session".

### Import sessions from other programs

- **PuTTY** and **SecureCRT:** reads the sessions saved on this PC (SecureCRT folders become groups).
  These programs do not allow reading their passwords: NetTerm will ask for them when connecting.
- **Excel or CSV:** a file with a header row. Recognized columns: **Name, Host (or IP),
  Port, Protocol, User, Password, Group**. Only the host is required. "Download Excel/CSV template"
  gives you an example.

You will see a list to choose which ones to import. Those you already have appear as "already exists" and are not duplicated.

### Share your configuration with the team

- **Export configuration:** creates a `.netterm` file with sessions, buttons and/or preferences.
  Passwords and the key editor are **not included**, or go **encrypted with a password** you choose.
- **Import configuration:** opens a `.netterm` file. If it has encrypted passwords, enter the file password.
  What you already have is not duplicated. Imported preferences replace yours (only if you mark it).

## 13. Updates

When opening, NetTerm checks for a new version. If there is one, you will see what's new and can choose:

- **Update now:** it downloads, closes, replaces itself and reopens. Your data is kept.
- **Later** or **Skip this version**.

Nothing is ever installed without your approval.

## 14. Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+Shift+N` | New session |
| `Ctrl+Shift+W` | Close tab |
| `Ctrl+Tab` / `Ctrl+Shift+Tab` | Next / previous tab |
| `Ctrl+B` | Show or hide the sessions panel |
| `Ctrl+,` | Preferences |
| `F1` | This manual |
| `Ctrl+Shift+F` | Search and filter in the terminal |
| `Ctrl+Shift+1` … `4` | Split screen |
| `Ctrl+Shift+M` | Multi-send |
| `Ctrl+Shift+C` / `Ctrl+Shift+V` | Copy / paste |
| The ones you assign | Your buttons and the key editor |

## 15. Your data and security

- Sessions, passwords and buttons are saved **encrypted** in `%USERPROFILE%\.netterm`, protected with your
  Windows user: another account or another PC cannot read them.
- Preferences are in `%USERPROFILE%\.netterm\settings.json`. Key editor texts are encrypted.
- **SSH and SFTP check the device:** its key is saved the first time (`known_hosts`, same folder). If it changes later,
  NetTerm stops **without sending the password** and shows both fingerprints. If you know why it changed (device replaced
  or reinstalled), type `accept` and press `Enter`. If you don't, report it before accepting.
- **Telnet and FTP are not encrypted:** the password and what you type travel in clear text. Use SSH or SFTP whenever you can.
- **Logs are not encrypted.** Keep them in a safe folder.
- **Only import `.netterm` files from people you trust:** their buttons and keys send commands to your devices.
- NetTerm does not send your data to any server. It only connects to your devices and, to check for updates,
  to GitHub.

## 16. Common problems

| Problem | Solution |
|---|---|
| "Windows protected your PC" | More info → Run anyway |
| "Incorrect user or password" | Type the password in the terminal and save it if it works. Check the keyboard layout used when creating the password on the device (`@` versus `2`) |
| "The server closed the connection" | Temporary block due to failed attempts: wait a few minutes |
| "The SSH key has changed" | The password was not sent. If the device was replaced or reinstalled, type `accept` and press `Enter`. If not, don't accept and report it |
| "Connection refused" | The port is not open or the service (SSH/Telnet) is not active on the device |
| "Timed out" | The device is not responding: check the IP, the VPN or the firewall |
| I can't see the sessions panel | Click `☰` or press `Ctrl+B` |
| Words are not colored | Preferences → Highlighting: check that it is on. It only affects what arrives afterwards |
| A button does nothing | The session must be connected (green dot). Passwords are only sent to SSH/Telnet |
| The device cuts commands with `...` or misplaces lines | Since version 1.4 NetTerm tells the device the real window width (SSH and Telnet). If it happens with an older version, update |
