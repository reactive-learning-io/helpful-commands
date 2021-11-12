# Linux Commands

### Start JVM in debug mode
`-Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n`

### Get all processes
```
rem
ps -elf | grep java
ps ax | grep anlayze-
kill -9 pid
```

### find java process ids only
`ps -C java -o pid`
	
### To set to all subfolders (recursively) use -R
`sudo chmod 755 /folder -R`
### Give full permission : 
`sudo chmod 777 file.txt`
### Check hidden files
`ls -lart`
### Edit envar file
`vi .bashrc`
### Reopen terminal to auto run .bashrc file
`. ./.bashrc`

### Show process with memory usage
```
ps aux --sort -rss
ps aux --sort -pid
ps aux --sort pid
```

### Clear cache
`sync; echo 1 > /proc/sys/vm/drop_caches;`

### zip all files in a folder
`tar -czf logs_13_june.tar.gz out/`

### Extract file
`tar -xvf filename.tar`

### Delete older files
`find . -type f -mtime +1 -exec rm -rf {} \;`

### find files starting with
`ls -lrt | grep analyze`
