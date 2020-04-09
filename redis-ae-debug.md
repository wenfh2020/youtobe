# Debug the Multiplexing events of redis

Debug the Multiplexing's workflow.

---

## server

redis-server

---

## client

redis-cli

---

## break point

* listen

```c
static int anetListen(char *err, int s, struct sockaddr *sa, socklen_t len, int backlog) {...}
```

* create event loop

```c
aeEventLoop *aeCreateEventLoop(int setsize) {...}
```

* client connect (new fd), create file event

```c
int aeCreateFileEvent(aeEventLoop *eventLoop, int fd, int mask,
    aeFileProc *proc, void *clientData) {...}
```

* close fd, delete file event

```c
void aeDeleteFileEvent(aeEventLoop *eventLoop, int fd, int mask) {...}
```

* process events

```c
int aeProcessEvents(aeEventLoop *eventLoop, int flags) {...}
```
