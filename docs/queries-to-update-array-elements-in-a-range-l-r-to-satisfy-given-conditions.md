# 更新范围[L，R]内的数组元素以满足给定条件的查询

> 原文:[https://www . geesforgeks . org/query-to-update-array-elements-in-range-l-r-to-conditions-给定条件/](https://www.geeksforgeeks.org/queries-to-update-array-elements-in-a-range-l-r-to-satisfy-given-conditions/)

给定一个由**N**T6【0】T7 s 和一个数组**Q【】【】**组成的[数组**arr【】**，每一行的形式为 **(L，R)** 。，每个查询的任务是更新范围**【L，R】**内的所有数组元素，使得**arr[I]= I–L+1**。](https://www.geeksforgeeks.org/array-data-structure/)

**示例:**

> **输入:** arr[] = { 0，0，0，0 }，Q[][] = { { 1，2 }，{ 0，1 } }
> **输出:** 1 3 2 0
> **解释:**T8】查询 1:更新 arr[1]= 1–1+1，arr[2]= 2–1+1 将 arr[]修改为{ 0，1，2，0 }
> 查询 2:更新 arr[0]= 0–0+1，arr[1]
> 
> **输入:** arr[] = { 0，0，0，0 }，Q[][] = { { 1，3 }，{ 0，1 } }
> **输出:** 1 3 2 3

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** 对于每个查询，[遍历给定范围内的所有数组元素](https://www.geeksforgeeks.org/iterating-arrays-java/)并更新**arr[I]+= I–L+1**。最后，打印数组元素。

***时间复杂度:** O(N * Q)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[差分阵列](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)的概念进行优化。按照以下步骤解决问题:

*   初始化两个数组 **arr1[]** 和 **arr2[]** ，并将所有元素初始化为 **0** 。
*   [遍历查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)， **Q[][]** 。对于类型为 **(L，R)** 的每个查询，更新 **arr1[L] += 1** 、 **arr1[R + 1] -= 1** 和**arr 2[R+1]-= R–L+1**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr1[]** ，存储 **arr1[]** 的前缀和，即 **arr1[i] += arr1[i -1]** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr2[]** 并更新**arr 2[I]+= arr 2[I–1]+arr 1[I]**。
*   最后打印数组， **arr2[]** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array
void printArray(int arr[], int N)
{
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Function to perform the query in range [L, R]
// such that arr[i] += i - L + 1
void modifyArray(int arr[], int N, int Q[][2],
                 int cntQuery)
{

    // Initialize array
    int arr1[N + 1] = { 0 };
    int arr2[N + 1] = { 0 };

    // Traverse the query array
    for (int i = 0; i < cntQuery; i++) {

        // Stores range in 1-based index
        int L = Q[i][0] + 1, R = Q[i][1] + 1;

        // Update arr1[L]
        arr1[L]++;

        // Update arr1[R + 1]
        arr1[R + 1]--;

        // Update arr2[R + 1]
        arr2[R + 1] -= R - L + 1;
    }

    // Calculate prefix sum
    for (int i = 1; i <= N; i++)
        arr1[i] += arr1[i - 1];

    // Traverse the array, arr2[]
    for (int i = 1; i <= N; i++)
        arr2[i] += arr2[i - 1] + arr1[i];

    // Copy arr2[] into arr[]
    for (int i = 1; i <= N; i++)
        arr[i - 1] = arr2[i];

    printArray(arr, N);
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 0, 0, 0, 0 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    int Q[][2] = { { 1, 3 }, { 0, 1 } };

    // Stores count of query
    int cntQuery
        = sizeof(Q) / sizeof(Q[0]);

    // Function Call
    modifyArray(arr, N, Q, cntQuery);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

    // Function to print the array
    static void printArray(int arr[], int N)
    {
        for (int i = 0; i < N; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }

    // Function to perform the query in range [L, R]
    // such that arr[i] += i - L + 1
    static void modifyArray(int arr[], int N, int Q[][],
                     int cntQuery)
    {

        // Initialize array
        int arr1[] = new int[N + 2];
        int arr2[] = new int[N + 2];

        // Traverse the query array
        for (int i = 0; i < cntQuery; i++)
        {

            // Stores range in 1-based index
            int L = Q[i][0] + 1, R = Q[i][1] + 1;

            // Update arr1[L]
            arr1[L]++;

            // Update arr1[R + 1]
            arr1[R + 1]--;

            // Update arr2[R + 1]
            arr2[R + 1] -= R - L + 1;
        }

        // Calculate prefix sum
        for (int i = 1; i <= N; i++)
            arr1[i] += arr1[i - 1];

        // Traverse the array, arr2[]
        for (int i = 1; i <= N; i++)
            arr2[i] += arr2[i - 1] + arr1[i];

        // Copy arr2[] into arr[]
        for (int i = 1; i <= N; i++)
            arr[i - 1] = arr2[i];   
        printArray(arr, N);
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Given array
        int arr[] = { 0, 0, 0, 0 };

        // Size of the array
        int N = arr.length;   
        int Q[][] = { { 1, 3 }, { 0, 1 } };

        // Stores count of query
        int cntQuery = Q.length;

        // Function Call
        modifyArray(arr, N, Q, cntQuery);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print array
def printArray(arr, N):
    print(*arr)

# Function to perform the query in range [L, R]
# such that arr[i] += i - L + 1
def modifyArray(arr, N, Q, cntQuery):

    # Initialize array
    arr1 = [0 for i in range(N + 2)]
    arr2 = [0 for i in range(N + 2)]

    # Traverse the query array
    for i in range(cntQuery):

        # Stores range in 1-based index
        L = Q[i][0] + 1
        R = Q[i][1] + 1
        # print(L,R)

        # Update arr1[L]
        arr1[L] += 1

        # Update arr1[R + 1]
        arr1[R + 1] -= 1

        # Update arr2[R + 1]
        arr2[R + 1] -= R - L + 1

    # Calculate prefix sum
    for i in range(1, N + 1):
        arr1[i] += arr1[i - 1]

    # Traverse the array, arr2[]
    for i in range(1, N + 1):
        arr2[i] += arr2[i - 1] + arr1[i]

    # Copy arr2[] into arr[]
    for i in range(1, N + 1):
        arr[i - 1] = arr2[i]
    printArray(arr, N)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [0, 0, 0, 0]

    # Size of the array
    N = len(arr)
    Q = [[ 1, 3 ], [ 0, 1 ]]

    # Stores count of query
    cntQuery = len(Q)

    # Function Call
    modifyArray(arr, N, Q, cntQuery)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to print the array
    static void printArray(int []arr, int N)
    {
        for (int i = 0; i < N; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }

    // Function to perform the query in range [L, R]
    // such that arr[i] += i - L + 1
    static void modifyArray(int []arr, int N, int[,] Q,
                     int cntQuery)
    {

        // Initialize array
        int []arr1 = new int[N + 2];
        int []arr2 = new int[N + 2];

        // Traverse the query array
        for (int i = 0; i < cntQuery; i++)
        {

            // Stores range in 1-based index
            int L = Q[i,0] + 1, R = Q[i,1] + 1;

            // Update arr1[L]
            arr1[L]++;

            // Update arr1[R + 1]
            arr1[R + 1]--;

            // Update arr2[R + 1]
            arr2[R + 1] -= R - L + 1;
        }

        // Calculate prefix sum
        for (int i = 1; i <= N; i++)
            arr1[i] += arr1[i - 1];

        // Traverse the array, arr2[]
        for (int i = 1; i <= N; i++)
            arr2[i] += arr2[i - 1] + arr1[i];

        // Copy arr2[] into arr[]
        for (int i = 1; i <= N; i++)
            arr[i - 1] = arr2[i];   
        printArray(arr, N);
    }

    // Driver Code
    public static void Main()
    {

        // Given array
        int []arr = { 0, 0, 0, 0 };

        // Size of the array
        int N = arr.Length;   
        int [,]Q = { { 1, 3 }, { 0, 1 } };

        // Stores count of query
        int cntQuery = 2;

        // Function Call
        modifyArray(arr, N, Q, cntQuery);
    }
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to print the array
function printArray(arr, N)
{
    for(let i = 0; i < N; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Function to perform the query in
// range [L, R] such that
// arr[i] += i - L + 1
function modifyArray(arr, N, Q, cntQuery)
{

    // Initialize array
    let arr1 = new Array(N + 2).fill(0);
    let arr2 = new Array(N + 2).fill(0);

    // Traverse the query array
    for(let i = 0; i < cntQuery; i++)
    {

        // Stores range in 1-based index
        let L = Q[i][0] + 1, R = Q[i][1] + 1;

        // Update arr1[L]
        arr1[L]++;

        // Update arr1[R + 1]
        arr1[R + 1]--;

        // Update arr2[R + 1]
        arr2[R + 1] -= R - L + 1;
    }

    // Calculate prefix sum
    for(let i = 1; i <= N; i++)
        arr1[i] += arr1[i - 1];

    // Traverse the array, arr2[]
    for(let i = 1; i <= N; i++)
        arr2[i] += arr2[i - 1] + arr1[i];

    // Copy arr2[] into arr[]
    for(let i = 1; i <= N; i++)
        arr[i - 1] = arr2[i];  

    prletArray(arr, N);
}

// Driver Code

// Given array
let arr = [ 0, 0, 0, 0 ];

// Size of the array
let N = arr.length;  
let Q = [ [ 1, 3 ], [ 0, 1 ] ];

// Stores count of query
let cntQuery = Q.length;

// Function Call
modifyArray(arr, N, Q, cntQuery);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
1 3 2 3
```

***时间复杂度:** O(N+Q)*
***辅助空间:** O(N)*