# 打印给定数字的所有可能的算术表达式

> 原文:[https://www . geeksforgeeks . org/print-给定数字的所有可能算术表达式/](https://www.geeksforgeeks.org/print-all-the-possible-arithmetic-expressions-for-a-given-number/)

给定一个整数 N，任务是使用从 1 到 N 的所有数字以及二进制运算符+、–、*和/，打印所有可能的算术表达式。
**例:**

> **输入:** n = 2
> **输出:**
> 1+2，1-2，1/2，1*2
> **输入:** n = 3
> **输出:**
> 1+2+3，1+2-3，1+2/3，1+2*3，1-2+3，1-2-3，1-2/3，1-2*3
> 1/2+3，1

**进场:**

*   我们将创建一个长度为=**n+n–1**的字符数组，因为要使带有 **n 个操作数**的表达式有效，我们需要 **n-1 个运算符**。

*   迭代数组，将数字放在偶数位置，而将符号放在奇数位置，并递归调用函数。

*   如果字符数等于数组长度，则打印数组。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print all the
// expressions for the input value

#include<iostream>
#include<bits/stdc++.h>
using namespace std;

// Function to print all the
// expressions using the number
void PrintRecursive(char *str,int arr[],
                 int i, int n,char *res,
                 int j, int len,int ln)
{
    // Termination condition
    if(j==len)
    {
        res[j]='\0';
        cout<<res<<endl;
        return;
    }
    // Even position will contain
    // the numbers
    if(j%2==0)
    {
        res[j]='0'+arr[i];

        // Recursive call
         PrintRecursive(str,arr,i+1,n,res,
                        j+1,len,ln);
    }
    else
    {
        // Add a symbol from string in
        // odd position.
        for(int k=0;k<ln;k++)
        {
            res[j]=str[k];
            PrintRecursive(str,arr,i,n,res,
                           j+1,len,ln);
        }
    }
}

void PrintExpressions(int n)
{
    // Character array containing
    // expressions
    char str[4]={'+','-','/','*'};

    str[4]='\0';

    int ln=strlen(str);

    int a[n];
    for(int i=0;i<n;i++)
    {
        a[i] = i + 1;
    }
    char res[( 2 * n ) - 1];

    PrintRecursive(str,a,0,n,res,0,
                   2*n-1,ln);
    return;
}

//Driver code
int main()
{
    int n = 2;

    PrintExpressions(n);

    return 0;
}
```

**Output:** 

```
1+2
1-2
1/2
1*2
```