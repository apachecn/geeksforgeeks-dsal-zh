# 检查是否可以通过只交换相应的值来使两个矩阵严格递增

> 原文:[https://www . geeksforgeeks . org/check-如果有可能制作两个矩阵-仅通过交换对应值严格递增/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-make-two-matrices-strictly-increasing-by-swapping-corresponding-values-only/)

给定两个 **n * m** 矩阵 **A[][]** 和 **B[][]** ，任务是仅通过交换不同矩阵中的两个元素(如果它们位于相应的位置，即 **A[i][j]** 只能与 **B[i][j]** 交换)来使两个矩阵严格递增(行和列)。如果可能，则打印**是**否则，**否**。
**示例:**

```
Input: 
A[][] = {{2, 10},      B[][] = {{9, 4},  
         {11, 5}}               {3, 12}}
Output: Yes
Swap 2 with 9 and 5 with 12 then the resulting 
matrices will be strictly increasing.

Input: 
A[][] = {{1, 3},       B[][] = {{3, 1}, 
         {2, 4},                {3, 6}, 
         {5, 10}}               {4, 8}}
Output: No
```

**进场:**我们可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题。如果 **A[i][j] > B[i][j]** ，则用 **B[i][j]** 替换 **A[i][j]** 。在每个 **i** 和 **j** 的末尾，我们有 **A[i][j] ≤ B[i][j]** 。
如果结果矩阵严格递增，则打印**是**否则，打印**否**。
以下是上述办法的实施情况:

## C++

```
#include<bits/stdc++.h>
using namespace std;

// Function to check whether the matrices 
// can be made strictly increasing 
// with the given operation
string Check(int a[][2], int b[][2], int n, int m)
{

    // Swap only when a[i][j] > b[i][j]
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (a[i][j] > b[i][j])
                swap(a[i][j], b[i][j]);

    // Check if rows are strictly increasing
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m - 1; j++)
            if(a[i][j] >= a[i][j + 1] || b[i][j] >= b[i][j + 1])
                return "No";

    // Check if columns are strictly increasing
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < m ;j++)
            if (a[i][j] >= a[i + 1][j] || b[i][j] >= b[i + 1][j])
                return "No";

    return "Yes";
}

// Driver code
int main()
{ 
    int n = 2, m = 2;
    int a[][2] = {{2, 10}, {11, 5}};
    int b[][2] = {{9, 4}, {3, 12}};
    cout << (Check(a, b,n,m));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// Function to check whether the matrices 
// can be made strictly increasing 
// with the given operation
public static String Check(int a[][], int b[][],
                           int n, int m)
{

    // Swap only when a[i][j] > b[i][j]
    for(int i = 0; i < n; i++)
        for(int j = 0; j < m; j++)
            if (a[i][j] > b[i][j])
            {
                int temp = a[i][j];
                a[i][j] = b[i][j];
                b[i][j] = temp;
            }

    // Check if rows are strictly increasing
    for(int i = 0; i < n; i++)
        for(int j = 0; j < m - 1; j++)
            if (a[i][j] >= a[i][j + 1] ||
                b[i][j] >= b[i][j + 1])
                return "No";

    // Check if columns are strictly increasing
    for(int i = 0; i < n - 1; i++)
        for(int j = 0; j < m ;j++)
            if (a[i][j] >= a[i + 1][j] ||
                b[i][j] >= b[i + 1][j])
                return "No";

    return "Yes";
}   

// Driver code
public static void main(String[] args)
{
    int n = 2, m = 2;
    int a[][] = { { 2, 10 }, { 11, 5 } };
    int b[][] = { { 9, 4 }, { 3, 12 } };

    System.out.print(Check(a, b, n, m));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Function to check whether the matrices 
# can be made strictly increasing 
# with the given operation
def Check(a, b):

    # Swap only when a[i][j] > b[i][j]
    for i in range(n):
        for j in range(m):
            if a[i][j]>b[i][j]:
                a[i][j], b[i][j]= b[i][j], a[i][j]

    # Check if rows are strictly increasing
    for i in range(n):
        for j in range(m-1):
            if(a[i][j]>= a[i][j + 1] or b[i][j]>= b[i][j + 1]):
                return "No"

    # Check if columns are strictly increasing
    for i in range(n-1):
        for j in range(m):
            if (a[i][j]>= a[i + 1][j] or b[i][j]>= b[i + 1][j]):
                return "No"

    return "Yes"

# Driver code
if __name__=="__main__":

    n, m = 2, 2
    a =[[2, 10], [11, 5]]
    b =[[9, 4], [3, 12]]
    print(Check(a, b))
```

## C#

```
// C# implementation of the 
// above approach 
using System;
using System.Collections;
class GfG{

// Function to check 
// whether the matrices 
// can be made strictly 
// increasing with the 
// given operation
static string Check(int [,]a, int [,]b, 
                    int n, int m)
{
  // Swap only when 
  // a[i][j] > b[i][j]
  for (int i = 0; i < n; i++)
    for (int j = 0; j < m; j++)
      if (a[i, j] > b[i, j])
      {
        int tmp = a[i, j];
        a[i, j] = b[i, j];
        b[i, j] = tmp;
      }

  // Check if rows are 
  // strictly increasing
  for (int i = 0; i < n; i++)
    for (int j = 0; j < m - 1; j++)
      if(a[i, j] >= a[i, j + 1] || 
         b[i, j] >= b[i, j + 1])
        return "No";

  // Check if columns are 
  // strictly increasing
  for (int i = 0; i < n - 1; i++)
    for (int j = 0; j < m ; j++)
      if (a[i, j] >= a[i + 1, j] || 
          b[i, j] >= b[i + 1, j])
        return "No";

  return "Yes";
}

// Driver Code
public static void Main(string []arg)
{
  int n = 2, m = 2;
  int [,]a = {{2, 10}, {11, 5}};
  int [,]b = {{9, 4}, {3, 12}};
  Console.Write(Check(a, b, n, m));
}
}

// This code is contributed by Rutvik_56
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach 

// Function to check whether the matrices 
// can be made strictly increasing 
// with the given operation 
function Check($a, $b, $n, $m)
{ 

    // Swap only when a[i][j] > b[i][j] 
    for ($i = 0; $i < $n; $i++)
    { 
        for ($j= 0; $j < $n; $j++)
        { 
            if ($a[$i][$j] > $b[$i][$j]) 
            {
                $temp = $a[$i][$j];
                $a[$i][$j] = $b[$i][$j];
                $b[$i][$j] = $temp;
            }
        }
    }

    // Check if rows are strictly increasing 
    for ($i = 0; $i < $n; $i++)
    { 
        for ($j= 0;$j < $m-1 ; $j++)
        { 
            if($a[$i][$j] >= $a[$i][$j + 1] or 
               $b[$i][$j] >= $b[$i][$j + 1])
                return "No";
        }
    }

    // Check if columns are strictly increasing 
    for ($i = 0; $i < $n - 1; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        { 
            if ($a[$i][$j] >= $a[$i + 1][$j] or 
                $b[$i][$j] >= $b[$i + 1][$j])
                return "No";
        }
    }
    return "Yes";
}

// Driver code 
$n = 2; $m = 2;
$a = array(array(2, 10), array(11, 5)); 
$b = array(array(9, 4), array(3, 12)); 
print(Check($a, $b, $n, $m));

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Function to check whether the matrices
// can be made strictly increasing
// with the given operation
function Check(a, b, n, m)
{

    // Swap only when a[i][j] > b[i][j]
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m; j++)
            if (a[i][j] > b[i][j])
            {
                let temp = a[i][j];
                a[i][j] = b[i][j];
                b[i][j] = temp;
            }

    // Check if rows are strictly increasing
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m - 1; j++)
            if (a[i][j] >= a[i][j + 1] ||
                b[i][j] >= b[i][j + 1])
                return "No";

    // Check if columns are strictly increasing
    for(let i = 0; i < n - 1; i++)
        for(let j = 0; j < m ;j++)
            if (a[i][j] >= a[i + 1][j] ||
                b[i][j] >= b[i + 1][j])
                return "No";

    return "Yes";
}  

// Driver Code

        let n = 2, m = 2;
    let a = [[ 2, 10 ], [ 11, 5 ]];
    let b = [[ 9, 4 ],  [3, 12 ]];

    document.write(Check(a, b, n, m));

</script>
```

**Output:** 

```
Yes
```