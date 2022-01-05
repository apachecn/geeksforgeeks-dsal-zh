# 二分搜索法的变种

> 原文:[https://www.geeksforgeeks.org/variants-of-binary-search/](https://www.geeksforgeeks.org/variants-of-binary-search/)

[二分搜索法](https://www.geeksforgeeks.org/binary-search/)很容易吧？当排序后的值列表中出现元素重复时，二分搜索法就会变得复杂。并不总是我们使用二分搜索法搜索的“包含或不包含”，而是有如下 5 种变体:
1)包含(真或假)
2)关键字首次出现的索引
3)关键字最后出现的索引
4)最小元素大于关键字的索引
5)最大元素小于关键字的索引

这些搜索中的每一个，虽然基本逻辑保持不变，但在实现上有微小的变化，有竞争力的程序员应该意识到这一点。您可能已经看到了其他方法，例如用于查找第一个和最后一个出现的[这个](https://www.geeksforgeeks.org/find-first-and-last-positions-of-an-element-in-a-sorted-array/)，在这里您可以比较相邻的元素，也可以检查是否到达了第一个/最后一个元素。

从复杂性的角度来看，它可能看起来像一个 O(log n)算法，但当比较本身很昂贵时，它就不起作用了。一个证明这一点的问题就链接在这个帖子的最后，随意尝试一下。
变量 1:包含键(真或假)

```
Input : 2 3 3 5 5 5 6 6
Function : Contains(4)
Returns : False

Function : Contains(5)
Returns : True
```

**变量 2:** 键的第一次出现(数组的索引)。这类似于

## C++

```
std::lower_bound(...)
```

```
Input : 2 3 3 5 5 5 6 6
Function : first(3)
Returns : 1

Function : first(5)
Returns : 3

Function : first(4)
Returns : -1
```

**变量 3:** 键的最后一次出现(数组的索引)

```
Input : 2 3 3 5 5 5 6 6
Function : last(3)
Returns : 2

Function : last(5)
Returns : 5

Function : last(4)
Returns : -1
```

**变量 4:** 大于键的最小整数的索引(第一次出现)。这类似于

## C++

```
std::upper_bound(...)
```

```
Input : 2 3 3 5 5 5 6 6
Function : leastGreater(2)
Returns : 1

Function : leastGreater(5)
Returns : 6
```

**变量 5:** 小于键的最大整数的索引(最后出现)

```
Input : 2 3 3 5 5 5 6 6
Function : greatestLesser(2)
Returns : -1

Function : greatestLesser(5)
Returns : 2
```

正如您将在下面看到的，如果您观察到实现之间的明显差异，您将看到相同的逻辑被用来寻找二分搜索法的不同变体。

## C++

```
// C++ program to variants of Binary Search
#include <bits/stdc++.h>

using namespace std;

int n = 8; // array size
int a[] = { 2, 3, 3, 5, 5, 5, 6, 6 }; // Sorted array

/* Find if key is in array
 * Returns: True if key belongs to array,
 *          False if key doesn't belong to array */
bool contains(int low, int high, int key)
{
    bool ans = false;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        int midVal = a[mid];

        if (midVal < key) {

            // if mid is less than key, all elements
            // in range [low, mid] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key) {

            // if mid is greater than key, all elements
            // in range [mid + 1, high] are also greater
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key) {

            // comparison added just for the sake
            // of clarity if mid is equal to key, we
            // have found that key exists in array
            ans = true;
            break;
        }
    }

    return ans;
}

/* Find first occurrence index of key in array
 * Returns: an index in range [0, n-1] if key belongs
 *          to array, -1 if key doesn't belong to array
 */
int first(int low, int high, int key)
{
    int ans = -1;

    while (low <= high) {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key) {

            // if mid is less than key, all elements
            // in range [low, mid] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key) {

            // if mid is greater than key, all elements
            // in range [mid + 1, high] are also greater
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key) {

            // if mid is equal to key, we note down
            //  the last found index then we search
            // for more in left side of mid
            // so we now search in [low, mid - 1]
            ans = mid;
            high = mid - 1;
        }
    }

    return ans;
}

/* Find last occurrence index of key in array
 * Returns: an index in range [0, n-1] if key
             belongs to array,
 *          -1 if key doesn't belong to array
 */
int last(int low, int high, int key)
{
    int ans = -1;

    while (low <= high) {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key) {

            // if mid is less than key, then all elements
            // in range [low, mid - 1] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key) {

            // if mid is greater than key, then all
            // elements in range [mid + 1, high] are
            // also greater so we now search in
            // [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key) {

            // if mid is equal to key, we note down
            // the last found index then we search
            // for more in right side of mid
            // so we now search in [mid + 1, high]
            ans = mid;
            low = mid + 1;
        }
    }

    return ans;
}

/* Find index of first occurrence of least element
   greater than key in array
 * Returns: an index in range [0, n-1] if key is not
             the greatest element in array,
 *          -1 if key is the greatest element in array */
int leastgreater(int low, int high, int key)
{
    int ans = -1;

    while (low <= high) {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key) {

            // if mid is less than key, all elements
            // in range [low, mid - 1] are <= key
            // then we search in right side of mid
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key) {

            // if mid is greater than key, all elements
            // in range [mid + 1, high] are >= key
            // we note down the last found index, then
            // we search in left side of mid
            // so we now search in [low, mid - 1]
            ans = mid;
            high = mid - 1;
        }
        else if (midVal == key) {

            // if mid is equal to key, all elements in
            // range [low, mid] are <= key
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
    }

    return ans;
}

/* Find index of last occurrence of greatest element
   less than key in array
 * Returns: an index in range [0, n-1] if key is not
             the least element in array,
 *          -1 if key is the least element in array */
int greatestlesser(int low, int high, int key)
{
    int ans = -1;

    while (low <= high) {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key) {

            // if mid is less than key, all elements
            // in range [low, mid - 1] are < key
            // we note down the last found index, then
            // we search in right side of mid
            // so we now search in [mid + 1, high]
            ans = mid;
            low = mid + 1;
        }
        else if (midVal > key) {

            // if mid is greater than key, all elements
            // in range [mid + 1, high] are > key
            // then we search in left side of mid
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key) {

            // if mid is equal to key, all elements
            // in range [mid + 1, high] are >= key
            // then we search in left side of mid
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
    }

    return ans;
}

int main()
{
    printf("Contains\n");
    for (int i = 0; i < 10; i++)
        printf("%d %d\n", i, contains(0, n - 1, i));

    printf("First occurrence of key\n");
    for (int i = 0; i < 10; i++)
        printf("%d %d\n", i, first(0, n - 1, i));

    printf("Last occurrence of key\n");
    for (int i = 0; i < 10; i++)
        printf("%d %d\n", i, last(0, n - 1, i));

    printf("Least integer greater than key\n");
    for (int i = 0; i < 10; i++)
        printf("%d %d\n", i, leastgreater(0, n - 1, i));

    printf("Greatest integer lesser than key\n");
    for (int i = 0; i < 10; i++)
        printf("%d %d\n", i, greatestlesser(0, n - 1, i));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to variants of Binary Search
import java.util.*;

class GFG{

// Array size   
static int n = 8;

// Sorted array
static int a[] = { 2, 3, 3, 5, 5, 5, 6, 6 };

/* Find if key is in array
 * Returns: True if key belongs to array,
 * False if key doesn't belong to array */
static int contains(int low, int high, int key)
{
    int ans = 0;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are also greater
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // Comparison added just for the sake
            // of clarity if mid is equal to key, we
            // have found that key exists in array
            ans = 1;
            break;
        }
    }
    return ans;
}

/* Find first occurrence index of key in array
 * Returns: an index in range [0, n-1] if key belongs
 *          to array, -1 if key doesn't belong to array
 */
static int first(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are also greater
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, we note down
            //  the last found index then we search
            // for more in left side of mid
            // so we now search in [low, mid - 1]
            ans = mid;
            high = mid - 1;
        }
    }
    return ans;
}

/* Find last occurrence index of key in array
 * Returns: an index in range [0, n-1] if key
            belongs to array, -1 if key doesn't
            belong to array
 */
static int last(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, then all elements
            // in range [low, mid - 1] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, then all
            // elements in range [mid + 1, high] are
            // also greater so we now search in
            // [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, we note down
            // the last found index then we search
            // for more in right side of mid
            // so we now search in [mid + 1, high]
            ans = mid;
            low = mid + 1;
        }
    }
    return ans;
}

/* Find index of first occurrence of least element
   greater than key in array
 * Returns: an index in range [0, n-1] if key is not
            the greatest element in array, -1 if key
 *          is the greatest element in array */
static int leastgreater(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid - 1] are <= key
            // then we search in right side of mid
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are >= key
            // we note down the last found index, then
            // we search in left side of mid
            // so we now search in [low, mid - 1]
            ans = mid;
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, all elements in
            // range [low, mid] are <= key
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
    }
    return ans;
}

/* Find index of last occurrence of greatest element
   less than key in array
 * Returns: an index in range [0, n-1] if key is not
            the least element in array, -1 if
 *          key is the least element in array */
static int greatestlesser(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid - 1] are < key
            // we note down the last found index, then
            // we search in right side of mid
            // so we now search in [mid + 1, high]
            ans = mid;
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are > key
            // then we search in left side of mid
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, all elements
            // in range [mid + 1, high] are >= key
            // then we search in left side of mid
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
    }

    return ans;
} 

// Driver Code
public static void main(String[] args)
{
    System.out.println("Contains");
    for(int i = 0; i < 10; i++)
        System.out.println(i + " " + contains(0, n - 1, i));

    System.out.println("First occurrence of key");
    for(int i = 0; i < 10; i++)
        System.out.println(i + " " + first(0, n - 1, i));

    System.out.println("Last occurrence of key");
    for(int i = 0; i < 10; i++)
        System.out.println(i + " " + last(0, n - 1, i));

    System.out.println("Least integer greater than key");
    for(int i = 0; i < 10; i++)
        System.out.println(i + " " +
                           leastgreater(0, n - 1, i));

    System.out.println("Greatest integer lesser than key");
    for(int i = 0; i < 10; i++)
        System.out.println(i + " " +
                           greatestlesser(0, n - 1, i));
}
}

// This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to variants of Binary Search
using System;

class GFG{

// Array size   
static int n = 8;

// Sorted array
static int[] a = { 2, 3, 3, 5, 5, 5, 6, 6 };

/* Find if key is in array
 * Returns: True if key belongs to array,
 * False if key doesn't belong to array */
static int contains(int low, int high, int key)
{
    int ans = 0;
    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are also greater
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // Comparison added just for the sake
            // of clarity if mid is equal to key, we
            // have found that key exists in array
            ans = 1;
            break;
        }
    }
    return ans;
}

/* Find first occurrence index of key in array
 * Returns: an index in range [0, n-1] if key belongs
 *          to array, -1 if key doesn't belong to array
 */
static int first(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are also greater
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, we note down
            //  the last found index then we search
            // for more in left side of mid
            // so we now search in [low, mid - 1]
            ans = mid;
            high = mid - 1;
        }
    }
    return ans;
}

/* Find last occurrence index of key in array
 * Returns: an index in range [0, n-1] if key
             belongs to array, -1 if key doesn't
             belong to array
 */
static int last(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, then all elements
            // in range [low, mid - 1] are also less
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, then all
            // elements in range [mid + 1, high] are
            // also greater so we now search in
            // [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, we note down
            // the last found index then we search
            // for more in right side of mid
            // so we now search in [mid + 1, high]
            ans = mid;
            low = mid + 1;
        }
    }
    return ans;
}

/* Find index of first occurrence of least element
   greater than key in array
 * Returns: an index in range [0, n-1] if key is not
             the greatest element in array,
 *          -1 if key is the greatest element in array */
static int leastgreater(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid - 1] are <= key
            // then we search in right side of mid
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are >= key
            // we note down the last found index, then
            // we search in left side of mid
            // so we now search in [low, mid - 1]
            ans = mid;
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, all elements in
            // range [low, mid] are <= key
            // so we now search in [mid + 1, high]
            low = mid + 1;
        }
    }
    return ans;
}

/* Find index of last occurrence of greatest element
   less than key in array
 * Returns: an index in range [0, n-1] if key is not
             the least element in array,
 *          -1 if key is the least element in array */
static int greatestlesser(int low, int high, int key)
{
    int ans = -1;

    while (low <= high)
    {
        int mid = low + (high - low + 1) / 2;
        int midVal = a[mid];

        if (midVal < key)
        {

            // If mid is less than key, all elements
            // in range [low, mid - 1] are < key
            // we note down the last found index, then
            // we search in right side of mid
            // so we now search in [mid + 1, high]
            ans = mid;
            low = mid + 1;
        }
        else if (midVal > key)
        {

            // If mid is greater than key, all elements
            // in range [mid + 1, high] are > key
            // then we search in left side of mid
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
        else if (midVal == key)
        {

            // If mid is equal to key, all elements
            // in range [mid + 1, high] are >= key
            // then we search in left side of mid
            // so we now search in [low, mid - 1]
            high = mid - 1;
        }
    }

    return ans;
}

// Driver Code
static void Main()
{
    Console.WriteLine("Contains");
    for(int i = 0; i < 10; i++)
        Console.WriteLine(i + " " + contains(0, n - 1, i));

    Console.WriteLine("First occurrence of key");
    for(int i = 0; i < 10; i++)
        Console.WriteLine(i + " " + first(0, n - 1, i));

    Console.WriteLine("Last occurrence of key");
    for(int i = 0; i < 10; i++)
        Console.WriteLine(i + " " + last(0, n - 1, i));

    Console.WriteLine("Least integer greater than key");
    for(int i = 0; i < 10; i++)
        Console.WriteLine(i + " " +
                          leastgreater(0, n - 1, i));

    Console.WriteLine("Greatest integer lesser than key");
    for(int i = 0; i < 10; i++)
        Console.WriteLine(i + " " +
                          greatestlesser(0, n - 1, i));
}
}

// This code is contributed by divyesh072019
```

**Output:** 

```
Contains
0 0
1 0
2 1
3 1
4 0
5 1
6 1
7 0
8 0
9 0
First occurrence of key
0 -1
1 -1
2 0
3 1
4 -1
5 3
6 6
7 -1
8 -1
9 -1
Last occurrence of key
0 -1
1 -1
2 0
3 2
4 -1
5 5
6 7
7 -1
8 -1
9 -1
Least integer greater than key
0 0
1 0
2 1
3 3
4 3
5 6
6 -1
7 -1
8 -1
9 -1
Greatest integer lesser than key
0 -1
1 -1
2 -1
3 0
4 2
5 2
6 5
7 7
8 7
9 7
```

下面是我在帖子开头提到的问题:[Codechef](https://www.codechef.com/problems/KCOMPRES)中的 KCOMPRES 问题。请尝试一下，并随时在这里发布您的疑问。
T3】更多二分搜索法练习题 T5】