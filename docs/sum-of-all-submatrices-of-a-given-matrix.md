# 给定矩阵的所有子矩阵之和

> 原文:[https://www . geeksforgeeks . org/给定矩阵的所有子矩阵之和/](https://www.geeksforgeeks.org/sum-of-all-submatrices-of-a-given-matrix/)

给定一个 **NxN** **2-D** 矩阵，任务是找出所有子矩阵的和。

**示例:**

```
Input :  arr[] = {{1, 1},
                  {1, 1}};
Output : 16
Explanation: 
Number of sub-matrices with 1 elements = 4
Number of sub-matrices with 2 elements = 4
Number of sub-matrices with 3 elements = 0
Number of sub-matrices with 4 elements = 1

Since all the entries are 1, the sum becomes
sum = 1 * 4 + 2 * 4 + 3 * 0 + 4 * 1 = 16

Input : arr[] = {{1, 2, 3},
                 {4, 5, 6},
                 {7, 8, 9}}
Output : 500
```

**简单解法:**一个天真的解法是生成所有可能的子矩阵，并把它们全部求和。
这种方法的时间复杂度为 O(n <sup>6</sup> )。

**高效解:**对于矩阵的每个元素，让我们试着找出子矩阵的个数，元素将位于其中。
这可以在 O(1)时间内完成。让我们假设一个元素的索引在基于 0 的索引中是(X，Y)，那么这个元素的子矩阵(S <sub>x，y</sub> )的数量可以由公式 **S <sub>x，Y</sub>=(X+1)*(Y+1)*(N–X)*(N–Y)**给出。这个公式是有效的，因为我们只需要在矩阵上选择两个不同的位置，这将创建一个包围元素的子矩阵。因此，对于每个元素，“sum”可以更新为 **sum += (S <sub>x，y</sub> ) * Arr <sub>x，y</sub>T14】。**

下面是上述方法的实现:

这里我们需要在**反向查找技术**中尝试解决这个问题:

1)对于一个特定的元素，该元素将包含在哪些**可能的子矩阵中**。

2)当我们得到可能的子矩阵的数量时，然后**我们可以通过做(a[i]*子矩阵的总数，其中这将包括在内)来计算该特定元素的贡献，其中 a[i] =当前元素**

3)现在问题来了，如何找到特定元素的可能子矩阵的数量。

 [[1 2 3]

  [4 5 6]

  [7 8 9]]

让我们将当前元素视为 5，因此对于 5，有(X+1)*(Y+1)个选择，其中子矩阵起点的坐标可以位于(左上角)

类似地，将有(N-X)*(N-Y)个选择，其中该子矩阵的末端坐标可以位于(右下方)

**左上角的选择数= (X+1)*(Y+1)**

**右下方的选择数= (N-X)*(N-Y)**

要包含在子矩阵中的当前元素的选择总数将是:(X+1)*(Y+1) * (N-X)*(N-Y)

**可以包含在所有可能的子矩阵中的当前元素的贡献将是= arr[X][Y]*(X+1)*(Y+1)*(N-X)*(N-Y)**

其中 **X 和 Y 是子矩阵的索引。**

**时间复杂度:O(N^2)**

**空间复杂度:O(1)**

## C++

```
// C++ program to find the sum of all
// possible submatrices of a given Matrix

#include <iostream>
#define n 3
using namespace std;

// Function to find the sum of all
// possible submatrices of a given Matrix
int matrixSum(int arr[][n])
{
    // Variable to store
    // the required sum
    int sum = 0;

    // Nested loop to find the number
    // of submatrices, each number belongs to
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {

            // Number of ways to choose
            // from top-left elements
            int top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            int bottom_right = (n - i) * (n - j);
            sum += (top_left * bottom_right * arr[i][j]);
        }

    return sum;
}

// Driver Code
int main()
{
    int arr[][n] = { { 1, 1, 1 },
                     { 1, 1, 1 },
                     { 1, 1, 1 } };

    cout << matrixSum(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all
// possible submatrices of a given Matrix
class GFG
{

    static final int n = 3;

    // Function to find the sum of all
    // possible submatrices of a given Matrix
    static int matrixSum(int arr[][])
    {
        // Variable to store
        // the required sum
        int sum = 0;

        // Nested loop to find the number
        // of submatrices, each number belongs to
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                // Number of ways to choose
                // from top-left elements
                int top_left = (i + 1) * (j + 1);

                // Number of ways to choose
                // from bottom-right elements
                int bottom_right = (n - i) * (n - j);
                sum += (top_left * bottom_right * arr[i][j]);
            }
        }

        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[][] = {{1, 1, 1},
        {1, 1, 1},
        {1, 1, 1}};

        System.out.println(matrixSum(arr));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the sum of all
# possible submatrices of a given Matrix
n = 3

# Function to find the sum of all
# possible submatrices of a given Matrix
def matrixSum(arr) :

    # Variable to store the required sum
    sum = 0;

    # Nested loop to find the number of
    # submatrices, each number belongs to
    for i in range(n) :
        for j in range(n) :

            # Number of ways to choose
            # from top-left elements
            top_left = (i + 1) * (j + 1);

            # Number of ways to choose
            # from bottom-right elements
            bottom_right = (n - i) * (n - j);
            sum += (top_left * bottom_right *
                                  arr[i][j]);

    return sum;

# Driver Code
if __name__ == "__main__" :
    arr = [[ 1, 1, 1 ],
           [ 1, 1, 1 ],
           [ 1, 1, 1 ]];

    print(matrixSum(arr))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the sum of all
// possible submatrices of a given Matrix
using System;

class GFG
{
static int n = 3;

// Function to find the sum of all
// possible submatrices of a given Matrix
static int matrixSum(int [,]arr)
{
    // Variable to store the
    // required sum
    int sum = 0;

    // Nested loop to find the number of 
    // submatrices, each number belongs to
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // Number of ways to choose
            // from top-left elements
            int top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            int bottom_right = (n - i) * (n - j);
            sum += (top_left * bottom_right * arr[i, j]);
        }
    }

    return sum;
}

// Driver Code
public static void Main()
{
    int [,]arr = {{1, 1, 1},
    {1, 1, 1},
    {1, 1, 1}};

    Console.WriteLine(matrixSum(arr));
}
}

// This code contributed by vt_m..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all
// possible submatrices of a given Matrix

// Function to find the sum of all
// possible submatrices of a given Matrix
function matrixSum($arr)
{
    $n = 3;

    // Variable to store the required sum
    $sum = 0;

    // Nested loop to find the number
    // of submatrices, each number belongs to
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)
        {

            // Number of ways to choose
            // from top-left elements
            $top_left = ($i + 1) * ($j + 1);

            // Number of ways to choose
            // from bottom-right elements
            $bottom_right = ($n - $i) * ($n - $j);
            $sum += ($top_left * $bottom_right *
                                 $arr[$i][$j]);
        }

    return $sum;
}

// Driver Code
$arr = array(array(1, 1, 1),
             array(1, 1, 1),
             array(1, 1, 1));

echo matrixSum($arr);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the sum of all
// possible submatrices of a given Matrix

let n = 3;
// Function to find the sum of all
// possible submatrices of a given Matrix
function matrixSum(arr)
{
    // Variable to store
    // the required sum
    let sum = 0;

    // Nested loop to find the number
    // of submatrices, each number belongs to
    for (let i = 0; i < n; i++)
        for (let j = 0; j < n; j++) {

            // Number of ways to choose
            // from top-left elements
            let top_left = (i + 1) * (j + 1);

            // Number of ways to choose
            // from bottom-right elements
            let bottom_right = (n - i) * (n - j);
            sum += (top_left * bottom_right * arr[i][j]);
        }

    return sum;
}

// Driver Code
let arr = [[ 1, 1, 1 ],
                     [ 1, 1, 1 ],
                     [ 1, 1, 1 ]] ;

    document.write(matrixSum(arr));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
100
```