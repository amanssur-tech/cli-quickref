# Bash / Linux CLI

# Most important Bash Commands

Master the terminal with essential Bash commands, package management, file handling, and permissions. Use Cmd + F or Notion’s search to find commands instantly. This guide is meant to cover the most basic and useful commands and their options and is not exhaustive.

---

## 📚 Index

## **📁 Navigation**

To navigate files and directories using a command line interface (CLI), such as **Terminal** on macOS or Linux, you can utilize a variety of commands that help you move around the file system efficiently. The  **tab**  key can be used to autocomplete codes, eg when writing folder paths, and the  **↑**  and  **↓**  keys can be used to cycle through previous commands.

> ⚠️ For commands that accept a location, omitting it defaults to the current working directory `.`. Some commands like `pwd` do not allow specifying a location at all.

**pwd**

Print folder path of current working directory

**cd**

Change current working directory

`-`		previous directory	→ can be used to jump between two folders

> 🔀 **Path Shortcuts**  
Use to quickly reference directories  
`.`		current directory  
`..`		parent directory, eg `cd ../..`  quickly goes up two levels  
`~`		home directory, eg `/Users/<username>`  
`/`		root directory, if used at beginning of location path

**ls**

List files and folders

`-a`		Include hidden files, ie those starting with `.`  
`-l`		Long listing format with detailed information  
`-h`		→ Human-readable sizes, eg `1K` for 1024 bytes, used with `-l`  
`-t`		Sort by modification time from recent to oldest  
`-S`		Sort by size  
`-r`		Reverse sort order, useful with `-t` or `-S`  
`-R`		List subdirectories recursively, ie up to the deepest level  
`-1`		List only 1 file per line, useful for piping or scripting  
`-d`		List targets directly, without contents of directories, eg with: `ls -d */`

> *️⃣ **Wildcards**  
Use wildcards to match multiple filenames:  
`*`		Matches **any amounts of characters**, e.g. `ls *.txt` lists all `.txt` files  
`.*`		Matches **any hidden files** (names start with `.`), which `*` alone doesn’t  
`?`		Matches **exactly one character**, e.g. `ls a?.txt` matches `a1.txt`, `a3.txt`  
`[abc]` Matches **one character** from the set, e.g. `ls a[12].txt` → `a1.txt`, `a2.txt`

**mkdir**

Make new directory

`-p`		Create parent directories if needed, eg `mkdir -p parent/child`  
`-v`		”Verbose output” - Show a message for each created directory  
`-m`		Set permissions, eg `mkdir -m 755 new_directory` , `755` = writable by owner

> 🧱 **Basic Command Structure**  
Many command lines follow this order:  
`<command> <options> <option-values or sources> <target or location>`  
e.g. `mkdir -m 755 new_directory`  
→ command: `mkdir` | option: `-m` | value: `755` | target: `new_directory`

**touch**

Create a new file or update its timestamps

`-a`		Update only the access time  
`-m`		Update only the modification time  
`-c`		Do not create any files if non-existent

**clear**

Clear the terminal view		← this won’t undo any commands

---

## 📄 **File Management**

Learn to manipulate directories and files from the command line. For commands that allow dealing with multiple files at once the last argument will act as the destination, eg when creating or copying files.

**cat**

Show file contents or concatenate multiple files to a single output

`-n` 		Add numbers to each line  
`-b` 		Add numbers to non-blank lines only  
`-s` 		Suppress repeated blank-lines, only showing up to one

**cp**

Copy files and directories

`-R` 		Copy directories recursively	→ Must be used when copying folders  
`-i`		Interactive — ask before overwriting existing files  
`-f`  	Force overwrite and delete destination if needed  
`-u` 		Only overwrite existing files if their modification time is older  
`-a` 		Create exact clone by copying recursively and preserving all attributes  
`-p` 		Preserve timestamps, ownerships and permissions  
`-v` 		Verbose — display what is being copied

**mv**

Move files and folders or rename them if the path doesn’t change

`-i`		Interactive — ask before overwriting existing files  
`-v` 		Verbose — display what is being copied

**rm**

Remove files and folders irrevocably ⚠️

`-r` 		Delete directories recursively	→ Required when deleting folders  
`-i`		Interactive — ask before deleting each file  
`-f` 		Force delete without prompting, even if files don’t exist  
`-v` 		Verbose — display what is being copied

---

## **🔁 Redirection & Pipes**

Learn to redirect input and output to and from files and commands and connect processes in the shell.

**echo**

Output a line of text or a variable's value

`-n`		Don't add a new line at the end  
`-e`		Enable backslash escapes, eg `
` for new lines, `	` for tabs, etc.

> 🔀 **Redirect Operators**  
Can be used with commands that write output like `echo`:  
`>`		Redirect output → Saves to a file and overwrites it if it already exists ⚠️  
`>>`		Append output → Saves to the end of a file without overwriting content  
`|`		Pipe to next command → Sends output as input for command after `|`  
`<`		Redirect input → Take input from a file  
`<<` 		Takes multiline input until a defined delimiter, eg: `cat << END` (lines) `END`

**tee**

Show input on screen while also saving it to a file

`-a`		Append input to a file rather than overwriting it

**wc**

Count the number of lines, words, and bytes from input

`-l`		Only count the number of lines  
`-w` 		Only count the number of words  
`-c` 		Only count the number of bytes  
`-m` 		Only count the number of characters

**sort**

Sort lines of text alphabetically

`-r`		Sort in reverse order  
`-n` 		Sort numbers numerically, not alphabetically, eg `2` before `10`  
`-k`		Sort by column (delimiter: space), eg `-k2,2` (only col 2) or `-k2` (col 2 and beyond)  
`-u`		Remove duplicate lines	← must be adjacent, so sort first  
`-t`		Set a custom delimiter for columns, eg `","`, and use with `-k`  
`-o`		Output result to file  
`-b`		Ignore leading blanks  
`-f`		Ignore case, ie treat uppercase and lowercase as equal

**uniq**

Remove adjacent duplicate lines

`-c`		Prefix lines with the number of adjacent occurrences  
`-d`		Show only adjacent duplicate lines  
`-u`		Show only unique lines, ie those that appear exactly once in the input  
`-i`		Ignore case, ie treat uppercase and lowercase as equal

**grep**

Search for specific text and output the matching lines

`-i` 		Ignore case, ie treat uppercase and lowercase as equal  
`-r` 		Search directories recursively	→ Required for folder search  
`-n` 		Show the line numbers where each match appears  
`-v` 		Show lines that do not match the search text  
`-l` 		List files that contain matches only  
`-c` 		Show count of matching lines per file  
`-o` 		Only output the matched text, not the whole lines → Eg for use with `| wc`  
`-e` 		Search for multiple terms separately, by using `-e` before each

**sed**

Perform temporary line-by-line first-instance edits

`-e` 		Apply multiple edits at once, eg `-e '...' -e '...'`  
`-i` 		Make edits permanent in-place — no backup, no output  
`-n` 		No default output → use with custom printing  
`-f` 		Run multiple `'///'` commands from a file instead of using `-e`  
`'s///'` 	Substitute like `'s/old/new/'`  
`'///p'` 	Print the edited lines → Use with `-n` to print only matches  
`'///g'` 	Apply edits globally, not just the first match per line
