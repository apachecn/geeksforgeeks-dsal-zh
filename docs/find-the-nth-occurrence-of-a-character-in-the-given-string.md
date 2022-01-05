# 查找给定字符串中第 n 次出现的字符

> 原文:[https://www . geeksforgeeks . org/find-第 n 次出现给定字符串中的字符/](https://www.geeksforgeeks.org/find-the-nth-occurrence-of-a-character-in-the-given-string/)

给定字符串 **str** 、字符 **ch** 和值 **N** ，任务是找到给定字符串中给定字符第 N 次出现的索引。如果不存在这种情况，打印-1。

**示例:**

> **输入:** str = "Geeks "，ch = 'e '，N = 2
> T3】输出: 2
> 
> **输入:** str = "GFG "，ch = 'e '，N = 2
> **输出:** -1

**进场:**

*   逐个字符遍历字符串。
*   检查每个字符是否与给定字符匹配。
*   如果计数与给定字符匹配，则将计数增加 1。
*   如果计数等于 N，则返回最新找到的索引
*   如果遍历后计数与 N 不匹配，返回-1

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// Nth occurrence of a character

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Nth occurrence of a character
int findNthOccur(string str,
                 char ch, int N)
{
    int occur = 0;

    // Loop to find the Nth
    // occurrence of the character
    for (int i = 0; i < str.length(); i++) {
        if (str[i] == ch) {
            occur += 1;
        }
        if (occur == N)
            return i;
    }
    return -1;
}

// Driver Code
int main()
{
    string str = "geeks";
    char ch = 'e';
    int N = 2;
    cout << findNthOccur(str, ch, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Nth occurrence of a character
import java.util.*;

class GFG
{

// Function to find the
// Nth occurrence of a character
static int findNthOccur(String str,
                    char ch, int N)
{
    int occur = 0;

    // Loop to find the Nth
    // occurrence of the character
    for (int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == ch)
        {
            occur += 1;
        }
        if (occur == N)
            return i;
    }
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    String str = "geeks";
    char ch = 'e';
    int N = 2;
    System.out.print(findNthOccur(str, ch, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Nth occurrence of a character

# Function to find the
# Nth occurrence of a character
def findNthOccur(string , ch, N) :
    occur = 0;

    # Loop to find the Nth
    # occurrence of the character
    for i in range(len(string)) :
        if (string[i] == ch) :
            occur += 1;

        if (occur == N) :
            return i;

    return -1;

# Driver Code
if __name__ == "__main__" :

    string = "geeks";
    ch = 'e';
    N = 2;
    print(findNthOccur(string, ch, N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// Nth occurrence of a character
using System;

class GFG
{

// Function to find the
// Nth occurrence of a character
static int findNthOccur(String str,
                    char ch, int N)
{
    int occur = 0;

    // Loop to find the Nth
    // occurrence of the character
    for (int i = 0; i < str.Length; i++)
    {
        if (str[i] == ch)
        {
            occur += 1;
        }
        if (occur == N)
            return i;
    }
    return -1;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "geeks";
    char ch = 'e';
    int N = 2;
    Console.Write(findNthOccur(str, ch, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// Nth occurrence of a character.

// Function to find the
// Nth occurrence of a character
function findNthOccur(str, ch, N)
{
    var occur = 0;

    // Loop to find the Nth
    // occurrence of the character
    for (var i = 0; i < str.length; i++) {
        if (str[i] == ch) {
            occur += 1;
        }
        if (occur == N)
            return i;
    }
    return -1;
}

var str = "geeks";
    var ch = 'e';
    var N = 2;
    document.write( findNthOccur(str, ch, N));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```