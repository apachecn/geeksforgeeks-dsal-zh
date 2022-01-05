# 排序数组上的交替异或运算

> 原文:[https://www . geesforgeks . org/alternate-xor-operations-on-sorted-array/](https://www.geeksforgeeks.org/alternate-xor-operations-on-sorted-array/)

给定一个数组 **arr[]** 和两个整数 **X** 和 **K** 。任务是对数组 **K** 次执行以下操作:

1.  对数组排序。
2.  将排序后的数组的每个替换元素与 **X** 异或，即 **arr[0]，arr[2]，arr[4]，…**

重复上述步骤 **K** 次后，打印修改后数组中的最大和最小元素。
**例:**

> **输入:** arr[] = {9，7，11，15，5}，K = 1，X = 2
> **输出:** 7 13
> 由于运算只需执行一次，
> 排序后的数组将是{5，7，9，11，15}
> 现在，对交替元素即 5，9 和 15 应用异或 2。
> {5 ^ 2，7，9 ^ 2，11，15 ^ 2}等于
> {7，7，11，11，13}
> **输入:** arr[] = {605，986}，K = 548，X = 569
> **输出:** 605 986

**方法:**不用在每次迭代中对数组进行排序，可以维护一个频率数组，该数组将存储数组中每个元素的频率。从 1 遍历到数组中的最大元素，可以按照排序的顺序处理元素，并且在每次操作之后，当替换元素与给定的整数异或时，可以调整相同元素的频率。有关更多详细信息，请查看编程实现。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

// Function to find the maximum and the
// minimum elements from the array after
// performing the given operation k times
void xorOnSortedArray(int arr[], int n, int k, int x)
{

    // To store the current sequence of elements
    int arr1[MAX + 1] = { 0 };

    // To store the next sequence of elements
    // after xoring with current elements
    int arr2[MAX + 1] = { 0 };
    int xor_val[MAX + 1];

    // Store the frequency of elements of arr[] in arr1[]
    for (int i = 0; i < n; i++)
        arr1[arr[i]]++;

    // Storing all precomputed XOR values so that
    // we don't have to do it again and again
    // as XOR is a costly operation
    for (int i = 0; i <= MAX; i++)
        xor_val[i] = i ^ x;

    // Perform the operations k times
    while (k--) {

        // The value of count decide on how many elements
        // we have to apply XOR operation
        int count = 0;
        for (int i = 0; i <= MAX; i++) {
            int store = arr1[i];

            // If current element is present in
            // the array to be modified
            if (arr1[i] > 0) {

                // Suppose i = m and arr1[i] = num, it means
                // 'm' appears 'num' times
                // If the count is even we have to perform
                // XOR operation on alternate 'm' starting
                // from the 0th index because count is even
                // and we have to perform XOR operations
                // starting with initial 'm'
                // Hence there will be ceil(num/2) operations on
                // 'm' that will change 'm' to xor_val[m] i.e. m^x
                if (count % 2 == 0) {
                    int div = ceil((float)arr1[i] / 2);

                    // Decrease the frequency of 'm' from arr1[]
                    arr1[i] = arr1[i] - div;

                    // Increase the frequency of 'm^x' in arr2[]
                    arr2[xor_val[i]] += div;
                }

                // If the count is odd we have to perform
                // XOR operation on alternate 'm' starting
                // from the 1st index because count is odd
                // and we have to leave the 0th 'm'
                // Hence there will be (num/2) XOR operations on
                // 'm' that will change 'm' to xor_val[m] i.e. m^x
                else if (count % 2 != 0) {
                    int div = arr1[i] / 2;
                    arr1[i] = arr1[i] - div;
                    arr2[xor_val[i]] += div;
                }
            }

            // Updating the count by frequency of
            // the current elements as we have
            // processed that many elements
            count = count + store;
        }

        // Updating arr1[] which will now store the
        // next sequence of elements
        // At this time, arr1[] stores the remaining
        // 'm' on which XOR was not performed and
        // arr2[] stores the frequency of 'm^x' i.e.
        // those 'm' on which operation was performed
        // Updating arr1[] with frequency of remaining
        // 'm' & frequency of 'm^x' from arr2[]
        // With help of arr2[], we prevent sorting of
        // the array again and again
        for (int i = 0; i <= MAX; i++) {
            arr1[i] = arr1[i] + arr2[i];

            // Resetting arr2[] for next iteration
            arr2[i] = 0;
        }
    }

    // Finding the maximum and the minimum element
    // from the modified array after the operations
    int min = INT_MAX;
    int max = INT_MIN;
    for (int i = 0; i <= MAX; i++) {
        if (arr1[i] > 0) {
            if (min > i)
                min = i;
            if (max < i)
                max = i;
        }
    }

    // Printing the max and the min element
    cout << min << " " << max << endl;
}

// Driver code
int main()
{
    int arr[] = { 605, 986 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 548, x = 569;

    xorOnSortedArray(arr, n, k, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static int MAX = 100000;

    // Function to find the maximum and the
    // minimum elements from the array after
    // performing the given operation k times
    public static void xorOnSortedArray(int[] arr, int n,
                                        int k, int x)
    {

        // To store the current sequence of elements
        int[] arr1 = new int[MAX + 1];

        // To store the next sequence of elements
        // after xoring with current elements
        int[] arr2 = new int[MAX + 1];
        int[] xor_val = new int[MAX + 1];

        // Store the frequency of elements
        // of arr[] in arr1[]
        for (int i = 0; i < n; i++)
            arr1[arr[i]]++;

        // Storing all precomputed XOR values so that
        // we don't have to do it again and again
        // as XOR is a costly operation
        for (int i = 0; i <= MAX; i++)
            xor_val[i] = i ^ x;

        // Perform the operations k times
        while (k-- > 0)
        {

            // The value of count decide on how many elements
            // we have to apply XOR operation
            int count = 0;
            for (int i = 0; i <= MAX; i++)
            {
                int store = arr1[i];

                // If current element is present in
                // the array to be modified
                if (arr1[i] > 0)
                {

                    // Suppose i = m and arr1[i] = num, it means
                    // 'm' appears 'num' times
                    // If the count is even we have to perform
                    // XOR operation on alternate 'm' starting
                    // from the 0th index because count is even
                    // and we have to perform XOR operations
                    // starting with initial 'm'
                    // Hence there will be ceil(num/2) operations on
                    // 'm' that will change 'm' to xor_val[m] i.e. m^x
                    if (count % 2 == 0)
                    {
                        int div = (int) Math.ceil(arr1[i] / 2);

                        // Decrease the frequency of 'm' from arr1[]
                        arr1[i] = arr1[i] - div;

                        // Increase the frequency of 'm^x' in arr2[]
                        arr2[xor_val[i]] += div;
                    }

                    // If the count is odd we have to perform
                    // XOR operation on alternate 'm' starting
                    // from the 1st index because count is odd
                    // and we have to leave the 0th 'm'
                    // Hence there will be (num/2) XOR operations on
                    // 'm' that will change 'm' to xor_val[m] i.e. m^x
                    else if (count % 2 != 0)
                    {
                        int div = arr1[i] / 2;
                        arr1[i] = arr1[i] - div;
                        arr2[xor_val[i]] += div;
                    }
                }

                // Updating the count by frequency of
                // the current elements as we have
                // processed that many elements
                count = count + store;
            }

            // Updating arr1[] which will now store the
            // next sequence of elements
            // At this time, arr1[] stores the remaining
            // 'm' on which XOR was not performed and
            // arr2[] stores the frequency of 'm^x' i.e.
            // those 'm' on which operation was performed
            // Updating arr1[] with frequency of remaining
            // 'm' & frequency of 'm^x' from arr2[]
            // With help of arr2[], we prevent sorting of
            // the array again and again
            for (int i = 0; i <= MAX; i++)
            {
                arr1[i] = arr1[i] + arr2[i];

                // Resetting arr2[] for next iteration
                arr2[i] = 0;
            }
        }

        // Finding the maximum and the minimum element
        // from the modified array after the operations
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i <= MAX; i++)
        {
            if (arr1[i] > 0)
            {
                if (min > i)
                    min = i;
                if (max < i)
                    max = i;
            }
        }

        // Printing the max and the min element
        System.out.println(min + " " + max);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 605, 986 };
        int n = arr.length;
        int k = 548, x = 569;
        xorOnSortedArray(arr, n, k, x);

    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 10000
import sys
from math import ceil, floor

# Function to find the maximum and the
# minimum elements from the array after
# performing the given operation k times
def xorOnSortedArray(arr, n, k, x):

    # To store the current sequence of elements
    arr1 = [0 for i in range(MAX + 1)]

    # To store the next sequence of elements
    # after xoring with current elements
    arr2 = [0 for i in range(MAX + 1)]
    xor_val = [0 for i in range(MAX + 1)]

    # Store the frequency of elements
    # of arr[] in arr1[]
    for i in range(n):
        arr1[arr[i]] += 1

    # Storing all precomputed XOR values
    # so that we don't have to do it
    # again and again as XOR is a costly operation
    for i in range(MAX + 1):
        xor_val[i] = i ^ x

    # Perform the operations k times
    while (k > 0):
        k -= 1

        # The value of count decide on
        # how many elements we have to
        # apply XOR operation
        count = 0
        for i in range(MAX + 1):
            store = arr1[i]

            # If current element is present in
            # the array to be modified
            if (arr1[i] > 0):

                # Suppose i = m and arr1[i] = num,
                # it means 'm' appears 'num' times
                # If the count is even we have to
                # perform XOR operation on alternate
                # 'm' starting from the 0th index because
                # count is even and we have to perform
                # XOR operations starting with initial 'm'
                # Hence there will be ceil(num/2)
                # operations on 'm' that will change
                # 'm' to xor_val[m] i.e. m^x
                if (count % 2 == 0):
                    div = arr1[i] // 2 + 1

                    # Decrease the frequency of
                    # 'm' from arr1[]
                    arr1[i] = arr1[i] - div

                    # Increase the frequency of
                    # 'm^x' in arr2[]
                    arr2[xor_val[i]] += div

                # If the count is odd we have to perform
                # XOR operation on alternate 'm' starting
                # from the 1st index because count is odd
                # and we have to leave the 0th 'm'
                # Hence there will be (num/2) XOR operations on
                # 'm' that will change 'm' to xor_val[m] i.e. m^x
                elif (count % 2 != 0):
                    div = arr1[i] // 2
                    arr1[i] = arr1[i] - div
                    arr2[xor_val[i]] += div

            # Updating the count by frequency of
            # the current elements as we have
            # processed that many elements
            count = count + store

        # Updating arr1[] which will now store the
        # next sequence of elements
        # At this time, arr1[] stores the remaining
        # 'm' on which XOR was not performed and
        # arr2[] stores the frequency of 'm^x' i.e.
        # those 'm' on which operation was performed
        # Updating arr1[] with frequency of remaining
        # 'm' & frequency of 'm^x' from arr2[]
        # With help of arr2[], we prevent sorting of
        # the array again and again
        for i in range(MAX+1):
            arr1[i] = arr1[i] + arr2[i]

            # Resetting arr2[] for next iteration
            arr2[i] = 0

    # Finding the maximum and the minimum element
    # from the modified array after the operations
    mn = sys.maxsize
    mx = -sys.maxsize-1
    for i in range(MAX + 1):
        if (arr1[i] > 0):
            if (mn > i):
                mn = i
            if (mx < i):
                mx = i

    # Printing the max and the min element
    print(mn,mx)

# Driver code
if __name__ == '__main__':
    arr = [605, 986]
    n = len(arr)
    k = 548
    x = 569

    xorOnSortedArray(arr, n, k, x)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MAX = 100000;

    // Function to find the maximum and the
    // minimum elements from the array after
    // performing the given operation k times
    public static void xorOnSortedArray(int[] arr, int n,
                                        int k, int x)
    {

        // To store the current sequence of elements
        int[] arr1 = new int[MAX + 1];

        // To store the next sequence of elements
        // after xoring with current elements
        int[] arr2 = new int[MAX + 1];
        int[] xor_val = new int[MAX + 1];

        // Store the frequency of elements
        // of arr[] in arr1[]
        for (int i = 0; i < n; i++)
            arr1[arr[i]]++;

        // Storing all precomputed XOR values so that
        // we don't have to do it again and again
        // as XOR is a costly operation
        for (int i = 0; i <= MAX; i++)
            xor_val[i] = i ^ x;

        // Perform the operations k times
        while (k-- > 0)
        {

            // The value of count decides on
            // how many elements we have to
            // apply XOR operation
            int count = 0;
            for (int i = 0; i <= MAX; i++)
            {
                int store = arr1[i];

                // If current element is present in
                // the array to be modified
                if (arr1[i] > 0)
                {

                    // Suppose i = m and arr1[i] = num,
                    // it means 'm' appears 'num' times
                    // If the count is even we have to perform
                    // XOR operation on alternate 'm' starting
                    // from the 0th index because count is even
                    // and we have to perform XOR operations
                    // starting with initial 'm'
                    // Hence there will be ceil(num/2) operations on
                    // 'm' that will change 'm' to xor_val[m] i.e. m^x
                    if (count % 2 == 0)
                    {
                        int div = (int) Math.Ceiling((double)(arr1[i] / 2));

                        // Decrease the frequency of 'm' from arr1[]
                        arr1[i] = arr1[i] - div;

                        // Increase the frequency of 'm^x' in arr2[]
                        arr2[xor_val[i]] += div;
                    }

                    // If the count is odd we have to perform
                    // XOR operation on alternate 'm' starting
                    // from the 1st index because count is odd
                    // and we have to leave the 0th 'm'
                    // Hence there will be (num/2) XOR operations on
                    // 'm' that will change 'm' to xor_val[m] i.e. m^x
                    else if (count % 2 != 0)
                    {
                        int div = arr1[i] / 2;
                        arr1[i] = arr1[i] - div;
                        arr2[xor_val[i]] += div;
                    }
                }

                // Updating the count by frequency of
                // the current elements as we have
                // processed that many elements
                count = count + store;
            }

            // Updating arr1[] which will now store the
            // next sequence of elements
            // At this time, arr1[] stores the remaining
            // 'm' on which XOR was not performed and
            // arr2[] stores the frequency of 'm^x' i.e.
            // those 'm' on which operation was performed
            // Updating arr1[] with frequency of remaining
            // 'm' & frequency of 'm^x' from arr2[]
            // With help of arr2[], we prevent sorting of
            // the array again and again
            for (int i = 0; i <= MAX; i++)
            {
                arr1[i] = arr1[i] + arr2[i];

                // Resetting arr2[] for next iteration
                arr2[i] = 0;
            }
        }

        // Finding the maximum and the minimum element
        // from the modified array after the operations
        int min = int.MaxValue;
        int max = int.MinValue;
        for (int i = 0; i <= MAX; i++)
        {
            if (arr1[i] > 0)
            {
                if (min > i)
                    min = i;
                if (max < i)
                    max = i;
            }
        }

        // Printing the max and the min element
        Console.WriteLine(min + " " + max);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 605, 986 };
        int n = arr.Length;
        int k = 548, x = 569;
        xorOnSortedArray(arr, n, k, x);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const MAX = 100000;

// Function to find the maximum and the
// minimum elements from the array after
// performing the given operation k times
function xorOnSortedArray(arr, n, k, x)
{

    // To store the current sequence of elements
    let arr1 = new Array(MAX + 1).fill(0);

    // To store the next sequence of elements
    // after xoring with current elements
    let arr2 = new Array(MAX + 1).fill(0);
    let xor_val = new Array(MAX + 1);

    // Store the frequency of elements of arr[] in arr1[]
    for (let i = 0; i < n; i++)
        arr1[arr[i]]++;

    // Storing all precomputed XOR values so that
    // we don't have to do it again and again
    // as XOR is a costly operation
    for (let i = 0; i <= MAX; i++)
        xor_val[i] = i ^ x;

    // Perform the operations k times
    while (k--) {

        // The value of count decide on how many elements
        // we have to apply XOR operation
        let count = 0;
        for (let i = 0; i <= MAX; i++) {
            let store = arr1[i];

            // If current element is present in
            // the array to be modified
            if (arr1[i] > 0) {

                // Suppose i = m and arr1[i] = num, it means
                // 'm' appears 'num' times
                // If the count is even we have to perform
                // XOR operation on alternate 'm' starting
                // from the 0th index because count is even
                // and we have to perform XOR operations
                // starting with initial 'm'
                // Hence there will be ceil(num/2) operations on
                // 'm' that will change 'm' to xor_val[m] i.e. m^x
                if (count % 2 == 0) {
                    let div = Math.ceil(arr1[i] / 2);

                    // Decrease the frequency of 'm' from arr1[]
                    arr1[i] = arr1[i] - div;

                    // Increase the frequency of 'm^x' in arr2[]
                    arr2[xor_val[i]] += div;
                }

                // If the count is odd we have to perform
                // XOR operation on alternate 'm' starting
                // from the 1st index because count is odd
                // and we have to leave the 0th 'm'
                // Hence there will be (num/2) XOR operations on
                // 'm' that will change 'm' to xor_val[m] i.e. m^x
                else if (count % 2 != 0) {
                    let div = parseInt(arr1[i] / 2);
                    arr1[i] = arr1[i] - div;
                    arr2[xor_val[i]] += div;
                }
            }

            // Updating the count by frequency of
            // the current elements as we have
            // processed that many elements
            count = count + store;
        }

        // Updating arr1[] which will now store the
        // next sequence of elements
        // At this time, arr1[] stores the remaining
        // 'm' on which XOR was not performed and
        // arr2[] stores the frequency of 'm^x' i.e.
        // those 'm' on which operation was performed
        // Updating arr1[] with frequency of remaining
        // 'm' & frequency of 'm^x' from arr2[]
        // With help of arr2[], we prevent sorting of
        // the array again and again
        for (let i = 0; i <= MAX; i++) {
            arr1[i] = arr1[i] + arr2[i];

            // Resetting arr2[] for next iteration
            arr2[i] = 0;
        }
    }

    // Finding the maximum and the minimum element
    // from the modified array after the operations
    let min = Number.MAX_VALUE;
    let max = Number.MIN_VALUE;
    for (let i = 0; i <= MAX; i++) {
        if (arr1[i] > 0) {
            if (min > i)
                min = i;
            if (max < i)
                max = i;
        }
    }

    // Printing the max and the min element
    document.write(min + " " + max);
}

// Driver code
    let arr = [ 605, 986 ];
    let n = arr.length;
    let k = 548, x = 569;

    xorOnSortedArray(arr, n, k, x);

</script>
```

**Output:** 

```
605 986
```

时间复杂度:0(n+k * MAX)

辅助空间:0(最大)