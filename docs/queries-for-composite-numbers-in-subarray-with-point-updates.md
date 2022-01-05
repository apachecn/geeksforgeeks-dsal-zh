# 查询子阵列中的合成数(带点更新)

> 原文:[https://www . geeksforgeeks . org/subarray 中带点更新的复合数字查询/](https://www.geeksforgeeks.org/queries-for-composite-numbers-in-subarray-with-point-updates/)

给定 N 个整数的数组，任务是对给定的数组执行以下两个操作:

> **查询(开始，结束)**:从头到尾打印子阵中的合成号码数量
> **更新(I，x)** :将索引 **i** 处的值更新为 x，即 arr[i] = x

**示例**:

```
Input : arr = {1, 12, 3, 5, 17, 9}
        Query 1: query(start = 0, end = 4)
        Query 2: update(i = 3, x = 6)
        Query 3: query(start = 0, end = 4)
Output :1
        2
Explanation
In Query 1, the subarray [0...4]
has 1 Composite number viz. {12}

In Query 2, the value at index 3 
is updated to 6, the array arr now is, {1, 12, 3, 
6, 7, 9}
In Query 3, the subarray [0...4]
has 2 Composite Numbers viz. {12, 6}
```

由于我们需要同时处理范围查询和点更新，一个有效的方法是使用段树来解决这个问题。段树最适合此目的。
我们可以使用厄拉多塞的[筛对所有素数进行预处理，直到我可以取的最大值，比如 MAX。该操作的时间复杂度为 **O(最大对数(log(MAX)))** 。
**构建段树:**
使用段树](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)可以将问题简化为[子阵求和。
现在，我们可以构建段树，其中叶节点表示为 0(如果是素数)或 1(如果是复合数)。
段树的内部节点等于其子节点之和，因此一个节点代表从 L 到 R 范围内的总合成数，其中 L 到 R 的范围属于该节点及其下的子树。
**处理查询和点更新:**
每当我们从开始到结束得到一个查询时，那么我们就可以在段树中查询范围**开始**到**结束**的节点之和，这又代表了范围开始到结束的复合数。
如果我们需要执行点更新并将索引 I 处的值更新为 x，那么我们检查以下情况:](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

> 设 arr <sub>i</sub> 的旧值为 y，新值为 x.
> **例 1:如果 x 和 y 都是复合的。**
> 子阵中复合物的计数不变，所以我们只更新数组，不做
> 修改段树
> **情况 2:如果 x 和 y 都是素数。**
> 子阵中复合的计数不变，所以我们只更新数组，不做
> 修改段树
> **情况 3:如果 y 是复合但 x 是素数。**
> 子阵中合成数的计数减少，所以我们更新数组，每隔一个
> 范围加-1，要更新的索引 I 是段树中的一部分
> **情况 4:如果 y 是质数但 x 是合成数。**
> 子阵列中复合数的计数增加，因此我们更新数组并为每个
> 范围增加 1，要更新的索引 I 是段树中的一部分

以下是上述方法的实现:

## C++

```
// C++ program to find number of composite numbers in a
// subarray and performing updates

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

// Function to calculate primes upto MAX
// using sieve of Eratosthenes
void sieveOfEratosthenes(bool isPrime[])
{
    isPrime[1] = true;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                isPrime[i] = false;
        }
    }
}

// A utility function to get the middle
// index from corner indexes.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/*  A recursive function to get the number of composites
    in a given range of array indexes. The following are
    parameters for this function.

    st --> Pointer to segment tree
    index --> Index of current node in the segment tree.
              Initially 0 is passed as root is always
              at index 0.
    ss & se --> Starting and ending indexes of the
                segment represented by current node,
                i.e., st[index]
    qs & qe --> Starting and ending indexes of
    query range
*/
int queryCompositesUtil(int* st, int ss, int se, int qs,
                        int qe, int index)
{
    // If segment of this node is a part of given range,
    // then return the number of composites
    // in the segment
    if (qs <= ss && qe >= se)
        return st[index];

    // If segment of this node is
    // outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return queryCompositesUtil(st, ss, mid, qs, qe, 2 * index + 1)
           + queryCompositesUtil(st, mid + 1, se, qs, qe, 2 * index + 2);
}

/*  A recursive function to update the nodes which
    have the given index in their range. The following
    are parameters st, si, ss and se are same as getSumUtil()

    i --> index of the element to be updated. This index is
          in input array.
    diff --> Value to be added to all nodes which
          have i in range
*/
void updateValueUtil(int* st, int ss, int se, int i,
                     int diff, int si)
{
    // Base Case: If the input index
    // lies outside the range of
    // this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of
    // this node, then update the value of
    // the node and its children
    st[si] = st[si] + diff;

    if (se != ss) {
        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i, diff, 2 * si + 1);
        updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2);
    }
}

// The function to update a value in input
// array and segment tree. It uses updateValueUtil()
// to update the value in segment tree
void updateValue(int arr[], int* st, int n, int i,
                 int new_val, bool isPrime[])
{
    // Check for erroneous input index
    if (i < 0 || i > n - 1) {
        printf("Invalid Input");
        return;
    }

    int diff, oldValue;

    oldValue = arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Case 1: Old and new values both are primes
    if (isPrime[oldValue] && isPrime[new_val])
        return;

    // Case 2: Old and new values both composite
    if ((!isPrime[oldValue]) && (!isPrime[new_val]))
        return;

    // Case 3: Old value was composite, new value is prime
    if (!isPrime[oldValue] && isPrime[new_val]) {
        diff = -1;
    }

    // Case 4: Old value was prime, new_val is composite
    if (isPrime[oldValue] && !isPrime[new_val]) {
        diff = 1;
    }

    // Update the values of nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0);
}

// Return number of composite numbers in range
// from index qs (query start) to qe (query end).
// It mainly uses queryCompositesUtil()
void queryComposites(int* st, int n, int qs, int qe)
{
    int compositesInRange = queryCompositesUtil(st, 0, n - 1, qs, qe, 0);

    cout << "Number of Composites in subarray from " << qs
         << " to " << qe << " = " << compositesInRange << "\n";
}

// A recursive function that constructs Segment Tree
// for array[ss..se].
// si is index of current node in segment tree st
int constructSTUtil(int arr[], int ss, int se, int* st,
                    int si, bool isPrime[])
{
    // If there is one element in array, check if it
    // is prime then store 1 in the segment tree else
    // store 0 and return
    if (ss == se) {

        // if arr[ss] is composite
        if (!isPrime[arr[ss]])
            st[si] = 1;
        else
            st[si] = 0;

        return st[si];
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum
    // of the two values in this node
    int mid = getMid(ss, se);
    st[si] = constructSTUtil(arr, ss, mid, st,
                             si * 2 + 1, isPrime)
             + constructSTUtil(arr, mid + 1, se, st,
                               si * 2 + 2, isPrime);
    return st[si];
}

/*  Function to construct segment tree from given array.
    This function allocates memory for segment tree and
    calls constructSTUtil() to fill the allocated memory */
int* constructST(int arr[], int n, bool isPrime[])
{
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    int* st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0, isPrime);

    // Return the constructed segment tree
    return st;
}

// Driver Code
int main()
{

    int arr[] = { 1, 12, 3, 5, 17, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    /*  Preprocess all primes till MAX.
        Create a boolean array "isPrime[0..MAX]".
        A value in prime[i] will finally be false
        if i is composite, else true.
    */
    bool isPrime[MAX + 1];
    memset(isPrime, true, sizeof isPrime);
    sieveOfEratosthenes(isPrime);

    // Build segment tree from given array
    int* st = constructST(arr, n, isPrime);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    queryComposites(st, n, start, end);

    // Query 2: Update(i = 3, x = 6), i.e Update
    // a[i] to x
    int i = 3;
    int x = 6;
    updateValue(arr, st, n, i, x, isPrime);

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryComposites(st, n, start, end);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of composite numbers in a
// subarray and performing updates
public class Main
{
    static int MAX = 1000;

    // Function to calculate primes upto MAX
    // using sieve of Eratosthenes
    static void sieveOfEratosthenes(boolean[] isPrime)
    {
        isPrime[1] = true;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (isPrime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // A utility function to get the middle
    // index from corner indexes.
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    /*  A recursive function to get the number of composites
        in a given range of array indexes. The following are
        parameters for this function.

        st --> Pointer to segment tree
        index --> Index of current node in the segment tree.
                  Initially 0 is passed as root is always
                  at index 0.
        ss & se --> Starting and ending indexes of the
                    segment represented by current node,
                    i.e., st[index]
        qs & qe --> Starting and ending indexes of
        query range
    */
    static int queryCompositesUtil(int[] st, int ss, int se, int qs, int qe, int index)
    {
        // If segment of this node is a part of given range,
        // then return the number of composites
        // in the segment
        if (qs <= ss && qe >= se)
            return st[index];

        // If segment of this node is
        // outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment
        // overlaps with the given range
        int mid = getMid(ss, se);
        return queryCompositesUtil(st, ss, mid, qs, qe, 2 * index + 1)
               + queryCompositesUtil(st, mid + 1, se, qs, qe, 2 * index + 2);
    }

    /*  A recursive function to update the nodes which
        have the given index in their range. The following
        are parameters st, si, ss and se are same as getSumUtil()

        i --> index of the element to be updated. This index is
              in input array.
        diff --> Value to be added to all nodes which
              have i in range
    */
    static void updateValueUtil(int[] st, int ss, int se, int i, int diff, int si)
    {
        // Base Case: If the input index
        // lies outside the range of
        // this segment
        if (i < ss || i > se)
            return;

        // If the input index is in range of
        // this node, then update the value of
        // the node and its children
        st[si] = st[si] + diff;

        if (se != ss) {
            int mid = getMid(ss, se);
            updateValueUtil(st, ss, mid, i, diff, 2 * si + 1);
            updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2);
        }
    }

    // The function to update a value in input
    // array and segment tree. It uses updateValueUtil()
    // to update the value in segment tree
    static void updateValue(int[] arr, int[] st, int n, int i, int new_val, boolean[] isPrime)
    {
        // Check for erroneous input index
        if (i < 0 || i > n - 1) {
            System.out.print("Invalid Input");
            return;
        }

        int diff = 0, oldValue;

        oldValue = arr[i];

        // Update the value in array
        arr[i] = new_val;

        // Case 1: Old and new values both are primes
        if (isPrime[oldValue] && isPrime[new_val])
            return;

        // Case 2: Old and new values both composite
        if ((!isPrime[oldValue]) && (!isPrime[new_val]))
            return;

        // Case 3: Old value was composite, new value is prime
        if (!isPrime[oldValue] && isPrime[new_val]) {
            diff = -1;
        }

        // Case 4: Old value was prime, new_val is composite
        if (isPrime[oldValue] && !isPrime[new_val]) {
            diff = 1;
        }

        // Update the values of nodes in segment tree
        updateValueUtil(st, 0, n - 1, i, diff, 0);
    }

    // Return number of composite numbers in range
    // from index qs (query start) to qe (query end).
    // It mainly uses queryCompositesUtil()
    static void queryComposites(int[] st, int n, int qs, int qe)
    {
        int compositesInRange = queryCompositesUtil(st, 0, n - 1, qs, qe, 0);

        System.out.println("Number of Composites in subarray from " + qs
             + " to " + qe + " = " + compositesInRange);
    }

    // A recursive function that constructs Segment Tree
    // for array[ss..se].
    // si is index of current node in segment tree st
    static int constructSTUtil(int[] arr, int ss, int se, int[] st, int si, boolean[] isPrime)
    {
        // If there is one element in array, check if it
        // is prime then store 1 in the segment tree else
        // store 0 and return
        if (ss == se) {

            // if arr[ss] is composite
            if (!isPrime[arr[ss]])
                st[si] = 1;
            else
                st[si] = 0;

            return st[si];
        }

        // If there are more than one elements, then recur
        // for left and right subtrees and store the sum
        // of the two values in this node
        int mid = getMid(ss, se);
        st[si] = constructSTUtil(arr, ss, mid, st,
                                 si * 2 + 1, isPrime)
                 + constructSTUtil(arr, mid + 1, se, st,
                                   si * 2 + 2, isPrime);
        return st[si];
    }

    /*  Function to construct segment tree from given array.
        This function allocates memory for segment tree and
        calls constructSTUtil() to fill the allocated memory */
    static int[] constructST(int[] arr, int n, boolean[] isPrime)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        int x = (int)(Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        int max_size = 2 * (int)Math.pow(2, x) - 1;

        int[] st = new int[max_size];

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0, isPrime);

        // Return the constructed segment tree
        return st;
    }

    public static void main(String[] args) {
        int[] arr = { 1, 12, 3, 5, 17, 9 };
        int n = arr.length;

        /*  Preprocess all primes till MAX.
            Create a boolean array "isPrime[0..MAX]".
            A value in prime[i] will finally be false
            if i is composite, else true.
        */
        boolean[] isPrime = new boolean[MAX + 1];
        for(int a = 0; a < MAX + 1; a++)
        {
            isPrime[a] = true;
        }
        sieveOfEratosthenes(isPrime);

        // Build segment tree from given array
        int[] st = constructST(arr, n, isPrime);

        // Query 1: Query(start = 0, end = 4)
        int start = 0;
        int end = 4;
        queryComposites(st, n, start, end);

        // Query 2: Update(i = 3, x = 6), i.e Update
        // a[i] to x
        int i = 3;
        int x = 6;
        updateValue(arr, st, n, i, x, isPrime);

        // Query 3: Query(start = 0, end = 4)
        start = 0;
        end = 4;
        queryComposites(st, n, start, end);
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program to find
# number of composite numbers
# in a subarray and performing
# updates
import math
MAX = 1000

# Function to calculate primes
# upto MAX using sieve of Eratosthenes
def sieveOfEratosthenes(isPrime):

    isPrime[1] = True;
    p = 2

    while p * p <= MAX:

        # If prime[p] is not
        # changed, then
        # it is a prime
        if (isPrime[p] == True):

            # Update all multiples of p
            for i in range(p * 2,
                           MAX + 1,  p):
                isPrime[i] = False;
        p += 1

# A utility function to get
# the middle index from
# corner indexes.
def getMid(s, e):

    return s + (e - s) // 2;

'''  A recursive function to get the number
    of composites in a given range of array
    indexes. The following are parameters
    for this function.

    st --> Pointer to segment tree
    index --> Index of current node in the
              segment tree. Initially 0 is
              passed as root is always at
              index 0.
    ss & se --> Starting and ending indexes
                of the segment represented
                by current node, i.e., st[index]
    qs & qe --> Starting and ending indexes of
    query range
'''

def queryCompositesUtil(st, ss, se, qs,
                        qe, index):

    # If segment of this node is a
    # part of given range, then
    # return the number of composites
    # in the segment
    if (qs <= ss and qe >= se):
        return st[index];

    # If segment of this node is
    # outside the given range
    if (se < qs or ss > qe):
        return 0;

    # If a part of this segment
    # overlaps with the given range
    mid = getMid(ss, se);
    return (queryCompositesUtil(st, ss,
                                mid, qs,
                                qe, 2 * index + 1) +
            queryCompositesUtil(st, mid + 1,
                                se, qs, qe,
                                2 * index + 2));

'''  A recursive function to update the
     nodes which have the given index in
     their range. The following are parameters
     st, si, ss and se are same as getSumUtil()

     i --> index of the element to be updated.
           This index is in input array.
     diff --> Value to be added to all nodes
              which have i in range
'''
def updateValueUtil(st, ss, se, i,
                    diff, si):

    # Base Case: If the input index
    # lies outside the range of
    # this segment
    if (i < ss or i > se):
        return;

    # If the input index is in
    # range of this node, then
    # update the value of the
    # node and its children
    st[si] = st[si] + diff;

    if (se != ss):
        mid = getMid(ss, se);
        updateValueUtil(st, ss,
                        mid, i,
                        diff, 2 * si + 1);
        updateValueUtil(st, mid + 1,
                        se, i, diff,
                        2 * si + 2);

# The function to update a value
# in input array and segment tree.
# It uses updateValueUtil() to
# update the value in segment tree
def updateValue(arr,  st, n, i,
                new_val, isPrime):

    # Check for erroneous
    # input index
    if (i < 0 or i > n - 1):
        print("Invalid Input");
        return

    oldValue = arr[i];

    # Update the value in array
    arr[i] = new_val;

    # Case 1: Old and new values
    # both are primes
    if (isPrime[oldValue] and
        isPrime[new_val]):
        return;

    # Case 2: Old and new values
    # both composite
    if ((not isPrime[oldValue]) and
        (not isPrime[new_val])):
        return;

    # Case 3: Old value was composite,
    # new value is prime
    if (not isPrime[oldValue] and
        isPrime[new_val]):
        diff = -1;

    # Case 4: Old value was prime,
    # new_val is composite
    if (isPrime[oldValue] and
        not isPrime[new_val]):
        diff = 1;

    # Update the values of
    # nodes in segment tree
    updateValueUtil(st, 0,
                    n - 1, i,
                    diff, 0);

# Return number of composite
# numbers in range from index
# qs (query start) to qe (query end).
# It mainly uses queryCompositesUtil()
def queryComposites(st, n, qs, qe):

    compositesInRange = queryCompositesUtil(st, 0,
                                            n - 1,
                                            qs, qe, 0);

    print("Number of Composites in subarray from ",
          qs, " to ", qe, " = ", compositesInRange)

# A recursive function that constructs
# Segment Tree for array[ss..se].
# si is index of current node in
# segment tree st
def constructSTUtil(arr, ss, se, st,
                    si, isPrime):

    # If there is one element in array,
    # check if it is prime then store
    # 1 in the segment tree else store
    # 0 and return
    if (ss == se):

        # if arr[ss] is composite
        if (not isPrime[arr[ss]]):
            st[si] = 1;
        else:
            st[si] = 0;

        return st[si];

    # If there are more than one elements,
    # then recur for left and right subtrees
    # and store the sum of the two values
    # in this node
    mid = getMid(ss, se);
    st[si] = (constructSTUtil(arr, ss,
                              mid, st,
                              si * 2 + 1,
                              isPrime) +
              constructSTUtil(arr, mid + 1,
                              se, st,
                              si * 2 + 2,
                              isPrime))
    return st[si];

'''  Function to construct segment tree
     from given array. This function
     allocates memory for segment tree
     and calls constructSTUtil() to fill
     the allocated memory '''
def constructST(arr, n, isPrime):

    # Allocate memory for
    # segment tree

    # Height of segment tree
    x = (int)(math.ceil(math.log2(n)));

    # Maximum size of segment tree
    max_size = 2 * pow(2, x) - 1;

    st = [0] * max_size

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1,
                    st, 0, isPrime);

    # Return the constructed
    # segment tree
    return st;

# Driver Code
if __name__ == "__main__":

    arr = [1, 12, 3, 5, 17, 9]
    n = len(arr)

    '''  Preprocess all primes till MAX.
        Create a boolean array "isPrime[0..MAX]".
        A value in prime[i] will finally be false
        if i is composite, else true.
    '''
    isPrime = [True] * (MAX + 1)

    sieveOfEratosthenes(isPrime);

    # Build segment tree from given array
    st = constructST(arr, n, isPrime);

    # Query 1: Query(start = 0,
    # end = 4)
    start = 0;
    end = 4;
    queryComposites(st, n,
                    start, end);

    # Query 2: Update(i = 3, x = 6),
    # i.e Update a[i] to x
    i = 3;
    x = 6;
    updateValue(arr, st, n, i,
                x, isPrime);

    # Query 3: Query(start = 0,
    # end = 4)
    start = 0;
    end = 4;
    queryComposites(st, n,
                    start, end)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find number of composite numbers in a
// subarray and performing updates
using System;
class GFG {

    static int MAX = 1000;

    // Function to calculate primes upto MAX
    // using sieve of Eratosthenes
    static void sieveOfEratosthenes(bool[] isPrime)
    {
        isPrime[1] = true;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (isPrime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // A utility function to get the middle
    // index from corner indexes.
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    /*  A recursive function to get the number of composites
        in a given range of array indexes. The following are
        parameters for this function.

        st --> Pointer to segment tree
        index --> Index of current node in the segment tree.
                  Initially 0 is passed as root is always
                  at index 0.
        ss & se --> Starting and ending indexes of the
                    segment represented by current node,
                    i.e., st[index]
        qs & qe --> Starting and ending indexes of
        query range
    */
    static int queryCompositesUtil(int[] st, int ss, int se, int qs, int qe, int index)
    {
        // If segment of this node is a part of given range,
        // then return the number of composites
        // in the segment
        if (qs <= ss && qe >= se)
            return st[index];

        // If segment of this node is
        // outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment
        // overlaps with the given range
        int mid = getMid(ss, se);
        return queryCompositesUtil(st, ss, mid, qs, qe, 2 * index + 1)
               + queryCompositesUtil(st, mid + 1, se, qs, qe, 2 * index + 2);
    }

    /*  A recursive function to update the nodes which
        have the given index in their range. The following
        are parameters st, si, ss and se are same as getSumUtil()

        i --> index of the element to be updated. This index is
              in input array.
        diff --> Value to be added to all nodes which
              have i in range
    */
    static void updateValueUtil(int[] st, int ss, int se, int i, int diff, int si)
    {
        // Base Case: If the input index
        // lies outside the range of
        // this segment
        if (i < ss || i > se)
            return;

        // If the input index is in range of
        // this node, then update the value of
        // the node and its children
        st[si] = st[si] + diff;

        if (se != ss) {
            int mid = getMid(ss, se);
            updateValueUtil(st, ss, mid, i, diff, 2 * si + 1);
            updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2);
        }
    }

    // The function to update a value in input
    // array and segment tree. It uses updateValueUtil()
    // to update the value in segment tree
    static void updateValue(int[] arr, int[] st, int n, int i, int new_val, bool[] isPrime)
    {
        // Check for erroneous input index
        if (i < 0 || i > n - 1) {
            Console.Write("Invalid Input");
            return;
        }

        int diff = 0, oldValue;

        oldValue = arr[i];

        // Update the value in array
        arr[i] = new_val;

        // Case 1: Old and new values both are primes
        if (isPrime[oldValue] && isPrime[new_val])
            return;

        // Case 2: Old and new values both composite
        if ((!isPrime[oldValue]) && (!isPrime[new_val]))
            return;

        // Case 3: Old value was composite, new value is prime
        if (!isPrime[oldValue] && isPrime[new_val]) {
            diff = -1;
        }

        // Case 4: Old value was prime, new_val is composite
        if (isPrime[oldValue] && !isPrime[new_val]) {
            diff = 1;
        }

        // Update the values of nodes in segment tree
        updateValueUtil(st, 0, n - 1, i, diff, 0);
    }

    // Return number of composite numbers in range
    // from index qs (query start) to qe (query end).
    // It mainly uses queryCompositesUtil()
    static void queryComposites(int[] st, int n, int qs, int qe)
    {
        int compositesInRange = queryCompositesUtil(st, 0, n - 1, qs, qe, 0);

        Console.WriteLine("Number of Composites in subarray from " + qs
             + " to " + qe + " = " + compositesInRange);
    }

    // A recursive function that constructs Segment Tree
    // for array[ss..se].
    // si is index of current node in segment tree st
    static int constructSTUtil(int[] arr, int ss, int se, int[] st, int si, bool[] isPrime)
    {
        // If there is one element in array, check if it
        // is prime then store 1 in the segment tree else
        // store 0 and return
        if (ss == se) {

            // if arr[ss] is composite
            if (!isPrime[arr[ss]])
                st[si] = 1;
            else
                st[si] = 0;

            return st[si];
        }

        // If there are more than one elements, then recur
        // for left and right subtrees and store the sum
        // of the two values in this node
        int mid = getMid(ss, se);
        st[si] = constructSTUtil(arr, ss, mid, st,
                                 si * 2 + 1, isPrime)
                 + constructSTUtil(arr, mid + 1, se, st,
                                   si * 2 + 2, isPrime);
        return st[si];
    }

    /*  Function to construct segment tree from given array.
        This function allocates memory for segment tree and
        calls constructSTUtil() to fill the allocated memory */
    static int[] constructST(int[] arr, int n, bool[] isPrime)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        int x = (int)(Math.Ceiling(Math.Log(n) / Math.Log(2)));

        // Maximum size of segment tree
        int max_size = 2 * (int)Math.Pow(2, x) - 1;

        int[] st = new int[max_size];

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0, isPrime);

        // Return the constructed segment tree
        return st;
    }

  static void Main() {
    int[] arr = { 1, 12, 3, 5, 17, 9 };
    int n = arr.Length;

    /*  Preprocess all primes till MAX.
        Create a boolean array "isPrime[0..MAX]".
        A value in prime[i] will finally be false
        if i is composite, else true.
    */
    bool[] isPrime = new bool[MAX + 1];
    for(int a = 0; a < MAX + 1; a++)
    {
        isPrime[a] = true;
    }
    sieveOfEratosthenes(isPrime);

    // Build segment tree from given array
    int[] st = constructST(arr, n, isPrime);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    queryComposites(st, n, start, end);

    // Query 2: Update(i = 3, x = 6), i.e Update
    // a[i] to x
    int i = 3;
    int x = 6;
    updateValue(arr, st, n, i, x, isPrime);

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryComposites(st, n, start, end);
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program to find number of composite numbers in a
    // subarray and performing updates

    let MAX = 1000;

    // Function to calculate primes upto MAX
    // using sieve of Eratosthenes
    function sieveOfEratosthenes(isPrime)
    {
        isPrime[1] = true;

        for (let p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (isPrime[p] == true) {

                // Update all multiples of p
                for (let i = p * 2; i <= MAX; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // A utility function to get the middle
    // index from corner indexes.
    function getMid(s, e)
    {
        return s + parseInt((e - s) / 2, 10);
    }

    /*  A recursive function to get the number of composites
        in a given range of array indexes. The following are
        parameters for this function.

        st --> Pointer to segment tree
        index --> Index of current node in the segment tree.
                  Initially 0 is passed as root is always
                  at index 0.
        ss & se --> Starting and ending indexes of the
                    segment represented by current node,
                    i.e., st[index]
        qs & qe --> Starting and ending indexes of
        query range
    */
    function queryCompositesUtil(st, ss, se, qs, qe, index)
    {
        // If segment of this node is a part of given range,
        // then return the number of composites
        // in the segment
        if (qs <= ss && qe >= se)
            return st[index];

        // If segment of this node is
        // outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment
        // overlaps with the given range
        let mid = getMid(ss, se);
        return queryCompositesUtil(st, ss, mid, qs, qe, 2 * index + 1)
               + queryCompositesUtil(st, mid + 1, se, qs, qe, 2 * index + 2);
    }

    /*  A recursive function to update the nodes which
        have the given index in their range. The following
        are parameters st, si, ss and se are same as getSumUtil()

        i --> index of the element to be updated. This index is
              in input array.
        diff --> Value to be added to all nodes which
              have i in range
    */
    function updateValueUtil(st, ss, se, i, diff, si)
    {
        // Base Case: If the input index
        // lies outside the range of
        // this segment
        if (i < ss || i > se)
            return;

        // If the input index is in range of
        // this node, then update the value of
        // the node and its children
        st[si] = st[si] + diff;

        if (se != ss) {
            let mid = getMid(ss, se);
            updateValueUtil(st, ss, mid, i, diff, 2 * si + 1);
            updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2);
        }
    }

    // The function to update a value in input
    // array and segment tree. It uses updateValueUtil()
    // to update the value in segment tree
    function updateValue(arr, st, n, i, new_val, isPrime)
    {
        // Check for erroneous input index
        if (i < 0 || i > n - 1) {
            document.write("Invalid Input");
            return;
        }

        let diff = 0, oldValue;

        oldValue = arr[i];

        // Update the value in array
        arr[i] = new_val;

        // Case 1: Old and new values both are primes
        if (isPrime[oldValue] && isPrime[new_val])
            return;

        // Case 2: Old and new values both composite
        if ((!isPrime[oldValue]) && (!isPrime[new_val]))
            return;

        // Case 3: Old value was composite, new value is prime
        if (!isPrime[oldValue] && isPrime[new_val]) {
            diff = -1;
        }

        // Case 4: Old value was prime, new_val is composite
        if (isPrime[oldValue] && !isPrime[new_val]) {
            diff = 1;
        }

        // Update the values of nodes in segment tree
        updateValueUtil(st, 0, n - 1, i, diff, 0);
    }

    // Return number of composite numbers in range
    // from index qs (query start) to qe (query end).
    // It mainly uses queryCompositesUtil()
    function queryComposites(st, n, qs, qe)
    {
        let compositesInRange = queryCompositesUtil(st, 0, n - 1, qs, qe, 0);

        document.write("Number of Composites in subarray from " + qs
             + " to " + qe + " = " + compositesInRange + "</br>");
    }

    // A recursive function that constructs Segment Tree
    // for array[ss..se].
    // si is index of current node in segment tree st
    function constructSTUtil(arr, ss, se, st, si, isPrime)
    {
        // If there is one element in array, check if it
        // is prime then store 1 in the segment tree else
        // store 0 and return
        if (ss == se) {

            // if arr[ss] is composite
            if (!isPrime[arr[ss]])
                st[si] = 1;
            else
                st[si] = 0;

            return st[si];
        }

        // If there are more than one elements, then recur
        // for left and right subtrees and store the sum
        // of the two values in this node
        let mid = getMid(ss, se);
        st[si] = constructSTUtil(arr, ss, mid, st,
                                 si * 2 + 1, isPrime)
                 + constructSTUtil(arr, mid + 1, se, st,
                                   si * 2 + 2, isPrime);
        return st[si];
    }

    /*  Function to construct segment tree from given array.
        This function allocates memory for segment tree and
        calls constructSTUtil() to fill the allocated memory */
    function constructST(arr, n, isPrime)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        let x = (Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        let max_size = 2 * Math.pow(2, x) - 1;

        let st = new Array(max_size);

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0, isPrime);

        // Return the constructed segment tree
        return st;
    }

    let arr = [ 1, 12, 3, 5, 17, 9 ];
    let n = arr.length;

    /*  Preprocess all primes till MAX.
        Create a boolean array "isPrime[0..MAX]".
        A value in prime[i] will finally be false
        if i is composite, else true.
    */
    let isPrime = new Array(MAX + 1);
    for(let a = 0; a < MAX + 1; a++)
    {
        isPrime[a] = true;
    }
    sieveOfEratosthenes(isPrime);

    // Build segment tree from given array
    let st = constructST(arr, n, isPrime);

    // Query 1: Query(start = 0, end = 4)
    let start = 0;
    let end = 4;
    queryComposites(st, n, start, end);

    // Query 2: Update(i = 3, x = 6), i.e Update
    // a[i] to x
    let i = 3;
    let x = 6;
    updateValue(arr, st, n, i, x, isPrime);

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryComposites(st, n, start, end);

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Number of Composites in subarray from 0 to 4 = 1
Number of Composites in subarray from 0 to 4 = 2
```

每次查询和更新的**时间复杂度**为 O(logn)，构建段树的时间复杂度为 O(n)
**注**:这里，使用厄拉多塞的筛子预处理素数直到 MAX 的时间复杂度为 O(MAX log(log(MAX))，其中 MAX 为 arr <sub>i</sub> 可以取的最大值。