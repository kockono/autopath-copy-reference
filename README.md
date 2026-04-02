# autopath-copy-reference

## Purpose
This VS Code extension adds a simple command that copies the current selection (or the entire line when nothing is selected) together with the full path of the active file. The copied text has the format:

```
<selection or line> @ <full‑path-to-file>
```

It is useful when you want to paste a reference to a piece of code into another place (e.g., a chat, a ticket, or a note) and keep both the snippet and where it comes from.

## How it works
1. When you run the command (`Copy Reference with Path`) the extension:
   - Checks if there is a text selection in the active editor.
   - If a selection exists, it copies that text.
   - If there is no selection, it copies the whole line where the cursor is located.
   - Retrieves the full filesystem path of the active document via `vscode.window.activeTextEditor?.document.uri.fsPath`.
   - Builds a string in the form `<text> @ <path>`.
   - Places that string on the clipboard.

2. The command can be triggered:
   - From the Command Palette (`Ctrl+Shift+P` → type “Copy Reference with Path”).
   - Or bound to a keyboard shortcut of your choice (e.g., `Ctrl+Shift+L`) via `keybindings.json`.

## Example
Assuming you have the following line in `src/utils/format.js`:

```js
function formatDate(date) {
  return date.toISOString().split('T')[0];
}
```

- If you select `return date.toISOString().split('T')[0];` and run the command, the clipboard will contain:

```
return date.toISOString().split('T')[0]; @ C:\projects\myapp\src\utils\format.js
```

- If you place the cursor anywhere on the line `function formatDate(date) {` and run the command with no selection, the clipboard will contain:

```
function formatDate(date) { @ C:\projects\myapp\src\utils\format.js }
```

## Installation
1. Download the latest `.vsix` from the [Releases] page (or build it yourself with `vsce package`).
2. In VS Code, open the Extensions view (`Ctrl+Shift+X`), click the … menu → **Install from VSIX…**, and select the downloaded file.
3. Reload the window when prompted.

## Usage
- Open the Command Palette (`Ctrl+Shift+P`), run **Copy Reference with Path**.
- Or use the keyboard shortcut you assigned.

## Contributing
Feel free to open issues or submit pull requests if you have ideas for improvements.

## License
MIT