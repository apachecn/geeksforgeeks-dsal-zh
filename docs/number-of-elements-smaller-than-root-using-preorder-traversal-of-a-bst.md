# 使用 BST 的前序遍历小于根的元素数量

> 原文:[https://www . geesforgeks . org/元素数量-小于根-使用-preorder-遍历-a-bst/](https://www.geeksforgeeks.org/number-of-elements-smaller-than-root-using-preorder-traversal-of-a-bst/)

给定一个 BST 的前序遍历。任务是找到小于根的元素数。
**例:**

```
Input: preorder[] = {3, 2, 1, 0, 5, 4, 6}
Output: 3

Input: preorder[] = {5, 4, 3, 2, 1}
Output: 4
```

对于二叉查找树，前序遍历的形式为:

> 根，{根的左子树中的元素}，{根的右子树中的元素}

**简单方法:**

1.  遍历给定的预订单。
2.  检查当前元素是否大于根元素。
3.  如果是，则返回当前元素的**索引–1**，因为小于根的元素数将是当前元素之前的所有元素，根除外。

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Function to find the first index of the element
// that is greater than the root
int findLargestIndex(int arr[], int n)
{
    int i, root = arr[0];

    // Traverse the given preorder
    for(i = 0; i < n-1; i++)
    {
        // Check if the number is greater than root
        // If yes then return that index-1
        if(arr[i] > root)
           return i-1;
    }

}

// Driver Code
int main()
{
    int preorder[] = {3, 2, 1, 0, 5, 4, 6};
    int n = sizeof(preorder) / sizeof(preorder[0]);

     cout << findLargestIndex(preorder, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach

class GFG
{
// Function to find the first
// index of the element that
// is greater than the root
static int findLargestIndex(int arr[],
                            int n)
{
    int i, root = arr[0];

    // Traverse the given preorder
    for(i = 0; i < n - 1; i++)
    {
        // Check if the number is
        // greater than root
        // If yes then return
        // that index-1
        if(arr[i] > root)
        return i-1;
    }
    return 0;
}

// Driver Code
public static void main(String ags[])
{
    int preorder[] = {3, 2, 1, 0, 5, 4, 6};
    int n = preorder.length;

    System.out.println(findLargestIndex(preorder, n));
}
}

// This code is contributed
// by Subhadeep Gupta
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find the first index of
# the element that is greater than the root
def findLargestIndex(arr, n):

    i, root = arr[0], arr[0];

    # Traverse the given preorder
    for i in range(0, n - 1):

        # Check if the number is greater than
        # root. If yes then return that index-1
        if(arr[i] > root):
            return i - 1;

# Driver Code
preorder= [3, 2, 1, 0, 5, 4, 6];
n = len(preorder)

print(findLargestIndex(preorder, n));

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the first
// index of the element that
// is greater than the root
static int findLargestIndex(int []arr,
                            int n)
{
    int i, root = arr[0];

    // Traverse the given preorder
    for(i = 0; i < n - 1; i++)
    {
        // Check if the number is
        // greater than root. If yes
        // then return that index-1
        if(arr[i] > root)
        return i - 1;
    }
    return 0;
}

// Driver Code
static public void Main()
{
    int []preorder = {3, 2, 1, 0, 5, 4, 6};
    int n = preorder.Length;

    Console.WriteLine(findLargestIndex(preorder, n));
}
}

// This code is contributed
// by Subhadeep Gupta
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the first index of
// the element that is greater than the root
function findLargestIndex( $arr, $n)
{
    $i; $root = $arr[0];

    // Traverse the given preorder
    for($i = 0; $i < $n - 1; $i++)
    {
        // Check if the number is greater than
        // root. If yes, then return that index-1
        if($arr[$i] > $root)
        return $i - 1;
    }

}

// Driver Code
$preorder = array(3, 2, 1, 0, 5, 4, 6);
$n = count($preorder);
echo findLargestIndex($preorder, $n);

// This code is contributed
// by 29AjayKumar
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to find the first index of the element
// that is greater than the root
function findLargestIndex(arr, n)
{
    var i, root = arr[0];

    // Traverse the given preorder
    for(i = 0; i < n-1; i++)
    {
        // Check if the number is greater than root
        // If yes then return that index-1
        if(arr[i] > root)
           return i-1;
    }

}

// Driver Code
var preorder = [3, 2, 1, 0, 5, 4, 6];
var n = preorder.length;
document.write( findLargestIndex(preorder, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)
**高效方法(利用二分搜索法)**:这里的思路是利用二分搜索法的一种扩展形式。步骤如下:

1.  去 mid。检查中间的元素是否大于根。如果是，那么我们在数组的左半部分递归。
2.  否则，如果中间的元素小于根，并且中间+1 的元素大于根，我们返回中间作为我们的答案。
3.  否则我们在数组的右半部分递归来重复上面的步骤。

以下是上述想法的实现。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the smaller elements
int findLargestIndex(int arr[], int n)
{
    int root = arr[0], lb = 0, ub = n-1;
    while(lb < ub)
    {

        int mid = (lb + ub)/2;

        // Check if the element at mid
        // is greater than root.
        if(arr[mid] > root)
            ub = mid - 1;
        else
        {
          // if the element at mid is lesser
          //  than root and element at mid+1
          // is greater
           if(arr[mid + 1] > root)
              return mid;
            else lb = mid + 1;
        }
     }
     return lb;
}

// Driver Code
int main()
{
    int preorder[] = {3, 2, 1, 0, 5, 4, 6};
    int n = sizeof(preorder) / sizeof(preorder[0]);

     cout << findLargestIndex(preorder, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.util.*;

class GFG
{

// Function to count the
// smaller elements
static int findLargestIndex(int arr[],
                            int n)
{
    int root = arr[0],
        lb = 0, ub = n - 1;
    while(lb < ub)
    {

        int mid = (lb + ub) / 2;

        // Check if the element at
        // mid is greater than root.
        if(arr[mid] > root)
            ub = mid - 1;
        else
        {

            // if the element at mid is
            // lesser than root and
            // element at mid+1 is greater
            if(arr[mid + 1] > root)
                return mid;
            else lb = mid + 1;
        }
    }
    return lb;
}

// Driver Code
public static void main(String args[])
{
    int preorder[] = {3, 2, 1, 0, 5, 4, 6};
    int n = preorder.length;

    System.out.println(
           findLargestIndex(preorder, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to count the smaller elements
def findLargestIndex(arr, n):
    root = arr[0];
    lb = 0;
    ub = n - 1;
    while(lb < ub):

        mid = (lb + ub) // 2;

        # Check if the element at mid
        # is greater than root.
        if(arr[mid] > root):
            ub = mid - 1;
        else:

            # if the element at mid is lesser
            # than root and element at mid+1
            # is greater
            if(arr[mid + 1] > root):
                return mid;
            else:
                lb = mid + 1;
    return lb;

# Driver Code
preorder = [3, 2, 1, 0, 5, 4, 6];
n = len(preorder);

print(findLargestIndex(preorder, n));

# This code is contributed by mits
```

## C#

```
// C# implementation
// of above approach
using System;

class GFG
{

// Function to count the
// smaller elements
static int findLargestIndex(int []arr,
                            int n)
{
    int root = arr[0],
        lb = 0, ub = n - 1;
    while(lb < ub)
    {

        int mid = (lb + ub) / 2;

        // Check if the element at
        // mid is greater than root.
        if(arr[mid] > root)
            ub = mid - 1;
        else
        {

            // if the element at mid is
            // lesser than root and
            // element at mid+1 is greater
            if(arr[mid + 1] > root)
                return mid;
            else lb = mid + 1;
        }
    }
    return lb;
}

// Driver Code
public static void Main(String []args)
{
    int []preorder = {3, 2, 1, 0, 5, 4, 6};
    int n = preorder.Length;

    Console.WriteLine(
        findLargestIndex(preorder, n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to count the smaller elements
function findLargestIndex($arr, $n)
{
    $root = $arr[0];
    $lb = 0;
    $ub = $n - 1;
    while($lb < $ub)
    {

        $mid = (int)(($lb + $ub) / 2);

        // Check if the element at mid
        // is greater than root.
        if($arr[$mid] > $root)
            $ub = $mid - 1;
        else
        {
            // if the element at mid is lesser
            // than root and element at mid+1
            // is greater
            if($arr[$mid + 1] > $root)
                return $mid;
            else
                $lb = $mid + 1;
        }
    }
    return $lb;
}

// Driver Code
$preorder = array(3, 2, 1, 0, 5, 4, 6);
$n = count($preorder);

echo findLargestIndex($preorder, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to count the smaller elements
function findLargestIndex(arr, n)
{
    var root = arr[0], lb = 0, ub = n-1;
    while(lb < ub)
    {

        var mid = parseInt((lb + ub)/2);

        // Check if the element at mid
        // is greater than root.
        if(arr[mid] > root)
            ub = mid - 1;
        else
        {
          // if the element at mid is lesser
          //  than root and element at mid+1
          // is greater
           if(arr[mid + 1] > root)
              return mid;
            else lb = mid + 1;
        }
     }
     return lb;
}

// Driver Code
var preorder = [3, 2, 1, 0, 5, 4, 6];
var n = preorder.length;
document.write( findLargestIndex(preorder, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(logn)