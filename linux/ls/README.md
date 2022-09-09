# ls

## вивести лише директорії:

```
ls -d */
desktop/  iso/   soft/
```

```
ls -lad */
drwxrwxr-x 2 olex olex 4096 чер 22 10:58 desktop/
drwxrwxr-x 2 olex olex 4096 лип 19 12:13 iso/
drwxrwxr-x 5 olex olex 4096 лип 19 01:29 soft/
```

```
ls -l | grep '^d'
drwxrwxr-x 2 olex olex 4096 чер 22 10:58 desktop
drwxrwxr-x 2 olex olex 4096 лип 19 12:13 iso
drwxrwxr-x 5 olex olex 4096 лип 19 01:29 soft
```

!!!
```
echo */
desktop/  iso/   soft/
```
