# Search & Replace in Vim
Search and replace in Vim takes the form:

```vim
:range s[ubstitute]/pattern/replacement/cgiI
```
For each line in `range` replace a match of `pattern` with `replacement`. The final flag denotes how the match is carried out:

- `c`: Confirm each substitution.
- `g`: Replace all occurrences of pattern in the line (without g, only the first instance is replaced).
- `i`: Ignore case for the pattern.
- `I`: Don't ignore case for the pattern.


Select lines to search & replace:

Find all instances of "original" in lines 10 - 20 inclusive and replace with the string "replacement":
```vim
:10,20s/original/replacement/g
```
Select the entire document with `:%`:

Find all instances of "original" in the entire document and replace with "replacement":
```vim
:%s/original/replacement/g
```
Anchors
-------
If you want to replace all instances of a given word, but not when it constitutes a substring of another word, you can use __word boundary symbols__: `\<` and `\>`.

Replace all occurrences of "vi" with "vim" only when "vi" is a whole word:

```vim
:%s/\<vi\>/vim/g
```
You can target beginning and end of lines:

```vim
# Replace "vi" when it is at a line beginning
:%s/^vi/VIM/g

# Replace "lorem." with "LOREM!" when it is at the end of a line:
:%s/lorem.$/LOREM!/g

# Match lines where "lorem" is the only word:
:%s/^Lorem$/LOREM/g
```

Pattern Capture
----------------
 

