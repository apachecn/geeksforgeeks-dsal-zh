# 找出前 K 个字母频率相同的最长子序列的长度

> 原文:[https://www . geeksforgeeks . org/find-长度最长的子序列与第一个 k 字母具有相同的频率/](https://www.geeksforgeeks.org/find-the-length-of-the-longest-subsequence-with-first-k-alphabets-having-same-frequency/)

给定带有大写字符的字符串**和整数 **K** ，任务是找到最长子序列的长度，使得第一个 **K** 字母表的频率相同。**

**示例:**

> **输入:** str = "ACAABCCAB "，K=3
> **输出:** 6
> **解释:**可能的子序列之一是“ACABCB”。
> 
> **输入:** str = "ACAABCCAB "，K=4
> **输出:** 0
> **说明:**由于字符串中不包含‘D’，所以无法得到这样的子序列。

**方法:**
遍历字符串，找到第一个 **K** 字母中最不频繁的一个。一旦找到，**(该元素的频率)* K** 会给出所需的结果。
以下是上述方法的实现:

## C++

```
// C++ program to find the longest
// subsequence with first K
// alphabets having same frequency

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// length of the longest
// subsequence with first K
// alphabets having same frequency
int lengthOfSubsequence(string str,
                            int K)
{
    // Map to store frequency
    // of all characters in
    // the string
    map<char,int> mp;
    for (char ch : str) {
        mp[ch]++;
    }

    // Variable to store the
    // frequency of the least
    // frequent of first K
    // alphabets
    int minimum = mp['A'];
    for (int i = 1; i < K; i++) {
        minimum = min(minimum,
                    mp[(char)(i + 'A')]);
    }

    return minimum * K;
}

int main()
{
    string str = "ACAABCCAB";
    int K = 3;

    cout << lengthOfSubsequence(str, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// subsequence with first K alphabets
// having same frequency
import java.util.*;

class GFG{

// Function to return the
// length of the longest
// subsequence with first K
// alphabets having same frequency
static int lengthOfSubsequence(String str,
                            int K)
{

    // Map to store frequency
    // of all characters in
    // the string
    Map<Character, Integer> mp = new HashMap<>();
    for(char ch : str.toCharArray())
    {
        mp.put(ch, mp.getOrDefault(ch, 0) + 1);
    }

    // Variable to store the
    // frequency of the least
    // frequent of first K
    // alphabets
    int minimum = mp.get('A');
    for(int i = 1; i < K; i++)
    {
        minimum = Math.min(minimum,
                        mp.get((char)(i + 'A')));
    }
    return minimum * K;
}

// Driver code
public static void main(String[] args)
{
    String str = "ACAABCCAB";
    int K = 3;

    System.out.println(lengthOfSubsequence(str, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the longest
# subsequence with first K alphabets
# having same frequency
from collections import defaultdict

# Function to return the
# length of the longest
# subsequence with first K
# alphabets having same frequency
def lengthOfSubsequence(st, K):

    # Map to store frequency
    # of all characters in
    # the string
    mp = defaultdict(int)
    for ch in st:
        mp[ch] += 1

    # Variable to store the
    # frequency of the least
    # frequent of first K
    # alphabets
    minimum = mp['A']

    for i in range(1, K):
        minimum = min(minimum,
                    mp[chr(i + ord('A'))])

    return (minimum * K)

# Driver code
if __name__ == "__main__":

    st = "ACAABCCAB"
    K = 3

    print(lengthOfSubsequence(st, K))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the longest
// subsequence with first K alphabets
// having same frequency
using System;
using System.Collections.Generic;

class GFG{

// Function to return the
// length of the longest
// subsequence with first K
// alphabets having same frequency
static int lengthOfSubsequence(string str,
                               int K)
{

    // Store frequency
    // of all characters in
    // the string
    Dictionary<char,
               int> mp = new Dictionary<char,
                                        int>();

    foreach(char ch in str.ToCharArray())
    {
        mp[ch] = mp.GetValueOrDefault(ch, 0) + 1;
    }

    // Variable to store the frequency
    // of the least frequent of first K
    // alphabets
    int minimum = mp['A'];
    for(int i = 1; i < K; i++)
    {
        minimum = Math.Min(minimum,
                           mp[(char)(i + 'A')]);
    }
    return minimum * K;
}

// Driver code
public static void Main(string[] args)
{
    string str = "ACAABCCAB";
    int K = 3;

    Console.Write(lengthOfSubsequence(str, K));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find the longest
// subsequence with first K
// alphabets having same frequency

// Function to return the
// length of the longest
// subsequence with first K
// alphabets having same frequency
function lengthOfSubsequence(str, K)
{
    // Map to store frequency
    // of all characters in
    // the string
    var mp = new Map();

    str.split('').forEach(ch => {
        if(mp.has(ch))
            mp.set(ch, mp.get(ch)+1)
        else   
            mp.set(ch, 1)
    });

    // Variable to store the
    // frequency of the least
    // frequent of first K
    // alphabets
    var minimum = mp.get('A');
    for (var i = 1; i < K; i++) {
        minimum = Math.min(minimum,
                    mp.get(String.fromCharCode(i + 'A'.charCodeAt(0))));
    }

    return minimum * K;
}

var str = "ACAABCCAB";
var K = 3;

document.write( lengthOfSubsequence(str, K));

</script>
```

**Output:** 

```
6
```