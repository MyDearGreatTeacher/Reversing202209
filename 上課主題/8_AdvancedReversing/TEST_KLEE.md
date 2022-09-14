# 

## 使用dockr執行 klee
- [Practical Symbolic Execution and SATisfiability Module Theories (SMT) 101(2019)](https://www.gushiciku.cn/pl/2n7j/zh-tw)
```
$ docker pull klee/klee
$ docker run -ti --name=my_klee_container --ulimit='stack=-1:-1' klee/klee
klee@02ca010455db:~$
```
### 求解線性方程式 Linear equation with 3 variables
```
x - 2y + 3z = 7
2x + y + z = 4
-3x + 2y - 2z = -10
```
```c
#include <assert.h>
#include "./klee_src/include/klee/klee.h"

int main(int argc, char* argv[]) 
{
  int x, y, z;

  klee_make_symbolic(&x, sizeof x, "x"); 
  klee_make_symbolic(&y, sizeof y, "y"); 
  klee_make_symbolic(&z, sizeof z, "z");

  if (x - 2 * y + 3 * z != 7) return 0;
  if (2 * x + y + z != 4) return 0;
  if (-3 * x + 2 * y - 2 * z != -10) return 0;

  klee_assert(0);
}
```
```c
$ clang -emit-llvm -g -c equation.c
$ klee equation.bc
KLEE: output directory is "/home/klee/klee-out-2"
KLEE: Using STP solver backend
KLEE: ERROR: /home/klee/equation.c:16: ASSERTION FAIL: 0
KLEE: NOTE: now ignoring this error at this location

KLEE: done: total instructions = 55
KLEE: done: completed paths = 4
KLEE: done: generated tests = 4
$ ls klee-last | grep err
test000003.assert.err
$ ktest-tool --write-ints klee-last/test000003.ktest
ktest file : 'klee-last/test000003.ktest'
args       : ['equation.bc']
num objects: 3
object    0: name: b'x'
object    0: size: 4
object    0: data: 2
object    1: name: b'y'
object    1: size: 4
object    1: data: -1
object    2: name: b'z'
object    2: size: 4
object    2: data: 1
```

## youtube頻道
- [Introduction to symbolic execution with KLEE(2020)](https://www.youtube.com/watch?v=z6bsk-lsk1Q)
- [Introduction to symbolic execution with KLEE (part 2) - running six examples of diverse small C apps](https://www.youtube.com/watch?v=BDvNDw2jsSs)
- [KLEE Workshop 2021](https://www.youtube.com/playlist?list=PLGuCE1-pfUlU5sGwZoTPMUHhUY1sAHsnG)

- [LazyKLEE:Lazy python wrapper of KLEE for solving CTF challenges](https://github.com/L4ys/LazyKLEE)
- [KLEE-CTF](https://hackmd.io/@Lays/SkKL68GIe?type=view)
