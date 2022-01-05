# 随机二分搜索法算法

> 原文:[https://www . geesforgeks . org/随机化-二进制-搜索-算法/](https://www.geeksforgeeks.org/randomized-binary-search-algorithm/)

给我们一个由 n 个元素组成的排序数组 A[]。我们需要找到 x 在 A 中是否存在。在二分搜索法，我们总是使用中间元素，这里我们将在给定的范围内随机选择一个元素。在二分搜索法我们有

```
middle = (start + end)/2
```

在随机二分搜索法中，我们执行以下操作

```
Generate a random number t
Since range of number in which we want a random
number is [start, end]
Hence we do, t = t % (end-start+1)
Then, t = start + t;
Hence t is a random number between start and end
```

这是一个拉斯维加斯随机化算法，因为它总能找到正确的结果。

**随机化二分搜索法算法的预期时间复杂度**
对于 n 个元素，假设所需的预期时间为 T(n)，在我们选择一个随机枢轴后，数组大小减少为 k。由于所有可能枢轴的选择概率相等，因此 p = 1/n。
T(n)是选择枢轴后所有可能大小的时间之和乘以选择该枢轴的概率加上生成随机枢轴索引所需的时间。因此

```
T(n) = p*T(1) + p*T(2) + ..... + p*T(n) + 1
putting p = 1/n
T(n) = ( T(1) + T(2) + ..... + T(n) ) / n + 1
n*T(n) = T(1) + T(2) + .... + T(n) + n      .... eq(1)
Similarly for n-1
(n-1)*T(n-1) = T(1) + T(2) + ..... + T(n-1) + n-1    .... eq(2)
Subtract eq(1) - eq(2)
n*T(n) - (n-1)*T(n-1) = T(n) + 1
(n-1)*T(n) - (n-1)*T(n-1) =  1
(n-1)*T(n) = (n-1)*T(n-1) + 1
T(n) = 1/(n-1) + T(n-1)
T(n) = 1/(n-1) + 1/(n-2) + T(n-2)
T(n) = 1/(n-1) + 1/(n-2) + 1/(n-3) + T(n-3)
Similarly,
T(n) = 1 + 1/2 + 1/3 + ... + 1/(n-1)
Hence T(n) is equal to (n-1)th Harmonic number, 
n-th harmonic number is O(log n)
Hence T(n) is O(log n) 
```

**随机化二分搜索法的递归实现**

## C++

```
// C++ program to implement recursive
// randomized algorithm.
#include <iostream>
#include <ctime>
using namespace std;

// To generate random number
// between x and y ie.. [x, y]
int getRandom(int x, int y)
{
    srand(time(NULL));
    return (x + rand() % (y-x+1));
}

// A recursive randomized binary search function.
// It returns location of x in
// given array arr[l..r] is present, otherwise -1
int randomizedBinarySearch(int arr[], int l,
                            int r, int x)
{
    if (r >= l)
    {
        // Here we have defined middle as
        // random index between l and r ie.. [l, r]
        int mid = getRandom(l, r);

        // If the element is present at the
        // middle itself
        if (arr[mid] == x)
            return mid;

        // If element is smaller than mid, then
        // it can only be present in left subarray
        if (arr[mid] > x)
          return randomizedBinarySearch(arr, l,
                                    mid-1, x);

        // Else the element can only be present
        // in right subarray
        return randomizedBinarySearch(arr, mid+1,
                                         r, x);
    }

    // We reach here when element is not present
    // in array
    return -1;
}

// Driver code
int main(void)
{
    int arr[] = {2, 3, 4, 10, 40};
    int n = sizeof(arr)/ sizeof(arr[0]);
    int x = 10;
    int result = randomizedBinarySearch(arr, 0, n-1, x);
    (result == -1)? printf("Element is not present in array")
    : printf("Element is present at index %d", result);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement recursive
// randomized algorithm.
public class RandomizedBinarySearch
{

    // To generate random number
    // between x and y ie.. [x, y]
    public static int getRandom(int x, int y)
    {
        return (x + (int)(Math.random() % (y-x+1)));
    }

    // A recursive randomized binary search function.
    // It returns location of x in
    // given array arr[l..r] is present, otherwise -1
    public static int randomizedBinarySearch(int arr[],
                            int low, int high, int key)
    {
        if (high >= low)
        {
            // Here we have defined middle as
            // random index between l and r ie.. [l, r]
            int mid = getRandom(low, high);

            // If the element is present at the
            // middle itself
            if (arr[mid] == key)
                return mid;

            // If element is smaller than mid, then
            // it can only be present in left subarray
            if (arr[mid] > key)
                return randomizedBinarySearch(arr, low, mid-1, key);

            // Else the element can only be present
            // in right subarray
            return randomizedBinarySearch(arr, mid+1, high, key);
        }

        // We reach here when element is not present
        // in array
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 3, 4, 10, 40};
        int n = arr.length;
        int key = 10;
        int result = randomizedBinarySearch(arr, 0, n-1, key);
        System.out.println((result == -1)?"Element is not present in array":
                "Element is present at index " + result);
    }
}

// This code is contributed by JEREM
```

## 蟒蛇 3

```
# Python3 program to implement recursive
# randomized algorithm.
# To generate random number
# between x and y ie.. [x, y]

import random
def getRandom(x,y):
    tmp=(x + random.randint(0,100000) % (y-x+1))
    return tmp

# A recursive randomized binary search function.
# It returns location of x in
# given array arr[l..r] is present, otherwise -1

def randomizedBinarySearch(arr,l,r,x) :
    if r>=l:

        # Here we have defined middle as
        # random index between l and r ie.. [l, r]
        mid=getRandom(l,r)

        # If the element is present at the
        # middle itself
        if arr[mid] == x:
            return mid

        # If element is smaller than mid, then
        # it can only be present in left subarray
        if arr[mid]>x:
            return randomizedBinarySearch(arr, l, mid-1, x)

        # Else the element can only be present
        # in right subarray
        return randomizedBinarySearch(arr, mid+1,r, x)

    # We reach here when element is not present
    # in array
    return -1

# Driver code
if __name__=='__main__':
    arr = [2, 3, 4, 10, 40]
    n=len(arr)
    x=10
    result = randomizedBinarySearch(arr, 0, n-1, x)
    if result==-1:
        print('Element is not present in array')
    else:
        print('Element is present at index ', result)

# This code is contributes by sahilshelangia
```

## C#

```
// C# program to implement recursive
// randomized algorithm.
using System;

class RandomizedBinarySearch
{

    // To generate random number
    // between x and y ie.. [x, y]
    public static int getRandom(int x, int y)
    {
        Random r = new Random();
        return (x + (int)(r.Next() % (y - x + 1)));
    }

    // A recursive randomized binary search function.
    // It returns location of x in
    // given array arr[l..r] is present, otherwise -1
    public static int randomizedBinarySearch(int []arr,
                            int low, int high, int key)
    {
        if (high >= low)
        {
            // Here we have defined middle as
            // random index between l and r ie.. [l, r]
            int mid = getRandom(low, high);

            // If the element is present at the
            // middle itself
            if (arr[mid] == key)
                return mid;

            // If element is smaller than mid, then
            // it can only be present in left subarray
            if (arr[mid] > key)
                return randomizedBinarySearch(arr, low, mid - 1, key);

            // Else the element can only be present
            // in right subarray
            return randomizedBinarySearch(arr, mid + 1, high, key);
        }

        // We reach here when element is not present
        // in array
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 3, 4, 10, 40};
        int n = arr.Length;
        int key = 10;
        int result = randomizedBinarySearch(arr, 0, n - 1, key);
        Console.WriteLine((result == -1)?"Element is not present in array":
                "Element is present at index " + result);
    }
}

// This code is contributed by 29AjayKumar
```

**输出:**

```
Element is present at index 3
```

**随机化二分搜索法的迭代实现**

## C++

```
// C++ program to implement iterative
// randomized algorithm.
#include <iostream>
#include <ctime>
using namespace std;

// To generate random number
// between x and y ie.. [x, y]
int getRandom(int x, int y)
{
    srand(time(NULL));
    return (x + rand()%(y-x+1));
}

// A iterative randomized binary search function.
// It returns location of x in
// given array arr[l..r] if present, otherwise -1
int randomizedBinarySearch(int arr[], int l,
                               int r, int x)
{
    while (l <= r)
    {
        // Here we have defined middle as
        // random index between l and r ie.. [l, r]
        int m = getRandom(l, r);

        // Check if x is present at mid
        if (arr[m] == x)
            return m;

        // If x greater, ignore left half
        if (arr[m] < x)
            l = m + 1;

        // If x is smaller, ignore right half
        else
            r = m - 1;
    }

    // if we reach here, then element was
    // not present
    return -1;
}

// Driver code
int main(void)
{
    int arr[] = {2, 3, 4, 10, 40};
    int n = sizeof(arr)/ sizeof(arr[0]);
    int x = 10;
    int result = randomizedBinarySearch(arr, 0, n-1, x);
    (result == -1)? printf("Element is not present in array")
        : printf("Element is present at index %d", result);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement iterative
// randomized algorithm.
class GFG
{

// To generate random number
// between x and y ie.. [x, y]
static int getRandom(int x, int y)
{

    return (int) (x + Math.random() * 10 % (y - x + 1));
}

// A iterative randomized binary search function.
// It returns location of x in
// given array arr[l..r] if present, otherwise -1
static int randomizedBinarySearch(int arr[], int l,
                                    int r, int x)
{
    while (l <= r)
    {
        // Here we have defined middle as
        // random index between l and r ie.. [l, r]
        int m = getRandom(l, r);

        // Check if x is present at mid
        if (arr[m] == x)
            return m;

        // If x greater, ignore left half
        if (arr[m] < x)
            l = m + 1;

        // If x is smaller, ignore right half
        else
            r = m - 1;
    }

    // if we reach here, then element was
    // not present
    return -1;
}

// Driver code
public static void main(String []args)
{
    int arr[] = {2, 3, 4, 10, 40};
    int n = arr.length;
    int x = 10;
    int result = randomizedBinarySearch(arr, 0, n - 1, x);
    if(result == -1)
        System.out.printf("Element is not present in array");
    else
        System.out.printf("Element is present at index %d", result);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to implement iterative
# randomized algorithm.

# To generate random number
# between x and y ie.. [x, y]

from random import randint

def getRandom(x, y):
    return randint(x,y)

# A iterative randomized binary search function.
# It returns location of x in
# given array arr[l..r] if present, otherwise -1
def randomizedBinarySearch(arr, l, r, x):
    while (l <= r):
        # Here we have defined middle as
        # random index between l and r ie.. [l, r]
        m = getRandom(l, r)

        # Check if x is present at mid
        if (arr[m] == x):
            return m

        # If x greater, ignore left half
        if (arr[m] < x):
            l = m + 1

        # If x is smaller, ignore right half
        else:
            r = m - 1
    # if we reach here, then element was
    # not present
    return -1

# Driver code
arr = [2, 3, 4, 10, 40]
n = len(arr)
x = 10
result = randomizedBinarySearch(arr, 0, n-1, x)
if result == 1:
    print("Element is not present in array")
else:
    print("Element is present at index", result)

# This code is contributed by ankush_953
```

## C#

```
// C# program to implement iterative
// randomized algorithm.
using System;
using System.Collections.Generic;

class GFG
{

// To generate random number
// between x and y ie.. [x, y]
static int getRandom(int x, int y)
{

    return (int) (x + new Random(10).Next(1) * 10 % (y - x + 1));
}

// A iterative randomized binary search function.
// It returns location of x in
// given array arr[l..r] if present, otherwise -1
static int randomizedBinarySearch(int []arr, int l,
                                    int r, int x)
{
    while (l <= r)
    {
        // Here we have defined middle as
        // random index between l and r ie.. [l, r]
        int m = getRandom(l, r);

        // Check if x is present at mid
        if (arr[m] == x)
            return m;

        // If x greater, ignore left half
        if (arr[m] < x)
            l = m + 1;

        // If x is smaller, ignore right half
        else
            r = m - 1;
    }

    // if we reach here, then element was
    // not present
    return -1;
}

// Driver code
public static void Main(String []args)
{
    int []arr = {2, 3, 4, 10, 40};
    int n = arr.Length;
    int x = 10;
    int result = randomizedBinarySearch(arr, 0, n - 1, x);
    if(result == -1)
        Console.Write("Element is not present in array");
    else
        Console.Write("Element is present at index {0}", result);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement iterative
// randomized algorithm.

// To generate random number
// between x and y ie.. [x, y]
function getRandom(x,y)
{
     return Math.floor(x + Math.floor(Math.random() * 10) %
                      (y - x + 1));
}

// A iterative randomized binary search function.
// It returns location of x in
// given array arr[l..r] if present, otherwise -1
function randomizedBinarySearch(arr,l,r,x)
{
    while (l <= r)
    {

        // Here we have defined middle as
        // random index between l and r ie.. [l, r]
        let m = getRandom(l, r);

        // Check if x is present at mid
        if (arr[m] == x)
            return m;

        // If x greater, ignore left half
        if (arr[m] < x)
            l = m + 1;

        // If x is smaller, ignore right half
        else
            r = m - 1;
    }

    // If we reach here, then element was
    // not present
    return -1;
}

// Driver code
let arr = [ 2, 3, 4, 10, 40 ];
let n = arr.length;
let x = 10;
let result = randomizedBinarySearch(arr, 0, n - 1, x);

if (result == -1)
    document.write("Element is not present in array");
else
    document.write("Element is present at index ",
                   result);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Element is present at index 3
```

本文由 [**普拉蒂克·查哈尔**](https://pratik-chhajer.github.io/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。