Copy Paste
==========

Copy Current File Path to Clipboard
-----------------------------------

Access the full path using `expand("%:p")`. 

Access the file name: `expand("%")`.

Add to a specific register:

```vim
# To clipboard
:set @+ = expand("%:p")

# To unnamed register, use `p` to paste:
:set @" = expand("%:p")
```

Yank the current file path in one window and put into the command buffer in another window:

```vim
# Yank path to main clipboard buffer (not system clipboard)
:let @" = expand("%:p")

# Open a new window
:sp

# In other window type:
:e Ctrl+R"
```

Paste Contents of File
----------------------

```vim
:r/path/to/file
```

