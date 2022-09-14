# Z3 API in Python

- [Z3 API in Python](https://ericpony.github.io/z3py-tutorial/guide-examples.htm)
- [[Z3 API in PYTHON Basics中文文档]](https://arabelatso.github.io/2018/06/14/Z3%20API%20in%20Python/)
- 原文版分成四大段落:Basics + Strategies + Fixpoints+ Advanced
- 底下僅列出基本Basics 在Google Colab環境的測試

- [官方GITHUB網址](https://github.com/Z3Prover/z3)
  - z3/examples/python有一些python程式範例

## Google Colab環境
```
!pip install z3-solver
```

## comments註解:不支持跨越多行的註解
```python
from z3 import *

# This is a comment
x = Real('x') # comment: creating x
print(x**2 + 2*x + 2)  # comment: printing polynomial
```

## 解不等式
```
from z3 import *

x = Int('x')
y = Int('y')
solve(x > 2, y < 10, x + 2*y == 7) 
```
- [y = 0, x = 7] 
- 呼叫 solve 函數求解三個條件下的滿足模型，這三個條件分別是 x 大於 2，y 小於 10，並且 x 加 2 個 y 等於 7
- Z3 在預設情況下，只尋找滿足所有條件的一組解，而不是找出所有解
- [y = 5, x = 1] 

- Int 可不是 C/C++ 裡面包含上下界的 int，
- Z3 中的 Int 對應的就是數學中的整數，Z3 中的 BitVector 才對應到 C/C++ 中的 int

## z3/examples/python/example.py
```python
from z3 import *

x = Real('x')
y = Real('y')
s = Solver()
s.add(x + y > 5, x > 1, y > 1)
print(s.check())
print(s.model())
```
```
<b>sat</b>
[y = 2, x = 4]
```

## [方程式簡化](https://ericpony.github.io/z3py-tutorial/guide-examples.htm)  
```python

#!/usr/bin/env python3

from z3 import *

x = Int('x')
y = Int('y')
#print(simplify(x + y + 2*x + 3))
#print(simplify(x < y + x + 2))
print(simplify(And(x + 1 >= 3, x**2 + x**2 + y**2 + 2 >= 5)))
```

## 運算式分析:Z3提供遍歷運算式的函數
```python
from z3 import *

x = Int('x')
y = Int('y')
n = x + y >= 3
print("num args: ", n.num_args())
print("children: ", n.children())
print("1st child:", n.arg(0))
print("2nd child:", n.arg(1))
print("operator: ", n.decl())
print("op name:  ", n.decl().name())
```
```
num args:  2
children:  [x + y, 3]
1st child: x + y
2nd child: 3
operator:  &ge;
op name:   >=
```

## 解非線性多項式約束
```python
from z3 import *

x = Real('x')
y = Real('y')
solve(x**2 + y**2 > 3, x**3 + y < 5)
```

```
[y = 2, x = 1/8]
```

## 使用set_option設定Z3環境: 實數運算的精準度 

- set_option用於設置全域配置選項，如結果如何顯示。
- 選項set_option(precision = 30)設置顯示結果時使用的小數位數
- 解答中以?來代表輸出被截斷

```python
from z3 import *

x = Real('x')
y = Real('y')
solve(x**2 + y**2 == 3, x**3 == 2)

set_option(precision=30)
print("Solving, and displaying result with 30 decimal places")
solve(x**2 + y**2 == 3, x**3 == 2)
```
```
[y = -1.1885280594?, x = 1.2599210498?]
Solving, and displaying result with 30 decimal places
[y = -1.188528059421316533710369365015?,
 x = 1.259921049894873164767210607278?]
```

##

```python
from z3 import *

x = Real('x')
solve(3*x == 1)

set_option(rational_to_decimal=True)
solve(3*x == 1)

set_option(precision=30)
solve(3*x == 1)
```

## 無解答的約束系統
- 約束系統也可能沒有解決方案。 在這種情況下，我們說這個系統是不可滿足的。
```python
from z3 import *

x = Real('x')
solve(x > 4, x < 0)
```

```
no solution
```

## 解布林運算式
```python
from z3 import *

p = Bool('p')
q = Bool('q')
r = Bool('r')
solve(Implies(p, q), r == Not(q), Or(Not(p), r))
```
```
[q = True, p = False, r = False]
```

## 求解多項式和布林約束
```python

from z3 import *

p = Bool('p')
x = Real('x')
solve(Or(x < 5, x > 10), Or(p, x**2 == 2), Not(p))
```

```
[x = -1.414213562373095048801688724209?, p = False]
```

## BitVector

- [Z3 API](https://z3prover.github.io/api/html/namespacez3py.html)

```python
def z3py.BitVecs	(	 	names,
 	bv,
 	ctx = None 
)		

Return a tuple of bit-vector constants of size bv

x, y, z = BitVecs('x y z', 16)

x.size()
```
