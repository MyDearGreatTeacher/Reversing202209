# Memory Layout of C Programs

- [講解 Memory Layout of C program](https://aticleworld.com/memory-layout-of-c-program/)
- [Memory Layout of C Program](https://www.hackerearth.com/practice/notes/memory-layout-of-c-program/)
- [Memory Layout of C Program](https://www.javatpoint.com/memory-layout-in-c)

- [C Programming Tutorial 1 : Memory Layout of a C / C++ Program : Think Aloud Academy](https://www.youtube.com/watch?v=0jhQBQcGnuM)
- [C Programming Tutorial 2 : Memory Leak in a C / C++ Program : Think Aloud Academy](https://www.youtube.com/watch?v=MT26vLibudQ)
- [Understanding Static, Stack, and Heap Memory Regions (Examples in C)](https://www.youtube.com/watch?v=jKcg3ze10Hk)
- [Pointers and dynamic memory - stack vs heap](https://www.youtube.com/watch?v=_8-ht2AKyH4&t=128s)


# example 1 
- 變數的記憶體位址

```c
# include <stdio.h>

int main(){

  int i = 0;
  int j = 20;
  int k = 101;
  double balance[5] = {1000.0, 2.0, 3.4, 7.0, 50.0};
  int a[20];
   
  for (int x = 0; x < 20; x ++)
  {
      a[x] =x;
  }
  
  printf("i adress is %x, value is %d \n", &i, i);
  printf("j adress is %x, value is %d \n", &j, j);
  printf("k adress is %x, value is %d \n", &k, k);
  printf("a adress is %x \n", a);
  printf("a[0] adress is %x, value is %d \n", &a[0], a[0]);
  printf("a[1] adress is %x, value is %d \n", &a[1], a[1]); 
  printf("balance[0] adress is %x, value is %f \n", &balance[0], balance[0]);
  printf("balance[1] adress is %x, value is %f \n", &balance[1], balance[1]);
  
  return 0;
}
```
## 執行程式兩次看看答案有何變化？　and why?
```
./test3
i adress is ffffe208, value is 0 
j adress is ffffe204, value is 20 
k adress is ffffe200, value is 101 
a adress is ffffe180 
a[0] adress is ffffe180, value is 0 
a[1] adress is ffffe184, value is 1 
balance[0] adress is ffffe1d0, value is 1000.000000 
balance[1] adress is ffffe1d8, value is 2.000000
```

###  How Effective is ASLR on Linux Systems?
```
Configure ASLR in Linux using the /proc/sys/kernel/randomize_va_space interface.

The following values are supported:
0 – No randomization. Everything is static.
1 – Conservative randomization. Shared libraries, stack, mmap(), VDSO and heap are randomized.
2 – Full randomization. In addition to elements listed in the previous point, memory managed through brk() is also randomized.

to disable aslr ==> echo 0 | sudo tee /proc/sys/kernel/randomize_va_space
to enable aslr  ==> echo 2 | sudo tee /proc/sys/kernel/randomize_va_space

This won't survive a reboot, so you'll have to configure this in sysctl. 
Add a file /etc/sysctl.d/01-disable-aslr.conf containing:

kernel.randomize_va_space = 0

should permanently disable this.
```
## struct 與 記憶體位址 
```c
# include <stdio.h>

int main(){

  int i = 0;
  int j = 20;
  int k = 101;
  double balance[5] = {1000.0, 2.0, 3.4, 7.0, 50.0};
  int a[20];
   
  for (int x = 0; x < 20; x ++)
  {
      a[x] =x;
  }
  
  struct Books
  {
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
  }; 
  
  struct Books book = {"C ", "NTHU", "Program", 723456};
  printf("i adress is %x, value is %d \n", &i, i);
  printf("j adress is %x, value is %d \n", &j, j);
  printf("k adress is %x, value is %d \n", &k, k);
  printf("a adress is %x \n", a);
  printf("a[0] adress is %x, value is %d \n", &a[0], a[0]);
  printf("a[1] adress is %x, value is %d \n", &a[1], a[1]); 
  printf("balance[0] adress is %x, value is %f \n", &balance[0], balance[0]);
  printf("balance[1] adress is %x, value is %f \n", &balance[1], balance[1]);
  printf("Address: book: %x, book.title: %x, book.author : %x, book.subject: %x, book.book_id : %x \n",&book, &book.title, &book.author, &book.subject, &book.book_id);
  printf("title : %s  author: %s  subject: %s  book_id: %d\n", book.title, book.author, book.subject, book.book_id);

  
  return 0;
}
```

```
i adress is ffffe208, value is 0 
j adress is ffffe204, value is 20 
k adress is ffffe200, value is 101 
a adress is ffffe180 
a[0] adress is ffffe180, value is 0 
a[1] adress is ffffe184, value is 1 
balance[0] adress is ffffe1d0, value is 1000.000000 
balance[1] adress is ffffe1d8, value is 2.000000 
Address: book: ffffe0b0, book.title: ffffe0b0, book.author : ffffe0e2, book.subject: ffffe114, book.book_id : ffffe178 
title : C   author: NTHU  subject: Program  book_id: 723456
```

# example 3:執行底下程式看看
```c
gcc memory-layout.c -o memory-layout
size memory-layout < ==使用size看看不同區段的大小增長
```
- [資料來源:Memory Layout of C Programs](https://www.geeksforgeeks.org/memory-layout-of-c-program/)
- [Memory Layout of C Programs](https://viblo.asia/p/memory-layout-of-c-programs-3NVRkbXnv9xn)

## example 3a:
```c
#include <stdio.h>
 
int main(void)
{
    return 0;
}
```

## example 3b:
```c

#include <stdio.h>
 
int global; /* Uninitialized variable stored in bss*/
 
int main(void)
{
    return 0;
}
```
## example 3c
```c
#include <stdio.h>
 
int global; /* Uninitialized variable stored in bss*/
 
int main(void)
{
    static int i; /* Uninitialized static variable stored in bss */
    return 0;
}
```
## example 3d
```c
#include <stdio.h>
 
int global; /* Uninitialized variable stored in bss*/
 
int main(void)
{
    static int i = 100; /* Initialized static variable stored in DS*/
    return 0;
}
```
## example 3e
```c
#include <stdio.h>
 
int global = 10; /* initialized global variable stored in DS*/
 
int main(void)
{
    static int i = 100; /* Initialized static variable stored in DS*/
    return 0;
}
```
## example 4:
```c
# https://www.hackerearth.com/practice/notes/memory-layout-of-c-program/
#include <stdio.h>

char c[]="rishabh tripathi";     /*  global variable stored in Initialized Data Segment in read-write area*/
const char s[]="HackerEarth";    /* global variable stored in Initialized Data Segment in read-only area*/

int main()
{
    static int i=11;          /* static variable stored in Initialized Data Segment*/
    return 0;
}
```
