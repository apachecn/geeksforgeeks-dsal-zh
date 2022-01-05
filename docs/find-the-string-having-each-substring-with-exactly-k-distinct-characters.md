# 找到每个子串都有 K 个不同字符的字符串

> 原文:[https://www . geeksforgeeks . org/find-the-string-having-with-k-distinct-characters/](https://www.geeksforgeeks.org/find-the-string-having-each-substring-with-exactly-k-distinct-characters/)

给定两个整数 **N** 和 **K** 。任务是找到长度为 N 的**串，这样长度大于等于 **K** 的每个子串都正好有 **K** 个不同的字符。
**举例:**** 

```
Input: N=10, K=3
Output : ABCABCABCA
Explanation:
The output string has 3 distinct characters.

Input : N=20, K=7
Output : ABCDEFGABCDEFGABCDEF
Explanation:
The output string has 7 distinct characters.
```

**方法:**
解决上述问题的主要思路是打印不同的元素直到长度 **K** ，然后重复相同的元素直到 **N** 。
以下是上述方法的实施:

## C++

```
// C++ Program to Find the
// String having each substring
// with exactly K distinct characters
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// required output string
void findString(int N, int K)
{
    // Each element at index
    // i is modulus of K
    for (int i = 0; i < N; i++) {

        cout << char('A' + i % K);
    }
}

// Driver code
int main()
{
    // initialise integers N and K
    int N = 10;
    int K = 3;

    findString(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// string having each substring
// with exactly K distinct characters
import java.io.*;

class GFG {

// Function to find the
// required output string
static void findString(int N, int K)
{

    // Each element at index
    // i is modulus of K
    for (int i = 0; i < N; i++)
    {
        System.out.print((char)('A' + i % K));
    }
}

// Driver code
public static void main(String[] args)
{
    // Initialise integers N and K
    int N = 10;
    int K = 3;
    findString(N, K);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 Program to Find the
# String having each substring
# with exactly K distinct characters

# Function to find the
# required output string
def findString(N, K) :
    # Each element at index
    # i is modulus of K
    for i in range(N) :

        print(chr(ord('A') + i % K),end="");

# Driver code
if __name__ == "__main__" :
    # initialise integers N and K
    N = 10;
    K = 3;

    findString(N, K);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the
// string having each substring
// with exactly K distinct characters
using System;

class GFG {

// Function to find the
// required output string
static void findString(int N, int K)
{

    // Each element at index
    // i is modulus of K
    for(int i = 0; i < N; i++)
    {
       Console.Write((char)('A' + i % K));
    }
}

// Driver code
public static void Main(String[] args)
{

    // Initialise integers N and K
    int N = 10;
    int K = 3;

    findString(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript Program to Find the
    // String having each substring
    // with exactly K distinct characters

    // Function to find the
    // required output string
    function findString(N, K)
    {

        // Each element at index
        // i is modulus of K
        for (let i = 0; i < N; i++)
        {
            document.write(String.fromCharCode('A'.charCodeAt() + i % K));
        }
    }

    // initialise integers N and K
    let N = 10;
    let K = 3;

    findString(N, K);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
ABCABCABCA
```

**时间复杂度:** O(N)