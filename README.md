# FastD Web 基础压力测试 (仅个人经验,欢迎指点)

##### 单核 CPU Pentium(R) Dual-Core  CPU      E5700  @ 3.00GHz
##### 内存 1922160 KB

#### 没开启 OPCache

```
Server Software:
Server Hostname:        127.0.0.1
Server Port:            8088

Document Path:          /
Document Length:        1049 bytes

Concurrency Level:      20
Time taken for tests:   59.914 seconds
Complete requests:      2000
Failed requests:        0
Write errors:           0
Total transferred:      2416000 bytes



HTML transferred:       2098000 bytes
Requests per second:    33.38 [#/sec] (mean)
Time per request:       599.140 [ms] (mean)
Time per request:       29.957 [ms] (mean, across all concurrent requests)
Transfer rate:          39.38 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       1
Processing:    73  597  75.8    567    1182
Waiting:       69  597  75.8    567    1182
Total:         74  597  75.8    567    1182

Percentage of the requests served within a certain time (ms)
  50%    567
  66%    606
  75%    634
  80%    648
  90%    694
  95%    760
  98%    805
  99%    838
 100%   1182 (longest request)
```

#### 开启OPCache

```
Server Software:
Server Hostname:        127.0.0.1
Server Port:            8088

Document Path:          /
Document Length:        1049 bytes

Concurrency Level:      20
Time taken for tests:   11.477 seconds
Complete requests:      2000
Failed requests:        0
Write errors:           0
Total transferred:      2416000 bytes
HTML transferred:       2098000 bytes
Requests per second:    174.27 [#/sec] (mean)
Time per request:       114.766 [ms] (mean)
Time per request:       5.738 [ms] (mean, across all concurrent requests)
Transfer rate:          205.58 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       1
Processing:    33  113  38.0    100     321
Waiting:       33  113  38.1    100     321
Total:         33  113  38.1    100     321

Percentage of the requests served within a certain time (ms)
  50%    100
  66%    115
  75%    124
  80%    132
  90%    159
  95%    202
  98%    237
  99%    252
 100%    321 (longest request)
```

开启 OPCache 扩展后,PHP性能上会大致有5倍的提升。

##### CPU model name	: Pentium(R) Dual-Core  CPU      E5800  @ 3.20GHz
          model name	: Pentium(R) Dual-Core  CPU      E5800  @ 3.20GHz
##### 内存 5994928 KB

#### 没开启 OPCache

```
Server Software:
Server Hostname:        127.0.0.1
Server Port:            8088

Document Path:          /
Document Length:        1049 bytes

Concurrency Level:      20
Time taken for tests:   3.273 seconds
Complete requests:      193
Failed requests:        0
Write errors:           0
Total transferred:      233144 bytes
HTML transferred:       202457 bytes
Requests per second:    58.96 [#/sec] (mean)
Time per request:       339.189 [ms] (mean)
Time per request:       16.959 [ms] (mean, across all concurrent requests)
Transfer rate:          69.56 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.9      0       3
Processing:    28  320  39.5    322     424
Waiting:       26  320  39.5    322     424
Total:         29  320  39.5    322     424

Percentage of the requests served within a certain time (ms)
  50%    322
  66%    335
  75%    343
  80%    348
  90%    363
  95%    379
  98%    397
  99%    405
 100%    424 (longest request)
```

#### 开启OPCache

```
Server Software:
Server Hostname:        127.0.0.1
Server Port:            8088

Document Path:          /
Document Length:        1049 bytes

Concurrency Level:      20
Time taken for tests:   6.341 seconds
Complete requests:      2000
Failed requests:        0
Write errors:           0
Total transferred:      2416000 bytes
HTML transferred:       2098000 bytes
Requests per second:    315.43 [#/sec] (mean)
Time per request:       63.406 [ms] (mean)
Time per request:       3.170 [ms] (mean, across all concurrent requests)
Transfer rate:          372.11 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   2.1      0      55
Processing:     5   63  29.2     60     245
Waiting:        5   62  29.3     59     245
Total:          5   63  29.4     60     245

Percentage of the requests served within a certain time (ms)
  50%     60
  66%     71
  75%     79
  80%     84
  90%     97
  95%    112
  98%    138
  99%    159
 100%    245 (longest request)
```

根据第二台机确认, 大致有5倍性能提升。

上述 CPU 使用率大致波动 75% ~ 80% 中, 负载压力较高

##### Nginx 负载均衡(LVS)测试

```
Server Software:
Server Hostname:        127.0.0.1
Server Port:            8090

Document Path:          /
Document Length:        1049 bytes

Concurrency Level:      200
Time taken for tests:   4.861 seconds
Complete requests:      2000
Failed requests:        0
Write errors:           0
Total transferred:      2420000 bytes
HTML transferred:       2098000 bytes
Requests per second:    411.44 [#/sec] (mean)
Time per request:       486.101 [ms] (mean)
Time per request:       2.431 [ms] (mean, across all concurrent requests)
Transfer rate:          486.17 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    1   2.7      0      12
Processing:     4  458 392.7    362    1210
Waiting:        4  458 392.7    362    1210
Total:          4  459 392.6    368    1210

Percentage of the requests served within a certain time (ms)
  50%    368
  66%    789
  75%    863
  80%    910
  90%    976
  95%   1018
  98%   1078
  99%   1118
 100%   1210 (longest request)
```

使用负载之后, 两台服务器大致压力

10.1.2.241 CPU:  65% 减少 15% 压力
10.1.2.242 CPU:  48% ~ 50% 减少 30% 压力

以上均为没有配置参数优化。

## 待续
