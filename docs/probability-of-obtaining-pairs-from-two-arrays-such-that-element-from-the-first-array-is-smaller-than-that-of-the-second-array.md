# 从两个阵列获得配对的概率，使得第一个阵列的元素小于第二个阵列的元素

> 原文:[https://www . geeksforgeeks . org/从两个数组中获取对的概率-这样第一个数组中的元素比第二个数组中的元素小/](https://www.geeksforgeeks.org/probability-of-obtaining-pairs-from-two-arrays-such-that-element-from-the-first-array-is-smaller-than-that-of-the-second-array/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr 1【】**和**arr 2【】**，任务是分别从**arr 1【】**和**arr 2【】**中找出随机选择这两个数字的概率，使得第一个选择的元素严格小于第二个选择的元素。

**示例:**

> **输入:** arr1[] = {3，2，1，1}，arr2[] = {1，2，5，2}
> **输出:** 0.5
> **解释:**
> 以下是从两个数组中选择数组元素的方法第一个数小于第二个数:
> 
> 1.  选择 arr1[0]，有 1 种方法可以选择 arr2[]中的元素。
> 2.  选择 arr1[1]，在 arr2[]中有 1 种选择元素的方式。
> 3.  选择 arr1[2]，在 arr2[]中有 3 种选择元素的方式。
> 4.  选择 arr1[3]，在 arr 2[3]中有 3 种选择元素的方式
> 
> 因此，总共有(3 + 3 + 1 + 1 = 8)种从满足条件的两个数组中选择元素的方式。因此，概率为(8/(4*4)) = 0.5。
> 
> **输入:** arr1[] = {5，2，6，1}，arr2[] = {1，6，10，1 }
> T3】输出: 0.4375

**天真方法:**给定的问题可以基于以下观察来解决:

*   想法是使用[条件概率的概念。](https://www.geeksforgeeks.org/conditional-probability/)从数组**arr 1【】**中选择元素的概率为 **1/N.**
*   现在假设 **X** 是**arr 2【】**中的元素数大于**arr 1【】**中的所选元素，那么从**arr 2【】**中选择一个这样的元素的概率是 **X/M** 。
*   因此，选择两个元素使得第一个元素小于第二个所选元素的概率是**arr 1【】**中每个元素的 **(1/N)*(X/M)** 之和。

按照以下步骤解决问题:

*   初始化一个变量，比如说**将**设为 **0** 来存储结果概率。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr 1【】**并执行以下步骤:
    *   [通过遍历数组**arr 2【】**找到**arr 2【】**中大于**arr 1【I】**T5 的元素个数，然后用它递增 **res** 。](https://www.geeksforgeeks.org/count-of-elements-in-first-array-greater-than-second-array-with-each-element-considered-only-once/)
    *   将 **res** 的值更新为 **res = res/N*M** 。
*   完成以上步骤后，打印 **res** 的值作为合成概率。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find  probability
// such that x < y and X belongs to
// arr1[] and Y belongs to arr2[]
double probability(vector<int> arr1,vector<int> arr2)
{
    // Stores the length of arr1
    int N = arr1.size();

    // Stores the length of arr2
    int M = arr2.size();

    // Stores the result
    double res = 0;

    // Traverse the arr1[]
    for (int i = 0; i < N; i++) {

        // Stores the count of
        // elements in arr2 that
        // are greater than arr[i]
        int y = 0;

        // Traverse the arr2[]
        for (int j = 0; j < M; j++) {

            // If arr2[j] is greater
            // than arr1[i]
            if (arr2[j] > arr1[i])
                y++;
        }

        // Increment res by y
        res += y;
    }

    // Update the value of res
    res = (double)res / (double)(N * M);

    // Return resultant probability
    return res;
}

// Driver Code
int main()
{
    vector<int> arr1 = { 5, 2, 6, 1 };
    vector<int> arr2 = { 1, 6, 10, 1 };
    cout<<probability(arr1, arr2);
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find  probability
    // such that x < y and X belongs to
    // arr1[] and Y belongs to arr2[]
    static double probability(int[] arr1,
                              int[] arr2)
    {
        // Stores the length of arr1
        int N = arr1.length;

        // Stores the length of arr2
        int M = arr2.length;

        // Stores the result
        double res = 0;

        // Traverse the arr1[]
        for (int i = 0; i < N; i++) {

            // Stores the count of
            // elements in arr2 that
            // are greater than arr[i]
            int y = 0;

            // Traverse the arr2[]
            for (int j = 0; j < M; j++) {

                // If arr2[j] is greater
                // than arr1[i]
                if (arr2[j] > arr1[i])
                    y++;
            }

            // Increment res by y
            res += y;
        }

        // Update the value of res
        res = (double)res / (double)(N * M);

        // Return resultant probability
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr1 = { 5, 2, 6, 1 };
        int[] arr2 = { 1, 6, 10, 1 };
        System.out.println(
            probability(arr1, arr2));
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find  probability
# such that x < y and X belongs to
# arr1[] and Y belongs to arr2[]
def probability(arr1, arr2):

    # Stores the length of arr1
    N = len(arr1)

    # Stores the length of arr2
    M = len(arr2)

    # Stores the result
    res = 0

    # Traverse the arr1[]
    for i in range(N):

        # Stores the count of
        # elements in arr2 that
        # are greater than arr[i]
        y = 0

        # Traverse the arr2[]
        for j in range(M):

            # If arr2[j] is greater
            # than arr1[i]
            if (arr2[j] > arr1[i]):
                y += 1

        # Increment res by y
        res += y

    # Update the value of res
    res = res / (N * M)

    # Return resultant probability
    return res

# Driver Code
if __name__ == "__main__":

    arr1 = [5, 2, 6, 1]
    arr2 = [1, 6, 10, 1]
    print(probability(arr1, arr2))

    # This code is contributed by ukasp.
```

## C#

```
//C# program for the above approach
using System;

class GFG {

    // Function to find  probability
    // such that x < y and X belongs to
    // arr1[] and Y belongs to arr2[]
    static double probability(int[] arr1, int[] arr2)
    {
        // Stores the length of arr1
        int N = arr1.Length;

        // Stores the length of arr2
        int M = arr2.Length;

        // Stores the result
        double res = 0;

        // Traverse the arr1[]
        for (int i = 0; i < N; i++) {

            // Stores the count of
            // elements in arr2 that
            // are greater than arr[i]
            int y = 0;

            // Traverse the arr2[]
            for (int j = 0; j < M; j++) {

                // If arr2[j] is greater
                // than arr1[i]
                if (arr2[j] > arr1[i])
                    y++;
            }

            // Increment res by y
            res += y;
        }

        // Update the value of res
        res = (double)res / (double)(N * M);

        // Return resultant probability
        return res;
    }

    // Driver Code
    static void Main()
    {
        int[] arr1 = { 5, 2, 6, 1 };
        int[] arr2 = { 1, 6, 10, 1 };
        Console.WriteLine(probability(arr1, arr2));
    }
}

// This code is contributed by SoumikMondal.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find  probability
    // such that x < y and X belongs to
    // arr1[] and Y belongs to arr2[]
    function probability(arr1, arr2)
    {
        // Stores the length of arr1
        let N = arr1.length;

        // Stores the length of arr2
        let M = arr2.length;

        // Stores the result
        let res = 0;

        // Traverse the arr1[]
        for (let i = 0; i < N; i++) {

            // Stores the count of
            // elements in arr2 that
            // are greater than arr[i]
            let y = 0;

            // Traverse the arr2[]
            for (let j = 0; j < M; j++) {

                // If arr2[j] is greater
                // than arr1[i]
                if (arr2[j] > arr1[i])
                    y++;
            }

            // Increment res by y
            res += y;
        }

        // Update the value of res
        res = (res / (N * M));

        // Return resultant probability
        return res;
    }

// Driver Code

     let arr1 = [ 5, 2, 6, 1 ];
     let arr2 = [ 1, 6, 10, 1 ];
     document.write(
            probability(arr1, arr2));

</script>
```

**Output:** 

```
0.4375
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效途径:**使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以优化上述途径。按照以下步骤解决问题:

*   初始化一个变量，说 **res** 为 **0** ，存储合成概率。
*   [按升序排列数组。](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr 1【】**并执行以下步骤:
    *   [用二分搜索法求**arr 2【】**大于**arr 1【I】**T5】的元素个数，然后用其递增 **res** 。](https://www.geeksforgeeks.org/element-1st-array-count-elements-less-equal-2nd-array/)
    *   将 **res** 的值更新为**RES = RES/N * m**
*   完成以上步骤后，打印 **res** 作为合成概率。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int countGreater(int* arr, int k);

// Function to find  probability
// such that x < y and X belongs
// to arr1[] & Y belongs to arr2[]
float probability(int* arr1,
                          int* arr2)
{
    // Stores the length of arr1
    int N = 4;

    // Stores the length of arr2
    int M = 4;

    // Stores the result
    float res = 0;

    // Sort the arr2[] in the
    // ascending order
    sort(arr2, arr2 + M);

    // Traverse the arr1[]
    for (int i = 0; i < N; i++) {

        // Stores the count of
        // elements in arr2 that
        // are greater than arr[i]
        int y = countGreater(
            arr2, arr1[i]);

        // Increment res by y
        res += y;
    }

    // Update the resultant
    // probability
    res = res / (N * M);

    // Return the result
    return res;
}

// Function to return the count
// of elements from the array
// which are greater than k
int countGreater(int* arr,
                        int k)
{
    int n = 4;
    int l = 0;
    int r = n - 1;

    // Stores the index of the
    // leftmost element from the
    // array which is at least k
    int leftGreater = n;

    // Finds number of elements
    // greater than k
    while (l <= r) {
        int m = l + (r - l) / 2;

        // If mid element is at least
        // K, then update the value
        // of leftGreater and r
        if (arr[m] > k) {

            // Update leftGreater
            leftGreater = m;

            // Update r
            r = m - 1;
        }

        // If mid element is
        // at most K, then
        // update the value of l
        else
            l = m + 1;
    }

    // Return the count of
    // elements greater than k
    return (n - leftGreater);
}

// Driver Code
int main()
{
    int arr1[] = { 5, 2, 6, 1 };
    int arr2[] = { 1, 6, 10, 1 };
    cout << probability(arr1, arr2);
    return 0;
}

// This code is contributed by Shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find  probability
    // such that x < y and X belongs
    // to arr1[] & Y belongs to arr2[]
    static double probability(int[] arr1,
                              int[] arr2)
    {
        // Stores the length of arr1
        int N = arr1.length;

        // Stores the length of arr2
        int M = arr2.length;

        // Stores the result
        double res = 0;

        // Sort the arr2[] in the
        // ascending order
        Arrays.sort(arr2);

        // Traverse the arr1[]
        for (int i = 0; i < N; i++) {

            // Stores the count of
            // elements in arr2 that
            // are greater than arr[i]
            int y = countGreater(
                arr2, arr1[i]);

            // Increment res by y
            res += y;
        }

        // Update the resultant
        // probability
        res = (double)res / (double)(N * M);

        // Return the result
        return res;
    }

    // Function to return the count
    // of elements from the array
    // which are greater than k
    static int countGreater(int[] arr,
                            int k)
    {
        int n = arr.length;
        int l = 0;
        int r = n - 1;

        // Stores the index of the
        // leftmost element from the
        // array which is at least k
        int leftGreater = n;

        // Finds number of elements
        // greater than k
        while (l <= r) {
            int m = l + (r - l) / 2;

            // If mid element is at least
            // K, then update the value
            // of leftGreater and r
            if (arr[m] > k) {

                // Update leftGreater
                leftGreater = m;

                // Update r
                r = m - 1;
            }

            // If mid element is
            // at most K, then
            // update the value of l
            else
                l = m + 1;
        }

        // Return the count of
        // elements greater than k
        return (n - leftGreater);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr1 = { 5, 2, 6, 1 };
        int[] arr2 = { 1, 6, 10, 1 };
        System.out.println(
            probability(arr1, arr2));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find  probability
# such that x < y and X belongs
# to arr1[] & Y belongs to arr2[]
def probability(arr1, arr2):

    # Stores the length of arr1
    n = len(arr1)

    # Stores the length of arr2
    m = len(arr2)

    # Stores the result
    res = 0

    # Sort the arr2[] in the
    # ascending order
    arr2.sort()

    # Traverse the arr1[]
    for i in range(n):

        # Stores the count of
        # elements in arr2 that
        # are greater than arr[i]
        y = countGreater(arr2, arr1[i])

        # Increment res by y
        res += y

    # Update the resultant
    # probability
    res /= (n * m)

    # Return the result
    return res

# Function to return the count
# of elements from the array
# which are greater than k
def countGreater(arr, k):

    n = len(arr)
    l = 0
    r = n - 1

    # Stores the index of the
    # leftmost element from the
    # array which is at least k
    leftGreater = n

    # Finds number of elements
    # greater than k
    while l <= r:
        m = (l + r) // 2

        # If mid element is at least
        # K, then update the value
        # of leftGreater and r
        if (arr[m] > k):

            # Update leftGreater
            leftGreater = m

            # Update r
            r = m - 1

        # If mid element is
        # at most K, then
        # update the value of l
        else:
            l = m + 1

    # Return the count of
    # elements greater than k
    return n - leftGreater

# Driver code
if __name__ == '__main__':

    arr1 = [ 5, 2, 6, 1 ]
    arr2 = [ 1, 6, 10, 1 ]

    print(probability(arr1, arr2))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;
class GFG {

   // Function to find  probability
    // such that x < y and X belongs
    // to arr1[] & Y belongs to arr2[]
    static double probability(int[] arr1,
                              int[] arr2)
    {

        // Stores the length of arr1
        int N = arr1.Length;

        // Stores the length of arr2
        int M = arr2.Length;

        // Stores the result
        double res = 0;

        // Sort the arr2[] in the
        // ascending order
        Array.Sort(arr2);

        // Traverse the arr1[]
        for (int i = 0; i < N; i++) {

            // Stores the count of
            // elements in arr2 that
            // are greater than arr[i]
            int y = countGreater(
                arr2, arr1[i]);

            // Increment res by y
            res += y;
        }

        // Update the resultant
        // probability
        res = (double)res / (double)(N * M);

        // Return the result
        return res;
    }

    // Function to return the count
    // of elements from the array
    // which are greater than k
    static int countGreater(int[] arr,
                            int k)
    {
        int n = arr.Length;
        int l = 0;
        int r = n - 1;

        // Stores the index of the
        // leftmost element from the
        // array which is at least k
        int leftGreater = n;

        // Finds number of elements
        // greater than k
        while (l <= r) {
            int m = l + (r - l) / 2;

            // If mid element is at least
            // K, then update the value
            // of leftGreater and r
            if (arr[m] > k) {

                // Update leftGreater
                leftGreater = m;

                // Update r
                r = m - 1;
            }

            // If mid element is
            // at most K, then
            // update the value of l
            else
                l = m + 1;
        }

        // Return the count of
        // elements greater than k
        return (n - leftGreater);
    }

    // Driver code
    public static void Main()
    {
       int[] arr1 = { 5, 2, 6, 1 };
        int[] arr2 = { 1, 6, 10, 1 };
        Console.Write(
            probability(arr1, arr2));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find  probability
// such that x < y and X belongs
// to arr1[] & Y belongs to arr2[]
function probability(arr1, arr2)
{
    // Stores the length of arr1
    var N = 4;

    // Stores the length of arr2
    var M = 4;

    // Stores the result
    var res = 0;

    // Sort the arr2[] in the
    // ascending order
    arr2.sort(function(a, b) {
        return a - b;
    });

    // Traverse the arr1[]
    for (var i = 0; i < N; i++) {

        // Stores the count of
        // elements in arr2 that
        // are greater than arr[i]
        var y = countGreater( arr2, arr1[i]);

        // Increment res by y
        res += y;
    }

    // Update the resultant
    // probability
    res = res / (N * M);

    // Return the result
    return res;
}

// Function to return the count
// of elements from the array
// which are greater than k
function countGreater(arr, k)
{
    var n = 4;
    var l = 0;
    var r = n - 1;

    // Stores the index of the
    // leftmost element from the
    // array which is at least k
    var leftGreater = n;

    // Finds number of elements
    // greater than k
    while (l <= r) {
        var m = Math.floor(l + (r - l) / 2);

        // If mid element is at least
        // K, then update the value
        // of leftGreater and r
        if (arr[m] > k) {

            // Update leftGreater
            leftGreater = m;

            // Update r
            r = m - 1;

        }

        // If mid element is
        // at most K, then
        // update the value of l
        else
            l = m + 1;

    }

    // Return the count of
    // elements greater than k
    return n - leftGreater;
}

// Driver Code
var arr1 = [ 5, 2, 6, 1 ];
var arr2 = [ 1, 6, 10, 1 ];
document.write(probability(arr1, arr2));

// This code is contributed by Shubhamsingh10
</script>
```

**Output:** 

```
0.4375
```

***时间复杂度:** O(N * log M)*
***辅助空间:** O(1)*