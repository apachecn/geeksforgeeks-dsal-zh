# 检查矩阵是否是双调和的

> 原文:[https://www . geesforgeks . org/check-if-a-matrix-is-bitonic-or-not/](https://www.geeksforgeeks.org/check-if-a-matrix-is-bitonic-or-not/)

给定一个矩阵 **m[][]** ，任务是检查给定的矩阵是否为 [**比通**](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/) 。如果给定的矩阵是**比通**，则打印**是**。否则，打印**否**。

> 如果给定矩阵的所有行和列都具有以下顺序之一的元素:
> 
> *   严格递增
> *   严格递减
> *   严格增加，然后严格减少
> 
> 那么给定的矩阵被称为**双调和矩阵**

**示例:**

> **输入:** m[][] = {{1，2，3}，{4，5，6}，{2，3，4}}
> **输出:** YES
> **解释:**
> 给定矩阵的所有列{1，4，2}，{2，5，3}，{3，6，4}形成递增后递减的序列
> 给定矩阵的所有行都具有递增序列。
> 因此，矩阵是双离子的。
> **输入:** m[][] = {{1，2，3}，{4，5，6}，{2，5，4}}
> **输出:** NO
> **解释:**
> 由于列{2，5，5}不满足三个条件中的任何一个，所以给定的矩阵不是 Bitonic。

**方法:**
按照以下步骤解决问题:

*   逐个检查矩阵每行的元素，看它是否形成一个双音素序列。如果发现任何一行不是 Bitonic，打印**否**。
*   同样，逐一检查每一列的元素，看它是否形成一个双音素序列。如果发现任何一行不是 Bitonic，打印**否**。
*   如果发现所有的行和列都是**双音素**，则打印**是**

下面是上述方法的实现:

## C++

```
// C++ Program to check if a
// matrix is Bitonic or not
#include <bits/stdc++.h>
using namespace std;

const int N = 3, M = 3;

// Function to check if an
// array is Bitonic or not
bool checkBitonic(int arr[], int n)
{
    int i, j, f = 0;

    // Check for increasing sequence
    for (i = 1; i < n; i++) {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else {
            f = 1;
            break;
        }
    }

    if (i == n)
        return true;

    // Check for decreasing sequence
    for (j = i + 1; j < n; j++) {

        if (arr[j] < arr[j - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else {
            if (f == 1)
                return false;
        }
    }

    return true;
}

// Function to check whether given
// matrix is bitonic or not
void check(int arr[N][M])
{
    int f = 0;

    // Check row-wise
    for (int i = 0; i < N; i++) {
        if (!checkBitonic(arr[i], M)) {
            cout << "NO" << endl;
            return;
        }
    }

    // Check column wise
    for (int i = 0; i < N; i++) {

        // Generate an array
        // consisting of elements
        // of the current column
        int temp[N];
        for (int j = 0; j < N; j++) {
            temp[j] = arr[j][i];
        }
        if (!checkBitonic(temp, N)) {
            cout << "NO" << endl;
            return;
        }
    }

    cout << "YES";
}

// Driver Code
int main()
{
    int m[N][M] = { { 1, 2, 3 },
                    { 3, 4, 5 },
                    { 2, 6, 4 } };

    check(m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// matrix is Bitonic or not
class GFG{

final static int N = 3, M = 3;

// Function to check if an
// array is Bitonic or not
static boolean checkBitonic(int arr[], int n)
{
    int i, j, f = 0;

    // Check for increasing sequence
    for(i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else
        {
            f = 1;
            break;
        }
    }
    if (i == n)
        return true;

    // Check for decreasing sequence
    for(j = i + 1; j < n; j++)
    {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else
        {
            if (f == 1)
                return false;
        }
    }
    return true;
}

// Function to check whether given
// matrix is bitonic or not
static void check(int arr[][])
{
    int f = 0;

    // Check row-wise
    for(int i = 0; i < N; i++)
    {
        if (!checkBitonic(arr[i], M))
        {
            System.out.println("NO");
            return;
        }
    }

    // Check column wise
    for(int i = 0; i < N; i++)
    {

        // Generate an array
        // consisting of elements
        // of the current column
        int temp[] = new int[N];
        for(int j = 0; j < N; j++)
        {
            temp[j] = arr[j][i];
        }
        if (!checkBitonic(temp, N))
        {
            System.out.println("NO");
            return;
        }
    }
    System.out.println("YES");
}

// Driver Code
public static void main(String[] args)
{
    int m[][] = { { 1, 2, 3 },
                  { 3, 4, 5 },
                  { 2, 6, 4 } };

    check(m);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to check if a
# matrix is Bitonic or not
N = 3
M = 3

# Function to check if an
# array is Bitonic or not
def checkBitonic(arr, n):

    i, j, f = 0, 0, 0

    # Check for increasing sequence
    for i in range(1, n):
        if (arr[i] > arr[i - 1]):
            continue

        if (arr[i] == arr[i - 1]):
            return False

        else:
            f = 1
            break

    if (i == n):
        return True

    # Check for decreasing sequence
    for j in range(i + 1, n):
        if (arr[j] < arr[j - 1]):
            continue

        if (arr[i] == arr[i - 1]):
            return False

        else:
            if (f == 1):
                return False

    return True

# Function to check whether given
# matrix is bitonic or not
def check(arr):

    f = 0

    # Check row wise
    for i in range(N):
        if (not checkBitonic(arr[i], M)):
            print("NO")
            return

    # Check column wise
    i = 0
    for i in range(N):

        # Generate an array consisting
        # of elements of current column
        temp = [0] * N
        for j in range(N):
            temp[j] = arr[j][i]

        if (not checkBitonic(temp, N)):
            print("NO")
            return

    print("YES")

# Driver Code
if __name__ == '__main__':

    m = [ [ 1, 2, 3 ],
          [ 3, 4, 5 ],
          [ 2, 6, 4 ] ]

    check(m)

# This code is contributed by himanshu77
```

## C#

```
// C# program to check if a
// matrix is Bitonic or not
using System;
class GFG{

readonly static int N = 3, M = 3;

// Function to check if an
// array is Bitonic or not
static bool checkBitonic(int []arr, int n)
{
    int i, j, f = 0;

    // Check for increasing sequence
    for(i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else
        {
            f = 1;
            break;
        }
    }
    if (i == n)
        return true;

    // Check for decreasing sequence
    for(j = i + 1; j < n; j++)
    {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else
        {
            if (f == 1)
                return false;
        }
    }
    return true;
}

// Function to check whether given
// matrix is bitonic or not
static void check(int [,]arr)
{
    int f = 0;

    // Check row-wise
    for(int i = 0; i < N; i++)
    {
        if (!checkBitonic(GetRow(arr, i), M))
        {
            Console.WriteLine("NO");
            return;
        }
    }

    // Check column wise
    for(int i = 0; i < N; i++)
    {

        // Generate an array
        // consisting of elements
        // of the current column
        int []temp = new int[N];
        for(int j = 0; j < N; j++)
        {
            temp[j] = arr[j, i];
        }
        if (!checkBitonic(temp, N))
        {
            Console.WriteLine("NO");
            return;
        }
    }
    Console.WriteLine("YES");
}
public static int[] GetRow(int[,] matrix, int row)
  {
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for (var i = 0; i < rowLength; i++)
      rowVector[i] = matrix[row, i];

    return rowVector;
  }   
// Driver Code
public static void Main(String[] args)
{
    int [,]m = { { 1, 2, 3 },
                 { 3, 4, 5 },
                 { 2, 6, 4 } };

    check(m);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Java  Script program to check if a
// matrix is Bitonic or not
let N = 3, M = 3;

// Function to check if an
// array is Bitonic or not
function checkBitonic(arr,n)
{
    let i, j, f = 0;

    // Check for increasing sequence
    for(i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else
        {
            f = 1;
            break;
        }
    }
    if (i == n)
        return true;

    // Check for decreasing sequence
    for(j = i + 1; j < n; j++)
    {
        if (arr[j] < arr[j - 1])
            continue;

        if (arr[i] == arr[i - 1])
            return false;

        else
        {
            if (f == 1)
                return false;
        }
    }
    return true;
}

// Function to check whether given
// matrix is bitonic or not
function check(arr)
{
    let f = 0;

    // Check row-wise
    for(let i = 0; i < N; i++)
    {
        if (!checkBitonic(arr[i], M))
        {
            document.write("NO");
            return;
        }
    }

    // Check column wise
    for(let i = 0; i < N; i++)
    {

        // Generate an array
        // consisting of elements
        // of the current column
        let temp = [N];
        for(let j = 0; j < N; j++)
        {
            temp[j] = arr[j][i];
        }
        if (!checkBitonic(temp, N))
        {
            document.write("NO");
            return;
        }
    }
    document.write("YES");
}

// Driver Code

    let m = [[ 1, 2, 3 ],
                [3, 4, 5 ],
                [ 2, 6, 4 ]];

    check(m);

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N)*