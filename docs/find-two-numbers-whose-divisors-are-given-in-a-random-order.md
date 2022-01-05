# 找出两个除数随机给出的数

> 原文:[https://www . geesforgeks . org/find-two-numbers-其除数以随机顺序给出/](https://www.geeksforgeeks.org/find-two-numbers-whose-divisors-are-given-in-a-random-order/)

给定一个由 N 个数字组成的数组，该数组具有任意顺序的两个数字的所有除数。任务是找出数组中给定除数的两个数。
**例:**

> **输入:** a[] = {10，2，8，1，2，4，1，20，4，5}
> **输出:** 20 8
> 数组中给出了 20 和 8 的除数。
> **输入:** a[] = {2，2，1，1}
> **输出:** 1 2

**方法:**按照以下步骤解决上述问题:

*   找到数组中的最大元素，这是两个数字之一。
*   保留一个计算数组元素出现次数的频率数组。
*   减少频率数组中最大元素的所有除数。
*   下一个 max 元素将是第二个数字。

以下是上述方法的实现:

## C++

```
// C++ program to find the two numbers
// when divisors are given in a random order
#include <bits/stdc++.h>
using namespace std;

// Function to get the two numbers
void getNumbers(int a[], int n)
{

    // Mark the frequency of all elements
    unordered_map<int, int> freq;
    for (int i = 0; i < n; i++)
        freq[a[i]]++;

    // Get the first maximum element
    int maxi1 = *max_element(a, a+n);

    // Decrease the frequency of all divisors
    // of the maximum number that are present
    // int a[]
    for (int i = 1; i * i <= maxi1; i++) {

        if (maxi1 % i == 0 &&
            freq.find(i) != freq.end() &&
            freq[i] != 0) {
            freq[i]--;

            if (i != (maxi1 / i) &&
               freq.find(maxi1 / i) != freq.end() &&
               freq[maxi1 / i] != 0)
                freq[maxi1 / i]--;
        }
    }

    // The second number is the largest number
    // present in remaining numbers.
    int maxi2 = -1;
    for (int i = 0; i < n; i++) {
        if (freq[a[i]] != 0)
            maxi2 = max(maxi2, a[i]);
    }

    cout << maxi1 << " " << maxi2;
}

// Driver Code
int main()
{
    int a[] = { 10, 2, 8, 1, 2, 4, 1, 20, 4, 5 };
    int n = sizeof(a) / sizeof(a[0]);
    getNumbers(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the two numbers
// when divisors are given in a random order

import java.util.*;

class GFG{

// Function to get the two numbers
static void getNumbers(int a[], int n)
{

    // Mark the frequency of all elements
    HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();
    for (int i = 0; i < n; i++)
        if(freq.containsKey(a[i])){
            freq.put(a[i], freq.get(a[i])+1);
        }
        else{
            freq.put(a[i], 1);
        }

    // Get the first maximum element
    int maxi1 = Arrays.stream(a).max().getAsInt();

    // Decrease the frequency of all divisors
    // of the maximum number that are present
    // int a[]
    for (int i = 1; i * i <= maxi1; i++) {

        if (maxi1 % i == 0 &&
            freq.containsKey(i)&&
            freq.get(i)!= 0) {
            freq.put(i, freq.get(i)- 1);

            if (i != (maxi1 / i) &&
               freq.containsKey(maxi1 / i) &&
               freq.get(maxi1 / i)!= 0)
                freq.put(maxi1 / i, freq.get(maxi1 / i) - 1);
        }
    }

    // The second number is the largest number
    // present in remaining numbers.
    int maxi2 = -1;
    for (int i = 0; i < n; i++) {
        if (freq.get(a[i]) != 0)
            maxi2 = Math.max(maxi2, a[i]);
    }

    System.out.print(maxi1+ " " +  maxi2);
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 10, 2, 8, 1, 2, 4, 1, 20, 4, 5 };
    int n = a.length;
    getNumbers(a, n);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the two numbers
# when divisors are given in a random order

# from math lib import sqrt method
from math import sqrt

# Function to get the two numbers
def getNumbers(a, n) :

    # Mark the frequency of all elements
    freq = {};
    for i in range(n) :
        if a[i] not in freq.keys() :
            freq[a[i]] = 0

        freq[a[i]] += 1

    # Get the first maximum element
    maxi1 = max(a)

    # Decrease the frequency of all divisors
    # of the maximum number that are present
    # int a[]
    for i in range(1, int(sqrt(maxi1)) + 1) :

        if (maxi1 % i == 0 and
            freq[i] in freq.keys() and
            freq[i] != 0) :
            freq[i] -= 1

            if (i != (maxi1 // i) and
                freq[maxi1 // i] in freq.keys() and
                freq[maxi1 // i] != 0) :
                freq[maxi1 // i] -= 1

    # The second number is the largest number
    # present in remaining numbers.
    maxi2 = -1
    for i in range(n) :
        if (freq[a[i]] != 0) :
            maxi2 = max(maxi2, a[i])

    print(maxi1, maxi2)

# Driver Code
if __name__ == "__main__" :

    a = [ 10, 2, 8, 1, 2, 4, 1, 20, 4, 5 ]
    n = len(a)
    getNumbers(a, n)

# This code is contributed by Ryuga
```

## C#

```

// C# program to find the two numbers
// when divisors are given in a random order

using System;
using System.Collections.Generic;
using System.Linq;
public class GFG{

// Function to get the two numbers
static void getNumbers(int []a, int n)
{

    // Mark the frequency of all elements
    Dictionary<int,int> freq = new Dictionary<int,int>();
    for (int i = 0; i < n; i++)
        if(freq.ContainsKey(a[i])){
            freq[a[i]] = freq[a[i]]+1;
        }
        else{
            freq.Add(a[i], 1);
        }

    // Get the first maximum element
    int maxi1 = a.Max();

    // Decrease the frequency of all divisors
    // of the maximum number that are present
    // int []a
    for (int i = 1; i * i <= maxi1; i++) {

        if (maxi1 % i == 0 &&
            freq.ContainsKey(i)&&
            freq[i]!= 0) {
            freq[i] = freq[i]- 1;

            if (i != (maxi1 / i) &&
               freq.ContainsKey(maxi1 / i) &&
               freq[maxi1 / i]!= 0)
                freq[maxi1 / i] = freq[maxi1 / i] - 1;
        }
    }

    // The second number is the largest number
    // present in remaining numbers.
    int maxi2 = -1;
    for (int i = 0; i < n; i++) {
        if (freq[a[i]] != 0)
            maxi2 = Math.Max(maxi2, a[i]);
    }

    Console.Write(maxi1+ " " +  maxi2);
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 10, 2, 8, 1, 2, 4, 1, 20, 4, 5 };
    int n = a.Length;
    getNumbers(a, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find the two numbers
// when divisors are given in a random order

// Function to get the two numbers
function getNumbers(a, n)
{

    // Mark the frequency of all elements
    var freq = new Map();
    for (var i = 0; i < n; i++)
        if(freq.has(a[i])){
            freq.set(a[i], freq.get(a[i])+1);
        }
        else{
            freq.set(a[i], 1);
        }

    // Get the first maximum element
    var maxi1 = a.reduce((a1, b1)=>Math.max(a1,b1));

    // Decrease the frequency of all divisors
    // of the maximum number that are present
    // int []a
    for (var i = 1; i * i <= maxi1; i++) {

        if (maxi1 % i == 0 &&
            (freq.has(i)&&
            freq.get(i)!= 0)) {
            freq.set(i, freq.get(i)-1);

            if (i != parseInt(maxi1 / i) &&
               freq.has(parseInt(maxi1 / i)) &&
               freq.get(parseInt(maxi1 / i))!= 0)
               freq.set(parseInt(maxi1 / i), freq.get(parseInt(maxi1 / i))-1);
        }
    }

    // The second number is the largest number
    // present in remaining numbers.
    var maxi2 = -1;
    for (var i = 0; i < n; i++) {
        if (freq.get(a[i])!=0)
            maxi2 = Math.max(maxi2, a[i]);
    }

    document.write(maxi1+ " " +  maxi2);
}

// Driver Code
var a = [10, 2, 8, 1, 2, 4, 1, 20, 4, 5];
var n = a.length;
getNumbers(a, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
20 8
```