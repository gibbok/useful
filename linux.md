# Linux

## General

### Grep from npm run

```shell
npm run XYZ &> tempfile && grep JYZ tempfile
```

### Netcatl isten to a specific port

```shell
nc -l 3000
```

### Grep and show 2 lines before and after the result

```shell
grep -C2
```

### Repeat a command every one second

```shell
while sleep 1; do echo "Hi"; done
```

### Pipe to file and at the same time show on screen

```shell
ls -al | tee file.txt
```

### Find list of open ports and associated processes

```shell
netstat -anvp tcp | awk 'NR<3 || /LISTEN/'
```

### List all process as: a = show processes for all users; u = display the process's user/owner; x = also show processes not attached to a terminal

```shell
ps aux
```

### Kill a process by pid

```shell
kill -9 41403
```

### Lookup signal process based on name X and kill

```shell
pkill X
```

### Check which video card is being used

```shell
prime-select query
```

### Use GIO

Current versions of Ubuntu Linux (including 20.04) contain a highly-developed version of the Gnome desktop manager. Part of that system is the included gio command, which provides control of the gnome virtual file system (gvfs), which allows non-administrative users to connect and access network file systems.

```shell
gio tree
gio trash
```

## Docker

### Inspect content for a container

```shell
docker exec -t -i mycontainer /bin/bash
```

## Resources

[Bash Builtin Commands](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html)
