# 检查矩阵是否为反向双调和

> 原文:[https://www . geesforgeks . org/check-if-a-matrix-is-reverse-bitonic-or-not/](https://www.geeksforgeeks.org/check-if-a-matrix-is-reverse-bitonic-or-not/)

给定一个矩阵 **m[][]** ，任务是检查给定的矩阵是否为[反向双音素](https://www.geeksforgeeks.org/count-of-all-possible-reverse-bitonic-subarrays/)。如果给定的矩阵是**反向双声道，**则打印*是*。否则，打印*否*。

> 如果给定矩阵的所有行和列都具有以下顺序之一的元素:
> 
> *   严格递增
> *   严格递减
> *   严格减少，然后严格增加
> 
> 那么给定的矩阵称为逆双调和矩阵

**示例**:

> **输入:** m[][] = {{2，3，4}，{1，2，3}，{4，5，6} }
> **输出:**是
> **说明:**
> 给定矩阵的所有行形成递增序列。
> 给定矩阵{2，1，4}、{3，2，5}、{4，3，6}的所有列形成先递减后递增的序列。
> 因此，矩阵为反向双离子。
> **输入:** m[][] = {{1，2，3}，{4，5，6}，{2，5，4}}
> **输出:**否
> **说明:**
> 由于列{1，4，2}不满足三个条件中的任何一个，因此给定的矩阵不是 Reverse Bitonic。

**接近** :
按照以下步骤解决问题:

*   逐个检查矩阵每行的元素，看是否形成 [【逆比通】](https://www.geeksforgeeks.org/count-of-all-possible-reverse-bitonic-subarrays/) 序列。如果发现任何一行不是**反向双位**，打印编号
*   同样，逐个检查每一列的元素，看其是否形成[反向双音素](https://www.geeksforgeeks.org/count-of-all-possible-reverse-bitonic-subarrays/)序列。如果发现任何一行不是**反向双字符**，打印编号
*   如果发现所有的行和列都是**反向双音素**，则打印*是。*

下面是上述方法的实现:

## C++

```
// C++ Program to check if a
// matrix is Reverse Bitonic or not
#include <bits/stdc++.h>
using namespace std;

const int N = 3, M = 3;

// Function to check if an
// array is Reverse Bitonic or not
bool checkReverseBitonic(int arr[], int n)
{
    int i, j, f = 0;

    // Check for decreasing sequence
    for (i = 1; i < n; i++) {
        if (arr[i] < arr[i - 1])
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

    // Check for increasing sequence
    for (j = i + 1; j < n; j++) {
        if (arr[j] > arr[j - 1])
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
        if (!checkReverseBitonic(arr[i], M)) {
            cout << "No" << endl;
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

        if (!checkReverseBitonic(temp, N)) {
            cout << "No" << endl;
            return;
        }
    }

    cout << "Yes";
}

// Driver Code
int main()
{
    int m[N][M] = { { 2, 3, 4 },
                    { 1, 2, 3 },
                    { 4, 5, 6 } };

    check(m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a
// matrix is Reverse Bitonic or not
import java.util.*;
class GFG{

static int N = 3, M = 3;

// Function to check if an
// array is Reverse Bitonic or not
static boolean checkReverseBitonic(int arr[], int n)
{
    int i, j, f = 0;

    // Check for decreasing sequence
    for (i = 1; i < n; i++)
    {
        if (arr[i] < arr[i - 1])
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

    // Check for increasing sequence
    for (j = i + 1; j < n; j++)
    {
        if (arr[j] > arr[j - 1])
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
    for (int i = 0; i < N; i++)
    {
        if (!checkReverseBitonic(arr[i], M))
        {
            System.out.print("No" + "\n");
            return;
        }
    }

    // Check column wise
    for (int i = 0; i < N; i++)
    {
        // Generate an array
        // consisting of elements
        // of the current column
        int temp[] = new int[N];

        for (int j = 0; j < N; j++)
        {
            temp[j] = arr[j][i];
        }

        if (!checkReverseBitonic(temp, N))
        {
            System.out.print("No" + "\n");
            return;
        }
    }
    System.out.print("Yes");
}

// Driver Code
public static void main(String[] args)
{
    int m[][] = { { 2, 3, 4 },
                  { 1, 2, 3 },
                  { 4, 5, 6 } };

    check(m);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if a
# matrix is Reverse Bitonic or not
N = 3
M = 3

# Function to check if an
# array is Reverse Bitonic or not
def checkReverseBitonic(arr, n):

    f = 0

    # Check for decreasing sequence
    for i in range(1, n):
        if (arr[i] < arr[i - 1]):
            continue

        if (arr[i] == arr[i - 1]):
            return False

        else:
            f = 1
            break

    if (i == n):
        return True

    # Check for increasing sequence
    for j in range(i + 1, n):
        if (arr[j] > arr[j - 1]):
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

    # Check row-wise
    for i in range (N):
        if (not checkReverseBitonic(arr[i], M)):
            print("No")
            return

    # Check column wise
    for i in range(N):

        # Generate an array
        # consisting of elements
        # of the current column
        temp = [0] * N

        for j in range(N):
            temp[j] = arr[j][i]

        if (not checkReverseBitonic(temp, N)):
            print("No")
            return

    print("Yes")

# Driver Code
if __name__ == "__main__":

    m = [ [ 2, 3, 4 ],
          [ 1, 2, 3 ],
          [ 4, 5, 6 ] ]

    check(m)

# This code is contributed by chitranayal
```

## C#

```
// C# Program to check if a
// matrix is Reverse Bitonic or not
using System;
class GFG{

static int N = 3, M = 3;

// Function to check if an
// array is Reverse Bitonic or not
static bool checkReverseBitonic(int []arr, int n)
{
    int i, j, f = 0;

    // Check for decreasing sequence
    for (i = 1; i < n; i++)
    {
        if (arr[i] < arr[i - 1])
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

    // Check for increasing sequence
    for (j = i + 1; j < n; j++)
    {
        if (arr[j] > arr[j - 1])
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
    // Check row-wise
    for (int i = 0; i < N; i++)
    {
        if (!checkReverseBitonic(GetRow(arr, i), M))
        {
            Console.Write("No" + "\n");
            return;
        }
    }

    // Check column wise
    for (int i = 0; i < N; i++)
    {
        // Generate an array
        // consisting of elements
        // of the current column
        int []temp = new int[N];

        for (int j = 0; j < N; j++)
        {
            temp[j] = arr[j,i];
        }

        if (!checkReverseBitonic(temp, N))
        {
            Console.Write("No" + "\n");
            return;
        }
    }
    Console.Write("Yes");
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
    int [,]m = {{ 2, 3, 4 },
                { 1, 2, 3 },
                { 4, 5, 6 }};

    check(m);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Java script Program to check if a
// matrix is Reverse Bitonic or not

let N = 3, M = 3;

// Function to check if an
// array is Reverse Bitonic or not
function checkReverseBitonic(arr,n)
{
    let i, j, f = 0;

    // Check for decreasing sequence
    for (i = 1; i < n; i++)
    {
        if (arr[i] < arr[i - 1])
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

    // Check for increasing sequence
    for (j = i + 1; j < n; j++)
    {
        if (arr[j] > arr[j - 1])
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
    for (let i = 0; i < N; i++)
    {
        if (!checkReverseBitonic(arr[i], M))
        {
            document.write("No" + "<br>");
            return;
        }
    }

    // Check column wise
    for (let i = 0; i < N; i++)
    {
        // Generate an array
        // consisting of elements
        // of the current column
        let temp= [N];

        for (let j = 0; j < N; j++)
        {
            temp[j] = arr[j][i];
        }

        if (!checkReverseBitonic(temp, N))
        {
            document.write("No" + "<br>");
            return;
        }
    }
    document.write("Yes");
}

// Driver Code
let m = [[ 2, 3, 4 ],
                [ 1, 2, 3 ],
                [ 4, 5, 6 ]];

    check(m);

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N × M)*
***辅助空间:** O(N)*