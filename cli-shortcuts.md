### CLEAR THE SCREEN

`clear` and `ctrl-l`

### JUMP TO BEGINNING/END

`ctrl-a` and `ctrl-e`

### WORD AT A TIME

`alt-f` and `alt-b`

### KILL BY LINE

`ctrl-k` - kill from cursor to end of line

`ctrl-u` - kill from cursor to start of line

### KILL BY WORD

`alt-d` kill to end of current word

`alt-delete` or `ctrl-w` - kill to start of word

### YANK

`ctrl-y` - Yank from kill ring (ie paste, although the kill ring and the sys clipboard are two different things)

### HISTORY

`history | less`

`ctrl-r` enters reverse search of history - so `ctrl-r` then `curl` shows me the most recent curl command, then I can scroll backward through them with more `ctrl-r`

### FIND

Finds every single file in current working dir including subdirectories

`find ~/Downloads` - find everything in Downloads + its subdirs

`find ~/Downloads -type f` or `find ~/Downloads -type d` finds only files or directories

`find ~/Downloads -name "*.md"` finds all md files in Downloads; Use `-iname` for case insensitive

`find ~/Downloads -iname "*.md" | wc -l` pipes results to wordcount with the -l option counting the number of lines, so this is a way to count how many results exist for this search.

`find -name "*[0-9]*" | wc -l` finds how many filenames contain a number

`find -size +1G` or maybe `-50M`

`find -user <username>`

`find -iname "*[13579]_open*"` finds files that have an odd number, then \_open

**TIMESTAMPS** (seen in `ls -l`)

- `mtime`, or modification time, is when a file was last modified AKA when its contents last changed. `ls -l` shows this by default; doesn't change when name, props, location changes
- `ctime`, or change time, is when a file was last changed. `ls -lc` includes permissions, name, location changes
- `atime`, or access time, is updated when a file is read by an application or a command like `cat`. `ls -lu`

**FIND WITH TIME**

- `find -mmin -20`matches items that were modified LESS than 20 minutes ago. Use `amin` and `cmin` for time accessed/modified
- We can use the `-mtime num` option to match files/folders that were last modified num\*24 hours ago. Not exactly by days, but by 24 hour periods

**LOGICAL OPERATORS** `-not`, `-or`, `-and` (but AND is usually implied and often not needed)

- `find -type f -not -name "*.html"` all files not ending in .html
- `find -cmin -60 -not -name "*.log"` all files changed in the last 60 w/o .log
- `!` is a shortcut for `-not`

### VIEW FILE CONTENTS

- `cat` - concatenate files together on screen or just show one: cat file1 file2 -n to show line numbers
- `tac` - Does the same, but returns file in reverse order (last line first)
- `rev` - Returns the file with the lines reversed horizontally - cats = stac
- `less` - show contents of file in paginated mode - move ahead a page with **SPACE** or **F**, back with **B**; **ENTER** or **arrows** to move by line, **forward slash plus pattern** to search, exit with q (man pages use less for display)
- `head` - prints first n lines (10 by default) - head .bash_history shows first 10
- `tail` - prints last n lines (10 by default) - tail -100 .bash_history (-100 is short for -n 100) shows last 100
- `tail -f` (or -follow) causes tail to wait for changes in the file - useful for monitoring an active log file - `tail mylog -100 -f`
- `wc` - word count, returns 3 numbers - lines, words (or things separated by spaces, ie ' - ' is a word), bytes use `-w` for words, `-l` for lines, `-m` for chars, `-c` for bytes
- `sort` - sorts the lines of a file - `-r` for reverse - `sort -r cats.txt` - use `-n` to sort numbers numerically, `-u` to show unique values

---

- ctrl-f and ctrl-b - works like the l/r arrows but keeping hands on home row
- ctrl-t - swaps current character with the preceeding one
- alt/opt-t - swap words
- !3543 (where 3543 is a line number in history) displays the command at that line, ready to run
- history lives in `~/.bash_history`
- locate - does a search of PATHNAMES across our machine - uses a db that it complies/maintains which is fast but may not be complete. Doesn't matter where you are when you do the search.
- locate /bin/less??? = match the string and return items that have three chars after (/bin/lesskey)
- options -i = ignore casing -l = limit the number of responses, ie -l3 -e = return results that exist - ie, if you delete files on the machine they will still be listed in the locate db for a time, so this option checks to see if they exist on the disc
- also, sudo updatedb will update the db manually (time consuming)

### Redirecting

- `date > today.txt`
- `sort -n prices.md > newprices.txt`
- `ls -la /my/dir > filelist.txt`
- `echo $PATH >> path.txt`
- `echo $PATH 2> errorlog.txt`
- `echo $PATH 2>> errorlog.txt`
- `echo $PATH >> path.txt 2>> errorlog.txt` (redir both output and error - put output FIRST)
- `echo $PATH &>> path.txt` (shortcut to redir standout and err to same file)

- > creates a new file if none exists, OVERWRITES an existing one
- > > also creates a new file, APPENDS to existing
- 2> redirects standard error, so error message goes to file, not screen - OVERWRITES
- 2>> appends
- We use 2 b/c that's the number for standerr; standin is 0, standout is 1, so > is actually short for 1>

### Environment

- `printenv` shows my environment vars.
- `echo $PATH` shows PATH
- `myvar=HeyNow` or `myvar="Hank Kingsley"` sets a shell var which belongs to the current(?) shell session
- `export myvar=HeyNow` sets an environment variable, or `export mayvar` if it has already been set as a shell var
- `unset myvar` removes it from the set of env vars

For "non-login" sessions (typical sessions when you launch the terminal from the GUI). `etc/bash.bashrc`contains global configs for all users, and `~/.bashrc` contains specific settings for each user. For example, `PS1` which defines the style of the prompt, lives here.

To change setting in .bashrc, first `cp .bashrc .bashrc.old` for a backup!

**Aliases** - Shortcuts for common commands. For ex, `ll` for `ls -la` (which actually comes built-in with Ubuntu) and `l` does `ls -lah` (h for human-readable)

These store aliases for the session only...

- `alias hank='echo HEY NOW!'` then when I enter hank, I get HEY NOW!
- `type hank` tells me that 'hank is an alias for echo HEY NOW!
- No man page for `type` :(

To make them permenant, the same commands need to be in `~/.bashrc` or put them in another dir that is referenced in `~/.bashrc`. My bashrc comes with a built-in if statement pointing to `~/.bash_aliases`
