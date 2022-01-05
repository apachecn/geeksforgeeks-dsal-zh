# 数组遍历期间最大值和最小值更新的次数

> 原文:[https://www . geeksforgeeks . org/数组遍历期间最大和最小值更新的次数/](https://www.geeksforgeeks.org/number-of-times-maximum-and-minimum-value-updated-during-traversal-of-array/)

给定一个数组 **arr[]** ，任务是统计数组遍历过程中最小值和最大值被更新的次数。
**例:**

> **输入:** arr[] = {10，5，20，22}
> **输出:**
> 最小值更新次数= 2 次
> 最大值更新次数= 3 次
> **解释:**
> **步骤 1:** 最小值= 10，最大值= 10
> **步骤 2:** 最小值= 5，最大值= 10
> **步骤 3:** 最小值= 10 最大值= 22
> **输入:** arr[] = {1，2，3，4，5}
> **输出:**
> 最小值更新次数= 1
> 最大值更新次数= 5
> **解释:**
> **第 1 步:**最小值= 1，最大值= 1
> **第 2 步:**最小值= 1，最大值= 2
> T41

**进场:**思路是跟踪最小值和最大值。最初将这些值初始化为数组的第一个元素。最后，迭代数组，每当最大值或最小值要被改变时，相应地增加计数。

```
if (cur_min > arr[i])
    cur_min = arr[i]
    count_min++;
if (cur_max < arr[i])
    cur_max = arr[i]
    count_max++;
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// number of times minimum and
// maximum value updated during the
// traversal of the array
#include<bits/stdc++.h>
using namespace std;

// Function to find the number of
// times minimum and maximum value
// updated during the traversal
// of the given array
void maxUpdated(vector<int> arr)
{
  int h_score = arr[0];
  int l_score = arr[0];
  int i = 1, j = 1;

  // Increment i if new
  // highest value occurs
  // Increment j if new
  // lowest value occurs
  for (auto n : arr)
  {
    if (h_score < n)
    {
      h_score = n;
      i++;
    }
    if (l_score > n)
    {
      l_score = n;
      j++;
    }
  }

  cout << "Number of times maximum value ";
  cout << "updated = " << i << endl;
  cout << "Number of times minimum value ";
  cout << "updated = " << j << endl;
}

// Driver Code
int main()
{
  vector<int> arr({10, 5, 20, 22});
  maxUpdated(arr);
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// number of times minimum and
// maximum value updated during the
// traversal of the array

public class GFG {

    // Function to find the number of
    // times minimum and maximum value
    // updated during the traversal
    // of the given array
    static void maxUpdated(int[] arr)
    {
        int h_score = arr[0];
        int l_score = arr[0];
        int i = 1, j = 1;

        // Increment i if new
        // highest value occurs
        // Increment j if new
        // lowest value occurs
        for (Integer n : arr) {
            if (h_score < n) {
                h_score = n;
                i++;
            }
            if (l_score > n) {
                l_score = n;
                j++;
            }
        }
        System.out.print(
            "Number of times maximum value ");
        System.out.print(
            "updated = " + i + "\n");
        System.out.print(
            "Number of times minimum value ");
        System.out.print(
            "updated = " + j);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 10, 5, 20, 22 };
        maxUpdated(arr);
    }
}
```

## 计算机编程语言

```
# Python implementation to count
# the number of times maximum
# and minimum value updated

# Function to find the count
# the number of times maximum
# and minimum value updated
def maximumUpdates(arr):
    min = arr[0]
    max = arr[0]
    minCount, maxCount = 1, 1

    # Update the maximum and
    # minimum values during traversal
    for arr in arr :
        if arr>max:
            maxCount+= 1
            max = arr
        if arr<min:
            minCount+= 1;
            min = arr

    print("Number of times maximum ", end = "")
    print("value updated = ", maxCount)
    print("Number of times minimum ", end = "")
    print("value updated = ", minCount)

# Driver code
if __name__ == "__main__" :

    arr = [ 10, 5, 20, 22 ]
    maximumUpdates(arr)
```

## C#

```
// C# implementation to find the
// number of times minimum and
// maximum value updated during the
// traversal of the array
using System;

class GFG {

// Function to find the number of
// times minimum and maximum value
// updated during the traversal
// of the given array
static void maxUpdated(int[] arr)
{
    int h_score = arr[0];
    int l_score = arr[0];
    int i = 1, j = 1;

    // Increment i if new highest
    // value occurs Increment j
    // if new lowest value occurs
    foreach(int n in arr)
    {
        if (h_score < n)
        {
            h_score = n;
            i++;
        }
        if (l_score > n)
        {
            l_score = n;
            j++;
        }
    }

    Console.Write("Number of times maximum value ");
    Console.Write("updated = " + i + "\n");
    Console.Write("Number of times minimum value ");
    Console.Write("updated = " + j);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 10, 5, 20, 22 };
    maxUpdated(arr);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// number of times minimum and
// maximum value updated during the
// traversal of the array

    // Function to find the number of
    // times minimum and maximum value
    // updated during the traversal
    // of the given array
    function maxUpdated(arr)
    {
        let h_score = arr[0];
        let l_score = arr[0];
        let i = 1, j = 1;

        // Increment i if new
        // highest value occurs
        // Increment j if new
        // lowest value occurs
        for (let n in arr) {
            if (h_score < arr[n]) {
                h_score = n;
                i++;
            }
            if (l_score > n) {
                l_score = n;
                j++;
            }
        }
        document.write(
            "Number of times maximum value ");
        document.write(
            "updated = " + i + "<br/>");
        document.write(
            "Number of times minimum value ");
        document.write(
            "updated = " + j);
    }

// Driver Code

    let arr = [ 10, 5, 20, 22 ];
    maxUpdated(arr);

</script>
```

**Output:** 

```
Number of times maximum value updated = 3
Number of times minimum value updated = 2
```

时间复杂度:0(n)

辅助空间:0(1)