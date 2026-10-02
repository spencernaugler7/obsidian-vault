---
source: https://github.com/MinottiAlessandro/Emerald
---
Welcome to **Emerald** — a tiny, fast, Obsidian-style note app. This note shows everything the editor can do; edit or delete it freely.

Emerald is a *live* Markdown editor — there is no separate preview pane. The markup on the line your cursor sits on stays visible so you can edit it, and melts into formatted text on every other line. A selection reveals the exact source of every line it crosses, then renders those lines again when the selection leaves.

## Text formatting
- **bold** — wrap text in `**double asterisks**`
- *italic* — wrap text in `*single asterisks*` or `_underscores_`
- ***bold italic*** — combine them: `***three asterisks***`
- ~~strikethrough~~ — wrap text in `~~tildes~~`
- ==highlight== — wrap text in `==double equals==`
- `inline code` — wrap text in single backticks

These styles stack: nest them to layer more on, e.g. `==dog ~~cat *horse **elephant***~~==` highlights everything, strikes “cat horse elephant”, italicises “horse elephant”, and bolds “elephant”.

## Headings
Start a line with one to six `#` marks; the more marks, the smaller the heading. Hover the left margin beside a heading and click the ▾ arrow to fold its whole section away — click the ▸ to unfold it.

### This is a third-level heading

## Lists
- bullets start with `-`, `*` or `+`
  - press Tab to indent, Shift+Tab to outdent
    - click a parent item's arrow to fold or unfold its children
    - the bullet glyph changes with the nesting depth
- Enter keeps the list going; Enter on an empty item ends it

1. ordered lists start with `1.` or `1)`
2. the next number is filled in for you on Enter

## Tasks
- [ ] an open task — type `- [ ] ` before the text
- [x] a finished task — `- [x] ` (the text is struck through)

Click a checkbox on any line other than the one you're editing to toggle it.

## Quotes
> Blockquotes start with `>`.
> Enter keeps quoting; Enter on an empty quote line stops.

Start a quote with `> [!tip]` to create an Obsidian-style callout. The whole quote becomes a continuous colored card and the marker becomes a type-specific emoji plus **Tip** when you leave the line; put text after it for a custom title, for example `> [!warning] Read this first`. Built-in types (each with its own emoji) are `note`, `abstract`, `summary`, `tldr`, `info`, `todo`, `tip`, `hint`, `important`, `success`, `check`, `done`, `question`, `help`, `faq`, `warning`, `caution`, `attention`, `failure`, `fail`, `missing`, `danger`, `error`, `bug`, `example`, `quote`, and `cite`; other names use a generic callout style.

## Code blocks
Fence a block between lines of three backticks (or three tildes) and add a language name for a labelled header bar — click the copy icon on the right of that bar to copy the whole block:

```cpp
int answer = 42;  // the header bar shows the language
return answer;
```

Move the caret into a code block to reveal both fences. Code stays verbatim inside, and the arrow beside its opening fence folds or unfolds the complete block. Typing the third opening backtick adds the closing fence automatically.

## Math
Write inline math between single dollar signs, such as `$x^2 + y^2$`, or display math between `$$` markers; display expressions may span several lines. Emerald's built-in renderer supports fractions and roots (`\frac`, `\sqrt`), super/subscripts, sums and integrals, accents, growing delimiters, text, matrices, Greek letters, operators, relations, and arrows. Bare currency dollars and math inside inline code stay literal.

## Images
Press **Ctrl+Shift+I**, choose **Insert Image…** from the gear or editor context menu, paste an image, or drop image files into a note. Files from outside the vault are copied into `_attachments`; files already inside it are linked in place. A standalone `![Alt](path)` line shows a responsive preview in both modes, reveals its compact Markdown when you edit the line, and shows a small fallback card if the local image is unavailable.

## Tables
Type a pipe table and Emerald lines the columns up as you go — on every Tab and when you click away. Colons in the separator row set the alignment — `:--` left, `:-:` centre, `--:` right.

Press **Enter** anywhere on a header row (the first line, before there's a `---` separator) and Emerald adds the separator and a first data row for you, dropping the caret in its first cell. Enter from an existing header or separator does the same and lines up the table when it fits.

Press **Tab** inside a table to jump to the next cell (**Shift+Tab** goes back). Tab on the last header cell adds a column; on the separator row it starts a new data row; on the last cell of the last row it adds a row — so you can build a whole table without leaving the keyboard. In body rows, **Enter** moves to the same cell below, adding that row at the bottom when needed. Tables stay as plain Markdown in Edit Mode.

| Mascot          |     Shortcut |
| :-------------- | -----------: |
| Open gallery    |       Ctrl+G |
| Generate mascot |       Ctrl+M |
| Delete mascot   | Ctrl+Shift+M |

## Templates
Pick a **Templates folder** inside your vault under **Settings**, then press **Ctrl+T** (or **Insert Template…** in the gear menu) to choose a template — every note under that folder, sub-folders included, is offered in a quick picker like *Go to note*. The template's text is dropped in at your cursor.

Templates can carry placeholders that fill themselves in on insert:

- `{{title}}` — the current note's title
- `{{date}}` — today's date (default `YYYY-MM-DD`)
- `{{time}}` — the current time (default `HH:mm`)

Give `{{date}}` or `{{time}}` a format after a colon to change it, e.g. `{{date:YYYY/MM/DD}}` or `{{time:HH:mm:ss}}`.

## Mascots
A note can have a small procedurally drawn mascot in its bottom-right corner. Press **Ctrl+M** to generate or re-roll one, **Ctrl+Shift+M** to remove it, or **Ctrl+G** (or click a mascot) to open the vault gallery. Settings can generate one automatically after a chosen character count; deleting it suppresses automatic generation for that note until you generate one manually.

The reproducible seed is a hidden first-line HTML comment, so it travels with the Markdown file without separate vault metadata. Press Up at the start of the body to reveal and edit it. Emerald also discovers custom layered SVG creatures under `mascots/creatures/<name>` in its standard app-data folder. Put PNG/JPG/WEBP files in `mascots/images` and enable **Use Image Mascots** in the gear menu to use deterministic image tiles instead.

## Horizontal rule
Three or more dashes on a line of their own draw a divider:

---

## Editing shortcuts
Handy keys while writing (on macOS, Ctrl is ⌘):

- **Ctrl+B** / **Ctrl+I** — bold / italic the selection
- **Ctrl+K** — wrap the selection as a link `[text](…)`
- **Ctrl+1** … **Ctrl+6** — set the line's heading level (press the same level again to clear it)
- **Ctrl+L** — select the whole line
- **Alt+↑** / **Alt+↓** — move the line (or selection) up / down
- **Tab** / **Shift+Tab** — indent / outdent the selected lines (or the current list item)
- **Ctrl+Enter** — start a new line below without splitting the current one (keeps continuing a list)
- Select text, then press **(** **[** **\*** **_** **=** **'** **"** **`**, **~**, or **$** to wrap the selection in it (brackets close with their match)

## Linking notes
Type `[[` to autocomplete a link to another note. `[[Emerald Manual]]` jumps to a note — click it once rendered, or Ctrl+click while editing — and a note that doesn't exist yet is created on the spot. Use `[[Note|label]]` to show a different label. Renaming a note's title rewrites every link that points to it; new link targets honor the vault's **New notes in** folder. Standard `[label](https://…)` links open in the system browser. Hold **Alt** briefly to label the links currently on screen, then type a hint to open one without the mouse (X is reserved for the shortcuts panel). **Ctrl+Shift+B** opens Broken Links, a filterable report of links whose target is missing or empty.

## Graph View
Press **Ctrl+Shift+G** (or **Settings → Vault → Graph view → Open global**) to replace this note with a map of every wiki-linked note in the vault. **Open local** starts from the current note. Both open in the same workspace, never another window. Drag empty space to pan, use the wheel to zoom, drag nodes, click one to inspect it, and double-click or press Enter to open it. **F** fits the graph, **0** resets its camera, and **/** or **Ctrl+F** focuses title search.

Filter the global view by folder and orphan or missing status, and optionally show direction arrows. Local mode can follow both, incoming-only, or outgoing-only links at depth 1–3. Note/link totals stay at the bottom-right. Back and Forward remember the graph's camera, search, filters, and selection alongside normal notes.

## Read Mode
Press **Ctrl+E** (or use **Settings → Vault → Read mode**) when you only want to read. Emerald removes the caret, fully renders every line, and prevents changes to the vault. Select text and press **Ctrl+Shift+H** to add or remove a saved `==highlight==`: if any of the selection is not highlighted Emerald fills the gaps, otherwise it removes the selected highlight. The plain **↑** and **↓** keys scroll the page; links, search, folding and selection/copy keep working, while checkboxes and saved highlights are the deliberate editable exceptions. Switching between Read and Edit Mode keeps the same source line at the same viewport position—even on long wrapped lists—so repeated toggles do not drift. Read Mode is remembered separately for each vault.

Ordinary mouse-wheel steps ease smoothly between pixel positions; high-resolution trackpad movement stays native and direct.

## Getting around
- **Title** — the first line above the body is the file name (without `.md`); edit it to rename the note.
- **Sidebar** — notes live in a folder tree. Right-click to create or delete notes and folders, drag to move them, Shift/Ctrl-click to select several at once, and single-click a folder to fold it. Collapse the whole sidebar with **Ctrl+\** (or click the divider) and again to bring it back.
- **Narrow windows** — at compact widths, Notes and the editor become separate full-width views. Use the Notes / Editor controls to switch; new-note, vault-search and gear controls remain in the editor bar.
- **History** — the back / forward arrows (Alt+Left / Alt+Right or the mouse side buttons) walk back and forward through the notes you've opened.
- **Find in note** — Ctrl+F opens a find bar; Enter and Shift+Enter step through the matches.
- **Search vault** — Ctrl+Shift+F searches the text of every note; Ctrl+P jumps to a note by title.

Emerald watches the vault for files changed, created, renamed, or deleted by other programs and refreshes the tree and search index. If an open note has unsaved local changes, Emerald keeps them and warns instead of silently overwriting them.

## Settings
Open the gear in the bottom-left for **Settings**: the editor font, its size and width, the line spacing between rows, local spell checking, the folder new notes are created in, a Home note to open at launch, a Templates folder, Read Mode, Broken Links, Graph View, and automatic mascot controls. Vault choices are stored separately for each vault without adding metadata files to it. The same menu has **New Vault…** to start a fresh vault, **Delete Note** to remove the open one (it asks first), and **Check for Updates…** to fetch and install the latest release. **Switch Vault…** jumps between vaults in the same folder, and **Insert Template…** drops in a template — both live in the menu. Edits save themselves a moment after you stop typing — Ctrl+S forces a save.

### Spelling
US English is included and works offline. Misspelled prose is underlined after the caret leaves the word; code, math, URLs, HTML, images, and wiki-link targets are ignored. Right-click an underlined word for suggestions, **Add to personal dictionary**, or **Ignore for this session**. Under **Settings → Spelling**, **Manage…** can download verified Italian, German, French, and Spanish dictionaries from versioned Emerald releases. Packs whose verified content changed are shown as **Update available**. Language packs and personal words are stored in Emerald's application-data folder, never in the vault.

## Other shortcuts
More keys to control the app workflow (on macOS, Ctrl is ⌘):
- **Ctrl+O** — Open a Vault
- **Ctrl+Shift+O** — Quick-switch to another vault in the same folder
- **Ctrl+N** — Create a new file
- **Ctrl+T** — Insert a template at the cursor
- **Ctrl+Shift+I** — Insert one or more image attachments
- **F2** — Rename the current note
- **Ctrl+Shift+Backspace** — Delete the current note (asks first)
- **Ctrl+S** — Save the current file (Emerald has auto-save)
- **Ctrl+F** — Find text in the current note
- **Ctrl+Shift+F** — Perform a Vault search
- **Ctrl+Shift+B** — Review broken links
- **Ctrl+Shift+G** — Open Graph View
- **Ctrl+E** — Toggle Read Mode for this vault
- **Ctrl+Shift+H** — Highlight or unhighlight selected Read Mode text
- **Ctrl+P** — Open the file picker
- **Ctrl+,** — Open Settings
- **Ctrl+Q** — Close Emerald
- **Ctrl++** / **Ctrl+-** — Increase / decrease the font size (**Ctrl+0** resets it)
- **Ctrl+\** — Toggle the sidebar (collapse / reopen the left pane)
- **Ctrl+G** — Open the mascot gallery (every note's creature at a glance)
- **Ctrl+M** — Generate (or re-roll) this note's mascot
- **Ctrl+Shift+M** — Delete this note's mascot
- Hold **Alt+X** — Show the keyboard shortcut cheatsheet; release either key to close it
- **Alt+←** — Back in the history
- **Alt+→** — Next in the history
