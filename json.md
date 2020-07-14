#JSON Helpers

Format a document as JSON:

```vim
:%!python -m json.tool
```

Define a Custom Command
-----------------------
Add to `~/.vimrc` config:

```vim
com! Jsonify %!python -m json.tool
```

Usage - in normal mode:

```vim
:Jsonify
```

Sourced from [this article][1].

[1]: https://confluence.jaytaala.com/display/TKB/Format+text+as+JSON+in+vim 
