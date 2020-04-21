# redis-benchmark

Stress test redis 6.0 multi-threaded processing network i/o

---

## obj

* redis-server
* redis-benchmark

---

## download redis 6.0

```shell
cd ~
cd src/other
wget https://codeload.github.com/antirez/redis/zip/6.0
tar zxf 6.0
```

---

## build

```shell
cd redis-6.0/src
make clean; make
```

---

## script

```shell
cd ..
wget https://raw.githubusercontent.com/wenfh2020/shell/master/redis/benchmark.sh
chmod +x benchmark.sh
```

---

## test

* copy config

```shell
cp redis.conf redis.conf.ths
cp redis.conf redis.conf.unths
vim redis.conf.ths
```

* update redis.conf.ths

```shell
# redis.conf.ths
io-threads 4
io-threads-do-reads yes
```

* command

```shell
ulimit -n 16384
./benchmark.sh
```

* result

```shell
#./benchmark.sh

------------------------------------
-benchmark_packs
---------
-10
-threads
SET: 159897.66 requests per second
GET: 137797.98 requests per second

-single
SET: 166805.67 requests per second
GET: 163505.55 requests per second

---------
-500
-threads
SET: 140686.55 requests per second
GET: 135648.39 requests per second

-single
SET: 81612.66 requests per second
GET: 116618.08 requests per second
...
```
