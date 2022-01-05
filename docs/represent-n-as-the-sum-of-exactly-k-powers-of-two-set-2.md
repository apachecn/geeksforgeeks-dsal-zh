# 将 n 表示为 2 的 k 次幂之和|集合 2

> 原文:[https://www . geeksforgeeks . org/representative-n-as-k 的二次幂之和-set-2/](https://www.geeksforgeeks.org/represent-n-as-the-sum-of-exactly-k-powers-of-two-set-2/)

给定两个整数 **n** 和 **k** ，任务是找出是否有可能将 **n** 表示为 **2** 的精确 **k** 次幂之和。如果可能，则打印 **k** 正整数，使其为 **2** 的幂，且其和正好等于 **n** ，否则打印**不可能的**。
**例:**

> **输入:** n = 9，k = 4
> **输出:** 1 2 2 4
> 1，2 和 4 都是 2 和 1 + 2 + 2 + 4 = 9 的幂。
> **输入:** n = 3，k = 7
> **输出:**不可能
> 不可能，因为 3 不能表示为 7 个数字的和，7 是 2 的幂。

我们已经在[中讨论了解决这个问题的一种方法，即求 k 个 2 的幂且和为 N 的数](https://www.geeksforgeeks.org/find-k-numbers-which-are-powers-of-2-and-have-sum-n/)。在这篇文章中，一种不同的方法正在被讨论。
**进场:**

*   创建一个大小为 **k** 的数组 **arr[]** ，所有元素初始化为 **1** ，并创建一个变量 **sum = k** 。
*   现在从 **arr[]** 的最后一个元素开始
    *   如果 **sum + arr[i] ≤ n** 则更新 **sum = sum + arr[i]** 和 **arr[i] = arr[i] * 2** 。
    *   否则跳过当前元素。
*   如果**和= n** ，则**arr【】**的内容是必需的元素。
*   否则不可能准确地将 **2** 的 **k** 次方表示为 **n** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to print k numbers which are powers of two
// and whose sum is equal to n
void FindAllElements(int n, int k)
{
    // Initialising the sum with k
    int sum = k;

    // Initialising an array A with k elements
    // and filling all elements with 1
    int A[k];
    fill(A, A + k, 1);

    for (int i = k - 1; i >= 0; --i) {

        // Iterating A[] from k-1 to 0
        while (sum + A[i] <= n) {

            // Update sum and A[i]
            // till sum + A[i] is less than equal to n
            sum += A[i];
            A[i] *= 2;
        }
    }

    // Impossible to find the combination
    if (sum != n) {
        cout << "Impossible";
    }

    // Possible solution is stored in A[]
    else {
        for (int i = 0; i < k; ++i)
            cout << A[i] << ' ';
    }
}

// Driver code
int main()
{
    int n = 12;
    int k = 6;

    FindAllElements(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

public class GfG {

    // Function to print k numbers which are powers of two
    // and whose sum is equal to n
    public static void FindAllElements(int n, int k)
    {
        // Initialising the sum with k
        int sum = k;

        // Initialising an array A with k elements
        // and filling all elements with 1
        int[] A = new int[k];
        Arrays.fill(A, 0, k, 1);

        for (int i = k - 1; i >= 0; --i) {

            // Iterating A[] from k-1 to 0
            while (sum + A[i] <= n) {

                // Update sum and A[i]
                // till sum + A[i] is less than equal to n
                sum += A[i];
                A[i] *= 2;
            }
        }

        // Impossible to find the combination
        if (sum != n) {
            System.out.print("Impossible");
        }

        // Possible solution is stored in A[]
        else {
            for (int i = 0; i < k; ++i)
                System.out.print(A[i] + " ");
        }
    }

    public static void main(String []args){

        int n = 12;
        int k = 6;

        FindAllElements(n, k);
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to print k numbers which are
# powers of two and whose sum is equal to n
def FindAllElements(n, k):

    # Initialising the sum with k
    sum = k

    # Initialising an array A with k elements
    # and filling all elements with 1
    A = [1 for i in range(k)]
    i = k - 1
    while(i >= 0):

        # Iterating A[] from k-1 to 0
        while (sum + A[i] <= n):

            # Update sum and A[i] till
            # sum + A[i] is less than equal to n
            sum += A[i]
            A[i] *= 2
        i -= 1

    # Impossible to find the combination
    if (sum != n):
        print("Impossible")

    # Possible solution is stored in A[]
    else:
        for i in range(0, k, 1):
            print(A[i], end = ' ')

# Driver code
if __name__ == '__main__':
    n = 12
    k = 6

    FindAllElements(n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GfG
{

    // Function to print k numbers
    // which are powers of two
    // and whose sum is equal to n
    public static void FindAllElements(int n, int k)
    {
        // Initialising the sum with k
        int sum = k;

        // Initialising an array A with k elements
        // and filling all elements with 1
        int[] A = new int[k];
        for(int i = 0; i < k; i++)
            A[i] = 1;

        for (int i = k - 1; i >= 0; --i)
        {

            // Iterating A[] from k-1 to 0
            while (sum + A[i] <= n)
            {

                // Update sum and A[i]
                // till sum + A[i] is less than equal to n
                sum += A[i];
                A[i] *= 2;
            }
        }

        // Impossible to find the combination
        if (sum != n)
        {
            Console.Write("Impossible");
        }

        // Possible solution is stored in A[]
        else
        {
            for (int i = 0; i < k; ++i)
                Console.Write(A[i] + " ");
        }
    }

    // Driver code
    public static void Main(String []args)
    {

        int n = 12;
        int k = 6;

        FindAllElements(n, k);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print k numbers which are
// powers of two and whose sum is equal to n
function FindAllElements($n, $k)
{
    // Initialising the sum with k
    $sum = $k;

    // Initialising an array A with k elements
    // and filling all elements with 1
    $A = array_fill(0, $k, 1) ;

    for ($i = $k - 1; $i >= 0; --$i)
    {

        // Iterating A[] from k-1 to 0
        while ($sum + $A[$i] <= $n)
        {

            // Update sum and A[i] till 
            // sum + A[i] is less than equal to n
            $sum += $A[$i];
            $A[$i] *= 2;
        }
    }

    // Impossible to find the combination
    if ($sum != $n)
    {
        echo"Impossible";
    }

    // Possible solution is stored in A[]
    else
    {
        for ($i = 0; $i < $k; ++$i)
            echo $A[$i], ' ';
    }
}

// Driver code
$n = 12;
$k = 6;

FindAllElements($n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to print k numbers which are powers of two
// and whose sum is equal to n
function FindAllElements( n, k)
{
    // Initialising the sum with k
    let sum = k;

    // Initialising an array A with k elements
    // and filling all elements with 1
    let A = new Array(k).fill(1);

    for (let i = k - 1; i >= 0; --i) {

        // Iterating A[] from k-1 to 0
        while (sum + A[i] <= n) {

            // Update sum and A[i]
            // till sum + A[i] is less than equal to n
            sum += A[i];
            A[i] *= 2;
        }
    }

    // Impossible to find the combination
    if (sum != n) {
        document.write("Impossible");
    }

    // Possible solution is stored in A[]
    else {
        for (let i = 0; i < k; ++i)
            document.write(A[i] + " ");
    }
}

// Driver Code

let n = 12;
let k = 6;

FindAllElements(n, k);

</script>
```

**Output**

```
1 1 1 1 4 4 
```

**时间复杂度:** O(k*log <sub>2</sub> (n-k))

**辅助空间:** O(k)