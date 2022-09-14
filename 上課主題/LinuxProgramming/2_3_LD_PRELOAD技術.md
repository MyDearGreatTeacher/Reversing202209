# 2.3_LD_PRELOAD技術
```
使用LD_PRELOAD技術完成簡易型駭客程式注入
```


## 範例
```c
// main.c
#include <stdio.h>
#include <math.h>

int main() {
  double x;
  
  scanf("%lf", &x);
  printf("%f\n", sqrt(x));//呼叫函數開根號
  return 0;
}
```
### 執行看看正確答案
```c
gcc -o main main.c -lm
./main
```
### 撰寫駭客程式
```c
//hook.c
double sqrt(double x) {
  return 2;
}
```
### 編譯並執行看看被竄改的答案
```c
gcc -o hook.so -shared hook.c
LD_PRELOAD=./hook.so ./main
```
### 
```
# 1.正常行為
ksu@KSU-Ubuntu-1604-32:~$ gedit main.c
ksu@KSU-Ubuntu-1604-32:~$ gcc -o main main.c -lm
ksu@KSU-Ubuntu-1604-32:~$ ./main
foo
-nan
ksu@KSU-Ubuntu-1604-32:~$ ./main
16
4.000000

# 2.駭客攻擊
ksu@KSU-Ubuntu-1604-32:~$ gedit hook.c
ksu@KSU-Ubuntu-1604-32:~$ gcc -o hook.so -shared hook.c
ksu@KSU-Ubuntu-1604-32:~$ LD_PRELOAD=./hook.so ./main
5
2.000000
```

## ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+)CTF:pass

## ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+)EasyCTF 2017 LuckGuess 

### `[延伸閱讀|read-around|Further reading|Weiterlesen|Lectures complémentaires]`

 - [[Practical Binary Analysis: Build Your Own Linux Tools for Binary Instrumentation, Analysis, and Disassembly,Dennis Andriesse]](https://www.tenlong.com.tw/products/9781593279127)
 - Chapter 7: Simple Code Injection Techniques for ELF
   - Four Simple Code Injection Techniques:
   - 1.Hex Editing ==> Binary Modification/Patch
   - 2.LD_Preload  ==>Modify Shared Library Behavior
   - 3.elfinject Tools ==> Inject an ELF Section
   - 4.ELF entry point modification technique | Constructor/destructor Hijacking | GOT Hijacking | PLT Hijacking


### 網路學習資源linux injection
- [jmpews/pwn2exploit](https://github.com/jmpews/pwn2exploit/)
- [DLL injection for Linux: LD_PRELOAD Demo](https://www.youtube.com/watch?v=KJPeZptzl1U)
- [Injector](https://github.com/kubo/injector)
- [DEFCON 19: Jugaad -- Linux Thread Injection Kit](https://www.youtube.com/watch?v=Nm5htFWAVUE)
- [Linux ptrace introduction AKA injecting into sshd for fun](https://blog.xpnsec.com/linux-process-injection-aka-injecting-into-sshd-for-fun/)
- [Becoming Root With Wildcard Injections on Linux|  Linux privilege escalation by exploiting a wildcard injection](https://betterprogramming.pub/becoming-root-with-wildcard-injections-on-linux-2dc94032abeb)
- [code injection on Linux and macOS with LD_PRELOAD](https://www.getambassador.io/resources/code-injection-on-linux-and-macos/)  [[GITHUB]](https://github.com/wolfcw/libfaketime/)
- [Code Injection into Running Linux Application](https://www.codeproject.com/Articles/33340/Code-Injection-into-Running-Linux-Application)
- [linux dynamic link library injection](https://stackoverflow.com/questions/30630084/linux-dynamic-link-library-injection?noredirect=1&lq=1)
- [Packit - Packet analysis and injection tool](https://linux.die.net/man/8/packit)
- sudo apt-get install packit
- [Packet injection](https://en.wikipedia.org/wiki/Packet_injection)
- [hexinject – Hexadecimal packet injector/sniffer](https://tools.kali.org/sniffingspoofing/hexinject)


### paper
- [FIFA: A Kernel-Level Fault Injection Framework for ARM-Based Embedded Linux System](https://ieeexplore.ieee.org/document/7927960)
- [Virtualized-Fault Injection Testing: A Machine Learning Approach](https://ieeexplore.ieee.org/document/8367057)
- [Active Machine Learning to Test Autonomous Driving](https://ieeexplore.ieee.org/document/9440164)

