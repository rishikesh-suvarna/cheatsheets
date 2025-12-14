# Vim Motions & Essentials (Developer Starter) — VSCode Vim

A compact reference of **essential Vim motions + core edits** with tiny examples.
Designed for **VSCode + Vim extension** users.

---

## Modes

- `Esc` / `Ctrl-[` → **Normal** (move/operate)
- `i` → insert **before** cursor
- `a` → insert **after** cursor
- `o` / `O` (Capital O) → open new line **below / above**
- `v` / `V` / `Ctrl-v` → Visual / Visual line / Visual block

---

## The core formula

**operator + motion/text-object**

Operators:
- `d` delete
- `c` change (delete + insert)
- `y` yank (copy)
- `>` indent, `<` outdent

Example:
- `dw` → delete word
- `dw` → delete word
- `ci"` → change inside quotes
- `yip` → copy paragraph (lines between blank lines)

---

## Basic movement

### Character
- `h j k l` → left/down/up/right

Example:
- `10j` → move down 10 lines

### Words
- `w` → next word start
- `b` → previous word start
- `e` → word end

Example:
- On `const myValue = 123;`
  - `w` hops `const → myValue → = → 123`

### Line
- `0` → start of line (column 0)
- `^` → first non-whitespace
- `$` → end of line

Example:
- In `    return value;`
  - `^` jumps to `r` in `return` (Ignores leading spaces)

### File
- `gg` → top of file
- `G` → bottom of file
- `:{number}` → go to line number

Example:
- `:42` → go to line 42

---

## Scrolling & keeping context

- `Ctrl-d` / `Ctrl-u` → half-page down/up
- `Ctrl-f` / `Ctrl-b` → page down/up
- `zz` → center cursor line
- `zt` / `zb` → cursor line to top/bottom

Example:
- `zz` after jumping keeps the focus centered.

---

## Find within a line (great mouse replacement)

- `f{char}` → find next `{char}` on line
- `F{char}` → find previous `{char}`
- `t{char}` → **to** just before `{char}`
- `T{char}` → backwards **to**
- `;` repeat last `f/F/t/T`
- `,` repeat in opposite direction

Example:
- On: `foo(bar, baz, qux)`
  - `fb` → jump to `b` in `bar`
  - `t,` → jump to just before `,`

---

## Search (like Ctrl+F but faster)

- `/{pattern}` → search forward
- `?{pattern}` → search backward
- `n` / `N` → next / previous match
- `*` / `#` → search word under cursor forward/back

Example:
- `/normalizeEmail` then `n` to hop through calls.

Tip (Vim word boundaries):
- Whole word search: `/\<users\>`
- Whole word substitute: `:%s/\<users\>/people/g`

---

## Text objects (the biggest productivity boost)

Use with `d/c/y`.

- `iw` / `aw` → inner/a word
- `i"` / `a"` → inside/around `"..."` (also works with `'` and `` ` ``)
- `i(` / `a(` → inside/around parentheses (also `{}`, `[]`, `<>`)
- `ip` / `ap` → inner/a paragraph

Examples:
- `ci"` on `"hello world"` → changes `hello world` (keeps quotes)
- `da(` on `fn(a, b, c)` → deletes `(a, b, c)` including parentheses
- `yi{` → copy contents inside `{ ... }`

---

## Visual mode selection

- `v` → start selecting (character-wise)
- `V` → select whole lines
- `Ctrl-v` → block select (columns)

Then use operators:
- `d` delete selection
- `c` change selection
- `y` yank selection
- `>` indent, `<` outdent

Examples:
- `v$` then `d` → delete from cursor to end of line
- `Vjj` then `>` → indent 3 lines

---

## Deleting & changing quickly

- `x` → delete character under cursor
- `dd` → delete line
- `D` → delete to end of line (`d$`)
- `cc` → change whole line
- `C` → change to end of line (`c$`)
- `dw` / `cw` → delete/change word

Examples:
- `dd` on `console.log("x")` → removes the whole line
- `C` on `return something;` → deletes rest of line and enters insert

---

## Copy (yank) & paste

- `yy` → yank line
- `y{motion}` → yank motion
- `p` → paste **after** cursor (or below line)
- `P` → paste **before** cursor (or above line)

Examples:
- `yy` then `p` → duplicate current line below
- `yi"` then `p` → copy string contents, paste elsewhere

VSCode tip:
- Enable system clipboard in settings:
  - `"vim.useSystemClipboard": true`

---

## Undo / redo

- `u` → undo
- `Ctrl-r` → redo

Example:
- After a bad delete: `u`

---

## Repeat

- `.` → repeat last change

Example:
- Change `log` → `info` once, then move to the next occurrence and press `.`

---

## Substitution (find & replace)

- `:%s/old/new/g` → replace in whole file
- `:%s/old/new/gc` → replace with confirmation

Examples:
- `:%s/var/const/g`
- `:%s/\.forEach/\.map/gc`

(Vim whole-word boundaries)
- `:%s/\<users\>/people/g`

---

## Macros (automation)

- `qa` → start recording macro into register `a`
- `q` → stop recording
- `@a` → run macro
- `10@a` → run macro 10 times

Example (add a comma at end of line, go down):
1. On a line: `name: "Ada"`
2. `qa`
3. `A,` (append comma)
4. `j`
5. `q`
6. Repeat: `@a @a @a`

Undo if you overshoot: `u`

---

## VSCode navigation helpers (commonly supported)

(These depend on your VSCode Vim extension config, but often work out of the box)

- `gd` → go to definition
- `gD` → peek definition
- `gr` → find references
- `gi` → go to last insert position
- `Ctrl-w h/j/k/l` → move between splits (editor groups)

---

## A tiny practice mini-routine (5 minutes)

1. `/return` then `n` (search + next)
2. On a string: `ci"` (edit inside quotes)
3. On a function call: `ci(` (edit arguments)
4. Delete a line: `dd`, then undo: `u`
5. Make one change and repeat it elsewhere: `.`

---

### Quick “top 15” to memorize

`w b e` • `0 ^ $` • `gg G` • `/ n` • `f t ;` • `v V` • `d c y` • `dd` • `ci"` • `ci(` • `p` • `u` • `.` • `:%s///g` • `qa @a`
