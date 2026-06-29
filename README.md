General Concepts
What does RTFM mean?
Read The Fing Manual*. It’s a common (and blunt) phrase in tech reminding you that the answer to your question is usually already documented in the software's manual or help pages.

What is a Shebang?
A shebang (#!) is a special character sequence at the very beginning of a script. It tells the operating system which interpreter to use to execute the rest of the file. For your project, #!/bin/bash tells the system to run the script using Bash.

What is the Shell?
The shell is a program that acts as a command interpreter. It takes the text commands you type, translates them for the operating system's kernel to execute, and returns the output to you.

What is the difference between a terminal and a shell?
Terminal: The window or visual interface where you type. It just captures your keyboard input and displays text output.

Shell: The brains inside that window. It is the program that actually understands and executes your commands (e.g., Bash, Zsh).

What is the shell prompt?
The text or symbols displayed by the shell indicating it is ready to accept a new command (e.g., user@ubuntu:~$).

How to use the history (the basics)
Press the Up Arrow and Down Arrow keys to cycle through previously typed commands.

Type history to see a numbered list of all past commands.

Navigation
What do the commands cd, pwd, and ls do?
pwd (Print Working Directory): Shows exactly where you currently are in the filesystem.

cd (Change Directory): Moves you to a different folder.

ls (List): Displays the files and folders inside your current directory.

What are the . and .. directories?
. (Single dot): Represents the current directory.

.. (Double dot): Represents the parent directory (the folder one level up).

What is the root directory?
The absolute top-level directory of the entire Linux system. It is represented by a single forward slash (/). Everything on the system lives inside it.

What is the home directory, and how to go there?
The home directory is a user's personal workspace (usually /home/username). You can instantly jump there by typing cd or cd ~.

What is the difference between / (root) and /root?
/ is the root directory, the absolute base of the entire system.

/root is the personal home directory for the administrator account (the "root" user).

Hidden files and how to list them
Characteristics: Hidden files start with a dot (e.g., .bashrc). They don't show up during a normal ls.

How to list: Use ls -a (the -a stands for all).

What does cd - do?
It toggles back to the previous directory you were just working in (like a "back" button).

Looking Around
What do ls, less, and file do?
ls: Lists directory contents.

less: Displays the contents of a text file one page at a time (great for reading long files).

file: Analyzes a file and tells you what kind of file it is (e.g., text, image, executable).

Options vs. Arguments
Options (Flags): Modify how a command behaves, usually starting with a dash (e.g., -l or -a).

Arguments: The target the command acts upon (e.g., a filename or folder path).

Example: In ls -l Documents, -l is the option and Documents is the argument.
