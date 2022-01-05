# 打印不同的排序排列，输入时允许重复

> 原文:[https://www . geesforgeks . org/print-distinct-sorted-排列-带重复-允许/](https://www.geeksforgeeks.org/print-distinct-sorted-permutations-with-duplicates-allowed/)

编写一个程序，按排序顺序打印给定字符串的所有不同排列。请注意，输入字符串可能包含重复字符。
在数学中，置换的概念涉及将集合的所有成员排列成某种序列或顺序的行为，或者如果集合已经排序，则重新排列(重新排序)其元素的行为，这一过程称为置换。
来源–[维基百科](https://en.wikipedia.org/wiki/Permutation)
**示例:**

> 输入:BAC
> 输出:ABC ACB BAC BCA CAB CBA
> 输入:AAB
> 输出:AAB ABA BAA
> 输入:DBCA
> 输出:ABCD ABDC ACBD ACDB ADBC ADCB BACD BADC BCAD BDAC BDCA CABD CADB CBAD CBDA CDAB DABC DABC DBAC DBCA DCAB DCBA

**使用的概念:**由长度为“n”的不同字符组成的字符串生成的字符串数等于“n！”。对任何给定的字符串进行排序，并生成字典序下一个更大的字符串，直到我们从这些字符中得到最大的字典序字符串。

> 单词“极客”的不同排列
> 字符串长度= 5
> 字符“e”重复 2 次。
> 成绩= 5！/2!= 60.

**步骤:**

**例:**考虑一个字符串“ABCD”。
**第一步:**整理字符串。
**第二步:**获取该字符串可形成的[排列总数。
**步骤 3:** 打印排序后的字符串，然后循环(排列-1)次，因为第一个字符串已经打印。
**第四步:**找到下一个更大的字符串](https://www.geeksforgeeks.org/number-distinct-permutation-string-can/)。
下面是这个问题的实现–

## C++

```
// C++ program to print all permutations
// of a string in sorted order.
#include <bits/stdc++.h>
using namespace std;

// Calculating factorial of a number
int factorial(int n)
{
    int f = 1;
    for (int i = 1; i <= n; i++)
        f = f * i;
    return f;
}

// Method to find total number of permutations
int calculateTotal(string temp, int n)
{
    int f = factorial(n);

    // Building Map to store frequencies of
    // all characters.
    map<char, int> hm;
    for (int i = 0; i < temp.length(); i++)
    {
        hm[temp[i]]++;
    }

    // Traversing map and
    // finding duplicate elements.
    for (auto e : hm)
    {
        int x = e.second;
        if (x > 1)
        {
            int temp5 = factorial(x);
            f /= temp5;
        }
        return f;
    }
}

static void nextPermutation(string &temp)
{

    // Start traversing from the end and
    // find position 'i-1' of the first character
    // which is greater than its successor.
    int i;
    for (i = temp.length() - 1; i > 0; i--)
        if (temp[i] > temp[i - 1]) break;

    // Finding smallest character after 'i-1' and
    // greater than temp[i-1]
    int min = i;
    int j, x = temp[i - 1];
    for (j = i + 1; j < temp.length(); j++)
        if ((temp[j] < temp[min]) and
            (temp[j] > x))
            min = j;

    // Swapping the above found characters.
    swap(temp[i - 1], temp[min]);

    // Sort all digits from position next to 'i-1'
    // to end of the string.
    sort(temp.begin() + i, temp.end());

    // Print the String
    cout << temp << endl;
}

void printAllPermutations(string s)
{

    // Sorting String
    string temp(s);
    sort(temp.begin(), temp.end());

    // Print first permutation
    cout << temp << endl;

    // Finding the total permutations
    int total = calculateTotal(temp, temp.length());
    for (int i = 1; i < total; i++)
    {
        nextPermutation(temp);
    }
}

// Driver Code
int main()
{
    string s = "AAB";
    printAllPermutations(s);
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all permutations of a string
// in sorted order.
import java.io.*;
import java.util.*;

class Solution {

  // Calculating factorial of a number
  static int factorial(int n) {
    int f = 1;
    for (int i = 1; i <= n; i++)
      f = f * i;
    return f;
  }

  // Method to print the array
  static void print(char[] temp) {
    for (int i = 0; i < temp.length; i++)
      System.out.print(temp[i]);
    System.out.println();
  }

  // Method to find total number of permutations
  static int calculateTotal(char[] temp, int n) {
    int f = factorial(n);

    // Building HashMap to store frequencies of
    // all characters.
    HashMap<Character, Integer> hm =
                     new HashMap<Character, Integer>();
    for (int i = 0; i < temp.length; i++) {
      if (hm.containsKey(temp[i]))
        hm.put(temp[i], hm.get(temp[i]) + 1);
      else
        hm.put(temp[i], 1);
    }

    // Traversing hashmap and finding duplicate elements.
    for (Map.Entry e : hm.entrySet()) {
      Integer x = (Integer)e.getValue();
      if (x > 1) {
        int temp5 = factorial(x);
        f = f / temp5;
      }
    }
    return f;
  }

  static void nextPermutation(char[] temp) {

    // Start traversing from the end and
    // find position 'i-1' of the first character
    // which is greater than its  successor.
    int i;
    for (i = temp.length - 1; i > 0; i--)
      if (temp[i] > temp[i - 1])
        break;

    // Finding smallest character after 'i-1' and
    // greater than temp[i-1]
    int min = i;
    int j, x = temp[i - 1];
    for (j = i + 1; j < temp.length; j++)
      if ((temp[j] < temp[min]) && (temp[j] > x))
        min = j;

    // Swapping the above found characters.
    char temp_to_swap;
    temp_to_swap = temp[i - 1];
    temp[i - 1] = temp[min];
    temp[min] = temp_to_swap;

    // Sort all digits from position next to 'i-1'
    // to end of the string.
    Arrays.sort(temp, i, temp.length);

    // Print the String
    print(temp);
  }

  static void printAllPermutations(String s) {

    // Sorting String
    char temp[] = s.toCharArray();
    Arrays.sort(temp);

    // Print first permutation
    print(temp);

    // Finding the total permutations
    int total = calculateTotal(temp, temp.length);
    for (int i = 1; i < total; i++)
      nextPermutation(temp);
  }

  // Driver Code
  public static void main(String[] args) {
    String s = "AAB";
    printAllPermutations(s);
  }
}
```

## 蟒蛇 3

```
# Python3 program to print
# all permutations of a
# string in sorted order.
from collections import defaultdict

# Calculating factorial
# of a number
def factorial(n):

    f = 1

    for i in range (1, n + 1):
        f = f * i
    return f

# Method to find total
# number of permutations
def calculateTotal(temp, n):

    f = factorial(n)

    # Building Map to store
    # frequencies of all
    # characters.
    hm = defaultdict (int)

    for i in range (len(temp)):
        hm[temp[i]] += 1

    # Traversing map and
    # finding duplicate elements.
    for e in hm:
        x = hm[e]
        if (x > 1):
            temp5 = factorial(x)
            f //= temp5
        return f

def nextPermutation(temp):

    # Start traversing from
    # the end and find position
    # 'i-1' of the first character
    # which is greater than its successor
    for i in range (len(temp) - 1, 0, -1):
        if (temp[i] > temp[i - 1]):
            break

    # Finding smallest character
    # after 'i-1' and greater
    # than temp[i-1]
    min = i
    x = temp[i - 1]
    for j in range (i + 1, len(temp)):
        if ((temp[j] < temp[min]) and
            (temp[j] > x)):
            min = j

    # Swapping the above
    # found characters.
    temp[i - 1], temp[min] = (temp[min],
                              temp[i - 1])

    # Sort all digits from
    # position next to 'i-1'
    # to end of the string
    temp[i:].sort()

    # Print the String
    print (''.join(temp))

def printAllPermutations(s):

    # Sorting String
    temp = list(s)
    temp.sort()

    # Print first permutation
    print (''.join( temp))

    # Finding the total permutations
    total = calculateTotal(temp,
                           len(temp))
    for i in range (1, total):
        nextPermutation(temp)

# Driver Code
if __name__ == "__main__":

    s = "AAB"
    printAllPermutations(s)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to print all permutations
// of a string in sorted order.
using System;
using System.Collections.Generic;

class GFG
{

// Calculating factorial of a number
static int factorial(int n)
{
    int f = 1;
    for (int i = 1; i <= n; i++)
    f = f * i;
    return f;
}

// Method to print the array
static void print(char[] temp)
{
    for (int i = 0; i < temp.Length; i++)
    Console.Write(temp[i]);
    Console.WriteLine();
}

// Method to find total number of permutations
static int calculateTotal(char[] temp, int n)
{
    int f = factorial(n);

    // Building Dictionary to store frequencies 
    // of all characters.
    Dictionary<char,
               int> hm = new Dictionary<char,
                                        int>();
    for (int i = 0; i < temp.Length; i++)
    {
        if (hm.ContainsKey(temp[i]))
            hm[temp[i]] = hm[temp[i]] + 1;
        else
            hm.Add(temp[i], 1);
    }

    // Traversing hashmap and
    // finding duplicate elements.
    foreach(KeyValuePair<char, int> e in hm)
    {
        int x = e.Value;
        if (x > 1)
        {
            int temp5 = factorial(x);
            f = f / temp5;
        }
    }
    return f;
}

static void nextPermutation(char[] temp)
{

    // Start traversing from the end and
    // find position 'i-1' of the first character
    // which is greater than its successor.
    int i;
    for (i = temp.Length - 1; i > 0; i--)
    if (temp[i] > temp[i - 1])
        break;

    // Finding smallest character after 'i-1'
    // and greater than temp[i-1]
    int min = i;
    int j, x = temp[i - 1];
    for (j = i + 1; j < temp.Length; j++)
    if ((temp[j] < temp[min]) && (temp[j] > x))
        min = j;

    // Swapping the above found characters.
    char temp_to_swap;
    temp_to_swap = temp[i - 1];
    temp[i - 1] = temp[min];
    temp[min] = temp_to_swap;

    // Sort all digits from position next to 'i-1'
    // to end of the string.
    Array.Sort(temp, i, temp.Length-i);

    // Print the String
    print(temp);
}

static void printAllPermutations(String s)
{

    // Sorting String
    char []temp = s.ToCharArray();
    Array.Sort(temp);

    // Print first permutation
    print(temp);

    // Finding the total permutations
    int total = calculateTotal(temp, temp.Length);
    for (int i = 1; i < total; i++)
    nextPermutation(temp);
}

// Driver Code
public static void Main(String[] args)
{
    String s = "AAB";
    printAllPermutations(s);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to print all permutations of a string
// in sorted order.

 // Calculating factorial of a number   
function factorial(n)
{
    let f = 1;
    for (let i = 1; i <= n; i++)
      f = f * i;
    return f;
}

// Method to print the array
function print(temp)
{
    for (let i = 0; i < temp.length; i++)
      document.write(temp[i]);
    document.write("<br>");
}

// Method to find total number of permutations
function calculateTotal(temp,n)
{
    let f = factorial(n);

    // Building HashMap to store frequencies of
    // all characters.
    let hm = new Map();
    for (let i = 0; i < temp.length; i++) {
      if (hm.has(temp[i]))
        hm.set(temp[i], hm.get(temp[i]) + 1);
      else
        hm.set(temp[i], 1);
    }

    // Traversing hashmap and finding duplicate elements.
    for (let [key, value] of hm.entries()) {
      let x = value;
      if (x > 1) {
        let temp5 = factorial(x);
        f = Math.floor(f / temp5);
      }
    }
    return f;
}

function nextPermutation(temp)
{
    // Start traversing from the end and
    // find position 'i-1' of the first character
    // which is greater than its  successor.
    let i;
    for (i = temp.length - 1; i > 0; i--)
      if (temp[i] > temp[i - 1])
        break;

    // Finding smallest character after 'i-1' and
    // greater than temp[i-1]
       let min = i;
    let j, x = temp[i - 1];
    for (j = i + 1; j < temp.length; j++)
      if ((temp[j] < temp[min]) && (temp[j] > x))
        min = j;

    // Swapping the above found characters.
    let temp_to_swap;
    temp_to_swap = temp[i - 1];
    temp[i - 1] = temp[min];
    temp[min] = temp_to_swap;

    // Sort all digits from position next to 'i-1'
    // to end of the string.
    temp=temp.slice(0,i).sort().concat(temp.slice(i,temp.length));

    // Print the String
    print(temp);
}

function printAllPermutations(s)
{
    // Sorting String
    let temp = s.split("");
    temp.sort();

    // Print first permutation
    print(temp);

    // Finding the total permutations
    let total = calculateTotal(temp, temp.length);
    for (let i = 1; i < total; i++)
      nextPermutation(temp);
}

// Driver Code
let s = "AAB";
printAllPermutations(s);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
AAB
ABA
BAA
```

**时间复杂度:** O(n*m)，其中 n 是数组的大小，m 是可能的排列数量。
**辅助空间:** O(n)。