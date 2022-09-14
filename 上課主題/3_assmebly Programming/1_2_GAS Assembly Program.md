# Writing Assembly Program using GAS

範例程式來源 [GNU Assembler Examples](https://cs.lmu.edu/~ray/notes/gasexamples/)

## 範例1:64-bit Hello World
```gas
        .global _start

        .text
_start:
        # write(1, message, 13)
        mov     $1, %rax                # system call 1 is write     $1 --> %rax  
        mov     $1, %rdi                # file handle 1 is stdout
        mov     $message, %rsi          # address of string to output
        mov     $13, %rdx               # number of bytes
        syscall                         # invoke operating system to do the write

        # exit(0)
        mov     $60, %rax               # system call 60 is exit
        xor     %rdi, %rdi              # we want return code 0
        syscall                         # invoke operating system to exit
message:
        .ascii  "Hello, world\n"
```
```
$ gcc -c hello.s && ld hello.o && ./a.out
Hello, World
```
## 範例2:Working with the C Library
```
# ----------------------------------------------------------------------------------------
# Writes "Hola, mundo" to the console using a C library. Runs on Linux or any other system
# that does not use underscores for symbols in its C library. To assemble and run:
#
#     gcc hola.s && ./a.out
# ----------------------------------------------------------------------------------------

        .global main

        .text
main:                                   # This is called by C library's startup code
        mov     $message, %rdi          # First integer (or pointer) parameter in %rdi
        call    puts                    # puts(message)
        ret                             # Return to C library code
message:
        .asciz "Hola, mundo"            # asciz puts a 0 byte at the end
```
## 範例3: 費式數列
```
# -----------------------------------------------------------------------------
# A 64-bit Linux application that writes the first 90 Fibonacci numbers.  It
# needs to be linked with a C library.
#
# Assemble and Link:
#     gcc fib.s
# -----------------------------------------------------------------------------

        .global main

        .text
main:
        push    %rbx                    # we have to save this since we use it

        mov     $90, %ecx               # ecx will countdown to 0
        xor     %rax, %rax              # rax will hold the current number
        xor     %rbx, %rbx              # rbx will hold the next number
        inc     %rbx                    # rbx is originally 1
print:
        # We need to call printf, but we are using eax, ebx, and ecx.  printf
        # may destroy eax and ecx so we will save these before the call and
        # restore them afterwards.

        push    %rax                    # caller-save register
        push    %rcx                    # caller-save register

        mov     $format, %rdi           # set 1st parameter (format)
        mov     %rax, %rsi              # set 2nd parameter (current_number)
        xor     %rax, %rax              # because printf is varargs

        # Stack is already aligned because we pushed three 8 byte registers
        call    printf                  # printf(format, current_number)

        pop     %rcx                    # restore caller-save register
        pop     %rax                    # restore caller-save register

        mov     %rax, %rdx              # save the current number
        mov     %rbx, %rax              # next number is now current
        add     %rdx, %rbx              # get the new next number
        dec     %ecx                    # count down
        jnz     print                   # if not done counting, do some more

        pop     %rbx                    # restore rbx before returning
        ret
format:
        .asciz  "%20ld\n"
```
```
$ gcc fib.s && ./a.out
                   0
                   1
                   1
                   2
                   3
                 ...
  420196140727489673
```

## ORW == open, read, write file

- [GAS x64 GNU Assembler file read write tutorial in Linux](https://www.youtube.com/watch?v=INqm4Vjqi-8)

```gas
.global _start
.data
file:.string "hi.txt"
space:.space 10

.text
start:
    mov $2,%rax
    mov $file,%rdi
    mov $2,%rsi
    mov $0777,%rdx
    syscall

    mov %rax,%r8
    
    mov $0,%rax
    mov %r8,%rdi
    mov $space,%rsi
    mov $10,%rdx
    syscall

    mov $1,%rax
    mov $1,%rdi
    mov $space,%rsi
    mov $10,%rdx
    syscall
    
    mov $3,%rax
    mov %r8,%rdi
    syscall
    
    mov $60,%rax
    mov $0,%rdi
    syscall
```

## `[延伸閱讀|read-around|Further reading|Weiterlesen|Lectures complémentaires]`
   - Mixing C and Assembly Language 用組合語言寫函數,再用C程式呼叫此函數
   - Command Line Arguments 撰寫帶有指令參數的程式
