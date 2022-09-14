1_Symbolic Execution.md


## Z3
- Z3 Theorem Prover is a cross-platform satisfiability modulo theories (SMT) solver by Microsoft.
- 2007  2012
- Z3 was developed in the Research in Software Engineering (RiSE) group at Microsoft Research and is targeted at solving problems that arise in software verification and software analysis. Z
- 3 supports arithmetic, fixed-size bit-vectors, extensional arrays, datatypes, uninterpreted functions, and quantifiers. 
- Its main applications are extended static checking, test case generation, and predicate abstraction.
- In 2015, it received the Programming Languages Software Award from ACM SIGPLAN.
- In 2018, Z3 received the Test of Time Award from the European Joint Conferences on Theory and Practice of Software (ETAPS).
- Microsoft researchers Nikolaj Bjørner and Leonardo de Moura received the 2019 Herbrand Award for Distinguished Contributions to Automated Reasoning in recognition of their work in advancing theorem proving with Z3.
- Z3 was open sourced in the beginning of 2015.
- The source code is licensed under MIT License and hosted on GitHub.
- The solver can be built using Visual Studio, a Makefile or using CMake and runs on Windows, FreeBSD, Linux, and macOS.
- It has bindings for various programming languages including C, C++, Java, Julia, Haskell, OCaml, Python, WebAssembly, and .NET/Mono. 
- The default input format is SMTLIB2.

- [Z3 Theorem Prover](https://en.wikipedia.org/wiki/Z3_Theorem_Prover)
- [原始論文Z3: An Efficient SMT Solver(2008)](https://link.springer.com/content/pdf/10.1007%2F978-3-540-78800-3_24.pdf)
- [相關論文](https://github.com/Z3Prover/z3/wiki/Publications)
- [官方GITHUB](https://github.com/Z3Prover)


## Z3環境搭建
- pip install z3-solver
- [Z3求解器簡介及環境搭建](https://blog.csdn.net/guo_shaokun/article/details/99891545?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162904945016780262523657%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=162904945016780262523657&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-5-99891545.pc_search_result_control_group&utm_term=z3&spm=1018.2226.3001.4187)

- [online Z3 練習環境jfmc's Z3 Playground](https://jfmc.github.io/z3-play/)

## Z3 Tutorial
- [Z3 Tutorial.ipynb](https://colab.research.google.com/github/philzook58/z3_tutorial/blob/master/Z3%20Tutorial.ipynb#scrollTo=DkSVZpVaK5KB)
- [Tutorials and Summer Schools](https://github.com/Z3Prover/z3/wiki/Slides)
- [Z3求解器基本指南](https://blog.csdn.net/weixin_39408343/article/details/102680614?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162904945016780262523657%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=162904945016780262523657&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-102680614.pc_search_result_control_group&utm_term=z3&spm=1018.2226.3001.4187)
- [Symbolic Fuzzing](https://www.fuzzingbook.org/html/SymbolicFuzzer.html)
- [Practical Symbolic Execution and SATisfiability Module Theories (SMT) 101(2019)](https://www.gushiciku.cn/pl/2n7j/zh-tw)
- [Symbolic Analysis with Python and Z3(2019)](https://secretlab.institute/2019/08/09/symbolic-analysis-with-python-and-z3/)
- [FORMAL METHODS FOR THE INFORMAL ENGINEER: TUTORIAL #1 - THE Z3 THEOREM PROVER(2019)Broad Institute of MIT and Harvard(2021)](https://www.youtube.com/watch?v=56IIrBZy9Rc)
- [Programming Z3](https://theory.stanford.edu/~nikolaj/programmingz3.html)
- [The Varied Forms of Verification with Z3|2016 Microsoft Research](https://www.youtube.com/watch?v=wHSmAThRBHg)
- [Z3_wiki](https://github.com/Z3Prover/z3/wiki)
- [PyExZ3](https://github.com/thomasjball/PyExZ3)
## 工作原理
- [The inner magic behind the Z3 theorem prover(2019)](https://www.microsoft.com/en-us/research/blog/the-inner-magic-behind-the-z3-theorem-prover/)

## Solving CTF challenges using Z3
- [Z3 Python CTF](https://github.com/ViRb3/z3-python-ctf)
- [Z3 API in Python](https://ericpony.github.io/z3py-tutorial/guide-examples.htm)
