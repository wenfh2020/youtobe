### Prepare

- install gdb

- install vscode



## Download

Download redis source.

http://download.redis.io/releases/

```
cd ~/src/other
wget http://download.redis.io/releases/redis-3.2.8.tar.gz
tar zxf redis-3.2.8.tar.gz
```



## Update Makefile

modify Makefile add -O0 to build redis-server project

```
cd redis-3.2.8
vim src/Makefile
```

```
# OPTIMIZATION?=-O2
OPTIMIZATION?=-O0
# REDIS_LD=$(QUIET_LINK)$(CC) $(FINAL_LDFLAGS)
REDIS_LD=$(QUIET_LINK)$(CC) $(FINAL_LDFLAGS) $(OPTIMIZATION)
```

## Build

```shell
make clean; make
ls -l src/redis-server
```



## Test

### server

```
./src/redis-server redis.conf
```

### client

```
./src/redis-cli
set k123456 v123456
```

### 

## Debug by gdb

### Gdb debug command

```
sudo gdb --args ./src/redis-server redis.conf
r
b dict.c:dictAdd
c
focus
info win
fs cmd
bt
f 11
f 10
s
n
p key
p (unsigned char*)key
n
quit
```





## VScode Gdb Debug

### open redis project

```shell
sudo code --user-data-dir="~/.vscode-root" .
```



### Debug by vscode

press F5 to begin the debuging project....



### Add config

- launch.json

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gcc build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/src/redis-server",
            "args": [
                "redis.conf"
            ],
            "stopAtEntry": true,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "preLaunchTask": "shell"
        }
    ]
}
```

- tasks.json

```shell
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "shell",
            "type": "shell",
            "command": "/usr/bin/make"
        }
    ]
}
```



### Clear

```
ps -ef | grep -i redis | grep -v grep | awk '{print $3}' | xargs sudo kill -9
ps -ef | grep -i vscode | grep -v grep | awk '{print $3}' | xargs sudo kill -9
```

