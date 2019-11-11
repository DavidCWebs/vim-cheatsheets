Swap Columns
============

Use `awk` to switch columns.

Switch columns, entire document:

```
:%!awk '{print $2, $1}'
```
Switch columns in the specified line range 10-15 inclusive:

```
:10,15!awk '{print $2, $1}'
```

