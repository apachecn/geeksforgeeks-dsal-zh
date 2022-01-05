# 找出数组中三元组的数量，使得 a[i] > a[j] > a[k]和 i

> Original:

给定一个大小为 **N** 的数组 **arr** 。任务是计算数组中三元组的数量，使得 **a[i] > a[j] > a[k]** 和 **i < j < k**
**示例:**

> **输入:** arr[] = {10，8，3，1}
> **输出:** 4
> 三胞胎为:
> 1，3，8
> 1，3，10
> 1，8，10
> 3，8，10
> **输入:** arr[] = {88，64，45，21，54}
> **输出:** 5 【T16

**先决条件:** [计数反转](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)
**进场:**

*   找到左大数组。greater_left[i]表示大于 a[i]且位于其左侧(从 0 到 i-1)的元素数量。
*   找到较小的右数组。small _ right[I]表示小于 a[i]且在 a[I]右侧的元素数量(从 i+1 到 n-1)
*   最终答案将是每个指数的大左[i]和小右[i]的乘积之和。

**以下是上述方法的实施:**

## C++

```
// CPP program to find triplets
// a[i]>a[j]>a[k] and i<j<k
#include<bits/stdc++.h>
using namespace std;

// Updates a node in Binary Index Tree (BIT)
// at given index(i) in BIT.  The given value
// 'val' is added to BITree[i] and
// all of its ancestors in tree.
void update(int BIT[], int n, int i, int val)
{
    for (; i <= n; i += (i & -i)) {
        BIT[i] += val;
    }
}

// Returns sum of arr[0..i]. This function
// assumes that the array is preprocessed
// and partial sums of array elements are
// stored in BIT[].
int query(int BIT[], int i)
{
    int sum = 0;
    for (; i > 0; i -= (i & -i)) {
        sum += BIT[i];
    }
    return sum;
}

// Converts an array to an array with values from 1 to n
// and relative order of smaller and greater elements
// remains same.  For example, {7, -90, 100, 1} is
// converted to {3, 1, 4 ,2 }
void Convert(int arr[], int n)
{
    int temp[n];
    for (int i = 0; i < n; i++) {
        temp[i] = arr[i];
    }
    sort(temp, temp + n);

    for (int i = 0; i < n; i++) {
    arr[i] = lower_bound(temp, temp + n, arr[i]) - temp + 1;
    }
}

// Function to find triplets
int getCount(int arr[], int n)
{
    // Decomposition
    Convert(arr, n);

    int BIT[n + 1] = { 0 };
    int smaller_right[n + 1] = { 0 };
    int greater_left[n + 1] = { 0 };

    // Find all right side smaller elements
    for (int i = n - 1; i >= 0; i--) {
        smaller_right[i] = query(BIT, arr[i]-1);
        update(BIT, n, arr[i], 1);
    }

    for (int i = 0; i <= n; i++) {
        BIT[i] = 0;
    }

    // Find all left side greater elements
    for (int i = 0; i < n; i++) {
        greater_left[i] = i - query(BIT, arr[i]);
        update(BIT, n, arr[i], 1);
    }

    // Find the required answer
    int ans = 0;
    for (int i = 0; i < n; i++) {
        ans += greater_left[i] * smaller_right[i];
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 7, 3, 4, 3, 3, 1};

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getCount(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;

class GFG {

    public static int lower(int a[], int x)     //Returns leftest index of x in sorted arr else n
     {                                                  //If not present returns index of just greater element
         int n = a.length;
           int l = 0;
        int r = n - 1;
        int ans = n;
        while(l <= r)
        {
            int m = (r - l) / 2 + l;
            if(a[m] >= x)
            {
                ans = m;
                r = m - 1;
            }
            else
            {
                 l = m + 1;
            }
        }
        return ans;
    }
    // Returns sum of arr[0..i]. This function
    // assumes that the array is preprocessed
    // and partial sums of array elements are
    // stored in BIT[].
    public static int query(int BIT[], int i)
    {
        int sum = 0;
        for (; i > 0; i -= (i & -i)) {
            sum += BIT[i];
        }
        return sum;
    }
    // Converts an array to an array with values from 1 to n
    // and relative order of smaller and greater elements
    // remains same.  For example, {7, -90, 100, 1} is
    // converted to {3, 1, 4 ,2 }
    public static void Convert(int arr[], int n)
    {
        int temp[]=new int[n];
        for (int i = 0; i < n; i++) {
            temp[i] = arr[i];
        }
        Arrays.sort(temp);
        for (int i = 0; i < n; i++) {
          arr[i] = lower(temp, arr[i]) + 1;
        }
    }
    // Updates a node in Binary Index Tree (BIT)
    // at given index(i) in BIT.  The given value
    // 'val' is added to BITree[i] and
    // all of its ancestors in tree.
    public static void update(int BIT[], int n, int i, int val)
    {
        for (; i <= n; i += (i & -i)) {
            BIT[i] += val;
        }
    }
    // Function to find triplets
    public static int getCount(int arr[], int n)
    {
        // Decomposition
        Convert(arr, n);

        int BIT[] = new int[n+1];
        int smaller_right[] = new int[n+1];
        int greater_left[] = new int[n+1];
        for(int i=0;i<n+1;i++){
            BIT[i]=0;
            smaller_right[i]=0;
            greater_left[i]=0;
        }
        // Find all right side smaller elements
        for (int i = n - 1; i >= 0; i--) {
            smaller_right[i] = query(BIT, arr[i]-1);
            update(BIT, n, arr[i], 1);
        }

        for (int i = 0; i <= n; i++) {
            BIT[i] = 0;
        }

        // Find all left side greater elements
        for (int i = 0; i < n; i++) {
            greater_left[i] = i - query(BIT, arr[i]);
            update(BIT, n, arr[i], 1);
        }

        // Find the required answer
        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans += greater_left[i] * smaller_right[i];
        }

        // Return the required answer
        return ans;
    }
    public static void main (String[] args) {
        int arr[] = { 7, 3, 4, 3, 3, 1};
        int n = 6;
        System.out.println(getCount(arr, n));
    }
}
// this code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program to find triplets
# a[i]>a[j]>a[k] and i<j<k
from bisect import bisect_left as lower_bound

# Updates a node in Binary Index Tree (BIT)
# at given index(i) in BIT. The given value
# 'val' is added to BITree[i] and
# all of its ancestors in tree.
def update(BIT, n, i, val):
    while i <= n:
        BIT[i] += val

        i += (i & -i)

# Returns sum of arr[0..i]. This function
# assumes that the array is preprocessed
# and partial sums of array elements are
# stored in BIT[].
def query(BIT, i):
    summ = 0
    while i > 0:
        summ += BIT[i]

        i -= (i & -i)

    return summ

# Converts an array to an array with values
# from 1 to n and relative order of smaller
# and greater elements remains same. For example,
# {7, -90, 100, 1} is converted to {3, 1, 4 ,2 }
def convert(arr, n):
    temp = [0] * n
    for i in range(n):
        temp[i] = arr[i]

    temp.sort()

    for i in range(n):
        arr[i] = lower_bound(temp, arr[i]) + 1

# Function to find triplets
def getCount(arr, n):

    # Decomposition
    convert(arr, n)

    BIT = [0] * (n + 1)
    smaller_right = [0] * (n + 1)
    greater_left = [0] * (n + 1)

    # Find all right side smaller elements
    for i in range(n - 1, -1, -1):
        smaller_right[i] = query(BIT, arr[i] - 1)
        update(BIT, n, arr[i], 1)

    for i in range(n + 1):
        BIT[i] = 0

    # Find all left side greater elements
    for i in range(n):
        greater_left[i] = i - query(BIT, arr[i])
        update(BIT, n, arr[i], 1)

    # Find the required answer
    ans = 0
    for i in range(n):
        ans += greater_left[i] * smaller_right[i]

    # Return the required answer
    return ans

# Driver Code
if __name__ == "__main__":
    arr = [7, 3, 4, 3, 3, 1]
    n = len(arr)

    print(getCount(arr, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
  public static int lower(int[] a, int x)     //Returns leftest index of x in sorted arr else n
  {                                                  //If not present returns index of just greater element
    int n = a.Length;
    int l = 0;
    int r = n - 1;
    int ans = n;
    while(l <= r)
    {
      int m = (r - l) / 2 + l;
      if(a[m] >= x)
      {
        ans = m;
        r = m - 1;
      }
      else
      {
        l = m + 1;
      }
    }
    return ans;
  }

  // Returns sum of arr[0..i]. This function
  // assumes that the array is preprocessed
  // and partial sums of array elements are
  // stored in BIT[].
  public static int query(int[] BIT, int i)
  {
    int sum = 0;
    for (; i > 0; i -= (i & -i)) {
      sum += BIT[i];
    }
    return sum;
  }
  // Converts an array to an array with values from 1 to n
  // and relative order of smaller and greater elements
  // remains same.  For example, {7, -90, 100, 1} is
  // converted to {3, 1, 4 ,2 }
  public static void Convert(int[] arr, int n)
  {
    int[] temp =new int[n];
    for (int i = 0; i < n; i++) {
      temp[i] = arr[i];
    }
    Array.Sort(temp);
    for (int i = 0; i < n; i++) {
      arr[i] = lower(temp, arr[i]) + 1;
    }
  }
  // Updates a node in Binary Index Tree (BIT)
  // at given index(i) in BIT.  The given value
  // 'val' is added to BITree[i] and
  // all of its ancestors in tree.
  public static void update(int[] BIT, int n, int i, int val)
  {
    for (; i <= n; i += (i & -i)) {
      BIT[i] += val;
    }
  }
  // Function to find triplets
  public static int getCount(int[] arr, int n)
  {

    // Decomposition
    Convert(arr, n);

    int[] BIT = new int[n + 1];
    int[] smaller_right = new int[n + 1];
    int[] greater_left = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
    {
      BIT[i] = 0;
      smaller_right[i] = 0;
      greater_left[i] = 0;
    }

    // Find all right side smaller elements
    for (int i = n - 1; i >= 0; i--)
    {
      smaller_right[i] = query(BIT, arr[i]-1);
      update(BIT, n, arr[i], 1);
    }

    for (int i = 0; i <= n; i++)
    {
      BIT[i] = 0;
    }

    // Find all left side greater elements
    for (int i = 0; i < n; i++)
    {
      greater_left[i] = i - query(BIT, arr[i]);
      update(BIT, n, arr[i], 1);
    }

    // Find the required answer
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
      ans += greater_left[i] * smaller_right[i];
    }

    // Return the required answer
    return ans;
  }

  // Driver code
  public static void Main ()
  {
    int[] arr = { 7, 3, 4, 3, 3, 1};
    int n = 6;
    Console.WriteLine(getCount(arr, n));

  }
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// JavaScript program to find triplets
// a[i]>a[j]>a[k] and i<j<k

// Updates a node in Binary Index Tree (BIT)
// at given index(i) in BIT. The given value
// 'val' is added to BITree[i] and
// all of its ancestors in tree.
function update(BIT, n, i, val) {
    for (; i <= n; i += (i & -i)) {
        BIT[i] += val;
    }
}

// Returns sum of arr[0..i]. This function
// assumes that the array is preprocessed
// and partial sums of array elements are
// stored in BIT[].
function query(BIT, i) {
    let sum = 0;
    for (; i > 0; i -= (i & -i)) {
        sum += BIT[i];
    }
    return sum;
}

//Returns leftest index of x in sorted arr else n
//If not present returns index of just greater element

function lower(a, x) {
    let n = a.length;
    let l = 0;
    let r = n - 1;
    let ans = n;
    while (l <= r) {
        let m = Math.floor((r - l) / 2) + l;
        if (a[m] >= x) {
            ans = m;
            r = m - 1;
        }
        else {
            l = m + 1;
        }
    }
    return ans;
}

// Converts an array to an array with values from 1 to n
// and relative order of smaller and greater elements
// remains same. For example, {7, -90, 100, 1} is
// converted to {3, 1, 4 ,2 }
function Convert(arr, n) {
    let temp = new Array(n);
    for (let i = 0; i < n; i++) {
        temp[i] = arr[i];
    }
    temp.sort((a, b) => a - b);

    for (let i = 0; i < n; i++) {
        arr[i] = lower(temp, arr[i]) + 1;
    }
}

// Function to find triplets
function getCount(arr, n) {
    // Decomposition
    Convert(arr, n);

    let BIT = new Array(n + 1).fill(0);
    let smaller_right = new Array(n + 1).fill(0);
    let greater_left = new Array(n + 1).fill(0);

    // Find all right side smaller elements
    for (let i = n - 1; i >= 0; i--) {
        smaller_right[i] = query(BIT, arr[i] - 1);
        update(BIT, n, arr[i], 1);
    }

    for (let i = 0; i <= n; i++) {
        BIT[i] = 0;
    }

    // Find all left side greater elements
    for (let i = 0; i < n; i++) {
        greater_left[i] = i - query(BIT, arr[i]);
        update(BIT, n, arr[i], 1);
    }

    // Find the required answer
    let ans = 0;
    for (let i = 0; i < n; i++) {
        ans += greater_left[i] * smaller_right[i];
    }

    // Return the required answer
    return ans;
}

// Driver code

let arr = [7, 3, 4, 3, 3, 1];

let n = arr.length;

document.write(getCount(arr, n) + "<br>");

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
8
```