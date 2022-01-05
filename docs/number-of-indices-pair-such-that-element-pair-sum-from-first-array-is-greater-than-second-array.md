# 第一个数组的元素对和大于第二个数组的索引对的数量

> 原文:[https://www . geesforgeks . org/index-number-of-pair-so-element-pair-sum-from-first-array-大于-second-array/](https://www.geeksforgeeks.org/number-of-indices-pair-such-that-element-pair-sum-from-first-array-is-greater-than-second-array/)

给定两个大小相等的整数数组 **A[]** 和 **B[]** ，任务是找出数组中的索引对{i，j}的数量，使得 **A[i] + A[j] > B[i] + B[j]** 和 **i < j** 。
**举例:**

> **输入:** A[] = {4，8，2，6，2}，B[] = {4，5，4，1，3}
> **输出:** 7
> **说明:**
> 数组中共有 7 对指数{i，j}符合条件。它们是:
> {0，1 }:A[0]+A[1]>B[0]+B[1]
> { 0，3 }:A[0]+A[3]>B[0]+B[3]
> { 1，2 }:A[1]+A[2]>B[1]+B[2]
> { 1，3}: A[1] + A[3] > B[1] 4}，B[] = {1，3，2，4}
> **输出:** 0
> **解释:**
> 找不到满足给定条件的{i，j}的可能对

**天真方法:**天真方法是考虑给定数组中所有可能的{i，j}对，并检查 **A[i] + A[j] > B[i] + B[j]** 。这可以通过使用[嵌套循环](https://www.geeksforgeeks.org/java-nested-loops-with-examples/)的概念来实现。
**时间复杂度:** O(N <sup>2</sup> )
**高效途径:**从问题中得到的关键观察是，给定的条件也可以可视化为(ai-bi) + (aj-bj) > 0 所以我们可以制作另一个数组来存储两个数组的差异。让这个数组为 D .因此，问题简化为用 Di+Dj > 0 寻找对。现在，我们可以对 D 数组进行排序，对于每个对应的元素 Di，我们将找到 Di 可以组成的良好对的数量，并将这个对的数量添加到一个计数变量中。对于每个元素 Di，为了找到它能产生的好对的数目，我们可以使用标准模板库的上界函数来找到-Di 的上界。因为数组是排序的，所以在-Di 之后出现的所有元素也将与 Di 很好地配对。因此，如果-Di 的上限是 x，n 是数组的总大小，那么对应于 Di 的总对将是 n-x。

*   问题中给定的条件可以改写为:

```
A[i] + A[j] > B[i] + B[j]
A[i] + A[j] - B[i] - B[j] > 0
(A[i] - B[i]) + (A[j] - B[j]) > 0
```

*   创建另一个数组，比如 D，以存储两个数组中相应索引处元素之间的差异，即

```
D[i] = A[i] - B[i]
```

*   现在确保约束 i < j is satisfied, [排序](https://www.geeksforgeeks.org/bubble-sort/)差数组 D，这样每个元素 I 都比它右边的元素小。
*   如果在某个索引 I 处，差数组 D 中的值为负，那么我们只需要找到距离最近的位置**‘j’**，在该位置处该值刚好大于**-D【I】**，这样在求和时该值变为 **> 0** 。
    为了找到这样的索引‘j’，可以使用[上界()](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)函数或[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，因为数组是排序的。

下面是上述方法的实现:

## C++

```
// C++ program to find the number of indices pair
// such that pair sum from first Array
// is greater than second Array

#include <bits/stdc++.h>
using namespace std;

// Function to get the number of pairs of indices
// {i, j} in the given two arrays A and B such that
// A[i] + A[j] > B[i] + B[j]
int getPairs(vector<int> A, vector<int> B, int n)
{
    // Initializing the difference array D
    vector<int> D(n);

    // Computing the difference between the
    // elements at every index and storing
    // it in the array D
    for (int i = 0; i < n; i++) {
        D[i] = A[i] - B[i];
    }

    // Sort the array D
    sort(D.begin(), D.end());

    // Variable to store the total
    // number of pairs that satisfy
    // the given condition
    long long total = 0;

    // Loop to iterate through the difference
    // array D and find the total number
    // of pairs of indices that follow the
    // given condition
    for (int i = n - 1; i >= 0; i--) {

        // If the value at the index i is positive,
        // then it remains positive for any pairs
        // with j such that j > i.
        if (D[i] > 0) {
            total += n - i - 1;
        }

        // If the value at that index is negative
        // then we need to find the index of the
        // value just greater than -D[i]
        else {
            int k = upper_bound(D.begin(),
                                D.end(), -D[i])
                    - D.begin();
            total += n - k;
        }
    }
    return total;
}

// Driver code
int main()
{
    int n = 5;
    vector<int> A;
    vector<int> B;

    A.push_back(4);
    A.push_back(8);
    A.push_back(2);
    A.push_back(6);
    A.push_back(2);

    B.push_back(4);
    B.push_back(5);
    B.push_back(4);
    B.push_back(1);
    B.push_back(3);

    cout << getPairs(A, B, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of indices pair
// such that pair sum from first Array
// is greater than second Array
import java.util.*;

class GFG{

// Function to get the number of pairs of indices
// {i, j} in the given two arrays A and B such that
// A[i] + A[j] > B[i] + B[j]
static long getPairs(Vector<Integer> A, Vector<Integer> B, int n)
{
    // Initializing the difference array D
    int []D = new int[n];

    // Computing the difference between the
    // elements at every index and storing
    // it in the array D
    for (int i = 0; i < n; i++)
    {
        D[i] = A.get(i) - B.get(i);
    }

    // Sort the array D
    Arrays.sort(D);

    // Variable to store the total
    // number of pairs that satisfy
    // the given condition
    long total = 0;

    // Loop to iterate through the difference
    // array D and find the total number
    // of pairs of indices that follow the
    // given condition
    for (int i = n - 1; i >= 0; i--) {

        // If the value at the index i is positive,
        // then it remains positive for any pairs
        // with j such that j > i.
        if (D[i] > 0) {
            total += n - i - 1;
        }

        // If the value at that index is negative
        // then we need to find the index of the
        // value just greater than -D[i]
        else {
            int k = upper_bound(D,0, D.length, -D[i]);
            total += n - k;
        }
    }
    return total;
}
static int upper_bound(int[] a, int low,
                        int high, int element)
{
    while(low < high){
        int middle = low + (high - low)/2;
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    Vector<Integer> A = new Vector<Integer>();
    Vector<Integer> B= new Vector<Integer>();

    A.add(4);
    A.add(8);
    A.add(2);
    A.add(6);
    A.add(2);

    B.add(4);
    B.add(5);
    B.add(4);
    B.add(1);
    B.add(3);

    System.out.print(getPairs(A, B, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the number of indices pair
# such that pair sum from first Array
# is greater than second Array
import bisect

# Function to get the number of pairs of indices
# {i, j} in the given two arrays A and B such that
# A[i] + A[j] > B[i] + B[j]
def getPairs(A,  B, n):

    # Initializing the difference array D
    D = [0]*(n)

    # Computing the difference between the
    # elements at every index and storing
    # it in the array D
    for i in range(n):
        D[i] = A[i] - B[i]

    # Sort the array D
    D.sort()

    # Variable to store the total
    # number of pairs that satisfy
    # the given condition
    total = 0

    # Loop to iterate through the difference
    # array D and find the total number
    # of pairs of indices that follow the
    # given condition
    for i in range(n - 1, -1, -1):

        # If the value at the index i is positive,
        # then it remains positive for any pairs
        # with j such that j > i.
        if (D[i] > 0):
            total += n - i - 1

        # If the value at that index is negative
        # then we need to find the index of the
        # value just greater than -D[i]
        else:
            k = bisect.bisect_right(D, -D[i], 0, len(D))
            total += n - k
    return total

# Driver code
if __name__ == "__main__":

    n = 5
    A = []
    B = []

    A.append(4);
    A.append(8);
    A.append(2);
    A.append(6);
    A.append(2);

    B.append(4);
    B.append(5);
    B.append(4);
    B.append(1);
    B.append(3);

    print(getPairs(A, B, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the number of indices pair
// such that pair sum from first Array
// is greater than second Array
using System;
using System.Collections.Generic;

class GFG{

// Function to get the number of pairs of indices
// {i, j} in the given two arrays A and B such that
// A[i] + A[j] > B[i] + B[j]
static long getPairs(List<int> A, List<int> B, int n)
{
    // Initializing the difference array D
    int []D = new int[n];

    // Computing the difference between the
    // elements at every index and storing
    // it in the array D
    for (int i = 0; i < n; i++)
    {
        D[i] = A[i] - B[i];
    }

    // Sort the array D
    Array.Sort(D);

    // Variable to store the total
    // number of pairs that satisfy
    // the given condition
    long total = 0;

    // Loop to iterate through the difference
    // array D and find the total number
    // of pairs of indices that follow the
    // given condition
    for (int i = n - 1; i >= 0; i--) {

        // If the value at the index i is positive,
        // then it remains positive for any pairs
        // with j such that j > i.
        if (D[i] > 0) {
            total += n - i - 1;
        }

        // If the value at that index is negative
        // then we need to find the index of the
        // value just greater than -D[i]
        else {
            int k = upper_bound(D,0, D.Length, -D[i]);
            total += n - k;
        }
    }
    return total;
}
static int upper_bound(int[] a, int low,
                        int high, int element)
{
    while(low < high){
        int middle = low + (high - low)/2;
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    List<int> A = new List<int>();
    List<int> B= new List<int>();

    A.Add(4);
    A.Add(8);
    A.Add(2);
    A.Add(6);
    A.Add(2);

    B.Add(4);
    B.Add(5);
    B.Add(4);
    B.Add(1);
    B.Add(3);

    Console.Write(getPairs(A, B, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript program to find the number of indices pair
// such that pair sum from first Array
// is greater than second Array

// Function to get the number of pairs of indices
// {i, j} in the given two arrays A and B such that
// A[i] + A[j] > B[i] + B[j]
function getPairs(A, B, n)
{
    // Initializing the difference array D
    let D = new Array(n);

    // Computing the difference between the
    // elements at every index and storing
    // it in the array D
    for (let i = 0; i < n; i++) {
        D[i] = A[i] - B[i];
    }

    // Sort the array D
    D.sort((a, b) => a - b);

    // Variable to store the total
    // number of pairs that satisfy
    // the given condition
    let total = 0;

    // Loop to iterate through the difference
    // array D and find the total number
    // of pairs of indices that follow the
    // given condition
    for (let i = n - 1; i >= 0; i--) {

        // If the value at the index i is positive,
        // then it remains positive for any pairs
        // with j such that j > i.
        if (D[i] > 0) {
            total += n - i - 1;
        }

        // If the value at that index is negative
        // then we need to find the index of the
        // value just greater than -D[i]
        else {
            let k = upper_bound(D, 0, D.length, -D[i])
            total += n - k;
        }
    }
    return total;
}

function upper_bound(a, low, high, element)
{
    while(low < high){
        let middle = low +  Math.floor((high - low)/2);
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver code

    let n = 5;
    let A = new Array();
    let B = new Array();

    A.push(4);
    A.push(8);
    A.push(2);
    A.push(6);
    A.push(2);

    B.push(4);
    B.push(5);
    B.push(4);
    B.push(1);
    B.push(3);

    document.write(getPairs(A, B, n))

// This code is contributed by gfgking
</script>
```

**Output:** 

```
7
```

**时间复杂度分析:**

*   数组的排序需要 **O(N * log(N))** 时间。
*   找到刚好大于特定值的索引所花费的时间是 **O(Log(N))** 。因为在最坏的情况下，可以对数组中的 **N** 元素执行此操作，所以此操作的整体时间复杂度为 **O(N * log(N))** 。
*   因此，整体时间复杂度为 **O(N * log(N))** 。