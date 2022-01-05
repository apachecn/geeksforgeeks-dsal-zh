# 找到给定行在二维数组中的位置

> 原文:[https://www . geeksforgeeks . org/find-给定行在二维数组中的位置/](https://www.geeksforgeeks.org/find-the-position-of-the-given-row-in-a-2-d-array/)

给定一个大小为 **m * n** 的矩阵 **mat[][]** ，按行排序，以及一个数组 **row[]** ，任务是检查矩阵中是否有任何行等于给定的数组 **row[]** 。
**举例:**

> **输入:** mat[][] = {
> {1，1，2，3，1}，
> {2，1，3，3，2}，
> {2，4，5，8，3}，
> {4，5，5，8，3}，
> {8，7，10，13，6}}
> row[] = {4，5，5，8，3}
> **输出:** 4
> 4
> **输入:** mat[][] = {
> {0，0，1，0}，
> {10，9，22，23}，
> {40，40，40，40}，
> {43，44，55，68}，
> {81，73，100，132}，
> {100，75，125，133 } }

**朴素方法:**类似于一维数组上的线性搜索，对矩阵执行线性搜索，并将矩阵的每一行与给定的数组进行比较。如果某行与数组匹配，则打印其行号，否则打印-1。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int m = 6, n = 4;

// Function to find a row in the
// given matrix using linear search
int linearCheck(int ar[][n], int arr[])
{
    for (int i = 0; i < m; i++) {

        // Assume that the current row matched
        // with the given array
        bool matched = true;

        for (int j = 0; j < n; j++) {

            // If any element of the current row doesn't
            // match with the corresponding element
            // of the given array
            if (ar[i][j] != arr[j]) {

                // Set matched to false and break;
                matched = false;
                break;
            }
        }

        // If matched then return the row number
        if (matched)
            return i + 1;
    }

    // No row matched with the given array
    return -1;
}

// Driver code
int main()
{
    int mat[m][n] = { { 0, 0, 1, 0 },
                      { 10, 9, 22, 23 },
                      { 40, 40, 40, 40 },
                      { 43, 44, 55, 68 },
                      { 81, 73, 100, 132 },
                      { 100, 75, 125, 133 } };
    int row[n] = { 10, 9, 22, 23 };

    cout << linearCheck(mat, row);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int m = 6, n = 4;

// Function to find a row in the
// given matrix using linear search
static int linearCheck(int ar[][], int arr[])
{
    for (int i = 0; i < m; i++)
    {

        // Assume that the current row matched
        // with the given array
        boolean matched = true;

        for (int j = 0; j < n; j++)
        {

            // If any element of the current row doesn't
            // match with the corresponding element
            // of the given array
            if (ar[i][j] != arr[j])
            {

                // Set matched to false and break;
                matched = false;
                break;
            }
        }

        // If matched then return the row number
        if (matched)
            return i + 1;
    }

    // No row matched with the given array
    return -1;
}

// Driver code
public static void main (String[] args)
{
    int mat[][] = { { 0, 0, 1, 0 },
                { 10, 9, 22, 23 },
                { 40, 40, 40, 40 },
                { 43, 44, 55, 68 },
                { 81, 73, 100, 132 },
                { 100, 75, 125, 133 } };
    int row[] = { 10, 9, 22, 23 };

    System.out.println (linearCheck(mat, row));
}
}

// This code is contributed BY @Tushil..
```

## 蟒蛇 3

```
# Python implementation of the approach

m, n = 6, 4;

# Function to find a row in the
# given matrix using linear search
def linearCheck(ar, arr):
    for i in range(m):

        # Assume that the current row matched
        # with the given array
        matched = True;

        for j in range(n):

            # If any element of the current row doesn't
            # match with the corresponding element
            # of the given array
            if (ar[i][j] != arr[j]):

                # Set matched to false and break;
                matched = False;
                break;
        # If matched then return the row number
        if (matched):
            return i + 1;
    # No row matched with the given array
    return -1;

# Driver code
if __name__ == "__main__" :

    mat = [
        [ 0, 0, 1, 0 ],
        [ 10, 9, 22, 23 ],
        [ 40, 40, 40, 40 ],
        [ 43, 44, 55, 68 ],
        [ 81, 73, 100, 132 ],
        [ 100, 75, 125, 133 ]
        ];

    row = [ 10, 9, 22, 23 ];

    print(linearCheck(mat, row));

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int m = 6;
static int n = 4;

// Function to find a row in the
// given matrix using linear search
static int linearCheck(int [,]ar, int []arr)
{
    for (int i = 0; i < m; i++)
    {

        // Assume that the current row matched
        // with the given array
        bool matched = true;

        for (int j = 0; j < n; j++)
        {

            // If any element of the current row doesn't
            // match with the corresponding element
            // of the given array
            if (ar[i,j] != arr[j])
            {

                // Set matched to false and break;
                matched = false;
                break;
            }
        }

        // If matched then return the row number
        if (matched)
            return i + 1;
    }

    // No row matched with the given array
    return -1;
}

// Driver code
static public void Main ()
{
    int [,]mat = { { 0, 0, 1, 0 },
                { 10, 9, 22, 23 },
                { 40, 40, 40, 40 },
                { 43, 44, 55, 68 },
                { 81, 73, 100, 132 },
                { 100, 75, 125, 133 } };
    int []row = { 10, 9, 22, 23 };

Console.Write(linearCheck(mat, row));
}
}

// This code is contributed BY ajit..
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let m = 6, n = 4;

    // Function to find a row in the
    // given matrix using linear search
    function linearCheck(ar, arr)
    {
        for (let i = 0; i < m; i++)
        {

            // Assume that the current row matched
            // with the given array
            let matched = true;

            for (let j = 0; j < n; j++)
            {

                // If any element of the current row doesn't
                // match with the corresponding element
                // of the given array
                if (ar[i][j] != arr[j])
                {

                    // Set matched to false and break;
                    matched = false;
                    break;
                }
            }

            // If matched then return the row number
            if (matched)
                return i + 1;
        }

        // No row matched with the given array
        return -1;
    }

    let mat = [ [ 0, 0, 1, 0 ],
                [ 10, 9, 22, 23 ],
                [ 40, 40, 40, 40 ],
                [ 43, 44, 55, 68 ],
                [ 81, 73, 100, 132 ],
                [ 100, 75, 125, 133 ] ];
    let row = [ 10, 9, 22, 23 ];

    document.write(linearCheck(mat, row));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(m * n)
**高效方法:**由于矩阵是按行排序的，所以我们可以像在一维数组中一样使用二分搜索法。有必要以逐行方式对数组进行排序。下面是使用二分搜索法在矩阵中查找一行的步骤，

1.  将 arr[]与中间一行进行比较。
2.  如果 arr[]与中间行完全匹配，我们返回中间索引。
3.  否则如果 arr[]大于中间行(至少存在一个 j，0<=j
4.  否则(arr[]较小)，我们检查上半部分。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int m = 6, n = 4;

// Function that compares both the arrays
// and returns -1, 0 and 1 accordingly
int compareRow(int a1[], int a2[])
{
    for (int i = 0; i < n; i++) {

        // Return 1 if mid row is less than arr[]
        if (a1[i] < a2[i])
            return 1;

        // Return 1 if mid row is greater than arr[]
        else if (a1[i] > a2[i])
            return -1;
    }

    // Both the arrays are equal
    return 0;
}

// Function to find a row in the
// given matrix using binary search
int binaryCheck(int ar[][n], int arr[])
{
    int l = 0, r = m - 1;
    while (l <= r) {
        int mid = (l + r) / 2;
        int temp = compareRow(ar[mid], arr);

        // If current row is equal to the given
        // array then return the row number
        if (temp == 0)
            return mid + 1;

        // If arr[] is greater, ignore left half
        else if (temp == 1)
            l = mid + 1;

        // If arr[] is smaller, ignore right half
        else
            r = mid - 1;
    }

    // No valid row found
    return -1;
}

// Driver code
int main()
{
    int mat[m][n] = { { 0, 0, 1, 0 },
                      { 10, 9, 22, 23 },
                      { 40, 40, 40, 40 },
                      { 43, 44, 55, 68 },
                      { 81, 73, 100, 132 },
                      { 100, 75, 125, 133 } };
    int row[n] = { 10, 9, 22, 23 };

    cout << binaryCheck(mat, row);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int m = 6, n = 4;

// Function that compares both the arrays
// and returns -1, 0 and 1 accordingly
static int compareRow(int a1[], int a2[])
{
    for (int i = 0; i < n; i++)
    {

        // Return 1 if mid row is less than arr[]
        if (a1[i] < a2[i])
            return 1;

        // Return 1 if mid row is greater than arr[]
        else if (a1[i] > a2[i])
            return -1;
    }

    // Both the arrays are equal
    return 0;
}

// Function to find a row in the
// given matrix using binary search
static int binaryCheck(int ar[][], int arr[])
{
    int l = 0, r = m - 1;
    while (l <= r)
    {
        int mid = (l + r) / 2;
        int temp = compareRow(ar[mid], arr);

        // If current row is equal to the given
        // array then return the row number
        if (temp == 0)
            return mid + 1;

        // If arr[] is greater, ignore left half
        else if (temp == 1)
            l = mid + 1;

        // If arr[] is smaller, ignore right half
        else
            r = mid - 1;
    }

    // No valid row found
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = { { 0, 0, 1, 0 },
                    { 10, 9, 22, 23 },
                    { 40, 40, 40, 40 },
                    { 43, 44, 55, 68 },
                    { 81, 73, 100, 132 },
                    { 100, 75, 125, 133 } };
    int row[] = { 10, 9, 22, 23 };

    System.out.println(binaryCheck(mat, row));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

m = 6;
n = 4;

# Function that compares both the arrays
# and returns -1, 0 and 1 accordingly
def compareRow(a1, a2) :

    for i in range(n) :

        # Return 1 if mid row is less than arr[]
        if (a1[i] < a2[i]) :
            return 1;

        # Return 1 if mid row is greater than arr[]
        elif (a1[i] > a2[i]) :
            return -1;

    # Both the arrays are equal
    return 0;

# Function to find a row in the
# given matrix using binary search
def binaryCheck(ar, arr) :

    l = 0; r = m - 1;

    while (l <= r) :

        mid = (l + r) // 2;
        temp = compareRow(ar[mid], arr);

        # If current row is equal to the given
        # array then return the row number
        if (temp == 0) :
            return mid + 1;

        # If arr[] is greater, ignore left half
        elif (temp == 1) :
            l = mid + 1;

        # If arr[] is smaller, ignore right half
        else :
            r = mid - 1;

    # No valid row found
    return -1;

# Driver code
if __name__ == "__main__" :

    mat = [
        [ 0, 0, 1, 0 ],
        [ 10, 9, 22, 23 ],
        [ 40, 40, 40, 40 ],
        [ 43, 44, 55, 68 ],
        [ 81, 73, 100, 132 ],
        [ 100, 75, 125, 133 ]
        ];

    row = [ 10, 9, 22, 23 ];

    print(binaryCheck(mat, row));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int m = 6, n = 4;

// Function that compares both the arrays
// and returns -1, 0 and 1 accordingly
static int compareRow(int []a1, int []a2)
{
    for (int i = 0; i < n; i++)
    {

        // Return 1 if mid row is less than arr[]
        if (a1[i] < a2[i])
            return 1;

        // Return 1 if mid row is greater than arr[]
        else if (a1[i] > a2[i])
            return -1;
    }

    // Both the arrays are equal
    return 0;
}

// Function to find a row in the
// given matrix using binary search
static int binaryCheck(int [,]ar, int []arr)
{
    int l = 0, r = m - 1;
    while (l <= r)
    {
        int mid = (l + r) / 2;
        int temp = compareRow(GetRow(ar, mid), arr);

        // If current row is equal to the given
        // array then return the row number
        if (temp == 0)
            return mid + 1;

        // If arr[] is greater, ignore left half
        else if (temp == 1)
            l = mid + 1;

        // If arr[] is smaller, ignore right half
        else
            r = mid - 1;
    }

    // No valid row found
    return -1;
}

public static int[] GetRow(int[,] matrix, int row)
{
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for (var i = 0; i < rowLength; i++)
    rowVector[i] = matrix[row, i];

    return rowVector;
}

// Driver code
public static void Main(String[] args)
{
    int [,]mat = {{ 0, 0, 1, 0 },
                  { 10, 9, 22, 23 },
                  { 40, 40, 40, 40 },
                  { 43, 44, 55, 68 },
                  { 81, 73, 100, 132 },
                  { 100, 75, 125, 133 }};
    int []row = { 10, 9, 22, 23 };

    Console.WriteLine(binaryCheck(mat, row));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var m = 6, n = 4;

// Function that compares both the arrays
// and returns -1, 0 and 1 accordingly
function compareRow(a1, a2)
{
    for (var i = 0; i < n; i++) {

        // Return 1 if mid row is less than arr[]
        if (a1[i] < a2[i])
            return 1;

        // Return 1 if mid row is greater than arr[]
        else if (a1[i] > a2[i])
            return -1;
    }

    // Both the arrays are equal
    return 0;
}

// Function to find a row in the
// given matrix using binary search
function binaryCheck(ar, arr)
{
    var l = 0, r = m - 1;
    while (l <= r) {
        var mid = parseInt((l + r) / 2);
        var temp = compareRow(ar[mid], arr);

        // If current row is equal to the given
        // array then return the row number
        if (temp == 0)
            return mid + 1;

        // If arr[] is greater, ignore left half
        else if (temp == 1)
            l = mid + 1;

        // If arr[] is smaller, ignore right half
        else
            r = mid - 1;
    }

    // No valid row found
    return -1;
}

// Driver code
var mat = [ [ 0, 0, 1, 0 ],
                  [ 10, 9, 22, 23 ],
                  [ 40, 40, 40, 40 ],
                  [ 43, 44, 55, 68 ],
                  [ 81, 73, 100, 132 ],
                  [ 100, 75, 125, 133 ] ];
var row = [10, 9, 22, 23];
document.write( binaryCheck(mat, row));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n * log(m))