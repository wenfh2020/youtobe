# Redis debug

## 1. Prepare

- install gdb

- install vscode

---

## 2. Download

Download [redis source](http://download.redis.io/releases/).

```shell
cd ~/src/other
wget http://download.redis.io/releases/redis-3.2.8.tar.gz
tar zxf redis-3.2.8.tar.gz
```

---

## 3. Update Makefile

Modify Makefile add -O0 to build redis-server project

```shell
cd redis-3.2.8
vim src/Makefile
```

```shell
# OPTIMIZATION?=-O2
OPTIMIZATION?=-O0
# REDIS_LD=$(QUIET_LINK)$(CC) $(FINAL_LDFLAGS)
REDIS_LD=$(QUIET_LINK)$(CC) $(FINAL_LDFLAGS) $(OPTIMIZATION)
```

---

## 4. Build

```shell
make clean; make
ls -l src/redis-server
```

---

## 5. Test

### 5.1. server

```shell
./src/redis-server redis.conf
```

---

### 5.2. client

```shell
./src/redis-cli
set k123456 v123456
```

---

## 6. Debug by gdb

### 6.1. Gdb debug command

```shell
sudo gdb --args ./src/redis-server redis.conf
r
ctrl + c
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

---

## 7. VScode Gdb Debug

### 7.1. open redis project

```shell
sudo code --user-data-dir="~/.vscode-root" .
```

---

### 7.2. Debug by vscode

press F5 to begin the debuging project....

---

### 7.3. Add config

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

```json
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

---

### 7.4. Clear

```shell
ps -ef | grep -i redis | grep -v grep | awk '{print $3}' | xargs sudo kill -9
ps -ef | grep -i vscode | grep -v grep | awk '{print $3}' | xargs sudo kill -9
```
