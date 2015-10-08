## Google C++ Style Guide

继承自 Google C++ Style Guide 的一些风格。

## 消灭幻数

### stdio.h

`EOF`.
文件指针：`stdin`, `stdout` 和 `stderr`.

### stdlib.h

返回值：`EXIT_SUCCESS` 和 `EXIT_FAILURE`.

### unistd.h

标准文件描述符：`STDIN_FILENO`, `STDOUT_FILENO` 和 `STDERR_FILENO`.

## 原子操作

以下分为两列，前者是后者的原子操作，自然以前者为优。

* `O_APPEND` vs `lseek()` 和 `write()`.
* `open(path, O_CREAT | O_EXCL` vs `open()` 和 `creat`.
* `dup2(fd, fd2)` vs `close(fd2); fcntl(fd, F_DUPFD, fd2)`

## 避免缓存区溢出

* `fgets()` vs `gets()`
* `fputs()` vs `puts()`, 虽然这输出函数并不会引起缓存区溢出，但鉴于 `puts()` 会额外添加换行符，又和鸡肋般的 `gets()` 成一对，干脆无视掉它的存在吧。
* `snprintf()` vs `sprintf()`

## 请勿在宏中用表达式

* `getc()`, `putc()`
* `FD_ISSET()`,` FD_CLR()`, `FD_SET()`, `FD_ZERO()`

## 构造内存

* `memset` vs `zero`, 就算用来构造初始值恒为零的 `sockaddr`, [就算就算 UNP 作者更编好后者，前者已经快要被淘汰了](http://stackoverflow.com/a/17097072/1546088)，何况 `memset` 能更灵活地选择所要构造的字节，优先用前者。
* `memcpy` vs `memmove` vs `bcopy`.

## IP 协议无关

* `inet_pton`, `inet_ntop` vs `inet_addr`, `inet_ntoa`, `inet_aton`. 前者与 IP 协议无关，后者限于 IPv4 协议。
* 

## 其它

鉴于 `creat` 只能只写方式打开所创建的文件，于是一律用 `open(path, O_CREAT, mode)` 统一代替。

始终要处理任何函数的任何可能返回值。

必要时，用带符号整型 `ssize_t` 代替无符号整型 `size_t`.

在修改文件描述符标志或文件状态标志，先获取，再修改，最后设置。

写入数据库文件，在 `open()`, 加上 `O_SYNC`. 或用 `fsync()` 强制更新。

不要在宏里用表达式。

文件流「结束」时，要用上 `ferror()` 和 `feof()` 以判断是达到文件结尾还是出错。

标准 I/O 并不比 POSIX I/O 慢，优先用。

声明原理上 `int a[]` 与 `int *a` 等价，然而在可读性上有所区别，用数组就用前者，用指针就用后者。

用同名但首字母大写的函数包裹标准库函数来进行 handle, 不失为一种解决方案。

在 C++ 要留意两个参数为同一个对象时带来的问题，在 C 更是要留意指针是否会重叠。
