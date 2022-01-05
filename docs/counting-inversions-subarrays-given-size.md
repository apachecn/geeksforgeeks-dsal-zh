# 计数给定大小的所有子阵列中的反转

> 原文:[https://www . geesforgeks . org/counting-inversion-subarrays-给定大小/](https://www.geeksforgeeks.org/counting-inversions-subarrays-given-size/)

给定一个数组和一个整数 k，计算大小为 k 的所有子数组中的所有逆序。
**示例:**

```
Input : a[] = {7, 3, 2, 4, 1}, 
        k = 3;
Output : 6
Explanation: subarrays of size 3 are - 
{7, 3, 2}
{3, 2, 4}
{2, 4, 1} 
and there inversion count are 3, 1, 2 
respectively. So, total number of 
inversions are  6.
```

强烈建议使用 BIT
引用数组中的[求逆计数，求逆计数的过程与上面链接的文章相同。首先，我们使用 BIT 计算阵列中前 k 个(k 是给定的子阵列大小)元素的反转。在此之后，对于每个下一个子阵列，我们减去上一个子阵列的第一个元素的反转，并加上上一个子阵列中未包含的下一个元素的反转。重复该过程，直到处理完最后一个子阵列。在上面的例子中，这个算法是这样工作的-](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/) 

```
a[] = {7, 3, 2, 4, 1}, 
  k = 3;

Inversion are counted for first subarray 
A = {7, 3, 2} Let this be equal to invcount_A.

For counting the inversion of subarray B we 
subtract the inversion of first element of A,
from invcount_A and add inversions of 4 (last 
element of B) in the subarray B.
So, invcount_B = invcount_A - 2 + 0
               = 3 - 2 + 0
               = 1

Same process is repeated for next subarray
and sum of all inversion count is the answer.  
```

## C++

```
// C++ program to count inversions in all sub arrays
// of size k using Binary Indexed Tree
#include <bits/stdc++.h>
using namespace std;

// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[].
int getSum(int BITree[], int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0) {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at
// given index in BITree.  The given value 'val' is
// added to BITree[i] and all of its ancestors in
// tree.
void updateBIT(int BITree[], int n, int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n) {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent
        // in update View
        index += index & (-index);
    }
}

// Converts an array to an array with values from 1 to n
// and relative order of smaller and greater elements
// remains same.  For example, {7, -90, 100, 1} is
// converted to {3, 1, 4, 2 }
void convert(int arr[], int n)
{
    // Create a copy of arrp[] in temp and sort
    // the temp array in increasing order
    int temp[n];
    for (int i = 0; i < n; i++)
        temp[i] = arr[i];
    sort(temp, temp + n);

    // Traverse all array elements
    for (int i = 0; i < n; i++) {

        // lower_bound() Returns pointer to
        //  the first element greater than
        // or equal to arr[i]
        arr[i] = lower_bound(temp, temp + n,
                         arr[i]) - temp + 1;
    }
}

// Returns inversion count of all subarray
// of size k in arr[0..n-1]
int getInvCount(int arr[], int k, int n)
{
    int invcount = 0; // Initialize result

    // Convert arr[] to an array with values from
    // 1 to n and relative order of smaller and
    // greater elements remains same.  For example,
    // {7, -90, 100, 1} is converted to {3, 1, 4, 2 }
    convert(arr, n);

    // Create a BIT with size equal to maxElement+1
    // (Extra one is used so that elements can be
    // directly be used as index)
    int BIT[n + 1];
    for (int i = 1; i <= n; i++)
        BIT[i] = 0;

    // Get inversion count of first subarray
    for (int i = k - 1; i >= 0; i--) {

        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    // now calculate the inversion of all other subarrays
    int ans = invcount;
    int i = 0, j = k, icnt = 0, jcnt = 0;
    while (j <= n - 1) {

        // calculate value of inversion count of first element
        // in previous subarray
        icnt = getSum(BIT, arr[i] - 1);
        updateBIT(BIT, n, arr[i], -1);

        // calculating inversion count of last element in the
        // current subarray
        jcnt = getSum(BIT, n) - getSum(BIT, arr[j]);
        updateBIT(BIT, n, arr[j], 1);

        // calculating inversion count of current subarray
        invcount = invcount - icnt + jcnt;

        // adding current inversion to the answer
        ans = ans + invcount;
        i++, j++;
    }
    return ans;
}
int main()
{
    int arr[] = { 7, 3, 2, 4, 1 };
    int k = 3;
    int n = sizeof(arr) / sizeof(int);
    cout << "Number of inversions in all "
         "subarrays of size " << k <<" are : "
         << getInvCount(arr, k, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count inversions in all sub arrays
// of size k using Binary Indexed Tree
import java.util.*;

class GFG
{

// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[].
static int getSum(int BITree[], int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {

        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at
// given index in BITree. The given value 'val' is
// added to BITree[i] and all of its ancestors in
// tree.
static void updateBIT(int BITree[], int n,
                      int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent
        // in update View
        index += index & (-index);
    }
}

// Converts an array to an array with values
// from 1 to n and relative order of smaller
// and greater elements remains same.
// For example, {7, -90, 100, 1} is
// converted to {3, 1, 4, 2 }
static void convert(int arr[], int n)
{
    // Create a copy of arrp[] in temp and sort
    // the temp array in increasing order
    int []temp = new int[n];
    for (int i = 0; i < n; i++)
        temp[i] = arr[i];
    Arrays.sort(temp);

    // Traverse all array elements
    for (int i = 0; i < n; i++)
    {

        // lower_bound() Returns pointer to
        // the first element greater than
        // or equal to arr[i]
        arr[i] = lower_bound(temp, 0, n,
                             arr[i]) + 1;
    }
}

static int lower_bound(int[] a, int low,
                       int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low) / 2;
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Returns inversion count of all subarray
// of size k in arr[0..n-1]
static int getInvCount(int arr[], int k, int n)
{
    int invcount = 0; // Initialize result

    // Convert arr[] to an array with values from
    // 1 to n and relative order of smaller and
    // greater elements remains same. For example,
    // {7, -90, 100, 1} is converted to {3, 1, 4, 2 }
    convert(arr, n);

    // Create a BIT with size equal to maxElement+1
    // (Extra one is used so that elements can be
    // directly be used as index)
    int []BIT = new int[n + 1];
    for (int i = 1; i <= n; i++)
        BIT[i] = 0;

    // Get inversion count of first subarray
    for (int i = k - 1; i >= 0; i--)
    {

        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    // now calculate the inversion of
    // all other subarrays
    int ans = invcount;
    int i = 0, j = k, icnt = 0, jcnt = 0;
    while (j <= n - 1)
    {

        // calculate value of inversion count of
        // first element in previous subarray
        icnt = getSum(BIT, arr[i] - 1);
        updateBIT(BIT, n, arr[i], -1);

        // calculating inversion count of
        // last element in the current subarray
        jcnt = getSum(BIT, n) - getSum(BIT, arr[j]);
        updateBIT(BIT, n, arr[j], 1);

        // calculating inversion count
        // of current subarray
        invcount = invcount - icnt + jcnt;

        // adding current inversion to the answer
        ans = ans + invcount;
        i++; j++;
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 7, 3, 2, 4, 1 };
    int k = 3;
    int n = arr.length;
    System.out.println("Number of inversions in all " +
                       "subarrays of size " + k +
                       " are : " + getInvCount(arr, k, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count inversions in all sub arrays
# of size k using Binary Indexed Tree
from bisect import bisect_left as lower_bound

# Returns sum of arr[0..index]. This function assumes
# that the array is preprocessed and partial sums of
# array elements are stored in BITree.
def getSum(BITree, index):

    sum = 0 # Initialize result

    # Traverse ancestors of BITree[index]
    while (index > 0):

        # Add current element of BITree to sum
        sum += BITree[index]

        # Move index to parent node in getSum View
        index -= index & (-index)

    return sum

# Updates a node in Binary Index Tree (BITree) at
# given index in BITree. The given value 'val' is
# added to BITree[i] and all of its ancestors in
# tree.
def updateBIT(BITree, n, index, val):

    # Traverse all ancestors and add 'val'
    while (index <= n):
        # Add 'val' to current node of BI Tree
        BITree[index] += val

        # Update index to that of parent
        # in update View
        index += index & (-index)

# Converts an array to an array with values from 1 to n
# and relative order of smaller and greater elements
# remains same. For example,7, -90, 100, 1 is
# converted to3, 1, 4, 2
def convert(arr, n):

    # Create a copy of arrp in temp and sort
    # the temp array in increasing order
    temp = [0]*(n)
    for i in range(n):
        temp[i] = arr[i]
    temp = sorted(temp)

    # Traverse all array elements
    for i in range(n):

        # lower_bound() Returns pointer to
        # the first element greater than
        # or equal to arr[i]
        arr[i] = lower_bound(temp, arr[i]) + 1

# Returns inversion count of all subarray
# of size k in arr[0..n-1]
def getInvCount(arr, k, n):

    invcount = 0 # Initialize result

    # Convert arr to an array with values from
    # 1 to n and relative order of smaller and
    # greater elements remains same. For example,
    # 7, -90, 100, 1 is converted to3, 1, 4, 2
    convert(arr, n)

    # Create a BIT with size equal to maxElement+1
    # (Extra one is used so that elements can be
    # directly be used as index)
    BIT=[0]*(n + 1)
    for i in range(1, n + 1):
        BIT[i] = 0

    # Get inversion count of first subarray
    for i in range(k - 1, -1, -1):

        # Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1)

        # Add current element to BIT
        updateBIT(BIT, n, arr[i], 1)

    # now calculate the inversion of all other subarrays
    ans = invcount
    i = 0
    j = k
    icnt = 0
    jcnt = 0
    while (j <= n - 1):

        # calculate value of inversion count of first element
        # in previous subarray
        icnt = getSum(BIT, arr[i] - 1)
        updateBIT(BIT, n, arr[i], -1)

        # calculating inversion count of last element in the
        # current subarray
        jcnt = getSum(BIT, n) - getSum(BIT, arr[j])
        updateBIT(BIT, n, arr[j], 1)

        # calculating inversion count of current subarray
        invcount = invcount - icnt + jcnt

        # adding current inversion to the answer
        ans = ans + invcount
        i += 1
        j += 1

    return ans

# Driver code
if __name__ == '__main__':
    arr= [7, 3, 2, 4, 1]
    k = 3
    n = len(arr)
    print("Number of inversions in all subarrays of size "
            ,k," are : ",getInvCount(arr, k, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count inversions in all sub arrays
// of size k using Binary Indexed Tree
using System;

class GFG
{

// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[].
static int getSum(int []BITree, int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {

        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at
// given index in BITree. The given value 'val' is
// added to BITree[i] and all of its ancestors in
// tree.
static void updateBIT(int []BITree, int n,
                      int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent
        // in update View
        index += index & (-index);
    }
}

// Converts an array to an array with values
// from 1 to n and relative order of smaller
// and greater elements remains same.
// For example, {7, -90, 100, 1} is
// converted to {3, 1, 4, 2 }
static void convert(int []arr, int n)
{
    // Create a copy of arrp[] in temp and sort
    // the temp array in increasing order
    int []temp = new int[n];
    for (int i = 0; i < n; i++)
        temp[i] = arr[i];
    Array.Sort(temp);

    // Traverse all array elements
    for (int i = 0; i < n; i++)
    {

        // lower_bound() Returns pointer to
        // the first element greater than
        // or equal to arr[i]
        arr[i] = lower_bound(temp, 0, n,
                             arr[i]) + 1;
    }
}

static int lower_bound(int[] a, int low,
                       int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low) / 2;
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Returns inversion count of all subarray
// of size k in arr[0..n-1]
static int getInvCount(int []arr, int k, int n)
{
    int invcount = 0; // Initialize result

    // Convert arr[] to an array with values from
    // 1 to n and relative order of smaller and
    // greater elements remains same. For example,
    // {7, -90, 100, 1} is converted to {3, 1, 4, 2 }
    convert(arr, n);

    // Create a BIT with size equal to maxElement+1
    // (Extra one is used so that elements can be
    // directly be used as index)
    int []BIT = new int[n + 1];
    for (int i = 1; i <= n; i++)
        BIT[i] = 0;

    // Get inversion count of first subarray
    for (int i = k - 1; i >= 0; i--)
    {

        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    // now calculate the inversion of
    // all other subarrays
    int ans = invcount;
    int x = 0, j = k, icnt = 0, jcnt = 0;
    while (j <= n - 1)
    {

        // calculate value of inversion count of
        // first element in previous subarray
        icnt = getSum(BIT, arr[x] - 1);
        updateBIT(BIT, n, arr[x], -1);

        // calculating inversion count of
        // last element in the current subarray
        jcnt = getSum(BIT, n) - getSum(BIT, arr[j]);
        updateBIT(BIT, n, arr[j], 1);

        // calculating inversion count
        // of current subarray
        invcount = invcount - icnt + jcnt;

        // adding current inversion to the answer
        ans = ans + invcount;
        x++; j++;
    }
    return ans;
}

// Driver Code
static public void Main ()
{
    int []arr = { 7, 3, 2, 4, 1 };
    int k = 3;
    int n = arr.Length;
    Console.Write("Number of inversions in all " +
                  "subarrays of size " + k +
                  " are : " + getInvCount(arr, k, n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript program to count inversions in all sub arrays
    // of size k using Binary Indexed Tree

    // Returns sum of arr[0..index]. This function assumes
    // that the array is preprocessed and partial sums of
    // array elements are stored in BITree[].
    function getSum(BITree, index)
    {
        let sum = 0; // Initialize result

        // Traverse ancestors of BITree[index]
        while (index > 0)
        {

            // Add current element of BITree to sum
            sum += BITree[index];

            // Move index to parent node in getSum View
            index -= index & (-index);
        }
        return sum;
    }

    // Updates a node in Binary Index Tree (BITree) at
    // given index in BITree. The given value 'val' is
    // added to BITree[i] and all of its ancestors in
    // tree.
    function updateBIT(BITree, n, index, val)
    {
        // Traverse all ancestors and add 'val'
        while (index <= n)
        {
            // Add 'val' to current node of BI Tree
            BITree[index] += val;

            // Update index to that of parent
            // in update View
            index += index & (-index);
        }
    }

    // Converts an array to an array with values
    // from 1 to n and relative order of smaller
    // and greater elements remains same.
    // For example, {7, -90, 100, 1} is
    // converted to {3, 1, 4, 2 }
    function convert(arr, n)
    {
        // Create a copy of arrp[] in temp and sort
        // the temp array in increasing order
        let temp = new Array(n);
        for (let i = 0; i < n; i++)
            temp[i] = arr[i];
        temp.sort(function(a, b){return a - b});

        // Traverse all array elements
        for (let i = 0; i < n; i++)
        {

            // lower_bound() Returns pointer to
            // the first element greater than
            // or equal to arr[i]
            arr[i] = lower_bound(temp, 0, n, arr[i]) + 1;
        }
    }

    function lower_bound(a, low, high, element)
    {
        while(low < high)
        {
            let middle = low + parseInt((high - low) / 2, 10);
            if(element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Returns inversion count of all subarray
    // of size k in arr[0..n-1]
    function getInvCount(arr, k, n)
    {
        let invcount = 0; // Initialize result

        // Convert arr[] to an array with values from
        // 1 to n and relative order of smaller and
        // greater elements remains same. For example,
        // {7, -90, 100, 1} is converted to {3, 1, 4, 2 }
        convert(arr, n);

        // Create a BIT with size equal to maxElement+1
        // (Extra one is used so that elements can be
        // directly be used as index)
        let BIT = new Array(n + 1);
        for (let i = 1; i <= n; i++)
            BIT[i] = 0;

        // Get inversion count of first subarray
        for (let i = k - 1; i >= 0; i--)
        {

            // Get count of elements smaller than arr[i]
            invcount += getSum(BIT, arr[i] - 1);

            // Add current element to BIT
            updateBIT(BIT, n, arr[i], 1);
        }

        // now calculate the inversion of
        // all other subarrays
        let ans = invcount;
        let x = 0, j = k, icnt = 0, jcnt = 0;
        while (j <= n - 1)
        {

            // calculate value of inversion count of
            // first element in previous subarray
            icnt = getSum(BIT, arr[x] - 1);
            updateBIT(BIT, n, arr[x], -1);

            // calculating inversion count of
            // last element in the current subarray
            jcnt = getSum(BIT, n) - getSum(BIT, arr[j]);
            updateBIT(BIT, n, arr[j], 1);

            // calculating inversion count
            // of current subarray
            invcount = invcount - icnt + jcnt;

            // adding current inversion to the answer
            ans = ans + invcount;
            x++; j++;
        }
        return ans;
    }

    let arr = [ 7, 3, 2, 4, 1 ];
    let k = 3;
    let n = arr.length;
    document.write("Number of inversions in all " +
                  "subarrays of size " + k +
                  " are : " + getInvCount(arr, k, n));

</script>
```

**输出:**

```
Number of inversions in all subarrays of size 3 are : 6
```

**时间复杂度:-** 第一个子阵列的反转计数需要 O(k log(n))个时间，对于所有其他子阵列需要 O((n-k)log(n))。所以总的时间复杂度是:O(n log n)。
**辅助空间:-** O(n)
本文由 [**Ashish Sharma**](https://auth.geeksforgeeks.org/profile.php?user=ashish136&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。