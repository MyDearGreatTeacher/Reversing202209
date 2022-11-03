# 期中考報告(11.7晚上會錄影說明)
```
檔案名稱: 學號_逆向工程_期中考報告
簡報標題: 逆向工程核心語法(組合語言)報告
Agenda:
1.逆向工程
2.Linux C 程式開發:編譯與組譯
3.Linux ELF 分析
4.計算機系統與組合語言
  Intel/AMD架構 vs ARM 架構
  組合語言語法格式: AT&T vs INTEL
  32位元計算機與64位元計算機
    - registers
  32位元組合語言與64位元組合語言
    - Function calling convention 
5.NASM 組合語言架構
6.NASM 組合語言開發
 32位元NASM 組合語言範例
 64位元NASM 組合語言範例
7.NASM 組合語言實戰(以分析的程式技術與數量評分):教科書程式碼的錄影(下周)
8.Assembly-CTF 解題
```
# 龍大大錄影
- [NASM與組合語言開發入門](https://youtu.be/1aWERf19I5A)
- [編譯與組譯](https://youtu.be/oWugDwITzLg)
- [Linux ELF 分析](https://youtu.be/gjcgiL0i02Q)


### 教科書Assembly Programming and Computer Architecture for Software Engineers(2017) 
- [簡中譯本:匯編程序設計與電腦體系結構：軟件工程師教程](https://www.tenlong.com.tw/products/9787111615163) 
- [GITHUB(原始碼)](https://github.com/brianrhall/Assembly)
- 以x86與x86_64這兩種主流架構為重點
- 兼顧AT&T及Intel語法，
- 適用於GAS、NASM及MASM三種常見的匯編器
- Linux、macOS及Windows三種常用的操作系統，

### Chapter 3: Assembly and Syntax Fundamentals
- [Program 3.1 Sample Assembly Program](https://github.com/brianrhall/Assembly/blob/master/Chapter_3/Program%203.1/x86_64/Program_3.1_NASM.asm)
- Program 3.2
### Chapter 4: Basic Instructions
- Program 4.1
- Program 4.2
- Program 4.3
- Program 4.4
### Chapter 5: Intermediate Instructions
- [Program 5.1 Conditional Jump](https://github.com/brianrhall/Assembly/blob/master/Chapter_5/Program%205.1/x86_64/Program_5.1_NASM.asm)
- [Program 5.2 Looping](https://github.com/brianrhall/Assembly/blob/master/Chapter_5/Program%205.2/x86_64/Program_5.2_NASM.asm)
- [Program 5.3 Nested for Loop](https://github.com/brianrhall/Assembly/blob/master/Chapter_5/Program%205.3/x86_64/Program_5.3_NASM.asm)
- [Program 5.4 while Loop](https://github.com/brianrhall/Assembly/blob/master/Chapter_5/Program%205.4/x86_64/Program_5.4_NASM.asm)
### Chapter 6: Functions
- Program 6.1 Sum Program
- Program 6.2 C++
- Program 6.3 Sum Program
### Chapter 7: String Instructions & Structures
- Program 7.1
- Program 7.2
