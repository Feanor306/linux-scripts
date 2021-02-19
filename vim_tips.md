## UP & DOWN PAGE
CTRL + u = UP 1/2 PAGE
CTRL + d = DOWN 1/2 PAGE
h = left_arrow 
j = up_arrow
k = down_arrow
l = right_arrow
{ = up_one_paragraph
} = down_one_paragraph
$ = go_to_end_of_line
0 = go_to_start_of_line
^ = go_to_start_of_line
w = jump_to_next_word
b = jump_to_previous_word

## EXIT VIM
SHIFT + ZQ (NO SAVE EXIT)
SHIFT + ZZ (SAVE + EXIT)

## CENTER SCREEN ON LINE
zz (CENTER)
zt (MOVE LINE TO TOP)
zb (MOVE LINE TO BOTTOM)

## Insert mode
i   = INSERT MODE (left_side_of_cursor)
a   = INSERT MODE (right_side_of_cursor)
Esc = EXIT INSERT MODE
A = INSERT MODE + MOVE CURSOR AT END OF LINE
I = INSERT MODE + MOVE CURSOR AT START OF LINE
o = Start new paragraph after current one and enter insert mode
O = Start new paragraph before current one and enter insert mode

## Command mode
:   = Enter command mode (from normal mode)
w   = Write file
q   = Quit file
!   = Force command (like :wq!)
x   = Write + quit = :wq
sort = sort all lines in file alphabetically
earlier 5m = GO BACK TO STATE OF FILE 5MIN AGO
later 10m = GO FORWARD IN TIME 10M (state of file)

## Delete
x   = Delete single character

dw  = Delete word until next word (cursor must be at first character)
de  = Delete word until its last char (cursor must be at first character)
db  = Delete previous word (relative to cursor at current word)

daw = Delete word and whitespace around it (cursor can be anywhere inside word)
diw = Delete word, not whitespace (cursor can be anywhere inside word)

dap = Delete whole paragraph (Delete around paragraph)

di( = Delete everything inside () -> cursor must be inside
da( = Delete everything inside (), including () and whitespace around

di" = Delete everything inside "" -> cursor can be anywhere on line

d{  = Delete previous paragraph
d}  = Delete next paragraph
dd  = Delete whole line

d$  = Delete until end of line (from cursor)
D   = Delete until end of line (from cursor)

ci( = same as di( but also enters insert mode after deletion
cw  = same as dw but also enters insert mode after deletion
C   = same as D but also enters insert mode after deletion

## Count
0-9 (any number) + command = repeat command NUM times
3w = move cursor 3 words forward
d5w = delete 5 words
d4{ = delete 4 paragraphs up
4dd = delete 4 lines
5dap = delete 5 paragraphs
5p  = paste 5 times

## UNDO
u   = UNDO last action
U   = UNDO all actions on current line
CTRL + r = REDO last action

## replace
r   = replace mode (requires another char that replaces char at cursor)
rx  = replace current selected char with 'x' or any other char
R   = enter replace mode until ESC is pressed

## % JUMPING
CTRL + g  = Show % location in file
25%   = jump to exactly 25% line in file
G     = jump to end of file
gg    = jump to start of file
''    = jump to last position before last jump

## SEARCH
/xyz  = Search for 'xyz' in file (after cursor position)
?xyz  = Search for 'xyz' in file (before cursor position)
n     = Jump to next search result
N     = Jump to pervious search result
:set ic = Activate case insensitive search
:set hlsearch = Activate highlighting of all occurences of search term
:nohlsearch = Dactivate search highlighting

## Parenthesis
when cursor is at any parenthesis '{([])}'
pressing % will find the other one

## Substitute
**replace all instances of text in current line**
:s/{text_to_replace}/{new_text}/g
:s/oldtext/newtext/g
**replace all instances of text from line to line**
:{start_line},{end_line}s/{text_to_replace}/{new_text}/g
:22,50s/oldtext/newtext/g
**replace all instances of text in whole file**
:%s/{text_to_replace}/{new_text}/g
:%s/oldtext/newtext/g
**replace all instances of text in whole file**
**and ask for confirmation each time**
:%s/{text_to_replace}/{new_text}/gc

## Visual selection
v   = Enter visual selection mode at cursor
V   = Enter visual selection mode and select whole line
Ctrl + v = Visual selection as block
vap = Visual select whole paragraph

## COPY = Yanking 
y   = Copy visual selection
yy  = Copy whole line
yap = Copy whole paragraph

## PASTE
p   = Put/Paste last deleted object

## REPEAT LAST COMMAND
.   = Repeat last command
:norm . = repeat last normal mode sequence

## Spell checker
**activate spell checker**
:setlocal spell! spelllang=en_us
move cursor to spellchecked word 
z=    -> shows spellcheck options for current selection (numbered list)
type number + Enter to replace word
]s    -> jump to next spellcheck word
**turn off spellcheck**
:setlocal spell!