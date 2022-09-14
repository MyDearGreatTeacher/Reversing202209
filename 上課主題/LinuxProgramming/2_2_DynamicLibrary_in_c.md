# Build C Library

- [Shared libraries with GCC on Linux](https://www.cprogramming.com/tutorial/shared-libraries-linux-gcc.html)
- [Static and Dynamic Libraries in C Language](https://medium.com/@luischaparroc/https-medium-com-luischaparroc-dynamic-libraries-in-c-96a989848476)
- [Library可分成三種，static、shared與dynamically loaded](https://blog.xuite.net/tzeng015/twblog/113272198)


| name | 說明|
|-----| -------|
|soname| 用來表示是一個特定library 的名稱，像是libmylib.so.1 。前面以`lib' 開頭，接著是該library 的名稱，然後是`.so' ，接著是版號，用來表名他的介面；如果介面改變時，就會增加版號來維護相容度。|
|real name| 實際放有library程式的檔案名稱，後面會再加上minor 版號與 release 版號，像是libmylib.so.1.0.0| 
|linker name| 於連結時的名稱，是不含版號的soname ，如: libmylib.so。 通常linker name與real name是用ln 指到對應的real name ，用來提供彈性與維護性。|


# 2_2_DynamicLibrary_in_c.md
## example 1:

- [Static and Dynamic Libraries in C Language](https://medium.com/@luischaparroc/https-medium-com-luischaparroc-dynamic-libraries-in-c-96a989848476)

```
calculator.c  
header.h  

main.c
```
### main.c
```c
#include "header.h"
#include <stdio.h>
/**
 * main - Entry Point
 *
 * Return: Always 0.
 */
int main(void)
{
    printf("4 + 2 = %d\n", calculator('+', 4, 2));
    printf("4 - 2 = %d\n", calculator('-', 4, 2));
    printf("4 * 2 = %d\n", calculator('*', 4, 2));
    printf("4 / 2 = %d\n", calculator('/', 4, 2));
    return (0);
}
```
### calculator.c
```c
#include "header.h"
/**
 * calculator - Executes basic math operations
 *
 * @op: char that indicates math operation executed.
 * @num1: number one.
 * @num2: number two.
 * Return: addition if op is '+'
 *         subtraction if op is '-'
 *         multiplication if op is '*'
 *         division if op is '/'
 *         otherwise, 0.
 */
int calculator(char op, int num1, int num2)
{
    if (op == '+')
        return (num1 + num2);
    if (op == '-')
        return (num1 - num2);
    if (op == '*')
        return (num1 * num2);
    if (op == '/')
        return (num1 /num2);
    return (0);
}
```
### header.h
```c
#ifndef __HEADER__
#define __HEADER__
int calculator(char op, int num1, int num2);
#endif
```
## 執行過程

### Step 1: Compiling with Position Independent Code
```
gcc -Wall -fPIC -c calculator.c   ==> 產生 calculator.o


-Wall, which prints all warning messages
-c, which creates the object file .o. 
-fPIC flag generates position-independent code, which accesses all constant address stored in the Global Offset Table (GOT). 
       This table is used by executable programs to find, during runtime, address of functions — of calculator, in this example— 
       and global variables unknown in compile time.
```
### Step 2: Creating a shared library from an object file

gcc -shared -Wl,-soname,libcalc.so -o libcalc.so *.o  ==> 產生函數庫 libcalc.so

```
-shared flag generates a shared object which, at the moment to be compiled with another object file, 
 it could be linked to form an executable file. 

-Wl,options passes options to linker: 
    in this case, -soname, to indicate the binary api compatibility of the library (0, by default). 
    -o flag saves the output library in a file with a given name — libcalc.so.
```

```
To use a dynamic library, it is needed to export the LD_LIBRARY_PATH environment variable, 
which has a value of the first searched libraries by the executable file:


export LD_LIBRARY_PATH=$PWD/libcalc.so:
```


- gcc -Wall -pedantic -Werror -Wextra -L. main.c -lcalc  ==> 產生執行檔a.out
```
- The -pedantic option tells GCC to issue warnings in such cases  
     https://gcc.gnu.org/onlinedocs/gcc/Warnings-and-Errors.html
 
-L flag the directory where the created library resides is indicated. 
-l flag, the name of the library is indicated to the compiler.
```

```
./a.out 
4 + 2 = 6
4 - 2 = 2
4 * 2 = 8
4 / 2 = 2
```
```
-shared 表示要編譯成shared library
-Wl 用於參遞參數給linker，因此-soname與libmylib.so.1會被傳給linker處理。
-soname用來指名soname 為limylib.so.1
library會被輸出成libmylib.so.1.0.0 (也就是real name)

若不指定soname 的話，在編譯結連後的執行檔會以連時的library檔名為
soname，並載入他。否則是載入soname指定的library檔案。


可以利用objdump 來看library 的soname。
$ objdump -p libmylib.so | grep SONAME
```
