# 除位于 a 和 b 之间的元素之外的数组元素的总和

> 原文:[https://www . geesforgeks . org/数组元素之和-不包括位于 a 和 b 之间的元素/](https://www.geeksforgeeks.org/sum-of-array-elements-excluding-the-elements-which-lie-between-a-and-b/)

给定一个由 N 个唯一数字组成的数组。也给了两个数字 **a** 和 **b** ，这样 *a* 在阵中永远在 *b* 之前。任务是找出数组元素的总和，不包括位于 a 和 b 之间的元素。

**示例:**

> **输入** : arr = [2，1，6，9，11]，a = 6，b = 9
> 输出 : 14
> 
> **输入** : arr = [1，2，4，5，6]，a = 2，b = 5
> 输出 : 7

**逼近:**在数组中遍历，一直加数组元素直到我们找到 a，继续迭代直到找到 b，不要加数组元素到和。找到 b 后，将数组元素加到和中，直到最后。迭代完成后，返回总和。

下面是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find sum
// of array exlcuding the
// range which has [a, b]
void sumexcludingrange(vector<int>li, int a, int b)
{
    int sum = 0;
    bool add = true;

    // loop in li
    int n = li.size();
    for (int i = 0;i < n; i++)
    {

        // if no != a then add
        if (li[i] != a &&
            add == true)
            sum = sum + li[i];

        // mark when a
        // and b are found
        else if (li[i] == a)
            add = false;
        else if( li[i] == b)
            add = true;
    }

    // print sum
cout<<(sum);
}

// Driver Code
int main()
{
    vector<int>lis{1, 2, 4, 5, 6};
    int a = 2;
    int b = 5;

    sumexcludingrange(lis, a, b);
}
// This code is contributed by
// Sahil_Shelangia
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

// Function to find sum
// of array exlcuding the
// range which has [a, b]
import java .io.*;

class GFG
{
static void sumexcludingrange(int li[],
                              int a, int b)
{
    int sum = 0;
    boolean add = true;

    // loop in li
    for (int i = 0;
             i < li.length; i++)
    {

        // if no != a then add
        if (li[i] != a &&
             add == true)
            sum = sum + li[i];

        // mark when a
        // and b are found
        else if (li[i] == a)
            add = false;
        else if( li[i] == b)
            add = true;
    }

    // print sum
    System.out.print(sum);
}

// Driver Code
public static void main(String[] args)
{
    int lis[] = {1, 2, 4, 5, 6};
    int a = 2;
    int b = 5;

    sumexcludingrange(lis, a, b);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find sum
# of array exlcuding the
# range which has [a, b]
def sumexcludingrange(li, a, b):

    sum = 0
    add = True

    # loop in li
    for no in li:

         # if no != a then add
        if no != a and add == True:
            sum = sum + no

        # mark when a and b are found
        elif no == a:
            add = False
        elif no == b:
            add = True

    # print sum
    print (sum)

lis = [1, 2, 4, 5, 6]
a = 2
b = 5

sumexcludingrange(lis, a, b)
```

## C#

```
// C# implementation of above approach

// Function to find sum
// of array exlcuding the
// range which has [a, b]

using System;

class GFG
{
static void sumexcludingrange(int[] li,
                              int a, int b)
{
    int sum = 0;
    bool add = true;

    // loop in li
    for (int i = 0;
             i < li.Length; i++)
    {

        // if no != a then add
        if (li[i] != a &&
             add == true)
            sum = sum + li[i];

        // mark when a
        // and b are found
        else if (li[i] == a)
            add = false;
        else if( li[i] == b)
            add = true;
    }

    // print sum
    Console.Write(sum);
}

// Driver Code
public static void Main()
{
    int[] lis = {1, 2, 4, 5, 6};
    int a = 2;
    int b = 5;

    sumexcludingrange(lis, a, b);
}
}
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to find sum
// of array exlcuding the
// range which has [a, b]
function sumexcludingrange(li, a, b)
{
    let sum = 0;
    let add = true;

    // Loop in li
    for(let i = 0; i < li.length; i++)
    {

        // If no != a then add
        if (li[i] != a &&
              add == true)
            sum = sum + li[i];

        // Mark when a
        // and b are found
        else if (li[i] == a)
            add = false;
        else if (li[i] == b)
            add = true;
    }

    // Print sum
    document.write(sum);
}

// Driver Code
let lis = [ 1, 2, 4, 5, 6 ];
let a = 2;
let b = 5;

sumexcludingrange(lis, a, b);

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
7
```