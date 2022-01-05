# 安排电梯以减少总耗时

> 原文:[https://www . geesforgeks . org/schedule-电梯减少总耗时/](https://www.geeksforgeeks.org/schedule-elevator-to-reduce-the-total-time-taken/)

给定一个整数 **k** 和一个数组**arr【】**表示当前在底层等待的 **N** 人的目的楼层，而 **k** 是电梯的容量，即它可以同时容纳的最大人数。电梯从当前楼层到达任何连续楼层需要 1 个单位时间。任务是安排电梯的时间，使所有人到达目的地楼层然后返回一楼所需的总时间最小化。
**举例:**

> **输入:** arr[] = {2，3，4}，k = 2
> **输出:** 12
> 第二、第三人(目的层 3、4)以 8 (4 + 4)个单位时间第一个转弯。只剩下一个人需要 2 个单位的时间到达目的地
> 然后电梯再需要 2 个单位的时间回到一楼。
> 总耗时= 8 + 2 + 2 = 12
> **输入:** arr[] = {5，5，4}，k = 3
> **输出:** 10
> 每个人可以同时上电梯
> 所需时间为 10 (5 + 5)。

**方法:**按照目的地的降序对给定数组进行排序。创建 K 组(从最高楼层开始)，每组的成本为 **2 *(最大值(当前组中的元素))**。所有组的总和将是答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum time taken
// by the elevator when operating optimally
int minTime(int n, int k, int a[])
{
    // Sort in descending order
    sort(a, a + n, greater<int>());
    int minTime = 0;

    // Iterate through the groups
    for (int i = 0; i < n; i += k)

        // Update the time taken for each group
        minTime += (2 * a[i]);

    // Return the total time taken
    return minTime;
}

// Driver code
int main()
{
    int k = 2;
    int arr[] = { 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minTime(n, k, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum time taken
// by the elevator when operating optimally
static int minTime(int n, int k, int a[])
{
    // Sort in descending order
    int temp;
    for(int i = 0; i < n; i++)
    {    
        for(int j = i + 1; j < n; j++)
        {
            if(a[i] < a[j])
            {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }
    }

    int minTime = 0;

    // Iterate through the groups
    for (int i = 0; i < n; i += k)

        // Update the time taken for each group
        minTime += (2 * a[i]);

    // Return the total time taken
    return minTime;
}

// Driver code
public static void main(String args[])
{
    int k = 2;
    int arr[] = { 2, 3, 4 };
    int n = arr.length;
    System.out.println(minTime(n, k, arr));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum time taken
# by the elevator when operating optimally
def minTime(n, k, a) :

    # Sort in descending order
    a.sort(reverse = True);

    minTime = 0;

    # Iterate through the groups
    for i in range(0, n, k) :

        # Update the time taken for
        # each group
        minTime += (2 * a[i]);

    # Return the total time taken
    return minTime;

# Driver code
if __name__ == "__main__" :

    k = 2;
    arr = [ 2, 3, 4 ];
    n = len(arr) ;
    print(minTime(n, k, arr));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum time taken
// by the elevator when operating optimally
static int minTime(int n, int k, int []a)
{
    // Sort in descending order
    int temp;
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            if(a[i] < a[j])
            {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }
    }

    int minTime = 0;

    // Iterate through the groups
    for (int i = 0; i < n; i += k)

        // Update the time taken for each group
        minTime += (2 * a[i]);

    // Return the total time taken
    return minTime;
}

// Driver code
public static void Main(String []args)
{
    int k = 2;
    int []arr = { 2, 3, 4 };
    int n = arr.Length;
    Console.Write(minTime(n, k, arr));
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum time taken
// by the elevator when operating optimally
function minTime(n , k , a)
{
    // Sort in descending order
    var temp;
    for(var i = 0; i < n; i++)
    {    
        for(var j = i + 1; j < n; j++)
        {
            if(a[i] < a[j])
            {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }
    }   var minTime = 0;

    // Iterate through the groups
    for (var i = 0; i < n; i += k)

        // Update the time taken for each group
        minTime += (2 * a[i]);

    // Return the total time taken
    return minTime;
}

// Driver code
var k = 2;
var arr = [ 2, 3, 4 ];
var n = arr.length;
document.write(minTime(n, k, arr));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(N * log(N))
**辅助空间:** O(1)