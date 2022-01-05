# 给定数字每个数字频率的 2 的最近幂

> 原文:[https://www . geeksforgeeks . org/给定数字的每位数频率的最近 2 次方/](https://www.geeksforgeeks.org/nearest-power-of-2-of-frequencies-of-each-digit-of-a-given-number/)

给定一个正整数 **N** ，任务是[打印 **N** 中出现的每个数字的频率的最近 2 次幂](https://www.geeksforgeeks.org/find-the-nearest-power-of-2-for-every-array-element/)。如果任何频率存在两个最接近的 2 的幂，则打印较大的一个。

**示例:**

> **输入:** N = 344422
> **输出:**
> 2->2
> 3->1
> 4->4
> **说明:**
> 数字 3 的频率为 1。2 的最近幂是 1。
> 数字 4 的频率为 3。2 的最近幂是 4。
> 数字 2 的频率为 2。2 的最近幂是 2。
> 
> **输入:** N = 16333331163
> **输出:**
> 3->8
> 1->4
> 6->2

**方法:**给定的问题可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来解决。按照以下步骤解决给定的问题:

*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，说 **S** 并转换给定的整数 **N** 并存储在字符串 **S** 中。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**S**[将每个字符](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)的频率存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，比如说 **M** 。
*   现在，[遍历](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) [地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** ，打印[存储在**地图**中的每个数字的频率的最近 2 次幂](https://www.geeksforgeeks.org/find-the-nearest-power-of-2-for-every-array-element/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest power of
// 2 for all frequencies in the Map freq
void nearestPowerOfTwoUtil(
    unordered_map<char, int>& freq)
{
    // Traverse the Map
    for (auto& it : freq) {

        cout << it.first << " -> ";

        // Calculate log of the
        // current array element
        int lg = log2(it.second);
        int a = pow(2, lg);
        int b = pow(2, lg + 1);

        // Find the nearest power of 2
        // for the current frequency
        if ((it.second - a)
            < (b - it.second)) {
            cout << a << endl;
        }
        else {
            cout << b << endl;
        }
    }
}

// Function to find nearest power of 2
// for frequency of each digit of num
void nearestPowerOfTwo(string& S)
{
    // Length of string
    int N = S.size();

    // Stores the frequency of each
    // character in the string
    unordered_map<char, int> freq;

    // Traverse the string S
    for (int i = 0; i < N; i++) {
        freq[S[i]]++;
    }

    // Function call to generate
    // nearest power of 2 for each
    // frequency
    nearestPowerOfTwoUtil(freq);
}

// Driver Code
int main()
{
    string N = "16333331163";
    nearestPowerOfTwo(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to find the nearest power of
  // 2 for all frequencies in the Map freq
  static void nearestPowerOfTwoUtil(HashMap<Character, Integer> freq)
  {

    // Traverse the Map
    for (char key : freq.keySet())
    {
      System.out.print(key + " -> ");

      // Calculate log of the
      // current array element
      int lg = (int)(Math.log(freq.get(key) / Math.log(2)));
      int a = (int)Math.pow(2, lg);
      int b = (int)Math.pow(2, lg + 1);

      // Find the nearest power of 2
      // for the current frequency
      if ((freq.get(key) - a) < (b - freq.get(key))) {
        System.out.println(a);
      }
      else {
        System.out.println(b);
      }
    }
  }

  // Function to find nearest power of 2
  // for frequency of each digit of num
  static void nearestPowerOfTwo(String S)
  {

    // Length of string
    int N = S.length();

    // Stores the frequency of each
    // character in the string
    HashMap<Character, Integer> freq = new HashMap<>();

    // Traverse the string S
    for (int i = 0; i < N; i++)
    {
      freq.put(S.charAt(i), freq.getOrDefault(S.charAt(i), 0) + 1);
    }

    // Function call to generate
    // nearest power of 2 for each
    // frequency
    nearestPowerOfTwoUtil(freq);
  }

  // Driver Code
  public static void main(String[] args)
  {

    String N = "16333331163";
    nearestPowerOfTwo(N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2, pow

# Function to find the nearest power of
# 2 for all frequencies in the Map freq
def nearestPowerOfTwoUtil(freq):

    # Traverse the Map
    temp = {}
    for key,value in freq.items():

        # Calculate log of the
        # current array element
        lg = int(log2(value))
        a  =  int(pow(2, lg))
        b  =  int(pow(2, lg + 1))

        # Find the nearest power of 2
        # for the current frequency
        if ((value - a) < (b - value)):
            temp[(int(a))] = key
        else:
            temp[(int(b))] = key
    for key,value in temp.items():
        print(value,"->",key)

# Function to find nearest power of 2
# for frequency of each digit of num
def nearestPowerOfTwo(S):

    # Length of string
    N = len(S)

    # Stores the frequency of each
    # character in the string
    freq = {}

    # Traverse the string S
    for i in range(N):
        if(S[i] in freq):
            freq[S[i]] += 1
        else:
            freq[S[i]] = 1

    # Function call to generate
    # nearest power of 2 for each
    # frequency
    nearestPowerOfTwoUtil(freq)

# Driver Code
if __name__ == '__main__':
    N = "16333331163"
    nearestPowerOfTwo(N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the nearest power of
// 2 for all frequencies in the Map freq
static void nearestPowerOfTwoUtil(
    Dictionary<char, int> freq)
{

    // Traverse the Map
    foreach (KeyValuePair<char, int> entry in freq)
    {
        char key = entry.Key;
        Console.Write(key + " -> ");

        // Calculate log of the
        // current array element
        int lg = (int)(Math.Log(freq[key] /
                       Math.Log(2)));
        int a = (int)Math.Pow(2, lg);
        int b = (int)Math.Pow(2, lg + 1);

        // Find the nearest power of 2
        // for the current frequency
        if ((freq[key] - a) < (b - freq[key]))
        {
            Console.Write(a + "\n");
        }
        else
        {
            Console.Write(b + "\n");
        }
    }
}

// Function to find nearest power of 2
// for frequency of each digit of num
static void nearestPowerOfTwo(string S)
{

    // Length of string
    int N = S.Length;

    // Stores the frequency of each
    // character in the string
    Dictionary<char,
               int> freq = new Dictionary<char,
                                          int>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {
        if (freq.ContainsKey(S[i]))
            freq[S[i]] += 1;
        else
            freq[S[i]] = 1;
    }

    // Function call to generate
    // nearest power of 2 for each
    // frequency
    nearestPowerOfTwoUtil(freq);
}

// Driver Code
public static void Main()
{
    string N = "16333331163";

    nearestPowerOfTwo(N);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the nearest power of
// 2 for all frequencies in the Map freq
function nearestPowerOfTwoUtil(freq)
{
    // Traverse the Map
    freq.forEach((value, key) => {
        document.write( key + " -> ");

        // Calculate log of the
        // current array element
        var lg = parseInt(Math.log2(value));
        var a = Math.pow(2, lg);
        var b = Math.pow(2, lg + 1);

        // Find the nearest power of 2
        // for the current frequency
        if ((value - a)
            < (b - value)) {
            document.write( a + "<br>");
        }
        else {
            document.write( b + "<br>");
        }
    });
}

// Function to find nearest power of 2
// for frequency of each digit of num
function nearestPowerOfTwo(S)
{
    // Length of string
    var N = S.length;

    // Stores the frequency of each
    // character in the string
    var freq = new Map();

    // Traverse the string S
    for (var i = 0; i < N; i++) {

        if(freq.has(S[i]))
        {
            freq.set(S[i], freq.get(S[i])+1)
        }
        else
        {
            freq.set(S[i], 1)
        }
    }

    // Function call to generate
    // nearest power of 2 for each
    // frequency
    nearestPowerOfTwoUtil(freq);
}

// Driver Code
var N = "16333331163";
nearestPowerOfTwo(N);

</script>
```

**Output:** 

```
3 -> 8
1 -> 4
6 -> 2
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*