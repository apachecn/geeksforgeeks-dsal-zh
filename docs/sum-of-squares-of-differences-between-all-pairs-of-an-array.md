# 数组中所有对之间的差的平方和

> 原文:[https://www . geeksforgeeks . org/数组所有对之间的差平方和/](https://www.geeksforgeeks.org/sum-of-squares-of-differences-between-all-pairs-of-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算所有可能对的差的平方和。

**示例:**

> **输入:** arr[] = {2，8，4}
> **输出:** 56
> **解释:**
> 所有可能对的平方差之和=(2–8)<sup>2</sup>+(2–4)<sup>2</sup>+(8–4)<sup>2</sup>= 56
> 
> **输入:** arr[] = {-5，8，9，-4，-3}
> 输出: 950

**天真方法:**最简单的方法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)并计算每对的差的平方，并不断将其添加到一个变量中，比如**求和**。最后，打印**总和的值。**

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**最优思想基于以如下方式重新排列表达式:

> <sub>I = 2</sub><sup>【n】</sup>【j = 1】<sup>【I-1】</sup>(a<sub>【I】</sub>-a】<sub>【j】</sub>
> 
> 由于 A<sub>I</sub>–A<sub>I</sub>= 0，上述表达式可重新排列为 1/2×(∑<sub>I = 1</sub><sup>n</sup>∑<sub>j = 1</sub><sup>n</sup>(A<sub>I</sub>-A<sub>j</sub>)<sup>2</sup>)可利用下式进一步简化:
> 
> (A–B)<sup>2</sup>= A<sup>2</sup>+B<sup>2</sup>–2 * A * B
> 
> as 1/2 *(√t0]I = 1<sup>【n】</sup>【j = 1】<sup>(a<sub>2</sub></sup>
> 
> 最终表达式为 n *∑<sub>I = 1</sub><sup>n</sup>A<sub>I</sub><sup>2</sup>–(≘<sub>I = 1</sub><sup>n</sup>A<sub>I</sub>)<sup>2</sup>，可以通过线性迭代数组来计算。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of squares
// of differences of all possible pairs
void sumOfSquaredDifferences(int arr[],
                             int N)
{
    // Stores the final sum
    int ans = 0;

    // Stores temporary values
    int sumA = 0, sumB = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        sumA += (arr[i] * arr[i]);
        sumB += arr[i];
    }

    sumA = N * sumA;
    sumB = (sumB * sumB);

    // Final sum
    ans = sumA - sumB;

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 8, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to find sum of square
    // of differences of all possible pairs
    sumOfSquaredDifferences(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate sum of squares
// of differences of all possible pairs
static void sumOfSquaredDifferences(int arr[],
                                    int N)
{

    // Stores the final sum
    int ans = 0;

    // Stores temporary values
    int sumA = 0, sumB = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        sumA += (arr[i] * arr[i]);
        sumB += arr[i];
    }

    sumA = N * sumA;
    sumB = (sumB * sumB);

    // Final sum
    ans = sumA - sumB;

    // Print the answer
    System.out.println(ans);
}

// Driver Code
public static void main (String[] args)
{

    // Given array
    int arr[] = { 2, 8, 4 };

    // Size of the array
    int N = arr.length;

    // Function call to find sum of square
    // of differences of all possible pairs
    sumOfSquaredDifferences(arr, N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of squares
# of differences of all possible pairs
def sumOfSquaredDifferences(arr, N):

    # Stores the final sum
    ans = 0

    # Stores temporary values
    sumA, sumB = 0, 0

    # Traverse the array
    for i in range(N):
        sumA += (arr[i] * arr[i])
        sumB += arr[i]

    sumA = N * sumA
    sumB = (sumB * sumB)

    # Final sum
    ans = sumA - sumB

    # Prthe answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [2, 8, 4]

    # Size of the array
    N = len(arr)

    # Function call to find sum of square
    # of differences of all possible pairs
    sumOfSquaredDifferences(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum of squares
// of differences of all possible pairs
static void sumOfSquaredDifferences(int []arr,
                                    int N)
{

    // Stores the final sum
    int ans = 0;

    // Stores temporary values
    int sumA = 0, sumB = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        sumA += (arr[i] * arr[i]);
        sumB += arr[i];
    }

    sumA = N * sumA;
    sumB = (sumB * sumB);

    // Final sum
    ans = sumA - sumB;

    // Print the answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(string[] args)
{

    // Given array
    int []arr = { 2, 8, 4 };

    // Size of the array
    int N = arr.Length;

    // Function call to find sum of square
    // of differences of all possible pairs
    sumOfSquaredDifferences(arr, N);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate sum of squares
// of differences of all possible pairs
function sumOfSquaredDifferences(arr, N)
{

    // Stores the final sum
    let ans = 0;

    // Stores temporary values
    let sumA = 0, sumB = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        sumA += (arr[i] * arr[i]);
        sumB += arr[i];
    }

    sumA = N * sumA;
    sumB = (sumB * sumB);

    // Final sum
    ans = sumA - sumB;

    // Print the answer
    document.write(ans);
}

// Driver Code

// Given array
let arr = [ 2, 8, 4 ];

// Size of the array
let N = arr.length;

// Function call to find sum of square
// of differences of all possible pairs
sumOfSquaredDifferences(arr, N);

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
56
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)