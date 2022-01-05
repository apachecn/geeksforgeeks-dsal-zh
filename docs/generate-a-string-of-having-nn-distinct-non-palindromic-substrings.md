# 生成具有 N*N 个不同的非回文子串的字符串

> 原文:[https://www . geesforgeks . org/generate-a-string-of-having-nn-distinct-non-回文-substrings/](https://www.geeksforgeeks.org/generate-a-string-of-having-nn-distinct-non-palindromic-substrings/)

给定一个偶数 **N** ，任务是构造一个字符串，使得该字符串中不是回文的**不同**子字符串的总数等于**N<sup>2</sup>T9】。**

**示例:**

> **输入:** N = 2
> **输出:** aabb
> **解释:**
> 所有不同的非回文子串都是 **ab、abb、aab 和 aabb** 。
> 因此，非回文子串的计数为 4 = 2 <sup>2</sup>
> **输入:** N = 4
> **输出:**cczzz
> **解释:**
> 该字符串所有不同的非回文子串为 **cz，czz，czzzz，ccz，cczzz，cczzz，cczzz，cczzz，cczzz，ccczz，cccz
> 非回文子串数为 16 个。**

**方法:**
可以观察到，如果一个字符串的第一个 **N** 字符是相同的，接着是与第一个 **N** 字符不同的 **N** 相同的字符，那么不同的非回文子串的计数将是 **N <sup>2</sup>** 。

> **证明:**
> 
> N = 3
> str = "aaabbb"
> 该字符串可以分成两个子串 **N** 个字符，每个子串为:“aaa”和“BBB”
> 第一个子串的第一个字符‘a’与第二子串形成 **N** 个不同的非回文子串“ab”、“abb”、“abbb”。
> 同样，前两个字符“aa”形成 N 个不同的非回文子串“aab”、“aabb”、“aabbb”。
> 同样，第一个子串剩余的 N-2 个字符也形成了不同的非回文子串。
> 因此，不同的非回文子串总数等于 **N <sup>2</sup>** 。

因此，要解决这个问题，打印**a‘**作为字符串的第一个 **N** 字符，**b‘**作为字符串的下一个 **N** 字符。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct a string
// having N*N non-palindromic substrings
void createString(int N)
{
    for (int i = 0; i < N; i++) {
        cout << 'a';
    }
    for (int i = 0; i < N; i++) {
        cout << 'b';
    }
}

// Driver Code
int main()
{
    int N = 4;

    createString(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

// Function to construct a string
// having N*N non-palindromic substrings
static void createString(int N)
{
    for (int i = 0; i < N; i++)
    {
        System.out.print('a');
    }
    for (int i = 0; i < N; i++)
    {
        System.out.print('b');
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;

    createString(N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to construct a string
# having N*N non-palindromic substrings
def createString(N):

    for i in range(N):
        print('a', end = '')
    for i in range(N):
        print('b', end = '')

# Driver Code
N = 4

createString(N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to construct a string
// having N*N non-palindromic substrings
static void createString(int N)
{
    for(int i = 0; i < N; i++)
    {
        Console.Write('a');
    }
    for(int i = 0; i < N; i++)
    {
        Console.Write('b');
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4;

    createString(N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to construct a string
// having N*N non-palindromic substrings
function createString(N)
{
    for (let i = 0; i < N; i++)
    {
        document.write('a');
    }
    for (let i = 0; i < N; i++)
    {
        document.write('b');
    }
}

// Driver Code

        let N = 4;

    createString(N);

</script>
```

**Output:** 

```
aaaabbbb
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*