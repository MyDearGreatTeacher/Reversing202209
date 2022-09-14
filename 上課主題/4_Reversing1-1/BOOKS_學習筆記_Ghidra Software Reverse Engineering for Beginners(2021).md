## [Ghidra Software Reverse Engineering for Beginners(2021)](https://www.packtpub.com/product/ghidra-software-reverse-engineering-for-beginners/9781800207974) [[GITHUB]](https://github.com/PacktPublishing/Ghidra-Software-Reverse-Engineering-for-Beginners)
```
## Section 1: Introduction to Ghidra
## Chapter 1: Getting Started with Ghidra
## Chapter 2: Automating RE Tasks with Ghidra Scripts
Chapter 3: Ghidra Debug Mode
Chapter 4: Using Ghidra Extensions

```
## Section 2: Reverse Engineering  先讀此章節

## Chapter 5: Reversing Malware Using Ghidra 找時間try看看

- 惡意程式相本Alina malware 
- Alina malware consists of two components: a Windows driver (rt.sys) and a Portable Executable (park.exe). 
  - see a compressed Ghidra project (alina_ghidra_project.zip) 
  - Alina is a Point of Sale Malware or POS RAM Scraper that is used by cybercriminals to scrape credit card and debit card information from the point of sale system.
  - It first started to scrape information in late 2012. 
  - It resembles JackPOS Malware
- [YOUTUBE Ghidra Software Reverse Engineering for Beginners| 5. Reversing Malware Using Ghidra](https://www.youtube.com/watch?v=4A4t7l6g710)
- [Alina, the Latest POS Malware(2017)](https://www.pandasecurity.com/en/mediacenter/pandalabs/alina-pos-malware/)

- Ghidra vulnerabilities
  - CVE-2019-17664
  - CVE-2019-17665 

- 分析內容與步驟
  - Looking for strings
  - Intelligence information and external sources
  - Checking import functions   ==> Ghidra's CodeBrowser Symbol Tree window 
    - ADVAPI32.DLL 
    - KERNEL32.DLL
  - Dissecting interesting malware sample parts


## Chapter 6: Scripting Malware Analysis
- Using the Ghidra scripting API
- Writing scripts using the Java programming language
- Writing scripts using the Python programming language
- Deobfuscating malware samples using scripts

- [Ghidra Software Reverse Engineering for Beginners| 6. Scripting Malware Analysis](https://www.youtube.com/watch?v=0LxBpNHZ6tc)


```
Chapter 7: Using Ghidra Headless Analyzer
Chapter 8: Auditing Program Binaries
Chapter 9: Scripting Binary Audits

## Section 3: Extending Ghidra
Chapter 10: Developing Ghidra Plugins
Chapter 11: Incorporating New Binary Formats
Chapter 12: Analyzing Processor Modules
Chapter 13: Contributing to the Ghidra Community
Chapter 14: Extending Ghidra for Advanced Reverse Engineering
```
