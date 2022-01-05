# 无界分数背包

> 原文:[https://www . geesforgeks . org/无界-分数背包/](https://www.geeksforgeeks.org/unbounded-fractional-knapsack/)

给定 **n** 个物品的重量和值，任务是将这些物品放入一个容量为 **W** 的背包中，得到背包中的最大总值，我们可以重复放入同一个物品，也可以放入一个物品的一小部分。

**示例:**

> **输入:** val[] = {14，27，44，19}，wt[] = {6，7，9，8}，W = 50
> **输出:** 244.444
> 
> **输入:** val[] = {100，60，120}，wt[] = {20，10，30}，W = 50
> **输出:** 300

**进场:**这里的思路就是只找到**值**与**权重**比值最大的物品。然后只用这个物品填满整个背包，以最大化背包的最终价值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum required value
float knapSack(int W, float wt[], float val[], int n)
{

    // maxratio will store the maximum value to weight
    // ratio we can have for any item and maxindex
    // will store the index of that element
    float maxratio = INT_MIN;
    int maxindex = 0;

    // Find the maximum ratio
    for (int i = 0; i < n; i++) {
        if ((val[i] / wt[i]) > maxratio) {
            maxratio = (val[i] / wt[i]);
            maxindex = i;
        }
    }

    // The item with the maximum value to
    // weight ratio will be put into
    // the knapsack repeatedly until full
    return (W * maxratio);
}

// Driver code
int main()
{
    float val[] = { 14, 27, 44, 19 };
    float wt[] = { 6, 7, 9, 8 };
    int n = sizeof(val) / sizeof(val[0]);
    int W = 50;

    cout << knapSack(W, wt, val, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximum required value
    static float knapSack(int W, float wt[],
                            float val[], int n)
    {

        // maxratio will store the maximum value to weight
        // ratio we can have for any item and maxindex
        // will store the index of that element
        float maxratio = Integer.MIN_VALUE;
        int maxindex = 0;

        // Find the maximum ratio
        for (int i = 0; i < n; i++)
        {
            if ((val[i] / wt[i]) > maxratio)
            {
                maxratio = (val[i] / wt[i]);
                maxindex = i;
            }
        }

        // The item with the maximum value to
        // weight ratio will be put into
        // the knapsack repeatedly until full
        return (W * maxratio);
    }

    // Driver code
    public static void main(String[] args)
    {
        float val[] = {14, 27, 44, 19};
        float wt[] = {6, 7, 9, 8};
        int n = val.length;
        int W = 50;

        System.out.println(knapSack(W, wt, val, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the approach

import sys

# Function to return the maximum required value
def knapSack(W, wt, val, n):

    # maxratio will store the maximum value to weight
    # ratio we can have for any item and maxindex
    # will store the index of that element
    maxratio = -sys.maxsize-1;
    maxindex = 0;

    # Find the maximum ratio
    for i in range(n):
        if ((val[i] / wt[i]) > maxratio):
            maxratio = (val[i] / wt[i]);
            maxindex = i;

    # The item with the maximum value to
    # weight ratio will be put into
    # the knapsack repeatedly until full
    return (W * maxratio);

# Driver code

val = [ 14, 27, 44, 19 ];
wt = [ 6, 7, 9, 8 ];
n = len(val);
W = 50;

print(knapSack(W, wt, val, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum required value
    static float knapSack(int W, float []wt,
                            float []val, int n)
    {

        // maxratio will store the maximum value to weight
        // ratio we can have for any item and maxindex
        // will store the index of that element
        float maxratio = int.MinValue;
        int maxindex = 0;

        // Find the maximum ratio
        for (int i = 0; i < n; i++)
        {
            if ((val[i] / wt[i]) > maxratio)
            {
                maxratio = (val[i] / wt[i]);
                maxindex = i;
            }
        }

        // The item with the maximum value to
        // weight ratio will be put into
        // the knapsack repeatedly until full
        return (W * maxratio);
    }

    // Driver code
    public static void Main()
    {
        float []val = {14, 27, 44, 19};
        float []wt = {6, 7, 9, 8};
        int n = val.Length;
        int W = 50;

        Console.WriteLine(knapSack(W, wt, val, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum required value
function knapSack(W, wt, val, n)
{

    // maxratio will store the maximum value to weight
    // ratio we can have for any item and maxindex
    // will store the index of that element
    var maxratio = -1000000000;
    var maxindex = 0;

    // Find the maximum ratio
    for (var i = 0; i < n; i++) {
        if (parseInt(val[i] / wt[i]) > maxratio) {
            maxratio = (val[i] / wt[i]);
            maxindex = i;
        }
    }

    // The item with the maximum value to
    // weight ratio will be put into
    // the knapsack repeatedly until full
    return (W * maxratio);
}

// Driver code
var val = [14, 27, 44, 19];
var wt = [6, 7, 9, 8];
var n = val.length;
var W = 50;
document.write( knapSack(W, wt, val, n).toFixed(3));

</script>
```

**Output:** 

```
244.444
```