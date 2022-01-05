# 按交替的升序和降序对矩阵进行行排序

> 原文:[https://www . geesforgeks . org/sort-matrix-in-alternative-升序-降序-rowwise/](https://www.geeksforgeeks.org/sort-matrix-in-alternating-ascending-and-descending-order-rowwise/)

给定一个**N×N**矩阵，我们的任务是交替按升序和降序打印矩阵的行。
**例:**

> **输入:**
> 5 7 3 4
> 9 5 8 2
> 6 3 8 1
> 5 8 9 3
> T7】输出:
> 3 4 5 7
> 9 8 5 2
> 1 3 6 8
> 9 8 5 3
> **说明:**
> 这里第一行按升序排序，第二行按降序排序，第三行按升序排序，以此类推。
> **输入:**
> 7 3 4
> 3 8 2
> 3 6 1
> **输出:**
> 3 4 7
> 8 3 2
> 1 3 6
> **说明:**
> 这里第一行按升序排序，第二行按降序排序，第三行按升序排序。

**解决方法**
为了解决上面提到的问题，我们迭代 0 到 N，检查第**行是偶数还是奇数**，如果是偶数，那么我们按升序对该行进行排序，否则按降序对第 I 行进行排序。N 次迭代后返回矩阵。
以下是上述方法的实施:

## C++

```
// C++ implementation to print row of
// matrix in ascending or descending
// order alternatively

#include <stdio.h>
#define N 4

void func(int a[][N])
{

    // Iterate matrix rowwise
    for (int i = 0; i < N; i++) {

        // Sort even rows in ascending order
        if (i % 2 == 0) {
            for (int j = 0; j < N; j++) {
                for (int k = j + 1; k < N; ++k) {

                    // compare adjacent elements
                    if (a[i][j] > a[i][k]) {

                        // swap adjacent element
                        int temp = a[i][j];
                        a[i][j] = a[i][k];
                        a[i][k] = temp;
                    }
                }
            }
        }

        // Sort even rows in descending order
        else {
            for (int j = 0; j < N; j++) {
                for (int k = j + 1; k < N; ++k) {

                    // compare adjacent elements
                    if (a[i][j] < a[i][k]) {

                        // swap adjacent element
                        int temp = a[i][j];
                        a[i][j] = a[i][k];
                        a[i][k] = temp;
                    }
                }
            }
        }
    }

    // Printing the final Output
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            printf("%d ", a[i][j]);
        }
        printf("\n");
    }
}

// Driver code
int main()
{

    int a[N][N] = {
        { 5, 7, 3, 4 },
        { 9, 5, 8, 2 },
        { 6, 3, 8, 1 },
        { 5, 8, 9, 3 }
    };

    func(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print row of
// matrix in ascending or descending
// order alternatively
class GFG{

static int N = 4;

static void func(int a[][])
{
    int i, j, k;

    // Iterate matrix rowwise
    for(i = 0; i < N; i++)
    {

       // Sort even rows in ascending order
       if (i % 2 == 0)
       {
           for(j = 0; j < N; j++)
           {
              for(k = j + 1; k < N; ++k)
              {

                 // Compare adjacent elements
                 if (a[i][j] > a[i][k])
                 {

                     // Swap adjacent element
                     int temp = a[i][j];
                     a[i][j] = a[i][k];
                     a[i][k] = temp;
                 }
              }
           }
       }

       // Sort even rows in descending order
       else
       {
           for(j = 0; j < N; j++)
           {
              for(k = j + 1; k < N; ++k)
              {

                 // Compare adjacent elements
                 if (a[i][j] < a[i][k])
                 {

                     // Swap adjacent element
                     int temp = a[i][j];
                     a[i][j] = a[i][k];
                     a[i][k] = temp;
                 }
              }
           }
       }
    }

    // Printing the final Output
    for(i = 0; i < N; i++)
    {
       for(j = 0; j < N; j++)
       {
          System.out.print(a[i][j] + " ");
       }
       System.out.print("\n");
    }
}

// Driver code
public static void main (String []args)
{

    int a[][] = { { 5, 7, 3, 4 },
                  { 9, 5, 8, 2 },
                  { 6, 3, 8, 1 },
                  { 5, 8, 9, 3 } };

    func(a);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to print row of
# matrix in ascending or descending
# order alternatively
N = 4

def func(a):

    # Iterate matrix rowwise
    for i in range(N):

        # Sort even rows in ascending order
        if i % 2 == 0:
            for j in range(N):
                for k in range(j + 1, N):

                    # Compare adjacent elements
                    if a[i][j] > a[i][k]:

                        # Swap adjacent element
                        temp = a[i][j]
                        a[i][j] = a[i][k]
                        a[i][k] = temp

        # Sort even rows in descending order
        else :
            for j in range(N):
                for k in range(j + 1, N):

                    # Compare adjacent elements
                    if a[i][j] < a[i][k]:

                        # Swap adjacent element
                        temp = a[i][j]
                        a[i][j] = a[i][k]
                        a[i][k] = temp

    # Printing the final output
    for i in range(N):
        for j in range(N):
            print(a[i][j], end = " ")
        print()

# Driver code
if __name__ == '__main__':

    a = [ [ 5, 7, 3, 4 ],
          [ 9, 5, 8, 2 ],
          [ 6, 3, 8, 1 ],
          [ 5, 8, 9, 3 ] ]

    func(a)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to print row of
// matrix in ascending or descending
// order alternatively
using System;
class GFG{

static int N = 4;

static void func(int[,]a)
{
    int i, j, k;

    // Iterate matrix rowwise
    for(i = 0; i < N; i++)
    {

       // Sort even rows in ascending order
       if (i % 2 == 0)
       {
           for(j = 0; j < N; j++)
           {
              for(k = j + 1; k < N; ++k)
              {

                 // Compare adjacent elements
                 if (a[i, j] > a[i, k])
                 {

                     // Swap adjacent element
                     int temp = a[i, j];
                     a[i, j] = a[i, k];
                     a[i, k] = temp;
                 }
              }
           }
       }

       // Sort even rows in descending order
       else
       {
           for(j = 0; j < N; j++)
           {
              for(k = j + 1; k < N; ++k)
              {

                 // Compare adjacent elements
                 if (a[i, j] < a[i, k])
                 {

                     // Swap adjacent element
                     int temp = a[i, j];
                     a[i, j] = a[i, k];
                     a[i, k] = temp;
                 }
              }
           }
       }
    }

    // Printing the readonly Output
    for(i = 0; i < N; i++)
    {
       for(j = 0; j < N; j++)
       {
          Console.Write(a[i, j] + " ");
       }
       Console.Write("\n");
    }
}

// Driver code
public static void Main(String []args)
{

    int[,]a = { { 5, 7, 3, 4 },
                { 9, 5, 8, 2 },
                { 6, 3, 8, 1 },
                { 5, 8, 9, 3 } };

    func(a);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to print row of
// matrix in ascending or descending
// order alternatively

let N = 4;

function func(a)
{

    // Iterate matrix rowwise
    for (let i = 0; i < N; i++) {

        // Sort even rows in ascending order
        if (i % 2 == 0) {
            for (let j = 0; j < N; j++) {
                for (let k = j + 1; k < N; ++k) {

                    // compare adjacent elements
                    if (a[i][j] > a[i][k]) {

                        // swap adjacent element
                        let temp = a[i][j];
                        a[i][j] = a[i][k];
                        a[i][k] = temp;
                    }
                }
            }
        }

        // Sort even rows in descending order
        else {
            for (let j = 0; j < N; j++) {
                for (let k = j + 1; k < N; ++k) {

                    // compare adjacent elements
                    if (a[i][j] < a[i][k]) {

                        // swap adjacent element
                        let temp = a[i][j];
                        a[i][j] = a[i][k];
                        a[i][k] = temp;
                    }
                }
            }
        }
    }

    // Printing the final Output
    for (let i = 0; i < N; i++) {
        for (let j = 0; j < N; j++) {
            document.write(" " + a[i][j]);
        }
        document.write("<br>");
    }
}

// Driver code

    let a = [
        [ 5, 7, 3, 4 ],
        [ 9, 5, 8, 2 ],
        [ 6, 3, 8, 1 ],
        [ 5, 8, 9, 3 ]
    ];

    func(a);

// This code is contributed by subham348.
</script>
```

**Output:** 

```
3 4 5 7 
9 8 5 2 
1 3 6 8 
9 8 5 3
```

**时间复杂度:** O(N <sup>3</sup> )

**辅助空间:** O(1)