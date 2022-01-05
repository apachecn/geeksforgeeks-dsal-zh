# 选择数字，使金额最大化

> 原文:[https://www . geesforgeks . org/select-numbers-in-so-way-to-maximum-of-money/](https://www.geeksforgeeks.org/select-numbers-in-such-way-to-maximize-the-amount-of-money/)

给定两个 N 个数的数组 A1 和 A2。有两个人 A 和 B 从 n 中选择号码，如果 A 选择第 I 个号码，那么他将获得 A1[i]笔钱，如果 B 选择第 I 个号码，那么他将获得 A2[i]笔钱，但是 A 不能选择超过 **X** 个号码，B 不能选择超过 **Y** 个号码。任务是选择 N 个数字，使最终的总资金量最大化。
**注:** X + Y > = N

```
Examples:
Input: N = 5, X = 3, Y = 3 
       A1[] = {1, 2, 3, 4, 5}, 
       A2= {5, 4, 3, 2, 1}
Output: 21 
B will take the first 3 orders and A 
will take the last two orders. 

Input: N = 2, X = 1, Y = 1 
       A1[] = {10, 10}, A2= {20, 20}
Output: 30 
```

**方法:**让我们创建一个新的数组 C，使得**C[I]= A2[I]–A1[I]**。现在我们将按降序对数组 **C** 进行排序。请注意，条件 **X + Y > = N** 保证我们能够将号码分配给任何一个人。假设对于某个 I，A1[i] > A2[i]，你给 B 分配了一个订单，这个分配导致的损失是 C[i]。同样，对于一些 I，A2[i] > A1[i]，你给 A 分配了一个号码，由于这个分配而遇到的损失是 C[i]。由于我们希望将遇到的损失降至最低，因此最好处理可能损失较高的数字，因为我们可以尝试减少起始部分的损失。分配损失较小的号码后，选择损失较大的号码是没有意义的。因此，我们最初将所有数字分配给 A，然后贪婪地减去损失。一旦指定的订单号在 X 以下，我们就存储它的最大值。
以下是上述方法的实施:

## C++

```
// C++ program to maximize profit

#include <bits/stdc++.h>
using namespace std;

// Function that maximizes the sum
int maximize(int A1[], int A2[], int n,
             int x, int y)
{
    // Array to store the loss
    int c[n];

    // Initial sum
    int sum = 0;

    // Generate the array C
    for (int i = 0; i < n; i++) {
        c[i] = A2[i] - A1[i];
        sum += A1[i];
    }

    // Sort the array elements
    // in descending order
    sort(c, c + n, greater<int>());

    // Variable to store the answer
    int maxi = -1;

    // Iterate in the array, C
    for (int i = 0; i < n; i++) {

        // Subtract the loss
        sum += c[i];

        // Check if X orders are going
        // to be used
        if (i + 1 >= (n - x))
            maxi = max(sum, maxi);
    }

    return maxi;
}

// Driver Code
int main()
{
    int A1[] = { 1, 2, 3, 4, 5 };
    int A2[] = { 5, 4, 3, 2, 1 };

    int n = 5;
    int x = 3, y = 3;

    cout << maximize(A1, A2, n, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximize profit
import java.util.*;

class GFG
{

// Function that maximizes the sum
static int maximize(int A1[], int A2[], int n,
            int x, int y)
{
    // Array to store the loss
    int[] c = new int[n];

    // Initial sum
    int sum = 0;

    // Generate the array C
    for (int i = 0; i < n; i++)
    {
        c[i] = A2[i] - A1[i];
        sum += A1[i];
    }

    // Sort the array elements
    // in descending order
int temp;
for(int i = 0; i < n - 1; i++)
{
    if(c[i] < c[i+1])
    {
        temp = c[i];
        c[i] = c[i + 1];
        c[i + 1] = temp;
    }
}

    // Variable to store the answer
    int maxi = -1;

    // Iterate in the array, C
    for (int i = 0; i < n; i++)
    {

        // Subtract the loss
        sum += c[i];

        // Check if X orders are going
        // to be used
        if (i + 1 >= (n - x))
            maxi = Math.max(sum, maxi);
    }

    return maxi;
}

// Driver Code
public static void main(String args[])
{
    int A1[] = { 1, 2, 3, 4, 5 };
    int A2[] = { 5, 4, 3, 2, 1 };

    int n = 5;
    int x = 3, y = 3;

    System.out.println(maximize(A1, A2, n, x, y));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to maximize profit

# Function that maximizes the Sum
def maximize(A1, A2, n, x, y):

    # Array to store the loss
    c = [0 for i in range(n)]

    # Initial Sum
    Sum = 0

    # Generate the array C
    for i in range(n):
        c[i] = A2[i] - A1[i]
        Sum += A1[i]

    # Sort the array elements
    # in descending order
    c.sort()
    c = c[::-1]

    # Variable to store the answer
    maxi = -1

    # Iterate in the array, C
    for i in range(n):

        # Subtract the loss
        Sum += c[i]

        # Check if X orders are going
        # to be used
        if (i + 1 >= (n - x)):
            maxi = max(Sum, maxi)

    return maxi

# Driver Code
A1 = [ 1, 2, 3, 4, 5 ]
A2 = [ 5, 4, 3, 2, 1 ]

n = 5
x, y = 3, 3

print(maximize(A1, A2, n, x, y))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to maximize profit
using System;

class GFG
{

    // Function that maximizes the sum
    static int maximize(int [] A1, int [] A2, int n,
                                    int x, int y)
    {
        // Array to store the loss
        int [] c = new int[n];

        // Initial sum
        int sum = 0;

        // Generate the array C
        for (int i = 0; i < n; i++)
        {
            c[i] = A2[i] - A1[i];
            sum += A1[i];
        }

        // Sort the array elements
        // in descending order
            int temp;
        for(int i = 0; i < n - 1; i++)
        {
            if(c[i] < c[i+1])
            {
                temp = c[i];
                c[i] = c[i + 1];
                c[i + 1] = temp;
            }
        }

        // Variable to store the answer
        int maxi = -1;

        // Iterate in the array, C
        for (int i = 0; i < n; i++)
        {

            // Subtract the loss
            sum += c[i];

            // Check if X orders are going
            // to be used
            if (i + 1 >= (n - x))
                maxi = Math.Max(sum, maxi);
        }

        return maxi;
    }

    // Driver Code
    public static void Main()
    {
        int [] A1 = { 1, 2, 3, 4, 5 };
        int [] A2 = { 5, 4, 3, 2, 1 };

        int n = 5;
        int x = 3, y = 3;

        Console.WriteLine(maximize(A1, A2, n, x, y));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to maximize profit

// Function that maximizes the sum
function maximize($A1, $A2, $n, $x, $y)
{
    # Array to store the loss
    $c = array();

    # Initial sum
    $sum = 0;

    // Generate the array C
    for ($i = 0; $i < $n; $i++)
    {
        $c[$i] = $A2[$i] - $A1[$i];
        $sum += $A1[$i];
    }

    // Sort the array elements
    // in descending order
    rsort($c);

    // Variable to store the answer
    $maxi = -1;

    // Iterate in the array, C
    for ($i = 0; $i < $n; $i++)
    {

        // Subtract the loss
        $sum += $c[$i];

        // Check if X orders are going
        // to be used
        if ($i + 1 >= ($n - $x))
            $maxi = max($sum, $maxi);
    }

    return $maxi;
}

# Driver Code
$A1 = array( 1, 2, 3, 4, 5 );
$A2 = array( 5, 4, 3, 2, 1 );

$n = 5;
$x = 3;
$y = 3;

echo maximize($A1, $A2, $n, $x, $y);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that maximizes the sum
function maximize(A1, A2, n,
            x, y)
{
    // Array to store the loss
    let c = Array(n).fill(0);

    // Initial sum
    let sum = 0;

    // Generate the array C
    for (let i = 0; i < n; i++)
    {
        c[i] = A2[i] - A1[i];
        sum += A1[i];
    }

    // Sort the array elements
    // in descending order
let temp;
for(let i = 0; i < n - 1; i++)
{
    if(c[i] < c[i+1])
    {
        temp = c[i];
        c[i] = c[i + 1];
        c[i + 1] = temp;
    }
}

    // Variable to store the answer
    let maxi = -1;

    // Iterate in the array, C
    for (let i = 0; i < n; i++)
    {

        // Subtract the loss
        sum += c[i];

        // Check if X orders are going
        // to be used
        if (i + 1 >= (n - x))
            maxi = Math.max(sum, maxi);
    }

    return maxi;
}

// Driver code

     let A1 = [ 1, 2, 3, 4, 5 ];
     let A2 = [ 5, 4, 3, 2, 1 ];

    let n = 5;
    let x = 3, y = 3;

    document.write(maximize(A1, A2, n, x, y));

</script>
```

**Output:** 

```
21
```

**时间复杂度:** O(N*logN)

**辅助空间:** O(1)