## keyboard shortcuts

### general

- `Ctrl + Shift + P` `F1` show command palette
- `Ctrl + Shift + N` new instance/window
- `Ctrl + Shift + W` close instance/window
- `Ctrl + ,` user settings
- `Ctrl + KS` keyboard shortcuts

### basic editing

- `Alt + ↑/↓` move the entire line up/down (useful)
- `Shift + Alt + ↑/↓` copy line up/down
- `Alt + ↑/↓` scroll line up/down
- `Ctrl + Enter` insert line below
- `Ctrl + Shift + Enter` insert line above
- `Ctrl + Shift + \` jump to matching bracket
- `Ctrl + ]/[` indent/outdent line
- `Ctrl + Shift + ]/[` collapse/uncollapse line

### search and replace

- `Ctrl + F` find
- `Ctrl + H` replace
- `F3`/`Shift + F3` find next/previous
- `Alt + Enter` select all occurences of find match

### rich languages editing

- `Ctrl + Space` trigger suggestion
- `Ctrl + Shift + Space` trigger parameter hints
- `Shift + Alt + F` format document
- `Ctrl + KF` format selection
- `F12` goto definition
- `Alt + F12` peek definition
- `Ctrl + .` quick fix
- `Shift + F12` show references
- `F2` rename symbol


### file management
- `Ctrl + N` new file
- `Ctrl + O` open file
- `Ctrl + Shift + S` save as
- `Ctrl + F4` close
- `Ctrl + Tab` open next
- `Ctrl + Shift + Tab` open previous

### display/navigate
- `Ctrl + B` toggle sidebar visibility
- `Ctrl + Shift + E` show explorer/toggle focus
- `Ctrl + Shift + F` show search

### debug
- `F9` togggle breakpoint
- `F5` start/continue
- `Shift + F5` stop

### integrated terminal
- `` Ctrl + ` `` show integrated terminal
- `` Ctrl + Shift + ` `` create new terminal

### preview
- `Ctrl + Shift + V` preview a markdown

### navigation
- `Alt + <-/->` switch tabs


### others (notes)
- right click:
    - `goto definition`
    - `find all references` to the function (only on the open files)
    - `peek definition`
    - `rename symbol`, changes all instances within scope for that variable
    - `change all instances`, within the file
    - `refactor`
- format as you type:
    - editor: format on type
- format on save
- formatting force aligned


### create custom keybindings for common commands
- if you have come from a different text editor (you can download the keymapping for that editor)

### using emmet notation
- HTML
    - instead of using `<div>` and pressing `spacebar`, you can use `div` and press `tab`
    - try `div>ul>li`, `div>ol*2>li*6`, img.
    - try `"emmet.triggerExpansionOnTab": true`
        - `.`-> class
        - `#` -> id
        - `$` -> wild card
            - try `ul>li.example$*4>lorem`
    - when multiple choices, even try fuzzy searches when figuring out what to type
    
### use git lens

### use code snippets
- open a new `.js` file and use `rafce`

### automating task to run on startup in VSCode
- create a `tasks.json` file in `.vscode` folder
  ```json
    {
    "version": "2.0.0",
    "tasks": [
        {
        "label": "Load .venv",
        "type": "shell",
        "command": "load .venv",
        "windows": {
            "command": ".venv/Scripts/Activate.ps1"
        },
        "presentation": {
            "reveal": "always",
            "panel": "new"
        },
        "runOptions": { "runOn": "folderOpen" }
        }
      ]
    }
```
