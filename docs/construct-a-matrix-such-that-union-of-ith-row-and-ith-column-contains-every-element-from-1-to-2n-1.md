# 构建一个矩阵，使得第 I 行和第 I 列的并集包含从 1 到 2N-1 的每个元素

> 原文:[https://www . geesforgeks . org/construct-a-matrix-so-of-with-row-and-with-column-包含从-1 到-2n-1 的每个元素/](https://www.geeksforgeeks.org/construct-a-matrix-such-that-union-of-ith-row-and-ith-column-contains-every-element-from-1-to-2n-1/)

给定一个数字 **N** ，任务是构建一个 **N * N** 的**正方形矩阵**，其中某些 **i <sup>第</sup>T9】行中的元素与 **i <sup>第</sup>T13】列的并集包含范围【1，2*N-1】中的每个元素。如果不存在这样的矩阵，打印-1。
**注:**特定 N 可以有多个可能的解
**例:****** 

> **输入:** N = 6
> **输出:**
> 6 4 2 5 3 1
> 10 6 5 3 1 2
> 8 11 6 1 4 3
> 11 9 7 6 2 4
> 9 7 10 8 6 5
> 7 8 9 10 11 6
> **说明:**
> 以上矩阵为 6 * 6，其中每 i <sup>第</sup>行和每列包含来自 像:
> 第一行和第一列= {6，4，2，5，3，1} & {6，10，8，11，9，7} = {1，2，3，4，5，6，7，8，9，10，11}
> 第二行和第二列= {10，6，5，3，1，2} & {4，6，11，9，7，8} = {1，2，3，4，5，6，6 6、7、10、9} = {1、2、3、4、5、6、7、8、9、10、11}
> 第 4 行第 4 列= {11、9、7、6、2、4} & {5、3、1、6、8、10} = {1、2、3、4、5、6、7、8、9、10、11}
> 第 5 行第 5 列= {9、7、10、8、6、5} 11}
> 第 6 行第 6 列= {7、8、9、10、11、6} & {1、2、3、4、5、6} = {1、2、3、4、5、6、7、8、9、10、11}
> **输入:** N = 6
> **输出:** -1
> **解释:**
> 不可能有这样的矩阵 因此，答案是-1。

**进场:**
如果仔细观察，可以看到:

*   对于除 1 以外的任何奇数，都不可能生成方阵
*   生成偶数阶的方阵，思路是将矩阵对角线元素的**上半部分填充到 **1 到 N-1** 的范围内，将所有的**对角线元素填充到 N** 中，对角线元素的**下半部分**可以从 **N + 1 到 2N–1**填充。**

下面是这种方法的算法:

1.  除了 **N = 1** 以外，奇数阶的矩阵不能按照观察填充
2.  对于偶数阶的矩阵，
    *   首先，填充所有等于 n 的对角线元素。
    *   考虑对角平分的矩阵的两半，每一半可以填充 N-1 个元素。
    *   用**【1，N-1】**的元素填充上半部分，用**【N+1，2N-1】**的元素填充下半部分。
    *   很容易看出，第二行的最后一个元素总是 2。
    *   现在，最后一列中的连续元素相差 2。因此，对于从 1 到 N-1 的所有 I，广义形式可以给出为 **A[i]=[(N-2)+2i]%(N-1)+1**
    *   只需将 *N* 添加到下半部分的所有元素中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

int matrix[100][100];

// Function to find the square matrix
void printRequiredMatrix(int n)
{
    // For Matrix of order 1,
    // it will contain only 1
    if (n == 1) {
        cout << "1"
             << "\n";
    }

    // For Matrix of odd order,
    // it is not possible
    else if (n % 2 != 0) {
        cout << "-1"
             << "\n";
    }

    // For Matrix of even order
    else {
        // All diagonal elements of the
        // matrix can be N itself.
        for (int i = 0; i < n; i++) {
            matrix[i][i] = n;
        }
        int u = n - 1;

        // Assign values at desired
        // place in the matrix
        for (int i = 0; i < n - 1; i++) {

            matrix[i][u] = i + 1;

            for (int j = 1; j < n / 2; j++) {

                int a = (i + j) % (n - 1);
                int b = (i - j + n - 1) % (n - 1);
                if (a < b)
                    swap(a, b);
                matrix[b][a] = i + 1;
            }
        }

        // Loop to add N in the lower half
        // of the matrix such that it contains
        // elements from 1 to 2*N - 1
        for (int i = 0; i < n; i++)
            for (int j = 0; j < i; j++)
                matrix[i][j] = matrix[j][i] + n;

        // Loop to print the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                cout << matrix[i][j] << " ";
            cout << "\n";
        }
    }
    cout << "\n";
}

// Driver Code
int main()
{
    int n = 1;
    printRequiredMatrix(n);

    n = 3;
    printRequiredMatrix(n);

    n = 6;
    printRequiredMatrix(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    static int matrix[][] = new int[100][100];

    // Function to find the square matrix
    static void printRequiredMatrix(int n)
    {
        // For Matrix of order 1,
        // it will contain only 1
        if (n == 1) {
            System.out.println("1");
        }

        // For Matrix of odd order,
        // it is not possible
        else if (n % 2 != 0) {
            System.out.println("-1");
        }

        // For Matrix of even order
        else {
            // All diagonal elements of the
            // matrix can be N itself.
            for (int i = 0; i < n; i++) {
                matrix[i][i] = n;
            }
            int u = n - 1;

            // Assign values at desired
            // place in the matrix
            for (int i = 0; i < n - 1; i++) {

                matrix[i][u] = i + 1;

                for (int j = 1; j < n / 2; j++) {

                    int a = (i + j) % (n - 1);
                    int b = (i - j + n - 1) % (n - 1);
                    if (a < b) {
                        int temp = a;
                        a = b;
                        b = temp;
                    }
                    matrix[b][a] = i + 1;
                }
            }

            // Loop to add N in the lower half
            // of the matrix such that it contains
            // elements from 1 to 2*N - 1
            for (int i = 0; i < n; i++)
                for (int j = 0; j < i; j++)
                    matrix[i][j] = matrix[j][i] + n;

            // Loop to print the matrix
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++)
                    System.out.print(matrix[i][j] + " ");
                System.out.println() ;
            }
        }
    System.out.println();
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 1;
        printRequiredMatrix(n);

        n = 3;
        printRequiredMatrix(n);

        n = 6;
        printRequiredMatrix(n);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import numpy as np;

matrix = np.zeros((100,100));

# Function to find the square matrix
def printRequiredMatrix(n) :

    # For Matrix of order 1,
    # it will contain only 1
    if (n == 1) :
        print("1");

    # For Matrix of odd order,
    # it is not possible
    elif (n % 2 != 0) :
        print("-1");

    # For Matrix of even order
    else :
        # All diagonal elements of the
        # matrix can be N itself.
        for i in range(n) :
            matrix[i][i] = n;

        u = n - 1;

        # Assign values at desired
        # place in the matrix
        for i in range(n - 1) :

            matrix[i][u] = i + 1;

            for j in range(1, n//2) :

                a = (i + j) % (n - 1);
                b = (i - j + n - 1) % (n - 1);
                if (a < b) :
                    a,b = b,a

                matrix[b][a] = i + 1;

        # Loop to add N in the lower half
        # of the matrix such that it contains
        # elements from 1 to 2*N - 1
        for i in range(n) :
            for j in range(i) :
                matrix[i][j] = matrix[j][i] + n;

        # Loop to print the matrix
        for i in range(n) :
            for j in range(n) :
                print(matrix[i][j] ,end=" ");
            print();

    print()

# Driver Code
if __name__ == "__main__" :

    n = 1;
    printRequiredMatrix(n);

    n = 3;
    printRequiredMatrix(n);

    n = 6;
    printRequiredMatrix(n);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    static int [,]matrix = new int[100, 100];

    // Function to find the square matrix
    static void printRequiredMatrix(int n)
    {
        // For Matrix of order 1,
        // it will contain only 1
        if (n == 1) {
            Console.WriteLine("1");
        }

        // For Matrix of odd order,
        // it is not possible
        else if (n % 2 != 0) {
            Console.WriteLine("-1");
        }

        // For Matrix of even order
        else
        {
            // All diagonal elements of the
            // matrix can be N itself.
            for (int i = 0; i < n; i++) {
                matrix[i, i] = n;
            }
            int u = n - 1;

            // Assign values at desired
            // place in the matrix
            for (int i = 0; i < n - 1; i++) {

                matrix[i, u] = i + 1;

                for (int j = 1; j < n / 2; j++) {

                    int a = (i + j) % (n - 1);
                    int b = (i - j + n - 1) % (n - 1);
                    if (a < b) {
                        int temp = a;
                        a = b;
                        b = temp;
                    }
                    matrix[b, a] = i + 1;
                }
            }

            // Loop to add N in the lower half
            // of the matrix such that it contains
            // elements from 1 to 2*N - 1
            for (int i = 0; i < n; i++)
                for (int j = 0; j < i; j++)
                    matrix[i, j] = matrix[j, i] + n;

            // Loop to print the matrix
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++)
                    Console.Write(matrix[i, j] + " ");
                Console.WriteLine() ;
            }
        }
    Console.WriteLine();
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int n = 1;
        printRequiredMatrix(n);

        n = 3;
        printRequiredMatrix(n);

        n = 6;
        printRequiredMatrix(n);
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let matrix = new Array();

for(let i = 0;  i < 100; i++){
    let temp = new Array();
    for(let j = 0; j < 100; j++){
        temp.push([])
    }
    matrix.push(temp)
}

// Function to find the square matrix
function printRequiredMatrix(n)
{
    // For Matrix of order 1,
    // it will contain only 1
    if (n == 1) {
        document.write("1" + "<br>");
    }

    // For Matrix of odd order,
    // it is not possible
    else if (n % 2 != 0) {
        document.write("-1" + "<br>");
    }

    // For Matrix of even order
    else {
        // All diagonal elements of the
        // matrix can be N itself.
        for (let i = 0; i < n; i++) {
            matrix[i][i] = n;
        }
        let u = n - 1;

        // Assign values at desired
        // place in the matrix
        for (let i = 0; i < n - 1; i++) {

            matrix[i][u] = i + 1;

            for (let j = 1; j < n / 2; j++) {

                let a = (i + j) % (n - 1);
                let b = (i - j + n - 1) % (n - 1);
                if (a < b){
                    let temp = a;
                    a = b;
                    b = temp
                }
                matrix[b][a] = i + 1;
            }
        }

        // Loop to add N in the lower half
        // of the matrix such that it contains
        // elements from 1 to 2*N - 1
        for (let i = 0; i < n; i++)
            for (let j = 0; j < i; j++)
                matrix[i][j] = matrix[j][i] + n;

        // Loop to print the matrix
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++)
                document.write(matrix[i][j] + " ");
            document.write("<br>");
        }
    }
    document.write("<br>");
}

// Driver Code

let n = 1;
printRequiredMatrix(n);

n = 3;
printRequiredMatrix(n);

n = 6;
printRequiredMatrix(n);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
1

-1

6 4 2 5 3 1 
10 6 5 3 1 2 
8 11 6 1 4 3 
11 9 7 6 2 4 
9 7 10 8 6 5 
7 8 9 10 11 6
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，有两个循环迭代整个 N*N 矩阵，在最坏的情况下需要 O(N <sup>2</sup> )个时间，因此时间复杂度为 **O(N <sup>2</sup> )** 。
*   **辅助空间复杂度:**和上面的方法一样，没有使用额外的空间，因此辅助空间复杂度为 **O(1)**