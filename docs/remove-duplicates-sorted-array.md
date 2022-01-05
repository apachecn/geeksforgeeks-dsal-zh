# 从排序的数组中删除重复项

> 原文:[https://www . geesforgeks . org/remove-duplicates-sorted-array/](https://www.geeksforgeeks.org/remove-duplicates-sorted-array/)

给定一个排序的数组，任务是从数组中移除重复的元素。
示例:

```
Input  : arr[] = {2, 2, 2, 2, 2}
Output : arr[] = {2}
         new size = 1

Input  : arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5}
Output : arr[] = {1, 2, 3, 4, 5}
         new size = 5
```

**方法 1:** (使用额外空间)

1.  创建一个辅助数组 temp[]来存储唯一元素。
2.  遍历输入数组，并将 arr[]的唯一元素逐个复制到 temp[]。还要记录独特元素的数量。让这个计数为 **j** 。
3.  将 **j** 元素从 temp[]复制到 arr[]并返回 j

## C++

```
// Simple C++ program to remove duplicates
#include<iostream>
using namespace std;

// Function to remove duplicate elements
// This function returns new size of modified
// array.
int removeDuplicates(int arr[], int n)
{
    // Return, if array is empty
    // or contains a single element
    if (n==0 || n==1)
        return n;

    int temp[n];

    // Start traversing elements
    int j = 0;
    for (int i=0; i<n-1; i++)

        // If current element is not equal
        // to next element then store that
        // current element
        if (arr[i] != arr[i+1])
            temp[j++] = arr[i];

    // Store the last element as whether
    // it is unique or repeated, it hasn't
    // stored previously
    temp[j++] = arr[n-1];

    // Modify original array
    for (int i=0; i<j; i++)
        arr[i] = temp[i];

    return j;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    // removeDuplicates() returns new size of
    // array.
    n = removeDuplicates(arr, n);

    // Print updated array
    for (int i=0; i<n; i++)
       cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// simple java program to remove
// duplicates

class Main
{
    // Function to remove duplicate elements
    // This function returns new size of modified
    // array.
    static int removeDuplicates(int arr[], int n)
    {
        // Return, if array is empty
        // or contains a single element
        if (n==0 || n==1)
            return n;

        int[] temp = new int[n];

        // Start traversing elements
        int j = 0;
        for (int i=0; i<n-1; i++)
            // If current element is not equal
            // to next element then store that
            // current element
            if (arr[i] != arr[i+1])
                temp[j++] = arr[i];

        // Store the last element as whether
        // it is unique or repeated, it hasn't
        // stored previously
        temp[j++] = arr[n-1];  

        // Modify original array
        for (int i=0; i<j; i++)
            arr[i] = temp[i];

        return j;
    }

    public static void main (String[] args)
    {
        int arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5};
        int n = arr.length;

        n = removeDuplicates(arr, n);

        // Print updated array
        for (int i=0; i<n; i++)
           System.out.print(arr[i]+" ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to
# remove duplicates
# Function to remove
# duplicate elements

# This function returns
# new size of modified
# array.
def removeDuplicates(arr, n):

    # Return, if array is
    # empty or contains
    # a single element
    if n == 0 or n == 1:
        return n

    temp = list(range(n))

    # Start traversing elements
    j = 0;
    for i in range(0, n-1):

        # If current element is
        # not equal to next
        # element then store that
        # current element
        if arr[i] != arr[i+1]:
            temp[j] = arr[i]
            j += 1

    # Store the last element
    # as whether it is unique
    # or repeated, it hasn't
    # stored previously
    temp[j] = arr[n-1]
    j += 1

    # Modify original array
    for i in range(0, j):
        arr[i] = temp[i]

    return j

# Driver code
arr = [1, 2, 2, 3, 4, 4, 4, 5, 5]
n = len(arr)

# removeDuplicates() returns
# new size of array.
n = removeDuplicates(arr, n)

# Print updated array
for i in range(n):
    print ("%d"%(arr[i]), end = " ")
```

## C#

```
// Simple C# program to remove
// duplicates
using System;

class GFG {

    // Function to remove duplicate
    // elements This function returns
    // new size of modified array.
    static int removeDuplicates(int []arr, int n)
    {

        // Return, if array is empty
        // or contains a single element
        if (n == 0 || n == 1)
            return n;

        int []temp = new int[n];

        // Start traversing elements
        int j = 0;

        for (int i = 0; i < n - 1; i++)

            // If current element is not equal
            // to next element then store that
            // current element
            if (arr[i] != arr[i+1])
                temp[j++] = arr[i];

        // Store the last element as
        // whether it is unique or
        // repeated, it hasn't
        // stored previously
        temp[j++] = arr[n-1];

        // Modify original array
        for (int i = 0; i < j; i++)
            arr[i] = temp[i];

        return j;
    }

    public static void Main ()
    {
        int []arr = {1, 2, 2, 3, 4, 4, 4, 5, 5};
        int n = arr.Length;

        n = removeDuplicates(arr, n);

        // Print updated array
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// Simple JavaScript program to remove
// duplicates

// Function to remove duplicate elements
// This function returns new size of modified
// array.
function removeDuplicates(arr, n)
{
    // Return, if array is empty
    // or contains a single element
    if (n==0 || n==1)
        return n;

    var temp = new Array(n);

    // Start traversing elements
    var j = 0;
    for (var i=0; i<n-1; i++)

        // If current element is not equal
        // to next element then store that
        // current element
        if (arr[i] != arr[i+1])
            temp[j++] = arr[i];

    // Store the last element as whether
    // it is unique or repeated, it hasn't
    // stored previously
    temp[j++] = arr[n-1];

    // Modify original array
    for (var i=0; i<j; i++)
        arr[i] = temp[i];

    return j;
}

var arr = [1, 2, 2, 3, 4, 4, 4, 5, 5];
    var n = arr.length;

    // removeDuplicates() returns new size of
    // array.
    n = removeDuplicates(arr, n);

    // Print updated array
    for (var i=0; i<n; i++)
       document.write( arr[i]+" ");

// This code is contributed by SoumikMondal

</script>
```

**输出:**

```
1 2 3 4 5
```

时间复杂度:O(n)
辅助空间:O(n)
**方法 2:** (恒定额外空间)
只需为同一数组维护一个单独的索引，就像方法 1 中为不同数组维护的索引一样。

## C++

```
// C++ program to remove duplicates in-place
#include<iostream>
using namespace std;

// Function to remove duplicate elements
// This function returns new size of modified
// array.
int removeDuplicates(int arr[], int n)
{
    if (n==0 || n==1)
        return n;

    // To store index of next unique element
    int j = 0;

    // Doing same as done in Method 1
    // Just maintaining another updated index i.e. j
    for (int i=0; i < n-1; i++)
        if (arr[i] != arr[i+1])
            arr[j++] = arr[i];

    arr[j++] = arr[n-1];

    return j;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    // removeDuplicates() returns new size of
    // array.
    n = removeDuplicates(arr, n);

    // Print updated array
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// simple java program to remove
// duplicates

class Main
{
    // Function to remove duplicate elements
    // This function returns new size of modified
    // array.
    static int removeDuplicates(int arr[], int n)
    {
        if (n == 0 || n == 1)
            return n;

        // To store index of next unique element
        int j = 0;

        // Doing same as done in Method 1
        // Just maintaining another updated index i.e. j
        for (int i = 0; i < n-1; i++)
            if (arr[i] != arr[i+1])
                arr[j++] = arr[i];

        arr[j++] = arr[n-1];

        return j;
    }

    public static void main (String[] args)
    {
        int arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5};
        int n = arr.length;

        n = removeDuplicates(arr, n);

        // Print updated array
        for (int i=0; i<n; i++)
           System.out.print(arr[i]+" ");
    }
}

/* This code is contributed by Harsh Agarwal */
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-2">蟒 3</gfg-tab>T3

```
 # Python3 program to remove
# duplicate elements

# This function returns new 
# size of modified array
def removeDuplicates(arr, n):
    if n == 0 or n == 1:
        return n

    # To store index of next
    # unique element
    j = 0

    # Doing same as done
    # in Method 1 Just
    # maintaining another 
    # updated index i.e. j
    for i in range(0, n-1):
        if arr[i] != arr[i+1]:
            arr[j] = arr[i]
            j += 1

    arr[j] = arr[n-1]
    j += 1
    return j

# Driver code
arr = [1, 2, 2, 3, 4, 4, 4, 5, 5]
n = len(arr)

# removeDuplicates() returns
# new size of array.
n = removeDuplicates(arr, n)

# Print updated array
for i in range(0, n):
    print (" %d "%(arr[i]), end = " ") 
```

T4

## C#

```
// simple C# program to remove
// duplicates
using System;

class GfG {

    // Function to remove duplicate
    // elements This function returns
    // new size of modified array.
    static int removeDuplicates(int []arr, int n)
    {

        if (n == 0 || n == 1)
            return n;

        // To store index of next
        // unique element
        int j = 0;

        // Doing same as done in Method 1
        // Just maintaining another updated
        // index i.e. j
        for (int i = 0; i < n - 1; i++)
            if (arr[i] != arr[i + 1])
                arr[j++] = arr[i];

        arr[j++] = arr[n - 1];

        return j;
    }

    public static void Main ()
    {
        int []arr = {1, 2, 2, 3, 4, 4,
                                 4, 5, 5};
        int n = arr.Length;

        n = removeDuplicates(arr, n);

        // Print updated array
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by parashar.
```

## java 描述语言

```
<script>
// simple javascript program to remove
// duplicates

    // Function to remove duplicate elements
    // This function returns new size of modified
    // array.
    function removeDuplicates(arr , n) {
        if (n == 0 || n == 1)
            return n;

        // To store index of next unique element
        var j = 0;

        // Doing same as done in Method 1
        // Just maintaining another updated index i.e. j
        for (i = 0; i < n - 1; i++)
            if (arr[i] != arr[i + 1])
                arr[j++] = arr[i];

        arr[j++] = arr[n - 1];

        return j;
    }

        var arr = [ 1, 2, 2, 3, 4, 4, 4, 5, 5 ];
        var n = arr.length;

        n = removeDuplicates(arr, n);

        // Print updated array
        for (i = 0; i < n; i++)
            document.write(arr[i] + " ");

// This code is contributed by umadevi9616
</script>
```

输出:

```
1 2 3 4 5
```

时间复杂度:O(n)
辅助空间:O(1)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。