# 自我練習_Linux_C的組合語法
- 編譯Linux C程式,看看對應的組合語言語法
- 看看從C 程式產生的組合語言程式和objdump逆向得到的組合語言
- 請自行設計或找C程式設計書籍範例練習

# 基礎 C 程式設計
```
1 輸出與輸入
   格式化的輸出與輸入
2.基本資料型態  ==> 進階型資料結構
   數值型資料型態
   字串或字元型資料型態
3.運算子、運算式與敘述
4.選擇性敘述 if   switch
5.迴圈 for   while     do.. while
6.函數
    遞迴函數
7.陣列(不使用指標)
8.字串(字元陣列)與字串處理(不使用指標)
```

# 注意底下組合語言下的函示呼叫 printf(), getchar(), putchar()
## 【字元】的輸出與輸入 ==> getchar(), putchar()
```
#include <stdio.h>
 
int main( )
{
   int c;
 
   printf( "Enter a value :");
   c = getchar( );
 
   printf( "\nYou entered: ");
   putchar( c );
   printf( "\n");
   return 0;
}
```
## 【字串】的輸出與輸入  ==> gets(),  puts()
```
#include <stdio.h>
 
int main( )
{
   char str[100];
 
   printf( "Enter a value :");
   gets( str );
 
   printf( "\nYou entered: ");
   puts( str );
   return 0;
}
```

## 格式化輸出
```
%c：以字元方式輸出

%d：10 進位整數輸出
%o：以 8 進位整數方式輸出
%x、%X：將整數以 16 進位方式輸出

%u：無號整數輸出
%lu：long unsigned 型態的整數

%f：浮點數輸出
%e、%E：使用科學記號顯示浮點數
%g、%G：浮點數輸出，取 %f 或 %e（%f 或 %E），看哪個表示精簡
%%：顯示 %


%s：字串輸出

%p：指標型態 
```
## 範例
```
#include <stdio.h>

int main(void) {
    printf("ASCII 編碼與解碼 初初階\n");
    printf("顯示字元 %c\n", 'A');
    printf("顯示為十進位整數 %d\n", 'A');
    printf("顯示為八進位整數 %o\n", 'A');
    printf("顯示為十六進位整數 %X\n", 'A');
    printf("顯示為十六進位整數 %x\n", 'A');
    
    return 0;
}
```

# 4.選擇性敘述 ==> 各類型 if   switch
## if
```
#include<stdio.h>
 
int main()
{
    int num;
 
    printf("請輸入一個正整數 : ");
    scanf("%d",&num);
 
    if (num%2==0)
      printf("你輸入的偶數");
}
```
## if ..else ..
```
#include<stdio.h>
 
int main()
{
    int num;
 
    printf("請輸入一個正整數 : ");
    scanf("%d",&num);
 
    if (num%2==0)
      printf("你輸入的偶數\n");
    else
      printf("你輸入的奇數\n");
}
```
## ? : 運算子(三元運算子)
```
#include<stdio.h>
 
int main()
{
    int num;
 
    printf("請輸入一個正整數 : ");
    scanf("%d",&num);
 
    (num%2==0)?printf("偶數"):printf("奇數");
}
```

## 範例: C 命令列參數(command-line arguments)
```
#include <stdio.h>

int main( int argc, char *argv[] )  
{
   if( argc == 2 )
   {
      printf("The argument supplied is %s\n", argv[1]);
   }
   else if( argc > 2 )
   {
      printf("Too many arguments supplied.\n");
   }
   else
   {
      printf("One argument expected.\n");
   }
}
```
## switch==> 執行底下程式 說明其結果為何會如此呈現? 
```
#include <stdio.h>
 
int main ()
{
   /* 區域變數定義 */
   char grade = 'B';
 
   switch(grade)
   {
   case 'A' :
      printf("很棒！\n" );
      //break;
   case 'B' :
   case 'C' :
      printf("做得好\n" );
      //break;
   case 'D' :
      printf("您通過了\n" );
      //break;
   case 'F' :
      printf("最好再試一下\n" );
      //break;
   default :
      printf("無效的成績\n" );
   }
   printf("您的成績是 %c\n", grade );
 
   return 0;
}
```
```
將 //break ==> 去掉// ==> 執行後答案有何不同?
```
# 5.迴圈 
```
for   
while     
do.. while
```
## for loop(迴圈)  ==> 計算n!
```
#include <stdio.h>

int main(void)
{
	int n;
	int total = 1;
	int i;

	scanf("%d", &n);

	for(i = 1; i <= 10; i++)
		total *= i;

	printf("the result is %d\n", total);

	return 0;
}
```
## while loop ==> 計算n!
```
#include <stdio.h>

int main(void)
{
	int n;
	int mul = 1;
	int i;

	scanf("%d", &n);
	
	i = 1;
	while(i <= n)
	{
		mul *= i;
		i++;
	};

	printf("the result is %d\n", mul);

	return 0;
}
```
## do ..while .. ==> 計算n!
```
//do_while
#include <stdio.h>

int main(void)
{
	int n;
	int mul = 1;
	int i;

	scanf("%d", &n);
	
	i = 1;
	do{
		mul *= i;
		i++;
	}while(i <= n);

	printf("the result is %d\n", mul);

	return 0;
}
```

# 6.函數
```
#include <stdio.h>
 
int ifactorial(int z)
{
	int mul = 1, i = 1;
	while(i <= z)
	{
		mul *= i;
		i++;
	};
	return mul;
}

int  main()
{
    int i = 4;
    printf("%d 的階乘為%d\n", i, ifactorial(i));
    return 0;
}
```

## 遞迴函數 ==> 計算n!
```
#include <stdio.h>
 
double factorial(unsigned int i)
{
   if(i <= 1)
      return 1;
   else   return i * factorial(i - 1);
}

int  main()
{
    int i = 15;
    printf("%d 的階乘為%f\n", i, factorial(i));
    return 0;
}
```
# 7.陣列(不使用指標) ==> 使用索引(index) 存取陣列資料 ==> 再用pointer做一次
```
#include <stdio.h>
 
int main ()
{
   int n[ 10 ]; /* n 是一個包含 10 個整數的陣列 */
   int i,j;
 
   /* 初始化陣列元素 */         
   for ( i = 0; i < 10; i++ )
   {
      n[ i ] = i + 100; /* 設置元素 i 為 i + 100 */
   }
   
   /* 輸出陣列中每個元素的值 */
   for (j = 0; j < 10; j++ )
   {
      printf("Element[%d] = %d\n", j, n[j] );
   }
 
   return 0;
}

```
# 8.字串(字元陣列)與字串處理(不使用指標)

## 範例
```
#include <stdio.h>
#include <string.h>
 
int main ()
{
   char str1[9] = "CTFer";
   char str2[9] = "hacker";
   char str3[9];
   char str4[9];
   int  len ;
 
   /* 複製 str1 的內容複製到 str3 */
   strcpy(str3, str1);
   printf("strcpy( str3, str1) :  %s\n", str3 );
 
   /* 連接 str1 和 str2後的結果 存到str1 */
   strcat( str1, str2);
   printf("strcat( str1, str2):   %s\n", str1 );
 
    /* 連接 str2 和 str1後的結果 存到str1   */
   strcat( str2, str1);
   printf("strcat( str2, str1):   %s\n", str2 );
   
   /* 連接後，str1 的總長度 */
   len = strlen(str1);
   printf("strlen(str1) :  %d\n", len );
 
   strcpy(str4, str1);
   printf("strcpy( str4, str1) :  %s\n", str3 );
   str4[3] = '\0';
   printf(str4);
   
   return 0;
}
```
```
https://www.onlinegdb.com/online_c_compiler 

執行結果
main.c:38:11: warning: format not a string literal and no format arguments [-Wformat-security]    
    printf(str4 );                                                                                
           ^~~~                                                                                   
strcpy( str3, str1) :  CTFer                                                                      
strcat( str1, str2):   CTFerhacker                                                                
strcat( str2, str1):   erCTFerhacker                                                              
strlen(str1) :  22                                                                                
strcpy( str4, str1) :  cker                                                                       
*** stack smashing detected ***: ./a.out terminated                                               
CTFAborted (core dumped)    
```

## 修正後的程式
```
#include <stdio.h>
#include <string.h>
 
int main ()
{
   char str1[9] = "CTFer";
   char str2[9] = "hacker";
   char str3[9];
   char str4[9];
   int  len ;
 
   /* 複製 str1 的內容複製到 str3 與str 4 */
   strcpy(str4, str1);
   strcpy(str3, str1);
   printf("strcpy( str3, str1) :  %s\n", str3 );
 
   /* 連接 str1 和 str2後的結果 存到str1 */
   strcat( str1, str2);
   printf("strcat( str1, str2):   %s\n", str1 );
 
    /* 連接 str2 和 str1後的結果 存到str1   */
   //strcat( str2, str1);
   //printf("strcat( str2, str1):   %s\n", str2 );
   
   /* 連接後，str1 的總長度 */
   len = strlen(str1);
   printf("strlen(str1) :  %d\n", len );
 
   printf("strcpy( str4, str1) :  %s\n", str4 );
   str4[3] = '\0';
   printf("處理過的字串變成(請說明why?) :  %s\n",str4);
   
   return 0;
}
```
