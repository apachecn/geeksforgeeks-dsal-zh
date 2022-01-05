# 在二进制数组中找到过渡点

> 原文:[https://www . geesforgeks . org/find-transition-point-binary-array/](https://www.geeksforgeeks.org/find-transition-point-binary-array/)

给定一个只包含数字 0 和 1 的排序数组，任务是高效地找到转换点。转变点是“0”结束和“1”开始的点。

**示例:**

```
Input: 0 0 0 1 1
Output: 3
Explanation: Index of first 1 is 3

Input: 0 0 0 0 1 1 1 1
Output: 4
Explanation: Index of first 1 is 4
```

**<u>天真方法:</u>** 遍历数组，打印前 1 的索引。

1.  从数组的开始到结束遍历数组。
2.  如果当前元素为 1，打印索引并终止程序。

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// the transition point
#include<iostream>
using namespace std;

// Function to find the transition point
int findTransitionPoint(int arr[], int n)
{
    //perform a linear search and
    // return the index of
    //first 1
    for(int i=0; i<n ;i++)
      if(arr[i]==1)
        return i;

    //if no element is 1
    return -1;
}

// Driver code
int main()
{
    int arr[] = {0, 0, 0, 0, 1, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    int point = findTransitionPoint(arr, n);

    point >= 0 ? cout << "Transition point is "
                      << point
        : cout<<"There is no transition point";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the transition point
import java.util.*;

class GFG
{

// Function to find the transition point
static int findTransitionPoint(int arr[], int n)
{
    // perform a linear search and return the index of
    // first 1
    for(int i = 0; i < n ; i++)
    if(arr[i] == 1)
        return i;

    // if no element is 1
    return -1;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = {0, 0, 0, 0, 1, 1};
    int n = arr.length;

    int point = findTransitionPoint(arr, n);

    if (point >= 0)
        System.out.print("Transition point is " + point);
    else
        System.out.print("There is no transition point");
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation to find the transition point

# Function to find the transition point
def findTransitionPoint(arr, n):

    # perform a linear search and return the index of
    # first 1
    for i in range(n):
        if(arr[i] == 1):
            return i

    # if no element is 1
    return -1

# Driver code
arr = [0, 0, 0, 0, 1, 1]
n = len(arr)

point = findTransitionPoint(arr, n)

if point >= 0:
    print("Transition point is", point)
else:
    print("There is no transition point")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find the transition point
using System;

class GFG
{

// Function to find the transition point
static int findTransitionPoint(int []arr ,int n)
{
    // perform a linear search and return the index of
    // first 1
    for(int i = 0; i < n ; i++)
    if(arr[i] == 1)
        return i;

    // if no element is 1
    return -1;
}

 // Driver method
    public static void Main()
    {
        int []arr = {0, 0, 0, 0, 1, 1};
        int point = findTransitionPoint(arr, arr.Length);

        Console.Write(point >= 0 ? "Transition point is " +
                   point : "There is no transition point");
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript implementation to
    // find the transition point

    // Function to find the transition point
    function findTransitionPoint(arr, n)
    {
        // perform a linear search and
        // return the index of
        // first 1
        for(let i = 0; i < n ; i++)
            if(arr[i] == 1)
                return i;

        // if no element is 1
        return -1;
    }

    let arr = [0, 0, 0, 0, 1, 1];
    let point = findTransitionPoint(arr, arr.length);

    document.write(point >= 0 ? "Transition point is " +
                  point : "There is no transition point");

</script>
```

**Output**

```
Transition point is 4
```

**复杂度分析:**

*   **时间复杂度:** O(n)，只需要一次遍历，所以时间复杂度为 O(n)
*   **辅助空间:** O(1)，不需要额外空间。

**<u>高效进场:</u>** 思路是利用二分搜索法，找到数组中最小的索引 1。当数组被排序时，可以执行二分搜索法。

1.  创建两个变量 *l* 和 *r* ，初始化 *l = 0* 和 *r = n-1* 和一个变量 *ans = -1* 来存储答案。
2.  重复下面的步骤，直到 *l < = r* ，下限小于上限。
3.  检查中间索引 *mid = (l+r)/2* 处的元素是否为 1。
4.  如果元素为 1，则检查中间元素左侧 1 个元素的最小索引，即更新*r = mid–1*和更新 *ans = mid* 。
5.  如果元素为零，则检查中间元素右侧 1 个元素的最小索引，即更新 *l = mid + 1* 。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the transition point
#include<iostream>
using namespace std;

// Function to find the transition point
int findTransitionPoint(int arr[], int n)
{
    // Initialise lower and upper bounnds
    int lb = 0, ub = n-1;

    // Perform Binary search
    while (lb <= ub)
    {
        // Find mid
        int mid = (lb+ub)/2;

        // update lower_bound if mid contains 0
        if (arr[mid] == 0)
            lb = mid+1;

        // If mid contains 1
        else if (arr[mid] == 1)
        {
            // Check if it is the left most 1
            // Return mid, if yes
            if (mid == 0
                    || (mid > 0 &&
                       arr[mid - 1] == 0))
                return mid;

            // Else update upper_bound
            ub = mid-1;
        }
    }
    return -1;
}

// Driver Code
int main()
{
    int arr[] = {0, 0, 0, 0, 1, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    int point = findTransitionPoint(arr, n);

    point >= 0 ? cout<<"Transition point is " << point
               : cout<<"There is no transition point";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the transition point

class Test {
    // Method to find the transition point
    static int findTransitionPoint(int arr[], int n)
    {
        // Initialise lower and upper bounnds
        int lb = 0, ub = n - 1;

        // Perform Binary search
        while (lb <= ub) {
            // Find mid
            int mid = (lb + ub) / 2;

            // update lower_bound if mid contains 0
            if (arr[mid] == 0)
                lb = mid + 1;
            // If mid contains 1
            else if (arr[mid] == 1) {
                // Check if it is the left most 1
                // Return mid, if yes
                if (mid == 0
                    || (mid > 0 &&
                       arr[mid - 1] == 0))
                    return mid;
                // Else update upper_bound
                ub = mid - 1;
            }
        }
        return -1;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 0, 0, 0, 0, 1, 1 };

        int point = findTransitionPoint(arr, arr.length);

        System.out.println(
            point >= 0 ? "Transition point is " + point
                       : "There is no transition point");
    }
}
```

## 蟒蛇 3

```
# python implementation to find the
# transition point

# Function to find the transition
# point
def findTransitionPoint(arr, n):
    # Initialise lower and upper
    # bounnds
    lb = 0
    ub = n - 1

    # Perform Binary search
    while (lb <= ub):
        # Find mid
        mid = (int)((lb + ub) / 2)

        # update lower_bound if
        # mid contains 0
        if (arr[mid] == 0):
            lb = mid + 1

        # If mid contains 1
        elif (arr[mid] == 1):

            # Check if it is the
            # left most 1 Return
            # mid, if yes
            if (mid == 0 \
                or (mid > 0 and\
                arr[mid - 1] == 0)):
                return mid

            # Else update
            # upper_bound
            ub = mid-1

    return -1

# Driver code
arr = [0, 0, 0, 0, 1, 1]
n = len(arr)
point = findTransitionPoint(arr, n);
if(point >= 0):
    print("Transition point is ", point)
else:
    print("There is no transition point")

# This code is contributed by Sam007
```

## C#

```
// C# implementation to find the transition point
using System;

class GFG
{
    // Method to find the transition point
    static int findTransitionPoint(int []arr, int n)
    {
        // Initialise lower and upper bounnds
        int lb = 0, ub = n-1;

        // Perform Binary search
        while (lb <= ub)
        {
            // Find mid
            int mid = (lb+ub)/2;

            // update lower_bound if mid contains 0
            if (arr[mid] == 0)
                lb = mid+1;

            // If mid contains 1
            else if (arr[mid] == 1)
            {
                // Check if it is the left most 1
                // Return mid, if yes
                if (mid == 0
                    || (mid > 0 &&
                       arr[mid - 1] == 0))
                    return mid;

                // Else update upper_bound
                ub = mid-1;
            }
        }
        return -1;
    }

    // Driver method
    public static void Main()
    {
        int []arr = {0, 0, 0, 0, 1, 1};
        int point = findTransitionPoint(arr, arr.Length);

        Console.Write(point >= 0 ? "Transition point is " +
                   point : "There is no transition point");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the transition point

// Function to find the
// transition point
function findTransitionPoint($arr, $n)
{

    // Initialise lower and
    // upper bounnds
    $lb = 0; $ub = $n-1;

    // Perform Binary search
    while ($lb <= $ub)
    {

        // Find mid
        $mid = floor(($lb + $ub) / 2);

        // update lower_bound
        // if mid contains 0
        if ($arr[$mid] == 0)
            $lb = $mid + 1;

        // If mid contains 1
        else if ($arr[$mid] == 1)
        {

            // Check if it is the
            // left most 1
            // Return mid, if yes
            if ($mid == 0 or
                ($mid > 0 and
                 $arr[$mid - 1] == 0))
                return $mid;

            // Else update upper_bound
            $ub = $mid - 1;
        }
    }
    return -1;
}

    // Driver Code
    $arr = array(0, 0, 0, 0, 1, 1);
    $n = sizeof($arr);
    $point = findTransitionPoint($arr, $n);

    if($point >= 0)
        echo "Transition point is " , $point;
    else
        echo"There is no transition point";
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to find the transition point

    // Method to find the transition point
    function findTransitionPoint(arr, n)
    {
        // Initialise lower and upper bounnds
        let lb = 0, ub = n-1;

        // Perform Binary search
        while (lb <= ub)
        {
            // Find mid
            let mid = parseInt((lb+ub)/2, 10);

            // update lower_bound if mid contains 0
            if (arr[mid] == 0)
                lb = mid+1;

            // If mid contains 1
            else if (arr[mid] == 1)
            {
                // Check if it is the left most 1
                // Return mid, if yes
                if (mid == 0
                    || (mid > 0 &&
                       arr[mid - 1] == 0))
                    return mid;

                // Else update upper_bound
                ub = mid-1;
            }
        }
        return -1;
    }

    let arr = [0, 0, 0, 0, 1, 1];
    let point = findTransitionPoint(arr, arr.length);

    document.write(point >= 0 ? "Transition point is " +
                  point : "There is no transition point");

</script>
```

**Output**

```
Transition point is 4
```

**复杂度分析:**

*   **时间复杂度:** O(log n)。二分搜索法的时间复杂度是 0(对数 n)。
*   **辅助空间:** O(1)。不需要额外的空间。

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。