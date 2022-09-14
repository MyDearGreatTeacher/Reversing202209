

## [miasm@Docker](https://registry.hub.docker.com/r/miasm/tested)

```
docker pull miasm/tested

docker run -i -t miasm/base bash

miasm2@8ee98f936055:/opt/miasm2/test$ cd ../example/

miasm2@8ee98f936055:/opt/miasm2/example$ python test_jit_arm.py -j python md5_arm A684
```

## miasm@colab

```
!pip install miasm

!wget https://github.com/PacktPublishing/Ghidra-Software-Reverse-Engineering-for-Beginners/blob/master/Chapter14/symbex_experiment/hello_world.exe
```
```python

#!/usr/bin/python3
from miasm.analysis.binary import Container
from miasm.analysis.machine import Machine
from miasm.core.locationdb import LocationDB
from miasm.ir.symbexec import SymbolicExecutionEngine

start_addr = 0x402300
loc_db = LocationDB()
target_file = open("hello_world.exe", 'rb')
container = Container.from_stream(target_file, loc_db)

machine = Machine(container.arch)  ## 此處出錯
mdis = machine.dis_engine(container.bin_stream, 
                          loc_db=loc_db)
ira = machine.ira(mdis.loc_db)
asm_cfg = mdis.dis_multiblock(start_addr)
ira_cfg = ira.new_ircfg_from_asmcfg(asm_cfg)
symbex = SymbolicExecutionEngine(ira)
symbex_state = symbex.run_block_at(ira_cfg, start_addr)
print (symbex_state)
```

# https://stackoverflow.com/questions/69694833/frappe-installation-error-attributeerror-module-pyparsing-has-no-attribute
```
pip install pyparsing==2.4.2
```

## 先測試
```python
from miasm.analysis.machine import Machine

mn = Machine('x86_32').mn

print(mn.dis('\x33\x30', 32))
```
## 改成
```python
machine = Machine('x86_64')
mdis = machine.dis_engine(container.bin_stream, 
                          loc_db=loc_db)
ira = machine.ira(mdis.loc_db)
asm_cfg = mdis.dis_multiblock(start_addr)
ira_cfg = ira.new_ircfg_from_asmcfg(asm_cfg)
symbex = SymbolicExecutionEngine(ira)
symbex_state = symbex.run_block_at(ira_cfg, start_addr)
print (symbex_state)
```

仍未得到正確的答案
