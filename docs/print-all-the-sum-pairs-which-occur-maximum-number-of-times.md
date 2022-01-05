# 打印出现次数最多的所有总和对

> 原文:[https://www . geeksforgeeks . org/print-all-sum-pairs-哪些发生-最大次数/](https://www.geeksforgeeks.org/print-all-the-sum-pairs-which-occur-maximum-number-of-times/)

给定不同整数的数组**arr[]****N**。任务是求两个数组整数的和 **a[i] + a[j]** ，出现次数最多。如果有多个答案，请全部打印出来。
**举例:**

> **输入:** arr[] = {1，8，3，11，4，9，2，7}
> **输出:**
> 10
> 12
> 11
> 10，12 和 11 之和出现 3 次
> 7 + 4 = 11，8 + 3 = 11，9 + 2 = 11
> 1 + 9 = 10，8 + 2 = 10，7 + 3 = 10
> 1 + 11 9 + 3 = 12
> **输入:** arr[] = {3，1，7，11，9，2，12}
> **输出:**
> 12
> 14
> 10
> 13

**方法:**可以按照以下步骤解决问题:

*   迭代每对元素。
*   使用散列表计算每个和对出现的次数。
*   最后，遍历散列表，找到出现次数最多的和对。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum pairs
// that occur the most
void findSumPairs(int a[], int n)
{
    // Hash-table
    unordered_map<int, int> mpp;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Keep a count of sum pairs
            mpp[a[i] + a[j]]++;
        }
    }

    // Variables to store
    // maximum occurrence
    int occur = 0;

    // Iterate in the hash table
    for (auto it : mpp) {
        if (it.second > occur) {
            occur = it.second;
        }
    }

    // Print all sum pair which occur
    // maximum number of times
    for (auto it : mpp) {
        if (it.second == occur)
            cout << it.first << endl;
    }
}

// Driver code
int main()
{
    int a[] = { 1, 8, 3, 11, 4, 9, 2, 7 };
    int n = sizeof(a) / sizeof(a[0]);
    findSumPairs(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to find the sum pairs
// that occur the most
static void findSumPairs(int a[], int n)
{
    // Hash-table
    Map<Integer,Integer> mpp = new HashMap<>();
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Keep a count of sum pairs
            mpp.put(a[i] + a[j],mpp.get(a[i] + a[j])==null?1:mpp.get(a[i] + a[j])+1);
        }
    }

    // Variables to store
    // maximum occurrence
    int occur = 0;

    // Iterate in the hash table
    for (Map.Entry<Integer,Integer> entry : mpp.entrySet())
    {
        if (entry.getValue() > occur)
        {
            occur = entry.getValue();
        }
    }

    // Print all sum pair which occur
    // maximum number of times
    for (Map.Entry<Integer,Integer> entry : mpp.entrySet())
    {
        if (entry.getValue() == occur)
            System.out.println(entry.getKey());
    }
}

// Driver code
public static void main(String args[])
{
    int a[] = { 1, 8, 3, 11, 4, 9, 2, 7 };
    int n = a.length;
    findSumPairs(a, n);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to find the sum pairs
# that occur the most
def findSumPairs(a, n):

    # Hash-table
    mpp = {i:0 for i in range(21)}
    for i in range(n - 1):
        for j in range(i + 1, n, 1):

            # Keep a count of sum pairs
            mpp[a[i] + a[j]] += 1

    # Variables to store
    # maximum occurrence
    occur = 0

    # Iterate in the hash table
    for key, value in mpp.items():
        if (value > occur):
            occur = value

    # Print all sum pair which occur
    # maximum number of times
    for key, value in mpp.items():
        if (value == occur):
            print(key)

# Driver code
if __name__ == '__main__':
    a = [1, 8, 3, 11, 4, 9, 2, 7]
    n = len(a)
    findSumPairs(a, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the sum pairs
// that occur the most
static void findSumPairs(int []a, int n)
{
    // Hash-table
    Dictionary<int,int> mpp = new Dictionary<int,int>();
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Keep a count of sum pairs
            if(mpp.ContainsKey(a[i] + a[j]))
            {
                var val = mpp[a[i] + a[j]];
                mpp.Remove(a[i] + a[j]);
                mpp.Add(a[i] + a[j], val + 1);
            }
            else
            {
                mpp.Add(a[i] + a[j], 1);
            }
        }
    }

    // Variables to store
    // maximum occurrence
    int occur = 0;

    // Iterate in the hash table
    foreach(KeyValuePair<int, int> entry in mpp)
    {
        if (entry.Value > occur)
        {
            occur = entry.Value;
        }
    }

    // Print all sum pair which occur
    // maximum number of times
    foreach(KeyValuePair<int, int> entry in mpp)
    {
        if (entry.Value == occur)
            Console.WriteLine(entry.Key);
    }
}

// Driver code
public static void Main(String []args)
{
    int []a = { 1, 8, 3, 11, 4, 9, 2, 7 };
    int n = a.Length;
    findSumPairs(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to find the sum pairs
// that occur the most
function findSumPairs( a, n){
    // Hash-table
    let mpp = new Map();
    for (let i = 0; i < n - 1; i++) {
        for (let j = i + 1; j < n; j++) {
          if(mpp[a[i]+a[j]])
              mpp[a[i]+a[j]]++;
           else
              mpp[a[i]+a[j]] = 1;
        }
    }

    // Variables to store
    // maximum occurrence
    let occur = 0;

    // Iterate in the hash table
    for (var it in mpp) {
        if (mpp[it] > occur) {
            occur = mpp[it];
        }
    }

    // Print all sum pair which occur
    // maximum number of times
    for (var it in mpp) {
        if (mpp[it] == occur)
            document.write( it ,'<br>');
    }
}

// Driver code
let a = [ 1, 8, 3, 11, 4, 9, 2, 7 ];
let len = a.length;
findSumPairs(a, len);
</script>
```

**Output:** 

```
10
12
11
```