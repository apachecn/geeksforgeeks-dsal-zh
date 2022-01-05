# 完全二叉树的数量，使得每个节点都是其子节点的乘积

> 原文:[https://www . geesforgeks . org/number-full-binary-trees-node-product-children/](https://www.geeksforgeeks.org/number-full-binary-trees-node-product-children/)

给定一组 **n 个**整数，每个整数都大于 1。任务是从给定的整数中找到[全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)的个数，使得每个非节点叶节点值都是其子节点值的乘积。考虑到这一点，每个整数都可以在一个完整的二叉树中多次使用。

示例:

```
Input : arr[] = { 2, 3, 4, 6 }.
Output : 7
There can be 7 full binary tree with the given product property.

// Four trees with single nodes
2  3  4  6

// Three trees with three nodes
  4   ,
 / \
2   2

  6    ,
 / \
2   3

  6
 / \
3   2  
```

我们找到给定数组中的最大值，并创建一个数组来存储该数组中元素的存在。其思想是，对于每个小于数组最大值的整数的所有倍数，如果数组中存在该倍数，则尝试生成完整的二叉树。
观察任何给定属性的全二叉树，较小的值总是在最后一级。所以，试着从数组的最小值到数组的最大值找到这样的全二叉树的个数。
解决问题的算法:
1。为每个元素初始化这种全二叉树的可能数目等于 1。既然单个节点也有助于回答。
2。对于数组的每个元素，arr[i]，从数组的最小值到最大值。
……a)对于 arr[i]的每个倍数，找出倍数是否存在。
……b)如果是，那么 arr[i]的倍数的这种可能的全二叉树的数目，比如 m，等于 arr[i]的这种可能的全二叉树的数目和 arr[i]/m 的这种可能的全二叉树的数目的乘积

## C++

```
// C++ program to find number of full binary tree
// such that each node is product of its children.
#include<bits/stdc++.h>
using namespace std;

// Return the number of all possible full binary
// tree with given product property.
int numoffbt(int arr[], int n)
{
    // Finding the minimum and maximum values in
    // given array.
    int maxvalue = INT_MIN, minvalue = INT_MAX;
    for (int i = 0; i < n; i++)
    {
        maxvalue = max(maxvalue, arr[i]);
        minvalue = min(minvalue, arr[i]);
    }

    int mark[maxvalue + 2];
    int value[maxvalue + 2];
    memset(mark, 0, sizeof(mark));
    memset(value, 0, sizeof(value));

    // Marking the presence of each array element
    // and initialising the number of possible
    // full binary tree for each integer equal
    // to 1 because single node will also
    // contribute as a full binary tree.
    for (int i = 0; i < n; i++)
    {
        mark[arr[i]] = 1;
        value[arr[i]] = 1;
    }

    // From minimum value to maximum value of array
    // finding the number of all possible Full
    // Binary Trees.
    int ans = 0;
    for (int i = minvalue; i <= maxvalue; i++)
    {
        // Find if value present in the array
        if (mark[i])
        {
            // For each multiple of i, less than
            // equal to maximum value of array
            for (int j = i + i;
                 j <= maxvalue && j/i <= i; j += i)
            {
                // If multiple is not present in the
                // array then continue.
                if (!mark[j])
                    continue;

                // Finding the number of possible Full
                // binary trees for multiple j by
                // multiplying number of possible Full
                // binary tree from the number i and
                // number of possible Full binary tree
                // from i/j.
                value[j] = value[j] + (value[i] * value[j/i]);

                // Condition for possibility when left
                // child became right child and vice versa.
                if (i != j/i)
                    value[j] = value[j] + (value[i] * value[j/i]);
            }
        }

        ans += value[i];
    }

    return ans;
}

// Driven Program
int main()
{
    int arr[] = { 2, 3, 4, 6 };
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << numoffbt(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of full
// binary tree such that each node is
// product of its children.
import java.util.Arrays;

class GFG {

    // Return the number of all possible
    // full binary tree with given product
    // property.
    static int numoffbt(int arr[], int n)
    {

        // Finding the minimum and maximum
        // values in given array.
        int maxvalue = -2147483647;
        int minvalue = 2147483647;
        for (int i = 0; i < n; i++)
        {
            maxvalue = Math.max(maxvalue, arr[i]);
            minvalue = Math.min(minvalue, arr[i]);
        }

        int mark[] = new int[maxvalue + 2];
        int value[] = new int[maxvalue + 2];
        Arrays.fill(mark, 0);
        Arrays.fill(value, 0);

        // Marking the presence of each array element
        // and initialising the number of possible
        // full binary tree for each integer equal
        // to 1 because single node will also
        // contribute as a full binary tree.
        for (int i = 0; i < n; i++)
        {
            mark[arr[i]] = 1;
            value[arr[i]] = 1;
        }

        // From minimum value to maximum value of array
        // finding the number of all possible Full
        // Binary Trees.
        int ans = 0;
        for (int i = minvalue; i <= maxvalue; i++)
        {

            // Find if value present in the array
            if (mark[i] != 0)
            {
                // For each multiple of i, less than
                // equal to maximum value of array
                for (int j = i + i;
                    j <= maxvalue && j/i <= i; j += i)
                {
                    // If multiple is not present in
                    // the array then continue.
                    if (mark[j] == 0)
                        continue;

                    // Finding the number of possible
                    // Full binary trees for multiple
                    // j by multiplying number of
                    // possible Full binary tree from
                    // the number i and number of
                    // possible Full binary tree from i/j.
                    value[j] = value[j] + (value[i]
                                          * value[j/i]);

                    // Condition for possibility when
                    // left child became right child
                    // and vice versa.
                    if (i != j / i)
                        value[j] = value[j] + (value[i]
                                         * value[j/i]);
                }
            }

            ans += value[i];
        }

        return ans;
    }

    //driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 3, 4, 6 };
        int n = arr.length;

        System.out.print(numoffbt(arr, n));
    }
}

//This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find number of
# full binary tree such that each node
# is product of its children.

# Return the number of all possible full
# binary tree with given product property.
def numoffbt(arr, n):

    # Finding the minimum and maximum
    # values in given array.
    maxvalue = -2147483647
    minvalue = 2147483647
    for i in range(n):

        maxvalue = max(maxvalue, arr[i])
        minvalue = min(minvalue, arr[i])

    mark = [0 for i in range(maxvalue + 2)]
    value = [0 for i in range(maxvalue + 2)]

    # Marking the presence of each array element
    # and initialising the number of possible
    # full binary tree for each integer equal
    # to 1 because single node will also
    # contribute as a full binary tree.
    for i in range(n):

        mark[arr[i]] = 1
        value[arr[i]] = 1

    # From minimum value to maximum value
    # of array finding the number of all
    # possible Full Binary Trees.
    ans = 0
    for i in range(minvalue, maxvalue + 1):

        # Find if value present in the array
        if (mark[i] != 0):

            # For each multiple of i, less than
            # equal to maximum value of array
            j = i + i
            while(j <= maxvalue and j // i <= i):

                # If multiple is not present in the
                # array then continue.
                if (mark[j] == 0):
                    continue

                # Finding the number of possible Full
                # binary trees for multiple j by
                # multiplying number of possible Full
                # binary tree from the number i and
                # number of possible Full binary tree
                # from i/j.
                value[j] = value[j] + (value[i] * value[j // i])

                # Condition for possibility when left
                # child became right child and vice versa.
                if (i != j // i):
                    value[j] = value[j] + (value[i] * value[j // i])
                j += i        

        ans += value[i]

    return ans

# Driver Code
arr = [ 2, 3, 4, 6 ]
n = len(arr)

print(numoffbt(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find number of
// full binary tree such that each
// node is product of its children.
using System;

class GFG
{
    // Return the number of all possible full binary
    // tree with given product property.
    static int numoffbt(int []arr, int n)
    {
        // Finding the minimum and maximum values in
        // given array.
        int maxvalue = -2147483647, minvalue = 2147483647;
        for (int i = 0; i < n; i++)
        {
            maxvalue = Math.Max(maxvalue, arr[i]);
            minvalue = Math.Min(minvalue, arr[i]);
        }

        int []mark=new int[maxvalue + 2];
        int []value=new int[maxvalue + 2];
        for(int i = 0;i < maxvalue + 2; i++)
            {
                mark[i]=0;
                value[i]=0;
            }

        // Marking the presence of each array element
        // and initialising the number of possible
        // full binary tree for each integer equal
        // to 1 because single node will also
        // contribute as a full binary tree.
        for (int i = 0; i < n; i++)
        {
            mark[arr[i]] = 1;
            value[arr[i]] = 1;
        }

        // From minimum value to maximum value of array
        // finding the number of all possible Full
        // Binary Trees.
        int ans = 0;
        for (int i = minvalue; i <= maxvalue; i++)
        {
            // Find if value present in the array
            if (mark[i] != 0)
            {
                // For each multiple of i, less than
                // equal to maximum value of array
                for (int j = i + i;
                     j <= maxvalue && j/i <= i; j += i)
                {
                    // If multiple is not present in the
                    // array then continue.
                    if (mark[j] == 0)
                        continue;

                    // Finding the number of possible Full
                    // binary trees for multiple j by
                    // multiplying number of possible Full
                    // binary tree from the number i and
                    // number of possible Full binary tree
                    // from i/j.
                    value[j] = value[j] + (value[i] * value[j/i]);

                    // Condition for possibility when left
                    // child became right child and vice versa.
                    if (i != j/i)
                        value[j] = value[j] + (value[i] * value[j/i]);
                }
            }

            ans += value[i];
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 3, 4, 6 };
        int n = arr.Length;

        Console.Write(numoffbt(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## java 描述语言

```
<script>
// Javascript program to find number of full binary tree
// such that each node is product of its children.

// Return the number of all possible full binary
// tree with given product property.
function numoffbt(arr, n) {
    // Finding the minimum and maximum values in
    // given array.
    let maxvalue = Number.MIN_SAFE_INTEGER, minvalue = Number.MAX_SAFE_INTEGER;
    for (let i = 0; i < n; i++) {
        maxvalue = Math.max(maxvalue, arr[i]);
        minvalue = Math.min(minvalue, arr[i]);
    }

    let mark = new Array(maxvalue + 2).fill(0);
    let value = new Array(maxvalue + 2).fill(0);

    // Marking the presence of each array element
    // and initialising the number of possible
    // full binary tree for each integer equal
    // to 1 because single node will also
    // contribute as a full binary tree.
    for (let i = 0; i < n; i++) {
        mark[arr[i]] = 1;
        value[arr[i]] = 1;
    }

    // From minimum value to maximum value of array
    // finding the number of all possible Full
    // Binary Trees.
    let ans = 0;
    for (let i = minvalue; i <= maxvalue; i++) {
        // Find if value present in the array
        if (mark[i]) {
            // For each multiple of i, less than
            // equal to maximum value of array
            for (let j = i + i;
                j <= maxvalue && j / i <= i; j += i) {
                // If multiple is not present in the
                // array then continue.
                if (!mark[j])
                    continue;

                // Finding the number of possible Full
                // binary trees for multiple j by
                // multiplying number of possible Full
                // binary tree from the number i and
                // number of possible Full binary tree
                // from i/j.
                value[j] = value[j] + (value[i] * value[j / i]);

                // Condition for possibility when left
                // child became right child and vice versa.
                if (i != j / i)
                    value[j] = value[j] + (value[i] * value[j / i]);
            }
        }

        ans += value[i];
    }

    return ans;
}

// Driven Program
let arr = [2, 3, 4, 6];
let n = arr.length;
document.write(numoffbt(arr, n) + "<br>");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
7
```

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。