# 计算数组中正和的对的数量

> 原文:[https://www . geeksforgeeks . org/count-数组正和对数/](https://www.geeksforgeeks.org/count-number-of-pairs-with-positive-sum-in-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算正和的对的数量。

**示例:**

> **输入:** arr[] = {-7，-1，3，2}
> **输出:** 3
> **说明:**
> 正和的对是:{-1，3}、{-1，2}、{3，2}。
> 
> **输入:** arr[] = {-4，-2，5}
> **输出:** 2
> **说明:**
> 正和的对是:{-4，5}、{-2，5}。

**天真法:**
天真法是遍历每个元素，检查[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中是否还有另一个数字**arr【】**可以加进去，给出正和与否。

以下是上述方法的实现:

## C++

```
// Naive approach to count pairs
// with positive sum.
#include <bits/stdc++.h>
using namespace std;

// Returns number of pairs in
// arr[0..n-1] with positive sum
int CountPairs(int arr[], int n)
{
    // Initialize result
    int count = 0;

    // Consider all possible pairs
    // and check their sums
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // If arr[i] & arr[j]
            // form valid pair
            if (arr[i] + arr[j] > 0)
                count += 1;
        }
    }

    return count;
}

// Driver's Code
int main()
{
    int arr[] = { -7, -1, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to find the
    // count of pairs
    cout << CountPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG 
{

    // Naive approach to count pairs
    // with positive sum.

    // Returns number of pairs in
    // arr[0..n-1] with positive sum
    static int CountPairs(int arr[], int n)
    {
        // Initialize result
        int count = 0;

        // Consider all possible pairs
        // and check their sums
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                // If arr[i] & arr[j]
                // form valid pair
                if (arr[i] + arr[j] > 0)
                    count += 1;
            }
        }

        return count;
    }

    // Driver's Code
    public static void main (String[] args)
    {
        int []arr = { -7, -1, 3, 2 };
        int n = arr.length;

        // Function call to find the
        // count of pairs
        System.out.println(CountPairs(arr, n));
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Naive approach to count pairs
# with positive sum.

# Returns number of pairs in
# arr[0..n-1] with positive sum
def CountPairs(arr, n) :
    # Initialize result
    count = 0;

    # Consider all possible pairs
    # and check their sums
    for i in range(n) :
        for j in range( i + 1, n) :

            # If arr[i] & arr[j]
            # form valid pair
            if (arr[i] + arr[j] > 0) :
                count += 1;

    return count;

# Driver's Code
if __name__ == "__main__" :

    arr = [ -7, -1, 3, 2 ];
    n = len(arr);

    # Function call to find the
    # count of pairs
    print(CountPairs(arr, n));

# This code is contributed by Yash_R
```

**Output:**

```
3

```

**时间复杂度:** O(N <sup>2</sup> )

**有效方法:**
想法是使用[两点技巧](https://www.geeksforgeeks.org/two-pointers-technique/)。以下是步骤:

1.  按递增顺序排列给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**。
2.  拿两个指针。一个代表第一个元素，第二个代表排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的最后一个元素。
3.  如果这些指针上的元素之和大于 0，那么指针之间的差将给出第二个指针上的元素的正和对的计数。将第二个指针减少 1。
4.  否则将第一个指针增加 1。
5.  重复上面的步骤，直到两个指针相互会聚。

以下是上述方法的实现:

## C++

```
// C++ program to count the
// pairs with positive sum
#include <bits/stdc++.h>
using namespace std;

// Returns number of pairs
// in arr[0..n-1] with
// positive sum
int CountPairs(int arr[], int n)
{
    // Sort the array in
    // increasing order
    sort(arr, arr + n);

    // Intialise result
    int count = 0;

    // Intialise first and
    // second pointer
    int l = 0, r = n - 1;

    // Till the pointers
    // doesn't converge
    // traverse array to
    // count the pairs
    while (l < r) {

        // If sum of arr[i] &&
        // arr[j] > 0, then the
        // count of pairs with
        // positive sum is the
        // difference between
        // the two pointers
        if (arr[l] + arr[r] > 0) {

            // Increase the count
            count += (r - l);
            r--;
        }
        else {
            l++;
        }
    }
    return count;
}

// Driver's Code
int main()
{
    int arr[] = { -7, -1, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to count
    // the pairs with positive
    // sum
    cout << CountPairs(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to count the 
# pairs with positive sum 

# Returns number of pairs 
# in arr[0..n-1] with 
# positive sum 
def CountPairs(arr, n) : 

    # Sort the array in 
    # increasing order 
    arr.sort()

    # Intialise result 
    count = 0; 

    # Intialise first and 
    # second pointer 
    l = 0; r = n - 1; 

    # Till the pointers 
    # doesn't converge 
    # traverse array to 
    # count the pairs 
    while (l < r) :

        # If sum of arr[i] && 
        # arr[j] > 0, then the 
        # count of pairs with 
        # positive sum is the 
        # difference between 
        # the two pointers 
        if (arr[l] + arr[r] > 0) :

            # Increase the count 
            count += (r - l); 
            r -= 1; 

        else :
            l += 1; 

    return count; 

# Driver's Code 
if __name__ == "__main__" : 

    arr = [ -7, -1, 3, 2 ]; 
    n = len(arr); 

    # Function call to count 
    # the pairs with positive 
    # sum 
    print(CountPairs(arr, n)); 

# This code is contributed by Yash_R
```

**Output:**

```
3

```

**时间复杂度:** O(N*log N)