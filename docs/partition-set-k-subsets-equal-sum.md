# 将一个集合划分为 K 个和相等的子集

> 原文:[https://www . geesforgeks . org/partition-set-k-subsets-equal-sum/](https://www.geeksforgeeks.org/partition-set-k-subsets-equal-sum/)

给定一个由 N 个元素组成的整数数组，任务是将这个数组分成 K 个非空子集，使得每个子集的元素之和相同。这个数组的所有元素都应该是一个分区的一部分。
**例:**

```
Input : arr = [2, 1, 4, 5, 6], K = 3
Output : Yes
we can divide above array into 3 parts with equal
sum as [[2, 4], [1, 5], [6]]

Input  : arr = [2, 1, 5, 5, 6], K = 3
Output : No
It is not possible to divide above array into 3
parts with equal sum

```

我们可以递归地解决这个问题，我们为每个分区的和保留一个数组，并保留一个布尔数组来检查某个元素是否已经进入某个分区。
首先我们需要检查一些基本情况，
如果 K 为 1，那么我们已经有了答案，完全数组只是和相同的子集。
如果 N < K，那么就不可能把数组分成和相等的子集，因为我们不能把数组分成 N 个以上的部分。
如果数组的和不能被 K 整除，那么就不可能对数组进行除。只有 k 除和，我们才会继续。我们的目标是将数组分成 K 个部分，每个部分的和应该是 array_sum/K
在下面的代码中，编写了一个递归方法，试图将数组元素添加到某个子集。如果这个子集的和达到要求的和，我们递归地迭代下一部分，否则我们回溯不同的元素集。如果其和达到所需和的子集的数量是(K-1)，我们标记有可能将数组划分为具有相等和的 K 个部分，因为剩余元素已经具有等于所需和的和。

## C++

```
// C++ program to check whether an array can be
// partitioned into K subsets of equal sum
#include <bits/stdc++.h>
using namespace std;

// Recursive Utility method to check K equal sum
// subsetition of array
/**
    array           - given input array
    subsetSum array   - sum to store each subset of the array
    taken           - boolean array to check whether element
                      is taken into sum partition or not
    K               - number of partitions needed
    N               - total number of element in array
    curIdx          - current subsetSum index
    limitIdx        - lastIdx from where array element should
                      be taken */
bool isKPartitionPossibleRec(int arr[], int subsetSum[], bool taken[],
                   int subset, int K, int N, int curIdx, int limitIdx)
{
    if (subsetSum[curIdx] == subset)
    {
        /*  current index (K - 2) represents (K - 1) subsets of equal
            sum last partition will already remain with sum 'subset'*/
        if (curIdx == K - 2)
            return true;

        //  recursive call for next subsetition
        return isKPartitionPossibleRec(arr, subsetSum, taken, subset,
                                            K, N, curIdx + 1, N - 1);
    }

    //  start from limitIdx and include elements into current partition
    for (int i = limitIdx; i >= 0; i--)
    {
        //  if already taken, continue
        if (taken[i])
            continue;
        int tmp = subsetSum[curIdx] + arr[i];

        // if temp is less than subset then only include the element
        // and call recursively
        if (tmp <= subset)
        {
            //  mark the element and include into current partition sum
            taken[i] = true;
            subsetSum[curIdx] += arr[i];
            bool nxt = isKPartitionPossibleRec(arr, subsetSum, taken,
                                            subset, K, N, curIdx, i - 1);

            // after recursive call unmark the element and remove from
            // subsetition sum
            taken[i] = false;
            subsetSum[curIdx] -= arr[i];
            if (nxt)
                return true;
        }
    }
    return false;
}

//  Method returns true if arr can be partitioned into K subsets
// with equal sum
bool isKPartitionPossible(int arr[], int N, int K)
{
    //  If K is 1, then complete array will be our answer
    if (K == 1)
        return true;

    //  If total number of partitions are more than N, then
    // division is not possible
    if (N < K)
        return false;

    // if array sum is not divisible by K then we can't divide
    // array into K partitions
    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];
    if (sum % K != 0)
        return false;

    //  the sum of each subset should be subset (= sum / K)
    int subset = sum / K;
    int subsetSum[K];
    bool taken[N];

    //  Initialize sum of each subset from 0
    for (int i = 0; i < K; i++)
        subsetSum[i] = 0;

    //  mark all elements as not taken
    for (int i = 0; i < N; i++)
        taken[i] = false;

    // initialize first subsubset sum as last element of
    // array and mark that as taken
    subsetSum[0] = arr[N - 1];
    taken[N - 1] = true;

    //  call recursive method to check K-substitution condition
    return isKPartitionPossibleRec(arr, subsetSum, taken,
                                     subset, K, N, 0, N - 1);
}

//  Driver code to test above methods
int main()
{
    int arr[] = {2, 1, 4, 5, 3, 3};
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    if (isKPartitionPossible(arr, N, K))
        cout << "Partitions into equal sum is possible.\n";
    else
        cout << "Partitions into equal sum is not possible.\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether an array can be
// partitioned into K subsets of equal sum
class GFG 
{

// Recursive Utility method to check K equal sum
// subsetition of array
/**
    array         - given input array
    subsetSum array - sum to store each subset of the array
    taken         - boolean array to check whether element
                    is taken into sum partition or not
    K             - number of partitions needed
    N             - total number of element in array
    curIdx         - current subsetSum index
    limitIdx     - lastIdx from where array element should
                    be taken */
static boolean isKPartitionPossibleRec(int arr[], int subsetSum[], boolean taken[],
                int subset, int K, int N, int curIdx, int limitIdx)
{
    if (subsetSum[curIdx] == subset)
    {
        /* current index (K - 2) represents (K - 1) subsets of equal
            sum last partition will already remain with sum 'subset'*/
        if (curIdx == K - 2)
            return true;

        // recursive call for next subsetition
        return isKPartitionPossibleRec(arr, subsetSum, taken, subset,
                                            K, N, curIdx + 1, N - 1);
    }

    // start from limitIdx and include elements into current partition
    for (int i = limitIdx; i >= 0; i--)
    {
        // if already taken, continue
        if (taken[i])
            continue;
        int tmp = subsetSum[curIdx] + arr[i];

        // if temp is less than subset then only include the element
        // and call recursively
        if (tmp <= subset)
        {
            // mark the element and include into current partition sum
            taken[i] = true;
            subsetSum[curIdx] += arr[i];
            boolean nxt = isKPartitionPossibleRec(arr, subsetSum, taken,
                                            subset, K, N, curIdx, i - 1);

            // after recursive call unmark the element and remove from
            // subsetition sum
            taken[i] = false;
            subsetSum[curIdx] -= arr[i];
            if (nxt)
                return true;
        }
    }
    return false;
}

// Method returns true if arr can be partitioned into K subsets
// with equal sum
static boolean isKPartitionPossible(int arr[], int N, int K)
{
    // If K is 1, then complete array will be our answer
    if (K == 1)
        return true;

    // If total number of partitions are more than N, then
    // division is not possible
    if (N < K)
        return false;

    // if array sum is not divisible by K then we can't divide
    // array into K partitions
    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];
    if (sum % K != 0)
        return false;

    // the sum of each subset should be subset (= sum / K)
    int subset = sum / K;
    int []subsetSum = new int[K];
    boolean []taken = new boolean[N];

    // Initialize sum of each subset from 0
    for (int i = 0; i < K; i++)
        subsetSum[i] = 0;

    // mark all elements as not taken
    for (int i = 0; i < N; i++)
        taken[i] = false;

    // initialize first subsubset sum as last element of
    // array and mark that as taken
    subsetSum[0] = arr[N - 1];
    taken[N - 1] = true;

    // call recursive method to check K-substitution condition
    return isKPartitionPossibleRec(arr, subsetSum, taken,
                                    subset, K, N, 0, N - 1);
}

// Driver code 
public static void main(String[] args)
{
    int arr[] = {2, 1, 4, 5, 3, 3};
    int N = arr.length;
    int K = 3;

    if (isKPartitionPossible(arr, N, K))
        System.out.println("Partitions into equal sum is possible.");
    else
        System.out.println("Partitions into equal sum is not possible.");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to check whether an array can be 
# partitioned into K subsets of equal sum 

# Recursive Utility method to check K equal sum 
# subsetition of array 

"""* 
array     - given input array 
subsetSum array - sum to store each subset of the array 
taken     - ean array to check whether element 
is taken into sum partition or not 
K         - number of partitions needed 
N         - total number of element in array 
curIdx     - current subsetSum index 
limitIdx     - lastIdx from where array element should 
be taken """

def isKPartitionPossibleRec(arr, subsetSum, taken, 
                            subset, K, N, curIdx, limitIdx):
    if subsetSum[curIdx] == subset:

        """ current index (K - 2) represents (K - 1) 
        subsets of equal sum last partition will 
        already remain with sum 'subset'"""
        if (curIdx == K - 2):
            return True

        # recursive call for next subsetition 
        return isKPartitionPossibleRec(arr, subsetSum, taken, 
                                       subset, K, N, curIdx + 1 , N - 1)

    # start from limitIdx and include 
    # elements into current partition 
    for i in range(limitIdx, -1, -1):

        # if already taken, continue 
        if (taken[i]):
            continue
        tmp = subsetSum[curIdx] + arr[i] 

        # if temp is less than subset, then only 
        # include the element and call recursively 
        if (tmp <= subset):

            # mark the element and include into 
            # current partition sum 
            taken[i] = True
            subsetSum[curIdx] += arr[i] 
            nxt = isKPartitionPossibleRec(arr, subsetSum, taken, 
                                          subset, K, N, curIdx, i - 1)

            # after recursive call unmark the element and 
            # remove from subsetition sum 
            taken[i] = False
            subsetSum[curIdx] -= arr[i] 
            if (nxt):
                return True
    return False

# Method returns True if arr can be 
# partitioned into K subsets with equal sum 
def isKPartitionPossible(arr, N, K):

    # If K is 1,
    # then complete array will be our answer 
    if (K == 1):
        return True

    # If total number of partitions are more than N, 
    # then division is not possible 
    if (N < K):
        return False

    # if array sum is not divisible by K then 
    # we can't divide array into K partitions 
    sum = 0
    for i in range(N):
        sum += arr[i] 
    if (sum % K != 0):
        return False

    # the sum of each subset should be subset (= sum / K) 
    subset = sum // K 
    subsetSum = [0] * K 
    taken = [0] * N

    # Initialize sum of each subset from 0 
    for i in range(K):
        subsetSum[i] = 0

    # mark all elements as not taken 
    for i in range(N):
        taken[i] = False

    # initialize first subsubset sum as  
    # last element of array and mark that as taken 
    subsetSum[0] = arr[N - 1] 
    taken[N - 1] = True

    # call recursive method to check 
    # K-substitution condition 
    return isKPartitionPossibleRec(arr, subsetSum, taken, 
                                   subset, K, N, 0, N - 1)

# Driver Code
arr = [2, 1, 4, 5, 3, 3 ]
N = len(arr) 
K = 3
if (isKPartitionPossible(arr, N, K)):
    print("Partitions into equal sum is possible.\n")
else:
    print("Partitions into equal sum is not possible.\n")

# This code is contributed by SHUBHAMSINGH8410
```

## C#

```
// C# program to check whether an array can be
// partitioned into K subsets of equal sum
using System;

class GFG
{

// Recursive Utility method to check K equal sum
// subsetition of array
/**
    array     - given input array
    subsetSum array - sum to store each subset of the array
    taken     - boolean array to check whether element
                    is taken into sum partition or not
    K         - number of partitions needed
    N         - total number of element in array
    curIdx     - current subsetSum index
    limitIdx     - lastIdx from where array element should
                    be taken */
static bool isKPartitionPossibleRec(int []arr, int []subsetSum, bool []taken,
                int subset, int K, int N, int curIdx, int limitIdx)
{
    if (subsetSum[curIdx] == subset)
    {
        /* current index (K - 2) represents (K - 1) subsets of equal
            sum last partition will already remain with sum 'subset'*/
        if (curIdx == K - 2)
            return true;

        // recursive call for next subsetition
        return isKPartitionPossibleRec(arr, subsetSum, taken, subset,
                                            K, N, curIdx + 1, N - 1);
    }

    // start from limitIdx and include elements into current partition
    for (int i = limitIdx; i >= 0; i--)
    {
        // if already taken, continue
        if (taken[i])
            continue;
        int tmp = subsetSum[curIdx] + arr[i];

        // if temp is less than subset then only include the element
        // and call recursively
        if (tmp <= subset)
        {
            // mark the element and include into current partition sum
            taken[i] = true;
            subsetSum[curIdx] += arr[i];
            bool nxt = isKPartitionPossibleRec(arr, subsetSum, taken,
                                            subset, K, N, curIdx, i - 1);

            // after recursive call unmark the element and remove from
            // subsetition sum
            taken[i] = false;
            subsetSum[curIdx] -= arr[i];
            if (nxt)
                return true;
        }
    }
    return false;
}

// Method returns true if arr can be partitioned into K subsets
// with equal sum
static bool isKPartitionPossible(int []arr, int N, int K)
{
    // If K is 1, then complete array will be our answer
    if (K == 1)
        return true;

    // If total number of partitions are more than N, then
    // division is not possible
    if (N < K)
        return false;

    // if array sum is not divisible by K then we can't divide
    // array into K partitions
    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];
    if (sum % K != 0)
        return false;

    // the sum of each subset should be subset (= sum / K)
    int subset = sum / K;
    int []subsetSum = new int[K];
    bool []taken = new bool[N];

    // Initialize sum of each subset from 0
    for (int i = 0; i < K; i++)
        subsetSum[i] = 0;

    // mark all elements as not taken
    for (int i = 0; i < N; i++)
        taken[i] = false;

    // initialize first subsubset sum as last element of
    // array and mark that as taken
    subsetSum[0] = arr[N - 1];
    taken[N - 1] = true;

    // call recursive method to check K-substitution condition
    return isKPartitionPossibleRec(arr, subsetSum, taken,
                                    subset, K, N, 0, N - 1);
}

// Driver code 
static public void Main ()
{

    int []arr = {2, 1, 4, 5, 3, 3};
    int N = arr.Length;
    int K = 3;

    if (isKPartitionPossible(arr, N, K))
        Console.WriteLine("Partitions into equal sum is possible.");
    else
        Console.WriteLine("Partitions into equal sum is not possible.");
}
}

// This code is contributed by ajit.
```

**输出:**

```
Partitions into equal sum is possible.

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。