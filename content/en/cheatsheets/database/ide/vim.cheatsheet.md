---
title: vim.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Cursor movement
#-#

Command    Description
-------    -----------
h or ←     move cursor left
j or ↓     move cursor down
k or →     move cursor up
l or ↑     move cursor right
w          jump forwards to the start of a word
W          jump forwards to the start of a word (words can contain punctuation)
e          jump forwards to the end of a word
E          jump forwards to the end of a word (words can contain punctuation)
b          jump backwards to the start of a word
B          jump backwards to the start of a word (words can contain punctuation)
0          jump to the start of the line
^          jump to the first non-blank character of the line
$          jump to the end of the line
G          go to the last line of the document
5G         go to line 5

Tip: Prefix a cursor movement command with a number to repeat it.
     For example, 4j moves down 4 lines.



#-#
#-# Insert mode - inserting/appending text
#-#

Command    Description
-------    -----------
i          insert before the cursor
I          insert at the beginning of the line
a          insert (append) after the cursor
A          insert (append) at the end of the line
o          append (open) a new line below the current line
O          append (open) a new line above the current line
ea         insert (append) at the end of the word
Esc        exit insert mode



#-#
#-# Editing
#-#

Command    Description
-------    -----------
r          replace a single character
J          join line below to the current one
cc         change (replace) entire line
cw         change (replace) to the end of the word
c$         change (replace) to the end of the line
s          delete character and substitute text
S          delete line and substitute text (same as cc)
xp         transpose two letters (delete and paste)
u          undo
Ctrl + r   redo
.          repeat last command



#-#
#-# Marking text (visual mode)
#-#

Command    Description
-------    -----------
v          start visual mode, mark lines, then do a command (like y-yank)
V          start linewise visual mode
o          move to other end of marked area
Ctrl + v   start visual block mode
O          move to other corner of block
aw         mark a word
ab         a block with ()
aB         a block with {}
ib         inner block with ()
iB         inner block with {}
Esc        exit visual mode



#-#
#-# Visual commands
#-#

Command    Description
-------    -----------
>          shift text right
<          shift text left
y          yank (copy) marked text
d          delete marked text
~          switch case



#-#
#-# Cut and paste
#-#

Command    Description
-------    -----------
yy         yank (copy) a line
2yy        yank (copy) 2 lines
yw         yank (copy) word
y$         yank (copy) to end of line
p          put (paste) the clipboard after cursor
P          put (paste) before cursor
dd         delete (cut) a line
2dd        delete (cut) 2 lines
dw         delete (cut) word
D          delete (cut) to the end of the line
d$         delete (cut) to the end of the line
x          delete (cut) character



#-#
#-# Search and replace
#-#

Command           Description
-------           -----------
/pattern          search for pattern
?pattern          search backward for pattern
n                 repeat search in same direction
N                 repeat search in opposite direction
:%s/old/new/g     replace all old with new throughout file
:%s/old/new/gc    replace all old with new throughout file with confirmations



#-#
#-# Working with multiple files
#-#

Command          Description
-------          -----------
:e filename      edit a file in a new buffer
:bnext or :bn    go to the next buffer
:bprev or :bp    go to the previous buffer
:bd              delete a buffer (close a file)
:sp filename     open a file in a new buffer and split window
:vsp filename    open a file in a new buffer and vertically split window
Ctrl + w s       split window
Ctrl + w w       switch windows
Ctrl + w q       quit a window
Ctrl + w v       split window vertically
Ctrl + w h       move cursor to the left window (vertical split)
Ctrl + w l       move cursor to the right window (vertical split)
Ctrl + w j       move cursor to the window below (horizontal split)
Ctrl + w k       move cursor to the window above (horizontal split)



#-#
#-# Tabs
#-#

Command                      Description
-------                      -----------
:tabnew or :tabn filename    open a file in a new tab
Ctrl + wT                    move the current split window into its own tab
gt or :tabnext or :tabn      move to the next tab
gT or :tabprev or :tabp      move to the previous tab
#gt                          move to tab number #
:tabmove #                   move current tab to the #th position (indexed from 0)
:tabclose or :tabc           close the current tab and all its windows
:tabonly or :tabo            close all tabs except for the current one



#-#
#-# Saving and Exiting
#-#

Command        Description
-------        -----------
:w             write (save) the current file, but don't exit
:w filename    write (save) as filename, but don't exit
:wq            write (save) and quit
:q             quit (fails if there are unsaved changes)
:q!            quit and throw away unsaved changes



