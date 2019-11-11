# Prepend to a Line in Vim

Example: insert "int " before the first character in lines 141 - 144 inclusive:

```vim
:141,144s/^\s*/&int /g
```

Before & After:

```c
// Before:

	upperBound = (y + 1 >= b->height) ? b->height : y + 2; // Exclusive
	lowerBound = (y - 1 <= 0) ? 0 : y - 1; // Inclusive
	lBound = (x - 1 <= 0) ? 0 : x - 1; // Inclusive
	rBound = (x + 1 >= b->width) ? b->width : x + 1; // Exclusive

// After:
	int upperBound = (y + 1 >= b->height) ? b->height : y + 2; // Exclusive
	int lowerBound = (y - 1 <= 0) ? 0 : y - 1; // Inclusive
	int lBound = (x - 1 <= 0) ? 0 : x - 1; // Inclusive
	int rBound = (x + 1 >= b->width) ? b->width : x + 1; // Exclusive

```
