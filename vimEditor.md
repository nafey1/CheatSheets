## Vim Cheatsheet

Loosely based on [Daniel Gryniewicz](https://www.fprintf.net/vimCheatSheet.html)'s version.

Vim is a modal text editor. It has three main modes: 

*Normal mode* (a.k.a Command mode) is the default mode. Vim starts in this mode.  
*Insert mode* is for entering text.  
*Visaul mode* is for selecting text.  

[Normal mode] indicates that you must be in normal mode first before a set of commands will work.


### Save and Exit [Normal mode]
```bash
:w # save changes
:wq # quit (save changes)
:q! # quit (discard changes)
<Shift>+z+z # save file and quit
```


### Cursor movement [Normal mode]

***Note***:  Prefix cursor command with a number to repeat it. For example, 4j moves down 4 lines; 5w jumps to 5th word

```bash
h # move left
j # move down
k # move up
l # move down
w # jump to beginning of next word (includes punctuation marks)
W # jump to beginning of next word (ignores/skips punctuations)
e # jump to end of next word (includes punctuation marks)
E # jump to end of next word (ignores/skips punctuations)
b # jump to beginning of previous word (includes punctuation marks)
B # jump to begining of previous word (ignores/skips punctuations)
0 # (zero) jump to beginning of line
^ # jump to first non-whitespace character of line
$ # jump to end of line
% # jump to matching bracket i.e. '(' ')' or '{' '}' or '[' ']'
gg # jump to beginning of first line of file. prefix with number to jump to specific line - 5gg jumps to line 5
G # jump to beginning of last line of file. prefix with number to jump to specific line - 5G jumps to line 5
<Ctrl>+f # Move down (forward) one page
<Ctrl>+b # Move up (back) one page
<Ctrl>+d # Move down half a screen
<Ctrl>+u # Move up half a screen
```


### Insert mode [Normal mode]
```bash
i # enter insert mode and insert before cursor
3ifoo # insert 'foo' three times
I # enter insert mode and insert at beginning of line
a # append after cursor
A # append to end of line
o # append to new line below current line (no need to press <Return>)
O # append to new line above current line
ea # append to end of word
GA # jumps and appends to the last line of file
<Esc> # exit insert mode (goes back to Normal mode)
```


### Find, Replace and Substitute [Normal mode]

***Substitute syntax***: **:[range]s/search/replace**

```bash
f # find next character. fw finds next 'w' character
F # find previous character. Fw finds previous 'w' character
r # replace a single character under cursor. rw replaces any character under cursor with 'w'
/[pattern] # search entire file for next match of pattern from current cursor position. For example, /foo will search for next 'foo' pattern in whole file
?[pattern] # search entire file for previous match of pattern from current cursor position. For example, ?foo will search for previous 'foo' pattern in whole file
n # move to next match from either /[pattern] or ?[pattern] match
N # move to previous match from either /[pattern] or ?[pattern] match
:s/foo/bar # find first instance of 'foo' and replace  with 'bar'. Only search current line (because no range is specified)
:8,10s/foo/bar/g # find all instances of 'foo' in lines 8 to 10 and replace with 'bar'. g - matches all instances in range (8,10)
:%s/foo/bar/g # find all instances of 'foo' and replace  with 'bar'. g - matches all instances in range (range is the entire file denoted by %)
:%s/foo/bar/gc # find all instances of 'foo' and replace  with 'bar'. gc - matches all instances (g) in file (%) and asks for confirmation before replacing (c)
```


### Editing [Normal mode]
```bash
J # append line below to current line
cc # replace (change) current line i.e. deletes line under cursor and replace with new text
cw # replace (change) current word i.e. delete word under cursor and replace with new text
C # replace (change) rest of line after cursor
c$ # replace (change) till end of line
s # delete character under cursor and substitute with new character (or text)
S # same as cc (synonym)
xp # transpose character (delete and paste technically). For example, if 'H' under cursor then: 'Hello' -> 'eHllo' -> 'elHlo'
u # undo
<Ctrl>+r # redo
. # repeat last command
```


### Visual mode [Normal mode]
```bash
v # enter visual mode for marking text
<Ctrl>+v # enter visual block mode for marking a block of text
<Ctrl>+q # same as <Ctrl>+v. Use this if above command does not work, for example, on Windows OS
<Shift>+v # enter visual line mode. automatically marks entire line under cursor. move cursor up or down to mark subsequent lines
<Esc> # exit visual mode (goes back to Normal mode)
```


### Selecting Text [Visual mode]

***Note***: Use movement commands to select text

```bash
o # move cursor to beginning of selected area. For example in text 'Hello World', if [Hello] is marked and cursor is on character 'o', jump to 'H'
O # move cursor to opposite corner of selected block
aw # select current word
ab # select text including parantheses e.g. ->(foo)<-
aB # select text including braces e.g. ->{bar}<-
ib # select text between paranthese e.g. (->foo<-)
iB # select text between braces e.g. {->bar<-}
```


### After Selecting Text [Visual mode]
```bash
> # shift selected text right
< # shift selected text left
y # copy (yank) selected text
d # delete selected text
~ # switch case of selected text
c # change selected text (i.e. replace with something else). Press <Esc> after entering new text
```


### Cut/Copy and Paste [Normal mode]

***Note***:  Prefix cursor command with a number to repeat it.

```bash
yy # copy (yank) current line
2yy # copy (yank) 2 lines (current line and line below)
yw # copy (yank) word
y2w # copy (yank) two words
y$ # copy (yank) from current cursor position till the end of line
p # paste (put) after cursor
P # paste (put) before cursor
dd # delete (cut) current line
dw # delete (cut) current word
d2w # delete (cut) two words
x # delete (cut) character under cursor
X # delete (cut) character left of cursor (like backspace)
```

*Tips*: 
  - **gg"&ast;yG** will copy an entire file!
  - To paste clipboard contents, switch to insert mode and enter:
    ```bash
    <Ctrl>+<Shift>+v
    ```


### Working with Multiple Files [Normal mode]

***Note***: Each file gets its own buffer

```bash
:e [filename] # edit file in a new buffer. If file doesn't exist, creates new file.
:bnext (or :bn) # go to next buffer
:bprev (or :bp) # go to previous buffer
:bd # delete current buffer (closes file). Only works if you save changes. Throws error if you don't!
:bd! # delete current buffer (closes file). Overrides above behaviour on saving changes!
:sp [filename] # split current window and edit file in a new buffer in the new window. If file doesn't exist, creates new file.
<Ctrl>+w,s # Split current window horizontally
<Ctrl>+w,v # Split current window vertically
<Ctrl>+w,w # Switch to next window
<Ctrl>+w,q # close current window
```

### Other Vim Cheatsheets
[Cheatsheet 1](https://web.archive.org/web/20161221161539/http://bullium.com/support/vim.html)
