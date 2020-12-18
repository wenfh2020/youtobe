# Debug the async events of redis

Multiplexing's workflow.

---

## 1. server

redis-server

---

## 2. client

redis-cli

---

## 3. break point

* listen

```c
// anet.c
static int anetListen(char *err, int s, struct sockaddr *sa, socklen_t len, int backlog) {...}
```

* create event loop

```c
// ae.c
aeEventLoop *aeCreateEventLoop(int setsize) {...}
```

* client connect (new fd), create file event

```c
// ae.c
int aeCreateFileEvent(aeEventLoop *eventLoop, int fd, int mask,
    aeFileProc *proc, void *clientData) {...}
```

* close fd, delete file event

```c
// ae.c
void aeDeleteFileEvent(aeEventLoop *eventLoop, int fd, int mask) {...}
```

* process events

```c
// ae.c
int aeProcessEvents(aeEventLoop *eventLoop, int flags) {...}
```
