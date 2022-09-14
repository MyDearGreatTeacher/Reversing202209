# 使用Angr解CTF
- [hitcon2017_sakura](#hitcon2017_sakura)
- [CSAW_CTF_2015_wyvern](#CSAW_CTF_2015_wyvern)
  - side-channel attack 的典型题目
  - 很多解法
    - [只使用gdb-gef來解,可以看看解的辛苦度:Nightmare有很好的學習資料一定要去看看](https://guyinatuxedo.github.io/36-obfuscated_reversing/csaw15_wyvern/index.html)
    - [[使用angr解題1(angr官方解法)]](https://github.com/angr/angr-doc/blob/master/examples/csaw_wyvern/solve.py)
    - [[使用angr解題2]](https://blog.csdn.net/doudoudouzoule/article/details/79969378?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-1.control)
    - [[使用Intel pin 解題1]](https://www.bookstack.cn/read/CTF-All-In-One/doc-6.2.4_re_csawctf2015_wyvern.md) 
    - [[使用Intel pin 解題2]](https://psmoe.com/side-channel-attack/) 
    - [[使用Intel pin 解題3]](https://bruce30262.github.io/csaw-ctf-2015-wyvern/)
    - [[使用afl-fuzz解題]](https://www.mathyvanhoef.com/2015/09/csaw-ctf-solving-reversing-wyvern-500.html)
    - [[binary patch作法]](https://www.bookstack.cn/read/CTF-All-In-One/doc-6.2.4_re_csawctf2015_wyvern.md)
    - [[writeup1 ddaa]](https://ithelp.ithome.com.tw/articles/10218237)
    - [[writeup3]](https://gist.github.com/inaz2/1682e7254b1c7a2cf641)
- [defcamp 2015 quals r100]()
  - [[使用angr]](https://guyinatuxedo.github.io/13-angr/defcamp_r100/index.html)
- [DEFCON_2017_crackme2000](#DEFCON_2017_crackme2000)
  - [[DEFCON 2017 crackme2000(angr官方解法)]](https://github.com/angr/angr-doc/tree/master/examples/defcon2017quals_crackme2000)
    - The 2017 DEFCON CTF qualifying event had an entire category of automated reverse engineering challenges 非常值得深入研究
    - 找時間研究automated reverse engineering
- [CodegateCTF2018_RedVelvet](#CodegateCTF2018_RedVelvet)
  - [[題目]](https://github.com/8wingflying/NTHU2021/blob/main/week3_20211001/3_Reverse-CTFwriteups/RedVelvet)
  - [[使用angr]](http://blog.redrocket.club/2018/02/04/Codegate-2018-Preliminary-RedVelvet/)
  - [[使用z3]](https://github.com/AnisBoss/CTFs/blob/master/Codegate%20CTF%202018/RedVelvet%20-%20254pts%20(Rev)/solve.py)
- [Securityfest 2019 fairlight]
  - [[使用angr]](https://guyinatuxedo.github.io/13-angr/securityfest_fairlight/index.html)
- [PlaidCTF_2019_i can count](#PlaidCTF_2019_i_can_count)
  - [[使用angr]](https://guyinatuxedo.github.io/13-angr/plaid19_icancount/index.html)
  - [撰寫gdb script求解](https://guyinatuxedo.github.io/13-angr/plaid19_icancount/index.html)
-  更多題目請參閱底下網址
  - [angr-doc/docs/examples.md](https://github.com/angr/angr-doc/blob/314f909875efe14c6cd6f815e28f2f65f213e903/docs/examples.md)  
  - [jakespringer/angr_ctf](https://github.com/jakespringer/angr_ctf)  

## hitcon2017_sakura
- [題目](https://github.com/angr/angr-doc/blob/master/examples/hitcon2017_sakura/sakura)
- [angr官方解答1](https://github.com/angr/angr-doc/blob/master/examples/ais3_crackme/solve.py)
- [angr解答2:符号执行入门](https://www.djinni.club/index.php/2020/10/23/%E7%AC%A6%E5%8F%B7%E6%89%A7%E8%A1%8C%E5%85%A5%E9%97%A8/)

### 逆向分析 

### angr求解
```python
#!/usr/bin/env python2
# -*- coding: utf-8 -*-
# Author: Kyle ZENG
# Runtime: ~6 minutes

import hashlib
import angr

def main():
    e = open('./sakura', 'rb').read()

    # make sure return value is not 0, add corresponding addr to avoid list
    avoids = []
    index = 0
    while True:
        # avoid asm('mov byte ptr [rbp-0x1E49], 0')
        index = e.find(b'\xc6\x85\xb7\xe1\xff\xff\x00', index+1)
        if index == -1:
            break
        addr = 0x400000 + index
        avoids.append(addr)

    # find list
    finds = []
    index = 0
    while True:
        # find asm('mov rdi, rax')
        index = e.find(b'H\x89\xc7', index+1)
        if index == -1 or index > 0x10ff5:
            break
        addr = 0x400000 + index
        finds.append(addr)

        # skip a addr we don't want to find
        index = e.find(b'H\x89\xc7', index+1)

    # initialize project
    proj = angr.Project('./sakura')
    state = proj.factory.entry_state()
    simgr = proj.factory.simulation_manager(state)

    # find ans stage by stage
    for find in finds:
        simgr.explore(find=find, avoid=avoids)
        found = simgr.found[0]
        simgr = proj.factory.simulation_manager(found)

    # evaluate text
    text = found.solver.eval(found.memory.load(0x612040, 400), cast_to=bytes)

    h = hashlib.sha256(text)
    flag = 'hitcon{'+h.hexdigest()+'}'
    return flag

def test():
    assert main() == 'hitcon{6c0d62189adfd27a12289890d5b89c0dc8098bc976ecc3f6d61ec0429cccae61}'

if __name__ == '__main__':
    import logging
    logging.getLogger('angr.sim_manager').setLevel(logging.DEBUG)

    print(main())

```
## CSAW_CTF_2015_wyvern 
```
There’s a dragon afoot, we need a hero. 
Give us the dragon’s secret and we’ll give you a flag.

HINT: static is only 1 of 2 methods to RE. IDA torrent unnecessary
```
- [題目檔案](https://github.com/angr/angr-doc/blob/master/examples/csaw_wyvern/wyvern)

### 逆向分析[待撰寫]

### [解答:資料來源](https://github.com/angr/angr-doc/blob/master/examples/csaw_wyvern/solve.py)
```python
#!/usr/bin/env python
# coding: utf-8
import angr
import claripy
import time

def main():
    # Load the binary. This is a 64-bit C++ binary, pretty heavily obfuscated.
    # its correct emulation by angr depends heavily on the libraries it is loaded with,
    # so if this script fails, try copying to this dir the .so files from our binaries repo:
    # https://github.com/angr/binaries/tree/master/tests/x86_64
    p = angr.Project('wyvern')

    # It's reasonably easy to tell from looking at the program in IDA that the key will
    # be 29 bytes long, and the last byte is a newline. Let's construct a value of several
    # symbols that we can add constraints on once we have a state.

    flag_chars = [claripy.BVS('flag_%d' % i, 8) for i in range(28)]
    flag = claripy.Concat(*flag_chars + [claripy.BVV(b'\n')])

    # This block constructs the initial program state for analysis.
    # Because we're going to have to step deep into the C++ standard libraries
    # for this to work, we need to run everyone's initializers. The full_init_state
    # will do that. In order to do this peformantly, we will use the unicorn engine!
    st = p.factory.full_init_state(
            args=['./wyvern'],
            add_options=angr.options.unicorn,
            stdin=flag,
    )

    # Constrain the first 28 bytes to be non-null and non-newline:
    for k in flag_chars:
        st.solver.add(k != 0)
        st.solver.add(k != 10)

    # Construct a SimulationManager to perform symbolic execution.
    # Step until there is nothing left to be stepped.
    sm = p.factory.simulation_manager(st)
    sm.run()

    # Get the stdout of every path that reached an exit syscall. The flag should be in one of these!
    out = b''
    for pp in sm.deadended:
        out = pp.posix.dumps(1)
        if b'flag{' in out:
            return next(filter(lambda s: b'flag{' in s, out.split()))

    # Runs in about 15 minutes!

def test():
    assert main() == b'flag{dr4g0n_or_p4tric1an_it5_LLVM}'

if __name__ == "__main__":
    before = time.time()
    print(main())
    after = time.time()
    print("Time elapsed: {}".format(after - before))
```
## DEFCON_2017_crackme2000

## CodegateCTF2018_RedVelvet
