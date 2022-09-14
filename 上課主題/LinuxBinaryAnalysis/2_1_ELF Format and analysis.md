# 檔案格式

| 系統 |檔案格式 |
|-----|------|
| Linux | [ELF](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format) |
|Windows |[PE Format(Windows)](https://docs.microsoft.com/en-us/windows/win32/debug/pe-format)|
|macOS, and iOS |[Mach-o](https://en.wikipedia.org/wiki/Mach-O)|


# ELF_Format:Analysis
```
ELF 檔案
ELF 檔案類型
ELF 檔案結構
檢視ELF 檔案  ==> readelf 
```

# ELF 檔案 == Executable and Linkable Format
- Linux 系統上所運行的就是ELF 格式的檔案
- 定義在"/usr/include/elf.h"檔案
- [ELF 各結構定義在 elf.h](https://github.com/torvalds/linux/blob/master/include/uapi/linux/elf.h)
- [The ELF Specification](http://sco.com/developers/gabi/latest/contents.html)
- [ELF man page:整理的不錯](http://manpages.courier-mta.org/htmlman5/elf.5.html)
- [In-depth: ELF - The Extensible & Linkable Format(2020)](https://www.youtube.com/watch?v=nC1U1LJQL8o)

# ELF 檔案類型 ==> 三種類型 + 核心轉儲檔案(Core Dump file) 

 - 可重定位檔案(relocatable file) 
   - 由原始檔案編譯而成且尚未連結的目的檔案
   - 通常以'.o" 作為副檔名。
   - 用於與其他目的檔案進行連結以組成可執行檔或動態連結程式庫
   - 通常是一段位置獨立的程式(Position Independent Code, PIC) 
 - 可執行檔（Executable File）
   - 經過連結的、可執行的目的檔案
   - 通常也被稱為程式。
 - 共用目的檔案(shared object file)
   - 動態連結程式庫檔案
   - 用於連結的程式碼和資料
   - 可在連結過程中與其他動態連結程式庫或可重定位檔案一起建構新的目的檔案
   - 或在可執行檔載入時，連結到處理程序中作為運行程式的一部分。
   - libc-2.2X.so

  - 核心轉儲檔案(Core Dump file) 
    - 作為處理程序意外終止時處理程序位址空間的轉儲，也是ELF 檔案的—種
    - 使用gdb讀取造種檔案可以輔助偵錯和尋找程式崩潰的原因。

# [範例程式:資料來源](https://firmianay.gitbooks.io/ctf-all-in-one/content/doc/1.5.3_elf.html)
```
# elfDemo.c
#include <stdio.h>

int global_init_var =10;
int global_uninit_var;

void func(int sum){
  printf ("%d\n", sum);
}

void main (void){ 
  static int local_static_init_var = 20;
  static int local_static_uninit_var;
  int local_init_val = 30;
  int local_uninit_var;
  func(global_init_var + local_init_val + local_static_init_var);
}
```

## 編譯成64-bit[使用Ubuntu 18.04/20,04 LTS or Kali_201902]
```
$ gcc elfDemo.c -o elf Demo.exec
$ gcc -static elfDemo.c -o elfDemo_static.exec
$ gcc -e elfDemo.c -o elfDemo.rel
$ gcc -e -fPIC elfDemo.c -o elfDemo_pie.rel && gcc -shared elfDemo_pie.rel -o elfDemo.dyn

# 執行檔(.exec)  可重定位檔案(.rel)  共用目的檔案(.dyn)
```
## DEMO
```
使用 ldd 命令檢視所依賴的共用函式庫  ==> ldd elfDemo.out
                                   ==>  ldd elfDemo_static.out   ==> see what happen and why?
使用 file 命令查看相應的檔案格式 ==> file elfDemo.rel
```

# ELF 檔案結構 : Linking view vs execution view
 - [ELF@Wiki](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format)
 - [Anatomy of an ELF Part 1: The Header](https://coolbyte.eu/2017/anatomy-elf-part-1-header/)

|名稱 |說明 |
|------- | -------------- |
|ELF 標頭頭（ELF Header）| 在目的檔案格式的最前面，包含了描述整個檔的基本屬性。|
|程式標頭表（Program Header Table）| 可選的，它告訴系統怎樣創建一個行程映射。可執行檔必須有程式頭表，而重定位檔不需要。|
| 段（Section） | 包含了`連結視圖Linking view`中大量的目的檔案資訊。|
| 段標頭表（Section Header Table）| 包含了描述檔中所有`段（Section）`的資訊。|

## 分析ELF的工具
- 使用python
  - [pwntools|pwnlib.elf](https://docs.pwntools.com/en/stable/elf.html) 
  - [pyelftools](https://github.com/eliben/pyelftools)
- 使用rust
  - [elf-parser](https://github.com/finixbit/elf-parser)
- 使用linux Tools:readelf, objdump 

## 使用readelf 檢視ELF  也可以使用 使用objdump 檢視ELF

|名稱|說明|readelf 檢視|
| -------|-------------------------|-------------|
| ELF header (Ehdr)| 在目的檔案格式的最前面，包含了描述整個檔的基本屬性 | readelf -h elfDemo.out |
| Program header (Phdr)  |  |  readelf -l elfDemo.out |
| Section Header Table |  | readelf -S elfDemo.o |
| .strtab == 字串表（Strings Table） |  | readelf -x .strtab elfDemo.o    |
| .shstrtab === 段表字串表（Section Header String Table） |  |  readelf -x .shstrtab elfDemo.o |
| 符號表symbol tables (Elf32/64_Sym)  Symbol table '.symtab' | An object file's symbol table holds information needed to locate and relocate a program's symbolic definitions and references | readelf -s elfDemo.o |
| 重定位表 Elf32/64_Rel|  | readelf -r elfDemo.o |


```
Usage: readelf <option(s)> elf-file(s)
 Display information about the contents of ELF format files
 Options are:
  -a --all               Equivalent to: -h -l -S -s -r -d -V -A -I
  -h --file-header       Display the ELF file header
  -l --program-headers   Display the program headers
     --segments          An alias for --program-headers
  -S --section-headers   Display the sections' header
     --sections          An alias for --section-headers
  -g --section-groups    Display the section groups
  -t --section-details   Display the section details
  -e --headers           Equivalent to: -h -l -S
  -s --syms              Display the symbol table
     --symbols           An alias for --syms
  --dyn-syms             Display the dynamic symbol table
  
  
  -n --notes             Display the core notes (if present)
  -r --relocs            Display the relocations (if present)
  -u --unwind            Display the unwind info (if present)
  -d --dynamic           Display the dynamic section (if present)
  -V --version-info      Display the version sections (if present)
  -A --arch-specific     Display architecture specific information (if any)
  -c --archive-index     Display the symbol/file index in an archive
  
  -D --use-dynamic       Use the dynamic section info when displaying symbols
  
  -x --hex-dump=<number|name>
                         Dump the contents of section <number|name> as bytes
  -p --string-dump=<number|name>
                         Dump the contents of section <number|name> as strings
  -R --relocated-dump=<number|name>
                         Dump the contents of section <number|name> as relocated bytes
                         
  -z --decompress        Decompress section before dumping it
  -w[lLiaprmfFsoRtUuTgAckK] or
  --debug-dump[=rawline,=decodedline,=info,=abbrev,=pubnames,=aranges,=macro,=frames,
               =frames-interp,=str,=loc,=Ranges,=pubtypes,
               =gdb_index,=trace_info,=trace_abbrev,=trace_aranges,
               =addr,=cu_index,=links,=follow-links]
                         Display the contents of DWARF debug sections
  --dwarf-depth=N        Do not display DIEs at depth N or greater
  --dwarf-start=N        Display DIEs starting with N, at the same depth
                         or deeper
  -I --histogram         Display histogram of bucket list lengths
  -W --wide              Allow output width to exceed 80 characters
  @<file>                Read options from <file>
  -H --help              Display this information
  -v --version           Display the version number of readelf
```
### 檢視 Section Headers

```
readelf --sections --wide /bin/bash
There are 29 section headers, starting at offset 0x11ce48:

Section Headers:
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .interp           PROGBITS        00000000000002a8 0002a8 00001c 00   A  0   0  1
  [ 2] .note.ABI-tag     NOTE            00000000000002c4 0002c4 000020 00   A  0   0  4
  [ 3] .note.gnu.build-id NOTE            00000000000002e4 0002e4 000024 00   A  0   0  4
  [ 4] .gnu.hash         GNU_HASH        0000000000000308 000308 004aa8 00   A  5   0  8
  [ 5] .dynsym           DYNSYM          0000000000004db0 004db0 00e400 18   A  6   1  8
  [ 6] .dynstr           STRTAB          00000000000131b0 0131b0 009728 00   A  0   0  1
  [ 7] .gnu.version      VERSYM          000000000001c8d8 01c8d8 001300 02   A  5   0  2
  [ 8] .gnu.version_r    VERNEED         000000000001dbd8 01dbd8 0000d0 00   A  6   3  8
  [ 9] .rela.dyn         RELA            000000000001dca8 01dca8 00dc80 18   A  5   0  8
  [10] .rela.plt         RELA            000000000002b928 02b928 001470 18  AI  5  24  8
  [11] .init             PROGBITS        000000000002d000 02d000 000017 00  AX  0   0  4
  [12] .plt              PROGBITS        000000000002d020 02d020 000db0 10  AX  0   0 16
  [13] .plt.got          PROGBITS        000000000002ddd0 02ddd0 000018 08  AX  0   0  8
  [14] .text             PROGBITS        000000000002ddf0 02ddf0 0ac991 00  AX  0   0 16
  [15] .fini             PROGBITS        00000000000da784 0da784 000009 00  AX  0   0  4
  [16] .rodata           PROGBITS        00000000000db000 0db000 019930 00   A  0   0 32
  [17] .eh_frame_hdr     PROGBITS        00000000000f4930 0f4930 0044c4 00   A  0   0  4
  [18] .eh_frame         PROGBITS        00000000000f8df8 0f8df8 017938 00   A  0   0  8
  [19] .init_array       INIT_ARRAY      00000000001123f0 1113f0 000008 08  WA  0   0  8
  [20] .fini_array       FINI_ARRAY      00000000001123f8 1113f8 000008 08  WA  0   0  8
  [21] .data.rel.ro      PROGBITS        0000000000112400 111400 0028f0 00  WA  0   0 32
  [22] .dynamic          DYNAMIC         0000000000114cf0 113cf0 000200 10  WA  6   0  8
  [23] .got              PROGBITS        0000000000114ef0 113ef0 000100 08  WA  0   0  8
  [24] .got.plt          PROGBITS        0000000000115000 114000 0006e8 08  WA  0   0  8
  [25] .data             PROGBITS        0000000000115700 114700 008604 00  WA  0   0 32
  [26] .bss              NOBITS          000000000011dd20 11cd04 009c78 00  WA  0   0 32
  [27] .gnu_debuglink    PROGBITS        0000000000000000 11cd04 000034 00      0   0  4
  [28] .shstrtab         STRTAB          0000000000000000 11cd38 00010a 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  l (large), p (processor specific)
```
### Execution view: Program Header Table (PHT)
```
readelf -l --wide /bin/bash

Elf file type is DYN (Shared object file)
Entry point 0x2f630
There are 11 program headers, starting at offset 64

Program Headers:
  Type           Offset   VirtAddr           PhysAddr           FileSiz  MemSiz   Flg Align
  PHDR           0x000040 0x0000000000000040 0x0000000000000040 0x000268 0x000268 R   0x8
  INTERP         0x0002a8 0x00000000000002a8 0x00000000000002a8 0x00001c 0x00001c R   0x1
      [Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
  LOAD           0x000000 0x0000000000000000 0x0000000000000000 0x02cd98 0x02cd98 R   0x1000
  LOAD           0x02d000 0x000000000002d000 0x000000000002d000 0x0ad78d 0x0ad78d R E 0x1000
  LOAD           0x0db000 0x00000000000db000 0x00000000000db000 0x035730 0x035730 R   0x1000
  LOAD           0x1113f0 0x00000000001123f0 0x00000000001123f0 0x00b914 0x0155a8 RW  0x1000
  DYNAMIC        0x113cf0 0x0000000000114cf0 0x0000000000114cf0 0x000200 0x000200 RW  0x8
  NOTE           0x0002c4 0x00000000000002c4 0x00000000000002c4 0x000044 0x000044 R   0x4
  GNU_EH_FRAME   0x0f4930 0x00000000000f4930 0x00000000000f4930 0x0044c4 0x0044c4 R   0x4
  GNU_STACK      0x000000 0x0000000000000000 0x0000000000000000 0x000000 0x000000 RW  0x10
  GNU_RELRO      0x1113f0 0x00000000001123f0 0x00000000001123f0 0x002c10 0x002c10 R   0x1

 Section to Segment mapping:
  Segment Sections...
   00     
   01     .interp 
   02     .interp .note.ABI-tag .note.gnu.build-id .gnu.hash .dynsym .dynstr .gnu.version .gnu.version_r .rela.dyn .rela.plt 
   03     .init .plt .plt.got .text .fini 
   04     .rodata .eh_frame_hdr .eh_frame 
   05     .init_array .fini_array .data.rel.ro .dynamic .got .got.plt .data .bss 
   06     .dynamic 
   07     .note.ABI-tag .note.gnu.build-id 
   08     .eh_frame_hdr 
   09     
   10     .init_array .fini_array .data.rel.ro .dynamic .got 
```

## 不同SECTIONS的說明

## `[實作練習|pratice|s'entraîner|üben|관행|práctica]`
 
  - strip or Not-strip: this is a test
  - 教科書1.2 Symbols and Stripped Binaries
  
| strip or not | test |
|-------- |  ---------|
|Not-strip | readelf --syms a.out|
|stripped  | strip --strip-all a.out  |
|  | file a.out  |
|  | readelf --syms a.out |


## 教科書 Practical Binary Analysis
 - [[教科書Practical Binary Analysis: Build Your Own Linux Tools for Binary Instrumentation, Analysis, and Disassembly,Dennis Andriesse]](https://www.tenlong.com.tw/products/9781593279127) [[Github]](https://github.com/wilvk/practical-binary) [[官方網站:下載ova及code]](https://practicalbinaryanalysis.com/)
   - chapter 2: THE ELF FORMAT(Executable and Linkable Format (ELF))

## `[實作練習|pratice|s'entraîner|üben|관행|práctica]`
- [Advanced C and C++ Compiling  Milan Stevanovic/Apress 高級C/C++編譯技術(2014)](https://www.books.com.tw/products/CN11244082)
  - 第3章 加載程序執行階段
 
## `[延伸閱讀|read-around|Further reading|Weiterlesen|Lectures complémentaires]`
 - [[教科書Practical Binary Analysis: Build Your Own Linux Tools for Binary Instrumentation, Analysis, and Disassembly,Dennis Andriesse]](https://www.tenlong.com.tw/products/9781593279127) [[Github]](https://github.com/wilvk/practical-binary) [[官方網站:下載ova及code]](https://practicalbinaryanalysis.com/)
   - chapter 3: THE PE FORMAT[Portable Executable (PE)]
   - write c/c++ using visual studio community or dev-c++
   - examine PE structure using tools(What tools? Googling them!)
   - examine PE structure using python
   - demo what you can find


## Midterm 30% 報告主題 Windows Binary Analysis
