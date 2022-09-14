# The Ghidra Book_The Definitive Guide 學習筆記
```
這是學習筆記  學習時間斷斷續續,沒有長時間專注   怕忘了,所以記錄重點與代辦事項
```
- [官方網站(含有程式碼可下載)+ 可網路購買電子書](https://ghidrabook.com/l)

- Chapter 1: Introduction to Disassembly

- Chapter 2: Reversing and Disassembly Tools
  - Classification Tools == > file |  PE Tools | PEiD 
  - Summary Tools == >   nm | ldd | objdump | otool(macOS) | dumpbin(Windows) | c++filt
    - dumpbin /dependents C:\Windows\System32\notepad.exe 
  - Deep Inspection Tools == > strings | Disassemblers [ndisasm and diStorm]

- Chapter 3: Meet Ghidra
  - The Ghidra Directory Layout 目錄結構
    - Extensions ==>  Contains useful prebuilt extensions and important content and information for writing Ghidra extensions. 
    - Ghidra  ==>   Contains the code for Ghidra.  

- Chapter 4: Getting Started with Ghidra  基本操作
  - 先啟動專案  File => New Project  ==> 注意專案路徑
  - 載入檔案 File => Import File
  - Ghidra Import Results Summary window
  - Ghidra CodeBrowser window
  - The Analysis Options dialog(分析的各種選項)
  - Ghidra Help=>About
  - import summary information


- Chapter 5: Ghidra Data Displays


- Chapter 6: Making Sense of a Ghidra Disassembly
- Chapter 7: Disassembly Manipulation
- Chapter 8: Data Types and Data Structures
- Chapter 9: Cross-References
- Chapter 10: Graphs
- Chapter 11: Collaborative SRE with Ghidra
  - 多人協同分析 
  - 使用Ghidra Server 

- Chapter 12: Customizing Ghidra
  - CodeBrowser
  - Ghidra Project Window
  - Tools
    - Ghidra Configure Tool window 
  - Workspaces

- Chapter 13: Extending Ghidra’s Worldview
  - a highquality reverse engineering tool ==> fully automated identification and annotation of as much of a binary as possible. 
  - How to identify various constructs within binaries and discuss how you can enhance its ability to do so.
  - Importing Files
    - Figure 13-1: Import dialog and options for a PE file Figure 
    - Figure 13-2: Import dialog and options for an ELF binary
    - Figure 13-4: Import Results Summary window for an ELF binary
  - Analyzers
  - Word Models 特殊字串
    - A word model provides a way to identify special strings and types of strings you’re interested in searching for, such as known identifiers, email addresses, directory pathnames, file extensions, and so on. 
  - Data Types
    - The Data Type Manager allows us to manage all of the data types associated with a file. 
    - Ghidra lets you reuse data type definitions by storing them in data type archive files. 
  - Function IDs
    - Figure 13-9: Auto analysis options 選項中有 Function IDs
  - Function ID Plugin
    - allows you to create, modify, and control associations for FidDbs. 
    - 預設為不啟動 
    - 啟動方式 ==> 點選  CodeBrowser window => File=>Configure and then click the checkbox for Function ID. 
  - Function ID Plugin Example: UPX


- Chapter 14: Basic Ghidra Scripting
  - Script Manager
  - Script Development
    - 使用java
    - 使用python
    - Support for Other Languages ? 那些啊?
  - Introduction to the Ghidra API
  - Ghidra Scripting Examples
    - Example 1: Enumerating Functions- 
    - Example 2: Enumerating Instructions
    - Example 3: Enumerating Cross-References
    - Example 4: Finding Function Calls
    - Example 5: Emulating Assembly Language Behavior

- Chapter 15: Eclipse and GhidraDev

- Chapter 16: Ghidra in Headless Mode
  - Ghidra has a command line interface called the Ghidra headless analyzer
  - analyzeHeadless command
    - analyzeHeadless D:\GhidraProjects CH16 -import global_array_demo_x64
    - analyzeHeadless D:\GhidraProjects CH16 -import D:\ch16
    - analyzeHeadless D:\GhidraProjects CH16 -import global_array_demo_x64 -log D:\GhidraProjects\CH16-logs\CH16-Logfile
  - Writing Scripts


- Chapter 17: Ghidra Loaders 檔案載入器
  - Unknown File Analysis
  - Manually Loading a Windows PE File
  - Example 1: SimpleShellcode Loader Module
  - Example 2: Simple Shellcode Source Loader
  - Example 3: Simple ELF Shellcode Loader


- Chapter 18: Ghidra Processors
- Chapter 19: The Ghidra Decompiler
  - Ghidra Decompiler analysis options 
- Chapter 20: Compiler Variations

- Chapter 21: Obfuscated Code Analysis 重要!
  - binary 保護技術 linux binary protection   ==>  Anti–Reverse Engineering
    - [Strike/Counter-Strike: Reverse Engineering Shiva - Black Hat](https://www.blackhat.com/presentations/bh-federal-03/bh-federal-03-eagle/bh-fed-03-eagle.pdf)
    - Linux ELF 保護軟體 ==> [Shiva 2003:Advances in ELF Binary Encryption - Black Hat](https://www.blackhat.com/presentations/bh-usa-03/bh-us-03-mehta/bh-us-03-mehta.pdf)
    - [Armouring the ELF: Binary encryption on the UNIX platform](https://grugq.github.io/docs/phrack-58-05.txt)
  - Deobfuscation of Binaries Using Ghidra

- Chapter 22: Patching Binaries 重要!

- 執行檔修正的情境
  - Modifying a malware sample to eliminate anti-debug techniques that prevent the malware from being studied
  - Patching vulnerabilities in software for which you have no source code
  - Customizing an application’s splash screen or string content
  - Modifying game logic for the purposes of cheating
  - Unlocking hidden features
  - Bypassing licensing checks or other anti-piracy protections
- 執行檔修正的做法與步驟
  - The Search Memory dialog
  - 使用 Byte Viewer修改
    - The Ghidra Byte Viewer (Window =>Bytes)

- Chapter 23: Binary Differencing and Version Tracking 重要!
  - 兩個惡意程式是否相似 或同一家族 ?
  - 有多少相似?多少差異?
  - Tools => Program Differences
  - The Version Tracking tool
    - 原理 
    - Seven types of correlators [At a high level, the Version Tracking tool is looking for correlations between two files.]
      - Data Match correlators
      - Function Match correlators
      - Legacy Import correlators
      - Implied correlators
      - Manual Match correlators
      - Symbol Name Match correlators
      - Reference correlators 

- Appendix: Ghidra for IDA Users
