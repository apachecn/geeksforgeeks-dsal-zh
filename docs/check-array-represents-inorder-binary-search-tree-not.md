# 检查一个数组是否代表二叉查找树的整数

> 原文:[https://www . geesforgeks . org/check-array-representatives-inoder-binary-search-tree-not/](https://www.geeksforgeeks.org/check-array-represents-inorder-binary-search-tree-not/)

给定一组 **N** 元素。任务是检查它是否是任意二叉查找树的有序遍历。打印“是”，如果它是任何其他二叉查找树的有序遍历打印“否”。
**例:**

```
Input : arr[] = { 19, 23, 25, 30, 45 }
Output : Yes

Input : arr[] = { 19, 23, 30, 25, 45 }
Output : No
```

这个想法是利用二叉查找树的有序遍历是有序的这一事实。所以，只要检查给定的数组是否排序。

## C++

```
// C++ program to check if a given array is sorted
// or not.
#include<bits/stdc++.h>
using namespace std;

// Function that returns true if array is Inorder
// traversal of any Binary Search Tree or not.
bool isInorder(int arr[], int n)
{
    // Array has one or no element
    if (n == 0 || n == 1)
        return true;

    for (int i = 1; i < n; i++)

        // Unsorted pair found
        if (arr[i-1] > arr[i])
            return false;

    // No unsorted pair found
    return true;
}

// Driver code
int main()
{
    int arr[] = { 19, 23, 25, 30, 45 };
    int n = sizeof(arr)/sizeof(arr[0]);

    if (isInorder(arr, n))
        cout << "Yesn";
    else
        cout << "Non";

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given array is sorted
// or not.

class GFG {

// Function that returns true if array is Inorder
// traversal of any Binary Search Tree or not.
    static boolean isInorder(int[] arr, int n) {
        // Array has one or no element
        if (n == 0 || n == 1) {
            return true;
        }

        for (int i = 1; i < n; i++) // Unsorted pair found
        {
            if (arr[i - 1] > arr[i]) {
                return false;
            }
        }

        // No unsorted pair found
        return true;
    }
// Drivers code

    public static void main(String[] args) {
        int arr[] = {19, 23, 25, 30, 45};
        int n = arr.length;
        if (isInorder(arr, n)) {
            System.out.println("Yes");
        } else {
            System.out.println("Non");
        }
    }
}
//This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to check if a given array
# is sorted or not.

# Function that returns true if array is Inorder
# traversal of any Binary Search Tree or not.
def isInorder(arr, n):

    # Array has one or no element
    if (n == 0 or n == 1):
        return True

    for i in range(1, n, 1):

        # Unsorted pair found
        if (arr[i - 1] > arr[i]):
            return False

    # No unsorted pair found
    return True

# Driver code
if __name__ == '__main__':
    arr = [19, 23, 25, 30, 45]
    n = len(arr)

    if (isInorder(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to check if a given
// array is sorted or not.
using System;

class GFG
{

// Function that returns true if
// array is Inorder traversal of
// any Binary Search Tree or not.
static bool isInorder(int[] arr, int n)
{
    // Array has one or no element
    if (n == 0 || n == 1)
    {
        return true;
    }

    // Unsorted pair found
    for (int i = 1; i < n; i++)
    {
        if (arr[i - 1] > arr[i])
        {
            return false;
        }
    }

    // No unsorted pair found
    return true;
}

// Driver code
public static void Main()
{
    int []arr = {19, 23, 25, 30, 45};
    int n = arr.Length;
    if (isInorder(arr, n))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("Non");
    }
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given
// array is sorted or not.

// Function that returns true if array
// is Inorder traversal of any Binary
// Search Tree or not.
function isInorder($arr, $n)
{
    // Array has one or no element
    if ($n == 0 || $n == 1)
        return true;

    for ($i = 1; $i < $n; $i++)

        // Unsorted pair found
        if ($arr[$i - 1] > $arr[$i])
            return false;

    // No unsorted pair found
    return true;
}

// Driver code
$arr = array(19, 23, 25, 30, 45);
$n = sizeof($arr);

if (isInorder($arr, $n))
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
// javascript program to check if a given array is sorted
// or not.

    // Function that returns true if array is Inorder
    // traversal of any Binary Search Tree or not.
    function isInorder(arr , n)
    {

        // Array has one or no element
        if (n == 0 || n == 1) {
            return true;
        }

        for (i = 1; i < n; i++) // Unsorted pair found
        {
            if (arr[i - 1] > arr[i]) {
                return false;
            }
        }

        // No unsorted pair found
        return true;
    }

    // Drivers code
        var arr = [ 19, 23, 25, 30, 45 ];
        var n = arr.length;
        if (isInorder(arr, n)) {
            document.write("Yes");
        } else {
            document.write("Non");
        }

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
Yes
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。