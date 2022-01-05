# 移除 k 个角元素，最大化剩余总和

> 原文:[https://www . geesforgeks . org/remove-k-corner-elements-to-maximum-remain-sum/](https://www.geeksforgeeks.org/remove-k-corner-elements-to-maximize-remaining-sum/)

给定一个数组，任务是从角中移除总共 k 个元素，以最大化剩余元素的总和。例如，如果我们 k = 5，如果我们从左上角移除 2 个元素，那么我们需要从右上角移除 3 个元素。
**例:**

> **输入**:arr =【11，49，100，20，86，29，72】，k = 4
> **输出** : 206
> **说明:**:我们从右上角去掉 29 和 72。我们还从左上角去掉 11 和 49，得到剩余元素的最大和为 206。
> 
> **输入**:arr[]=【1，2，3，4，5，6，1】，k = 3
> **输出:** 18
> **说明:**:我们从左上角(1 和 2)去掉两个元素，从右上角(1)去掉一个元素。

**天真方法:**
1)将结果初始化为负无穷大。
2)计算总和。
3)运行 x = 1 到 k
的循环…..从左侧移除“x”元素，从右侧移除 k–I 元素。
…..如果剩余元素的总和大于结果，请更新结果。

时间复杂度:O(n * k)
**高效方法(使用** [**窗口滑动**](https://www.geeksforgeeks.org/window-sliding-technique/) **技巧)**
1)找到前 n-k 个元素的和，并将其初始化为当前和，同时将其初始化为结果。
2)运行 i = n-k 到 n-1 的循环
…。curr _ sum = curr _ sum–arr[I–n+k]+arr[I]
…。res = max(res，curr_sum)
在第 2 步中，我们主要运行滑动窗口。我们从左侧移除一个元素，从右侧添加一个元素。

下面是上述问题语句的 c++实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;
int calculate(int arr[], int n, int k)
{
    // Calculate the sum of all elements
    // excluding the last k elements..
    int curr_sum = 0;
    for (int i = 0; i < n - k; i++)
        curr_sum += arr[i];

    // now here its time to use sliding window
    // concept, remove the first element from
    // the current window and add the new element
    // in it in order to get the sum of all n-k size
    // of elements in arr.
    // Calculate the minimum sum of elements of
    // size n-k and stored it into the result
    int res = curr_sum;
    for (int i = n - k; i < n; i++) {
        curr_sum = curr_sum - arr[i - n + k] + arr[i];
        res = max(res, curr_sum);
    }

    // Now return result (sum of remaining n-k elements)
    return res;
}

// main function
int main()
{
    int arr[] = { 11, 49, 100, 20, 86, 29, 72 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    cout << "Maximum sum of remaining elements "
         << calculate(arr, n, k) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static int calculate(int[] arr,
                     int n, int k)
{
  // Calculate the total
  // sum of all elements
  // present in the array..
  int total_sum = 0;

  for (int i = 0; i < n; i++)
    total_sum += arr[i];

  // Now calculate the sum
  // of all elements excluding
  // the last k elements..
  int curr_sum = 0;

  for (int i = 0; i < n - k; i++)
    curr_sum += arr[i];

  // Now here its time to use
  // sliding window concept,
  // remove the first element
  // from the current window
  // and add the new element
  // in it in order to get
  // the sum of all n-k size
  // of elements in arr.
  // Calculate the minimum
  // sum of elements of
  // size n-k and stored it
  // into the result
  int res = curr_sum;

  for (int i = n - k; i < n; i++)
  {
    curr_sum = curr_sum -
               arr[i - n + k] +
               arr[i];
    res = Math.max(res, curr_sum);
  }

  // Now return result (sum of
  // remaining n-k elements)
  return res;
}

// Driver code
public static void main(String[] args)
{
  int[] arr = {11, 49, 100,
               20, 86, 29, 72};
  int n = arr.length;
  int k = 4;
  System.out.print("Maximum sum of remaining " +
                   "elements " +
                    calculate(arr, n, k) + "\n");
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
def calculate(arr, n, k):

    # calculate the total sum of all elements
    # present in the array..
    total_sum = 0
    for i in arr:
        total_sum += i

    # now calculate the sum of all elements
    # excluding the last k elements..
    curr_sum = 0
    for i in range(n - k):
        curr_sum += arr[i]

    # now here its time to use sliding window
    # concept, remove the first element from
    # the current window and add the new element
    # in it in order to get the sum of all n-k size
    # of elements in arr.
    # Calculate the minimum sum of elements of
    # size n-k and stored it into the result
    res = curr_sum
    for i in range(n - k, n):
        curr_sum = curr_sum - arr[i - n + k] + arr[i]
        res = max(res, curr_sum)

    # Now return result (sum of remaining n-k elements)
    return res

# main function
if __name__ == '__main__':
    arr=[11, 49, 100, 20, 86, 29, 72]
    n = len(arr)
    k = 4
    print("Maximum sum of remaining elements ",calculate(arr, n, k))

# This code is contributed by mohit kumar 29   
```

## C#

```
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

static int calculate(int []arr, int n, int k)
{

    // Calculate the total sum of all elements
    // present in the array..
    int total_sum = 0;
    for(int i = 0; i < n; i++)
        total_sum += arr[i];

    // Now calculate the sum of all elements
    // excluding the last k elements..
    int curr_sum = 0;
    for(int i = 0; i < n - k; i++)
        curr_sum += arr[i];

    // Now here its time to use sliding window
    // concept, remove the first element from
    // the current window and add the new element
    // in it in order to get the sum of all n-k size
    // of elements in arr.
    // Calculate the minimum sum of elements of
    // size n-k and stored it into the result
    int res = curr_sum;
    for(int i = n - k; i < n; i++)
    {
        curr_sum = curr_sum -
                  arr[i - n + k] + arr[i];
        res = Math.Max(res, curr_sum);
    }

    // Now return result (sum of
    // remaining n-k elements)
    return res;
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 11, 49, 100, 20, 86, 29, 72 };
    int n = arr.Length;
    int k = 4;

    Console.Write("Maximum sum of remaining " +
                  "elements " +
                  calculate(arr, n, k) + "\n");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

function calculate(arr, n, k)
{

    // calculate the total sum of all elements
    // present in the array..
    let total_sum = 0;
    for (let i = 0; i < n; i++)
        total_sum += arr[i];

    // now calculate the sum of all elements
    // excluding the last k elements..
    let curr_sum = 0;
    for (let i = 0; i < n - k; i++)
        curr_sum += arr[i];

    // now here its time to use sliding window
    // concept, remove the first element from
    // the current window and add the new element
    // in it in order to get the sum of all n-k size
    // of elements in arr.
    // Calculate the minimum sum of elements of
    // size n-k and stored it into the result
    let res = curr_sum;
    for (let i = n - k; i < n; i++) {
        curr_sum = curr_sum - arr[i - n + k] + arr[i];
        res = Math.max(res, curr_sum);
    }

    // Now return result (sum of remaining n-k elements)
    return res;
}

// main function
let arr = [11, 49, 100, 20, 86, 29, 72];
let n = arr.length;
let k = 4;
document.write("Maximum sum of remaining elements " + calculate(arr, n, k) + "<br>");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Maximum sum of remaining elements 206
```

**时间复杂度:**O(k)
T3】辅助空间: O(1)