# HH：MM：SS 格式的最长时间，可以用给定的六位数字表示

> 原文：[https://www.geeksforgeeks.org/maximum-time-in-hhmmss-format-that-can-be-represented-by-given-six-digits/](https://www.geeksforgeeks.org/maximum-time-in-hhmmss-format-that-can-be-represented-by-given-six-digits/)

给定仅由六个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，任务是以 **24 小时格式**返回最大时间，可以使用 给定数组中的数字。

**注意**：24 小时格式的最短时间为 00:00:00，最大时间为 23:59:59。 如果无法形成有效时间，请打印-1。

**示例**：

> **输入**：arr [] = {0，2，1，9，9，3，2}
> **输出**：23:29:10
> **说明：[**
> 使用数组数字可以形成的最大 24 小时格式化时间是 23:29:10
> 
> **输入**：arr [] = {6，2，6，7，5，6}
> **输出**：-1

**方法**：请按照以下步骤解决问题：

*   创建[哈希图](https://www.geeksforgeeks.org/hashing-data-structure/)并将数字的频率存储在给定数组中。

*   从最大时间 23:59:59 迭代到最小时间 00:00:00

*   对于每次，请检查是否所有数字都在哈希图中。

*   发现上述条件成立的第一次打印。 如果找不到满足条件的时间，则打印“ -1”。

下面是上述方法的实现：

## C++

```cpp

// C++ Program of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// possible time in 24-Hours format
// that can be represented by array elements
string largestTimeFromDigits(vector<int>& A)
{

    // Stores the frequency
    // of the array elmenets
    map<int, int> mp1, mp2;
    for (auto x : A) {
        mp1[x]++;
    }
    mp2 = mp1;

    // Maximum possible time
    int hr = 23, m = 59, s = 59;

    // Iterate to minimum possible time
    while (hr >= 0) {
        int h0 = hr / 10, h1 = hr % 10;
        int m0 = m / 10, m1 = m % 10;
        int s0 = s / 10, s1 = s % 10;
        int p = 0;
        vector<int> arr{ h0, h1, m0,
                         m1, s0, s1 };

        // Conditions to reduce the
        // the time iteratively
        for (auto& it : arr) {
            if (mp1[it] > 0) {
                mp1[it]--;
            }
            else {
                p = 1;
            }
        }

        // If all required digits
        // are present in the Map
        if (p == 0) {
            string s = "";
            s = to_string(h0)
                + to_string(h1);
            s += ':' + to_string(m0)
                 + to_string(m1);
            s += ':' + to_string(s0)
                 + to_string(s1);

            return s;
        }

        // Retrieve Original Count
        mp1 = mp2;

        // If seconds is reduced to 0
        if (s == 0) {
            s = 59;
            m--;
        }

        // If minutes is reduced to 0
        else if (m < 0) {
            m = 59;
            hr--;
        }
        if (s > 0) {
            s--;
        }
    }
    return "-1";
}

// Driver Code
int main()
{
    vector<int> v = { 0, 2, 1, 9, 3, 2 };
    cout << largestTimeFromDigits(v);
}

```

## Java

```java

// Java Program of the
// above approach
import java.util.*;
class GFG{

// Function to return the maximum
// possible time in 24-Hours format
// that can be represented by array elements
static String largestTimeFromDigits(int []A)
{
  // Stores the frequency
  // of the array elmenets
  HashMap<Integer,
          Integer> mp1 = new HashMap<Integer,
                                     Integer>();
  HashMap<Integer,
          Integer> mp2 = new HashMap<Integer,
                                     Integer>();
  for (int x : A) 
  {
    if(mp1.containsKey(x))
      mp1.put(x, mp1.get(x) + 1);
    else
      mp1.put(x, 1);
  }
  mp2 = (HashMap<Integer, 
                 Integer>) mp1.clone();

  // Maximum possible time
  int hr = 23, m = 59, s = 59;

  // Iterate to minimum 
  // possible time
  while (hr >= 0) 
  {
    int h0 = hr / 10, h1 = hr % 10;
    int m0 = m / 10, m1 = m % 10;
    int s0 = s / 10, s1 = s % 10;
    int p = 0;
    int []arr = {h0, h1, m0,
                 m1, s0, s1};

    // Conditions to reduce the
    // the time iteratively
    for (int it : arr) 
    {
      if (mp1.containsKey(it) && 
          mp1.get(it) > 0) 
      { 
        mp1.put(it, mp1.get(it) - 1);
      }
      else
      {
        p = 1;
      }
    }

    // If all required digits
    // are present in the Map
    if (p == 0) 
    {
      String st = "";
      st = String.valueOf(h0) + 
           String.valueOf(h1);
      st += ':' + String.valueOf(m0) + 
                  String.valueOf(m1);
      st += ':' + String.valueOf(s0) + 
                  String.valueOf(s1);
      return st;
    }

    // Retrieve Original Count
    mp1 = (HashMap<Integer, 
                   Integer>) mp2.clone();

    // If seconds is reduced to 0
    if (s == 0) 
    {
      s = 59;
      m--;
    }

    // If minutes is reduced to 0
    else if (m < 0) 
    {
      m = 59;
      hr--;
    }
    if (s > 0) 
    {
      s--;
    }
  }
  return "-1";
}

// Driver Code
public static void main(String[] args)
{
  int []v = {0, 2, 1, 9, 3, 2};
  System.out.print(largestTimeFromDigits(v));
}
}

// This code contributed by Princi Singh

```

## Python3

```py

# Python 3 Program of the
# above approach

# Function to return the 
# maximum possible time in 
# 24-Hours format that can 
# be represented by array elements
def largestTimeFromDigits(A):

    # Stores the frequency
    # of the array elmenets
    mp1 = {}
    mp2 = {}

    for x in A:
        mp1[x] = mp1.get(x, 0) + 1
    mp2 = mp1.copy()

    # Maximum possible time
    hr = 23
    m = 59
    s = 59

    # Iterate to minimum 
    # possible time
    while(hr >= 0):
        h0 = hr//10
        h1 = hr % 10
        m0 = m//10
        m1 = m%10
        s0 = s//10
        s1 = s%10
        p = 0
        arr = [h0, h1, m0, 
               m1, s0, s1]

        # Conditions to reduce the
        # the time iteratively
        for it in arr:
            if (it in mp1 and
                mp1.get(it) > 0):
                mp1[it] = mp1.get(it) - 1
            else:
                p = 1

        # If all required digits
        # are present in the Map
        if (p == 0):
            s = ""
            s = (str(h0) +
                 str(h1))
            s += (':' + str(m0) +
                        str(m1))
            s += (':' + str(s0) +
                        str(s1))

            return s

        # Retrieve Original Count
        mp1 = mp2.copy()

        # If seconds is
        # reduced to 0
        if (s == 0):
            s = 59
            m -= 1

        # If minutes is 
        # reduced to 0
        elif (m < 0):
            m = 59
            hr -= 1
        if (s > 0):
            s -= 1
    return "-1"

# Driver Code
if __name__ == '__main__':

    v =  [0, 2, 1, 9, 3, 2]
    print(largestTimeFromDigits(v))

# This code is contributed by ipg2016107

```

## C#

```cs

// C# Program of the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the maximum
// possible time in 24-Hours format
// that can be represented by array elements
static String largestTimeFromDigits(int []A)
{
  // Stores the frequency
  // of the array elmenets
  Dictionary<int,
             int> mp1 = new Dictionary<int, 
                                       int>();
  Dictionary<int, 
             int> mp2 = new Dictionary<int,
                                       int>();
  foreach (int x in A) 
  {
    if(mp1.ContainsKey(x))
      mp1[x] = mp1[x] + 1;
    else
      mp1.Add(x, 1);
  }
  mp2 =  new Dictionary<int, 
                        int>(mp1);

  // Maximum possible time
  int hr = 23, m = 59, s = 59;

  // Iterate to minimum 
  // possible time
  while (hr >= 0) 
  {
    int h0 = hr / 10, h1 = hr % 10;
    int m0 = m / 10, m1 = m % 10;
    int s0 = s / 10, s1 = s % 10;
    int p = 0;
    int []arr = {h0, h1, m0,
                 m1, s0, s1};

    // Conditions to reduce the
    // the time iteratively
    foreach (int it in arr) 
    {
      if (mp1.ContainsKey(it) && 
          mp1[it] > 0) 
      { 
        mp1[it]= mp1[it] - 1;
      }
      else
      {
        p = 1;
      }
    }

    // If all required digits
    // are present in the Map
    if (p == 0) 
    {
      String st = "";
      st = String.Join("", h0) + 
           String.Join("", h1);
      st += ':' + String.Join("", m0) + 
                  String.Join("", m1);
      st += ':' + String.Join("", s0) + 
                  String.Join("", s1);
      return st;
    }

    // Retrieve Original Count
    mp1 = new Dictionary<int, int>(mp2);

    // If seconds is reduced to 0
    if (s == 0) 
    {
      s = 59;
      m--;
    }

    // If minutes is reduced to 0
    else if (m < 0) 
    {
      m = 59;
      hr--;
    }
    if (s > 0) 
    {
      s--;
    }
  }
  return "-1";
}

// Driver Code
public static void Main(String[] args)
{
  int []v = {0, 2, 1, 9, 3, 2};
  Console.Write(largestTimeFromDigits(v));
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
23:29:10

```

***时间复杂度**：O（60 * 60 * 60）*

***辅助空间**：O（1）*



* * *

* * *



