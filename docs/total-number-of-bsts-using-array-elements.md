# 使用数组元素的 BST 总数

> 原文:[https://www . geeksforgeeks . org/total-number-of-BST-use-array-elements/](https://www.geeksforgeeks.org/total-number-of-bsts-using-array-elements/)

**先决条件:** [具有 N 个键的可能二分搜索法树的总数](https://www.geeksforgeeks.org/total-number-of-possible-binary-search-trees-with-n-keys/)
给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 的 **N 个**整数。任务是统计**arr【】**中元素的每个节点作为根节点可以制作的[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)的数量。
**举例:**

> **输入:** arr[] = { 20，10，30 }
> **输出:** 1 2 2
> **输入:** arr[] = { 1，2，3，4，5 }
> **输出:** 14 5 4 5 14

**途径:**T2】二叉查找树(BST) 可能的总数由[加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/) :
给出

```
Cn = (2n)!/(( n+1)!*n!) 
where n = number of distinct keys.
```

1.  计算小于当前节点的元素数(比如 **c1** )。
2.  计算大于当前节点的元素数量(比如 **c2** )。
3.  那么使用当前元素作为根节点可以形成的[二叉查找树(BST)](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) 的总数等于使用 **c1** 元素形成的 [BST](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) 的总数与使用 **c2** 元素形成的 [BST](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) 的总数的乘积。

```
Total Number of BST = Cc1*Cc2
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above code
#include <iostream>
using namespace std;

// A function to find factorial of a
// given number
int fact(int num)
{
    int fact = 1;

    while(num > 1)
    {
        fact *= num;
        num -= 1;
    }
    return fact;
}

// Find nth catalan number
int catalan(int n)
{
    return fact(2 * n)/(fact(n) * fact(n + 1)) ;
}

// Driver Code
int main()
{

    // size of arr[]
    int n = 5;

    // Elements in arr[]
    int arr[] = {1, 2, 3, 4, 5};
    int i,k;
    for(k = 0; k < n; k++)
    {
        int s = 0;

        // Count the number of element
        // less than current element
        // in arr[k]
        for(i = 0; i < n; i++)
        {
            if (arr[i] < arr[k])
                s += 1 ;
        }

        // Here s = number of node in left
        // BST and (n-s-1) = number of node
        // in right BST
        // Find number of BST using elements
        // in left BST
        int catalan_leftBST = catalan(s) ;

        // Find number of BST using elements
        // in right BST
        int catalan_rightBST = catalan(n - s - 1) ;

        // Find total number of BST
        int totalBST = catalan_rightBST * catalan_leftBST ;

        // Print total BST count
        cout<< totalBST <<  " " ;

    }
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation of the above code
public class GFG
{

// A function to find factorial of a
// given number
static int fact(int num)
{
    int fact = 1;

    while(num > 1)
    {
        fact *= num;
        num -= 1;
    }
    return fact;
    }

// Find nth catalan number
static int catalan(int n)
{
    return fact(2 * n)/(fact(n) * fact(n + 1)) ;
}

// Driver Code
public static void main (String[] args)
{

    // size of arr[]
    int n = 5;

    // Elements in arr[]
    int arr[] = {1, 2, 3, 4, 5};
    int i,k;
    for(k = 0; k < n; k++)
    {
        int s = 0;

        // Count the number of element
        // less than current element
        // in arr[k]
        for(i = 0; i < n; i++)
        {
            if (arr[i] < arr[k])
                s += 1 ;
        }

        // Here s = number of node in left
        // BST and (n-s-1) = number of node
        // in right BST
        // Find number of BST using elements
        // in left BST
        int catalan_leftBST = catalan(s) ;

        // Find number of BST using elements
        // in right BST
        int catalan_rightBST = catalan(n - s - 1) ;

        // Find total number of BST
        int totalBST = catalan_rightBST * catalan_leftBST ;

        // Print total BST count
        System.out.print(totalBST + " ") ;

    }
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# A function to find factorial of a
# given number
def fact(num):
    fact = 1;

    while(num>1):
        fact = fact * num;
        num = num-1;
    return fact;

# Find nth catalan number
def catalan(n):
    return fact(2 * n)//(fact(n)*fact(n + 1))

# Driver Code
if __name__ == '__main__':

    # size of arr[]
    n = 5

    # Elements in arr[]
    arr = [1, 2, 3, 4, 5]

    for k in range(n):
        s = 0

        # Count the number of element
        # less than current element
        # in arr[k]
        for i in range(n):
            if arr[i] < arr[k]:
                s+= 1

        # Here s = number of node in left
        # BST and (n-s-1) = number of node
        # in right BST
        # Find number of BST using elements
        # in left BST
        catalan_leftBST = catalan(s)

        # Find number of BST using elements
        # in right BST
        catalan_rightBST = catalan(n-s-1)

        # Find total number of BST
        totalBST = catalan_rightBST * catalan_leftBST

        # Print total BST count
        print(totalBST, end =" ")
```

## C#

```
// C# implementation of the above code
using System;

class GFG
{

// A function to find factorial of a
// given number
static int fact(int num)
{
    int fact = 1;

    while(num > 1)
    {
        fact *= num;
        num -= 1;
    }
    return fact;
    }

// Find nth catalan number
static int catalan(int n)
{
    return fact(2 * n)/(fact(n) * fact(n + 1)) ;
}

// Driver Code
public static void Main(String[] args)
{

    // size of []arr
    int n = 5;

    // Elements in []arr
    int []arr = {1, 2, 3, 4, 5};
    int i,k;
    for(k = 0; k < n; k++)
    {
        int s = 0;

        // Count the number of element
        // less than current element
        // in arr[k]
        for(i = 0; i < n; i++)
        {
            if (arr[i] < arr[k])
                s += 1 ;
        }

        // Here s = number of node in left
        // BST and (n-s-1) = number of node
        // in right BST
        // Find number of BST using elements
        // in left BST
        int catalan_leftBST = catalan(s) ;

        // Find number of BST using elements
        // in right BST
        int catalan_rightBST = catalan(n - s - 1) ;

        // Find total number of BST
        int totalBST = catalan_rightBST * catalan_leftBST ;

        // Print total BST count
        Console.Write(totalBST + " ") ;

    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above code

// A function to find factorial of a
// given number
function fact(num)
{
    var fact = 1;

    while(num > 1)
    {
        fact *= num;
        num -= 1;
    }
    return fact;
}

// Find nth catalan number
function catalan(n)
{
    return fact(2 * n)/(fact(n) * fact(n + 1)) ;
}

// Driver Code

// size of arr[]
var n = 5;

// Elements in arr[]
var arr = [1, 2, 3, 4, 5] ;
var i,k;
for(k = 0; k < n; k++)
{
    var s = 0;

    // Count the number of element
    // less than current element
    // in arr[k]
    for(i = 0; i < n; i++)
    {
        if (arr[i] < arr[k])
            s += 1 ;
    }
    // Here s = number of node in left
    // BST and (n-s-1) = number of node
    // in right BST
    // Find number of BST using elements
    // in left BST
    var catalan_leftBST = catalan(s) ;

    // Find number of BST using elements
    // in right BST
    var catalan_rightBST = catalan(n - s - 1) ;

    // Find total number of BST
    var totalBST = catalan_rightBST * catalan_leftBST ;

    // Print total BST count
    document.write( totalBST + " ");
}

</script>
```

**Output:** 

```
14 5 4 5 14
```

**时间复杂度:** O(N <sup>2</sup> )