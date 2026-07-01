Welcome to the **I/O Redirection and Filters** project! This is where the real power of the Linux command line unlocks. Instead of just managing file properties, you are about to learn how to manipulate data streams, chain programs together, and process text like a pro.

---

## 🛑 Critical Project Rules to Remember

Before writing a single line of code, keep these strict requirements in mind to avoid immediate checker failures:

* **Strictly 2 lines per file:** Every script must be exactly `#!/bin/bash` on line 1, and your command on line 2.
* **No forbidden operators:** You are strictly **not** allowed to use backticks (```), `&&`, `||`, or semicolons (`;`).
* **No advanced text stream editors:** Using `sed` or `awk` is completely prohibited for these tasks.
* **Mandatory Newline:** Every file must end with a trailing newline (pressing `Enter` on line 2), or the byte counters and checker will fail.

---

## 🛠️ The Core Concepts Broken Down

### 1. I/O Redirection (The Data Pipelines)

By default, commands take input from your keyboard (**stdin**) and print output to your screen (**stdout**). Redirection lets you change this:

* **`>` (Overwrite):** Redirects standard output to a file. If the file exists, it wipes it clean first.
```bash
echo "Hello World" > file.txt

```


* **`>>` (Append):** Redirects standard output to a file, but tacks it onto the end without deleting what's already there.
```bash
echo "Another line" >> file.txt

```


* **`<` (Input Redirection):** Forces a command to read data from a file instead of waiting for you to type it.
```bash
cat < file.txt

```


* **`|` (The Pipe):** Takes the standard output of the command on the left and passes it directly as the standard input to the command on the right. **This is how you chain filters.**
```bash
cat file.txt | grep "Hello"

```



---

### 2. The Core Command Toolbox (Filters)

Here is exactly what your assigned tools do:

| Command | Primary Action | Common Practical Example |
| --- | --- | --- |
| **`head`** | Displays the *first* few lines of a file (default is 10). | `head -n 5 file.txt` (Shows first 5 lines) |
| **`tail`** | Displays the *last* few lines of a file (default is 10). | `tail -n 3 file.txt` (Shows last 3 lines) |
| **`wc`** | Counts lines (`-l`), words (`-w`), or bytes (`-c`). | `wc -l file.txt` (Counts total lines) |
| **`sort`** | Sorts text lines alphabetically or numerically (`-n`). | `sort -n numbers.txt` |
| **`uniq`** | Removes **adjacent** duplicate lines. *(Tip: Usually paired right after a `sort` command!)* | `sort file.txt | uniq` |
| **`grep`** | Searches text for lines matching a specific pattern. | `grep "error" log.txt` |
| **`tr`** | Translates, squeezes, or deletes specific characters. | `tr 'a-z' 'A-Z'` (Converts text to UPPERCASE) |
| **`cut`** | Slices out specific columns or sections from each line. | `cut -d':' -f1` (Extracts username from config files) |
| **`rev`** | Reverses the character order of every line horizontally. | `echo "abc" -> "cba"` |
| **`find`** | Searches the directory tree for files matching criteria. | `find . -name "*.sh"` |

---

### 3. Understanding System Identity Files

You will be asked to extract data from core system text databases. You need to know their layouts:

* **`/etc/passwd`**: Stores essential user account configuration details. Every line uses a colon (`:`) separator with 7 distinct fields:

$$\text{username} : \text{password\_placeholder(x)} : \text{UID} : \text{GID} : \text{User Info} : \text{Home Directory} : \text{Login Shell}$$


* **`/etc/shadow`**: Securely stores encrypted user password data, requiring root access to read.

---


# Shell I/O Redirection & Filters — Command Cheat Sheet

A comprehensive quick-reference guide tracking the command lines and text-manipulation utilities designed during the project tasks.

---

## 📋 Command Reference Matrix

| Task File | Objective / Operation | Core Command String |
| :--- | :--- | :--- |
| `10-no_more_js` | Delete all regular `.js` files recursively | `find . -type f -name "*.js" -delete` |
| `11-directories` | Count all directories & sub-directories (excl. `.`/`..`) | `find . -mindepth 1 -type d \| wc -l` |
| `12-newest_files` | Display 10 newest files sorted newest to oldest | `ls -t1 \| head -n 10` |
| `13-unique` | Output words appearing exactly once from a list | `sort \| uniq -u` |
| `14-root` | Parse lines containing the pattern "root" | `grep "root" /etc/passwd` |
| `15-countthatword`| Count lines containing the pattern "bin" | `grep -c "bin" /etc/passwd` |
| `16-whatsnext` | Display matching pattern "root" + 3 lines after | `grep -A 3 "root" /etc/passwd` |
| `17-hidethis` | Invert match to show lines without "bin" | `grep -v "bin" /etc/passwd` |
| `18-letteronly` | Extract lines starting strictly with a letter | `grep '^[a-zA-Z]' /etc/ssh/sshd_config` |
| `19-A_and_c` | Translate characters (A $\rightarrow$ Z, c $\rightarrow$ e) | `tr 'Ac' 'Ze'` |
| `20-hi_c` | Strip out all occurrences of 'c' and 'C' | `tr -d 'cC'` |
| `21-reverse` | Reverse character order of standard input streams | `rev` |
| `22-users_and_homes`| Extract and sort users with their home paths | `cut -d: -f1,6 /etc/passwd \| sort` |

---

## 🛠️ Tool Deep Dive

### 1. The `find` Command
Used for directory traversal and selective target asset operations.
* `-type f` / `-type d` : Filter purely for regular files or directories respectively.
* `-mindepth 1` : Forces omission of the baseline matching directory (`.`).
* `-delete` : Performs an atomic removal on items matching preceding conditions.

### 2. Stream Filters (`grep`, `tr`, `cut`)
* **`grep`**: Regular expression search. Use `-v` to invert matching, `-c` to tally instances, and `-A [n]` for trailing context.
* **`tr`**: Translate or delete tokens out of a character stream sequence.
* **`cut`**: Splice tabular files horizontally using structural indicators like `-d:` (colon field extraction).

### 3. Pipeline Aggregators (`sort`, `uniq`, `wc`)
* `sort | uniq -u` isolates unique records cleanly. 
* `wc -l` generates row tallies from input vectors.