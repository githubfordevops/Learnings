# Git: Add a Folder Recursively

This document explains how to add and commit an entire folder (including all subfolders and files) using Git.

---

## Add a Folder Recursively

To stage all files and subdirectories inside a folder:

```bash
git add path/to/folder/

```

This stages:

- All files inside `src/`
- All nested subfolders and their contents

---

## Commit the Changes

After staging, commit the folder:

```bash
git commit -m "Add src folder recursively"
```
## Add All Files in the Repository (Optional)

To stage everything in the current repository:

```bash
git add .
```

Then commit:

```bash
git commit -m "Add all files recursively"
```

---

## Important Notes

- `git add folder/` **includes new and modified files**
- `git commit -am` **does NOT include new (untracked) files**
- Always verify what will be committed:

```bash
git status
```

To preview staged changes:

```bash
git diff --cached
```
