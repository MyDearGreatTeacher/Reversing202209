# objdump -d ctf --no-show-raw-insn
```
objdump -d ctf --no-show-raw-insn

ctf:     file format elf64-x86-64


Disassembly of section .init:

0000000000400a68 <_init@@Base>:
  400a68: sub    $0x8,%rsp
  400a6c: mov    0x201585(%rip),%rax        # 601ff8 <_fini@@Base+0x200ec4>
  400a73: test   %rax,%rax
  400a76: je     400a7d <_init@@Base+0x15>
  400a78: callq  400bb0 <_Unwind_Resume@plt+0x10>
  400a7d: add    $0x8,%rsp
  400a81: retq  

Disassembly of section .plt:

0000000000400a90 <_Z11rc4_decryptP11rc4_state_tRNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE@plt-0x10>:
  400a90: pushq  0x201572(%rip)        # 602008 <_fini@@Base+0x200ed4>
  400a96: jmpq   *0x201574(%rip)        # 602010 <_fini@@Base+0x200edc>
  400a9c: nopl   0x0(%rax)

0000000000400aa0 <_Z11rc4_decryptP11rc4_state_tRNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE@plt>:
  400aa0: jmpq   *0x201572(%rip)        # 602018 <_fini@@Base+0x200ee4>
  400aa6: pushq  $0x0
  400aab: jmpq   400a90 <_init@@Base+0x28>

0000000000400ab0 <puts@plt>:
  400ab0: jmpq   *0x20156a(%rip)        # 602020 <_fini@@Base+0x200eec>
  400ab6: pushq  $0x1
  400abb: jmpq   400a90 <_init@@Base+0x28>

0000000000400ac0 <fseek@plt>:
  400ac0: jmpq   *0x201562(%rip)        # 602028 <_fini@@Base+0x200ef4>
  400ac6: pushq  $0x2
  400acb: jmpq   400a90 <_init@@Base+0x28>

0000000000400ad0 <_ZdlPv@plt>:
  400ad0: jmpq   *0x20155a(%rip)        # 602030 <_fini@@Base+0x200efc>
  400ad6: pushq  $0x3
  400adb: jmpq   400a90 <_init@@Base+0x28>

0000000000400ae0 <__printf_chk@plt>:
  400ae0: jmpq   *0x201552(%rip)        # 602038 <_fini@@Base+0x200f04>
  400ae6: pushq  $0x4
  400aeb: jmpq   400a90 <_init@@Base+0x28>

0000000000400af0 <fopen@plt>:
  400af0: jmpq   *0x20154a(%rip)        # 602040 <_fini@@Base+0x200f0c>
  400af6: pushq  $0x5
  400afb: jmpq   400a90 <_init@@Base+0x28>

0000000000400b00 <__libc_start_main@plt>:
  400b00: jmpq   *0x201542(%rip)        # 602048 <_fini@@Base+0x200f14>
  400b06: pushq  $0x6
  400b0b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b10 <fgets@plt>:
  400b10: jmpq   *0x20153a(%rip)        # 602050 <_fini@@Base+0x200f1c>
  400b16: pushq  $0x7
  400b1b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b20 <_Z8rc4_initP11rc4_state_tPhi@plt>:
  400b20: jmpq   *0x201532(%rip)        # 602058 <_fini@@Base+0x200f24>
  400b26: pushq  $0x8
  400b2b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b30 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE9_M_assignERKS4_@plt>:
  400b30: jmpq   *0x20152a(%rip)        # 602060 <_fini@@Base+0x200f2c>
  400b36: pushq  $0x9
  400b3b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b40 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE6assignEPKc@plt>:
  400b40: jmpq   *0x201522(%rip)        # 602068 <_fini@@Base+0x200f34>
  400b46: pushq  $0xa
  400b4b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b50 <getenv@plt>:
  400b50: jmpq   *0x20151a(%rip)        # 602070 <_fini@@Base+0x200f3c>
  400b56: pushq  $0xb
  400b5b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b60 <__stack_chk_fail@plt>:
  400b60: jmpq   *0x201512(%rip)        # 602078 <_fini@@Base+0x200f44>
  400b66: pushq  $0xc
  400b6b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b70 <strcmp@plt>:
  400b70: jmpq   *0x20150a(%rip)        # 602080 <_fini@@Base+0x200f4c>
  400b76: pushq  $0xd
  400b7b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b80 <fclose@plt>:
  400b80: jmpq   *0x201502(%rip)        # 602088 <_fini@@Base+0x200f54>
  400b86: pushq  $0xe
  400b8b: jmpq   400a90 <_init@@Base+0x28>

0000000000400b90 <__gxx_personality_v0@plt>:
  400b90: jmpq   *0x2014fa(%rip)        # 602090 <_fini@@Base+0x200f5c>
  400b96: pushq  $0xf
  400b9b: jmpq   400a90 <_init@@Base+0x28>

0000000000400ba0 <_Unwind_Resume@plt>:
  400ba0: jmpq   *0x2014f2(%rip)        # 602098 <_fini@@Base+0x200f64>
  400ba6: pushq  $0x10
  400bab: jmpq   400a90 <_init@@Base+0x28>

Disassembly of section .plt.got:

0000000000400bb0 <.plt.got>:
  400bb0: jmpq   *0x201442(%rip)        # 601ff8 <_fini@@Base+0x200ec4>
  400bb6: xchg   %ax,%ax

Disassembly of section .text:

0000000000400bc0 <.text>:
  400bc0: push   %rbp
  400bc1: push   %rbx
  400bc2: sub    $0x208,%rsp
  400bc9: mov    %fs:0x28,%rax
  400bd2: mov    %rax,0x1f8(%rsp)
  400bda: xor    %eax,%eax
  400bdc: lea    0x10(%rsp),%rax
  400be1: cmp    $0x1,%edi
  400be4: movq   $0x0,0x8(%rsp)
  400bed: movb   $0x0,0x10(%rsp)
  400bf2: movq   $0x0,0x28(%rsp)
  400bfb: mov    %rax,(%rsp)
  400bff: lea    0x30(%rsp),%rax
  400c04: movb   $0x0,0x30(%rsp)
  400c09: movq   $0x0,0x48(%rsp)
  400c12: movb   $0x0,0x50(%rsp)
  400c17: mov    %rax,0x20(%rsp)
  400c1c: lea    0x50(%rsp),%rax
  400c21: mov    %rax,0x40(%rsp)
  400c26: jle    400cc3 <_Unwind_Resume@plt+0x123>
  400c2c: mov    0x8(%rsi),%rbx
  400c30: mov    $0x1,%edi
  400c35: mov    $0x401158,%esi
  400c3a: xor    %eax,%eax
  400c3c: mov    %rbx,%rdx
  400c3f: callq  400ae0 <__printf_chk@plt>
  400c44: mov    $0x401167,%esi
  400c49: mov    %rbx,%rdi
  400c4c: callq  400b70 <strcmp@plt>
  400c51: test   %eax,%eax
  400c53: je     400ce6 <_Unwind_Resume@plt+0x146>
  400c59: nopl   0x0(%rax)
  400c60: mov    $0x1,%ebx
  400c65: mov    0x40(%rsp),%rdi
  400c6a: lea    0x50(%rsp),%rax
  400c6f: cmp    %rax,%rdi
  400c72: je     400c79 <_Unwind_Resume@plt+0xd9>
  400c74: callq  400ad0 <_ZdlPv@plt>
  400c79: mov    0x20(%rsp),%rdi
  400c7e: lea    0x30(%rsp),%rax
  400c83: cmp    %rax,%rdi
  400c86: je     400c8d <_Unwind_Resume@plt+0xed>
  400c88: callq  400ad0 <_ZdlPv@plt>
  400c8d: mov    (%rsp),%rdi
  400c91: lea    0x10(%rsp),%rax
  400c96: cmp    %rax,%rdi
  400c99: je     400ca0 <_Unwind_Resume@plt+0x100>
  400c9b: callq  400ad0 <_ZdlPv@plt>
  400ca0: mov    0x1f8(%rsp),%rcx
  400ca8: xor    %fs:0x28,%rcx
  400cb1: mov    %ebx,%eax
  400cb3: jne    400f20 <_Unwind_Resume@plt+0x380>
  400cb9: add    $0x208,%rsp
  400cc0: pop    %rbx
  400cc1: pop    %rbp
  400cc2: retq  
  400cc3: cmpl   $0x0,0x2013ea(%rip)        # 6020b4 <_edata@@Base+0x4>
  400cca: je     400c60 <_Unwind_Resume@plt+0xc0>
  400ccc: mov    0x8(%rsi),%rdx
  400cd0: mov    $0x1,%edi
  400cd5: mov    $0x401144,%esi
  400cda: xor    %eax,%eax
  400cdc: callq  400ae0 <__printf_chk@plt>
  400ce1: jmpq   400c60 <_Unwind_Resume@plt+0xc0>
  400ce6: mov    $0x401178,%edi
  400ceb: callq  400ab0 <puts@plt>
  400cf0: lea    0xc0(%rsp),%rdi
  400cf8: mov    $0x42,%edx
  400cfd: mov    $0x4011c0,%esi
  400d02: callq  400b20 <_Z8rc4_initP11rc4_state_tPhi@plt>
  400d07: mov    $0x40117b,%esi
  400d0c: mov    %rsp,%rdi
  400d0f: callq  400b40 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE6assignEPKc@plt>
  400d14: lea    0xc0(%rsp),%rsi
  400d1c: lea    0x60(%rsp),%rdi
  400d21: mov    %rsp,%rdx
  400d24: callq  400aa0 <_Z11rc4_decryptP11rc4_state_tRNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE@plt>
  400d29: lea    0x60(%rsp),%rsi
  400d2e: mov    %rsp,%rdi
  400d31: callq  400b30 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE9_M_assignERKS4_@plt>
  400d36: mov    0x60(%rsp),%rdi
  400d3b: lea    0x70(%rsp),%rax
  400d40: cmp    %rax,%rdi
  400d43: je     400d4a <_Unwind_Resume@plt+0x1aa>
  400d45: callq  400ad0 <_ZdlPv@plt>
  400d4a: mov    (%rsp),%rdi
  400d4e: callq  400b50 <getenv@plt>
  400d53: test   %rax,%rax
  400d56: mov    %rax,%rbx
  400d59: je     400c60 <_Unwind_Resume@plt+0xc0>
  400d5f: lea    0x20(%rsp),%rdi
  400d64: mov    $0x401183,%esi
  400d69: callq  400b40 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE6assignEPKc@plt>
  400d6e: lea    0x20(%rsp),%rdx
  400d73: lea    0xc0(%rsp),%rsi
  400d7b: lea    0x80(%rsp),%rdi
  400d83: callq  400aa0 <_Z11rc4_decryptP11rc4_state_tRNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE@plt>
  400d88: lea    0x80(%rsp),%rsi
  400d90: lea    0x20(%rsp),%rdi
  400d95: callq  400b30 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE9_M_assignERKS4_@plt>
  400d9a: mov    0x80(%rsp),%rdi
  400da2: lea    0x90(%rsp),%rax
  400daa: cmp    %rax,%rdi
  400dad: je     400db4 <_Unwind_Resume@plt+0x214>
  400daf: callq  400ad0 <_ZdlPv@plt>
  400db4: mov    0x20(%rsp),%rcx
  400db9: xor    %eax,%eax
  400dbb: nopl   0x0(%rax,%rax,1)
  400dc0: movzbl (%rbx,%rax,1),%edx
  400dc4: test   %dl,%dl
  400dc6: je     400dcd <_Unwind_Resume@plt+0x22d>
  400dc8: cmp    (%rcx,%rax,1),%dl
  400dcb: je     400de0 <_Unwind_Resume@plt+0x240>
  400dcd: mov    $0x4011af,%edi
  400dd2: callq  400ab0 <puts@plt>
  400dd7: jmpq   400c60 <_Unwind_Resume@plt+0xc0>
  400ddc: nopl   0x0(%rax)
  400de0: add    $0x1,%rax
  400de4: cmp    $0x15,%rax
  400de8: jne    400dc0 <_Unwind_Resume@plt+0x220>
  400dea: lea    0x40(%rsp),%rdi
  400def: mov    $0x401199,%esi
  400df4: callq  400b40 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE6assignEPKc@plt>
  400df9: lea    0x40(%rsp),%rdx
  400dfe: lea    0xc0(%rsp),%rsi
  400e06: lea    0xa0(%rsp),%rdi
  400e0e: callq  400aa0 <_Z11rc4_decryptP11rc4_state_tRNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE@plt>
  400e13: lea    0xa0(%rsp),%rsi
  400e1b: lea    0x40(%rsp),%rdi
  400e20: callq  400b30 <_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE9_M_assignERKS4_@plt>
  400e25: mov    0xa0(%rsp),%rdi
  400e2d: lea    0xb0(%rsp),%rax
  400e35: cmp    %rax,%rdi
  400e38: je     400e3f <_Unwind_Resume@plt+0x29f>
  400e3a: callq  400ad0 <_ZdlPv@plt>
  400e3f: mov    0x40(%rsp),%rdi
  400e44: mov    $0x4011a1,%esi
  400e49: callq  400af0 <fopen@plt>
  400e4e: test   %rax,%rax
  400e51: mov    %rax,%rbp
  400e54: je     400c60 <_Unwind_Resume@plt+0xc0>
  400e5a: xor    %edx,%edx
  400e5c: mov    $0x1fcb0,%esi
  400e61: mov    %rax,%rdi
  400e64: callq  400ac0 <fseek@plt>
  400e69: test   %eax,%eax
  400e6b: mov    %eax,%ebx
  400e6d: jne    400c60 <_Unwind_Resume@plt+0xc0>
  400e73: lea    0x1d0(%rsp),%rdi
  400e7b: mov    %rbp,%rdx
  400e7e: mov    $0x21,%esi
  400e83: callq  400b10 <fgets@plt>
  400e88: test   %rax,%rax
  400e8b: je     400c60 <_Unwind_Resume@plt+0xc0>
  400e91: mov    %rbp,%rdi
  400e94: movb   $0x0,0x1f0(%rsp)
  400e9c: callq  400b80 <fclose@plt>
  400ea1: lea    0x1d0(%rsp),%rdx
  400ea9: lea    0x1c0(%rsp),%r8
  400eb1: mov    %rdx,%rax
  400eb4: mov    %rdx,%rcx
  400eb7: movzbl (%rcx),%esi
  400eba: movzbl 0x1f(%rax),%edi
  400ebe: sub    $0x1,%rax
  400ec2: add    $0x1,%rcx
  400ec6: mov    %dil,-0x1(%rcx)
  400eca: mov    %sil,0x20(%rax)
  400ece: cmp    %rax,%r8
  400ed1: jne    400eb7 <_Unwind_Resume@plt+0x317>
  400ed3: lea    0x1f0(%rsp),%rsi
  400edb: jmp    400eeb <_Unwind_Resume@plt+0x34b>
  400edd: sub    $0x1a,%eax
  400ee0: mov    %al,(%rdx)
  400ee2: add    $0x1,%rdx
  400ee6: cmp    %rdx,%rsi
  400ee9: je     400f02 <_Unwind_Resume@plt+0x362>
  400eeb: movsbl (%rdx),%eax
  400eee: lea    -0x61(%rax),%ecx
  400ef1: cmp    $0x19,%cl
  400ef4: ja     400ee2 <_Unwind_Resume@plt+0x342>
  400ef6: add    $0xd,%eax
  400ef9: cmp    $0x7a,%eax
  400efc: jg     400edd <_Unwind_Resume@plt+0x33d>
  400efe: mov    %al,(%rdx)
  400f00: jmp    400ee2 <_Unwind_Resume@plt+0x342>
  400f02: lea    0x1d0(%rsp),%rdx
  400f0a: mov    $0x4011a4,%esi
  400f0f: mov    $0x1,%edi
  400f14: xor    %eax,%eax
  400f16: callq  400ae0 <__printf_chk@plt>
  400f1b: jmpq   400c65 <_Unwind_Resume@plt+0xc5>
  400f20: callq  400b60 <__stack_chk_fail@plt>
  400f25: mov    0xa0(%rsp),%rdi
  400f2d: lea    0xb0(%rsp),%rdx
  400f35: mov    %rax,%rbx
  400f38: cmp    %rdx,%rdi
  400f3b: je     400f42 <_Unwind_Resume@plt+0x3a2>
  400f3d: callq  400ad0 <_ZdlPv@plt>
  400f42: mov    0x40(%rsp),%rdi
  400f47: lea    0x50(%rsp),%rax
  400f4c: cmp    %rax,%rdi
  400f4f: je     400f56 <_Unwind_Resume@plt+0x3b6>
  400f51: callq  400ad0 <_ZdlPv@plt>
  400f56: mov    0x20(%rsp),%rdi
  400f5b: lea    0x30(%rsp),%rax
  400f60: cmp    %rax,%rdi
  400f63: je     400f6a <_Unwind_Resume@plt+0x3ca>
  400f65: callq  400ad0 <_ZdlPv@plt>
  400f6a: mov    (%rsp),%rdi
  400f6e: lea    0x10(%rsp),%rax
  400f73: cmp    %rax,%rdi
  400f76: je     400f7d <_Unwind_Resume@plt+0x3dd>
  400f78: callq  400ad0 <_ZdlPv@plt>
  400f7d: mov    %rbx,%rdi
  400f80: callq  400ba0 <_Unwind_Resume@plt>
  400f85: mov    %rax,%rbx
  400f88: jmp    400f42 <_Unwind_Resume@plt+0x3a2>
  400f8a: mov    0x80(%rsp),%rdi
  400f92: lea    0x90(%rsp),%rdx
  400f9a: mov    %rax,%rbx
  400f9d: cmp    %rdx,%rdi
  400fa0: jne    400f3d <_Unwind_Resume@plt+0x39d>
  400fa2: jmp    400f42 <_Unwind_Resume@plt+0x3a2>
  400fa4: mov    0x60(%rsp),%rdi
  400fa9: lea    0x70(%rsp),%rdx
  400fae: mov    %rax,%rbx
  400fb1: cmp    %rdx,%rdi
  400fb4: jne    400f3d <_Unwind_Resume@plt+0x39d>
  400fb6: jmp    400f42 <_Unwind_Resume@plt+0x3a2>
  400fb8: nopl   0x0(%rax,%rax,1)
  400fc0: xor    %ebp,%ebp
  400fc2: mov    %rdx,%r9
  400fc5: pop    %rsi
  400fc6: mov    %rsp,%rdx
  400fc9: and    $0xfffffffffffffff0,%rsp
  400fcd: push   %rax
  400fce: push   %rsp
  400fcf: mov    $0x401130,%r8
  400fd6: mov    $0x4010c0,%rcx
  400fdd: mov    $0x400bc0,%rdi
  400fe4: callq  400b00 <__libc_start_main@plt>
  400fe9: hlt    
  400fea: nopw   0x0(%rax,%rax,1)
  400ff0: mov    $0x6020b7,%eax
  400ff5: push   %rbp
  400ff6: sub    $0x6020b0,%rax
  400ffc: cmp    $0xe,%rax
  401000: mov    %rsp,%rbp
  401003: jbe    401020 <_Unwind_Resume@plt+0x480>
  401005: mov    $0x0,%eax
  40100a: test   %rax,%rax
  40100d: je     401020 <_Unwind_Resume@plt+0x480>
  40100f: pop    %rbp
  401010: mov    $0x6020b0,%edi
  401015: jmpq   *%rax
  401017: nopw   0x0(%rax,%rax,1)
  401020: pop    %rbp
  401021: retq  
  401022: nopl   0x0(%rax)
  401026: nopw   %cs:0x0(%rax,%rax,1)
  401030: mov    $0x6020b0,%esi
  401035: push   %rbp
  401036: sub    $0x6020b0,%rsi
  40103d: sar    $0x3,%rsi
  401041: mov    %rsp,%rbp
  401044: mov    %rsi,%rax
  401047: shr    $0x3f,%rax
  40104b: add    %rax,%rsi
  40104e: sar    %rsi
  401051: je     401068 <_Unwind_Resume@plt+0x4c8>
  401053: mov    $0x0,%eax
  401058: test   %rax,%rax
  40105b: je     401068 <_Unwind_Resume@plt+0x4c8>
  40105d: pop    %rbp
  40105e: mov    $0x6020b0,%edi
  401063: jmpq   *%rax
  401065: nopl   (%rax)
  401068: pop    %rbp
  401069: retq  
  40106a: nopw   0x0(%rax,%rax,1)
  401070: cmpb   $0x0,0x201039(%rip)        # 6020b0 <_edata@@Base>
  401077: jne    40108a <_Unwind_Resume@plt+0x4ea>
  401079: push   %rbp
  40107a: mov    %rsp,%rbp
  40107d: callq  400ff0 <_Unwind_Resume@plt+0x450>
  401082: pop    %rbp
  401083: movb   $0x1,0x201026(%rip)        # 6020b0 <_edata@@Base>
  40108a: repz retq
  40108c: nopl   0x0(%rax)
  401090: mov    $0x601df0,%edi
  401095: cmpq   $0x0,(%rdi)
  401099: jne    4010a0 <_Unwind_Resume@plt+0x500>
  40109b: jmp    401030 <_Unwind_Resume@plt+0x490>
  40109d: nopl   (%rax)
  4010a0: mov    $0x0,%eax
  4010a5: test   %rax,%rax
  4010a8: je     40109b <_Unwind_Resume@plt+0x4fb>
  4010aa: push   %rbp
  4010ab: mov    %rsp,%rbp
  4010ae: callq  *%rax
  4010b0: pop    %rbp
  4010b1: jmpq   401030 <_Unwind_Resume@plt+0x490>
  4010b6: nopw   %cs:0x0(%rax,%rax,1)
  4010c0: push   %r15
  4010c2: push   %r14
  4010c4: mov    %edi,%r15d
  4010c7: push   %r13
  4010c9: push   %r12
  4010cb: lea    0x200d0e(%rip),%r12        # 601de0 <_fini@@Base+0x200cac>
  4010d2: push   %rbp
  4010d3: lea    0x200d0e(%rip),%rbp        # 601de8 <_fini@@Base+0x200cb4>
  4010da: push   %rbx
  4010db: mov    %rsi,%r14
  4010de: mov    %rdx,%r13
  4010e1: sub    %r12,%rbp
  4010e4: sub    $0x8,%rsp
  4010e8: sar    $0x3,%rbp
  4010ec: callq  400a68 <_init@@Base>
  4010f1: test   %rbp,%rbp
  4010f4: je     401116 <_Unwind_Resume@plt+0x576>
  4010f6: xor    %ebx,%ebx
  4010f8: nopl   0x0(%rax,%rax,1)
  401100: mov    %r13,%rdx
  401103: mov    %r14,%rsi
  401106: mov    %r15d,%edi
  401109: callq  *(%r12,%rbx,8)
  40110d: add    $0x1,%rbx
  401111: cmp    %rbp,%rbx
  401114: jne    401100 <_Unwind_Resume@plt+0x560>
  401116: add    $0x8,%rsp
  40111a: pop    %rbx
  40111b: pop    %rbp
  40111c: pop    %r12
  40111e: pop    %r13
  401120: pop    %r14
  401122: pop    %r15
  401124: retq  
  401125: nop
  401126: nopw   %cs:0x0(%rax,%rax,1)
  401130: repz retq

Disassembly of section .fini:

0000000000401134 <_fini@@Base>:
  401134: sub    $0x8,%rsp
  401138: add    $0x8,%rsp
  40113c: retq  
```
