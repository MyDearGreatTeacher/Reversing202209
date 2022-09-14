# 組合語言CTF解題
```
pico-ctf-2014 :basic-asm-60
angstromCTF 2016:asm-tracing-45
PicoCTF2018-assembly-0
PicoCTF-2021/Let's get dynamic
```

## pico-ctf-2014 reverse-engineering/basic-asm-60
```
pico-ctf-2014
reverse-engineering/basic-asm-60

We found this program snippet.txt, but we're having some trouble figuring it out. 
What's the value of %eax when the last instruction (the NOP) runs?
```

```
# This file is in AT&T syntax - see http://www.imada.sdu.dk/Courses/DM18/Litteratur/IntelnATT.htm
# and http://en.wikipedia.org/wiki/X86_assembly_language#Syntax. Both gdb and objdump produce
# AT&T syntax by default.

MOV $10814,%ebx
MOV $2972,%eax
MOV $10017,%ecx
CMP %eax,%ebx
JL L1
JMP L2
L1:
IMUL %eax,%ebx
ADD %eax,%ebx
MOV %ebx,%eax
SUB %ecx,%eax
JMP L3
L2:
IMUL %eax,%ebx
SUB %eax,%ebx
MOV %ebx,%eax
ADD %ecx,%eax
L3:
NOP
```
```
https://github.com/VulnHub/ctf-writeups/blob/master/2014/picoctf/basic-asm.md

https://ehsan.dev/pico2014/reverse_engineering/basic_asm.html
```

## angstromCTF 2016 : asm-tracing-45
```
Reading assembly language is one of the core skills for reverse engineering. 
Test your abilities by tracing this code and seeing what %eax contains by the end! 
Enter the result as an unsigned decimal integer.

# This ASM is AT&T syntax: http://www.imada.sdu.dk/Courses/DM18/Litteratur/IntelnATT.htm
# All the GNU tools (as, gdb, and objdump) use AT&T syntax by default
start:
	mov $1337, %eax
	mov $6098, %ebx
	mov $4352, %ecx
	xor %edx, %edx
	
	sub %ecx, %ebx
	cmp %ebx, %eax
	jge next1
	jmp next2
next1:
	cmp $4, %edx
	jg end
	inc %edx
next2:
	xchg %eax, %ebx
	idiv %ebx
	add %edx, %eax
	imul %ecx
	jmp next1
end:
```
## PicoCTF2018-assembly-0
```
Reversing 150: assembly-0
Challenge

What does asm0(0xd8,0x7a) return? Submit the flag as a hexadecimal value (starting with 0x).

NOTE: Your submission for this question will NOT be in the normal flag format. 
Source located in the directory at /problems/assembly-0_1_fc43dbf0079fd5aab87236bf3bf4ac63.
```
```
.intel_syntax noprefix
.bits 32
	
.global asm0

asm0:
	push	ebp
	mov	ebp,esp
	mov	eax,DWORD PTR [ebp+0x8]
	mov	ebx,DWORD PTR [ebp+0xc]
	mov	eax,ebx
	mov	esp,ebp
	pop	ebp	
	ret
```
## PicoCTF-2021/Let's get dynamic
```
Can you tell what this file is reading? chall.S

chall.S
```

```
https://github.com/HHousen/PicoCTF-2021/tree/master/Reverse%20Engineering/Let's%20get%20dynamic
```
```
	.file	"chall.c"
	.text
	.section	.rodata
	.align 8
.LC0:
	.string	"Correct! You entered the flag."
.LC1:
	.string	"No, that's not right."
	.text
	.globl	main
	.type	main, @function
main:
.LFB5:
	.cfi_startproc
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	pushq	%rbx
	subq	$296, %rsp
	.cfi_offset 3, -24
	movl	%edi, -292(%rbp)
	movq	%rsi, -304(%rbp)
	movq	%fs:40, %rax
	movq	%rax, -24(%rbp)
	xorl	%eax, %eax
	movabsq	$4137700413143496212, %rax
	movabsq	$3668774195188830448, %rdx
	movq	%rax, -144(%rbp)
	movq	%rdx, -136(%rbp)
	movabsq	$-3415231997387159298, %rax
	movabsq	$3180240096696696075, %rdx
	movq	%rax, -128(%rbp)
	movq	%rdx, -120(%rbp)
	movabsq	$-5717177924950513641, %rax
	movabsq	$-3967246834314051972, %rdx
	movq	%rax, -112(%rbp)
	movq	%rdx, -104(%rbp)
	movw	$97, -96(%rbp)
	movabsq	$6214777055764401527, %rax
	movabsq	$8184225536171504527, %rdx
	movq	%rax, -80(%rbp)
	movq	%rdx, -72(%rbp)
	movabsq	$-8364134581669616439, %rax
	movabsq	$5916610601309242417, %rdx
	movq	%rax, -64(%rbp)
	movq	%rdx, -56(%rbp)
	movabsq	$-2598080388612165765, %rax
	movabsq	$-4252370736625094538, %rdx
	movq	%rax, -48(%rbp)
	movq	%rdx, -40(%rbp)
	movw	$63, -32(%rbp)
	movq	stdin(%rip), %rdx
	leaq	-208(%rbp), %rax
	movl	$49, %esi
	movq	%rax, %rdi
	call	fgets@PLT
	movl	$0, -276(%rbp)
	jmp	.L2
.L3:
	movl	-276(%rbp), %eax
	cltq
	movzbl	-144(%rbp,%rax), %edx
	movl	-276(%rbp), %eax
	cltq
	movzbl	-80(%rbp,%rax), %eax
	xorl	%eax, %edx
	movl	-276(%rbp), %eax
	xorl	%edx, %eax
	xorl	$19, %eax
	movl	%eax, %edx
	movl	-276(%rbp), %eax
	cltq
	movb	%dl, -272(%rbp,%rax)
	addl	$1, -276(%rbp)
.L2:
	movl	-276(%rbp), %eax
	movslq	%eax, %rbx
	leaq	-144(%rbp), %rax
	movq	%rax, %rdi
	call	strlen@PLT
	cmpq	%rax, %rbx
	jb	.L3
	leaq	-272(%rbp), %rcx
	leaq	-208(%rbp), %rax
	movl	$49, %edx
	movq	%rcx, %rsi
	movq	%rax, %rdi
	call	memcmp@PLT
	testl	%eax, %eax
	je	.L4
	leaq	.LC0(%rip), %rdi
	call	puts@PLT
	movl	$0, %eax
	jmp	.L6
.L4:
	leaq	.LC1(%rip), %rdi
	call	puts@PLT
	movl	$1, %eax
.L6:
	movq	-24(%rbp), %rcx
	xorq	%fs:40, %rcx
	je	.L7
	call	__stack_chk_fail@PLT
.L7:
	addq	$296, %rsp
	popq	%rbx
	popq	%rbp
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE5:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
```
```
Step 1. Compiling

    gcc -g chall.S -o chall
    
Step 2. Reverse engineering using Ghidra

Step 3. Debugging with GDB
```
