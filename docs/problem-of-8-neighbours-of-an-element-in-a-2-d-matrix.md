# 二维矩阵中一个元素的 8 个邻域的问题

> 原文:[https://www . geeksforgeeks . org/矩阵中元素的 8 个邻居问题/](https://www.geeksforgeeks.org/problem-of-8-neighbours-of-an-element-in-a-2-d-matrix/)

给定二维矩阵和整数“K”，任务是在“K”次迭代后预测矩阵，如下所示:

> *   Element 1 in the current matrix will remain 1 in the next iteration only if it is surrounded by multiple 1s, where 0 < = range 1a < = A < = range 1b.
> *   The element 0 in the current matrix will only become 1 in the next iteration if it is surrounded by the number of b of 1, where 0<= range 0a<= B<= range 0b.

**我们用一个例子来理解一下:**

> 约束:
> 1<= K<= 100000
> 0<=范围 1a、范围 1b、范围 0a、范围 0b < = 8

*   在上述单元格(0，0)的图像中，单元格在第一次迭代中为“0”，但由于它仅被一个包含“1”的相邻单元格包围，因此不在范围[range0a，range0b]内。因此它将继续保持“0”。
*   对于第二次迭代，单元格(0，0)为 0，但这次它被两个包含“1”的单元格包围，两个单元格位于范围[range0a，range0b]内。因此，它在下一次(第二次)迭代中变为“1”。

**示例:**

> **输入:**范围 1a = 2
> 范围 1b = 2
> 范围 0a = 2
> 范围 0b = 3
> K = 1
> **输出:**
> 0 1 1 0
> 0 1 1
> 1 0 0 1
> 0 0 1 0
> **输入:**范围 1a = 2
> 范围 1b = 2
> 范围 0a = 2
> 范围 0b = 3

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Dimension of Array
#define N 4

void predictMatrix(int arr[N][N],
                   int range1a,
                   int range1b,
                   int range0a,
                   int range0b,
                   int K,
                   int b[N][N])
{

    // Count of 1s
    int c = 0;

    while (K--) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                c = 0;

                // Counting all neighbouring 1s

                if (i > 0 && arr[i - 1][j] == 1)
                    c++;
                if (j > 0 && arr[i][j - 1] == 1)
                    c++;
                if (i > 0 && j > 0
                    && arr[i - 1][j - 1] == 1)
                    c++;
                if (i < N - 1 && arr[i + 1][j] == 1)
                    c++;
                if (j < N - 1 && arr[i][j + 1] == 1)
                    c++;
                if (i < N - 1 && j < N - 1
                    && arr[i + 1][j + 1] == 1)
                    c++;
                if (i < N - 1 && j > 0
                    && arr[i + 1][j - 1] == 1)
                    c++;
                if (i > 0 && j < N - 1
                    && arr[i - 1][j + 1] == 1)
                    c++;

                // Comparing the number of
                // neighbouring 1s with
                // given ranges
                if (arr[i][j] == 1) {
                    if (c >= range1a && c <= range1b)
                        b[i][j] = 1;
                    else
                        b[i][j] = 0;
                }
                if (arr[i][j] == 0) {
                    if (c >= range0a && c <= range0b)
                        b[i][j] = 1;
                    else
                        b[i][j] = 0;
                }
            }
        }

        // Copying changes to
        // the main matrix
        for (int k = 0; k < N; k++)
            for (int m = 0; m < N; m++)
                arr[k][m] = b[k][m];
    }
}

// Driver code
int main()
{
    int arr[N][N] = { 0, 0, 0, 0,
                      0, 1, 1, 0,
                      0, 0, 1, 0,
                      0, 1, 0, 1 };
    int range1a = 2, range1b = 2;
    int range0a = 2, range0b = 3;
    int K = 3, b[N][N] = { 0 };

    // Function call to calculate
    // the resultant matrix
    // after 'K' iterations.
    predictMatrix(arr, range1a, range1b,
                  range0a, range0b, K, b);

    // Printing Result
    for (int i = 0; i < N; i++) {
        cout << endl;
        for (int j = 0; j < N; j++)
            cout << b[i][j] << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG{

// Dimension of Array
final static int N  = 4 ;

static void predictMatrix(int arr[][],
                   int range1a,
                   int range1b,
                   int range0a,
                   int range0b,
                   int K,
                   int b[][])
{

    // Count of 1s
    int c = 0;

    while (K != 0) {
        K--;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                c = 0;

                // Counting all neighbouring 1s

                if (i > 0 && arr[i - 1][j] == 1)
                    c++;
                if (j > 0 && arr[i][j - 1] == 1)
                    c++;
                if (i > 0 && j > 0
                    && arr[i - 1][j - 1] == 1)
                    c++;
                if (i < N - 1 && arr[i + 1][j] == 1)
                    c++;
                if (j < N - 1 && arr[i][j + 1] == 1)
                    c++;
                if (i < N - 1 && j < N - 1
                    && arr[i + 1][j + 1] == 1)
                    c++;
                if (i < N - 1 && j > 0
                    && arr[i + 1][j - 1] == 1)
                    c++;
                if (i > 0 && j < N - 1
                    && arr[i - 1][j + 1] == 1)
                    c++;

                // Comparing the number of
                // neighbouring 1s with
                // given ranges
                if (arr[i][j] == 1) {
                    if (c >= range1a && c <= range1b)
                        b[i][j] = 1;
                    else
                        b[i][j] = 0;
                }
                if (arr[i][j] == 0) {
                    if (c >= range0a && c <= range0b)
                        b[i][j] = 1;
                    else
                        b[i][j] = 0;
                }
            }
        }

        // Copying changes to
        // the main matrix
        for (int k = 0; k < N; k++)
            for (int m = 0; m < N; m++)
                arr[k][m] = b[k][m];
    }

}

// Driver code
public static void main(String []args)
{
    int arr[][] = { {0, 0, 0, 0},
                      {0, 1, 1, 0},
                      {0, 0, 1, 0},
                      {0, 1, 0, 1 } };
    int range1a = 2, range1b = 2;
    int range0a = 2, range0b = 3;
    int K = 3;
    int b[][] = new int[N][N] ;

    // Function call to calculate
    // the resultant matrix
    // after 'K' iterations.
    predictMatrix(arr, range1a, range1b,
                  range0a, range0b, K, b);

    // Printing Result
    for (int i = 0; i < N; i++) {
        System.out.println();
        for (int j = 0; j < N; j++)
            System.out.print(b[i][j]+ " ");
    }

}
// This Code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Dimension of Array
N = 4

def predictMatrix(arr, range1a, range1b,
                  range0a, range0b, K, b):

    # Count of 1s
    c = 0

    while (K):
        for i in range(N) :
            for j in range(N):
                c = 0

                # Counting all neighbouring 1s
                if (i > 0 and arr[i - 1][j] == 1):
                    c += 1
                if (j > 0 and arr[i][j - 1] == 1):
                    c += 1
                if (i > 0 and j > 0 and
                    arr[i - 1][j - 1] == 1):
                    c += 1
                if (i < N - 1 and arr[i + 1][j] == 1):
                    c += 1
                if (j < N - 1 and arr[i][j + 1] == 1):
                    c += 1
                if (i < N - 1 and j < N - 1
                    and arr[i + 1][j + 1] == 1):
                    c += 1
                if (i < N - 1 and j > 0
                    and arr[i + 1][j - 1] == 1):
                    c += 1
                if (i > 0 and j < N - 1
                    and arr[i - 1][j + 1] == 1):
                    c += 1

                # Comparing the number of neighbouring
                # 1s with given ranges
                if (arr[i][j] == 1) :
                    if (c >= range1a and c <= range1b):
                        b[i][j] = 1
                    else:
                        b[i][j] = 0

                if (arr[i][j] == 0):
                    if (c >= range0a and c <= range0b):
                        b[i][j] = 1
                    else:
                        b[i][j] = 0
        K -= 1

        # Copying changes to the main matrix
        for k in range(N):
            for m in range( N):
                arr[k][m] = b[k][m]

# Driver code
if __name__ == "__main__":

    arr = [[0, 0, 0, 0],
           [0, 1, 1, 0],
           [0, 0, 1, 0],
           [0, 1, 0, 1]]
    range1a = 2
    range1b = 2
    range0a = 2
    range0b = 3
    K = 3
    b = [[0 for x in range(N)]
            for y in range(N)]

    # Function call to calculate
    # the resultant matrix
    # after 'K' iterations.
    predictMatrix(arr, range1a, range1b,
                  range0a, range0b, K, b)

    # Printing Result
    for i in range( N):
        print()
        for j in range(N):
            print(b[i][j], end = " ")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Dimension of Array
readonly static int N = 4 ;

static void predictMatrix(int [,]arr, int range1a,
                          int range1b, int range0a,
                          int range0b, int K, int [,]b)
{

    // Count of 1s
    int c = 0;

    while (K != 0)
    {
        K--;
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                c = 0;

                // Counting all neighbouring 1s

                if (i > 0 && arr[i - 1, j] == 1)
                    c++;
                if (j > 0 && arr[i, j - 1] == 1)
                    c++;
                if (i > 0 && j > 0
                    && arr[i - 1, j - 1] == 1)
                    c++;
                if (i < N - 1 && arr[i + 1, j] == 1)
                    c++;
                if (j < N - 1 && arr[i, j + 1] == 1)
                    c++;
                if (i < N - 1 && j < N - 1 &&
                    arr[i + 1, j + 1] == 1)
                    c++;
                if (i < N - 1 && j > 0 &&
                    arr[i + 1, j - 1] == 1)
                    c++;
                if (i > 0 && j < N - 1 &&
                    arr[i - 1, j + 1] == 1)
                    c++;

                // Comparing the number of
                // neighbouring 1s with
                // given ranges
                if (arr[i,j] == 1)
                {
                    if (c >= range1a && c <= range1b)
                        b[i, j] = 1;
                    else
                        b[i, j] = 0;
                }
                if (arr[i,j] == 0)
                {
                    if (c >= range0a && c <= range0b)
                        b[i, j] = 1;
                    else
                        b[i, j] = 0;
                }
            }
        }

        // Copying changes to the main matrix
        for (int k = 0; k < N; k++)
            for (int m = 0; m < N; m++)
                arr[k, m] = b[k, m];
    }
}

// Driver code
public static void Main()
{
    int [,]arr = { {0, 0, 0, 0},
                   {0, 1, 1, 0},
                   {0, 0, 1, 0},
                   {0, 1, 0, 1 } };
    int range1a = 2, range1b = 2;
    int range0a = 2, range0b = 3;
    int K = 3;
    int [,]b = new int[N, N];

    // Function call to calculate
    // the resultant matrix
    // after 'K' iterations.
    predictMatrix(arr, range1a, range1b,
                range0a, range0b, K, b);

    // Printing Result
    for (int i = 0; i < N; i++)
    {
        Console.WriteLine();
        for (int j = 0; j < N; j++)
            Console.Write(b[i, j] + " ");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Dimension of Array
#define N 4

function predictMatrix($arr, $range1a, $range1b,
                       $range0a, $range0b, $K, $b)
{
$N = 4;
    // Count of 1s
    $c = 0;

    while ($K--)
    {
        for ($i = 0; $i < $N; $i++)
        {
            for ($j = 0; $j < $N; $j++)
            {
                $c = 0;

                // Counting all neighbouring 1s

                if ($i > 0 && $arr[$i - 1][$j] == 1)
                    $c++;
                if ($j > 0 && $arr[$i][$j - 1] == 1)
                    $c++;
                if ($i > 0 && $j > 0 && $arr[$i - 1][$j - 1] == 1)
                    $c++;
                if ($i < $N - 1 && $arr[$i + 1][$j] == 1)
                    $c++;
                if ($j < $N - 1 && $arr[$i][$j + 1] == 1)
                    $c++;
                if ($i < $N - 1 && $j < $N - 1 &&
                    $arr[$i + 1][$j + 1] == 1)
                    $c++;
                if ($i < $N - 1 && $j > 0 && $arr[$i + 1][$j - 1] == 1)
                    $c++;
                if ($i > 0 && $j < $N - 1 && $arr[$i - 1][$j + 1] == 1)
                    $c++;

                // Comparing the number of
                // neighbouring 1s with
                // given ranges
                if ($arr[$i][$j] == 1)
                {
                    if ($c >= $range1a && $c <= $range1b)
                        $b[$i][$j] = 1;
                    else
                        $b[$i][$j] = 0;
                }
                if ($arr[$i][$j] == 0) {
                    if ($c >= $range0a && $c <= $range0b)
                        $b[$i][$j] = 1;
                    else
                        $b[$i][$j] = 0;
                }
            }
        }

        // Copying changes to
        // the main matrix
        for ($k = 0; $k < $N; $k++)
            for ($m = 0; $m < $N; $m++)
                $arr[$k][$m] = $b[$k][$m];
    }
    return $b;
}

// Driver code
$N = 4;
$arr= array(array(0, 0, 0, 0),
        array(0, 1, 1, 0),
        array(0, 0, 1, 0),
        array(0, 1, 0, 1));
$range1a = 2; $range1b = 2;
$range0a = 2; $range0b = 3;
$K = 3; $b = array(array(0));

// Function call to calculate
// the resultant matrix
// after 'K' iterations.
$b1 = predictMatrix($arr, $range1a, $range1b,
            $range0a, $range0b, $K, $b);

// Printing Result
for ($i = 0; $i < $N; $i++)
{
    echo "\n";
    for ($j = 0; $j < $N; $j++)
        echo $b1[$i][$j] . " ";
}

// This code is contributed by Akanksha Rai
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Dimension of Array
let N  = 4 ;

function predictMatrix(arr,range1a,range1b,range0a,range0b,K,b)
{
      // Count of 1s
    let c = 0;

    while (K != 0) {
        K--;
        for (let i = 0; i < N; i++) {
            for (let j = 0; j < N; j++) {
                c = 0;

                // Counting all neighbouring 1s

                if (i > 0 && arr[i - 1][j] == 1)
                    c++;
                if (j > 0 && arr[i][j - 1] == 1)
                    c++;
                if (i > 0 && j > 0
                    && arr[i - 1][j - 1] == 1)
                    c++;
                if (i < N - 1 && arr[i + 1][j] == 1)
                    c++;
                if (j < N - 1 && arr[i][j + 1] == 1)
                    c++;
                if (i < N - 1 && j < N - 1
                    && arr[i + 1][j + 1] == 1)
                    c++;
                if (i < N - 1 && j > 0
                    && arr[i + 1][j - 1] == 1)
                    c++;
                if (i > 0 && j < N - 1
                    && arr[i - 1][j + 1] == 1)
                    c++;

                // Comparing the number of
                // neighbouring 1s with
                // given ranges
                if (arr[i][j] == 1) {
                    if (c >= range1a && c <= range1b)
                        b[i][j] = 1;
                    else
                        b[i][j] = 0;
                }
                if (arr[i][j] == 0) {
                    if (c >= range0a && c <= range0b)
                        b[i][j] = 1;
                    else
                        b[i][j] = 0;
                }
            }
        }

        // Copying changes to
        // the main matrix
        for (let k = 0; k < N; k++)
            for (let m = 0; m < N; m++)
                arr[k][m] = b[k][m];
    }
}

    // Driver code
    let arr = [[0, 0, 0, 0],
           [0, 1, 1, 0],
           [0, 0, 1, 0],
           [0, 1, 0, 1]];

    let range1a = 2, range1b = 2;
    let range0a = 2, range0b = 3;
    let K = 3;
    let b = new Array(N) ;
    for(let i=0;i<N;i++)
    {
        b[i]=new Array(N);
        for(let j=0;j<N;j++)
        {
            b[i][j]=0;
        }
    }

    // Function call to calculate
    // the resultant matrix
    // after 'K' iterations.
    predictMatrix(arr, range1a, range1b,
                  range0a, range0b, K, b);

    // Printing Result
    for (let i = 0; i < N; i++) {
        document.write("<br>");
        for (let j = 0; j < N; j++)
            document.write(b[i][j]+ " ");
    }

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
0 1 0 0 
0 1 0 0 
1 1 1 0 
0 0 1 0
```