# 在螺旋排序矩阵中搜索元素

> 原文:[https://www . geesforgeks . org/search-element-in-a-spiral-sorted-matrix/](https://www.geeksforgeeks.org/search-element-in-a-spirally-sorted-matrix/)

给定一个带有 **N × N** 元素和一个整数 **X** 的螺旋排序矩阵，任务是找到这个给定整数在矩阵中的位置(如果存在的话)，否则打印 **-1** 。**注意**所有矩阵元素都是不同的。

**示例:**

> **输入:** arr[] = {
> {1，2，3，4}，
> {12，13，14，5}，
> {11，16，15，6}，
> {10，9，8，7}}，X = 9
> **输出:** 3 1
> 9 出现在第 3 行和第 1 列(基于 0 的索引)
> 因此，输出为(3，1)。
> 
> **输入:** arr[] = {
> {1，2，3}，
> {8，9，4}，
> {7，6，5}}，X = 9
> **输出:** 1 1

一个**简单的解决方案**是搜索数组中的所有元素。这种方法最糟糕的时间复杂度是 **O(n <sup>2</sup> )** 。

一个**更好的解决方案**就是用二分搜索法。我们分两个阶段应用二分搜索法。
但在跳到这个问题之前，让我们先定义一下戒指在这里的含义。环被定义为阵列中所有单元的集合，使得它们与所有四个边的最小距离相等。
首先，我们尝试确定数字‘X’将属于哪个环。我们将利用二分搜索法来做到这一点。为此，观察矩阵的对角线元素。对角矩阵的第一个上限(N/2)保证按递增顺序排序。因此，每个天花板(N/2)对角线元素可以代表一个环。通过在第一个对角线元素上应用二进制，我们确定了数字“X”在 O(log(n))时间内所属的环。
之后，我们在环的元素上应用一个二分搜索法。在此之前，我们确定环的一边，数字“X”将属于。然后，我们相应地应用二分搜索法。
所以，总时间复杂度变成 **O(log(n))** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <iostream>
#define n 4
using namespace std;

// Function to return the ring, the number x
// belongs to.
int findRing(int arr[][n], int x)
{
    // Returns -1 if number x is smaller than
    // least element of arr
    if (arr[0][0] > x)
        return -1;

    // l and r represent the diagonal
    // elements to search in
    int l = 0, r = (n + 1) / 2 - 1;

    // Returns -1 if number x is greater
    // than the largest element of arr
    if (n % 2 == 1 && arr[r][r] < x)
        return -1;
    if (n % 2 == 0 && arr[r + 1][r] < x)
        return -1;

    while (l < r) {
        int mid = (l + r) / 2;
        if (arr[mid][mid] <= x)
            if (mid == (n + 1) / 2 - 1
                || arr[mid + 1][mid + 1] > x)
                return mid;
            else
                l = mid + 1;
        else
            r = mid - 1;
    }

    return r;
}

// Function to perform binary search
// on an array sorted in increasing order
// l and r represent the left and right
// index of the row to be searched
int binarySearchRowInc(int arr[][n], int row,
                    int l, int r, int x)
{
    while (l <= r) {
        int mid = (l + r) / 2;

        if (arr[row][mid] == x)
            return mid;

        if (arr[row][mid] < x)
            l = mid + 1;
        else
            r = mid - 1;
    }

    return -1;
}

// Function to perform binary search on
// a particular column of the 2D array
// t and b represent top and
// bottom rows
int binarySearchColumnInc(int arr[][n], int col,
                        int t, int b, int x)
{
    while (t <= b) {

        int mid = (t + b) / 2;

        if (arr[mid][col] == x)
            return mid;

        if (arr[mid][col] < x)
            t = mid + 1;
        else
            b = mid - 1;
    }

    return -1;
}

// Function to perform binary search on
// an array sorted in decreasing order
int binarySearchRowDec(int arr[][n], int row,
                    int l, int r, int x)
{
    while (l <= r) {

        int mid = (l + r) / 2;

        if (arr[row][mid] == x)
            return mid;

        if (arr[row][mid] < x)
            r = mid - 1;
        else
            l = mid + 1;
    }

    return -1;
}

// Function to perform binary search on a
// particular column of the 2D array
int binarySearchColumnDec(int arr[][n], int col,
                        int t, int b, int x)
{
    while (t <= b) {
        int mid = (t + b) / 2;

        if (arr[mid][col] == x)
            return mid;

        if (arr[mid][col] < x)
            b = mid - 1;
        else
            t = mid + 1;
    }

    return -1;
}

// Function to find the position of the number x
void spiralBinary(int arr[][n], int x)
{

    // Finding the ring
    int f1 = findRing(arr, x);

    // To store row and column
    int r, c;

    if (f1 == -1) {
        cout << "-1";
        return;
    }

    // Edge case if n is odd
    if (n % 2 == 1 && f1 == (n + 1) / 2 - 1) {
        cout << f1 << " " << f1 << endl;
        return;
    }

    // Check which of the 4 sides, the number x
    // lies in
    if (x < arr[f1][n - f1 - 1]) {
        c = binarySearchRowInc(arr, f1, f1,
                            n - f1 - 2, x);
        r = f1;
    }
    else if (x < arr[n - f1 - 1][n - f1 - 1]) {
        c = n - f1 - 1;

        r = binarySearchColumnInc(arr, n - f1 - 1, f1,
                                n - f1 - 2, x);
    }
    else if (x < arr[n - f1 - 1][f1]) {

        c = binarySearchRowDec(arr, n - f1 - 1, f1 + 1,
                            n - f1 - 1, x);
        r = n - f1 - 1;
    }
    else {

        r = binarySearchColumnDec(arr, f1, f1 + 1,
                                n - f1 - 1, x);
        c = f1;
    }

    // Printing the position
    if (c == -1 || r == -1)
        cout << "-1";
    else
        cout << r << " " << c;

    return;
}

// Driver code
int main()
{
    int arr[][n] = { { 1, 2, 3, 4 },
                    { 12, 13, 14, 5 },
                    { 11, 16, 15, 6 },
                    { 10, 9, 8, 7 } };

    spiralBinary(arr, 7);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

final static int n =4;

// Function to return the ring,
// the number x belongs to.
static int findRing(int arr[][], int x)
{
    // Returns -1 if number x is 
    // smaller than least element of arr
    if (arr[0][0] > x)
        return -1;

    // l and r represent the diagonal
    // elements to search in
    int l = 0, r = (n + 1) / 2 - 1;

    // Returns -1 if number x is greater
    // than the largest element of arr
    if (n % 2 == 1 && arr[r][r] < x)
        return -1;
    if (n % 2 == 0 && arr[r + 1][r] < x)
        return -1;

    while (l < r)
    {
        int mid = (l + r) / 2;
        if (arr[mid][mid] <= x)
            if (mid == (n + 1) / 2 - 1
                || arr[mid + 1][mid + 1] > x)
                return mid;
            else
                l = mid + 1;
        else
            r = mid - 1;
    }
    return r;
}

// Function to perform binary search
// on an array sorted in increasing order
// l and r represent the left and right
// index of the row to be searched
static int binarySearchRowInc(int arr[][], int row,
                    int l, int r, int x)
{
    while (l <= r)
    {
        int mid = (l + r) / 2;

        if (arr[row][mid] == x)
            return mid;

        if (arr[row][mid] < x)
            l = mid + 1;
        else
            r = mid - 1;
    }
    return -1;
}

// Function to perform binary search on
// a particular column of the 2D array
// t and b represent top and
// bottom rows
static int binarySearchColumnInc(int arr[][], int col,
                        int t, int b, int x)
{
    while (t <= b)
    {
        int mid = (t + b) / 2;

        if (arr[mid][col] == x)
            return mid;

        if (arr[mid][col] < x)
            t = mid + 1;
        else
            b = mid - 1;
    }
    return -1;
}

// Function to perform binary search on
// an array sorted in decreasing order
static int binarySearchRowDec(int arr[][], int row,
                    int l, int r, int x)
{
    while (l <= r) {

        int mid = (l + r) / 2;

        if (arr[row][mid] == x)
            return mid;

        if (arr[row][mid] < x)
            r = mid - 1;
        else
            l = mid + 1;
    }
    return -1;
}

// Function to perform binary search on a
// particular column of the 2D array
static int binarySearchColumnDec(int arr[][], int col,
                        int t, int b, int x)
{
    while (t <= b)
    {
        int mid = (t + b) / 2;

        if (arr[mid][col] == x)
            return mid;

        if (arr[mid][col] < x)
            b = mid - 1;
        else
            t = mid + 1;
    }
    return -1;
}

// Function to find the position of the number x
static void spiralBinary(int arr[][], int x)
{

    // Finding the ring
    int f1 = findRing(arr, x);

    // To store row and column
    int r, c;

    if (f1 == -1)
    {
            System.out.print("-1");
        return;
    }

    // Edge case if n is odd
    if (n % 2 == 1 && f1 == (n + 1) / 2 - 1)
    {
            System.out.println(f1+" "+f1);
        return;
    }

    // Check which of the 4 sides, the number x
    // lies in
    if (x < arr[f1][n - f1 - 1])
    {
        c = binarySearchRowInc(arr, f1, f1,
                            n - f1 - 2, x);
        r = f1;
    }
    else if (x < arr[n - f1 - 1][n - f1 - 1])
    {
        c = n - f1 - 1;

        r = binarySearchColumnInc(arr, n - f1 - 1, f1,
                                n - f1 - 2, x);
    }
    else if (x < arr[n - f1 - 1][f1])
    {
        c = binarySearchRowDec(arr, n - f1 - 1, f1 + 1,
                            n - f1 - 1, x);
        r = n - f1 - 1;
    }
    else
    {
        r = binarySearchColumnDec(arr, f1, f1 + 1,
                                n - f1 - 1, x);
        c = f1;
    }

    // Printing the position
    if (c == -1 || r == -1)
        System.out.print("-1");
    else
            System.out.print(r+" "+c);

    return;
}

// Driver code
public static void main(String[] args)
{
        int arr[][] = { { 1, 2, 3, 4 },
                    { 12, 13, 14, 5 },
                    { 11, 16, 15, 6 },
                    { 10, 9, 8, 7 } };

    spiralBinary(arr, 7);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the ring,
# the number x belongs to.
def findRing(arr, x):

    # Returns -1 if number x is smaller
    # than least element of arr
    if arr[0][0] > x:
        return -1

    # l and r represent the diagonal
    # elements to search in
    l, r = 0, (n + 1) // 2 - 1

    # Returns -1 if number x is greater
    # than the largest element of arr
    if n % 2 == 1 and arr[r][r] < x:
        return -1
    if n % 2 == 0 and arr[r + 1][r] < x:
        return -1

    while l < r:
        mid = (l + r) // 2
        if arr[mid][mid] <= x:

            if (mid == (n + 1) // 2 - 1 or
                arr[mid + 1][mid + 1] > x):
                return mid
            else:
                l = mid + 1

        else:
            r = mid - 1

    return r

# Function to perform binary search
# on an array sorted in increasing order
# l and r represent the left and right
# index of the row to be searched
def binarySearchRowInc(arr, row, l, r, x):

    while l <= r:
        mid = (l + r) // 2

        if arr[row][mid] == x:
            return mid
        elif arr[row][mid] < x:
            l = mid + 1
        else:
            r = mid - 1

    return -1

# Function to perform binary search on
# a particular column of the 2D array
# t and b represent top and
# bottom rows
def binarySearchColumnInc(arr, col, t, b, x):

    while t <= b:

        mid = (t + b) // 2

        if arr[mid][col] == x:
            return mid
        elif arr[mid][col] < x:
            t = mid + 1
        else:
            b = mid - 1

    return -1

# Function to perform binary search on
# an array sorted in decreasing order
def binarySearchRowDec(arr, row, l, r, x):

    while l <= r:

        mid = (l + r) // 2

        if arr[row][mid] == x:
            return mid
        elif arr[row][mid] < x:
            r = mid - 1
        else:
            l = mid + 1

    return -1

# Function to perform binary search on a
# particular column of the 2D array
def binarySearchColumnDec(arr, col, t, b, x):

    while t <= b:
        mid = (t + b) // 2

        if arr[mid][col] == x:
            return mid
        elif arr[mid][col] < x:
            b = mid - 1
        else:
            t = mid + 1

    return -1

# Function to find the position of the number x
def spiralBinary(arr, x):

    # Finding the ring
    f1 = findRing(arr, x)

    # To store row and column
    r, c = None, None

    if f1 == -1:
        print("-1")
        return

    # Edge case if n is odd
    if n % 2 == 1 and f1 == (n + 1) // 2 - 1:
        print(f1, f1)
        return

    # Check which of the 4 sides,
    # the number x lies in
    if x < arr[f1][n - f1 - 1]:
        c = binarySearchRowInc(arr, f1, f1,
                            n - f1 - 2, x)
        r = f1

    elif x < arr[n - f1 - 1][n - f1 - 1]:
        c = n - f1 - 1

        r = binarySearchColumnInc(arr, n - f1 - 1, f1,
                                n - f1 - 2, x)

    elif x < arr[n - f1 - 1][f1]:

        c = binarySearchRowDec(arr, n - f1 - 1, f1 + 1,
                            n - f1 - 1, x)
        r = n - f1 - 1

    else:

        r = binarySearchColumnDec(arr, f1, f1 + 1,
                                n - f1 - 1, x)
        c = f1

    # Printing the position
    if c == -1 or r == -1:
        print("-1")
    else:
        print("{0} {1}".format(r, c))

# Driver code
if __name__ == "__main__":

    n = 4
    arr = [[1, 2, 3, 4],
        [12, 13, 14, 5],
        [11, 16, 15, 6],
        [10, 9, 8, 7]]

    spiralBinary(arr, 7)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{

 static int n =4;

// Function to return the ring,
// the number x belongs to.
static int findRing(int [,]arr, int x)
{
    // Returns -1 if number x is
    // smaller than least element of arr
    if (arr[0,0] > x)
        return -1;

    // l and r represent the diagonal
    // elements to search in
    int l = 0, r = (n + 1) / 2 - 1;

    // Returns -1 if number x is greater
    // than the largest element of arr
    if (n % 2 == 1 && arr[r,r] < x)
        return -1;
    if (n % 2 == 0 && arr[r + 1,r] < x)
        return -1;

    while (l < r)
    {
        int mid = (l + r) / 2;
        if (arr[mid,mid] <= x)
            if (mid == (n + 1) / 2 - 1
                || arr[mid + 1,mid + 1] > x)
                return mid;
            else
                l = mid + 1;
        else
            r = mid - 1;
    }
    return r;
}

// Function to perform binary search
// on an array sorted in increasing order
// l and r represent the left and right
// index of the row to be searched
static int binarySearchRowInc(int [,]arr, int row,
                    int l, int r, int x)
{
    while (l <= r)
    {
        int mid = (l + r) / 2;

        if (arr[row,mid] == x)
            return mid;

        if (arr[row,mid] < x)
            l = mid + 1;
        else
            r = mid - 1;
    }
    return -1;
}

// Function to perform binary search on
// a particular column of the 2D array
// t and b represent top and
// bottom rows
static int binarySearchColumnInc(int [,]arr, int col,
                        int t, int b, int x)
{
    while (t <= b)
    {
        int mid = (t + b) / 2;

        if (arr[mid,col] == x)
            return mid;

        if (arr[mid,col] < x)
            t = mid + 1;
        else
            b = mid - 1;
    }
    return -1;
}

// Function to perform binary search on
// an array sorted in decreasing order
static int binarySearchRowDec(int [,]arr, int row,
                    int l, int r, int x)
{
    while (l <= r) {

        int mid = (l + r) / 2;

        if (arr[row,mid] == x)
            return mid;

        if (arr[row,mid] < x)
            r = mid - 1;
        else
            l = mid + 1;
    }
    return -1;
}

// Function to perform binary search on a
// particular column of the 2D array
static int binarySearchColumnDec(int [,]arr, int col,
                        int t, int b, int x)
{
    while (t <= b)
    {
        int mid = (t + b) / 2;

        if (arr[mid,col] == x)
            return mid;

        if (arr[mid,col] < x)
            b = mid - 1;
        else
            t = mid + 1;
    }
    return -1;
}

// Function to find the position of the number x
static void spiralBinary(int [,]arr, int x)
{

    // Finding the ring
    int f1 = findRing(arr, x);

    // To store row and column
    int r, c;

    if (f1 == -1)
    {
            Console.Write("-1");
        return;
    }

    // Edge case if n is odd
    if (n % 2 == 1 && f1 == (n + 1) / 2 - 1)
    {
            Console.WriteLine(f1+" "+f1);
        return;
    }

    // Check which of the 4 sides, the number x
    // lies in
    if (x < arr[f1,n - f1 - 1])
    {
        c = binarySearchRowInc(arr, f1, f1,
                            n - f1 - 2, x);
        r = f1;
    }
    else if (x < arr[n - f1 - 1,n - f1 - 1])
    {
        c = n - f1 - 1;

        r = binarySearchColumnInc(arr, n - f1 - 1, f1,
                                n - f1 - 2, x);
    }
    else if (x < arr[n - f1 - 1,f1])
    {
        c = binarySearchRowDec(arr, n - f1 - 1, f1 + 1,
                            n - f1 - 1, x);
        r = n - f1 - 1;
    }
    else
    {
        r = binarySearchColumnDec(arr, f1, f1 + 1,
                                n - f1 - 1, x);
        c = f1;
    }

    // Printing the position
    if (c == -1 || r == -1)
        Console.Write("-1");
    else
            Console.Write(r+" "+c);

    return;
}

// Driver code
public static void Main(String []args)
{
        int [,]arr = { { 1, 2, 3, 4 },
                    { 12, 13, 14, 5 },
                    { 11, 16, 15, 6 },
                    { 10, 9, 8, 7 } };

    spiralBinary(arr, 7);
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$n = 4;

// Function to return the ring, the number x
// belongs to.
function findRing($arr, $x)
{
    global $n;

    // Returns -1 if number x is smaller than
    // least element of arr
    if ($arr[0][0] > $x)
        return -1;

    // l and r represent the diagonal
    // elements to search in
    $l = 0;
    $r = (int)(($n + 1) / 2 - 1);

    // Returns -1 if number x is greater
    // than the largest element of arr
    if ($n % 2 == 1 && $arr[$r][$r] < $x)
        return -1;
    if ($n % 2 == 0 && $arr[$r + 1][$r] < $x)
        return -1;

    while ($l < $r)
    {
        $mid = (int)(($l + $r) / 2);
        if ($arr[$mid][$mid] <= $x)
            if ($mid == (int)(($n + 1) / 2 - 1) ||
                $arr[$mid + 1][$mid + 1] > $x)
                return $mid;
            else
                $l = $mid + 1;
        else
            $r = $mid - 1;
    }

    return $r;
}

// Function to perform binary search
// on an array sorted in increasing order
// l and r represent the left and right
// index of the row to be searched
function binarySearchRowInc($arr, $row,
                            $l, $r, $x)
{
    while ($l <= $r)
    {
        $mid = (int)(($l + $r) / 2);

        if ($arr[$row][$mid] == $x)
            return $mid;

        if ($arr[$row][$mid] < $x)
            $l = $mid + 1;
        else
            $r = $mid - 1;
    }

    return -1;
}

// Function to perform binary search on
// a particular column of the 2D array
// t and b represent top and
// bottom rows
function binarySearchColumnInc($arr, $col,
                               $t, $b, $x)
{
    while ($t <= $b)
    {
        $mid = (int)(($t + b) / 2);

        if ($arr[$mid][$col] == $x)
            return $mid;

        if ($arr[$mid][$col] < $x)
            $t = $mid + 1;
        else
            $b = $mid - 1;
    }

    return -1;
}

// Function to perform binary search on
// an array sorted in decreasing order
function binarySearchRowDec($arr, $row, $l, $r, $x)
{
    while ($l <= $r)
    {

        $mid = (int)(($l + $r) / 2);

        if ($arr[$row][$mid] == $x)
            return $mid;

        if ($arr[$row][$mid] < $x)
            $r = $mid - 1;
        else
            $l = $mid + 1;
    }

    return -1;
}

// Function to perform binary search on a
// particular column of the 2D array
function binarySearchColumnDec($arr, $col,
                               $t, $b, $x)
{
    while ($t <= $b)
    {
        $mid = (int)(($t + $b) / 2);

        if ($arr[$mid][$col] == $x)
            return $mid;

        if ($arr[$mid][$col] < $x)
            $b = $mid - 1;
        else
            $t = $mid + 1;
    }

    return -1;
}

// Function to find the position of the number x
function spiralBinary($arr, $x)
{
    global $n;

    // Finding the ring
    $f1 = findRing($arr, $x);

    // To store row and column
    $r = -1;
    $c = -1;

    if ($f1 == -1)
    {
        echo "-1";
        return;
    }

    // Edge case if n is odd
    if ($n % 2 == 1 &&
        $f1 == (int)(($n + 1) / 2 - 1))
    {
        echo $f1 . " " . $f1 . "\n";
        return;
    }

    // Check which of the 4 sides, the number x
    // lies in
    if ($x < $arr[$f1][$n - $f1 - 1])
    {
        $c = binarySearchRowInc($arr, $f1, $f1,
                                   $n - $f1 - 2, $x);
        $r = $f1;
    }
    else if ($x < $arr[$n - $f1 - 1][$n - $f1 - 1])
    {
        $c = $n - $f1 - 1;

        $r = binarySearchColumnInc($arr, $n - $f1 - 1,
                                    $f1, $n - $f1 - 2, $x);
    }
    else if ($x < $arr[$n - $f1 - 1][$f1])
    {

        $c = binarySearchRowDec($arr, $n - $f1 - 1,
                                $f1 + 1, $n - $f1 - 1, $x);
        $r = $n - $f1 - 1;
    }
    else
    {
        $r = binarySearchColumnDec($arr, $f1, $f1 + 1,
                                   $n - $f1 - 1, $x);
        $c = $f1;
    }

    // Printing the position
    if ($c == -1 || $r == -1)
        echo "-1";
    else
        echo $r . " " . $c;

    return;
}

// Driver code
$arr = array(array( 1, 2, 3, 4 ),
             array( 12, 13, 14, 5 ),
             array( 11, 16, 15, 6 ),
             array( 10, 9, 8, 7 ));

spiralBinary($arr, 7);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
var n = 4;

// Function to return the ring, the number x
// belongs to.
function findRing(arr, x)
{
    // Returns -1 if number x is smaller than
    // least element of arr
    if (arr[0][0] > x)
        return -1;

    // l and r represent the diagonal
    // elements to search in
    var l = 0, r = parseInt((n + 1) / 2) - 1;

    // Returns -1 if number x is greater
    // than the largest element of arr
    if (n % 2 == 1 && arr[r][r] < x)
        return -1;
    if (n % 2 == 0 && arr[r + 1][r] < x)
        return -1;

    while (l < r) {
        var mid = parseInt((l + r) / 2);
        if (arr[mid][mid] <= x)
            if (mid == (n + 1) / 2 - 1
                || arr[mid + 1][mid + 1] > x)
                return mid;
            else
                l = mid + 1;
        else
            r = mid - 1;
    }

    return r;
}

// Function to perform binary search
// on an array sorted in increasing order
// l and r represent the left and right
// index of the row to be searched
function binarySearchRowInc(arr, row, l, r, x)
{
    while (l <= r) {
        var mid = parseInt((l + r) / 2);

        if (arr[row][mid] == x)
            return mid;

        if (arr[row][mid] < x)
            l = mid + 1;
        else
            r = mid - 1;
    }

    return -1;
}

// Function to perform binary search on
// a particular column of the 2D array
// t and b represent top and
// bottom rows
function binarySearchColumnInc(arr, col, t, b, x)
{
    while (t <= b) {

        var mid = parseInt((t + b) / 2);

        if (arr[mid][col] == x)
            return mid;

        if (arr[mid][col] < x)
            t = mid + 1;
        else
            b = mid - 1;
    }

    return -1;
}

// Function to perform binary search on
// an array sorted in decreasing order
function binarySearchRowDec(arr, row, l, r, x)
{
    while (l <= r) {

        var mid = parseInt((l + r) / 2);

        if (arr[row][mid] == x)
            return mid;

        if (arr[row][mid] < x)
            r = mid - 1;
        else
            l = mid + 1;
    }

    return -1;
}

// Function to perform binary search on a
// particular column of the 2D array
function binarySearchColumnDec(arr, col, t, b, x)
{
    while (t <= b) {
        var mid = parseInt((t + b) / 2);

        if (arr[mid][col] == x)
            return mid;

        if (arr[mid][col] < x)
            b = mid - 1;
        else
            t = mid + 1;
    }

    return -1;
}

// Function to find the position of the number x
function spiralBinary(arr, x)
{

    // Finding the ring
    var f1 = findRing(arr, x);

    // To store row and column
    var r, c;

    if (f1 == -1) {
        document.write( "-1");
        return;
    }

    // Edge case if n is odd
    if (n % 2 == 1 && f1 == (n + 1) / 2 - 1) {
        document.write( f1 + " " + f1 + "<br>");
        return;
    }

    // Check which of the 4 sides, the number x
    // lies in
    if (x < arr[f1][n - f1 - 1]) {
        c = binarySearchRowInc(arr, f1, f1,
                            n - f1 - 2, x);
        r = f1;
    }
    else if (x < arr[n - f1 - 1][n - f1 - 1]) {
        c = n - f1 - 1;

        r = binarySearchColumnInc(arr, n - f1 - 1, f1,
                                n - f1 - 2, x);
    }
    else if (x < arr[n - f1 - 1][f1]) {

        c = binarySearchRowDec(arr, n - f1 - 1, f1 + 1,
                            n - f1 - 1, x);
        r = n - f1 - 1;
    }
    else {

        r = binarySearchColumnDec(arr, f1, f1 + 1,
                                n - f1 - 1, x);
        c = f1;
    }

    // Printing the position
    if (c == -1 || r == -1)
        document.write( "-1");
    else
        document.write( r + " " + c);

    return;
}

// Driver code
var arr = [ [ 1, 2, 3, 4 ],
                [ 12, 13, 14, 5 ],
                [ 11, 16, 15, 6 ],
                [ 10, 9, 8, 7 ] ];
spiralBinary(arr, 7);

</script>
```

**Output:** 

```
3 3
```

**时间复杂度:**O(logN)
T3】辅助空间: O(logN)