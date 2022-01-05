# 找出使用给定字符串的不同字符形成的字符串数量

> 原文:[https://www . geeksforgeeks . org/find-使用给定字符串的不同字符形成的字符串数/](https://www.geeksforgeeks.org/find-the-number-of-strings-formed-using-distinct-characters-of-a-given-string/)

给定一个由小写英文字母组成的字符串 **str** ，任务是找到所有可能的最大长度字符串的计数，这些字符串可以使用 **str** 的字符形成，这样生成的字符串中没有两个字符相同。
**例:**

> **输入:** str = "aba"
> **输出:**2
> “ab”和“ba”是唯一有效的字符串。
> **输入:** str = "geeksforgeeks"
> **输出:** 5040

**方法:**首先，计算字符串中不同字符的数量，说 **cnt** ，因为在结果字符串中没有两个字符可以相同。现在可以用 **cnt** 字符数组成的字符串总数是 **cnt！**由于**字符串**的每个字符都必须出现在生成的字符串中，以便最大化长度，因此任何字符都不应出现一次以上。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the factorial of n
int fact(int n)
{
    int fact = 1;
    for (int i = 1; i <= n; i++)
        fact *= i;

    return fact;
}

// Function to return the count of all
// possible strings that can be formed
// with the characters of the given string
// without repeating characters
int countStrings(string str, int n)
{

    // To store the distinct characters
    // of the string str
    set<char> distinct_char;
    for (int i = 0; i < n; i++) {
        distinct_char.insert(str[i]);
    }

    return fact(distinct_char.size());
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int n = str.length();

    cout << countStrings(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the factorial of n
static int fact(int n)
{
    int fact = 1;
    for (int i = 1; i <= n; i++)
        fact *= i;

    return fact;
}

// Function to return the count of all
// possible strings that can be formed
// with the characters of the given string
// without repeating characters
static int countStrings(String str, int n)
{

    // To store the distinct characters
    // of the string str
    Set<Character> distinct_char = new HashSet<>();
    for (int i = 0; i < n; i++)
    {
        distinct_char.add(str.charAt(i));
    }

    return fact(distinct_char.size());
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.length();

    System.out.println(countStrings(str, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the factorial of n
def fact(n) :

    fact = 1;
    for i in range(1, n + 1) :
        fact *= i;

    return fact;

# Function to return the count of all
# possible strings that can be formed
# with the characters of the given string
# without repeating characters
def countStrings(string, n) :

    # To store the distinct characters
    # of the string str
    distinct_char = set();
    for i in range(n) :
        distinct_char.add(string[i]);

    return fact(len(distinct_char));

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    n = len(string);

    print(countStrings(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the factorial of n
static int fact(int n)
{
    int fact = 1;
    for (int i = 1; i <= n; i++)
        fact *= i;

    return fact;
}

// Function to return the count of all
// possible strings that can be formed
// with the characters of the given string
// without repeating characters
static int countStrings(String str, int n)
{

    // To store the distinct characters
    // of the string str
    HashSet<char> distinct_char = new HashSet<char>();
    for (int i = 0; i < n; i++)
    {
        distinct_char.Add(str[i]);
    }

    return fact(distinct_char.Count);
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.Length;

    Console.WriteLine(countStrings(str, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the factorial of n
    function fact(n)
    {
        let fact = 1;
        for (let i = 1; i <= n; i++)
            fact *= i;

        return fact;
    }

    // Function to return the count of all
    // possible strings that can be formed
    // with the characters of the given string
    // without repeating characters
    function countStrings(str, n)
    {

        // To store the distinct characters
        // of the string str
        let distinct_char = new Set();
        for (let i = 0; i < n; i++) {
            distinct_char.add(str[i]);
        }

        return fact(distinct_char.size);
    }

    let str = "geeksforgeeks";
    let n = str.length;

    document.write(countStrings(str, n));

</script>
```

**Output:** 

```
5040
```