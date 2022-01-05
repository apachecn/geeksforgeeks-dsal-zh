# 计算 N 次移动后数组中 1 的个数

> 原文:[https://www . geesforgeks . org/count-n 次移动后阵列中的 1 个数/](https://www.geeksforgeeks.org/count-number-of-1s-in-the-array-after-n-moves/)

给定一个大小为 N 的数组，其中所有元素最初都是 0(零)。任务是在数组上执行 N 次移动后，计算数组中 1 的个数，如下所述:
在每次移动中(从 1 到 N 开始)，移动数倍数位置的元素从 0 变为 1 或从 1 变为 0。
**移动 1** :改变 1、2、3、…
位置的元素**移动 2** :改变 2、4、6、…
位置的元素**移动 3** :改变 3、6、9、…
位置的元素执行 N 次移动后，计数数值为 1 的元素。

**注**:考虑数组是 1 索引的。

> **示例:**
> **输入** : N = 5，arr[] = {0，0，0，0}
> **输出** : 2
> **解释** :
> 移动 1: {1，1，1，1，1}
> 移动 2: {1，0，1，0，1}
> 移动 3: {1，0，0，0，1}
> 移动 4: {1，0，1，1
> 
> **输入** : N = 10，arr[] = {0，0，0，0，0，0，0，0，0}
> 输出 : 3

**简单方法:**迭代移动次数，每次移动遍历从移动次数到 N 的元素，检查位置是否是移动次数的倍数。如果是移动数的倍数，则改变该位置的元素，即如果是 0，则改变为 1，如果是 1，则改变为 0。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>

using namespace std;

// Function to count number of 1's in the
// array after performing N moves
int countOnes(int arr[], int N)
{
    for (int i = 1; i <= N; i++) {
        for (int j = i; j <= N; j++) {

            // If index is multiple of move number
            if (j % i == 0) {
                if (arr[j - 1] == 0)
                    arr[j - 1] = 1; // Convert 0 to 1
                else
                    arr[j - 1] = 0; // Convert 1 to 0
            }
        }
    }

    int count = 0;

    // Count number of 1's
    for (int i = 0; i < N; i++)
        if (arr[i] == 1)
            count++; // count number of 1's

    return count;
}

// Driver Code
int main()
{
    int N = 10; // Initialize array size

    // Initialize all elements to 0
    int arr[10] = { 0 };

    int ans = countOnes(arr, N);

    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{

    // Function to count number of 1's in the
    // array after performing N moves
    static int countOnes(int arr[], int N)
    {
        for (int i = 1; i <= N; i++)
        {
            for (int j = i; j <= N; j++)
            {

                // If index is multiple of move number
                if (j % i == 0)
                {
                    if (arr[j - 1] == 0)
                    {
                        arr[j - 1] = 1; // Convert 0 to 1
                    }
                    else
                    {
                        arr[j - 1] = 0; // Convert 1 to 0
                    }
                }
            }
        }

        int count = 0;

        // Count number of 1's
        for (int i = 0; i < N; i++)
        {
            if (arr[i] == 1)
            {
                count++; // count number of 1's
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 10; // Initialize array size

        // Initialize all elements to 0
        int arr[] = new int[10];

        int ans = countOnes(arr, N);

        System.out.println(ans);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count number of 1's in the
# array after performing N moves
def countOnes(arr, N):
    for i in range(1, N + 1, 1):
        for j in range(i, N + 1, 1):
            # If index is multiple of move number
            if (j % i == 0):
                if (arr[j - 1] == 0):
                    arr[j - 1] = 1 # Convert 0 to 1
                else:
                    arr[j - 1] = 0 # Convert 1 to 0

    count = 0

    # Count number of 1's
    for i in range(N):
        if (arr[i] == 1):
            count += 1 # count number of 1's

    return count

# Driver Code
if __name__ == '__main__':
    N = 10 # Initialize array size

    # Initialize all elements to 0
    arr = [0 for i in range(10)]

    ans = countOnes(arr, N)

    print(ans)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to count number of 1's in the
    // array after performing N moves
    static int countOnes(int []arr, int N)
    {
        for (int i = 1; i <= N; i++)
        {
            for (int j = i; j <= N; j++)
            {

                // If index is multiple of move number
                if (j % i == 0)
                {
                    if (arr[j - 1] == 0)
                    {
                        arr[j - 1] = 1; // Convert 0 to 1
                    }
                    else
                    {
                        arr[j - 1] = 0; // Convert 1 to 0
                    }
                }
            }
        }

        int count = 0;

        // Count number of 1's
        for (int i = 0; i < N; i++)
        {
            if (arr[i] == 1)
            {
                count++; // count number of 1's
            }
        }
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 10; // Initialize array size

        // Initialize all elements to 0
        int []arr = new int[10];

        int ans = countOnes(arr, N);

        Console.WriteLine(ans);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to count number of 1's in the
// array after performing N moves
function countOnes(arr, N)
{
    for(let i = 1; i <= N; i++)
    {
        for(let j = i; j <= N; j++)
        {

            // If index is multiple of move number
            if (j % i == 0)
            {
                if (arr[j - 1] == 0)

                    // Convert 0 to 1
                    arr[j - 1] = 1;
                else

                    // Convert 1 to 0
                    arr[j - 1] = 0;
            }
        }
    }

    let count = 0;

    // Count number of 1's
    for(let i = 0; i < N; i++)
        if (arr[i] == 1)

            // count number of 1's
            count++;

    return count;
}

// Driver Code

// Initialize array size
let N = 10;

// Initialize all elements to 0
let arr = new Uint8Array(10);

let ans = countOnes(arr, N);

document.write(ans);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sup>2</sup> )

**高效方法:**高效方法基于贪婪方法。它基本上是基于下面的模式。
当我们对 N = 1，2，3，4，5…进行此运算时，我们发现所需的答案是从 1 到 N(包括 1 和 N)的完美正方形的总数。
因此，答案=从 1 到 N 的完美正方形的总数

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>

using namespace std;

// Function to count number of perfect squares
int perfectSquares(int a, int b)
{
    // Counting number of perfect squares
    // between a and b
    return (floor(sqrt(b)) - ceil(sqrt(a)) + 1);
}

// Function to count number of 1s in
// array after N moves
int countOnes(int arr[], int n)
{
    return perfectSquares(1, n);
}

// Driver Code
int main()
{
    // Initialize array size
    int N = 10;

    // Initialize all elements to 0
    int arr[10] = { 0 };

    cout << countOnes(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

    // Function to count number of perfect squares
    static double perfectSquares(int a, int b)
    {
        // Counting number of perfect squares
        // between a and b
        return (Math.floor(Math.sqrt(b)) - Math.ceil(Math.sqrt(a)) + 1);
    }

    // Function to count number of 1s in
    // array after N moves
    static double countOnes(int arr[], int n)
    {
        return perfectSquares(1, n);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Initialize array size
        int N = 10;

        // Initialize all elements to 0
        int arr[] = { 0 };

        System.out.println(countOnes(arr, N));
    }
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import sqrt, ceil, floor;

# Function to count number of perfect squares
def perfectSquares(a, b) :

    # Counting number of perfect squares
    # between a and b
    return (floor(sqrt(b)) -
             ceil(sqrt(a)) + 1);

# Function to count number of 1s in
# array after N moves
def countOnes(arr, n) :

    return perfectSquares(1, n);

# Driver Code
if __name__ == "__main__" :

    # Initialize array size
    N = 10;

    # Initialize all elements to 0
    arr = [0] * 10;

    print(countOnes(arr, N));

# This code is contributed by Ankit Rai
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Function to count number of perfect squares
    static double perfectSquares(int a, int b)
    {
        // Counting number of perfect squares
        // between a and b
        return (Math.Floor(Math.Sqrt(b)) - Math.Ceiling(Math.Sqrt(a)) + 1);
    }

    // Function to count number of 1s in
    // array after N moves
    static double countOnes(int[] arr, int n)
    {
        return perfectSquares(1, n);
    }

    // Driver Code
    static public void Main()
    {
        // Initialize array size
        int N = 10;

        // Initialize all elements to 0
        int[] arr = { 0 };

        Console.WriteLine(countOnes(arr, N));
    }
}

// This code is contributed by JitSalal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count number of perfect squares
function perfectSquares($a, $b)
{
    // Counting number of perfect squares
    // between a and b
    return (floor(sqrt($b)) - ceil(sqrt($a)) + 1);
}

// Function to count number of 1s in
// array after N moves
function countOnes($arr, $n)
{
    return perfectSquares(1, $n);
}

// Driver Code
// Initialize array size
$N = 10;

// Initialize all elements to 0
$arr[10] = array(0);

echo countOnes($arr, $N);

// This code is contributed by jit_t

?>
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    // Function to count number of perfect squares
    function perfectSquares(a, b)
    {

        // Counting number of perfect squares
        // between a and b
        return (Math.floor(Math.sqrt(b)) - Math.ceil(Math.sqrt(a)) + 1);
    }

    // Function to count number of 1s in
    // array after N moves
    function countOnes(arr , n)
    {
        return perfectSquares(1, n);
    }

    // Driver Code

        // Initialize array size
        var N = 10;

        // Initialize all elements to 0
        var arr = [ 0 ];
        document.write(countOnes(arr, N));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(log(log N))