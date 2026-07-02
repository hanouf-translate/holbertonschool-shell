Here is a complete, master-level study guide explicitly covering every single command, conceptual objective, and technical constraint outlined in your prompt. This acts as a comprehensive reference guide for your project and your upcoming viva/evaluation.

### Part 1: Command Reference Cheat Sheet

- **`printenv`**: Displays all environment (global) variables exported to the current environment and any child processes.
    
- **`set`**: Displays _all_ variables (both local and environment) as well as any shell functions currently defined.
    
- **`unset`**: Deletes a local or environment variable from memory entirely (e.g., `unset MY_VAR`).
    
- **`export`**: Promotes a local variable into an environment (global) variable so that child processes and external scripts can access it.
    
- **`alias`**: Creates a shortcut or replacement name for a long command (e.g., `alias ll='ls -l'`). When typed without arguments, it lists all active aliases.
    
- **`unalias`**: Removes a previously defined shortcut (e.g., `unalias ll`).
    
- **`.` (Dot)**: A built-in command that reads and executes commands from a file _within the current shell session_ instead of spinning up a subshell.
    
- **`source`**: An exact synonym for the `.` (dot) command in Bash.
    
- **`printf`**: Formats and prints data to standard output. It is more robust, predictable, and powerful than `echo`.
    

### Part 2: Shell Initialization Files

When you log into a Linux system, Bash configures itself by executing special configuration files in a specific order depending on whether it is a login or non-login shell.

```
[User Login Session]
       │
       ▼
 1. /etc/profile  ───► Reads files in ──► 2. /etc/profile.d/
       │
       ▼
 2. ~/.bashrc
```

- **`/etc/profile`**: A system-wide initialization file that sets environment variables and settings for **all users** upon their initial interactive login shell.
    
- **`/etc/profile.d/`**: A structural directory containing individual `.sh` script files. The `/etc/profile` file loops through and executes everything inside this directory. It allows package maintainers to drop in application-specific environment settings cleanly without modifying `/etc/profile` directly.
    
- **`~/.bashrc`**: A user-specific file executed for every **non-login interactive shell** (for example, every time you open a new terminal window inside an existing GUI or start a subshell). This is the best place to define your custom aliases and local environment paths.
    

### Part 3: Variables & Special Parameters

#### Local vs. Global (Environment) Variables

- **Local Variable**: Variables that exist _only_ within the specific shell process where they were created. Subshells, child processes, or external scripts launched from this terminal cannot see them.
    
- **Global (Environment) Variable**: Variables marked by `export`. They are passed down to any child processes, commands, or application scripts started by that shell session.
    

#### Variables Management

- **Create/Update**: `VAR_NAME="value"` (Note: _Never_ put spaces around the `=` sign).
    
- **Delete**: `unset VAR_NAME`
    

#### Reserved Variables

- **`HOME`**: Stores the absolute pathname of the current user's home directory (e.g., `/home/username`). Used by commands like `cd` to know where to go when typed without arguments.
    
- **`PATH`**: A colon-separated list of directories (e.g., `/usr/bin:/bin`) that the shell searches through sequentially whenever you type a command. If an executable isn't in one of these folders, the shell returns `command not found`.
    
- **`PS1`**: The "Prompt String 1". This variable defines the visual layout of your command line prompt (e.g., showing username, hostname, and current directory `user@host:~$` ).
    

#### Special Parameters

- **`$?`**: Stores the exit status code of the **most recently executed foreground command**. A `0` indicates absolute success, while any non-zero integer (`1` through `255`) represents an error code or specific failure state.
    

### Part 4: Expansions & Quoting

#### Expansion

Expansion is the process where Bash looks at tokens on your command line and evaluates them into something else _before_ executing the final command. This includes expanding wildcards, evaluating arithmetic, substituting command outputs, and evaluating variable names.

#### Single Quotes (`'`) vs. Double Quotes (`"`)

- **Single Quotes**: Strong, literal preservation. Bash treats _every single character_ inside literal single quotes completely at face value. No expansions of any kind happen (e.g., `'$VAR'` prints exactly `$VAR`).
    
- **Double Quotes**: Flexible preservation. It protects spaces and most characters but explicitly **allows** three major expansions: Variable expansion (`$VAR`), Command substitution (`$()`), and Arithmetic expansion (`$(())`). For example, `"$VAR"` evaluates to the actual content stored in the variable.
    

#### Command Substitution

Command substitution lets you run a command and plug its output directly into another command or assign it to a variable.

- **Modern way**: `$(command)` — Highly recommended because it nests easily.
    
- **Legacy way**: `` `command` `` (Backticks) — Harder to read and difficult to nest, but functionally identical.
    

### Part 5: Shell Arithmetic

Because you are explicitly barred from using `bc`, you must rely completely on Bash's native integer arithmetic engine using the **`$(())`** operator structure:

Bash

```
# Basic Addition example
RESULT=$((5 + 3))

# Using variables inside arithmetic (the $ symbol on internal variables is optional)
X=10
Y=2
TOTAL=$((X * Y))
```

_Note: Bash arithmetic only supports whole integers. It does not natively handle decimals/floating-point operations._

### Part 6: The `alias` Command

- **Create an alias**: `alias custom_name='command_to_run'`
    
- **List all active aliases**: Type exactly `alias` on a line by itself.
    
- **Temporarily disable an alias**: Escape the alias using a backslash (`\alias_name`). This bypasses the alias substitution layer completely and runs the real underlying system command.
    

### Part 7: Conceptual Deep Dive

#### What happens when you type `ls -l *.txt`?

When you press enter, the shell orchestrates the following exact steps:

1. **Expansion (Globbing)**: Before running `ls`, the shell looks at the wildcard expression `*.txt`. It scans the current directory and replaces `*.txt` with a space-separated list of all matching files (e.g., `ls -l notes.txt draft.txt`). If no matching files exist, it passes the literal string `*.txt` forward (depending on shell configuration).
    
2. **Alias Resolution**: The shell checks if `ls` is defined as an alias. If it is, it expands it to its full definition (like `ls --color=auto`).
    
3. **Command Lookup**: The shell verifies if the command is a built-in. Since `ls` is an external program, it starts looking through the directories listed inside your `$PATH` variable until it locates the binary file at `/bin/ls` or `/usr/bin/ls`.
    
4. **Execution**: The shell forks a child process and uses `execve` to execute the binary, passing `-l`, `notes.txt`, and `draft.txt` as distinct arguments in its command-line array (`argv`).
    

### Part 8: Hard Project Requirements Checklist

To pass the automated checker framework flawlessly, ensure every script matches these constraints perfectly:

- **Length Constraint**: Exactly two lines long. Checking via `wc -l filename` must report `2`.
    
- **Trailing Newline**: Every file must end with a clean empty newline character.
    
    - _Why?_ UNIX standards define a valid "line" of text as a sequence of characters terminated by a newline (`\n`). Without it, processing utilities like `head`, `tail`, `sed`, or streaming tools might drop or fail to process the final line of your script.
        
- **Shebang Header**: Line 1 must be perfectly formatted as:
    
    Bash
    
    ```
    #!/bin/bash
    ```
    
- **Banned Elements**: Absolutely no `&&`, `||`, `;`, `bc`, `sed`, or `awk`. Pipelines must rely entirely on single paths (`|`) and standard redirections (`>`, `>>`, `<`, `2>`).
    
- **Permissions**: Mark every script executable before checking into Git:
    
    Bash
    
    ```
    git update-index --add --chmod=+x <filename>
    ```