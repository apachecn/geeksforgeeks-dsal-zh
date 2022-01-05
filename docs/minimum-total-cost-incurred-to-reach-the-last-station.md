# 到达最后一站的最小总成本

> 原文:[https://www . geeksforgeeks . org/到达最后一站的最低总成本/](https://www.geeksforgeeks.org/minimum-total-cost-incurred-to-reach-the-last-station/)

给定一个数组，其中每个元素表示对应于每个站的巧克力数量，并且从站 I 移动到站 i+1，我们免费获得 A[I]–A[I+1]巧克力，如果这个数字是负数，我们也会失去那么多巧克力。
如果我们有非负数的巧克力，你只能从 I 站移动到 i+1 站。
给定一个巧克力 p 的成本，寻找从第一站(站 1)到达最后一站的最小成本的任务。
**注:**最初我们有 0 块巧克力。
示例:

```
Input : arr[] = {1, 2, 3}   p = 10
Output : 30
Initial choc_buy = 1 (arr[0])
To reach index 0 to 1, arr[0] - arr[1] = -1,
so choc_buy +=1.
Similarly To reach index 2 to 1, 
arr[1] - arr[2] = -1, so choc_buy +=1.
Total choc_buy = 3.
Total cost = choc_by * p = 3*10 = 30.

Input : arr[] = {10, 6, 11, 4, 7, 1}    p = 5
Output : 55
Initial choc_buy = 10 (arr[0])
To reach index 0 to 1, arr[0] - arr[1] = 4, 
so curr_choc =4.
Similarly To reach index 2 to 1, 
arr[1] - arr[2] = -5, so curr_choc=4+-5 = -1.
choc_buy += abs(-1).
So, similarly till last station, Total choc_buy = 11.
Total cost = choc_by * p = 11*5 = 55.
```

**进场:**
1。用数组的第一个元素初始化 choc_buy，curr_choc =0。
2。将 arr[i]-arr[i+1]添加到每个 I 的 curr_choc 中。
a)检查 curr_choc 是否为负数。
choc _ buy+= ABS(arr[I]-arr[I+1])
curr _ choc = 0
3。返回 choc_buy * p。

## C++

```
// C++ program to calculate
// minimum cost for candies
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum cost
// to be incurred
int findMinCost(int arr[], int n, int choc_cost) {

  // To reach first station, initial
  // chocolates required
  int choc_buy = arr[0];
  int curr_choc = 0;

  // Start traversing
  for (int i = 0; i < n - 1; i++) {

    // Find no. of chocolates
    // lose or gain
    int choc = arr[i] - arr[i + 1];

    // Add into curr_coc
    curr_choc += choc;

    // if no. of chocolates becomes
    // negative that means we have
    // to buy that no. of chocolates
    if (curr_choc < 0) {
      choc_buy += abs(curr_choc);
      curr_choc = 0;
    }
  }

  // Return cost required
  return choc_buy * choc_cost;
}

// Drivers code
int main() {
  int arr[] = {10, 6, 11, 4, 7, 1};
  int n = sizeof(arr) / sizeof(arr[0]);

  // Price of each candy
  int p = 5;

  cout << findMinCost(arr, n, p);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// minimum cost for candies
import java.io.*;

class GFG 
{
    // Function to find minimum cost
    // to be incurred
    static int findMinCost(int arr[], int n, int choc_cost) 
    {

    // To reach first station, initial
    // chocolates required
    int choc_buy = arr[0];
    int curr_choc = 0;

    // Start traversing
    for (int i = 0; i < n - 1; i++) 
    {

        // Find no. of chocolates
        // lose or gain
        int choc = arr[i] - arr[i + 1];

        // Add into curr_coc
        curr_choc += choc;

        // if no. of chocolates becomes
        // negative that means we have
        // to buy that no. of chocolates
        if (curr_choc < 0) 
        {
            choc_buy += Math.abs(curr_choc);
            curr_choc = 0;
        }
    }

    // Return cost required
    return choc_buy * choc_cost;
    }

    // Drivers code
    public static void main (String[] args) 
    {
        int arr[] = {10, 6, 11, 4, 7, 1};
        int n = arr.length;

        // Price of each candy
        int p = 5;

        System.out.println ( findMinCost(arr, n, p));   
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to calculate
# minimum cost for candies

# Function to find minimum cost
# to be incurred
def findMinCost(arr, n, choc_cost): 

    # To reach first station, 
    # initial chocolates required
    choc_buy = arr[0] 
    curr_choc = 0

    # Start traversing
    for i in range(0,n - 1): 

        # Find no. of chocolates lose
        # or gain
        choc = arr[i] - arr[i + 1] 

        # Add into curr_coc
        curr_choc += choc 

        # if no. of chocolates becomes
        # negative that means we have
        # to buy that no. of chocolates
        if (curr_choc < 0): 
            choc_buy += abs(curr_choc) 
            curr_choc = 0

    # Return cost required
    return choc_buy * choc_cost 

# Drivers code
arr = [10, 6, 11, 4, 7, 1] 
n = len(arr)

# Price of each candy
p = 5

print(findMinCost(arr, n, p))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to calculate
// minimum cost for candies
using System;

class GFG 
{
    // Function to find minimum cost
    // to be incurred
    static int findMinCost(int []arr,
                    int n, int choc_cost) 
    {

        // To reach first station, initial
        // chocolates required
        int choc_buy = arr[0];
        int curr_choc = 0;

        // Start traversing
        for (int i = 0; i < n - 1; i++) 
        {

            // Find no. of chocolates
            // lose or gain
            int choc = arr[i] - arr[i + 1];

            // Add into curr_coc
            curr_choc += choc;

            // if no. of chocolates becomes
            // negative that means we have
            // to buy that no. of chocolates
            if (curr_choc < 0) 
            {
                choc_buy += Math.Abs(curr_choc);
                curr_choc = 0;
            }
    }

    // Return cost required
    return choc_buy * choc_cost;
    }

    // Drivers code
    public static void Main () 
    {
        int []arr = {10, 6, 11, 4, 7, 1};
        int n = arr.Length;

        // Price of each candy
        int p = 5;

    Console.WriteLine( findMinCost(arr, n, p)); 
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// minimum cost for candies

// Function to find minimum cost
// to be incurred
function findMinCost($arr, $n, $choc_cost) 
{

    // To reach first station, initial
    // chocolates required
    $choc_buy = $arr[0];
    $curr_choc = 0;

    // Start traversing
    for ($i = 0; $i < $n - 1; $i++) {

        // Find no. of chocolates
        // lose or gain
        $choc = $arr[$i] - $arr[$i + 1];

        // Add into curr_coc
        $curr_choc += $choc;

        // if no. of chocolates becomes
        // negative that means we have
        // to buy that no. of chocolates
        if ($curr_choc < 0) {
        $choc_buy += abs($curr_choc);
        $curr_choc = 0;
        }
    }

    // Return cost required
    return $choc_buy * $choc_cost;
}

// Driver Code
$arr = array(10, 6, 11, 4, 7, 1);
$n = count($arr);

// Price of each candy
$p = 5;

echo findMinCost($arr, $n, $p);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// Javascript program to calculate
// minimum cost for candies

// Function to find minimum cost
// to be incurred
function findMinCost(arr,  n,  choc_cost) {

// To reach first station, initial
// chocolates required
var choc_buy = arr[0];
var curr_choc = 0;

// Start traversing
for (var i = 0; i < n - 1; i++) {

    // Find no. of chocolates
    // lose or gain
    var choc = arr[i] - arr[i + 1];

    // Add into curr_coc
    curr_choc += choc;

    // if no. of chocolates becomes
    // negative that means we have
    // to buy that no. of chocolates
    if (curr_choc < 0) {
    choc_buy += Math.abs(curr_choc);
    curr_choc = 0;
    }
}

// Return cost required
return (choc_buy * choc_cost);
}

var  arr = [10, 6, 11, 4, 7, 1];
var n = 6;

// Price of each candy
var p = 5;

document.write(findMinCost(arr, n, p));

</script>
```

**Output:** 

```
55
```