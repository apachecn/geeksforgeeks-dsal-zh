# N×N 矩阵的交替元素之和

> 原文:[https://www . geesforgeks . org/a-n-x-n-matrix 交替元素之和/](https://www.geeksforgeeks.org/sum-of-alternate-elements-of-a-n-x-n-matrix/)

给定一个 NxN 矩阵。任务是找出给定矩阵的交替元素的和。
例如，在 2×2 矩阵中，交替元素是{ A[0][0]，A[1，1] }和{ A[1][0]，A[0][1] }。
**例:**

```
Input: mat[][] = { { 1, 2},
                   { 3, 4} }
Output : Sum of alternate elements : 5, 5
Explanation: The alternate elements are {1, 4} 
and {2, 3} so their sum are 5, 5.

Input : mat[][] = { { 1, 2, 3 },
                    { 4, 5, 6 },
                    { 7, 8, 9 } }
Output : Sum of alternate elements :25, 20
```

这个想法是遍历矩阵，同时保留一个计数器。我们将在一个变量中添加计数器值为偶数的元素，在另一个变量中添加计数器值为奇数的元素，最后在矩阵的完全遍历中打印这两个和。
以下是上述方法的实现:

## C++

```
// C++ program to print sum of alternate
// elements of a N x N matrix
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of alternate
// elements of a matrix
void sumAlternate(int* arr, int n)
{
    int sum1 = 0, sum2 = 0;

    // check the alternate elements
    for (int i = 0; i < n * n; i++) {

        // count the elements at even places
        if (i % 2 == 0)
            sum1 += *(arr + i);

        else // count the elements at odd places
            sum2 += *(arr + i);
    }

    cout << "Sum of alternate elements : " << sum1
         << ", " << sum2 << endl;
}

// Driver code
int main()
{
    int mat[3][3] = { { 1, 2, 3 },
                      { 4, 5, 6 },
                      { 7, 8, 9 } };
    int n = 3;

    // find the sum of alternate elements
    sumAlternate(&mat[0][0], n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print sum of alternate
// elements of a N x N matrix

class GFG
{
        // Function to find the sum of alternate
        // elements of a matrix
        static void sumAlternate(int [][] mat, int n)
        {
            int sum1 = 0, sum2 = 0;
            int cnt=0;
            // check the alternate elements
            for (int i = 0; i < n; i++) {

                for(int j=0;j<n ;j++)
                {
                    if (cnt % 2 == 0)
                        sum1 += mat[i][j];

                    else // count the elements at odd places
                        sum2 += mat[i][j];

                   cnt++;
                }
            }

            System.out.println("Sum of alternate elements : " + sum1 + ", " + sum2);
        }

        // Driver code
        public static void main(String [] args)
        {
            int [][]mat = { { 1, 2, 3 },
                            { 4, 5, 6 },
                            { 7, 8, 9 } };
            int n = 3;

            // find the sum of alternate elements
            sumAlternate(mat, n);

        }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to print sum of
# alternate elements of a N x N matrix

# Function to find the sum of
# alternate elements of a matrix
def sumAlternate(arr, n):

    sum1 = 0
    sum2 = 0

    # check the alternate elements
    i = 0
    while i < n * n :

        # count the elements at
        # even places
        if (i % 2 == 0):
            sum1 += (arr + i)

        else: # count the elements
              # at odd places
            sum2 += (arr + i)

        i += 1

    print("Sum of alternate elements : " +
             str(sum1) + ", " + str(sum2))

# Driver code
if __name__ == "__main__":
    mat = [[ 1, 2, 3 ],
        [4, 5, 6 ],
        [7, 8, 9 ]]
    n = 3

    # find the sum of alternate elements
    sumAlternate(mat[0][0], n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print sum of alternate
// elements of a N x N matrix
using System;
class GFG
{
// Function to find the sum of
// alternate elements of a matrix
static void sumAlternate(int[,] mat,
                         int n)
{
    int sum1 = 0, sum2 = 0;
    int cnt = 0;

    // check the alternate elements
    for (int i = 0; i < n; i++)
    {

        for(int j = 0; j < n; j++)
        {
            if (cnt % 2 == 0)
                sum1 += mat[i, j];

            else // count the elements
                 // at odd places
                sum2 += mat[i, j];

        cnt++;
        }
    }

    Console.WriteLine("Sum of alternate elements : " +
                                  sum1 + ", " + sum2);
}

// Driver code
public static void Main()
{
    int[,] mat = { { 1, 2, 3 },
                    { 4, 5, 6 },
                    { 7, 8, 9 } };
    int n = 3;

    // find the sum of alternate elements
    sumAlternate(mat, n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
// Javascript program to print sum of alternate
// elements of a N x N matrix

// Function to find the sum of alternate
// elements of a matrix
function sumAlternate(arr, n)
{
    var sum1 = 0, sum2 = 0;
    var cnt = 0;

    // check the alternate elements
    for (var i = 0; i < n ; i++) {

        for (var j = 0; j < n ; j++) {
        // count the elements at even places
        if (cnt % 2 == 0)
            sum1 += arr[i][j];

        else // count the elements at odd places
            sum2 += arr[i][j];
        cnt++;
        }
    }

    document.write( "Sum of alternate elements : " + sum1
        + ", " + sum2 );
}

// Driver code
var mat = [ [ 1, 2, 3 ],
                [ 4, 5, 6 ],
                [ 7, 8, 9 ] ];
var n = 3;
// find the sum of alternate elements
sumAlternate(mat, n);

</script>
```

**Output:** 

```
Sum of alternate elements : 25, 20
```

**时间复杂度:** O(N <sup>2</sup> )