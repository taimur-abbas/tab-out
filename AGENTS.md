# AGENTS.md - Tab Out: Setup & Onboarding Guide for Coding Agents

You're installing **Tab Out** for the user. Your job is not just to set it up - it's to get them excited about using it. Explain what it does, why it's useful, and walk them through the experience.

---

## Step 0 - Introduce the product

Before doing anything technical, tell the user what they're about to get. Say something like:

> **Tab Out** replaces your new tab page with a clean dashboard that integrates with Chrome's native tab groups. It gives you a two-column view: your tab groups on the left, ungrouped tabs on the right.
>
> Here's what makes it great:
> - **Chrome tab groups integration** - Uses Chrome's native groups, syncs both ways
> - **Simple group creation** - Just type a name, color auto-rotates, adds 1 most recent tab
> - **Drag-and-drop organization** - Drag ungrouped tabs into groups, or drag grouped tabs back out
> - **Visual feedback** - Blue highlight when grouping, orange when ungrouping
> - **Click any tab to jump to it** - Even across different Chrome windows
> - **Save for later** - Bookmark individual tabs to a checklist before closing them
> - **100% local** - Your browsing data never leaves your machine
> - **Always on** - Starts automatically when you log in, runs silently in the background
>
> Let's set it up - takes about 2 minutes.

---

## Step 1 - Clone and install

```bash
git clone https://github.com/taimur-abbas/tab-out.git
cd tab-out
npm install
```

---

## Step 2 - Write the config

Create `~/.mission-control/config.json`:

```json
{
  "port": 3456
}
```

---

## Step 3 - Run the setup script

```bash
npm run install-service
```

This creates data/logs directories and installs a platform-specific auto-start service (macOS Launch Agent, Linux systemd, or Windows Startup script).

---

## Step 4 - Install the Chrome extension

This is the one step that requires manual action from the user. Make it as easy as possible:

**First**, tell the user the full path they'll need. Print it clearly:
```bash
echo "Extension folder: $(cd extension && pwd)"
```

**Then**, copy the path to their clipboard so they can paste it in the file picker:
- macOS: `cd extension && pwd | pbcopy && echo "Path copied to clipboard"`
- Linux: `cd extension && pwd | xclip -selection clipboard 2>/dev/null || pwd | xsel --clipboard 2>/dev/null || echo "Path: $(pwd)"`
- Windows: `cd extension && echo %CD% | clip`

**Then**, open the extensions page:
```bash
open "chrome://extensions"
```

**Then**, walk the user through it step by step. Say something like:

> I've copied the extension folder path to your clipboard. Now:
>
> 1. You should see Chrome's extensions page. In the **top-right corner**, toggle on **Developer mode** (it's a switch).
> 2. Once Developer mode is on, you'll see a button called **"Load unpacked"** appear in the top-left. Click it.
> 3. A file picker will open. **Press Cmd+Shift+G** (Mac) or **Ctrl+L** (Windows/Linux) to open the "Go to folder" bar, then **paste** the path I copied (Cmd+V / Ctrl+V) and press Enter.
> 4. Click **"Select"** or **"Open"** - the extension will install immediately.
>
> You should see "Tab Out" appear in your extensions list.

**Also**, open Finder/Explorer directly to the extension folder as a fallback:
- macOS: `open extension/`
- Linux: `xdg-open extension/`
- Windows: `explorer extension\\`

This way the user can also just drag or navigate to it visually if the clipboard approach doesn't work.

---

## Step 5 - Start, verify, and show them around

```bash
npm start &
sleep 2
open http://localhost:3456
```

Once the dashboard loads, walk them through the experience:

> You're all set! Here's how to use Tab Out:
>
> **Creating groups:**
> 1. Click "➕ Create Group" at the bottom of the Tab Groups column
> 2. Enter a group name (color auto-selects, adds 1 most recent tab)
> 3. The group appears in the left column
>
> **Organizing tabs:**
> 1. Drag any ungrouped tab (right column) into a group - you'll see a blue highlight
> 2. Drag a grouped tab back to the ungrouped section - you'll see an orange highlight
> 3. Click "Ungroup All" to remove all tabs from a group
>
> **Other actions:**
> 1. Click any tab title to jump directly to that tab (no new tab opened)
> 2. Save individual tabs for later by clicking the bookmark icon
> 3. Rename groups by clicking the "✏️ Rename" button
>
> The server runs automatically in the background - you never need to start it again. Every new tab is now your dashboard.

---

## Key Facts

- Config: `~/.mission-control/config.json`
- Logs: `~/.mission-control/logs/`
- Default port: `3456`
- Auto-starts on login (macOS Launch Agent / Linux systemd / Windows Startup)
- 100% local - no data is sent to any external service
- Uses Chrome Tab Groups API for native integration
