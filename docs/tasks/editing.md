---
title: "Editing"
description: "Comments, surround, auto-pairs, text objects, macros, registers, and more"
category: "tasks"
related:
  - README.md
  - code-intelligence.md
---

# Editing

## Comments

Toggle comments with the `gc` operator:

| Key | Mode | Action |
|-----|------|--------|
| `gcc` | Normal | Toggle line comment |
| `gbc` | Normal | Toggle block comment |
| `gc{motion}` | Normal | Comment with motion |
| `gc` | Visual | Comment selection |
| `gb` | Visual | Block comment selection |

### Examples

```
gcc          " Comment current line
gc3j         " Comment 3 lines down
gcip         " Comment inner paragraph
```

Visual mode: Select lines, then press `gc`.

Comments are language-aware (JSX, HTML with scripts, Vue/Svelte).

## Surround

Add, change, or delete surrounding characters:

### Add Surroundings

| Key | Action |
|-----|--------|
| `ys{motion}{char}` | Add surrounding |
| `yss{char}` | Surround entire line |
| `S{char}` | Surround selection (visual) |

**Examples:**

```
ysiw"    " Surround word with quotes:  hello → "hello"
ysiw)    " Surround with parens:       hello → (hello)
ys$"     " Surround to end of line
```

### Change Surroundings

| Key | Action |
|-----|--------|
| `cs{old}{new}` | Change surrounding |

**Examples:**

```
cs"'     " Change quotes:    "hello" → 'hello'
cs)]     " Change brackets:  (hello) → [hello]
```

### Delete Surroundings

| Key | Action |
|-----|--------|
| `ds{char}` | Delete surrounding |

**Examples:**

```
ds"      " Delete quotes:  "hello" → hello
ds)      " Delete parens:  (hello) → hello
```

## Text Objects (mini.ai)

Extended text objects for working with code structures:

### Available Text Objects

| Key | Description |
|-----|-------------|
| `f` | Function |
| `c` | Class |
| `a` | Argument/parameter |
| `o` | Block/conditional/loop |

### Usage with Operators

Combine with `d` (delete), `c` (change), `y` (yank), `v` (visual):

| Key | Action |
|-----|--------|
| `daf` | Delete around function |
| `cif` | Change inside function |
| `yac` | Yank around class |
| `vic` | Select inside class |
| `daa` | Delete around argument |
| `cia` | Change inside argument |
| `dao` | Delete around block/loop |

### Examples

```
daf          " Delete entire function including signature
cif          " Change function body, keep signature
yaa          " Yank argument including comma
cia          " Change just the argument value
vaf          " Select entire function
```

Text objects are treesitter-aware and work across all configured languages.

## Auto Pairs

Brackets and quotes close automatically:

| You type | Result |
|----------|--------|
| `(` | `()` with cursor inside |
| `{` | `{}` with cursor inside |
| `[` | `[]` with cursor inside |
| `"` | `""` with cursor inside |
| `'` | `''` with cursor inside |

**Smart features:**
- Typing `)` when on `)` moves cursor right
- `Alt+e` wraps next word in pairs

## Text Selection

Treesitter incremental selection:

| Key | Mode | Action |
|-----|------|--------|
| `Ctrl+Space` | Normal | Start selection |
| `Ctrl+Space` | Visual | Expand selection |
| `Backspace` | Visual | Shrink selection |

Expands to increasingly larger syntax nodes (word → expression → statement → block → function).

## Visual Mode Operations

| Key | Mode | Action |
|-----|------|--------|
| `<` | Visual | Indent left (stay in visual) |
| `>` | Visual | Indent right (stay in visual) |
| `J` | Visual | Move selection down |
| `K` | Visual | Move selection up |

## Completion

Autocompletion appears as you type:

| Key | Mode | Action |
|-----|------|--------|
| `Ctrl+Space` | Insert | Trigger completion manually |
| `Tab` | Insert | Next item / expand snippet |
| `Shift+Tab` | Insert | Previous item |
| `Enter` | Insert | Confirm selection |
| `Ctrl+e` | Insert | Abort completion |
| `Ctrl+b` | Insert | Scroll docs up |
| `Ctrl+f` | Insert | Scroll docs down |

### Completion Sources

1. LSP (highest priority)
2. Snippets
3. Buffer words
4. File paths

See [plugins/completion.md](../plugins/completion.md) for configuration.

## Macros

Record and replay sequences of keystrokes:

### Recording

| Key | Action |
|-----|--------|
| `qa` | Start recording to register `a` |
| `q` | Stop recording (while recording) |
| `@a` | Play macro from register `a` |
| `@@` | Replay last macro |
| `5@a` | Play macro 5 times |

### Examples

```
qa           " Start recording to register 'a'
0f"ci"NEW    " Go to start, find quote, change inside
q            " Stop recording
j@a          " Move down, replay macro
10@@         " Replay 10 more times
```

### Editing Macros

Macros are stored in registers. To edit:

```
"ap          " Paste register 'a' contents
             " Edit the text
"ay$         " Yank back to register 'a'
```

## Registers

Vim has multiple registers for storing text:

### Named Registers

| Register | Description |
|----------|-------------|
| `"a` - `"z` | Named registers (you control) |
| `"A` - `"Z` | Append to named register |
| `""` | Unnamed (default) register |
| `"0` | Last yank |
| `"1` - `"9` | Delete history (most recent first) |

### Special Registers

| Register | Description |
|----------|-------------|
| `"+` | System clipboard |
| `"*` | Selection clipboard (X11) |
| `"_` | Black hole (discard) |
| `"/` | Last search pattern |
| `".` | Last inserted text |
| `":` | Last command |
| `"=` | Expression register |

### Usage

| Key | Action |
|-----|--------|
| `"ay` | Yank to register `a` |
| `"ap` | Paste from register `a` |
| `"+y` | Yank to system clipboard |
| `"+p` | Paste from system clipboard |
| `"_d` | Delete without saving |
| `:reg` | View all registers |
| `:reg a` | View register `a` |

### Examples

```
"ayiw        " Yank word to register 'a'
"Ayy         " Append line to register 'a'
"+yy         " Yank line to system clipboard
"0p          " Paste last yank (ignores deletes)
"_dd         " Delete line, don't save anywhere
```

## Marks

Set bookmarks in your code:

### Setting Marks

| Key | Action |
|-----|--------|
| `ma` | Set local mark `a` |
| `mA` | Set global mark `A` (works across files) |

### Jumping to Marks

| Key | Action |
|-----|--------|
| `` `a `` | Jump to mark `a` (exact position) |
| `'a` | Jump to mark `a` (line start) |
| `` `A `` | Jump to global mark `A` |
| `:marks` | List all marks |
| `:delmarks a` | Delete mark `a` |
| `:delmarks!` | Delete all lowercase marks |

### Special Marks

| Mark | Description |
|------|-------------|
| `` `. `` | Last change position |
| `` `" `` | Position when last exited file |
| `` `^ `` | Last insert position |
| `` `[ `` | Start of last yank/change |
| `` `] `` | End of last yank/change |
| `` `< `` | Start of last visual selection |
| `` `> `` | End of last visual selection |
| `''` | Previous position (before jump) |

### Examples

```
ma           " Set mark 'a' here
...edit...
`a           " Jump back to exact position
'a           " Jump to start of marked line
`.           " Jump to last edit
''           " Jump back to where you were
```

## Dot Repeat

The `.` command repeats the last change:

| Key | Action |
|-----|--------|
| `.` | Repeat last change |
| `u` | Undo last change |
| `Ctrl+r` | Redo |

### What Counts as a Change

- Insert mode session (from `i` to `Esc`)
- Delete/change commands (`d`, `c`, `x`, etc.)
- Put commands (`p`, `P`)
- Replace (`r`, `R`)

### Examples

```
ciw"hello"<Esc>   " Change word to "hello"
w.                " Move to next word, repeat change
.                 " Repeat again

dd                " Delete line
j.                " Move down, delete another line

A;<Esc>           " Append semicolon
j.                " Next line, append semicolon
```

### Pro Tips

- Design changes to be repeatable
- Use `ciw` instead of `bcw` (more repeatable)
- Combine with `/` search: `n.n.n.` to repeat across matches

## Undo and Redo

| Key | Action |
|-----|--------|
| `u` | Undo |
| `Ctrl+r` | Redo |
| `U` | Undo all changes on line |

### Undo Branches

Vim maintains an undo tree, not just linear history:

| Key | Action |
|-----|--------|
| `g-` | Go to older text state |
| `g+` | Go to newer text state |
| `:earlier 5m` | State from 5 minutes ago |
| `:later 2m` | State from 2 minutes later |
| `:undolist` | Show undo branches |

### Examples

```
:earlier 10        " Go back 10 changes
:earlier 5m        " Go back 5 minutes
:later 30s         " Go forward 30 seconds
g-                 " Previous state (follows branches)
```

## Related

- [Code Intelligence](code-intelligence.md) - LSP features, formatting
- [Searching](searching.md) - Find and replace
