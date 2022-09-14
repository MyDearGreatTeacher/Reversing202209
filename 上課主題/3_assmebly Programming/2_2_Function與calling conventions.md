
## [calling conventions呼叫約定](https://en.wikipedia.org/wiki/Calling_convention)  [[中文說明]](https://zh.wikipedia.org/wiki/%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

```c
int callee(int, int, int);

int caller(void)
{
   register int ret;
      
   ret = callee(1, 2, 3);
   ret += 5;
   return ret;
}
```

- 呼叫約定是一種定義子過程從呼叫處接受參數以及返回結果的方法的約定。
- 不同呼叫約定的區別在於：
  - 參數和返回值放置的位置 ==> 暫存器(register) vs 呼叫棧(stack) vs 兩者混合
  - 參數傳遞的順序（或者單個參數不同部分的順序）==> 由右到左  vs 由左到右
  - 呼叫前設定和呼叫後清理的工作，在呼叫者(caller)和被呼叫者(callee)之間如何分配


## [x86-calling conventions](https://en.wikipedia.org/wiki/X86_calling_conventions) [[中文說明]](https://zh.wikipedia.org/wiki/X86%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)
![x86_callingconventions](x86_callingconventions.png)


- cdecl(C declaration) [[NASM ]](https://cs.lmu.edu/~ray/notes/nasmtutorial/)
  - Parameters are passed in reverse order (from right to left) via the stack.
  - eax, ecx, and edx are caller-saved (volatile), while the rest of the general purpose registers are callee-saved (non-volatile). Consequently, if you want to save eax, ecx, and edx, you need to do so in the calling function because they will likely be overwritten during function execution.
  - eax is used as the return register in most cases. st(0) is used for a floating-point return.
  - The caller is responsible for cleaning up the stack. 

### [練習: 完成課本範例程式Program_6.1的測試](https://github.com/brianrhall/Assembly/tree/master/Chapter_6/Program%206.1)
```c
# include <stdio.h>

int sum(int, int);

int main() {
  int numl = 2, num2 = 4, answer;
  answer = sum (numl, num2);
  printf("%d + %d = %d \n",num1,num2,answer);
  return 0;
}

int sum (int numl, int num2) {
  return numl + num2;
}
```
### Program_6.1_32bit NASM.asm
```c
section .data
num1: dd 2
num2: dd 4

section .text
global _main, _sum
_main:

mov eax, 10
dec eax
mov ebx, 5

push DWORD[num2]
push DWORD[num1]
call _sum
add esp, 8

add eax, ebx
dec eax

mov eax, 1
mov ebx, 0
int 80h

_sum:
push ebp
mov ebp, esp
push ebx
mov ebx, [ebp + 8]
mov eax, [ebp + 12]
add eax, ebx
pop ebx
pop ebp
ret
```

### Program_6.1_64bit NASM.asm
```c
section .data
num1: dd 2
num2: dd 4

section .text
global _main, _sum
_main:

mov rax, 10
dec rax
mov rbx, 5

movsx rdi, DWORD [rel num1]
movsx rsi, DWORD [rel num2]
call _sum

add rax, rbx
dec rax

mov rax, 60
xor rdi, rdi
syscall

_sum:
push rbp
mov rbp, rsp
push rbx
mov rax, rdi
add rax, rsi
pop rbx
pop rbp
ret
```

### Ubuntu 16.04 LTS(32bit) 測試結果
```c
# include <stdio.h>

int sum(int, int);

int main() {
  int numl = 2, num2 = 4, answer;
  answer = sum (numl, num2);
  printf("%d + %d = %d \n",num1,num2,answer);
  return 0;
}

int sum (int numl, int num2) {
  return numl + num2;
}
```
- objdump -M intel -D -j .text test1 --no-show-raw-insn

```C
0804840b <main>:
 804840b:	lea    ecx,[esp+0x4]
 804840f:	and    esp,0xfffffff0
 8048412:	push   DWORD PTR [ecx-0x4]
 8048415:	push   ebp
 8048416:	mov    ebp,esp
 8048418:	push   ecx
 8048419:	sub    esp,0x14
 804841c:	mov    DWORD PTR [ebp-0x14],0x2
 8048423:	mov    DWORD PTR [ebp-0x10],0x4
 804842a:	sub    esp,0x8
 804842d:	push   DWORD PTR [ebp-0x10]
 8048430:	push   DWORD PTR [ebp-0x14]
 8048433:	call   8048461 <sum>
 8048438:	add    esp,0x10
 804843b:	mov    DWORD PTR [ebp-0xc],eax
 804843e:	push   DWORD PTR [ebp-0xc]
 8048441:	push   DWORD PTR [ebp-0x10]
 8048444:	push   DWORD PTR [ebp-0x14]
 8048447:	push   0x80484f0
 804844c:	call   80482e0 <printf@plt>
 8048451:	add    esp,0x10
 8048454:	mov    eax,0x0
 8048459:	mov    ecx,DWORD PTR [ebp-0x4]
 804845c:	leave  
 804845d:	lea    esp,[ecx-0x4]
 8048460:	ret    

08048461 <sum>:
 8048461:	push   ebp
 8048462:	mov    ebp,esp
 8048464:	mov    edx,DWORD PTR [ebp+0x8]
 8048467:	mov    eax,DWORD PTR [ebp+0xc]
 804846a:	add    eax,edx
 804846c:	pop    ebp
 804846d:	ret    
 804846e:	xchg   ax,ax
```
## 有時間看看microsoft cdecl, stdcall, and fastcall conventions in 32-bit 的差異


## x86-64 calling conventions 
![x86_64_callingconventions](x86_64_callingconventions.png)

- Table 6.1 x86_64 Calling conventions
- 第一類型 :System V AMD64 ABI
  - Solaris，GNU/Linux，FreeBSD和其他非微軟OS上使用。
  - 前六個整數型參數放在暫存器RDI, RSI, RDX, RCX, R8和R9 | For integers and pointers, rdi, rsi, rdx, rcx, r8, r9.
  - XMM0到XMM7用來放置浮點數參數。For floating-point (float, double), xmm0, xmm1, xmm2, xmm3, xmm4, xmm5, xmm6, xmm7.
  - 其他額外的參數(大於6)推入棧(stack) | Additional parameters are pushed on the stack, right to left, and are to be removed by the caller after the call.
  - 系統呼叫==> 使用R10(替代RCX)
  - 返回值儲存在RAX   ==> Integers are returned in rax or rdx:rax, and floating point values are returned in xmm0 or xmm1:xmm0.
  - 與微軟不同的是，不需要提供影子空間。
  - 在函式入口，返回值與棧上第七個整型參數相鄰。 


- [AMD64 Calling Conventions for Linux / Mac OSX](https://courses.cs.washington.edu/courses/cse378/10au/sections/Section1_recap.pdf)
- [NASM Tutorial](https://cs.lmu.edu/~ray/notes/nasmtutorial/)
```
After the parameters are pushed, the call instruction is made, so when the called function gets control, the return address is at [rsp], the first memory parameter is at [rsp+8], etc.
The stack pointer rsp must be aligned to a 16-byte boundary before making a call. Fine, but the process of making a call pushes the return address (8 bytes) on the stack, so when a function gets control, rsp is not aligned. You have to make that extra space yourself, by pushing something or subtracting 8 from rsp.
The only registers that the called function is required to preserve (the calle-save registers) are: rbp, rbx, r12, r13, r14, r15. All others are free to be changed by the called function.
The callee is also supposed to save the control bits of the XMCSR and the x87 control word, but x87 instructions are rare in 64-bit code so you probably don’t have to worry about this.
```


-第二類型 :[微軟x86-64呼叫約定](https://docs.microsoft.com/en-us/cpp/build/x64-calling-convention?view=msvc-160)
 - 在Windows x64環境下編譯代碼時，只有一種呼叫約定(32位元下的各種約定在64位元下統一成一種)
 - Two important differences between x86 and x64 are the 64-bit addressing capability and a flat set of 16 64-bit registers for general use. 
 - Given the expanded register set, x64 uses the __fastcall calling convention and a RISC-based exception-handling model. 
 - The __fastcall convention uses registers for the first four arguments and the stack frame to pass additional arguments. 

## 驗證32bit 與64bit函數呼叫的機制 [Linux 版本] [Microsoft有不同的story]
- example 1:三個參數的函數
- example 2:七個參數的函數 32bit vs 64 bit see 參數傳遞方式的差異

## example 1
```c
# include <stdio.h>

int sum(int a1, int b1,int c1)
{
  return a1+b1+c1;
}


int main()
{
  int a=1,b=2,c=3;
  int summation1;

  summation1 = sum(a,b,c);
  printf("summation1 is %d\n",summation1);

  return 0;

}
```
### Kali Linux 2019(64bit) 測試結果
- gcc test1.c -o test1 -g
- objdump -M intel -D -j .text test1
```
test:     file format elf64-x86-64


Disassembly of section .text:

0000000000001135 <sum>:
    1135:	55                   	push   rbp
    1136:	48 89 e5             	mov    rbp,rsp
    1139:	89 7d fc             	mov    DWORD PTR [rbp-0x4],edi
    113c:	89 75 f8             	mov    DWORD PTR [rbp-0x8],esi
    113f:	89 55 f4             	mov    DWORD PTR [rbp-0xc],edx
    1142:	8b 55 fc             	mov    edx,DWORD PTR [rbp-0x4]
    1145:	8b 45 f8             	mov    eax,DWORD PTR [rbp-0x8]
    1148:	01 c2                	add    edx,eax
    114a:	8b 45 f4             	mov    eax,DWORD PTR [rbp-0xc]
    114d:	01 d0                	add    eax,edx
    114f:	5d                   	pop    rbp
    1150:	c3                   	ret    

0000000000001151 <main>:
    1151:	55                   	push   rbp
    1152:	48 89 e5             	mov    rbp,rsp
    1155:	48 83 ec 10          	sub    rsp,0x10
    1159:	c7 45 fc 01 00 00 00 	mov    DWORD PTR [rbp-0x4],0x1
    1160:	c7 45 f8 02 00 00 00 	mov    DWORD PTR [rbp-0x8],0x2
    1167:	c7 45 f4 03 00 00 00 	mov    DWORD PTR [rbp-0xc],0x3
    116e:	8b 55 f4             	mov    edx,DWORD PTR [rbp-0xc]
    1171:	8b 4d f8             	mov    ecx,DWORD PTR [rbp-0x8]
    1174:	8b 45 fc             	mov    eax,DWORD PTR [rbp-0x4]
    1177:	89 ce                	mov    esi,ecx
    1179:	89 c7                	mov    edi,eax
    117b:	e8 b5 ff ff ff       	call   1135 <sum>
    1180:	89 45 f0             	mov    DWORD PTR [rbp-0x10],eax
    1183:	8b 45 f0             	mov    eax,DWORD PTR [rbp-0x10]
    1186:	89 c6                	mov    esi,eax
    1188:	48 8d 3d 75 0e 00 00 	lea    rdi,[rip+0xe75]        # 2004 <_IO_stdin_used+0x4>
    118f:	b8 00 00 00 00       	mov    eax,0x0
    1194:	e8 97 fe ff ff       	call   1030 <printf@plt>
    1199:	b8 00 00 00 00       	mov    eax,0x0
    119e:	c9                   	leave  
    119f:	c3                   	ret    
```

### Ubuntu 16.04 LTS(32bit)測試結果
- gcc test3.c -o test3 -g
- objdump -M intel -D -j .text test3 --no-show-raw-insn
```c
0804840b <sum>:
 804840b:	push   ebp
 804840c:	mov    ebp,esp
 804840e:	mov    edx,DWORD PTR [ebp+0x8]
 8048411:	mov    eax,DWORD PTR [ebp+0xc]
 8048414:	add    edx,eax
 8048416:	mov    eax,DWORD PTR [ebp+0x10]
 8048419:	add    eax,edx
 804841b:	pop    ebp
 804841c:	ret    

0804841d <main>:
 804841d:	lea    ecx,[esp+0x4]
 8048421:	and    esp,0xfffffff0
 8048424:	push   DWORD PTR [ecx-0x4]
 8048427:	push   ebp
 8048428:	mov    ebp,esp
 804842a:	push   ecx
 804842b:	sub    esp,0x14
 804842e:	mov    DWORD PTR [ebp-0x18],0x1
 8048435:	mov    DWORD PTR [ebp-0x14],0x2
 804843c:	mov    DWORD PTR [ebp-0x10],0x3
 8048443:	push   DWORD PTR [ebp-0x10]
 8048446:	push   DWORD PTR [ebp-0x14]
 8048449:	push   DWORD PTR [ebp-0x18]
 804844c:	call   804840b <sum>
 8048451:	add    esp,0xc
 8048454:	mov    DWORD PTR [ebp-0xc],eax
 8048457:	sub    esp,0x8
 804845a:	push   DWORD PTR [ebp-0xc]
 804845d:	push   0x8048500
 8048462:	call   80482e0 <printf@plt>
 8048467:	add    esp,0x10
 804846a:	mov    eax,0x0
 804846f:	mov    ecx,DWORD PTR [ebp-0x4]
 8048472:	leave  
 8048473:	lea    esp,[ecx-0x4]
 8048476:	ret    
 8048477:	xchg   ax,ax
 8048479:	xchg   ax,ax
 804847b:	xchg   ax,ax
 804847d:	xchg   ax,ax
 804847f:	nop
```
##  example 2
```c
# include <stdio.h>

int sum(int a1, int b1,int c1,int d1,int e1,int f1,int g1)
{
  return a1+b1+c1+d1+e1+f1+g1;
}


int main()
{
  int a=1,b=2,c=3,d=4,e=5,f=6,g=7;
  int summation;
  
  summation = sum(a,b,c,d,e,f,g);
  printf("summation is %d\n",summation);
  
  return 0;
}
```
### Kali Linux 2019(64bit) 測試結果
- gcc test2.c -o test2 -g
- objdump -M intel -D -j .text test2
```c
0000000000001135 <sum>:
    1135:	55                   	push   rbp
    1136:	48 89 e5             	mov    rbp,rsp
    1139:	89 7d fc             	mov    DWORD PTR [rbp-0x4],edi
    113c:	89 75 f8             	mov    DWORD PTR [rbp-0x8],esi
    113f:	89 55 f4             	mov    DWORD PTR [rbp-0xc],edx
    1142:	89 4d f0             	mov    DWORD PTR [rbp-0x10],ecx
    1145:	44 89 45 ec          	mov    DWORD PTR [rbp-0x14],r8d
    1149:	44 89 4d e8          	mov    DWORD PTR [rbp-0x18],r9d
    114d:	8b 55 fc             	mov    edx,DWORD PTR [rbp-0x4]
    1150:	8b 45 f8             	mov    eax,DWORD PTR [rbp-0x8]
    1153:	01 c2                	add    edx,eax
    1155:	8b 45 f4             	mov    eax,DWORD PTR [rbp-0xc]
    1158:	01 c2                	add    edx,eax
    115a:	8b 45 f0             	mov    eax,DWORD PTR [rbp-0x10]
    115d:	01 c2                	add    edx,eax
    115f:	8b 45 ec             	mov    eax,DWORD PTR [rbp-0x14]
    1162:	01 c2                	add    edx,eax
    1164:	8b 45 e8             	mov    eax,DWORD PTR [rbp-0x18]
    1167:	01 c2                	add    edx,eax
    1169:	8b 45 10             	mov    eax,DWORD PTR [rbp+0x10]
    116c:	01 d0                	add    eax,edx               ==> 最後的 eax 就是函數回傳值
    116e:	5d                   	pop    rbp
    116f:	c3                   	ret    

0000000000001170 <main>:
    1170:	55                   	push   rbp
    1171:	48 89 e5             	mov    rbp,rsp
    1174:	48 83 ec 20          	sub    rsp,0x20
    1178:	c7 45 fc 01 00 00 00 	mov    DWORD PTR [rbp-0x4],0x1
    117f:	c7 45 f8 02 00 00 00 	mov    DWORD PTR [rbp-0x8],0x2
    1186:	c7 45 f4 03 00 00 00 	mov    DWORD PTR [rbp-0xc],0x3
    118d:	c7 45 f0 04 00 00 00 	mov    DWORD PTR [rbp-0x10],0x4
    1194:	c7 45 ec 05 00 00 00 	mov    DWORD PTR [rbp-0x14],0x5
    119b:	c7 45 e8 06 00 00 00 	mov    DWORD PTR [rbp-0x18],0x6
    11a2:	c7 45 e4 07 00 00 00 	mov    DWORD PTR [rbp-0x1c],0x7
    11a9:	44 8b 4d e8          	mov    r9d,DWORD PTR [rbp-0x18]
    11ad:	44 8b 45 ec          	mov    r8d,DWORD PTR [rbp-0x14]
    11b1:	8b 4d f0             	mov    ecx,DWORD PTR [rbp-0x10]
    11b4:	8b 55 f4             	mov    edx,DWORD PTR [rbp-0xc]
    11b7:	8b 75 f8             	mov    esi,DWORD PTR [rbp-0x8]
    11ba:	8b 45 fc             	mov    eax,DWORD PTR [rbp-0x4]
    11bd:	8b 7d e4             	mov    edi,DWORD PTR [rbp-0x1c]
    11c0:	57                   	push   rdi
    11c1:	89 c7                	mov    edi,eax
    11c3:	e8 6d ff ff ff       	call   1135 <sum>
    11c8:	48 83 c4 08          	add    rsp,0x8
    11cc:	89 45 e0             	mov    DWORD PTR [rbp-0x20],eax
    11cf:	8b 45 e0             	mov    eax,DWORD PTR [rbp-0x20]
    11d2:	89 c6                	mov    esi,eax
    11d4:	48 8d 3d 29 0e 00 00 	lea    rdi,[rip+0xe29]        # 2004 <_IO_stdin_used+0x4>
    11db:	b8 00 00 00 00       	mov    eax,0x0
    11e0:	e8 4b fe ff ff       	call   1030 <printf@plt>
    11e5:	b8 00 00 00 00       	mov    eax,0x0
    11ea:	c9                   	leave  
    11eb:	c3                   	ret    
    11ec:	0f 1f 40 00          	nop    DWORD PTR [rax+0x0]
```

### Ubuntu 16.04 LTS(32bit)測試結果
- gcc test2.c -o test2 -g
- objdump -M intel -D -j .text test2 --no-show-raw-insn
```
0804840b <sum>:
 804840b:	push   ebp
 804840c:	mov    ebp,esp
 804840e:	mov    edx,DWORD PTR [ebp+0x8]
 8048411:	mov    eax,DWORD PTR [ebp+0xc]
 8048414:	add    edx,eax
 8048416:	mov    eax,DWORD PTR [ebp+0x10]
 8048419:	add    edx,eax
 804841b:	mov    eax,DWORD PTR [ebp+0x14]
 804841e:	add    edx,eax
 8048420:	mov    eax,DWORD PTR [ebp+0x18]
 8048423:	add    edx,eax
 8048425:	mov    eax,DWORD PTR [ebp+0x1c]
 8048428:	add    edx,eax
 804842a:	mov    eax,DWORD PTR [ebp+0x20]
 804842d:	add    eax,edx                 ==> 最後的 eax 就是函數回傳值
 804842f:	pop    ebp
 8048430:	ret    

08048431 <main>:
 8048431:	lea    ecx,[esp+0x4]
 8048435:	and    esp,0xfffffff0
 8048438:	push   DWORD PTR [ecx-0x4]
 804843b:	push   ebp
 804843c:	mov    ebp,esp
 804843e:	push   ecx
 804843f:	sub    esp,0x24
 8048442:	mov    DWORD PTR [ebp-0x28],0x1
 8048449:	mov    DWORD PTR [ebp-0x24],0x2
 8048450:	mov    DWORD PTR [ebp-0x20],0x3
 8048457:	mov    DWORD PTR [ebp-0x1c],0x4
 804845e:	mov    DWORD PTR [ebp-0x18],0x5
 8048465:	mov    DWORD PTR [ebp-0x14],0x6
 804846c:	mov    DWORD PTR [ebp-0x10],0x7
 8048473:	push   DWORD PTR [ebp-0x10]
 8048476:	push   DWORD PTR [ebp-0x14]
 8048479:	push   DWORD PTR [ebp-0x18]
 804847c:	push   DWORD PTR [ebp-0x1c]
 804847f:	push   DWORD PTR [ebp-0x20]
 8048482:	push   DWORD PTR [ebp-0x24]
 8048485:	push   DWORD PTR [ebp-0x28]
 8048488:	call   804840b <sum>
 804848d:	add    esp,0x1c
 8048490:	mov    DWORD PTR [ebp-0xc],eax
 8048493:	sub    esp,0x8
 8048496:	push   DWORD PTR [ebp-0xc]
 8048499:	push   0x8048540
 804849e:	call   80482e0 <printf@plt>
 80484a3:	add    esp,0x10
 80484a6:	mov    eax,0x0
 80484ab:	mov    ecx,DWORD PTR [ebp-0x4]
 80484ae:	leave  
 80484af:	lea    esp,[ecx-0x4]
 80484b2:	ret    
 80484b3:	xchg   ax,ax
 80484b5:	xchg   ax,ax
 80484b7:	xchg   ax,ax
 80484b9:	xchg   ax,ax
 80484bb:	xchg   ax,ax
 80484bd:	xchg   ax,ax
 80484bf:	nop
```
