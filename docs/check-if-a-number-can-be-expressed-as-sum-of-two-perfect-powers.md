# 检查一个数是否可以表示为两个完美幂的和

> 原文:[https://www . geeksforgeeks . org/check-如果一个数字可以表示为两个完美幂的和/](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-sum-of-two-perfect-powers/)

给定一个正数 **N** ，任务是检查给定的数 **N** 是否可以用**a<sup>x</sup>+b<sup>y</sup>**<sup>的形式表示，其中 x 和 y > 1 和 a 和 b > 0。如果 N 可以用给定的形式表示，则打印**真**否则打印**假**。</sup>

**示例:**

> **输入:** N = 5
> **输出:**真
> **说明:**
> 5 可以表示为 2 <sup>2</sup> +1 <sup>2</sup>
> 
> **输入:**N = 15
> T3】输出:假

**方法:**思路是用[完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)的概念来判断和是否存在。以下是步骤:

1.  创建一个数组(比如 **perfectPower[]** )来存储[的数字，这些数字是不是完美的幂](https://www.geeksforgeeks.org/count-perfect-power-of-k-in-a-range-l-r/)。
2.  现在数组 **perfectPower[]** 存储了所有的元素，这些元素都是完美幂，因此我们生成了这个数组中所有元素的所有可能的对和。
3.  将上一步计算的和的标记保存在数组 **isSum[]** 中，因为它可以用**a<sup>x</sup>+b<sup>y</sup>**<sup>的形式表示。</sup>
4.  经过以上步骤如果**isSum【N】**为真则打印**为真**否则打印**为假**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n
// can be written as a^m+b^n
bool isSumOfPower(int n)
{
    // Taking isSum boolean array
    // for check the sum exist or not
    bool isSum[n + 1];

    // To store perfect squares
    vector<int> perfectPowers;

    perfectPowers.push_back(1);

    for (int i = 0; i < (n + 1); i++) {

        // Initially all sums as false
        isSum[i] = false;
    }

    for (long long int i = 2;
         i < (n + 1); i++) {

        if (isSum[i] == true) {

            // If sum exist then push
            // that sum into perfect
            // square vector
            perfectPowers.push_back(i);
            continue;
        }

        for (long long int j = i * i;
             j > 0 && j < (n + 1);
             j *= i) {
            isSum[j] = true;
        }
    }

    // Mark all perfect powers as false
    for (int i = 0;
         i < perfectPowers.size(); i++) {
        isSum[perfectPowers[i]] = false;
    }

    // Traverse each perfectPowers
    for (int i = 0;
         i < perfectPowers.size(); i++) {

        for (int j = i;
             j < perfectPowers.size(); j++) {

            // Calculating Sum with
            // perfect powers array
            int sum = perfectPowers[i]
                      + perfectPowers[j];

            if (sum < (n + 1))
                isSum[sum] = true;
        }
    }
    return isSum[n];
}

// Driver Code
int main()
{
    // Given Number n
    int n = 9;

    // Function Call
    if (isSumOfPower(n)) {
        cout << "true\n";
    }
    else {
        cout << "false\n";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that returns true if n
// can be written as a^m+b^n
static boolean isSumOfPower(int n)
{

    // Taking isSum boolean array
    // for check the sum exist or not
    boolean []isSum = new boolean[n + 1];

    // To store perfect squares
    Vector<Integer> perfectPowers = new Vector<Integer>();

    perfectPowers.add(1);

    for(int i = 0; i < (n + 1); i++)
    {

        // Initially all sums as false
        isSum[i] = false;
    }

    for(int i = 2; i < (n + 1); i++)
    {
        if (isSum[i] == true)
        {

            // If sum exist then push
            // that sum into perfect
            // square vector
            perfectPowers.add(i);
            continue;
        }

        for(int j = i * i;
                j > 0 && j < (n + 1);
                j *= i)
        {
            isSum[j] = true;
        }
    }

    // Mark all perfect powers as false
    for(int i = 0;
            i < perfectPowers.size();
            i++)
    {
        isSum[perfectPowers.get(i)] = false;
    }

    // Traverse each perfectPowers
    for(int i = 0;
            i < perfectPowers.size();
            i++)
    {
        for(int j = i;
                j < perfectPowers.size();
                j++)
        {

            // Calculating Sum with
            // perfect powers array
            int sum = perfectPowers.get(i) +
                      perfectPowers.get(j);

            if (sum < (n + 1))
                isSum[sum] = true;
        }
    }
    return isSum[n];
}

// Driver Code
public static void main(String[] args)
{

    // Given number n
    int n = 9;

    // Function call
    if (isSumOfPower(n))
    {
        System.out.print("true\n");
    }
    else
    {
        System.out.print("false\n");
    }
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that returns true if n
# can be written as a^m+b^n
def isSumOfPower(n):

    # Taking isSum boolean array
    # for check the sum exist or not
    isSum = [0] * (n + 1)

    # To store perfect squares
    perfectPowers = []

    perfectPowers.append(1)

    for i in range(n + 1):

        # Initially all sums as false
        isSum[i] = False

    for i in range(2, n + 1):
        if (isSum[i] == True):

            # If sum exist then push
            # that sum into perfect
            # square vector
            perfectPowers.append(i)
            continue

        j = i * i
        while(j > 0 and j < (n + 1)):
            isSum[j] = True
            j *= i

    # Mark all perfect powers as false
    for i in range(len(perfectPowers)):
        isSum[perfectPowers[i]] = False

    # Traverse each perfectPowers
    for i in range(len(perfectPowers)):
        for j in range(len(perfectPowers)):

            # Calculating Sum with
            # perfect powers array
            sum = (perfectPowers[i] +
                   perfectPowers[j])

            if (sum < (n + 1)):
                isSum[sum] = True

    return isSum[n]

# Driver Code

# Given Number n
n = 9

# Function call
if (isSumOfPower(n)):
    print("true")
else:
    print("false")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that returns true if n
// can be written as a^m+b^n
static bool isSumOfPower(int n)
{

    // Taking isSum bool array
    // for check the sum exist or not
    bool []isSum = new bool[n + 1];

    // To store perfect squares
    List<int> perfectPowers = new List<int>();

    perfectPowers.Add(1);

    for(int i = 0; i < (n + 1); i++)
    {

        // Initially all sums as false
        isSum[i] = false;
    }

    for(int i = 2; i < (n + 1); i++)
    {
        if (isSum[i] == true)
        {

            // If sum exist then push
            // that sum into perfect
            // square vector
            perfectPowers.Add(i);
            continue;
        }

        for(int j = i * i;
                j > 0 && j < (n + 1);
                j *= i)
        {
            isSum[j] = true;
        }
    }

    // Mark all perfect powers as false
    for(int i = 0;
            i < perfectPowers.Count;
            i++)
    {
        isSum[perfectPowers[i]] = false;
    }

    // Traverse each perfectPowers
    for(int i = 0;
            i < perfectPowers.Count;
            i++)
    {
        for(int j = i;
                j < perfectPowers.Count;
                j++)
        {

            // Calculating Sum with
            // perfect powers array
            int sum = perfectPowers[i] +
                      perfectPowers[j];

            if (sum < (n + 1))
                isSum[sum] = true;
        }
    }
    return isSum[n];
}

// Driver Code
public static void Main(String[] args)
{

    // Given number n
    int n = 9;

    // Function call
    if (isSumOfPower(n))
    {
        Console.Write("true\n");
    }
    else
    {
        Console.Write("false\n");
    }
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript  program to implement
// the above approach

// Function that returns true if n
// can be written as a^m+b^n
function isSumOfPower(n)
{

    // Taking isSum boolean array
    // for check the sum exist or not
    let isSum = Array(n+1).fill(0);

    // To store perfect squares
    let perfectPowers = [];

    perfectPowers.push(1);

    for(let i = 0; i < (n + 1); i++)
    {

        // Initially all sums as false
        isSum[i] = false;
    }

    for(let i = 2; i < (n + 1); i++)
    {
        if (isSum[i] == true)
        {

            // If sum exist then push
            // that sum into perfect
            // square vector
            perfectPowers.push(i);
            continue;
        }

        for(let j = i * i;
                j > 0 && j < (n + 1);
                j *= i)
        {
            isSum[j] = true;
        }
    }

    // Mark all perfect powers as false
    for(let i = 0;
            i < perfectPowers.length;
            i++)
    {
        isSum[perfectPowers[i]] = false;
    }

    // Traverse each perfectPowers
    for(let i = 0;
            i < perfectPowers.length;
            i++)
    {
        for(let j = i;
                j < perfectPowers.length;
                j++)
        {

            // Calculating Sum with
            // perfect powers array
            let sum = perfectPowers[i] +
                      perfectPowers[j];

            if (sum < (n + 1))
                isSum[sum] = true;
        }
    }
    return isSum[n];
}

// Driver Code

    // Given number n
    let n = 9;

    // Function call
    if (isSumOfPower(n))
    {
        document.write("true\n");
    }
    else
    {
        document.write("false\n");
    }

</script>
```

**Output:** 

```
true
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)