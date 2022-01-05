# 检查整数溢出

> 原文:[https://www.geeksforgeeks.org/check-for-integer-overflow/](https://www.geeksforgeeks.org/check-for-integer-overflow/)

写一个“C”函数，int addOvf(int* result，int a，int b)如果没有溢出，该函数将结果= sum a+b 放入“result”中并返回 0。否则返回-1。不允许使用长整型和加法检测溢出的解决方案。

**方法 1**
只有两个数的符号相同，且和的符号与数的符号相反，才能有溢出。

```
1)  Calculate sum
2)  If both numbers are positive and sum is negative then return -1
     Else 
        If both numbers are negative and sum is positive then return -1
        Else return 0

```

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* Takes pointer to result and two numbers as 
    arguments. If there is no overflow, the function 
    places the resultant = sum a+b in “result” and 
    returns 0, otherwise it returns -1 */
int addOvf(int* result, int a, int b) 
{ 
    *result = a + b; 
    if(a > 0 && b > 0 && *result < 0) 
        return -1; 
    if(a < 0 && b < 0 && *result > 0) 
        return -1; 
    return 0; 
} 

// Driver code
int main() 
{ 
    int *res = new int[(sizeof(int))]; 
    int x = 2147483640; 
    int y = 10; 

    cout<<addOvf(res, x, y); 

    cout<<"\n"<<*res; 
    return 0; 
} 

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#include<stdlib.h>

/* Takes pointer to result and two numbers as
    arguments. If there is no overflow, the function
    places the resultant = sum a+b in “result” and
    returns 0, otherwise it returns -1 */
 int addOvf(int* result, int a, int b)
 {
     *result = a + b;
     if(a > 0 && b > 0 && *result < 0)
         return -1;
     if(a < 0 && b < 0 && *result > 0)
         return -1;
     return 0;
 }

 int main()
 {
     int *res = (int *)malloc(sizeof(int));
     int x = 2147483640;
     int y = 10;

     printf("%d", addOvf(res, x, y));

     printf("\n %d", *res);
     getchar();
     return 0;
}
```

**Output:**

```
-1
-2147483646

```