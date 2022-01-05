# 重新排列前 N 个数字，使其处于 K 距离

> 原文:[https://www . geesforgeks . org/relay-first-n-numbers-make-k-distance/](https://www.geeksforgeeks.org/rearrange-first-n-numbers-make-k-distance/)

给定一个正数 K，我们需要对前 N 个自然数进行置换，使得每个置换数与其原始位置的绝对距离为 K，如果不能以这种方式重新排列它们，则打印是不可能的。
**例:**

```
Input  :  N = 12   
          K = 2
Output : [3 4 1 2 7 8 5 6 11 12 9 10]
Explanation : Initial permutation is
[1 2 3 4 5 6 7 8 9 10 11 12]
In rearrangement, [3 4 1 2 7 8 5 6 11
12 9 10] we have all elements at
distance 2\. 

Input  :  N = 12   
          K = 3
Output : [4 5 6 1 2 3 10 11 12 7 8 9]
```

我们可以通过在解决方案中找到模式来解决这个问题。如果我们手动遍历很多解，可以看到如果把 N 个数分割成大小为 2K 的槽，那么每个槽都可以重新排列成大小为 K 的两部分，其中位置与实际位置的差将是 K。

```
Example 1 : N = 12 and K = 2

First 12 numbers are partitioned into 
2*2 = 4 sized 12/4 = 3 slots as shown below,
[[1 2 3 4] [5 6 7 8] [9 10 11 12]]

Now each half of the slot is swapped so that, 
every number will go at K position distance 
from its initial position as shown below,
[[3 4 1 2] [7 8 5 6] [11 12 9 10]]

Example 2 :  N = 12 and K = 3,
[1 2 3 4 5 6 7 8 9 10 11 12]
[[1 2 3 4 5 6] [7 8 9 10 11 12]]
[[4 5 6 1 2 3] [10 11 12 7 8 9]]
[4 5 6 1 2 3 10 11 12 7 8 9]
Which is the final rearrangement for 
N = 12 and K = 3
```

在下面的代码中，K = 0 的情况通过按实际顺序打印所有数字来单独处理。当 N 不能被 2K 整除时，直接打印“不可能”。

## C++

```
// C++ program to rearrange permutations to make
// them K distance away
#include <bits/stdc++.h>
using namespace std;

/* Method prints permutation of first N numbers,
where each number is K distance away from its
actual position */
void printRearrangeNnumberForKDistance(int N, int K)
{
    // If K = 0, then print numbers in their natural
    // order
    if (K == 0)
    {
        for (int i = 1; i <= N; i++)
            cout << i << " ";
        cout << endl;
        return;
    }

    // If N doesn't divide (2K) evenly, then
    // rearrangement is not possible
    if (N % (2 * K) != 0)
    {
        cout << "Not Possible\n";
        return;
    }

    // Copy first N numbers to an auxiliary
    // array
    int arr[N + 1];
    for (int i = 1; i <= N; i++)
        arr[i] = i;

    // Swap halves of each 2K sized slot
    for (int i = 1; i <= N; i += 2 * K)
        for (int j = 1; j <= K; j++)
            swap(arr[i + j - 1], arr[K + i + j - 1]);

    // Print the rearranged array
    for (int i = 1; i <= N; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int N = 12, K = 3;
    printRearrangeNnumberForKDistance(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange permutations
// to make them K distance away

class GFG
{
    /* Method prints permutation of first N numbers,
    where each number is K distance away from its
    actual position */
    static void printRearrangeNnumberForKDistance(int N, int K)
    {
        // If K = 0, then print numbers
        // in their natural order
        if (K == 0)
        {
            for (int i = 1; i <= N; i++)
                System.out.print(i + " ");
            System.out.println();
            return;
        }

        // If N doesn't divide (2K) evenly, then
        // rearrangement is not possible
        if (N % (2 * K) != 0)
        {
            System.out.print("Not Possible\n");
            return;
        }

        // Copy first N numbers to an auxiliary
        // array
        int arr[]=new int[N + 1];
        for (int i = 1; i <= N; i++)
            arr[i] = i;

        // Swap halves of each 2K sized slot
        for (int i = 1; i <= N; i += 2 * K)
            for (int j = 1; j <= K; j++)
            {
                int temp = arr[i + j - 1];
                arr[i + j - 1] = arr[K + i + j - 1];
                arr[K + i + j - 1] = temp;
            }

        // Print the rearranged array
        for (int i = 1; i <= N; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 12, K = 3;
        printRearrangeNnumberForKDistance(N, K);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to rearrange
# permutations to make them
# K distance away

'''
 * Method prints permutation of
 first N numbers, where each number
 is K distance * away from its actual
 position
 '''
def printRearrangeNnumberForKDistance(N, K):

    # If K = 0, then prnumbers
    # in their natural order
    if (K == 0):
        for i in range(1, N + 1):
            print(i, end = " ");
        print();
        return;

    # If N doesn't divide (2K) evenly,
    # then rearrangement is not possible
    if (N % (2 * K) != 0):
        print("Not Possible");
        return;

    # Copy first N numbers to an
    # auxiliary array
    arr = [0] * (N + 1);

    for i in range(1, N + 1):
        arr[i] = i;

    # Swap halves of each 2K
    # sized slot
    for i in range(1, N + 1,
                   2 * K):
        for j in range(1, K + 1):
            temp = arr[i + j - 1];
            arr[i + j - 1] = arr[K + i + j - 1];
            arr[K + i + j - 1] = temp;

    # Print rearranged array
    for i in range(1, N + 1):
        print(arr[i], end = " ");

# Driver code
if __name__ == '__main__':

    N = 12;
    K = 3;
    printRearrangeNnumberForKDistance(N, K);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to rearrange permutations
// to make them K distance away
using System;

class GFG
{
    /* Method prints permutation of first N numbers,
    where each number is K distance away from its
    actual position */
    static void printRearrangeNnumberForKDistance(int N, int K)
    {
        // If K = 0, then print numbers
        // in their natural order
        if (K == 0)
        {
            for (int i = 1; i <= N; i++)
            Console.Write(i + " ");
            Console.WriteLine();
            return;
        }

        // If N doesn't divide (2K) evenly, then
        // rearrangement is not possible
        if (N % (2 * K) != 0)
        {
            Console.Write("Not Possible\n");
            return;
        }

        // Copy first N numbers to an auxiliary
        // array
        int []arr=new int[N + 1];
        for (int i = 1; i <= N; i++)
            arr[i] = i;

        // Swap halves of each 2K sized slot
        for (int i = 1; i <= N; i += 2 * K)
            for (int j = 1; j <= K; j++)
            {
                int temp = arr[i + j - 1];
                arr[i + j - 1] = arr[K + i + j - 1];
                arr[K + i + j - 1] = temp;
            }

        // Print the rearranged array
        for (int i = 1; i <= N; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main ()
    {
        int N = 12, K = 3;
        printRearrangeNnumberForKDistance(N, K);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    /* Method prints permutation of first N numbers,
    where each number is K distance away from its
    actual position */
    function printRearrangeNnumberForKDistance(N, K)
    {
        // If K = 0, then print numbers
        // in their natural order
        if (K == 0)
        {
            for (let i = 1; i <= N; i++)
                document.write(i + " ");
            document.write("<br/>");
            return;
        }

        // If N doesn't divide (2K) evenly, then
        // rearrangement is not possible
        if (N % (2 * K) != 0)
        {
            document.write("Not Possible\n");
            return;
        }

        // Copy first N numbers to an auxiliary
        // array
        let arr = [];
        for (let i = 1; i <= N; i++)
            arr[i] = i;

        // Swap halves of each 2K sized slot
        for (let i = 1; i <= N; i += 2 * K)
            for (let j = 1; j <= K; j++)
            {
                let temp = arr[i + j - 1];
                arr[i + j - 1] = arr[K + i + j - 1];
                arr[K + i + j - 1] = temp;
            }

        // Print the rearranged array
        for (let i = 1; i <= N; i++)
            document.write(arr[i] + " ");
    }

// Driver Code
    let N = 12, K = 3;
    printRearrangeNnumberForKDistance(N, K);

</script>
```

**输出:**

```
4 5 6 1 2 3 10 11 12 7 8 9
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。