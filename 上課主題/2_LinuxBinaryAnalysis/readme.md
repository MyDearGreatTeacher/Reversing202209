# agenda
```
2_1_ELF Format and analysis

2_2_Linux Tools for Binary Analysis

2_3_dynamic binary analysis and static analysis

2_4_Memory Layout of C Programs
```

# ELF 檔案格式與分析
```
Linking view vs Execution view
ELF 檔案的類型
ELF 檔案格式與分析
可執行檔的載入
```

## 實作練習_ELF檔案格式分析


# 參考書籍與推薦章節

 - [[教科書Practical Binary Analysis: Build Your Own Linux Tools for Binary Instrumentation, Analysis, and Disassembly,Dennis Andriesse]](https://www.tenlong.com.tw/products/9781593279127) [[Github]](https://github.com/wilvk/practical-binary) [[官方網站:下載ova及code]](https://practicalbinaryanalysis.com/)

- [Binary Analysis Cookbook By Michael Born(2019)](https://www.packtpub.com/product/binary-analysis-cookbook/9781789807608) [[GITHUB]](https://github.com/PacktPublishing/Binary-Analysis-Cookbook)
```
1.Setting Up the Lab
2.32-bit Assembly on Linux and the ELF Specification
3.64-bit Assembly on Linux and the ELF Specification
4.Creating a Binary Analysis Methodology
5.Linux Tools for Binary Analysis

6.Analyzing a Simple Bind Shell(32bit)
7.Analyzing a Simple Reverse Shell
8.Identifying Vulnerabilities
9.Understanding Anti-Analysis Techniques
10.A Simple Reverse Shell With Polymorphism
```
### 4.Creating a Binary Analysis Methodology
```
Technical requirements
Performing binary discovery
Information gathering
Static analysis
Dynamic analysis
Iterating each step
Automating methodology tasks
Adapting the methodology steps
```

# Advanced Binary Analysis
### Taint Analysis 
- [Taint checking](https://en.wikipedia.org/wiki/Taint_checking)
- [Taint Analysis簡報](https://www.cs.cmu.edu/~ckaestne/15313/2018/20181023-taint-analysis.pdf)

- 污點檢驗是某些程序語言所擁有的特性，例如Perl[1]和Ruby[2]，可用於增加安全性和避免惡意用戶在主機上執行命令。
- 污點會檢驗突出的安全風險，一般來說這些風險與那些使用SQL注入或緩衝區溢出攻擊的網站相關。
- 污點檢驗的原理是任何變量（例如在網頁表單區域的一個變量集）能夠被外部用戶修改，從而造成了潛在的安全危險。
- 如果該變量被一個表達式賦值給第二個變量，那麼第二變量也是可疑的。
- 污點檢驗工具在變量間傳遞運行，直到外部輸入潛在地影響到所有的變量。
- 如果這些變量中任何一個變量被用於執行危險命令（例如對SQL資料庫或主機作業系統的直接命令），污點檢檢驗工具將警告該程序正在使用有潛在危險的污點變量。程式設計師可以通過重新設計程序來避免因危險的輸入而導致的安全問題。
- 污點檢驗能夠被視為一個無界面全面驗證的保守近似或者是更一般化的安全信息流[3]概念。
- 因為系統中的信息流不能通過檢驗一個簡單的執行追蹤而被驗證，污點分析的結果將必然地反映關於該系統信息流特徵的近似信息
