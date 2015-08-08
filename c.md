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

## 其它

鉴于 `creat` 只能只写方式打开所创建的文件，于是一律用 `open(path, O_CREAT, mode)` 统一代替。

始终要处理任何函数的任何可能返回值。

必要时，用带符号整型 `ssize_t` 代替无符号整型 `size_t`.

在修改文件描述符标志或文件状态标志，先获取，再修改，最后设置。

写入数据库文件，在 `open()`, 加上 `O_SYNC`. 或用 `fsync()` 强制更新。
