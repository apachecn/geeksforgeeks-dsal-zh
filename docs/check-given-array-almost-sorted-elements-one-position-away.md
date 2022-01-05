# 检查给定数组是否已排序完毕(元素最多相距一个位置)

> 原文:[https://www . geesforgeks . org/check-given-array-几乎排序-elements-one-position-away/](https://www.geeksforgeeks.org/check-given-array-almost-sorted-elements-one-position-away/)

给定一个有 n 个不同元素的数组。如果一个数组的任何元素在排序后的数组中离其原始位置最多有 1 个距离，则称该数组几乎是排序的(非递减的)。我们需要找到给定的数组是否已经排序。
**例:**

```
Input : arr[] = {1, 3, 2, 4}
Output : Yes
Explanation : All elements are either
at original place or at most a unit away. 

Input : arr[] = {1, 4, 2, 3}
Output : No
Explanation : 4 is 2 unit away from
its original place.
```

**排序方法:**借助于排序，我们可以预测给定的数组是否几乎被排序。这背后的思想是首先对输入数组 A[]进行排序，然后如果数组将几乎被排序，那么给定数组的每个元素 Ai 必须等于排序数组 B[]的 Bi-1、Bi 或 Bi+1 中的任何一个。
时间复杂度:0(nlogn)

```
// suppose B[] is copy of A[]
sort(B, B+n);

// check first element
if ((A[0]!=B[0]) && (A[0]!=B[1]) )
    return 0;
// iterate over array
for(int i=1; i<n-1; i++)
{
    if (A[i]!=B[i-1]) && (A[i]!=B[i]) && (A[i]!=B[i+1]) )
        return false;
}
// check for last element
if ((A[i]!=B[i-1]) && (A[i]!=B[i]) )
    return 0;

// finally return true
return true;
```

时间复杂度:O(n Log n)
**高效方法:**这个想法基于[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)。像冒泡排序一样，我们比较相邻的元素，如果它们没有按顺序排列，就交换它们。这里交换之后，我们将索引额外移动一个位置，这样冒泡就被限制在一个位置。因此，在一次迭代之后，如果结果数组被排序，那么我们可以说我们的输入数组几乎被排序了，否则几乎没有排序。

```
// perform bubble sort tech once
for (int i=0; i<n-1; i++)
    if (A[i+1]<A[i])
        swap(A[i], A[i+1]);
        i++;

// check whether resultant is sorted or not
for (int i=0; i<n-1; i++)
    if (A[i+1]<A[i])
        return false;

// If resultant is sorted return true
return true;
```

## C++

```
// CPP program to find whether given array
// almost sorted or not
#include <bits/stdc++.h>
using namespace std;

// function for checking almost sort
bool almostSort(int A[], int n)
{
    // One by one compare adjacents.
    for (int i = 0; i < n - 1; i++) {
        if (A[i] > A[i + 1]) {
            swap(A[i], A[i + 1]);
            i++;
        }
    }

    // check whether resultant is sorted or not
    for (int i = 0; i < n - 1; i++)
        if (A[i] > A[i + 1])
            return false;

    // is resultant is sorted return true
    return true;
}

// driver function
int main()
{
    int A[] = { 1, 3, 2, 4, 6, 5 };
    int n = sizeof(A) / sizeof(A[0]);
    if (almostSort(A, n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to check if given array is almost
// sorted or not
import java.util.*;

class GFG {

    // function for checking almost sort
    public static boolean almostSort(int A[], int n)
    {
        // One by one compare adjacents.
        for (int i = 0; i < n - 1; i++) {
            if (A[i] > A[i + 1]) {
                int temp = A[i];
                A[i] = A[i+1];
                A[i+1] = temp;
                i++;
            }
        }

        // check whether resultant is sorted or not
        for (int i = 0; i < n - 1; i++)
            if (A[i] > A[i + 1])
                return false;

        // is resultant is sorted return true
        return true;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int A[] = { 1, 3, 2, 4, 6, 5 };
        int n = A.length;
        if (almostSort(A, n))
            System.out.print("Yes");
        else
            System.out.print("No");

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find whether given
# array almost sorted or not

# Function for checking almost sort
def almostSort(A, n):

    # One by one compare adjacents.
    i = 0
    while i < n - 1:
        if A[i] > A[i + 1]:
            A[i], A[i + 1] = A[i + 1], A[i]
            i += 1

        i += 1

    # check whether resultant is sorted or not
    for i in range(0, n - 1):
        if A[i] > A[i + 1]:
            return False

    # Is resultant is sorted return true
    return True

# Driver Code
if __name__ == "__main__":

    A = [1, 3, 2, 4, 6, 5]
    n = len(A)
    if almostSort(A, n):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# Code to check if given array
// is almost sorted or not
using System;

class GFG {

    // function for checking almost sort
    public static bool almostSort(int []A, int n)
    {

        // One by one compare adjacents.
        for (int i = 0; i < n - 1; i++)
        {
            if (A[i] > A[i + 1])
            {
                int temp = A[i];
                A[i] = A[i + 1];
                A[i + 1] = temp;
                i++;
            }
        }

        // Check whether resultant is
        // sorted or not
        for (int i = 0; i < n - 1; i++)
            if (A[i] > A[i + 1])
                return false;

        // is resultant is sorted return true
        return true;
    }

    // Driver Code
    public static void Main()
    {
        int []A = {1, 3, 2, 4, 6, 5};
        int n = A.Length;
        if (almostSort(A, n))
            Console.Write("Yes");
        else
            Console.Write("No");

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// whether given array
// almost sorted or not

// function for checking
// almost sort
function almostSort($A, $n)
{
    // One by one compare adjacents.
    for ($i = 0; $i < $n - 1; $i++)
    {
        if ($A[$i] > $A[$i + 1])
        {
            list($A[$i],
                 $A[$i + 1]) = array($A[$i + 1],
                                     $A[$i] );

            $i++;
        }
    }

    // check whether resultant
    // is sorted or not
    for ($i = 0; $i <$n - 1; $i++)
        if ($A[$i] > $A[$i + 1])
            return false;

    // is resultant is
    // sorted return true
    return true;
}

// Driver Code
$A = array (1, 3, 2,
            4, 6, 5);
$n = sizeof($A) ;
if (almostSort($A, $n))
    echo "Yes", "\n";
else
    echo "Yes", "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Code to check if given array
    // is almost sorted or not

    // function for checking almost sort
    function almostSort(A, n)
    {

        // One by one compare adjacents.
        for (let i = 0; i < n - 1; i++)
        {
            if (A[i] > A[i + 1])
            {
                let temp = A[i];
                A[i] = A[i + 1];
                A[i + 1] = temp;
                i++;
            }
        }

        // Check whether resultant is
        // sorted or not
        for (let i = 0; i < n - 1; i++)
            if (A[i] > A[i + 1])
                return false;

        // is resultant is sorted return true
        return true;
    }

    let A = [1, 3, 2, 4, 6, 5];
    let n = A.length;
    if (almostSort(A, n))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**输出:**

```
Yes
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.linkedin.com/in/imanuj)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。