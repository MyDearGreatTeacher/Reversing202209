# 使用z3求解CTF

- [PicoCTF2013_Harder_Serial](#PicoCTF2013_Harder_Serial)
- [HSCTF_2019_A Byte](#HSCTF_2019_A_Byte)
  - [解法1:使用z3](https://guyinatuxedo.github.io/12-z3/hs19_abyte/index.html)
  - [解法2](https://github.com/zst-ctf/hsctf-2019-writeups/tree/master/Solved/A_Byte)
- [Tokyo Westerns CTF 2017: rev_rev_rev]()
  - [解法1:使用z3](https://guyinatuxedo.github.io/12-z3/tokyowesterns17_revrevrev/index.html) 
- [TUCTF_2017_future]()
  - [解法1:使用z3](https://guyinatuxedo.github.io/12-z3/tuctf_future/index.html) 
- [DEFCAMP_2017_Misc_forgot_my_key](#DEFCAMP_2017_Misc_forgot_my_key)
- [CSAW_2017_realism](#CSAW_2017_realism)


## PicoCTF2013_Harder_Serial

- [題目改編自CTF all in one](https://firmianay.gitbooks.io/ctf-all-in-one/content/doc/5.8.1_z3.html)

```
序號破解器
底下Python程式碼要求輸入一段 20 個數字構成的序號，
然後程式會對序號的每一位進行驗證，以滿足各種要求
請問此序號為多少?
```
```python
import sys

print ("Please enter a valid serial number from your RoboCorpIntergalactic purchase")

if len(sys.argv) < 2:
  print ("Usage: %s [serial number]"%sys.argv[0])
  exit()

print ("#>" + sys.argv[1] + "<#")

def check_serial(serial):
  if (not set(serial).issubset(set(map(str,range(10))))):
    print ("only numbers allowed")
    return False
  if len(serial) != 20:
    return False
  if int(serial[15]) + int(serial[4]) != 10:
    return False
  if int(serial[1]) * int(serial[18]) != 2:
    return False
  if int(serial[15]) / int(serial[9]) != 1:
    return False
  if int(serial[17]) - int(serial[0]) != 4:
    return False
  if int(serial[5]) - int(serial[17]) != -1:
    return False
  if int(serial[15]) - int(serial[1]) != 5:
    return False
  if int(serial[1]) * int(serial[10]) != 18:
    return False
  if int(serial[8]) + int(serial[13]) != 14:
    return False
  if int(serial[18]) * int(serial[8]) != 5:
    return False
  if int(serial[4]) * int(serial[11]) != 0:
    return False
  if int(serial[8]) + int(serial[9]) != 12:
    return False
  if int(serial[12]) - int(serial[19]) != 1:
    return False
  if int(serial[9]) % int(serial[17]) != 7:
    return False
  if int(serial[14]) * int(serial[16]) != 40:
    return False
  if int(serial[7]) - int(serial[4]) != 1:
    return False
  if int(serial[6]) + int(serial[0]) != 6:
    return False
  if int(serial[2]) - int(serial[16]) != 0:
    return False
  if int(serial[4]) - int(serial[6]) != 1:
    return False
  if int(serial[0]) % int(serial[5]) != 4:
    return False
  if int(serial[5]) * int(serial[11]) != 0:
    return False
  if int(serial[10]) % int(serial[15]) != 2:
    return False
  if int(serial[11]) / int(serial[3]) != 0:
    return False
  if int(serial[14]) - int(serial[13]) != -4:
    return False
  if int(serial[18]) + int(serial[19]) != 3:
    return False
  return True

if check_serial(sys.argv[1]):
  print ("Thank you! Your product has been verified!")
else:
  print ("I'm sorry that is incorrect. Please use a valid RoboCorpIntergalactic serial number")
```

### [解答](https://firmianay.gitbooks.io/ctf-all-in-one/content/doc/5.8.1_z3.html)

```python
from z3 import *

solver = Solver()

serial = [Int("serial[%d]" % i) for i in range(20)]

solver.add(serial[15] + serial[4]  == 10)
solver.add(serial[1]  * serial[18] == 2 )
solver.add(serial[15] / serial[9]  == 1)
solver.add(serial[17] - serial[0]  == 4)
solver.add(serial[5]  - serial[17] == -1)
solver.add(serial[15] - serial[1]  == 5)
solver.add(serial[1]  * serial[10] == 18)
solver.add(serial[8]  + serial[13] == 14)
solver.add(serial[18] * serial[8]  == 5)
solver.add(serial[4]  * serial[11] == 0)
solver.add(serial[8]  + serial[9]  == 12)
solver.add(serial[12] - serial[19] == 1)
solver.add(serial[9]  % serial[17] == 7)
solver.add(serial[14] * serial[16] == 40)
solver.add(serial[7]  - serial[4]  == 1)
solver.add(serial[6]  + serial[0]  == 6)
solver.add(serial[2]  - serial[16] == 0)
solver.add(serial[4]  - serial[6]  == 1)
solver.add(serial[0]  % serial[5]  == 4)
solver.add(serial[5]  * serial[11] == 0)
solver.add(serial[10] % serial[15] == 2)
solver.add(serial[11] / serial[3]  == 0)    # serial[3] can't be 0
solver.add(serial[14] - serial[13] == -4)
solver.add(serial[18] + serial[19] == 3)

for i in range(20):
    solver.add(serial[i] >= 0, serial[i] < 10)

solver.add(serial[3] != 0)

if solver.check() == sat:
    m = solver.model()
    for d in m.decls():
        print("%s = %s" % (d.name(), m[d]))

    print("".join([str(m.eval(serial[i])) for i in range(20)]))
```
## HSCTF_2019_A_Byte
```
Free arbitrary null write primitive, get the flag

nc pwn.hsctf.com 6666  <==已經不能連過去

Binary updated without breaking changes: 
5223e3fe7827c664a5adc5e0fa6f2c0ced8abaaf byte
```
- [題目](https://github.com/zst-ctf/hsctf-2019-writeups/blob/master/Solved/A_Byte/a-byte)
- [HSCTF ("High School Capture the Flag")](https://hsctf.com/)

### [逆向分析:資料來源](https://guyinatuxedo.github.io/12-z3/hs19_abyte/index.html)

### [解答:資料來源](https://guyinatuxedo.github.io/12-z3/hs19_abyte/index.html)
```python
from z3 import *

# Designate the desired output
desiredOutput = [0x69, 0x72, 0x62, 0x75, 0x67, 0x7a, 0x76, 0x31, 0x76, 0x5e, 0x78, 0x31, 0x74, 0x5e, 0x6a, 0x6f, 0x31, 0x76, 0x5e, 0x65, 0x35, 0x5e, 0x76, 0x40, 0x32, 0x5e, 0x39, 0x69, 0x33, 0x63, 0x40, 0x31, 0x33, 0x38, 0x7c]


# Designate the input z3 will have control of
inp = []
for i in xrange(0x23):
    byte = BitVec("%s" % i, 8)
    inp.append(byte)

z = Solver()

for i in xrange(0x23):
    z.add((inp[i] ^ 1) == desiredOutput[i])


#Check if z3 can solve it, and if it can print out the solution
if z.check() == sat:
#	print z
    print "Condition is satisfied, would still recommend crying: " + str(z.check())
    solution = z.model()
    flag = ""
    for i in range(0, 0x23):
        flag += chr(int(str(solution[inp[i]])))
    print flag

#Check if z3 can't solve it
elif z.check() == unsat:
    print "Condition is not satisfied, would recommend crying: " + str(z.check())

```
## DEFCAMP_2017_Misc_forgot_my_key
- [資料來源](https://zhuanlan.zhihu.com/p/30548907)
```
I forgot my flag & key. 
Help me recover them.

5616f5962674d26741d2810600a6c5647620c4e3d2870177f09716b2379012c342d3b584c5672195d653722443f1c39254360007010381b721c741a532b03504d2849382d375c0d6806251a2946335a67365020100f160f17640c6a05583f49645d3b557856221b2
```
```
<?php
/* 
	5616f5962674d26741d2810600a6c5647620c4e3d2870177f09716b2379012c342d3b584c5672195d653722443f1c39254360007010381b721c741a532b03504d2849382d375c0d6806251a2946335a67365020100f160f17640c6a05583f49645d3b557856221b2
*/

function my_encrypt($flag, $key) {
	$key = md5($key);
	$message = $flag . "|" . $key;

	$encrypted = chr(rand(0, 126));
	for($i=0;$i<strlen($message);$i++) {
		$encrypted .= chr((ord($message[$i]) + ord($key[$i % strlen($key)]) + ord($encrypted[$i])) % 126);
	}
	$hexstr = unpack('h*', $encrypted);
	return array_shift($hexstr);
}

?>
```
### 解答
```
#!/usr/bin/env python3

from z3 import *
import binascii

s = '5616f5962674d26741d2810600a6c5647620c4e3d2870177f09716b2379012c342d3b584c5672195d653722443f1c39254360007010381b721c741a532b03504d2849382d375c0d6806251a2946335a67365020100f160f17640c6a05583f49645d3b557856221b2'

encrypted = []
for i in range(0, len(s), 2):
    encrypted.append(binascii.unhexlify(s[i+1] + s[i])[0])

print('message len:', len(encrypted)-1)
print(encrypted)

# 聲明變數，encrypted 是已知，因此 IntVal 即可
encrypted = [IntVal(i) for i in encrypted]
message = [Int('flag%d' % i) for i in range(len(encrypted)-1)]
# 創建一個求解器，求解全靠它
solver = Solver()

ml = len(encrypted) - 1

# 添加明文字元的約束條件
for i in range(ml):
    if i == ml - 33:
        solver.add(message[i] == ord('|'))
    else:
        # 肯定是可見字元，因此限定範圍如下
        solver.add(message[i] < 127)
        solver.add(message[i] >= 32)
# 添加明文和密文對照關係的約束條件
for i in range(ml):
    solver.add(encrypted[i+1] == (message[i] + message[ml-32+i%32] + encrypted[i]) % 126)

if solver.check() == sat:
    m = solver.model()
    s = []
    for i in range(ml):
        s.append(m[message[i]].as_long())
    print(bytes(s))
else:
    print('unsat') 
```
##  CSAW_2017_realism

- [資料來源](https://zhuanlan.zhihu.com/p/30548907)
### 逆向分析

```
xmm5 = results[0]

for i in range(8, 0, -1):
    xmm2 = andps(flag, bytes(masks[i:i+8]))
    xmm5 = psadbw(xmm5, xmm2)
    assert xmm5 == results[9-i] 
```
### 使用z3求解
- [解答1](https://gist.github.com/zTrix/036d904e85946fa273067f184210a6de)
```python
#!/usr/bin/env python3

from z3 import *

def int2bytes(a: int) -> bytes:
    return a.to_bytes(16, byteorder='little')

def combine128(a, b):
    return (a << 64) | b

def edx2xmm5(e):
    return combine128(e & 0xffff, (e & 0xffff0000) >> 16)

xmm5_results = [
    0x220f02c883fbe083c0200f10cd0013b8,
    edx2xmm5(0x02df028f),
    edx2xmm5(0x0290025d),
    edx2xmm5(0x02090221),
    edx2xmm5(0x027b0278),
    edx2xmm5(0x01f90233),
    edx2xmm5(0x025e0291),
    edx2xmm5(0x02290255),
    edx2xmm5(0x02110270),
]

# Z3 Solve here

def int2bitvecval(x):
    return [BitVecVal(i, 16) for i in int2bytes(x)]

def andps_z3(a, b):
    assert len(a) == len(b) == 16
    r = []
    for i in range(16):
        r.append(a[i] & b[i])
    return r

def abs_z3(x):
    return If(x >= 0, x, -x)

def psadbw_z3(a, b):
    assert len(a) == len(b) == 16
    t = [BitVecVal(0, 16) for _ in range(16)]
    for i in range(16):
        t[i] = abs_z3(a[i] - b[i])

    s1 = Sum(t[0:8])
    s2 = Sum(t[8:])
    r = [BitVecVal(0, 16) for _ in range(16)]
    r[0] = s1 % BitVecVal(256,16)
    r[1] = s1 / BitVecVal(256,16)
    r[8] = s2 % BitVecVal(256,16)
    r[9] = s2 / BitVecVal(256,16)
    return r

solver = Solver()
flag = [BitVec('flag%d' % i, 16) for i in range(16)]
masks = [0xff] * 8 + [0x00] + [0xff] * 7 + [0x00] + [0xff] * 7
masks = [BitVecVal(i, 16) for i in masks]

xmm5 = int2bitvecval(xmm5_results[0])
for i in range(8, 0, -1):
    xmm2 = andps_z3(flag, masks[i:i+16])
    xmm5 = psadbw_z3(xmm5, xmm2)
    expected = int2bitvecval(xmm5_results[9-i])
    for j in range(16):
        solver.add(xmm5[j] == expected[j])

if solver.check() == sat:
    m = solver.model()
    # print(m)
    s = []
    for i in range(16):
        s.append(m[flag[i]].as_long())
    # shuffle back
    s = s[12:16] + s[8:12] + s[0:8]
    print(b'flag' + bytes(s))
else:
    print('unsat')
```


## Reversing.kr
- [資料來源]()
