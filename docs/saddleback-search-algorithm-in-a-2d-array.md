# 2D 阵列中的鞍背搜索算法

> 原文:[https://www . geeksforgeeks . org/saddle back-search-algorithm in-a-2d-array/](https://www.geeksforgeeks.org/saddleback-search-algorithm-in-a-2d-array/)

在给定的矩阵中找到一个元素，这样每一行和每一列都会被排序。
**例:**

```
Input : arr[] = {
                 { 1, 2, 3},
                 { 4, 5, 6},
                 { 7, 8, 9}
                }
         element=5
Output : Element Found at position (1, 1).

Input : arr[]={
              { 11, 21, 31, 41, 51 },
              { 12, 22, 32, 42, 52 },
              { 13, 23, 33, 43, 53 },
              { 14, 24, 34, 44, 54 },
              { 15, 25, 35, 45, 55 }
              }
        element=11

Output : Element Found at position (0, 0).
```

一个**简单的解决方法**就是一个个搜索。这个解的时间复杂度为 O(n <sup>2</sup> )。
一个**更好的解决方案**就是[用分治法找到元素](https://www.geeksforgeeks.org/divide-conquer-set-6-search-row-wise-column-wise-sorted-2d-array/)。这个解的时间复杂度为 O(n <sup>1.58</sup> )。详见这篇文章。
下面是一个在 O(m + n)时间内工作的**高效解决方案**。
1)从左下元素
开始 2)循环:将这个元素 e 与 x
进行比较……I)如果它们相等，则返回其位置
…ii) e x，然后将其向右移动(如果超出矩阵的界限，则断开返回 false)
3)重复 I)、ii)和 iii)直到您找到一个元素或返回 false
感谢 devendraiiit 建议下面的方法。
**实现:**

## C++

```
// C++ program to search an element in row-wise
// and column-wise sorted matrix
#include<bits/stdc++.h>
using namespace std;
#define MAX 100

/* Searches the element x in mat[m][n]. If the
   element is found, then prints its position
   and returns true, otherwise prints "not found"
   and returns false */
bool search(int mat[][MAX], int m, int n, int x)
{
   int i = m-1, j = 0;  //set indexes for bottom left element
   while ( i >= 0 && j < n )
   {
      if ( mat[i][j] == x )
         return true;
      if ( mat[i][j] > x )
        i--;
      else //  if mat[i][j] < x
        j++;
   }

   return false;
}

// driver program to test above function
int main()
{
  int mat[][MAX] = { {10, 20, 30, 40},
                     {15, 25, 35, 45},
                     {27, 29, 37, 48},
                     {32, 33, 39, 50},
                     {50, 60, 70, 80},
                  };
  if (search(mat, 5, 4, 29))
      cout << "Yes";
  else
      cout << "No";
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to search an
// element in row-wise and
// column-wise sorted matrix

class GFG
{
static final int MAX = 100;

/* Searches the element x
in mat[m][n]. If the element
is found, then prints its
position and returns true,
otherwise prints "not found"
and returns false */
static boolean search(int mat[][], int m,
                      int n, int x)
{

    // set indexes for
    // bottom left element
    int i = m - 1, j = 0;
        while (i >= 0 && j < n)
        {
            if (mat[i][j] == x)
                return true;
            if (mat[i][j] > x)
                i--;
            else // if mat[i][j] < x
                j++;
        }

        return false;
}

// Driver Code
public static void main(String args[])
{
int mat[][] = {{10, 20, 30, 40},
               {15, 25, 35, 45},
               {27, 29, 37, 48},
               {32, 33, 39, 50},
               {50, 60, 70, 80}};
if (search(mat, 5, 4, 29))
    System.out.println("Yes");
else
    System.out.println("No");
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python program to search an element in
# row-wise and column-wise sorted matrix

# define MAX 100

# Searches the element x in mat[m][n].
# If the element is found, then prints
# its position and returns true, otherwise
# prints "not found" and returns false
def search(mat, m, n, x):
    i, j = m - 1, 0 # set indexes for bottom
                    # left element
    while (i >= 0 and j < n):
        if (mat[i][j] == x):
            return True;
        if (mat[i][j] > x):
            i -= 1
        else: # if mat[i][j] < x
            j += 1
    return False

# Driver Code
if __name__ == '__main__':
    mat = [[10, 20, 30, 40],
           [15, 25, 35, 45],
           [27, 29, 37, 48],
           [32, 33, 39, 50],
           [50, 60, 70, 80]]

    if (search(mat, 5, 4, 29)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to search an
// element in row-wise and
// column-wise sorted matrix
using System;

class GFG
{

/* Searches the element x
in mat[m][n]. If the element
is found, then prints its
position and returns true,
otherwise prints "not found"
and returns false */
static bool search(int[,] mat, int m,
                   int n, int x)
{

    // set indexes for
    // bottom left element
    int i = m - 1, j = 0;
        while (i >= 0 && j < n)
        {
            if (mat[i, j] == x)
                return true;
            if (mat[i, j] > x)
                i--;
            else // if mat[i][j] < x
                j++;
        }

        return false;
}

// Driver Code
public static void Main()
{
int [,]mat = {{10, 20, 30, 40},
              {15, 25, 35, 45},
              {27, 29, 37, 48},
              {32, 33, 39, 50},
              {50, 60, 70, 80}};
if (search(mat, 5, 4, 29))
    Console.WriteLine("Yes");
else
    Console.WriteLine("No");
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to search an element in row-wise
// and column-wise sorted matrix

$MAX = 100;

/* Searches the element x in mat[m][n]. If the
element is found, then prints its position
and returns true, otherwise prints "not found"
and returns false */
function search($mat, $m, $n, $x)
{
    $i = $m - 1;
    $j = 0; // set indexes for bottom left element
    while ($i >= 0 && $j < $n)
    {
        if ($mat[$i][$j] == $x)
            return true;
        if ($mat[$i][$j] > $x)
            $i--;
        else // if mat[i][j] < x
            $j++;
    }

    return false;
}

// Driver Code
$mat = array(array(10, 20, 30, 40),
             array(15, 25, 35, 45),
             array(27, 29, 37, 48),
             array(32, 33, 39, 50),
             array(50, 60, 70, 80));
if (search($mat, 5, 4, 29))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to search an
// element in row-wise and
// column-wise sorted matrix

/* Searches the element x
in mat[m][n]. If the element
is found, then prints its
position and returns true,
otherwise prints "not found"
and returns false */
function search(mat, m, n, x)
{

    // set indexes for
    // bottom left element
    var i = m - 1, j = 0;
        while (i >= 0 && j < n)
        {
            if (mat[i][j] == x)
                return true;
            if (mat[i][j] > x)
                i--;
            else // if mat[i][j] < x
                j++;
        }

        return false;
}

// Driver Code
var mat = [[10, 20, 30, 40],
              [15, 25, 35, 45],
              [27, 29, 37, 48],
              [32, 33, 39, 50],
              [50, 60, 70, 80]];
if (search(mat, 5, 4, 29))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(m + n)
以上也可以从右上角开始实现。请参见[在行方向和列方向排序矩阵中的搜索](https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/)了解替代实现。