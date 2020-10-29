# 检查给定字符串的字符是否可用于形成 N 个相等的字符串

> 原文：[https://www.geeksforgeeks.org/check-if-characters-of-a-given-string-can-be-used-to-form-any-n-equal-strings/](https://www.geeksforgeeks.org/check-if-characters-of-a-given-string-can-be-used-to-form-any-n-equal-strings/)

给定字符串 **S** 和整数 **N** ，任务是检查是否有可能从给定字符串的字符中生成 N N 次的任何字符串**或 不。 如果可能，打印**是**。 否则，打印**否**。**

**示例**：

> **输入**：S =“ caacbb”，N = 2
> **输出**：是
> **说明**：可以生成的所有可能的字符串 N（= 2）时间为{“ abc”，“ ab”，“ aa”，“ bb”，“ cc”，“ bc”，“ ca”}
> 
> **输入**：S =“ cbacbac”，N = 3
> **输出**：否
> 说明：由于没有字符出现 N 次，因此无法生成字符串 N 给定字符串的字符次数。

**天真的方法**：解决问题的最简单方法是[生成给定字符串所有可能长度的所有可能排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，并检查是否发生任何排列 **N** 次 或不。 如果发现是真的，则打印“ **是”** 。 否则，打印“ **否”**

**时间复杂度**：O（N * L！），其中 L 是给定字符串的长度。

**辅助空间**：O（L）

**高效方法**：的想法是存储所有字符的频率，并计算至少 **N** 次出现的字符数。 请按照以下步骤解决问题：

1.  将字符串的每个字符的频率存储在一个数组中，例如 **freq []** 。

2.  遍历 **freq []** 数组，并对于第 i 个<sup>第</sup>个字符，检查 **freq [i] > = N** 。

3.  如果发现任何字符满足上述条件，请打印**是**。 否则，打印**否**。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the freq of
// any charcater is divisible by N
bool isSame(string str, int n)
{
    // Stores the frequency of characters
    map<int, int> mp;

    for (int i = 0; i < str.length(); i++) {
        mp[str[i] - 'a']++;
    }

    for (auto it : mp) {

        // If frequency of a character
        // is not divisible by n
        if ((it.second) >= n) {
            return true;
        }
    }

    // If no character has frequency
    // at least N
    return false;
}

// Driver Code
int main()
{
    string str = "ccabcba";
    int n = 4;

    // Function Call
    if (isSame(str, n)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
class GFG{

// Function to check if the freq of
// any charcater is divisible by N
static boolean isSame(String str, int n)
{
    // Stores the frequency of characters
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    for (int i = 0; i < str.length(); i++) 
    {
        if(mp.containsKey(str.charAt(i) - 'a'))
        {
            mp.put(str.charAt(i) - 'a', 
                   mp.get(str.charAt(i) - 'a') + 1);
        }
          else
        {
            mp.put(str.charAt(i) - 'a', 1);
        }
    }

    for (Map.Entry<Integer, Integer> it : mp.entrySet()) 
    {
        // If frequency of a character
        // is not divisible by n
        if ((it.getValue()) >= n) 
        {
            return true;
        }
    }

    // If no character has frequency
    // at least N
    return false;
}

// Driver Code
public static void main(String[] args)
{
    String str = "ccabcba";
    int n = 4;

    // Function Call
    if (isSame(str, n)) 
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program for the above approach 
from collections import defaultdict

# Function to check if the freq of
# any charcater is divisible by N 
def isSame(str, n):

    # Stores the frequency of characters
    mp = defaultdict(lambda : 0)

    for i in range(len(str)):
        mp[ord(str[i]) - ord('a')] += 1

    for it in mp.keys():

        # If frequency of a character
        # is not divisible by n
        if(mp[it] >= n):
            return True

    # If no character has frequency
    # at least N
    return False

# Driver Code
str = "ccabcba"
n = 4

# Function call
if(isSame(str, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check if the freq of
// any charcater is divisible by N
static bool isSame(String str, int n)
{
    // Stores the frequency of characters
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    for (int i = 0; i < str.Length; i++) 
    {
        if(mp.ContainsKey(str[i] - 'a'))
        {
            mp[str[i] - 'a'] = 
                   mp[str[i] - 'a'] + 1;
        }
          else
        {
            mp.Add(str[i] - 'a', 1);
        }
    }

    foreach (KeyValuePair<int, 
                          int> it in mp) 
    {
        // If frequency of a character
        // is not divisible by n
        if ((it.Value) >= n) 
        {
            return true;
        }
    }

    // If no character has frequency
    // at least N
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "ccabcba";
    int n = 4;

    // Function Call
    if (isSame(str, n)) 
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
No

```

**时间复杂度**：O（L），其中 L 是给定字符串的长度

**辅助空间**：O（L）



* * *

* * *



