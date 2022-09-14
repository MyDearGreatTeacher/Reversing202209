#

## 核心觀念與範例說明
- 以一個(最簡單的)範例說明angr解題的核心觀念與技術
- [](https://github.com/angr/angr-doc/blob/master/docs/toplevel.md)
```
Top Level Interfaces
Loading a Binary
Solver Engine
Program State
Simulation Managers
Execution Engines
Analyses
```

### 測試環境建置:

- 在 Google Colab建置angr ==> !pip install angr
- 安裝學習範例 1 ==>!git clone https://github.com/FSecureLABS/z3_and_angr_binary_analysis_workshop.git 
- 安裝學習範例 2:下載angr-doc/examples的許多範例  ==>!git clone https://github.com/angr/angr-doc.git
- 再使用linux指令執行
```
ls
cd z3_and_angr_binary_analysis_workshop

ls
cd ..


python3 xxxxx.py
```

- 註解:同學 可以在github建立你的目錄  讓助教下載並執行你的解答 以便 驗證你的解答
- 建議:建立底下目錄結構(不要太多層)
```
- readme.md  ==> 解題總綱
- [題目1]
  - readme.md ==> 題目敘述與解題writeup
  - binary1 ==> 你要逆向的執行檔
- [題目2]
  - readme.md ==> 題目敘述與解題writeup
  - binary2 ==> 你要逆向的執行檔
```


## 範例說明1:ais3_crackme

## 
- 切換到案例/examples/ais3_crackme
- 檢視有多少檔案 ==> ais3_crackme  solve.py
- 檢視解答 ==> cat solve.py
- 執行 ==> python3 solve.py
- 答案 ==> 

### [Angr官方解法](https://github.com/angr/angr-doc/blob/master/examples/ais3_crackme/solve.py)
```python
#!/usr/bin/env python


'''
ais3_crackme has been developed by Tyler Nighswander (tylerni7) for ais3.
It is an easy crackme challenge. It checks the command line argument.
'''

import angr
import claripy


def main():
    project = angr.Project("./ais3_crackme")

    #create an initial state with a symbolic bit vector as argv1
    argv1 = claripy.BVS("argv1",100*8) #since we do not the length now, we just put 100 bytes
    initial_state = project.factory.entry_state(args=["./crackme1",argv1])

    #create a path group using the created initial state 
    sm = project.factory.simulation_manager(initial_state)

    #symbolically execute the program until we reach the wanted value of the instruction pointer
    sm.explore(find=0x400602) #at this instruction the binary will print(the "correct" message)

    found = sm.found[0]
    #ask to the symbolic solver to get the value of argv1 in the reached state as a string
    solution = found.solver.eval(argv1, cast_to=bytes)

    print(repr(solution))
    solution = solution[:solution.find(b"\x00")]
    print(solution)
    return solution

def test():
    res = main()
    assert res == b"ais3{I_tak3_g00d_n0t3s}"


if __name__ == '__main__':
    print(repr(main()))
```
## 範例說明2 

- 切換到案例/examples/defcon2016quals_baby-re
- 檢視有多少檔案 ==> baby-re*  solve.py
- 檢視解答 ==> cat solve.py
- 執行 ==> python3 solve.py
- 答案 ==> Math is hard!

```python
#!/usr/bin/env python2
from __future__ import print_function

# Authors: David Manouchehri <manouchehri@protonmail.com>
#          P1kachu <p1kachu@lse.epita.fr>
#          Audrey Dutcher <audrey@rhelmot.io>
# DEFCON CTF Qualifier 2016
# Challenge: baby-re
# Write-up: http://hack.carleton.team/2016/05/21/defcon-ctf-qualifier-2016-baby-re/
# Runtime: ~15 seconds (thanks lazy solves!)

import angr
import claripy

def main():
    proj = angr.Project('./baby-re', auto_load_libs=False)

    # let's provide the exact variables received through the scanf so we don't have to worry about parsing stdin into a bunch of ints.
    flag_chars = [claripy.BVS('flag_%d' % i, 32) for i in range(13)]
    class my_scanf(angr.SimProcedure):
        def run(self, fmt, ptr): # pylint: disable=arguments-differ,unused-argument
            self.state.mem[ptr].dword = flag_chars[self.state.globals['scanf_count']]
            self.state.globals['scanf_count'] += 1

    proj.hook_symbol('__isoc99_scanf', my_scanf(), replace=True)

    sm = proj.factory.simulation_manager()
    sm.one_active.options.add(angr.options.LAZY_SOLVES)
    sm.one_active.globals['scanf_count'] = 0

    # search for just before the printf("%c%c...")
    # If we get to 0x402941, "Wrong" is going to be printed out, so definitely avoid that.
    sm.explore(find=0x4028E9, avoid=0x402941)

    # evaluate each of the flag chars against the constraints on the found state to construct the flag
    flag = ''.join(chr(sm.one_found.solver.eval(c)) for c in flag_chars)
    return flag

def test():
    assert main() == 'Math is hard!'

if __name__ == '__main__':
    print(main())
```

## 參考簡報
- [資料來源SymbolicExecution](https://github.com/jakespringer/angr_ctf/blob/master/SymbolicExecution.pptx)

- Representation of Symbols: Bitvectors
- [資料來源](https://github.com/jakespringer/angr_ctf/blob/master/SymbolicExecution.pptx)
- Angr’s symbols are represented by what it calls bitvectors.
- Bitvectors have a size, the number of bits they represent.
- As with all data in programming, bitvectors can represent any type that can fit. Most commonly, they represent either n-bit integers or strings.
- The difference between a bitvector and a typical variable is that, while typical variables store a single value, bitvectors store every value that meet certain constraints.
