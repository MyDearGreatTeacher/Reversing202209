# FASM @ Windows



## 範例程式 Mastering-Assembly-Programming/Chapter02/FASM/fasm1win.asm
```fasm
   include 'win32a.inc'

   format PE GUI
   entry _start

   section '.text' code readable executable
   _start:
	   push    0
	   push    0
	   push    title
	   push    message
	   push    0
	   call    [MessageBox]
	   call    [ExitProcess]

   section '.data' data readable writeable
	   message db	'Hello from FASM!', 0x00
	   title   db	'Hello!', 0x00

   section '.idata' import data readable writeable

   library kernel, 'kernel32.dll',\
	   user, 'user32.dll'

   import kernel,\
	  ExitProcess, 'ExitProcess'

   import user,\
	  MessageBox, 'MessageBoxA'
```

## Mastering-Assembly-Programming/Chapter03/template_win.asm
```fasm
   
; File: src\template_win.asm

; First of all, we tell the compiler which type of executable we want it to be. In our case it is a 32-bit PE executable.
format PE GUI

; Tell the compiler where we want our program to start - define the entry point. We want it to be at the place labeled with '_start'.
entry _start

; The following line includes a set of macros, shipped with FASM, which are essential for Windows program. We can, of course, implement all we need ourselves, and we will do that in chapter 9.
include 'win32a.inc'

; PE file consists of at least one section. In this template we only need 3:
;    1. '.text' - section that contains executable code
;    2. '.data' - section that contains data
;    3. '.idata' - section that contains import information
;
; '.text' section: contains code, is readable, is executable
section '.text' code readable executable

; Entry point
_start:

   ;
   ; Put your code here
   ;


   ; We have to terminate the process properly
   ; Put return code on stack
   push  0
   ; Call ExitProcess Windows API function
   call [exitProcess]

; '.data' section: contains data, is readable, may be writeable
section '.data' data readable writeable
   ;
   ; Put your data here
   ;

; '.idata' section: contains import information, is readable, is writeable
section '.idata' import data readable writeable

; 'library' macro from 'win32a.inc' creates proper entry for importing functions from a dynamic link library. For now it is only 'kernel32.dll'.
library kernel, 'kernel32.dll'

; 'import' macro creates the actual entries for functions we want to import from a dynamic link library
import kernel, 
   exitProcess, 'ExitProcess'
```
