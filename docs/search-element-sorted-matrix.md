# 在排序矩阵中搜索元素

> 原文:[https://www.geeksforgeeks.org/search-element-sorted-matrix/](https://www.geeksforgeeks.org/search-element-sorted-matrix/)

给定一个排序的矩阵 mat[n][m]和一个元素“x”。找到 x 在矩阵中的位置(如果存在),否则打印-1。矩阵的排序方式是，一行中的所有元素按递增顺序排序，对于行“I”，其中 1 <= i <= n-1，行“I”的第一个元素大于或等于行“i-1”的最后一个元素。该方法应该具有 0(对数 n +对数 m)的时间复杂度。

**示例:**

```
Input : mat[][] = { {1, 5, 9},
                    {14, 20, 21},
                    {30, 34, 43} }
        x = 14
Output : Found at (1, 0)

Input : mat[][] = { {1, 5, 9, 11},
                    {14, 20, 21, 26},
                    {30, 34, 43, 50} }
        x = 42
Output : -1
```

请注意，这个问题不同于[按行搜索和按列搜索排序矩阵](https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/)。这里，矩阵被更严格地排序，因为一行的第一个元素大于前一行的最后一个元素。

一个**简单的解决方法**就是把 x 和矩阵的每个元素一一比较。如果匹配，则返回位置。如果我们到达终点，返回-1。这个解决方案的时间复杂度是 O(n×m)。

一个有效的解决方案是将一个给定的 2D 数组类型转换成一个 1D 数组，然后在类型转换后的数组上应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。

**另一种不需要类型转换的有效方法**解释如下。

```
1) Perform binary search on the middle column 
   till only two elements are left or till the
   middle element of some row in the search is
   the required element 'x'. This search is done
   to skip the rows that are not required
2) The two left elements must be adjacent. Consider
   the rows of two elements and do following
   a) check whether the element 'x' equals to the 
      middle element of any one of the 2 rows
   b) otherwise according to the value of the 
      element 'x' check whether it is present in 
      the 1st half of 1st row, 2nd half of 1st row, 
      1st half of 2nd row or 2nd half of 2nd row. 

Note: This approach works for the matrix n x m 
      where 2 <= n. The algorithm can be modified
      for matrix 1 x m, we just need to check whether
      2nd row exists or not      
```

**<u>例:</u>**

```
Consider:    | 1  2  3  4| 
x = 3, mat = | 5  6  7  8|   Middle column:
             | 9 10 11 12|    = {2, 6, 10, 14}
             |13 14 15 16|   perform binary search on them
                             since, x < 6, discard the 
                             last 2 rows as 'a' will 
                             not lie in them(sorted matrix)
Now, only two rows are left
             | 1  2  3  4| 
x = 3, mat = | 5  6  7  8|   Check whether element is present
                             on the middle elements of these
                             rows = {2, 6}
                             x != 2 or 6
If not, consider the four sub-parts
1st half of 1st row = {1}, 2nd half of 1st row = {3, 4}
1st half of 2nd row = {5}, 2nd half of 2nd row = {7, 8}

According the value of 'x' it will be searched in the
2nd half of 1st row = {3, 4} and found at (i, j): (0, 2)                              
```

## C++

```
// C++ implementation to search an element in a
// sorted matrix
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// This function does Binary search for x in i-th
// row. It does the search from mat[i][j_low] to
// mat[i][j_high]
void binarySearch(int mat[][MAX], int i, int j_low,
                                int j_high, int x)
{
    while (j_low <= j_high)
    {
        int j_mid = (j_low + j_high) / 2;

        // Element found
        if (mat[i][j_mid] == x)
        {
            cout << "Found at (" << i << ", "
                 << j_mid << ")";
            return;
        }

        else if (mat[i][j_mid] > x)
            j_high = j_mid - 1;

        else
            j_low = j_mid + 1;
    }

    // element not found
    cout << "Element no found";
}

// Function to perform binary search on the mid
// values of row to get the desired pair of rows
// where the element can be found
void sortedMatrixSearch(int mat[][MAX], int n,
                                  int m, int x)
{
    // Single row matrix
    if (n == 1)
    {
        binarySearch(mat, 0, 0, m-1, x);
        return;
    }

    // Do binary search in middle column.
    // Condition to terminate the loop when the
    // 2 desired rows are found
    int i_low = 0;
    int i_high = n-1;
    int j_mid = m/2;
    while ((i_low+1) < i_high)
    {
        int i_mid = (i_low + i_high) / 2;

        // element found
        if (mat[i_mid][j_mid] == x)
        {
            cout << "Found at (" << i_mid << ", "
                 << j_mid << ")";
            return;
        }

        else if (mat[i_mid][j_mid] > x)
            i_high = i_mid;

        else
            i_low = i_mid;
    }

    // If element is present on the mid of the
    // two rows
    if (mat[i_low][j_mid] == x)
        cout << "Found at (" << i_low << ","
             << j_mid << ")";
    else if (mat[i_low+1][j_mid] == x)
        cout << "Found at (" << (i_low+1)
             << ", " << j_mid << ")";

    // search element on 1st half of 1st row
    else if (x <= mat[i_low][j_mid-1])
        binarySearch(mat, i_low, 0, j_mid-1, x);

    // Search element on 2nd half of 1st row
    else if (x >= mat[i_low][j_mid+1]  &&
             x <= mat[i_low][m-1])
       binarySearch(mat, i_low, j_mid+1, m-1, x);

    // Search element on 1st half of 2nd row
    else if (x <= mat[i_low+1][j_mid-1])
        binarySearch(mat, i_low+1, 0, j_mid-1, x);

    // search element on 2nd half of 2nd row
    else
        binarySearch(mat, i_low+1, j_mid+1, m-1, x);
}

// Driver program to test above
int main()
{
    int n = 4, m = 5, x = 8;
    int mat[][MAX] = {{0, 6, 8, 9, 11},
                     {20, 22, 28, 29, 31},
                     {36, 38, 50, 61, 63},
                     {64, 66, 100, 122, 128}};

    sortedMatrixSearch(mat, n, m, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation to search
// an element in a sorted matrix
import java.io.*;

class GFG
{
    static int MAX = 100;

    // This function does Binary search for x in i-th
    // row. It does the search from mat[i][j_low] to
    // mat[i][j_high]
    static void binarySearch(int mat[][], int i, int j_low,
                                    int j_high, int x)
    {
        while (j_low <= j_high)
        {
            int j_mid = (j_low + j_high) / 2;

            // Element found
            if (mat[i][j_mid] == x)
            {
                System.out.println ( "Found at (" + i
                                     + ", " + j_mid +")");
                return;
            }

            else if (mat[i][j_mid] > x)
                j_high = j_mid - 1;

            else
                j_low = j_mid + 1;
        }

        // element not found
        System.out.println ( "Element no found");
    }

    // Function to perform binary search on the mid
    // values of row to get the desired pair of rows
    // where the element can be found
    static void sortedMatrixSearch(int mat[][], int n,
                                         int m, int x)
    {
        // Single row matrix
        if (n == 1)
        {
            binarySearch(mat, 0, 0, m - 1, x);
            return;
        }

        // Do binary search in middle column.
        // Condition to terminate the loop when the
        // 2 desired rows are found
        int i_low = 0;
        int i_high = n - 1;
        int j_mid = m / 2;
        while ((i_low + 1) < i_high)
        {
            int i_mid = (i_low + i_high) / 2;

            // element found
            if (mat[i_mid][j_mid] == x)
            {
                System.out.println ( "Found at (" + i_mid +", "
                                    + j_mid +")");
                return;
            }

            else if (mat[i_mid][j_mid] > x)
                i_high = i_mid;

            else
                i_low = i_mid;
        }

        // If element is present on
        // the mid of the two rows
        if (mat[i_low][j_mid] == x)
            System.out.println ( "Found at (" + i_low + ","
                                 + j_mid +")");
        else if (mat[i_low + 1][j_mid] == x)
            System.out.println ( "Found at (" + (i_low + 1)
                                + ", " + j_mid +")");

        // search element on 1st half of 1st row
        else if (x <= mat[i_low][j_mid - 1])
            binarySearch(mat, i_low, 0, j_mid - 1, x);

        // Search element on 2nd half of 1st row
        else if (x >= mat[i_low][j_mid + 1] &&
                 x <= mat[i_low][m - 1])
        binarySearch(mat, i_low, j_mid + 1, m - 1, x);

        // Search element on 1st half of 2nd row
        else if (x <= mat[i_low + 1][j_mid - 1])
            binarySearch(mat, i_low + 1, 0, j_mid - 1, x);

        // search element on 2nd half of 2nd row
        else
            binarySearch(mat, i_low + 1, j_mid + 1, m - 1, x);
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 4, m = 5, x = 8;
        int mat[][] = {{0, 6, 8, 9, 11},
                       {20, 22, 28, 29, 31},
                       {36, 38, 50, 61, 63},
                       {64, 66, 100, 122, 128}};

        sortedMatrixSearch(mat, n, m, x);

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 implementation
# to search an element in a
# sorted matrix
MAX = 100

# This function does Binary
# search for x in i-th
# row. It does the search
# from mat[i][j_low] to
# mat[i][j_high]
def binarySearch(mat, i, j_low,
                 j_high, x):

    while (j_low <= j_high):

        j_mid = (j_low + j_high) // 2

        # Element found
        if (mat[i][j_mid] == x):

            print("Found at (", i, ", ", j_mid, ")")
            return

        elif (mat[i][j_mid] > x):
            j_high = j_mid - 1

        else:
            j_low = j_mid + 1

    # Element not found
    print ("Element no found")

# Function to perform binary
# search on the mid values of
# row to get the desired pair of rows
# where the element can be found
def sortedMatrixSearch(mat, n, m, x):

    # Single row matrix
    if (n == 1):

        binarySearch(mat, 0, 0, m - 1, x)
        return

    # Do binary search in middle column.
    # Condition to terminate the loop
    # when the 2 desired rows are found
    i_low = 0
    i_high = n - 1
    j_mid = m // 2
    while ((i_low + 1) < i_high):

        i_mid = (i_low + i_high) // 2

        # element found
        if (mat[i_mid][j_mid] == x):

            print ("Found at (", i_mid, ", ", j_mid, ")")
            return

        elif (mat[i_mid][j_mid] > x):
            i_high = i_mid

        else:
            i_low = i_mid

    # If element is present on the mid of the
    # two rows
    if (mat[i_low][j_mid] == x):
        print ("Found at (" , i_low, ",", j_mid , ")")
    elif (mat[i_low + 1][j_mid] == x):
        print ("Found at (", (i_low + 1), ", ", j_mid, ")")

    # search element on 1st half of 1st row
    elif (x <= mat[i_low][j_mid - 1]):
        binarySearch(mat, i_low, 0, j_mid - 1, x)

    # Search element on 2nd half of 1st row
    elif (x >= mat[i_low][j_mid + 1] and
          x <= mat[i_low][m - 1]):
       binarySearch(mat, i_low, j_mid + 1, m - 1, x)

    # Search element on 1st half of 2nd row
    elif (x <= mat[i_low + 1][j_mid - 1]):
        binarySearch(mat, i_low + 1, 0, j_mid - 1, x)

    # Search element on 2nd half of 2nd row
    else:
        binarySearch(mat, i_low + 1, j_mid + 1, m - 1, x)

# Driver program to test above
if __name__ == "__main__":

    n = 4
    m = 5
    x = 8
    mat = [[0, 6, 8, 9, 11],
           [20, 22, 28, 29, 31],
           [36, 38, 50, 61, 63],
           [64, 66, 100, 122, 128]]
    sortedMatrixSearch(mat, n, m, x)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to search
// an element in a sorted matrix
using System;

class GFG
{
    // This function does Binary search for x in i-th
    // row. It does the search from mat[i][j_low] to
    // mat[i][j_high]
    static void binarySearch(int [,]mat, int i, int j_low,
                                        int j_high, int x)
    {
        while (j_low <= j_high)
        {
            int j_mid = (j_low + j_high) / 2;

            // Element found
            if (mat[i,j_mid] == x)
            {
                Console.Write ( "Found at (" + i +
                                ", " + j_mid +")");
                return;
            }

            else if (mat[i,j_mid] > x)
                j_high = j_mid - 1;

            else
                j_low = j_mid + 1;
        }

        // element not found
        Console.Write ( "Element no found");
    }

    // Function to perform binary search on the mid
    // values of row to get the desired pair of rows
    // where the element can be found
    static void sortedMatrixSearch(int [,]mat, int n,
                                        int m, int x)
    {
        // Single row matrix
        if (n == 1)
        {
            binarySearch(mat, 0, 0, m - 1, x);
            return;
        }

        // Do binary search in middle column.
        // Condition to terminate the loop when the
        // 2 desired rows are found
        int i_low = 0;
        int i_high = n - 1;
        int j_mid = m / 2;
        while ((i_low + 1) < i_high)
        {
            int i_mid = (i_low + i_high) / 2;

            // element found
            if (mat[i_mid,j_mid] == x)
            {

                Console.Write ( "Found at (" + i_mid +
                                ", "    + j_mid +")");
                return;
            }

            else if (mat[i_mid,j_mid] > x)
                i_high = i_mid;

            else
                i_low = i_mid;
        }

        // If element is present on
        // the mid of the two rows
        if (mat[i_low,j_mid] == x)
        Console.Write ( "Found at (" + i_low +
                           "," + j_mid +")");
        else if (mat[i_low + 1,j_mid] == x)
        Console.Write ( "Found at (" + (i_low
                   + 1) + ", " + j_mid +")");

        // search element on 1st half of 1st row
        else if (x <= mat[i_low,j_mid - 1])
            binarySearch(mat, i_low, 0, j_mid - 1, x);

        // Search element on 2nd half of 1st row
        else if (x >= mat[i_low,j_mid + 1] &&
                 x <= mat[i_low,m - 1])
        binarySearch(mat, i_low, j_mid + 1, m - 1, x);

        // Search element on 1st half of 2nd row
        else if (x <= mat[i_low + 1,j_mid - 1])
            binarySearch(mat, i_low + 1, 0, j_mid - 1, x);

        // search element on 2nd half of 2nd row
        else
            binarySearch(mat, i_low + 1, j_mid + 1, m - 1, x);
    }

    // Driver program
    public static void Main (String[] args)
    {
        int n = 4, m = 5, x = 8;
        int [,]mat = {{0, 6, 8, 9, 11},
                    {20, 22, 28, 29, 31},
                    {36, 38, 50, 61, 63},
                    {64, 66, 100, 122, 128}};

        sortedMatrixSearch(mat, n, m, x);
    }
}

// This code is contributed by parashar...
```

## java 描述语言

```
<script>

// Javascript implementation to search
// an element in a sorted matrix
let MAX = 100;

// This function does Binary search for x in i-th
// row. It does the search from mat[i][j_low] to
// mat[i][j_high]
function binarySearch(mat, i, j_low, j_high, x)
{
    while (j_low <= j_high)
    {
        let j_mid = Math.floor((j_low + j_high) / 2);

        // Element found
        if (mat[i][j_mid] == x)
        {
            document.write("Found at (" + i + ", " +
                           j_mid +")");
            return;
        }

        else if (mat[i][j_mid] > x)
            j_high = j_mid - 1;

        else
            j_low = j_mid + 1;
    }

    // Element not found
    document.write( "Element no found<br>");
}

// Function to perform binary search on the mid
// values of row to get the desired pair of rows
// where the element can be found
function sortedMatrixSearch(mat, n, m, x)
{

    // Single row matrix
    if (n == 1)
    {
        binarySearch(mat, 0, 0, m - 1, x);
        return;
    }

    // Do binary search in middle column.
    // Condition to terminate the loop when the
    // 2 desired rows are found
    let i_low = 0;
    let i_high = n - 1;
    let j_mid = Math.floor(m / 2);

    while ((i_low + 1) < i_high)
    {
        let i_mid = Math.floor((i_low + i_high) / 2);

        // Element found
        if (mat[i_mid][j_mid] == x)
        {
            document.write("Found at (" + i_mid +
                           ", " + j_mid +")");
            return;
        }

        else if (mat[i_mid][j_mid] > x)
            i_high = i_mid;
        else
            i_low = i_mid;
    }

    // If element is present on
    // the mid of the two rows
    if (mat[i_low][j_mid] == x)
        document.write("Found at (" + i_low +
                       "," + j_mid +")");
    else if (mat[i_low + 1][j_mid] == x)
        document.write("Found at (" + (i_low + 1) +
                       ", " + j_mid +")");

    // Search element on 1st half of 1st row
    else if (x <= mat[i_low][j_mid - 1])
        binarySearch(mat, i_low, 0, j_mid - 1, x);

    // Search element on 2nd half of 1st row
    else if (x >= mat[i_low][j_mid + 1] &&
             x <= mat[i_low][m - 1])
        binarySearch(mat, i_low, j_mid + 1,
                                     m - 1, x);

    // Search element on 1st half of 2nd row
    else if (x <= mat[i_low + 1][j_mid - 1])
        binarySearch(mat, i_low + 1, 0,
                          j_mid - 1, x);

    // search element on 2nd half of 2nd row
    else
        binarySearch(mat, i_low + 1, j_mid + 1,
                              m - 1, x);
}

// Driver code
let n = 4, m = 5, x = 8;
let mat = [ [ 0, 6, 8, 9, 11 ],
            [ 20, 22, 28, 29, 31 ],
            [ 36, 38, 50, 61, 63 ],
            [ 64, 66, 100, 122, 128 ] ];

sortedMatrixSearch(mat, n, m, x);

// This code is contributed by ab2127

</script>
```

**Output**

```
Found at (0,2)
```

时间复杂度:O(log n + log m)。需要 O(Log n)时间来找到所需的两行。那么在大小等于 m/2 的四个部分之一中，二分搜索法需要 O(Log m)时间。

这个方法是由**阿育什·乔哈里**贡献的。

**<u>方法二:</u>** 二维使用二分搜索法

这个方法也有同样的时间复杂度:O(log(m) + log(n))和辅助空间:O(1)，但是算法要容易得多，代码方式也更清晰易懂。

**方法:**我们可以观察到，我们想要查找的任何数字(比如 k)都必须存在于一行中，包括该行的第一个和最后一个元素(如果它存在的话)。因此，我们首先使用二分搜索法(O(logn))找到 k 必须位于的行，然后再次使用二分搜索法搜索该行(O(logm))。

**算法:**

1)首先我们会找到正确的行，其中 k=2 可能存在。为此，我们将在第一列和最后一列同时应用二分搜索法。

> 低=0，高=n-1
> 
> I)如果(k < first element of row(a[mid][0]) ) => k 必须存在于上一行中
> 
> => *高=中-1*；
> 
> ii)如果(k >行的最后一个元素(a[mid][m-1])= > k 必须存在于上面的行中
> 
> => *低=中+1*<u>；</u>
> 
> iii) if( k >行的第一个元素(a[mid][0])& k
> 
> => k 必须存在于此行中
> 
> => <u>像在一维数组中一样在这一行中应用二分搜索法</u>
> 
> iv) i)如果(k==行的第一个元素(a[mid][0]) || k==行的最后一个元素(a[mid][m-1])= >*找到*

```
Example:
let k=2; n=3,m=4;
    matrix a: [0, 1, 2, 3 ]
              [10,11,12,13]
              [20,21,22,23]

1) low=0, high=n-1(=2) => mid=1 //check 1st row     [0....3]
                                                 -->[10...13]<-- 
                                                    [20...23]                                                        
   k < a[mid][0] => high = mid-1;(=1)
2) low=0, high=1; =>mid=0; //check 0th row    -->[0...3]<--  
    k>a[mid][0] && k<a[mid][m-1]  => k must exist in this row

    now simply apply binary search in 1-D array: [0,1,2,3]                              
```

下面是上述算法的 Java 实现:

## C++

```
//C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

void binarySearch(int a[][MAX], int n, int m, int k, int x)
// x is the row number
{
    // now we simply have to apply binary search as we
    // did in a 1-D array, for the elements in row
    // number
    // x

    int l = 0, r = m - 1, mid;
    while (l <= r)
    {
        mid = (l + r) / 2;

        if (a[x][mid] == k)
        {
            cout << "Found at (" << x << "," << mid << ")" << endl;
            return;
        }

        if (a[x][mid] > k)
            r = mid - 1;
        if (a[x][mid] < k)
            l = mid + 1;
    }
    cout << "Element not found" << endl;
}

void findRow(int a[][MAX], int n, int m, int k)
{

    int l = 0, r = n - 1, mid;

    while (l <= r)
    {
        mid = (l + r) / 2;

        // we'll check the left and
        // right most elements
        // of the row here itself
        // for efficiency
        if (k == a[mid][0]) // checking leftmost element
        {
            cout << "Found at (" << mid << ",0)" << endl;
            return;
        }

        if (k == a[mid][m - 1]) // checking rightmost
                                // element
        {
            int t = m - 1;
            cout << "Found at (" << mid << "," << t << ")" << endl;
            return;
        }

        if (k > a[mid][0] && k < a[mid][m - 1])
        // this means the element
        // must be within this row
        {
            binarySearch(a, n, m, k, mid);
            // we'll apply binary
            // search on this row
            return;
        }

        if (k < a[mid][0])
            r = mid - 1;
        if (k > a[mid][m - 1])
            l = mid + 1;
    }
}

//Driver Code
int main()
{
    int n = 4; // no. of rows
    int m = 5; // no. of columns

    int a[][MAX] = {{0, 6, 8, 9, 11},
                    {20, 22, 28, 29, 31},
                    {36, 38, 50, 61, 63},
                    {64, 66, 100, 122, 128}};

    int k = 31; // element to search

    findRow(a, n, m, k);

    return 0;
}
// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main {

    static void findRow(int[][] a, int n, int m, int k)
    {
        int l = 0, r = n - 1, mid;

        while (l <= r) {
            mid = (l + r) / 2;

            // we'll check the left and
            // right most elements
            // of the row here itself
            // for efficiency
            if (k == a[mid][0]) // checking leftmost element
            {
                System.out.println("Found at (" + mid + ","
                                   + "0)");
                return;
            }

            if (k == a[mid][m - 1]) // checking rightmost
                                    // element
            {
                int t = m - 1;
                System.out.println("Found at (" + mid + ","
                                   + t + ")");
                return;
            }

            if (k > a[mid][0]
                && k < a[mid]
                        [m - 1]) // this means the element
                                 // must be within this row
            {
                binarySearch(a, n, m, k,
                             mid); // we'll apply binary
                                   // search on this row
                return;
            }

            if (k < a[mid][0])
                r = mid - 1;
            if (k > a[mid][m - 1])
                l = mid + 1;
        }
    }

    static void binarySearch(int[][] a, int n, int m, int k,
                             int x) // x is the row number
    {
        // now we simply have to apply binary search as we
        // did in a 1-D array, for the elements in row
        // number
        // x

        int l = 0, r = m - 1, mid;
        while (l <= r) {
            mid = (l + r) / 2;

            if (a[x][mid] == k) {
                System.out.println("Found at (" + x + ","
                                   + mid + ")");
                return;
            }

            if (a[x][mid] > k)
                r = mid - 1;
            if (a[x][mid] < k)
                l = mid + 1;
        }
        System.out.println("Element not found");
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 4; // no. of rows
        int m = 5; // no. of columns

        int a[][] = { { 0, 6, 8, 9, 11 },
                      { 20, 22, 28, 29, 31 },
                      { 36, 38, 50, 61, 63 },
                      { 64, 66, 100, 122, 128 } };

        int k = 31; // element to search

        findRow(a, n, m, k);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach
def findRow(a, n, m, k):
    l = 0
    r = n - 1
    mid = 0
    while (l <= r) :
        mid = int((l + r) / 2)

        # we'll check the left and
        # right most elements
        # of the row here itself
        # for efficiency
        if(k == a[mid][0]): #checking leftmost element
            print("Found at (" , mid , ",", "0)", sep = "")
            return

        if(k == a[mid][m - 1]): # checking rightmost element
            t = m - 1
            print("Found at (" , mid , ",", t , ")", sep = "")
            return
        if(k > a[mid][0] and k < a[mid][m - 1]):    # this means the element
                                                    # must be within this row
            binarySearch(a, n, m, k, mid)    # we'll apply binary
                                            # search on this row
            return
        if (k < a[mid][0]):
            r = mid - 1
        if (k > a[mid][m - 1]):
            l = mid + 1

def binarySearch(a, n, m, k, x):    #x is the row number

    # now we simply have to apply binary search as we
    # did in a 1-D array, for the elements in row
    # number
    # x
    l = 0
    r = m - 1
    mid = 0
    while (l <= r):
        mid = int((l + r) / 2)

        if (a[x][mid] == k):
            print("Found at (" , x , ",", mid , ")", sep = "")
            return
        if (a[x][mid] > k):
            r = mid - 1
        if (a[x][mid] < k):
            l = mid + 1

    print("Element not found")

# Driver Code
n = 4 # no. of rows
m = 5 # no. of columns
a = [[ 0, 6, 8, 9, 11], [20, 22, 28, 29, 31], [36, 38, 50, 61, 63 ], [64, 66, 100, 122, 128]]
k = 31  # element to search
findRow(a, n, m, k)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  static void findRow(int[,] a, int n, int m, int k)
  {
    int l = 0, r = n - 1, mid;

    while (l <= r) {
      mid = (l + r) / 2;

      // we'll check the left and
      // right most elements
      // of the row here itself
      // for efficiency
      if (k == a[mid,0]) // checking leftmost element
      {
        Console.WriteLine("Found at (" + mid + ","
                          + "0)");
        return;
      }

      if (k == a[mid,m - 1]) // checking rightmost
        // element
      {
        int t = m - 1;
        Console.WriteLine("Found at (" + mid + ","
                          + t + ")");
        return;
      }

      if (k > a[mid,0]
          && k < a[mid,m - 1]) // this means the element
        // must be within this row
      {
        binarySearch(a, n, m, k,
                     mid); // we'll apply binary
        // search on this row
        return;
      }

      if (k < a[mid,0])
        r = mid - 1;
      if (k > a[mid,m - 1])
        l = mid + 1;
    }
  }

  static void binarySearch(int[,] a, int n, int m, int k,
                           int x) // x is the row number
  {
    // now we simply have to apply binary search as we
    // did in a 1-D array, for the elements in row
    // number
    // x

    int l = 0, r = m - 1, mid;
    while (l <= r) {
      mid = (l + r) / 2;

      if (a[x,mid] == k) {
        Console.WriteLine("Found at (" + x + ","
                          + mid + ")");
        return;
      }

      if (a[x,mid] > k)
        r = mid - 1;
      if (a[x,mid] < k)
        l = mid + 1;
    }
    Console.WriteLine("Element not found");
  }

  // Driver Code
  static public void Main ()
  {
    int n = 4; // no. of rows
    int m = 5; // no. of columns

    int[,] a = { { 0, 6, 8, 9, 11 },
                { 20, 22, 28, 29, 31 },
                { 36, 38, 50, 61, 63 },
                { 64, 66, 100, 122, 128 } };

    int k = 31; // element to search

    findRow(a, n, m, k);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// JavaScript program for above approach
var MAX = 100;

function binarySearch(a, n, m, k, x)
// x is the row number
{
    // now we simply have to apply binary search as we
    // did in a 1-D array, for the elements in row
    // number
    // x

    var l = 0, r = m - 1, mid;
    while (l <= r)
    {
        mid = (l + r) / 2;

        if (a[x][mid] == k)
        {
            document.write( "Found at (" + x + "," + mid + ")<br>");
            return;
        }

        if (a[x][mid] > k)
            r = mid - 1;
        if (a[x][mid] < k)
            l = mid + 1;
    }
    document.write( "Element not found<br>");
}

function findRow(a, n, m, k)
{

    var l = 0, r = n - 1, mid;

    while (l <= r)
    {
        mid = parseInt((l + r) / 2);

        // we'll check the left and
        // right most elements
        // of the row here itself
        // for efficiency
        if (k == a[mid][0]) // checking leftmost element
        {
            document.write( "Found at (" + mid + ",0)<br>");
            return;
        }

        if (k == a[mid][m - 1]) // checking rightmost
                                // element
        {
            var t = m - 1;
            document.write( "Found at (" + mid + "," + t + ")<br>");
            return;
        }

        if (k > a[mid][0] && k < a[mid][m - 1])
        // this means the element
        // must be within this row
        {
            binarySearch(a, n, m, k, mid);
            // we'll apply binary
            // search on this row
            return;
        }

        if (k < a[mid][0])
            r = mid - 1;
        if (k > a[mid][m - 1])
            l = mid + 1;
    }
}

//Driver Code
var n = 4; // no. of rows
var m = 5; // no. of columns
var a = [[0, 6, 8, 9, 11],
                [20, 22, 28, 29, 31],
                [36, 38, 50, 61, 63],
                [64, 66, 100, 122, 128]];
var k = 31; // element to search
findRow(a, n, m, k);

</script>
```

**Output**

```
Found at (1,4)
```

这种方法是由**阿尤施旺·高拉夫**贡献的。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。