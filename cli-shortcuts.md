### CLEAR THE SCREEN

`clear`
`ctrl-l`

## JUMP TO BEGINNING/END

`ctrl-a`
`ctrl-e`

## WORD AT A TIME

`alt-f` and `alt-b`

## KILL BY LINE

`ctrl-k` - kill from cursor to end of line

## `ctrl-u` - kill from cursor to start of line

## KILL BY WORD

`alt-d` kill to end of current word
`alt-delete` or `ctrl-w` - kill to start of word

## YANK

`ctrl-y` - Yank from kill ring (ie paste, although the kill ring and the sys clipboard are two different things)

## HISTORY

`history | less`
`ctrl-r` enters reverse search of history - so `ctrl-r` then `curl` shows me the most recent curl command, then I can scroll backward through them with more `ctrl-r`

---

ctrl-f and ctrl-b - works like the l/r arrows but keeping hands on home row
ctrl-t - swaps current character with the preceeding one
alt/opt-t - swap words
!3543 (where 3543 is a line number in history) displays the command at that line, ready to run
history lives in ~/.bash_history
