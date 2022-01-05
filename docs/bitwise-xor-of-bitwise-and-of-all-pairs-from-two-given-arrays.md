# 来自两个给定数组的所有对的按位“与”的按位“异或”

> 原文:[https://www . geeksforgeeks . org/两个给定数组的所有对的按位异或运算/](https://www.geeksforgeeks.org/bitwise-xor-of-bitwise-and-of-all-pairs-from-two-given-arrays/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr 1【】**和**arr 2【】**，任务是通过从**arr 1【】**和 **arr2】中选择一个元素来打印所有可能的对的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。**

**示例:**

> **输入:** arr1[] = {1，2，3}，arr2[] = {6，5}
> **输出:** 0
> **解释:**
> 对(arr1[0]，arr2[]) = 1 & 6 = 0。
> 对的按位“与”(arr1[0]，arr2[1]) = 1 & 5 = 1。
> 对的按位“与”(arr1[1]，arr2[0]) = 2 & 6 = 2。
> 对的按位“与”(arr1[1]，arr2[1]) = 2 & 5 = 0。
> 对的按位“与”(arr1[2]，arr2[0]) = 3 & 6 = 2。
> 对的按位“与”(arr1[2]，arr2[1]) = 3 & 5 = 1。
> 因此，获得的按位 AND 值的按位 xor = 0 ^ 1 ^ 2 ^ 0^ 2 ^ 1 = 0。
> 
> **输入:** arr1[] = {12}，arr 2[]= { 4 }
> T3】输出: 4

**天真方法:**最简单的方法是通过从**arr 1【】**中选择一个元素，从**arr 2【】**中选择另一个元素，然后计算结果对的所有**逐位“与”**的[逐位“异或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)来找到所有可能对的[。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
int findXORS(int arr1[], int arr2[], int N, int M)
{
    // Stores the result
    int res = 0;

    // Iterate over the range [0, N - 1]
    for (int i = 0; i < N; i++) {

        // Iterate over the range [0, M - 1]
        for (int j = 0; j < M; j++) {

            // Stores Bitwise AND of
            // the pair {arr1[i], arr2[j]}
            int temp = arr1[i] & arr2[j];

            // Update res
            res ^= temp;
        }
    }
    // Return the res
    return res;
}

// Driver Code
int main()
{
    // Input
    int arr1[] = { 1, 2, 3 };
    int arr2[] = { 6, 5 };
    int N = sizeof(arr1) / sizeof(arr1[0]);
    int M = sizeof(arr2) / sizeof(arr2[0]);

    cout << findXORS(arr1, arr2, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
static int findXORS(int arr1[], int arr2[],
                    int N, int M)
{

    // Stores the result
    int res = 0;

    // Iterate over the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Iterate over the range [0, M - 1]
        for(int j = 0; j < M; j++)
        {

            // Stores Bitwise AND of
            // the pair {arr1[i], arr2[j]}
            int temp = arr1[i] & arr2[j];

            // Update res
            res ^= temp;
        }
    }

    // Return the res
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int arr1[] = { 1, 2, 3 };
    int arr2[] = { 6, 5 };
    int N = arr1.length;
    int M = arr2.length;

    System.out.print(findXORS(arr1, arr2, N, M));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the Bitwise XOR
# of Bitwise AND of all pairs from
# the arrays arr1[] and arr2[]
def findXORS(arr1, arr2, N, M):

    # Stores the result
    res = 0

    # Iterate over the range [0, N - 1]
    for i in range(N):

        # Iterate over the range [0, M - 1]
        for j in range(M):
            # Stores Bitwise AND of
            # the pair {arr1[i], arr2[j]}
            temp = arr1[i] & arr2[j]

            # Update res
            res ^= temp
    # Return the res
    return res

# Driver Code
if __name__ == '__main__':

    # Input
    arr1 = [1, 2, 3]
    arr2 = [6, 5]
    N = len(arr1)
    M = len(arr2)
    print(findXORS(arr1, arr2, N, M))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the Bitwise XOR
    // of Bitwise AND of all pairs from
    // the arrays arr1[] and arr2[]
    static int findXORS(int[] arr1, int[] arr2, int N,
                        int M)
    {
        // Stores the result
        int res = 0;

        // Iterate over the range [0, N - 1]
        for (int i = 0; i < N; i++) {

            // Iterate over the range [0, M - 1]
            for (int j = 0; j < M; j++)
            {

                // Stores Bitwise AND of
                // the pair {arr1[i], arr2[j]}
                int temp = arr1[i] & arr2[j];

                // Update res
                res ^= temp;
            }
        }

        // Return the res
        return res;
    }

    // Driver Code
    public static void Main()
    {

        // Input
        int[] arr1 = { 1, 2, 3 };
        int[] arr2 = { 6, 5 };
        int N = arr1.Length;
        int M = arr2.Length;

        Console.Write(findXORS(arr1, arr2, N, M));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
function findXORS(arr1, arr2, N, M) {
    // Stores the result
    let res = 0;

    // Iterate over the range [0, N - 1]
    for (let i = 0; i < N; i++) {

        // Iterate over the range [0, M - 1]
        for (let j = 0; j < M; j++) {

            // Stores Bitwise AND of
            // the pair {arr1[i], arr2[j]}
            let temp = arr1[i] & arr2[j];

            // Update res
            res ^= temp;
        }
    }
    // Return the res
    return res;
}

// Driver Code

// Input
let arr1 = [1, 2, 3];
let arr2 = [6, 5];
let N = arr1.length;
let M = arr2.length;

document.write(findXORS(arr1, arr2, N, M));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
0
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   [逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[逐位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)运算具有加法和分配属性。
*   因此，将数组视为 arr1[] = {A，B}和 arr2[] = {X，Y}:
    *   (A 与 X)异或(A 与 Y)异或(B 与 X)异或(B 与 Y)
    *   (A 与(X 异或 Y))异或(B 与(X 异或 Y))
    *   (异或)与(异或)
*   因此，从以上步骤，任务简化为寻找 **arr1[]** 和 **arr2[]的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的[逐位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。**

按照以下步骤解决问题:

*   [求数组中每个数组元素的按位异或](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/) arr1【】并将其存储在一个变量中，比如 **XORS1。**
*   [求一个数组中每个数组元素的按位异或](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/) arr2[]，并将其存储在一个变量中，比如 **XORS2** 。
*   最后，将结果打印为 **XORS1 和 XORS2 的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
int findXORS(int arr1[], int arr2[],
             int N, int M)
{
    // Stores XOR of array arr1[]
    int XORS1 = 0;

    // Stores XOR of array arr2[]
    int XORS2 = 0;

    // Traverse the array arr1[]
    for (int i = 0; i < N; i++) {
        XORS1 ^= arr1[i];
    }

    // Traverse the array arr2[]
    for (int i = 0; i < M; i++) {
        XORS2 ^= arr2[i];
    }

    // Return the result
    return XORS1 and XORS2;
}

// Driver Code
int main()
{
    // Input
    int arr1[] = { 1, 2, 3 };
    int arr2[] = { 6, 5 };
    int N = sizeof(arr1) / sizeof(arr1[0]);
    int M = sizeof(arr2) / sizeof(arr2[0]);

    cout << findXORS(arr1, arr2, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
static int findXORS(int arr1[], int arr2[],
                    int N, int M)
{

    // Stores XOR of array arr1[]
    int XORS1 = 0;

    // Stores XOR of array arr2[]
    int XORS2 = 0;

    // Traverse the array arr1[]
    for(int i = 0; i < N; i++)
    {
        XORS1 ^= arr1[i];
    }

    // Traverse the array arr2[]
    for(int i = 0; i < M; i++)
    {
        XORS2 ^= arr2[i];
    }

    // Return the result
    return (XORS1 & XORS2);
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int arr1[] = { 1, 2, 3 };
    int arr2[] = { 6, 5 };
    int N = arr1.length;
    int M = arr2.length;

    System.out.println(findXORS(arr1, arr2, N, M));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Bitwise XOR
# of Bitwise AND of all pairs from
# the arrays arr1[] and arr2[]
def findXORS(arr1, arr2, N, M):

    # Stores XOR of array arr1[]
    XORS1 = 0

    # Stores XOR of array arr2[]
    XORS2 = 0

    # Traverse the array arr1[]
    for i in range(N):
        XORS1 ^= arr1[i]

    # Traverse the array arr2[]
    for i in range(M):
        XORS2 ^= arr2[i]

    # Return the result
    return XORS1 and XORS2

# Driver Code
if __name__ == '__main__':

    # Input
    arr1 = [ 1, 2, 3 ]
    arr2 = [ 6, 5 ]
    N = len(arr1)
    M = len(arr2)

    print(findXORS(arr1, arr2, N, M))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
static int findXORS(int []arr1, int []arr2,
                    int N, int M)
{

    // Stores XOR of array arr1[]
    int XORS1 = 0;

    // Stores XOR of array arr2[]
    int XORS2 = 0;

    // Traverse the array arr1[]
    for(int i = 0; i < N; i++)
    {
        XORS1 ^= arr1[i];
    }

    // Traverse the array arr2[]
    for(int i = 0; i < M; i++)
    {
        XORS2 ^= arr2[i];
    }

    // Return the result
    return (XORS1 & XORS2);
}

// Driver Code
public static void Main(String[] args)
{

    // Input
    int []arr1 = { 1, 2, 3 };
    int []arr2 = { 6, 5 };
    int N = arr1.Length;
    int M = arr2.Length;

    Console.WriteLine(findXORS(arr1, arr2, N, M));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the Bitwise XOR
// of Bitwise AND of all pairs from
// the arrays arr1[] and arr2[]
function findXORS(arr1, arr2, N, M)
{
    // Stores XOR of array arr1[]
    let XORS1 = 0;

    // Stores XOR of array arr2[]
    let XORS2 = 0;

    // Traverse the array arr1[]
    for (let i = 0; i < N; i++) {
        XORS1 ^= arr1[i];
    }

    // Traverse the array arr2[]
    for (let i = 0; i < M; i++) {
        XORS2 ^= arr2[i];
    }

    // Return the result
    return XORS1 && XORS2;
}

// Driver Code

    // Input
    let arr1 = [ 1, 2, 3 ];
    let arr2 = [ 6, 5 ];
    let N = arr1.length;
    let M = arr2.length;

    document.write(findXORS(arr1, arr2, N, M));

       // This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
0
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*