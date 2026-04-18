# Tab Out

**Keep tabs on your tabs.**

Tab Out replaces your Chrome new tab page with a dashboard that integrates with Chrome's native tab groups. Organize your tabs, drag-and-drop to group/ungroup, and keep your browser clean.

Built for people who want better tab organization without the complexity.

> **Note:** This is a fork of [zarazhangrui/tab-out](https://github.com/zarazhangrui/tab-out) with a focus on Chrome tab groups integration instead of domain-based grouping.

---

## What's Different in This Fork

This version has been redesigned around Chrome's native tab groups:

**Added:**
- Full Chrome tab groups integration (create, rename, color, collapse)
- Drag-and-drop to move tabs into groups
- Drag-to-ungroup (drag grouped tabs back to ungrouped)
- Simplified group creation (just enter name, auto-selects color, uses 1 most recent tab)
- Groups default to expanded
- Two-column layout (Tab Groups | Ungrouped Tabs)

**Removed:**
- Domain-based grouping
- Landing pages group
- Swoosh sound and confetti animations
- Duplicate detection
- Update notifications

If you want the original version with domain grouping and confetti, see [Zara's original repo](https://github.com/zarazhangrui/tab-out).

---

## Features

- **Chrome tab groups integration** - Uses Chrome's native tab groups, syncs both ways
- **Simple group creation** - Just type a group name, color auto-rotates, adds 1 most recent tab
- **Drag-and-drop grouping** - Drag ungrouped tabs into any group
- **Drag-to-ungroup** - Drag tabs from groups back to ungrouped section
- **Visual feedback** - Blue highlight when grouping, orange when ungrouping
- **Click to focus** - Click any tab to switch to it, even across windows
- **Save for later** - Bookmark tabs to a checklist before closing
- **100% local** - Your browsing data never leaves your machine
- **Always on** - Starts automatically when you log in

---

## Install with a coding agent

Send your coding agent (Claude Code, Cursor, Windsurf, etc.) this repo and say **"install this"**:

```
https://github.com/taimur-abbas/tab-out
```

The agent will explain what Tab Out does and set everything up. Takes about 2 minutes.

---

## Manual Setup

If you prefer to set things up yourself:

**1. Clone and install**

```bash
git clone https://github.com/taimur-abbas/tab-out.git
cd tab-out
npm install
```

**2. Run the setup script**

```bash
npm run install-service
```

This creates `~/.mission-control/`, writes a default config, and installs an auto-start service for your platform (macOS Launch Agent, Linux systemd, or Windows Startup script).

**3. Load the Chrome extension**

1. Go to `chrome://extensions` in Chrome
2. Enable **Developer mode** (top-right toggle)
3. Click **Load unpacked**
4. Select the `extension/` folder from this repo

**4. Start the server**

```bash
npm start
```

Open a new tab - you'll see Tab Out. The server auto-starts on future logins.

---

## How to Use

**Create a new group:**
1. Click "➕ Create Group" at the bottom of Tab Groups section
2. Enter a group name (color auto-selects, adds 1 most recent tab)
3. Drag more tabs into the group as needed

**Organize tabs:**
- Drag ungrouped tabs into any group (blue highlight)
- Drag grouped tabs to ungrouped section (orange highlight)
- Click tab titles to switch to that tab
- Use "Ungroup All" to remove all tabs from a group

**Save for later:**
- Click the bookmark icon on any tab
- Saved tabs appear in "Saved for later" section
- Check them off as you complete them

---

## Configuration

Config lives at `~/.mission-control/config.json`:

| Field | Default | What it does |
|-------|---------|-------------|
| `port` | `3456` | Local port for the dashboard |

---

## How it works

```
You open a new tab
  -> Chrome extension loads Tab Out in an iframe
  -> Dashboard shows your Chrome tab groups + ungrouped tabs
  -> You organize tabs by dragging them into groups
  -> Chrome's native tab groups stay in sync
  -> Repeat
```

The server runs silently in the background. It starts on login and restarts if it crashes.

---

## Tech stack

| What | How |
|------|-----|
| Server | Node.js + Express |
| Database | better-sqlite3 (local SQLite) |
| Extension | Chrome Manifest V3 with Tab Groups API |
| Auto-start | macOS Launch Agent / Linux systemd / Windows Startup |
| UI | Vanilla JS + CSS (no framework) |

---

## Credits

Original project by [Zara Zhang](https://x.com/zarazhangrui) - [zarazhangrui/tab-out](https://github.com/zarazhangrui/tab-out)

This fork maintains the core architecture while focusing on Chrome tab groups integration.

---

## License

MIT
