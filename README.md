Vim Cheatsheets
===============

Looping
-------

Output a numbered list, with a concatenated '. ', ranging from 1 to 50:

```
:for i in range (1,5) | put = i.'. '| endfor

# Output:
1. 
2. 
3. 
4. 
5. 
```

Output some local network addresses:

```
:for i in range(1,5) | put ='192.168.0.'.i | endfor

# Output:
192.168.0.1
192.168.0.2
192.168.0.3
192.168.0.4
192.168.0.5
```
