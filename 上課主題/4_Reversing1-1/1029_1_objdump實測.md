#
```
0000000000400b1e <main>:
  400b1e:	push   rbp
  400b1f:	mov    rbp,rsp
  400b22:	sub    rsp,0x20
  400b26:	mov    DWORD PTR [rbp-0xc],0x0
  400b2d:	mov    DWORD PTR [rbp-0x10],0x0
  400b34:	mov    DWORD PTR [rbp-0x14],0x0
  400b3b:	mov    esi,0x400cd0
  400b40:	mov    edi,0x6021a0
  400b45:	call   400830 <_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc@plt>
  400b4a:	lea    rax,[rbp-0xc]
  400b4e:	mov    rsi,rax
  400b51:	mov    edi,0x602080
  400b56:	call   400850 <_ZNSirsERi@plt>
  400b5b:	lea    rdx,[rbp-0x10]
  400b5f:	mov    rsi,rdx
  400b62:	mov    rdi,rax
  400b65:	call   400850 <_ZNSirsERi@plt>
  400b6a:	lea    rdx,[rbp-0x14]
  400b6e:	mov    rsi,rdx
  400b71:	mov    rdi,rax
  400b74:	call   400850 <_ZNSirsERi@plt>
  400b79:	mov    edx,DWORD PTR [rbp-0xc]
  400b7c:	mov    eax,DWORD PTR [rbp-0x10]
  400b7f:	add    edx,eax
  400b81:	mov    eax,DWORD PTR [rbp-0x14]
  400b84:	add    eax,edx
  400b86:	mov    edi,eax
  400b88:	call   40094d <_Z3geni>
  400b8d:	mov    QWORD PTR [rbp-0x8],rax
  400b91:	mov    edx,DWORD PTR [rbp-0xc]
  400b94:	mov    eax,DWORD PTR [rbp-0x10]
  400b97:	add    edx,eax
  400b99:	mov    eax,DWORD PTR [rbp-0x14]
  400b9c:	add    eax,edx
  400b9e:	cmp    eax,0x539
  400ba3:	jne    400bcc <main+0xae>
  400ba5:	mov    esi,0x400ce6
  400baa:	mov    edi,0x6021a0
  400baf:	call   400830 <_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc@plt>
  400bb4:	mov    rax,QWORD PTR [rbp-0x8]
  400bb8:	mov    rdi,rax
  400bbb:	call   400ae3 <_Z9print_ptrPc>
  400bc0:	mov    edi,0x400cef
  400bc5:	call   4007c0 <puts@plt>
  400bca:	jmp    400bdb <main+0xbd>
  400bcc:	mov    esi,0x400cf1
  400bd1:	mov    edi,0x6021a0
  400bd6:	call   400830 <_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc@plt>
  400bdb:	mov    rax,QWORD PTR [rbp-0x8]
  400bdf:	mov    rdi,rax
  400be2:	call   400840 <free@plt>
  400be7:	mov    eax,0x0
  400bec:	leave  
  400bed:	ret    
```
