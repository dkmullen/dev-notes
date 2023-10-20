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

### Piping

- `ls -la | less` for pagination of large set of results
- `ls -la | sort -h | head -8` - List all files in long format, sort by comparing human-readable numbers, output the first eight results

Redirecting v Piping - `>` redirects standout to a file; `|` connects a command to another command

- `tee` (like a T-shaped fitting in a pipe) sends standard output in two directions, ie to a file and to another command at the same time.
  `cat colors.txt words.txt | tee colorsAndWords.txt | wc` concatenates two files and (with the tee) sends the results to a new file AND counts the words

### Cron

Edit cron job with the command `crontab -e` (the e fires up the editor, and crontab is the program that handles cron files)

**Syntax** - Five values with a space (or several spaces, doesn't matter) between them.

- a b c d e command = minute (0-59) hour (0-23), day of month (1-31) month (1-12, or spell out the month), day of week (0-6))
- Other syntax = `*` for any value, **comma** for a list of values (5,6,8), **dash** for range of values (1-3) and `*/5` for step values (every 5 in this case)

**Examples**

- `30 * * * * * <command>` - Run on min 30 of every hour, day... (not every 30 minutes!)
- `*/30 * * * * * <command>` - Every 30 min
- `0 0 * * *` - Every day at midnight (when the hour and minute are both 0)
- `30 6 * * *` - Every day at 6:30 am
- `30 6 * * 1` - Every Monday at 6:30 am
- `30 6 * 4 1` - Every Monday in April at 6:30 am
- `0 0 1 * *` - First day of each month at midnight
- `* * * * * echo "Hey now! - $(date)" >> ~/cron-demo.log 2>&1` - Echo the message to the file every minute and save errors in the same file.

https://crontab.guru is a helper site

### Expansion

Using wildcards is called expansion b/c `ls *.doc` gets expanded by the shell to be `ls cats.doc dogs.doc` etc

- In addition to the `*` wildcard, there is `?` which matches a single character. Ie, `ls app.??` matches app.js, app.py, not app.txt
- Square brackets can specify a range - `ls pic[123].png` or `ls pic[1-3].png` will return pic1.png, pic2.png, pic3.png - `ls [A-Z]*` lists all files that start with a capital letter
- `^` in brackets negates, ie `ls [^A-Z]*` lists all that don't begin with capital letters

**Curley braces**

- `touch {M,T,W,TH,F}-journal.txt` makes m-journal.txt...
- `mkdir jan{1..31}` makes directories jan1 thru jan31
- `mkdir jan{1..31..2}` makes directories jan1 thru jan31 adds a third value for the range, and makes jan1, jan3, jan5 etc
- `mkdir -p {Mon,Tue,Wed,Thur,Fri}/{Breakfast,Lunch,Dinner}` makes directories for each day, each of which has subdirs for each meal (the `-p` arg says to not throw an error if the parent dir doesn't exist, which is the normal behavior if you try to create a subdir to a non-existent parent)
- `mkdir -p {Mon,Tue/{1..10}{AM,PM},Wed,Thur,Fri}/{Breakfast,Lunch,Dinner}` does the same but with Tuesday, makes subs for 1-10 am and pm

### Quotes

Double quotes allow use of extra spaces, and doesn't change the meaning of $, backslash, or backtick. Single quotes take everything as literal.

- `echo "Today is...     $(date)"` gives Today is... Mon Oct 7<etc>
- `echo 'Today is...     $(date)'` gives Today is... $(date)

### Command substition

$(date) or `date` works

- `echo $(whoami)` or echo `whoami`

### grep

Searches the CONTENTS of files (or text not in a file too) for matches

- `grep <pattern> <file>` - ie `grep chicken animals.txt` finds all occurances of 'chicken' in animals.txt, whether chicken is part of a word or whole.
- `-w` - the word option, matches full words only, ie `grep -w 'mail' myfile.txt` will find mail but ignore email, mailed, etc.
- `-r` is the recursive option - `grep -ri 'chicken'` searches the current dir and all subs (case-insentive, which is what the `-i` is)
- `grep -ri parm[ae]san' meals/food` searches the dir for two possible spellings of parmesan (with an a and with an e in the middle)
- `-c` returns the count of matches, not the matches themselves
- `-n` returns the line number that the result is on

#### grep and regex

- Any single character (.): `grep 'p....' <file or path>` returns p + any four chars, b/c the dot represents any single character
- Start of a line (^): `grep '^I' <file>` returns lines that begin with I
- End of a line ($): `grep ')$' <file>` returns lines that end with )
- Also: `[abc]` = characters in a set; `[^abc]` characters not in a set; `[A-Z]` chars in a range

To use extended regex stuff, such as `?` (match 0 or one occurances). `{}` (used to set the number of occurances), we have to use the extended version of grep OR escape these special characters with '\'

Extended grep can be used by typing `egrep` or using the `-E` option

`[aeiou]{3}` means match three vowels in a row (but only using extended grep), and `[aeiou]{2,4} means anything from two to four vowels in a row

#### Piping to grep

- `man grep | grep 'count' -i` returns the word 'count' from the grep man page
- `ls -l | grep 'Aug'` returns files with an Aug date

### Permissions

- `drwxr-xr-x`- Execute on a dir is required to open it

- `chmod u+x myfile.txt` - Who? (u, g, o [user, group, others] or a for all), add or remove? (+, -, =), which permission? (r, w, x). The example gives the user executable permission
- `chmod a=rx myFile.txt` gives all the permissions to read and execute

#### Octal notation

**Octal - Binary - File Mode**

0 000 ---

1 001 --x

2 010 -w-

3 011 -wx

4 100 r--

5 101 r-x

6 110 rw-

7 111 rwx
