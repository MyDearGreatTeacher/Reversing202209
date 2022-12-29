#
```c
undefined8 main(void)

{
  basic_istream<char,std--char_traits<char>> *this;
  int local_1c;
  int local_18;
  int local_14;
  char *local_10;
  
  local_14 = 0;
  local_18 = 0;
  local_1c = 0;
  operator<<<std--char_traits<char>>((basic_ostream *)cout,"Enter three numbers!\n");
  this = (basic_istream<char,std--char_traits<char>> *)
         operator>>((basic_istream<char,std--char_traits<char>> *)cin,&local_14);
  this = (basic_istream<char,std--char_traits<char>> *)operator>>(this,&local_18);
  operator>>(this,&local_1c);
  local_10 = (char *)gen(local_1c + local_14 + local_18);
  if (local_1c + local_14 + local_18 == 0x539) {
    operator<<<std--char_traits<char>>((basic_ostream *)cout,"easyctf{");
    print_ptr(local_10);
    puts("}");
  }
  else {
    operator<<<std--char_traits<char>>((basic_ostream *)cout,"nope.\n");
  }
  free(local_10);
  return 0;
}
```
