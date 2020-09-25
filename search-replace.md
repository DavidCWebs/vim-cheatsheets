# Search & Replace in Vim
Search replace in Vim takes the form:

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
Separators
----------
The '/' symbol has been used as a separator in the preceding examples. Most non-alphanumeric characters can be used so long as the separator is applied consistently. Note that `\`, `"` or `|` should not be used.

Quantifiers
-----------
- `*`: Matches zero or more of the preceding characters, ranges or metacharacters. `.*` matches everything, including empty lines.
- `\+`: Matches one or more of the preceding characters.
- `\=`: Matches zero or one of the preceding characters.
- `\{n,m}`: Matches from n to m of the preceding characters.
- `{n}`: Matches exactly n times of the preceding characters.
- `{,m}`: Matches at most m (from 0 to m) of the preceding characters.
- `{n,}`: Matches at least n of the preceding characters.


Example: Non Greedy Matching
----------------------------
For the sentence:

`Qui quis vi autet dicta atque est sunt "aaa" voluptate. "Alias" officia`

The following command replaces the first quoted string only.
```vim
:13s/".\{-}"/"xxx"/
```
Result:

`Qui quis vi autet dicta atque est sunt "xxx" voluptate. "Alias" officia`

`\{-}` Matches 0 or more of the preceding atom - in this case, any character. So "" and "abc" are both replaced with "xxx".


Pattern Capture
----------------
TODO
 
Example: Clean up Whitespace
----------------------------
Convert two or more space characters to a tab character.

```vim
:%s/\s\s\+/\t/g
```

Example: Remove Leading Whitespace
----------------------------------
```vim
:%s/^\s\+//g

# No error displayed if no leading whitespace found
:%s/^\s\+//e
```

Example: Remove Trailing Whitespace
-----------------------------------
```vim
:%s/\s\+$//e
```

Example: Capture Data and Process Before Replacement
----------------------------------------------------
This example converts values in `px` units to `rem`. It uses the `#` character as a separator:

```vim
:%s#\(\d\+\)px#\=printf("%.02f", (submatch(1) / 16.0))."rem"#g

# This could be simplified with the `\v` very-magic specifier:
:%s#\v(\d+)px#\=printf("%.02f", (submatch(1) / 16.0))."rem"#g
```

- It searches the entire document and captures digits that precede the string "px", and matches the digits and the "px".
- It then writes back the captured data using `printf()`.
- Within the `printf()` function, the captured data is processed (converted from px units to rem).
- The string "rem" is added to the processed data

The `printf()` format specifier can be used to set precision - in this case, 2 significant figures after the decimal: `"%.02f"`.

The second example with the "very magic" setting means you can use unescaped parentheses to capture the group, and you don't need to escape the `+` symbol (which denotes one or more of the preceding characters).

[See this thread][2] for more.

Insert Characters at a Particular Column
----------------------------------------

* Move cursor to the right of the uppermost character - where you want to start insertion.
* Enter *visual block mode*: `Ctrl+v`
* Select the column using j & k keys (or arrow keys)
* Enter *insert mode*: `Shift + i`
* Type the text to insert, which will only display on the first line
* Exit insert, `Ctrl+{` or `esc` twice

Replace All Underlined H2 Styles with H3
----------------------------------------
Useful when converting h2 headings to h3 in markdown documents.

Search in the range for a newline followed by any number of '-' characters, in turn followed by a newline, capturing the group up to the first newline.
Replace with the capture group with "### " prepended and a single newline appended.

```vim
:%s/\(.*\)\n-\+\n/### \1\r/g
```


References
----------
* [Really good Vim Regex article][1]

[1]: http://www.vimregex.com/
[2]: https://www.reddit.com/r/vim/comments/feeaub/so_i_needed_to_replace_all_px_to_rems_in_a_css/
