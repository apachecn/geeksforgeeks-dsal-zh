# 用因式分解法求字符串的第 N 次字典排列

> 原文:[https://www . geeksforgeeks . org/find-the-n-th-字典排列-字符串排列-使用-factory adic-method/](https://www.geeksforgeeks.org/find-the-n-th-lexicographic-permutation-of-string-using-factoradic-method/)

给定带有唯一字符的字符串**和一个数字 **N** ，任务是使用因式分解法找到字符串的第 N 个字典排列。
**示例:****

> **输入:** str = "abc "，N = 3
> **输出:** bac
> **解释:**
> 排序顺序中所有可能的排列:abc、acb、bac、bca、cab、cba
> 第三个排列是 bac
> **输入:**str =【ABA】，N = 2
> **输出:** aba
> **解释:**
> 排序顺序中所有可能的排列

**方法:**思路是使用因式表示的概念。因式分解法的主要概念是计算一个数的序列。以下是使用因式分解法寻找第 N 个字典排列的步骤:

1.  将 **N 减 1** ，因为此方法将排序顺序视为第 0 次排列。
2.  用 1 除以字符串的长度，每次将剩余部分存储在堆栈中，同时将 N 的值更新为 **N/i** 。
3.  每一步计算出的余数就是因式分解数。因此，在计算最终的 factoradic 表示后，开始在结果字符串中追加位置上的元素。
4.  每次迭代时从堆栈中移除元素。
5.  重复以上三个步骤，直到堆栈变空。

让我们用一个例子来理解这个方法。让弦线为**“abcde”**，N 为 **11** 。然后:

*   最初，从 n 中减去 1。

```
N = 11 - 1
N = 10
```

*   现在，在每次迭代中，用 I 除 N，其中 I 的范围从 1 到长度，并将余数存储在堆栈中:

```
divide       Remainder    Quotient     Factoradic
10%1           0            10              0
10%2           0             5             00
5%3            2             1            200
2%4            1             0           1200
2%5            0             0          01200  
```

*   现在，将元素追加到堆栈的结果字符串中，并不断从堆栈中移除元素。这里，给定数字的因式分解表示是 01200。因此:

```
[0]=a   <- Selected
[1]=b
[2]=d 
[3]=e
[4]=f

result = a

[0]=b
[1]=c <- Selected
[2]=d
[3]=e

result= ac

[0]=b
[1]=d
[2]=e <-Selected

result= ace

[0]=b <- Selected
[1]=d

result= aceb

[0]=d <-selected

result =acebd
```

*   因此，字符串的第 11 个排列是**“acebd”**。

以下是上述方法的实现:

## C++

```
// C++ program to find the N-th lexicographic
// permutation of string using Factroid method
#include <bits/stdc++.h>
using namespace std;

// Function to calculate nth permutation of string
void string_permutation(long long int n, string str)
{
    // Creating an empty stack
    stack<int> s;
    string result;

    // Subtracting 1 from N because the
    // permutations start from 0 in
    // factroid method
    n = n - 1;

    // Loop to generate the factroid
    // of the sequence
    for (int i = 1; i < str.size() + 1; i++) {
        s.push(n % i);
        n = n / i;
    }

    // Loop to generate nth permutation
    for (int i = 0; i < str.size(); i++) {
        int a = s.top();
        result += str[a];
        int j;

        // Remove 1-element in each cycle
        for (j = a; j < str.length(); j++)
            str[j] = str[j + 1];
        str[j + 1] = '\0';
        s.pop();
    }

    // Final answer
    cout << result << endl;
}

// Driver code
int main()
{
    string str = "abcde";
    long long int n = 11;

    string_permutation(n, str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th lexicographic
// permutation of String using Factroid method
import java.util.*;

class GFG{

// Function to calculate nth permutation of String
static void String_permutation(int n, String str)
{

    // Creating an empty stack
    Stack<Integer> s = new Stack<Integer>();
    String result = "";

    // Subtracting 1 from N because the
    // permutations start from 0 in
    // factroid method
    n = n - 1;

    // Loop to generate the factroid
    // of the sequence
    for(int i = 1; i < str.length() + 1; i++)
    {
       s.add(n % i);
       n = n / i;
    }

    // Loop to generate nth permutation
    for(int i = 0; i < str.length(); i++)
    {
       int a = s.peek();
       result += str.charAt(a);
       int j;

       // Remove 1-element in each cycle
       for(j = a; j < str.length() - 1; j++)
          str = str.substring(0, j) +
                str.charAt(j + 1) +
                str.substring(j + 1);

       str = str.substring(0, j + 1);
       s.pop();
    }

    // Final answer
    System.out.print(result + "\n");
}

// Driver code
public static void main(String[] args)
{
    String str = "abcde";
    int n = 11;

    String_permutation(n, str);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find
# the N-th lexicographic
# permutation of string
# using Factroid method

# Function to calculate
# nth permutation of string
def string_permutation(n, str):

    # Creating an empty list
    s = []
    result = ""
    str = list(str)

    # Subtracting 1 from N
    # because the permutations
    # start from 0 in factroid method
    n = n - 1

    # Loop to generate the
    # factroid of the sequence
    for i in range(1, len(str) + 1):
        s.append(n % i)
        n = int(n / i)

    # Loop to generate
    # nth permutation
    for i in range(len(str)):
        a = s[-1]
        result += str[a]

        # Remove 1-element in
        # each cycle
        for j in range(a, len(str) - 1):
            str[j] = str[j + 1]

        str[j + 1] = '\0'
        s.pop()

    # Final answer
    print(result)

# Driver code
str = "abcde"
n = 11
string_permutation(n, str)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find the N-th lexicographic
// permutation of String using Factroid method
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate nth permutation of String
static void String_permutation(int n, String str)
{

    // Creating an empty stack
    Stack<int> s = new Stack<int>();
    String result = "";

    // Subtracting 1 from N because the
    // permutations start from 0 in
    // factroid method
    n = n - 1;

    // Loop to generate the factroid
    // of the sequence
    for(int i = 1; i < str.Length + 1; i++)
    {
       s.Push(n % i);
       n = n / i;
    }

    // Loop to generate nth permutation
    for(int i = 0; i < str.Length; i++)
    {
       int a = s.Peek();
       result += str[a];
       int j;

       // Remove 1-element in each cycle
       for(j = a; j < str.Length - 1; j++)
       {
          str = str.Substring(0, j) +
                str[j + 1] +
                str.Substring(j + 1);
       }
       str = str.Substring(0, j + 1);
       s.Pop();
    }

    // Final answer
    Console.Write(result + "\n");
}

// Driver code
public static void Main(String[] args)
{
    String str = "abcde";
    int n = 11;

    String_permutation(n, str);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to find the N-th lexicographic
// permutation of string using Factroid method

// Function to calculate nth permutation of string
function string_permutation( n, str){
    // Creating an empty stack
    let s = [];
    let result = '';

    // Subtracting 1 from N because the
    // permutations start from 0 in
    // factroid method
    n = n - 1;

    // Loop to generate the factroid
    // of the sequence
    for (let i = 1; i < str.length + 1; i++) {
        s.push(n % i);
        n = Math.floor(n / i);
    }

    // Loop to generate nth permutation
    let len = str.length;
    for (let i = 0; i < len ; i++) {
        let a = s[s.length-1];
        result += str[a];
        let j;

        // Remove 1-element in each cycle
        for (j = a; j < str.length ; j++)
          str = str.substring(0, j) +
                str.charAt(j + 1) +
                str.substring(j + 1);

       str = str.substring(0, j + 1);

        s.pop();
    }

    // Final answer
    document.write(result,'<br>');
}

// Driver code
let str = "abcde";
n = 11;

string_permutation(n, str);

</script>
```

**Output:** 

```
acebd
```

**时间复杂度:** O(|str|)

**辅助空间:** O(|str|)

**注:**在[这篇文章](https://www.geeksforgeeks.org/lexicographically-n-th-permutation-string/)中讨论了用重复字符寻找第 N 个<sup>排列的方法。</sup>