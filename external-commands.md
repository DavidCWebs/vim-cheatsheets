External Commands in Vim
========================

Insert Files
------------
* The `:r[file]` reads.
* The `:r!{cmd}` Executes {cmd} and inserts stdout from this below the cursor. 

### Insert Text From File
Insert entire file, normal mode:

```vim
:r /path/to/file
```

### Insert specified lines from an external file

```vim
:r! sed -n '3,4 p' < foo.txt
```

### Insert from webpage

```vim
:r! wget -qO- https://raw.githubusercontent.com/DavidCWebs/generate-randomness/master/README.md
```

### Insert working directory
```vim
:r! pwd
```

### Insert date (shell)
```
:r! date
```
Inserts: `Sun Jun 30 16:09:27 IST 2019`

### Insert date (internal)
```vim
:put =strftime('%c')
```
Inserts: `Sun 30 Jun 2019 16:10:54 IST`
