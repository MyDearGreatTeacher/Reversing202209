# Ubuntu18.04LTS系統環境建置
```
0.from iso to ova
socat


1.reverse engineering
gdb powerkits ==> peda gef pwngdb(heapinfo) pwndbg
radare2
Ghidra


2.Pwn
pwntools
angelboy
onegaget
ROPgaget
```


# 1.reverse engineering
-[Ubuntu 18.04 安裝 pwndbg](https://www.twblogs.net/a/5d485a28bd9eee5327fb9acb)


 
## 安裝pwndbg
```bash
git clone https://github.com/pwndbg/pwndbg
cd pwndbg
./setup.sh
```
 
## 安裝gef
```
wget -q -O ~/.gdbinit-gef.py https://github.com/hugsy/gef/raw/master/gef.py
echo source ~/.gdbinit-gef.py >> ~/.gdbinit
```
 
## 安裝peda
```
git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
```
 
## 設定peda，gef，pwndbg的切換配置
```
alias pwndbg="echo \"source /home/pwnner/pwndbg/gdbinit.py\" > ~/.gdbinit; gdb"
alias gef="echo \"source /home/pwnner/.gdbinit-gef.py\" > ~/.gdbinit; gdb"
alias peda="echo \"source ~/peda/peda.py\" > ~/.gdbinit; gdb"
```

# PWN

## pwntools

### 撰寫安裝SCRIPT
```
apt-get update
apt-get install python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential
python3 -m pip install --upgrade pip
python3 -m pip install --upgrade pwntools
```
### 執行
```
root@kali:~# gedit pwntools_install.sh
root@kali:~# bash pwntools_install.sh 
```
```
一路yes到底
```
### pwn -h
```
```
### 測試 from pwn import *

##
### 安裝seccomp-tools
```
root@kali:~# gem install seccomp-tools
Fetching: os-1.1.1.gem (100%)
Successfully installed os-1.1.1
Fetching: seccomp-tools-1.5.0.gem (100%)
Building native extensions. This could take a while...
Successfully installed seccomp-tools-1.5.0
Parsing documentation for os-1.1.1
Installing ri documentation for os-1.1.1
Parsing documentation for seccomp-tools-1.5.0
Installing ri documentation for seccomp-tools-1.5.0
Done installing documentation for os, seccomp-tools after 1 seconds
2 gems installed
```

### 安裝one_gadget
```
oot@kali:~# gem install one_gadget
Fetching: bindata-2.4.10.gem (100%)
Successfully installed bindata-2.4.10
Fetching: elftools-1.1.3.gem (100%)
Successfully installed elftools-1.1.3
Fetching: one_gadget-1.7.4.gem (100%)
Successfully installed one_gadget-1.7.4
Parsing documentation for bindata-2.4.10
Installing ri documentation for bindata-2.4.10
Parsing documentation for elftools-1.1.3
Installing ri documentation for elftools-1.1.3
Parsing documentation for one_gadget-1.7.4
Installing ri documentation for one_gadget-1.7.4
Done installing documentation for bindata, elftools, one_gadget after 10 seconds
3 gems installed
```
