# 计数岩样| TCS Codevita 2020

> 原文:[https://www . geesforgeks . org/counting-rock-samples-TCS-code vita-2020/](https://www.geeksforgeeks.org/counting-rock-samples-tcs-codevita-2020/)

约翰是一名地质学家，他需要对岩石样本进行计数，以便将其送往化学实验室。他有问题。实验室只接受以 ppm(百万分之几)为单位的各种尺寸的岩石样品。约翰需要你的帮助。你的任务是开发一个程序，以获得实验室接受的每个范围内的岩石数量。

**问题陈述:**给定一个表示岩石样本大小的数组**样本【】**和一个 2D 数组**范围【】**，任务是为每一个可能的 **1 < = i < = N** 计算范围**范围【I】【0】到范围【I】【1】**的岩石样本。

**示例:**

> **输入:**样本[] = {345，604，321，433，704，470，808，718，517，811}，范围[] = {{300，380}，{400，700 } }
> T3】输出: 2 4
> **解释:**
> 范围【300，380】:样本{345，321}位于范围内因此，计数为 2。
> 范围[400，700]:样本{433，604，517，470}位于范围内。因此，计数为 4。
> 
> **输入:**样本[] = {400，567，890，765，987}，范围[] = {{300，380}，{800，1000}
> **输出:** 0 2

**方法:**想法是针对每个**范围【I】**迭代**样本【】**，并计算位于指定范围内的样本数量。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)范围[]。
*   对于每一行**范围【I】**，遍历阵列**样本【】**并计算位于范围**【范围【I】【0】、范围【I】【1】】**内的岩石样本数量。

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach
#include<bits/stdc++.h>
using namespace std;

void findRockSample(vector<vector<int>>ranges,
             int n, int r, vector<int>arr)
{
    vector<int>a;

    // Iterate over the ranges
    for(int i = 0; i < r; i++)
    {
       int  c = 0;
       int l = ranges[i][0];
       int h = ranges[i][1];

       for(int j = 0; j < arr.size(); j++)
       {
           if (l <= arr[j] && arr[j] <= h)
               c += 1;
        }
        a.push_back(c);
    }
    for(auto i:a)
        cout << i << " ";
}

// Driver Code
int main()
{
    int n = 5;
    int r = 2;

    vector<int>arr = { 400, 567, 890, 765, 987 };
    vector<vector<int>>ranges = { { 300, 380 },
                                  { 800, 1000 } };

    // Function call
    findRockSample(ranges, n, r, arr);
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to find the rock
// samples in the ranges
static ArrayList<Integer>findRockSample(int ranges[][],
                                        int n, int r,
                                        int  arr[])
{
    ArrayList<Integer> a = new ArrayList<>();

    // Iterate over the ranges
    for(int i = 0; i < r; i++)
    {
       int  c = 0;
       int l = ranges[i][0];
       int h = ranges[i][1];

       for(int j = 0; j < arr.length; j++)
       {
           if (l <= arr[j] && arr[j] <= h)
               c += 1;
        }
        a.add(c);
    }
    return a;
}

// Driver Code
public static void main(String args[])
{
    int n = 5;
    int r = 2;
    int arr[] = { 400, 567, 890, 765, 987 };
    int ranges[][] = { { 300, 380 }, { 800, 1000 } };

    ArrayList<Integer> answer = new ArrayList<>();

    // Function call
    answer = findRockSample(ranges, n, r, arr);

    for(int i = 0; i < answer.size(); i++)
        System.out.print(answer.get(i) + " ");

    System.out.println();
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

# Function to find the rock
# samples in the ranges
def findRockSample(ranges,
                   n, r, arr):
    a = []

# Iterate over the ranges
    for i in range(r):
        c = 0
        l, h = ranges[i][0], ranges[i][1]
        for val in arr:
            if l <= val <= h:
                c += 1
        a.append(c)
    return a

# Driver Code
if __name__ == "__main__":
    n = 5
    r = 2
    arr = [400, 567, 890, 765, 987]
    ranges = [[300, 380], [800, 1000]]

# Function Call
    print(*findRockSample(ranges, n, r, arr))
```

## C#

```
// C# program of the
// above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find the rock
// samples in the ranges
static void findRockSample(int [,]ranges,
                           int n, int r,
                           int [] arr)
{
    List<int> a = new List<int>();

    // Iterate over the ranges
    for(int i = 0; i < r; i++)
    {
        int  c = 0;
        int l = ranges[i, 0];
        int h = ranges[i, 1];

        for(int j = 0; j < arr.Length; j++)
        {
            if (l <= arr[j] && arr[j] <= h)
                c += 1;
        }
        a.Add(c);
    }
    foreach (var i in a)
    {
        Console.Write(i + " ");
    }
}

// Driver Code
public static void Main()
{
    int n = 5;
    int r = 2;

    int []arr = { 400, 567, 890, 765, 987 };
    int [,]ranges = { { 300, 380 },
                      { 800, 1000 } };

    // Function call
    findRockSample(ranges, n, r, arr);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
    // Javascript program of the above approach

    // Function to find the rock
    // samples in the ranges
    function findRockSample(ranges, n, r, arr)
    {
        let a = [];

        // Iterate over the ranges
        for(let i = 0; i < r; i++)
        {
            let c = 0;
            let l = ranges[i][0];
            let h = ranges[i][1];

            for(let j = 0; j < arr.length; j++)
            {
                if (l <= arr[j] && arr[j] <= h)
                    c += 1;
            }
            a.push(c);
        }
        for(let i = 0; i < a.length; i++)
        {
            document.write(a[i] + " ");
        }
    }

    let n = 5;
    let r = 2;

    let arr = [ 400, 567, 890, 765, 987 ];
    let ranges = [ [ 300, 380 ], [ 800, 1000 ] ];

    // Function call
    findRockSample(ranges, n, r, arr);

</script>
```

**Output:** 

```
0 2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*