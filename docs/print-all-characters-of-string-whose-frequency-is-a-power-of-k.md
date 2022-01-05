# 打印频率为 K 次幂的字符串的所有字符

> 原文:[https://www . geesforgeks . org/print-全字符字符串，其频率是 k 的幂/](https://www.geeksforgeeks.org/print-all-characters-of-string-whose-frequency-is-a-power-of-k/)

给定大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **字符串**，任务是按照字典排序顺序打印频率为 **K** 幂的字符串字符。

**示例:**

> **输入:**str = " aacbb " K = 2
> **输出:** bbc
> **说明:**a 的频率是 3，不是 2 的幂。c 的频率是 1，b 的频率是 2，是 2 的幂。
> 
> **输入:**str = " geeksgeekgkeks " K = 3
> **输出:** eeeeeegggkkk

**天真方法:**想法是为字符串的每个字母计数频率，如果频率是 **K** 的幂，那么将其添加到新字符串中。[排序字符串](https://www.geeksforgeeks.org/sort-string-characters/)并打印。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**想法是使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)。以下是步骤:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并将每个字母的频率存储在地图中
*   [遍历地图](https://www.geeksforgeeks.org/iterate-map-java/)打印频率为 K 次方的字母

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the frequency
// of every alphabet in the string
// and print the alphabets with
// frequency as the power of K
void countFrequency(string str, int N, int K)
{

    // Map will store the frequency
    // of each alphabet of the string
    map<char, int> freq;

    // Store the frequency of each
    // alphabet of the string
    for (int i = 0; i < N; i++) {

        freq[str[i]]++;
    }

    // Traverse the Map
    for (auto i : freq) {

        // Calculate log of the
        // current string alphabet
        int lg = log2(i.second);

        // Power of 2 of the log value
        int a = pow(2, lg);

        if (a == i.second) {
            while (a--)
                cout << i.first << endl;
        }
    }
}

// Driver Code
int main()
{

    string str = "aaacbb";

    // Size of string
    int N = str.size();

    // Initialize K
    int K = 2;

    // Function call
    countFrequency(str, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG{

// Function to count the frequency
// of every alphabet in the String
// and print the alphabets with
// frequency as the power of K
static void countFrequency(String str, int N, int K)
{

    // Map will store the frequency
    // of each alphabet of the String
    HashMap<Character,
            Integer> freq = new HashMap<Character,
                                        Integer>();

    // Store the frequency of each
    // alphabet of the String
    for(int i = 0; i < N; i++)
    {

        if (freq.containsKey(str.charAt(i)))
        {
            freq.put(str.charAt(i),
            freq.get(str.charAt(i)) + 1);
        }
        else
        {
            freq.put(str.charAt(i), 1);
        }
    }

    // Traverse the Map
    for(Map.Entry<Character, Integer> i : freq.entrySet())
    {

        // Calculate log of the
        // current String alphabet
        int lg = (int)Math.ceil(Math.log(i.getValue()));

        // Power of 2 of the log value
        int a = (int)Math.pow(2, lg);

        if (a == i.getValue())
        {
            while (a-->0)
                System.out.print(i.getKey() + "\n");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "aaacbb";

    // Size of String
    int N = str.length();

    // Initialize K
    int K = 2;

    // Function call
    countFrequency(str, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python code for the above approach
import math

# Function to count the frequency
# of every alphabet in the string
# and print the alphabets with
# frequency as the power of K
def countFrequency(str, N, K):

    # Map will store the frequency
    # of each alphabet of the string
    freq = {}

    # Store the frequency of each
    # alphabet of the string
    for i in range(N):
        if str[i] in freq.keys():
            freq[str[i]] = freq[str[i]] + 1
        else:
            freq[str[i]] = 1

    # Traverse the Map
    for i in sorted(freq.keys()):

        # Calculate log of the
        # current string alphabet
        lg = math.floor(math.log2(freq[i]))

        # Power of 2 of the log value
        a = math.pow(2, lg)

        if a == freq[i]:
            while a != 0:
                print(i)
                a = a - 1

# Driver Code
str = "aaacbb"

# Size of string
N = len(str)

# Initialize K
K = 2

# Function call
countFrequency(str, N, K)

# This code is contributed by Potta Lokesh
```

## C#

```
// C# code for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{
// Function to count the frequency
// of every alphabet in the String
// and print the alphabets with
// frequency as the power of K
static void countFrequency(string str, int N, int K)
{

    // Map will store the frequency
    // of each alphabet of the String
    Dictionary<char, int> freq =
          new Dictionary<char, int>();

    // Store the frequency of each
    // alphabet of the String
    foreach(char i in str)
    {
        if(freq.ContainsKey(i))
        {
          freq[i]++;
        }
        else
        {
          freq[i]=1;
        }
    }
    ArrayList ch = new ArrayList();
    // Traverse the dict
    foreach(KeyValuePair<char, int> i in freq)
    {

        // Calculate log of the
        // current String alphabet
        int lg = (int)Math.Ceiling(Math.Log(i.Value));

        // Power of 2 of the log value
        int a = (int)Math.Pow(2, lg);
        if (a == i.Value)
        {
            while (a-->0)
                ch.Add(i.Key);
        }
    }
    ch.Sort();
    for(int i = 0; i < ch.Count; i++){
        Console.Write(ch[i] + "\n");
    }
}

// Driver Code
public static void Main () {

    string str = "aaacbb";

    // Size of String
    int N = str.Length;

    // Initialize K
    int K = 2;

    // Function call
    countFrequency(str, N, K);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to count the frequency
// of every alphabet in the string
// and print the alphabets with
// frequency as the power of K
function countFrequency(str, N, K) {

    // Map will store the frequency
    // of each alphabet of the string
    let freq = new Map();

    // Store the frequency of each
    // alphabet of the string
    for (let i = 0; i < N; i++) {
        if (freq.has(str[i])) {
            freq.set(str[i], freq.get(str[i]) + 1)
        } else {
            freq.set(str[i], 1)
        }
    }

    let ch = [];

    // Traverse the Map
    for (i of freq) {

        // Calculate log of the
        // current string alphabet
        let lg = Math.floor(Math.log2(i[1]));

        // Power of 2 of the log value
        let a = Math.pow(2, lg);

        if (a == i[1]) {
            while (a--)
                ch.push(i[0]);
        }
    }

    ch.sort()
    ch.forEach((val) => { document.write(val + "<br>") })
}

// Driver Code
let str = "aaacbb";

// Size of string
let N = str.length;

// Initialize K
let K = 2;

// Function call
countFrequency(str, N, K);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
b
b
c
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*