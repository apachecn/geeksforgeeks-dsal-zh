# 通过增加子集和排序的第 Kth 个子集的最大值和最小值之和

> 原文:[https://www . geeksforgeeks . org/最大和最小子集之和-按子集之和递增排序/](https://www.geeksforgeeks.org/sum-of-maximum-and-minimum-of-kth-subset-ordered-by-increasing-subset-sum/)

给定一个整数 **N** 和一组 **N** 的所有非负幂作为 **S = {N <sup>0</sup> ，N <sup>1</sup> ，N <sup>2</sup> ，N <sup>3</sup> ，… }** ，按照子集和的递增顺序排列 **S** 的所有非空子集。任务是从该排序中找到 **K <sup>第</sup>** 子集的最大和最小元素的和。

**示例:**

> **输入:** N = 4，K = 3
> **输出:** 5
> **解释:**
> S = {1，4，16，64，…}。
> 因此，非空子集按其和的递增顺序排列= {{1}、{4}、{1，4}、{16}、{1，16}、{4，16}、{1，4，16 }……}。
> 所以 K <sup>第</sup> (3 <sup>第</sup>)子集的元素是{1，4}。所以这个子集的最大和最小元素之和= (4 + 1) = 5。
> 
> **输入:** N = 3，K = 4
> **输出:** 18
> **解释:**
> S = {1，3，9，27，81，…}。
> 因此，非空子集按其和的递增顺序排列= {{1}、{3}、{1，3}、{9}、{1，9}、{3，9}、{1，3，9} ……..}.
> 所以子集 4 <sup>第</sup>位置的元素是{9}。所以这个子集的最大和最小元素之和= (9 + 9) = 18。

**方法:**该方法基于[动力装置](https://www.geeksforgeeks.org/power-set/)的概念。按照以下步骤解决问题:

1.  逆序生成整数 **K** 的对应二进制表达式(即子集的位置)，以保持子集内元素的和不断增加。
2.  然后根据连续位置的**lst【】**列表中出现的位，计算在相应位置的子集中是否会有元素。
3.  迭代 **lst[]** ，如果 **lst[i]** 为 **0** ，则忽略该位，否则( **N <sup>i</sup> )*lst[i]** 将为**K**T14 子集 **num[]** )。
4.  然后取位置 0 和最后一个位置的**num【】**的元素计算和。
5.  在上述步骤后打印结果总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of greatest
// and smallest element of Kth Subset
void sumofExtremes(int N, int K)
{

    // Stores the binary equivalent
    // of k in inverted order
    list<int> lst;

    while (K > 0)
    {
        lst.push_back(K % 2);
        K = K / 2;
    }

    // Stores the kth subset
    list<int> num;

    int x = 0;

    // Iterate over the list
    for(auto element : lst)
    {

        // If the element is non-zero
        if (element != 0)
        {
            int a = pow(N, x);
            a = a * (element);
            num.push_back(a);
        }
        x++;
    }

    // Update S to length of num
    int s = num.size();

    // If length of the subset is 1
    if (s == 1)

        // Print twice of that element
        cout << (2 * num.front()) << "\n";

    // Print the sum of first and
    // last element
    else
        cout << num.front() + num.back();
}

// Driver Code
int main()
{

    // Given number N
    int N = 4;

    // Given position K
    int K = 6;

    sumofExtremes(N, K);
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the sum of greatest
// and smallest element of Kth Subset
public static void sumofExtremes(int N, int K)
{

    // Stores the binary equivalent
    // of k in inverted order
    List<Integer> lst = new ArrayList<Integer>();

    while (K > 0)
    {
        lst.add(K % 2);
        K = K / 2;
    }

    // Stores the kth subset
    List<Integer> num = new ArrayList<Integer>();

    int x = 0;

    // Iterate over the list
    for(int element : lst)
    {

        // If the element is non-zero
        if (element != 0)
        {
            int a = (int)Math.pow(N, x);
            a = a * (element);
            num.add(a);
        }
        x++;
    }

    // Update S to length of num
    int s = num.size();

    // If length of the subset is 1
    if (s == 1)

        // Print twice of that element
        System.out.println(2 * num.get(0));

    // Print the sum of first and
    // last element
    else
        System.out.println(num.get(0) +
                           num.get(s - 1));
}

// Driver Code
public static void main(String[] args)
{

    // Given number N
    int N = 4;

    // Given position K
    int K = 6;

    // Function call
    sumofExtremes(N, K);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of greatest
# and smallest element of Kth Subset
def sumofExtremes(N, K):

    # Stores the binary equivalent
    # of k in inverted order
    lst = []

    while K > 0:
        lst.append(K % 2)
        K = K//2

    # Stores the kth subset
    num = []

    # Iterate over the list
    for i in range(0, len(lst)):

        # If the element is non-zero
        if(lst[i] != 0):
            a = N**i
            a = a * lst[i]
            num.append(a)

    # Update S to length of num
    s = len(num)

    # If length of the subset is 1
    if(s == 1):

        # Print twice of that element
        print(2 * num[0])

    # Print the sum of first and
    # last element
    else:
        print(num[0] + num[s - 1])

# Driver Code

# Given number N
N = 4

# Given position K
K = 6

# Function Call
sumofExtremes(N, K)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the sum of greatest
// and smallest element of Kth Subset
public static void sumofExtremes(int N, int K)
{

    // Stores the binary equivalent
    // of k in inverted order
    List<int> lst = new List<int>();

    while (K > 0)
    {
        lst.Add(K % 2);
        K = K / 2;
    }

    // Stores the kth subset
    List<int> num = new List<int>();

    // Iterate over the list
    for(int i = 0; i < lst.Count; i++)
    {

        // If the element is non-zero
        if (lst[i] != 0)
        {
            int a = (int)Math.Pow(N, i);
            a = a * (lst[i]);
            num.Add(a);
        }
    }

    // Update S to length of num
    int s = num.Count;

    // If length of the subset is 1
    if (s == 1)

        // Print twice of that element
        Console.WriteLine(2 * num[0]);

    // Print the sum of first and
    // last element
    else
        Console.WriteLine(num[0] + num[s - 1]);
}

// Driver Code
static public void Main()
{

    // Given number N
    int N = 4;

    // Given position K
    int K = 6;

    // Function call
    sumofExtremes(N, K);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the sum of greatest
// and smallest element of Kth Subset
function sumofExtremes(N, K)
{

    // Stores the binary equivalent
    // of k in inverted order
    let lst = [];

    while (K > 0)
    {
        lst.push(K % 2);
        K = Math.floor(K / 2);
    }

    // Stores the kth subset
    let num = [];

    let x = 0;

    // Iterate over the list
    for(let element of lst)
    {

        // If the element is non-zero
        if (element != 0)
        {
            let a = Math.pow(N, x);
            a = a * (element);
            num.push(a);
        }
        x++;
    }

    // Update S to length of num
    let s = num.length;

    // If length of the subset is 1
    if (s == 1)

        // Print twice of that element
        document.write((2 * num[0]) + "+");

    // Print the sum of first and
    // last element
    else
        document.write(num[0] + num[num.length - 1]);
}

// Driver Code

    // Given number N
    let N = 4;

    // Given position K
    let K = 6;

    sumofExtremes(N, K);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
20
```

***时间复杂度:** O(log K)*
***辅助空间:** O(N)*