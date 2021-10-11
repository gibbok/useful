# Linux

## General

### Grep from npm run
npm run XYZ &> tempfile && grep JYZ tempfile

### Netcatl isten to a specific port
nc -l 3000

### Grep and show 2 lines before and after the result
grep -C2

### Repeat a command every one second
while sleep 1; do echo "Hi"; done

### Pipe to file and at the same time show on screen
ls -al | tee file.txt

### Find list of open ports and associated processes
netstat -anvp tcp | awk 'NR<3 || /LISTEN/'

### List all process as: a = show processes for all users; u = display the process's user/owner; x = also show processes not attached to a terminal
ps aux

### Kill a process by pid
kill -9 41403

### Lookup signal process based on name X and kill
pkill X

## Docker

### Inspect content for a container
docker exec -t -i mycontainer /bin/bash
