## Navigate to a directory quickly in Cursor (after SSH connection)

When connected to a remote machine via SSH in Cursor, browsing folders through the file explorer can be slow. Instead, you can jump directly to directories using these methods.

---

### 1. Open a folder directly by path (recommended)

1. Press:

   `Ctrl + K` then `Ctrl + O`

   *(or go to **File → Open Folder**)*

2. In the path field, type the **absolute path**:

   `/home/ramesh/projects/k8s-operator`

   or a **relative path**:

   `../configs`

3. Press **Enter**

Cursor will immediately open that directory and show its structure in the explorer.

---

### 2. Use the Command Palette

1. Press:

   `Ctrl + Shift + P`

2. Type:

   `File: Open Folder`

3. Enter the directory path and press **Enter**.

---

### 3. Navigate via terminal (fast if you know the path)

Open the integrated terminal:

`Ctrl + \``

Navigate using:

```bash
cd /home/ramesh/projects/operator
```

Then open that directory as the workspace:

```bash
cursor .
```
### 4. Jump to a file quickly

If you know the file name but not its location:

Press:

`Ctrl + P`

Then type the file name, for example:

`deployment.yaml`

Cursor will search the entire workspace and open the file.

---

### 5. Open a file using its path

Press:

`Ctrl + P`

Then type something like:

`configs/envoy/envoy.yaml`

Cursor will jump directly to that file.

---

### Pro Tip

Use **Go to Symbol in Workspace** to jump across code:

`Ctrl + T`

This allows you to navigate directly to functions, structs, variables, or symbols without browsing directories.

---

### Recommended workflow when using SSH with Cursor

- `Ctrl + P` → jump to files instantly  
- `Ctrl + K Ctrl + O` → open folder by path  
- `Ctrl + T` → jump to symbols across the workspace  

With these shortcuts, you rarely need to manually navigate through the directory tree.
