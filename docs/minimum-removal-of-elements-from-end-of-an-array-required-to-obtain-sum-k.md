# 从数组末尾移除元素的最少次数，以获得总和 K

> 原文:[https://www . geeksforgeeks . org/从数组末尾移除最少元素-需要获取总和-k/](https://www.geeksforgeeks.org/minimum-removal-of-elements-from-end-of-an-array-required-to-obtain-sum-k/)

给定一个整数 **K** 和一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是用最少的操作数创建一个和 **K** 的新数组，其中在每个操作中，一个元素可以从**A【】**的开始或结束处移除并追加到新数组中。如果无法用总和 **K** 生成新数组，则打印 **-1** 。如果有多个答案，打印任意一个。

**示例**

> **输入:** K = 6，A[] = {1，2，3，1，3}，N = 5
> **输出:** 1 3 2
> **说明:**操作 1:移除 A[0]将 A[]修改为{2，3，1，3}。总和= 1。
> 操作 2:移除 A[3]将 A[]修改为{2，1，3}。总和= 4。
> 操作 3:移除 A[0]会将 A[]修改为{1，3}。总和= 6。
> 
> **输入:** K = 5，A[] = {1，2，7}，N = 3
> T3】输出: -1

**天真方法:**按照以下步骤解决问题:

1.  任务是找到两个最小长度的子阵列，一个从阵列的开始，一个从阵列的结束(可能是空的)，这样它们的和等于 **K** 。
2.  [从左侧遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并计算需要从右侧移除的子数组，使得总和为 **K** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// elements required to be removed from
// the ends of an array to obtain a sum K
int minSizeArr(int A[], int N, int K)
{
    // Number of elements removed from the
    // left and right ends of the array
    int leftTaken = N, rightTaken = N;

    // Sum of left and right subarrays
    int leftSum = 0, rightSum = 0;

    // No element is taken from left initially
    for (int left = -1; left < N; left++) {

        if (left != -1)
            leftSum += A[left];

        rightSum = 0;

        // Start taking elements from right side
        for (int right = N - 1; right > left; right--) {

            rightSum += A[right];

            if (leftSum + rightSum == K) {

                // (left + 1): Count of elements
                // removed from the left
                // (N-right): Count of elements
                // removed from the right
                if (leftTaken + rightTaken
                    > (left + 1) + (N - right)) {

                    leftTaken = left + 1;
                    rightTaken = N - right;
                }
                break;
            }
            // If sum is greater than K
            if (leftSum + rightSum > K)
                break;
        }
    }

    if (leftTaken + rightTaken <= N) {

        for (int i = 0; i < leftTaken; i++)
            cout << A[i] << " ";
        for (int i = 0; i < rightTaken; i++)
            cout << A[N - i - 1] << " ";
    }

    // If it is not possible to obtain sum K
    else
        cout << -1;
}

// Driver Code
int main()
{
    int N = 7;

    // Given Array
    int A[] = { 3, 2, 1, 1, 1, 1, 3 };

    // Given target sum
    int K = 10;

    minSizeArr(A, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the minimum number of
// elements required to be removed from
// the ends of an array to obtain a sum K
static void minSizeArr(int A[], int N, int K)
{
    // Number of elements removed from the
    // left and right ends of the array
    int leftTaken = N, rightTaken = N;

    // Sum of left and right subarrays
    int leftSum = 0, rightSum = 0;

    // No element is taken from left initially
    for (int left = -1; left < N; left++) {

        if (left != -1)
            leftSum += A[left];

        rightSum = 0;

        // Start taking elements from right side
        for (int right = N - 1; right > left; right--)
        {

            rightSum += A[right];

            if (leftSum + rightSum == K) {

                // (left + 1): Count of elements
                // removed from the left
                // (N-right): Count of elements
                // removed from the right
                if (leftTaken + rightTaken
                    > (left + 1) + (N - right)) {

                    leftTaken = left + 1;
                    rightTaken = N - right;
                }
                break;
            }
            // If sum is greater than K
            if (leftSum + rightSum > K)
                break;
        }
    }

    if (leftTaken + rightTaken <= N) {

        for (int i = 0; i < leftTaken; i++)
            System.out.print( A[i] + " ");
        for (int i = 0; i < rightTaken; i++)
            System.out.print(A[N - i - 1] + " ");
    }

    // If it is not possible to obtain sum K
    else
        System.out.print(-1);
}

// Driver code
public static void main(String[] args)
{
    int N = 7;

    // Given Array
    int A[] = { 3, 2, 1, 1, 1, 1, 3 };

    // Given target sum
    int K = 10;

    minSizeArr(A, N, K);
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number of
# elements required to be removed from
# the ends of an array to obtain a sum K
def minSizeArr(A, N, K):

    # Number of elements removed from the
    # left and right ends of the array
    leftTaken = N
    rightTaken = N

    # Sum of left and right subarrays
    leftSum = 0
    rightSum = 0

    # No element is taken from left initially
    for left in range(-1, N):
        if (left != -1):
            leftSum += A[left]

        rightSum = 0

        # Start taking elements from right side
        for right in range(N - 1, left, -1):
            rightSum += A[right]

            if (leftSum + rightSum == K):

                # (left + 1): Count of elements
                # removed from the left
                # (N-right): Count of elements
                # removed from the right
                if (leftTaken + rightTaken >
                   (left + 1) + (N - right)):
                    leftTaken = left + 1
                    rightTaken = N - right

                break

            # If sum is greater than K
            if (leftSum + rightSum > K):
                break

    if (leftTaken + rightTaken <= N):
        for i in range(leftTaken):
            print(A[i], end = " ")

        for i in range(rightTaken):
            print(A[N - i - 1], end = " ")

    # If it is not possible to obtain sum K
    else:
        print(-1)

# Driver Code
if __name__ == "__main__":

    N = 7

    # Given Array
    A = [ 3, 2, 1, 1, 1, 1, 3 ]

    # Given target sum
    K = 10

    minSizeArr(A, N, K)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to find the smallest
// array that can be removed from
// the ends of an array to obtain sum K
static void minSizeArr(int[] A, int N, int K)
{

    // Number of elements removed from the
    // left and right ends of the array
    int leftTaken = N, rightTaken = N;

    // Sum of left and right subarrays
    int leftSum = 0, rightSum = 0;

    // No element is taken from left initially
    for (int left = -1; left < N; left++) {

        if (left != -1)
            leftSum += A[left];

        rightSum = 0;

        // Start taking elements from right side
        for (int right = N - 1; right > left; right--)
        {

            rightSum += A[right];

            if (leftSum + rightSum == K) {

                // (left + 1): Count of elements
                // removed from the left
                // (N-right): Count of elements
                // removed from the right
                if (leftTaken + rightTaken
                    > (left + 1) + (N - right)) {

                    leftTaken = left + 1;
                    rightTaken = N - right;
                }
                break;
            }
            // If sum is greater than K
            if (leftSum + rightSum > K)
                break;
        }
    }

    if (leftTaken + rightTaken <= N) {

        for (int i = 0; i < leftTaken; i++)
            Console.Write( A[i] + " ");
        for (int i = 0; i < rightTaken; i++)
            Console.Write(A[N - i - 1] + " ");
    }

    // If it is not possible to obtain sum K
    else
        Console.Write(-1);
}

    // Driver Code
    public static void Main()
    {
        int N = 7;

    // Given Array
    int[] A = { 3, 2, 1, 1, 1, 1, 3 };

    // Given target sum
    int K = 10;

    minSizeArr(A, N, K);
    }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum number of
// elements required to be removed from
// the ends of an array to obtain a sum K
function minSizeArr(A, N, K)
{
    // Number of elements removed from the
    // left and right ends of the array
    let leftTaken = N, rightTaken = N;

    // Sum of left and right subarrays
    let leftSum = 0, rightSum = 0;

    // No element is taken from left initially
    for (let left = -1; left < N; left++) {

        if (left != -1)
            leftSum += A[left];

        rightSum = 0;

        // Start taking elements from right side
        for (let right = N - 1; right > left; right--)
        {

            rightSum += A[right];

            if (leftSum + rightSum == K) {

                // (left + 1): Count of elements
                // removed from the left
                // (N-right): Count of elements
                // removed from the right
                if (leftTaken + rightTaken
                    > (left + 1) + (N - right)) {

                    leftTaken = left + 1;
                    rightTaken = N - right;
                }
                break;
            }
            // If sum is greater than K
            if (leftSum + rightSum > K)
                break;
        }
    }

    if (leftTaken + rightTaken <= N) {

        for (let i = 0; i < leftTaken; i++)
            document.write( A[i] + " ");
        for (let i = 0; i < rightTaken; i++)
            document.write(A[N - i - 1] + " ");
    }

    // If it is not possible to obtain sum K
    else
        document.write(-1);
}

// Driver code
    let N = 7;

    // Given Array
    let A = [ 3, 2, 1, 1, 1, 1, 3 ];

    // Given target sum
    let K = 10;

    minSizeArr(A, N, K);

// This code is contributed by souraavghosh0416.
</script>
```

**Output:** 

```
3 2 3 1 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

1.  计算数组**【A】**元素的[和并存储在变量中，比如 **Total** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
2.  问题可以看作是用总和 **(总–K)找到[最大尺寸子阵。](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)**
3.  剩下的元素加起来就是 **K** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// array that can be removed from
// the ends of an array to obtain sum K
void minSizeArr(int A[], int N, int K)
{
    int sum = 0;
    // Sum of complete array
    for (int i = 0; i < N; i++)
        sum += A[i];

    // If given number is greater
    // than sum of the array
    if (K > sum) {
        cout << -1;
        return;
    }

    // If number is equal to
    // the sum of array
    if (K == sum) {
        for (int i = 0; i < N; i++) {
            cout << A[i] << " ";
        }
        return;
    }

    // tar is sum of middle subarray
    int tar = sum - K;

    // Find the longest subarray
    // with sum equal to tar
    unordered_map<int, int> um;
    um[0] = -1;

    int left, right;
    int cur = 0, maxi = -1;
    for (int i = 0; i < N; i++) {
        cur += A[i];
        if (um.find(cur - tar) != um.end()
            && i - um[cur - tar] > maxi) {
            maxi = i - um[cur - tar];
            right = i;
            left = um[cur - tar];
        }
        if (um.find(cur) == um.end())
            um[cur] = i;
    }

    // If there is no subarray with
    // sum equal to tar
    if (maxi == -1)
        cout << -1;

    else {
        for (int i = 0; i <= left; i++)
            cout << A[i] << " ";
        for (int i = 0; i < right; i++)
            cout << A[N - i - 1] << " ";
    }
}

// Driver Code
int main()
{
    int N = 7;

    // Given Array
    int A[] = { 3, 2, 1, 1, 1, 1, 3 };

    // Given target sum
    int K = 10;

    minSizeArr(A, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

      // Function to find the smallest
// array that can be removed from
// the ends of an array to obtain sum K
static void minSizeArr(int A[], int N, int K)
{
    int sum = 0;

    // Sum of complete array
    for (int i = 0; i < N; i++)
        sum += A[i];

    // If given number is greater
    // than sum of the array
    if (K > sum) {
        System.out.print(-1);
        return;
    }

    // If number is equal to
    // the sum of array
    if (K == sum) {
        for (int i = 0; i < N; i++) {
            System.out.print(A[i] + " ");
        }
        return;
    }

    // tar is sum of middle subarray
    int tar = sum - K;

    // Find the longest subarray
    // with sum equal to tar
    HashMap<Integer, Integer> um = new HashMap<Integer, Integer>();
     um.put(0, -1);

    int left = 0, right = 0;
    int cur = 0, maxi = -1;
    for (int i = 0; i < N; i++) {
        cur += A[i];
        if (um.containsKey(cur - tar)
            && i - um.get(cur - tar) > maxi) {
            maxi = i - um.get(cur - tar);
            right = i;
            left = um.get(cur - tar);
        }
        if (!um.containsKey(cur))
            um.put(cur, i);
    }

    // If there is no subarray with
    // sum equal to tar
    if (maxi == -1)
        System.out.println(-1);

    else {
        for (int i = 0; i <= left; i++)
            System.out.print(A[i] + " ");
        for (int i = 0; i < right; i++)
            System.out.print(A[N - i - 1] + " ");
    }
}

// Driver Code
    public static void main (String[] args) {
        int N = 7;

    // Given Array
    int A[] = { 3, 2, 1, 1, 1, 1, 3 };

    // Given target sum
    int K = 10;

    minSizeArr(A, N, K);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find the smallest
# array that can be removed from
# the ends of an array to obtain sum K
def minSizeArr(A, N, K):
    sum = 0

    # Sum of complete array
    for i in range(N):
        sum += A[i]

    # If given number is greater
    # than sum of the array
    if (K > sum):
        print(-1);
        return

    # If number is equal to
    # the sum of array
    if (K == sum):
        for i in range(N):
            print(A[i],end = " ")
        return

    # tar is sum of middle subarray
    tar = sum - K

    # Find the longest subarray
    # with sum equal to tar
    um = {}
    um[0] = -1

    left = 0
    right = 0
    cur = 0
    maxi = -1
    for i in range(N):
        cur += A[i]
        if((cur - tar) in um and (i - um[cur - tar]) > maxi):
            maxi = i - um[cur - tar]
            right = i
            left = um[cur - tar]
        if(cur not in um):
            um[cur] = i

    # If there is no subarray with
    # sum equal to tar
    if (maxi == -1):
        print(-1)

    else:
        for i in range(left+1):
            print(A[i], end = " ")
        for i in range(right):
            print(A[N - i - 1], end = " ")

# Driver Code
if __name__ == '__main__':
    N = 7

    # Given Array
    A = [3, 2, 1, 1, 1, 1, 3]

    # Given target sum
    K = 10
    minSizeArr(A, N, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function to find the smallest
// array that can be removed from
// the ends of an array to obtain sum K
static void minSizeArr(int[] A, int N, int K)
{
    int sum = 0;

    // Sum of complete array
    for(int i = 0; i < N; i++)
        sum += A[i];

    // If given number is greater
    // than sum of the array
    if (K > sum)
    {
        Console.WriteLine(-1);
        return;
    }

    // If number is equal to
    // the sum of array
    if (K == sum)
    {
        for(int i = 0; i < N; i++)
        {
           Console.Write(A[i] + " ");
        }
        return;
    }

    // tar is sum of middle subarray
    int tar = sum - K;

    // Find the longest subarray
    // with sum equal to tar
    Dictionary<int,
               int> um =  new Dictionary<int,
                                         int>();
     um[0] = -1;

    int left = 0, right = 0;
    int cur = 0, maxi = -1;
    for(int i = 0; i < N; i++)
    {
        cur += A[i];
        if (um.ContainsKey(cur - tar) &&
             i - um[cur - tar] > maxi)
        {
            maxi = i - um[cur - tar];
            right = i;
            left = um[cur - tar];
        }
        if (!um.ContainsKey(cur))
            um[cur] = i;
    }

    // If there is no subarray with
    // sum equal to tar
    if (maxi == -1)
        Console.Write(-1);

    else
    {
        for(int i = 0; i <= left; i++)
            Console.Write(A[i] + " ");
        for(int i = 0; i < right; i++)
            Console.Write(A[N - i - 1] + " ");
    }
}  

// Driver code
static public void Main()
{
    int N = 7;

    // Given Array
    int[] A = { 3, 2, 1, 1, 1, 1, 3 };

    // Given target sum
    int K = 10;

    minSizeArr(A, N, K);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the smallest
// array that can be removed from
// the ends of an array to obtain sum K
function minSizeArr(A, N, K)
{
    var sum = 0;
    var i;
    // Sum of complete array
    for (i = 0; i < N; i++)
        sum += A[i];

    // If given number is greater
    // than sum of the array
    if (K > sum) {
        cout << -1;
        return;
    }

    // If number is equal to
    // the sum of array
    if (K == sum) {
        for (i = 0; i < N; i++) {
            document.write(A[i]+' ');
        }
        return;
    }

    // tar is sum of middle subarray
    var tar = sum - K;

    // Find the longest subarray
    // with sum equal to tar
    var um = new Map();
    um[0] = -1;

    var left, right;
    var cur = 0, maxi = -1;
    for (i = 0; i < N; i++) {
        cur += A[i];
        if (um.has(cur - tar)
            && i - um.get(cur - tar) > maxi) {
            maxi = i - um.get(cur - tar);
            right = i;
            left = um.get(cur - tar);
        }
        if (!um.has(cur))
            um.set(cur,i);
    }

    // If there is no subarray with
    // sum equal to tar
    if (maxi == -1)
        cout << -1;

    else {
        for (i = 0; i <= left; i++)
            document.write(A[i]+' ');
        for (i = 0; i < right; i++)
            document.write(A[N - i - 1]+ ' ');
    }
}

// Driver Code

    var N = 7;

    // Given Array
    var A = [3, 2, 1, 1, 1, 1, 3];

    // Given target sum
    var K = 10;

    minSizeArr(A, N, K);

</script>
```

**Output:** 

```
3 2 3 1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)