# [A Survey of Symbolic Execution Techniques](https://arxiv.org/pdf/1610.00502.pdf)

- [Warm-Up](#Warm-Up)
- [Challenges in Symbolic Execution](#Challenges)
- [SYMBOLIC EXECUTION ENGINES](#SYMBOLIC_EXECUTION_ENGINES)

## Warm-Up

## Challenges
- Memory
  - how does the symbolic engine handle pointers, arrays, or other complex objects?
  - Code manipulating pointers and data structures may give rise not only to symbolic stored data, but also to addresses being described by symbolic expressions.

- Environment: 
  - how does the engine handle interactions across the software stack? 
  - Calls to library and system code can cause side effects, e.g., the creation of a file or a call back to user code, that could later affect the execution and must be accounted for. 
  - However, evaluating any possible interaction outcome may be unfeasible.

- State space explosion: 
  - how does symbolic execution deal with path explosion? 
  - Language constructs such as loops might exponentially increase the number of execution states. 
  - It is thus unlikely that a symbolic execution engine can exhaustively explore all the possible states within a reasonable amount of time.

- Constraint solving: 
  - what can a constraint solver do in practice? 
  - SMT solvers can scale to complex combinations of constraints over hundreds of variables. 
  - However, constructs such as non-linear arithmetic pose a major obstacle to efficiency

## SYMBOLIC_EXECUTION_ENGINES

### classical symbolic execution
  - [Symbolic Execution for Software Testing: Three Decades Later(2013)](https://people.eecs.berkeley.edu/~ksen/papers/cacm13.pdf)

### Modern Symbolic Execution Techniques

- One of the key elements of modern symbolic execution techniques is their ability to mix concrete and symbolic execution

- Concolic Testing: 
  - [Directed Automated Random Testing(DART, 2005)](https://web.eecs.umich.edu/~weimerw/590/reading/p213-godefroid.pdf) [[PPT]](http://www.cs.toronto.edu/~geri/doc/GeriGrolingerCSC2125Report.pdf)
  - Concolic testing 
```
K. Sen and G. Agha. 
CUTE and jCUTE : Concolic unit testing and explicit path model-checking tools. In CAV’06, 2006.
```  
  - performs symbolic execution dynamically, while the program is executed on some concrete input values. 
  - Concolic testing maintains a concrete state and a symbolic state: 
    - the concrete state maps all variables to their concrete values; 
    - the symbolic state only maps variables that have non-concrete values.

- Execution-Generated Testing (EGT): 
  - The EGT approach
  - EXE 
  - [KLEE](https://klee.github.io/) 
  - making a distinction between the concrete and symbolic state of a program. 
  - To this end, EGT intermixes concrete and symbolic execution by dynamically checking before every operation

```
C. Cadar, D. Dunbar, and D. Engler. 
KLEE: Unassisted and automatic generation of high-coverage tests for complex systems programs. In OSDI’08, Dec 2008
```
### concolic execution


## S²E
```
Vitaly Chipounov, Volodymyr Kuznetsov, and George Candea. 2012. 
The S2E Platform: Design, Implementation, and Applications. 
ACM Trans. on Computer Systems (TOCS) 30, 1 (2012), 2:1–2:49. https://doi.org/10.1145/2110356.2110358
```
- [S²E: A Platform for In-Vivo Analysis of Software Systems](http://s2e.systems/)

## KLEE

##
- [哈佛大學 CS 252r: Advanced Topics in Programming Languages]()

## 參考資料

```
] Corina S. Pasareanu and Willem Visser. 2009. 
A Survey of New Trends in Symbolic Execution for Software Testing and Analysis. 
Int. Journal on Software Tools for Technology Transfer 11, 4 (2009), 339–353. https://doi.org/10.1007/s10009-009-0118-1
```
```
Cristian Cadar and Koushik Sen. 2013. 
Symbolic Execution for Software Testing: Three Decades Later. 
Commun. ACM 56, 2 (2013), 82–90. https://doi.org/10.1145/2408776.2408795
```

```
Ting Chen, Xiao-Song Zhang, Shi-Ze Guo, Hong-Yuan Li, and Yue Wu. 2013. 
State of the Art: Dynamic Symbolic Execution for Automated Test Generation. 
Future Gen. Comput. Syst. 29, 7 (2013), 1758–1773. https://doi.org/10.1016/j.future.2012.02.006
```

```
A Survey of Symbolic Execution Techniques
Roberto Baldoni, Emilio Coppa, Daniele Cono D'Elia, Camil Demetrescu, Irene Finocchi
https://arxiv.org/abs/1610.00502
```

- [Automated Test Generation using Symbolic Execution](https://www.coursera.org/lecture/automated-analysis/automated-test-generation-using-symbolic-execution-lRd2c)
