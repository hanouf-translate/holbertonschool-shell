# Linux Commands & Git Bash Quick Reference Guide

A structured cheat sheet of the essential shell core-utilities, positional expansion switches, and repository flags covered during project configuration tasks.

---

## 1. Directory Traversal & Structure Deployment

| Command Syntax | Functional Behavior & Context Application |
| :--- | :--- |
| `cd -` | **Change to Previous Directory:** Switches your shell back to your last immediate directory position (queries the `$OLDPWD` variable). |
| `cd ..` | **Move to Parent Folder:** Moves you up one single nesting level. *(Note: Linux strictly requires the space before the double dots; `cd..` fails).* |
| `mkdir /tmp/name` | **Make Temporary Subfolder:** Deploys a new custom target workspace directory safely inside `/tmp/`. |
| `mkdir -p w/to/s` | **Recursive Directory Path Provisioning:** The `-p` flag builds missing parent containers automatically in a row without breaking or complaining. |

---

## 2. Target Identification & Directory Inspection

| Command Syntax | Functional Behavior & Context Application |
| :--- | :--- |
| `ls -lan` | **Numerical Content List:** Formats the output layout long (`-l`), targets all system-hidden dotfiles (`-a`), and prints User/Group IDs numerically (`-n`). |
| `ls -la . .. /boot` | **Multi-Path Sequenced Listing:** Evaluates and cleanly streams contents of the current workspace (`.`), parent (`..`), and system `/boot` folders in precise sequence. |
| `file <path>` | **Header Integrity Verification:** Directly interrogates file signatures to return their exact internal type structure, independent of the suffix extension. |

---

## 3. Storage Alteration & Filter Globbing Patterns

| Command Syntax | Functional Behavior & Context Application |
| :--- | :--- |
| `mv source dest` | **Item Relocation or Renaming:** Displaces item binaries or documents across distinct directories. |
| `cp -u *.html ..` | **Conditional Sync Copying:** The `-u` update flag pushes files up one layer *only* if they are missing or hold a newer modification timestamp. |
| `rm *~` | **Editor Workspace Purge:** Employs explicit shell expansion filters to safely isolate and strip backup/temporary files terminating in a tilde (`~`). |
| `[[:upper:]]*` | **POSIX Upper Case Selection:** Match files starting with uppercase letters. Requires dual brackets: inner `[:upper:]` defines the class, outer `[ ]` acts as the matcher. |

---

## 4. Workstation Automation & Validation Workflow Checklist

When managing workspace development inside a standard **Windows Host** interfacing with an automated grading infrastructure via **Git Bash**, execute this precise sequence to bypass access blocks and line ending errors:

```bash
# 1. Silences annoying automatic Windows CRLF warning loops permanently
git config --global core.safecrlf false

# 2. Indexes the new file and forces execution flags to stick upstream
git update-index --add --chmod=+x <filename>

# 3. Snapshot change status and deploy safely to origin
git commit -m "Configure script tracking structures with executable bit permissions"
git push
pwd is for printing absolute path name of the current working directory.
FLAGS
l -> long format 
a -> hidden files 
n -> groups and id along with users
ls -> listing dict
u -> The update flag (handles both conditions: missing files or newer files).
FOLDERS
/boot -> the global boot dict