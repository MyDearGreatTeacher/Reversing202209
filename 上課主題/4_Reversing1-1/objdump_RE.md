# objdump技術實戰
- [objdump](#objdump)
- [objdump指令參數](#objdump指令參數)
- [objdump反組譯範例](#objdump反組譯範例)
- [CTF解題](#CTF解題)

## [objdump]()
- objdump is a command-line program for displaying various information about object files on Unix-like operating systems.
- it can be used as a disassembler to view an executable in assembly form. 
- It is part of the GNU Binutils for fine-grained control over executables and other binary data. 
- objdump uses the BFD library to read the contents of object files.
- 常用應用
  - 1.使用objdump 檢視ELF
    - objdump -h elfDemo.o ==> 使用 objdump 來查看目的檔案的內部結構
    - objdump -x -s -d elfDemo.o  ==> 檢視 Sections
      - .data 段 ==> 保存已經初始化了的全域變數和局部靜態變數
      - .rodata 段  ==> 保存唯讀資料，包括唯讀變數和字串常量
      - .bss 段 ==> 保存未初始化的全域變數和局部靜態變數
      - Contents of section .text:      =====> .text 的程式的十六進位形式
      - Disassembly of section .text:   =====> .text 程式反組譯(assembly程式)
  - 2.objdump 反組譯 [本節重點]

## objdump指令參數
- objdump -D -M intel file.bin | grep main.: -A20
```
objdump --help
Usage: objdump <option(s)> <file(s)>
 Display information from object <file(s)>.
 At least one of the following switches must be given:
  -a, --archive-headers    Display archive header information
  -f, --file-headers       Display the contents of the overall file header
  -p, --private-headers    Display object format specific file header contents
  -P, --private=OPT,OPT... Display object format specific contents
  -h, --[section-]headers  Display the contents of the section headers
  -x, --all-headers        Display the contents of all headers
  -d, --disassemble        Display assembler contents of executable sections
  -D, --disassemble-all    Display assembler contents of all sections
  -S, --source             Intermix source code with disassembly
  -s, --full-contents      Display the full contents of all sections requested
  -g, --debugging          Display debug information in object file
  -e, --debugging-tags     Display debug information using ctags style
  -G, --stabs              Display (in raw form) any STABS info in the file
  -W[lLiaprmfFsoRtUuTgAckK] or
  --dwarf[=rawline,=decodedline,=info,=abbrev,=pubnames,=aranges,=macro,=frames,
          =frames-interp,=str,=loc,=Ranges,=pubtypes,
          =gdb_index,=trace_info,=trace_abbrev,=trace_aranges,
          =addr,=cu_index,=links,=follow-links]
                           Display DWARF info in the file
  -t, --syms               Display the contents of the symbol table(s)
  -T, --dynamic-syms       Display the contents of the dynamic symbol table
  -r, --reloc              Display the relocation entries in the file
  -R, --dynamic-reloc      Display the dynamic relocation entries in the file
  @<file>                  Read options from <file>
  -v, --version            Display this program's version number
  -i, --info               List object formats and architectures supported
  -H, --help               Display this information

 The following switches are optional:
  -b, --target=BFDNAME           Specify the target object format as BFDNAME
  -m, --architecture=MACHINE     Specify the target architecture as MACHINE
  -j, --section=NAME             Only display information for section NAME
  -M, --disassembler-options=OPT Pass text OPT on to the disassembler
  -EB --endian=big               Assume big endian format when disassembling
  -EL --endian=little            Assume little endian format when disassembling
      --file-start-context       Include context from start of file (with -S)
  -I, --include=DIR              Add DIR to search list for source files
  -l, --line-numbers             Include line numbers and filenames in output
  -F, --file-offsets             Include file offsets when displaying information
  -C, --demangle[=STYLE]         Decode mangled/processed symbol names
                                  The STYLE, if specified, can be `auto', `gnu',
                                  `lucid', `arm', `hp', `edg', `gnu-v3', `java'
                                  or `gnat'
  -w, --wide                     Format output for more than 80 columns
  -z, --disassemble-zeroes       Do not skip blocks of zeroes when disassembling
      --start-address=ADDR       Only process data whose address is >= ADDR
      --stop-address=ADDR        Only process data whose address is <= ADDR
      --prefix-addresses         Print complete address alongside disassembly
      --[no-]show-raw-insn       Display hex alongside symbolic disassembly
      --insn-width=WIDTH         Display WIDTH bytes on a single line for -d
      --adjust-vma=OFFSET        Add OFFSET to all displayed section addresses
      --special-syms             Include special symbols in symbol dumps
      --inlines                  Print all inlines for source line (with -l)
      --prefix=PREFIX            Add PREFIX to absolute paths for -S
      --prefix-strip=LEVEL       Strip initial directory names for -S
      --dwarf-depth=N        Do not display DIEs at depth N or greater
      --dwarf-start=N        Display DIEs starting with N, at the same depth
                             or deeper
      --dwarf-check          Make additional dwarf internal consistency checks.      

objdump: supported targets: 
      elf64-x86-64 elf32-i386 elf32-iamcu elf32-x86-64 pei-i386 pei-x86-64 
      elf64-l1om elf64-k1om elf64-little elf64-big elf32-little elf32-big 
      pe-x86-64 pe-bigobj-x86-64 pe-i386 plugin srec symbolsrec verilog tekhex binary ihex
objdump: supported architectures: 
      i386 i386:x86-64 i386:x64-32 i8086 i386:intel i386:x86-64:intel i386:x64-32:intel i386:nacl 
      i386:x86-64:nacl i386:x64-32:nacl iamcu iamcu:intel l1om l1om:intel k1om k1om:intel plugin

反組譯常用參數
The following i386/x86-64 specific disassembler options are supported for use
with the -M switch (multiple options should be separated by commas):
  x86-64      Disassemble in 64bit mode
  i386        Disassemble in 32bit mode
  i8086       Disassemble in 16bit mode
  att         Display instruction in AT&T syntax
  intel       Display instruction in Intel syntax
  att-mnemonic
              Display instruction in AT&T mnemonic
  intel-mnemonic
              Display instruction in Intel mnemonic
  addr64      Assume 64bit address size
  addr32      Assume 32bit address size
  addr16      Assume 16bit address size
  data32      Assume 32bit data size
  data16      Assume 16bit data size
  suffix      Always display instruction suffix in AT&T syntax
  amd64       Display instruction in AMD64 ISA
  intel64     Display instruction in Intel64 ISA
Report bugs to <http://www.sourceware.org/bugzilla/>.
```
## objdump反組譯範例
－ 逆向工程技術 -d  -M -j -S參數

### 範例程式  
```
// helloCTFer.c
#include <stdio.h>

int main()
{
   printf("Hello CTFer\n ”);
   return 0;
}
```
## 測試下列結果

| 測試 | 說明結果  |
|------ | -------- |
|gcc helloCTFer.c -o helloCTFer -g|編譯程式|
|objdump -d helloCTFer |預設使用 AT&T 語法格式|
|objdump -d -M intel helloCTFer| 指定使用intel 語法格式|
|objdump -d -j .text -M intel helloCTFer ||
|objdump -d -j .text -M intel helloCTFer --no-show-raw-insn  ||
|objdump -S helloCTFer ||
|objdump -S -M intel helloCTFer||
|objdump -S -j .text -M intel helloCTFer ||
|objdump -S -j .text -M intel helloCTFer --no-show-raw-insn  ||

## CTF解題
### EasyCTF 2017_LuckyGuess 
#### [參考解答1](https://github.com/ss8651twtw/Reverse-CTF-writeups/tree/main/EasyCTF_LuckyGuess)
- 使用objdump 反組譯會發現有使用rand 
- 查看rand 語法
- 撰寫rand
```c
#include <stdlib.h>

int rand(void) {
	return 0;
}
```
- 編譯與執行 ==> 使用LD_PRELOAD
```
gcc -fPIC -shared -o hook.so ./hook.c -ldl
echo 0 | LD_PRELOAD=./hook.so ./LuckyGuess
```
#### 解法2: binary Patch see Ghidra_RE

- [InCTF Junior　blade](https://medium.com/@amustaque97/demystify-reverse-engineering-ctf-challenge-blade-40c45e7933c0)
- [easyCTF-2018-Adder](https://github.com/asinggih/easyCTF-2018-writeups/blob/master/Reverse_Engineering/Adder.md)
