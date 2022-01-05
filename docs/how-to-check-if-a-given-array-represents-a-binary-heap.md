# 如何检查给定数组是否代表二进制堆？

> 原文:[https://www . geesforgeks . org/如何检查给定数组是否代表二进制堆/](https://www.geeksforgeeks.org/how-to-check-if-a-given-array-represents-a-binary-heap/)

给定一个数组，如何检查给定的数组是否代表一个[二进制最大堆](http://geeksquiz.com/binary-heap/)。
**例:**

```
Input:  arr[] = {90, 15, 10, 7, 12, 2} 
Output: True
The given array represents below tree
       90
     /    \
   15      10
  /  \     /
 7    12  2 
The tree follows max-heap property as every
node is greater than all of its descendants.

Input:  arr[] = {9, 15, 10, 7, 12, 11} 
Output: False
The given array represents below tree
       9
     /    \
   15      10
  /  \     /
 7    12  11
The tree doesn't follows max-heap property 9 is 
smaller than 15 and 10, and 10 is smaller than 11\. 
```

一个**简单的解决方法**是首先检查根是否大于它的所有后代。然后检查根的孩子。这个解的时间复杂度为 O(n <sup>2</sup> )
一个**高效解**是只比较根与其子代(不是所有的后代)，如果根大于其子代，并且所有节点都是如此，那么树就是 max-heap(这个结论是基于>算子的传递性，即如果 x > y 和 y > z，那么 x > z。
假设索引从 0 开始，最后一个内部节点出现在索引(n-2)/2 处。
下面是这个解决方案的实现。

## C++

```
// C program to check whether a given array
// represents a max-heap or not
#include <limits.h>
#include <stdio.h>

// Returns true if arr[i..n-1] represents a
// max-heap
bool isHeap(int arr[], int i, int n)
{
    // If a leaf node
    if (i >= (n - 2) / 2)
        return true;

    // If an internal node and is
    // greater than its children,
    // and same is recursively
    // true for the children
    if (arr[i] >= arr[2 * i + 1] &&
        arr[i] >= arr[2 * i + 2]
        && isHeap(arr, 2 * i + 1, n)
        && isHeap(arr, 2 * i + 2, n))
        return true;

    return false;
}

// Driver program
int main()
{
    int arr[] = { 90, 15, 10, 7, 12, 2, 7, 3 };
    int n = sizeof(arr) / sizeof(int) - 1;

    isHeap(arr, 0, n) ? printf("Yes") : printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a given array
// represents a max-heap or not
class GFG
{

    // Returns true if arr[i..n-1]
    // represents a max-heap
    static boolean isHeap(int arr[],
                          int i, int n)
    {
        // If a leaf node
        if (i >= (n - 2) / 2)
        {
            return true;
        }

        // If an internal node and
        // is greater than its
        // children, and same is
        // recursively true for the
        // children
        if (arr[i] >= arr[2 * i + 1]
            && arr[i] >= arr[2 * i + 2]
            && isHeap(arr, 2 * i + 1, n)
            && isHeap(arr, 2 * i + 2, n))
        {
            return true;
        }

        return false;
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = { 90, 15, 10, 7, 12, 2, 7, 3 };
        int n = arr.length - 1;
        if (isHeap(arr, 0, n)) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}

// This code contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check whether a
# given array represents a max-heap or not

# Returns true if arr[i..n-1]
# represents a max-heap
def isHeap(arr, i, n):

# If a leaf node
    if i >= int((n - 2) / 2):
        return True

    # If an internal node and is greater
    # than its children, and same is
    # recursively true for the children
    if(arr[i] >= arr[2 * i + 1] and
       arr[i] >= arr[2 * i + 2] and
       isHeap(arr, 2 * i + 1, n) and
       isHeap(arr, 2 * i + 2, n)):
        return True

    return False

# Driver Code
if __name__ == '__main__':
    arr = [90, 15, 10, 7, 12, 2, 7, 3]
    n = len(arr) - 1

    if isHeap(arr, 0, n):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
// C# program to check whether a given 
// array represents a max-heap or not
using System;

class GFG
{

// Returns true if arr[i..n-1] represents a
// max-heap
static bool isHeap(int []arr, int i, int n)
{
    // If a leaf node
    if (i >= (n - 2) / 2)
    {
        return true;
    }

    // If an internal node and is greater
    // than its children, and same is
    // recursively true for the children
    if (arr[i] >= arr[2 * i + 1] &&
        arr[i] >= arr[2 * i + 2] &&
        isHeap(arr, 2 * i + 1, n) &&
        isHeap(arr, 2 * i + 2, n))
    {
        return true;
    }

    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {90, 15, 10, 7, 12, 2, 7, 3};
    int n = arr.Length-1;
    if (isHeap(arr, 0, n))
    {
        Console.Write("Yes");
    }

    else
    {
        Console.Write("No");
    }
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether a given
// array represents a max-heap or not

// Returns true if arr[i..n-1]
// represents a max-heap
function isHeap($arr, $i, $n)
{

// If a leaf node
if ($i >= ($n - 2) / 2)
    return true;

// If an internal node and is greater
// than its children, and same is
// recursively true for the children
if ($arr[$i] >= $arr[2 * $i + 1] &&
    $arr[$i] >= $arr[2 * $i + 2] &&
    isHeap($arr, 2 * $i + 1, $n) &&
    isHeap($arr, 2 * $i + 2, $n))
    return true;

return false;
}

// Driver Code
$arr = array(90, 15, 10, 7, 12, 2, 7, 3);
$n = sizeof($arr);

if(isHeap($arr, 0, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to check whether a given array
// represents a max-heap or not

// Returns true if arr[i..n-1]
    // represents a max-heap
function isHeap(arr,i,n)
{
    // If a leaf node
        if (i >= (n - 2) / 2)
        {
            return true;
        }

        // If an internal node and
        // is greater than its
        // children, and same is
        // recursively true for the
        // children
        if (arr[i] >= arr[2 * i + 1]
            && arr[i] >= arr[2 * i + 2]
            && isHeap(arr, 2 * i + 1, n)
            && isHeap(arr, 2 * i + 2, n))
        {
            return true;
        }

        return false;
}

// Driver program
let arr=[ 90, 15, 10, 7, 12, 2, 7, 3 ];
let n = arr.length - 1;
if (isHeap(arr, 0, n)) {
    document.write("Yes<br>");
}
else {
    document.write("No<br>");
}

// This code is contributed by rag2127
</script>
```

**输出:**

```
Yes
```

这个解的时间复杂度是 O(n)。解决方法类似于二叉树的前序遍历。
感谢[乌卡什·特里维迪](http://qa.geeksforgeeks.org/user/utkarsh111)提出上述解决方案。
一个**迭代解**是遍历所有内部节点，检查 id 节点是否大于其子节点。

## C++

```
// C program to check whether a given array
// represents a max-heap or not
#include <stdio.h>
#include <limits.h>

// Returns true if arr[i..n-1] represents a
// max-heap
bool isHeap(int arr[],  int n)
{
    // Start from root and go till the last internal
    // node
    for (int i=0; i<=(n-2)/2; i++)
    {
        // If left child is greater, return false
        if (arr[2*i +1] > arr[i])
                return false;

        // If right child is greater, return false
        if (2*i+2 < n && arr[2*i+2] > arr[i])
                return false;
    }
    return true;
}

// Driver program
int main()
{
    int arr[] = {90, 15, 10, 7, 12, 2, 7, 3};
    int n = sizeof(arr) / sizeof(int);

    isHeap(arr, n)? printf("Yes"): printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a given array
// represents a max-heap or not

class GFG {

// Returns true if arr[i..n-1] represents a
// max-heap
    static boolean isHeap(int arr[], int n) {
        // Start from root and go till the last internal
        // node
        for (int i = 0; i <= (n - 2) / 2; i++) {
            // If left child is greater, return false
            if (arr[2 * i + 1] > arr[i]) {
                return false;
            }

            // If right child is greater, return false
            if (2 * i + 2 < n && arr[2 * i + 2] > arr[i]) {
                return false;
            }
        }
        return true;
    }

// Driver program
    public static void main(String[] args) {
        int arr[] = {90, 15, 10, 7, 12, 2, 7, 3};
        int n = arr.length;
        if (isHeap(arr, n)) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check whether a
# given array represents a max-heap or not

# Returns true if arr[i..n-1]
# represents a max-heap
def isHeap(arr, n):

    # Start from root and go till
    # the last internal node
    for i in range(int((n - 2) / 2) + 1):

        # If left child is greater,
        # return false
        if arr[2 * i + 1] > arr[i]:
                return False

        # If right child is greater,
        # return false
        if (2 * i + 2 < n and
            arr[2 * i + 2] > arr[i]):
                return False
    return True

# Driver Code
if __name__ == '__main__':
    arr = [90, 15, 10, 7, 12, 2, 7, 3]
    n = len(arr)

    if isHeap(arr, n):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
// C# program to check whether a given array
// represents a max-heap or not
using System;

class GFG
{

// Returns true if arr[i..n-1]
// represents a max-heap
static bool isHeap(int []arr, int n)
{
    // Start from root and go till
    // the last internal node
    for (int i = 0; i <= (n - 2) / 2; i++)
    {
        // If left child is greater,
        // return false
        if (arr[2 * i + 1] > arr[i])
        {
            return false;
        }

        // If right child is greater,
        // return false
        if (2 * i + 2 < n && arr[2 * i + 2] > arr[i])
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void Main()
{
    int []arr = {90, 15, 10, 7, 12, 2, 7, 3};
    int n = arr.Length;
    if (isHeap(arr, n))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether a
// given array represents a max-heap or not

// Returns true if arr[i..n-1]
// represents a max-heap
function isHeap($arr, $i, $n)
{
    // Start from root and go till
    // the last internal node
    for ($i = 0; $i < (($n - 2) / 2) + 1; $i++)
    {
        // If left child is greater,
        // return false
        if($arr[2 * $i + 1] > $arr[$i])
                return False;

        // If right child is greater,
        // return false
        if (2 * $i + 2 < $n &&
                $arr[2 * $i + 2] > $arr[$i])
                return False;

    return True;
    }
}

// Driver Code
$arr = array(90, 15, 10, 7, 12, 2, 7, 3);
$n = sizeof($arr);

if(isHeap($arr, 0, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Princi Singh
?>
```

## java 描述语言

```
<script>

// Javascript program to check
// whether a given array
// represents a max-heap or not

// Returns true if arr[i..n-1]
// represents a max-heap
function isHeap( arr, n)
{
    // Start from root and go till
    // the last internal node
    for (let i=0; i<=Math.floor((n-2)/2); i++)
    {
        // If left child is greater,
        // return false
        if (arr[2*i +1] > arr[i])
                return false;

        // If right child is greater,
        // return false
        if (2*i+2 < n && arr[2*i+2] > arr[i])
                return false;
    }
    return true;
}
    // driver code

    let arr = [90, 15, 10, 7, 12, 2, 7, 3];
    let n = arr.length;
    if (isHeap(arr, n)) {
        document.write("Yes");
        }
    else {
        document.write("No");
        }

</script>
```

**输出:**

```
Yes
```

感谢希曼舒提出这个解决方案。
如果发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论