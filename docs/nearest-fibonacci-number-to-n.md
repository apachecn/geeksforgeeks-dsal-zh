# 最接近 N 的斐波那契数

> 原文:[https://www . geesforgeks . org/near-Fibonacci-number-to-n/](https://www.geeksforgeeks.org/nearest-fibonacci-number-to-n/)

给定一个正整数 **N** ，任务是找到与给定整数 **N** 最近的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。如果有两个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)与 **N** 有相同的差异，则打印较小的值。

**示例:**

> **输入:** N = 20
> **输出:** 21
> **说明:**离 20 最近的斐波那契数是 21。
> 
> **输入:**N = 17
> T3】输出: 13

**方法:**按照以下步骤解决问题:

*   如果 **N** 等于 **0** ，则打印 **0** 作为结果。
*   初始化一个变量，比如说**和**，来存储离**最近的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)**。
*   初始化两个变量，将**第一个**设为 **0** ，将**第二个**设为 **1** ，存储[斐波那契数列](https://www.geeksforgeeks.org/program-to-print-first-n-fibonacci-numbers/)的第一项和第二项。
*   将**第一个**和**第二个**的总和存储在一个变量中，比如说**第三个**。
*   迭代至**第三个**的值最多为 **N** ，执行以下步骤:
    *   将**第一**的值更新为**第二**和**第二**到**第三**的值。
    *   将**第一**和**第二**的总和存储在变量**第三**中。
*   如果**秒**和 **N** 的[绝对](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)差最多是**秒**和 **N** 的值，那么更新 **ans** 的值为**秒**。
*   否则，将**和**的值更新为**第三个**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Fibonacci
// number which is nearest to N
void nearestFibonacci(int num)
{
    // Base Case
    if (num == 0) {
        cout << 0;
        return;
    }

    // Initialize the first & second
    // terms of the Fibonacci series
    int first = 0, second = 1;

    // Store the third term
    int third = first + second;

    // Iterate until the third term
    // is less than or equal to num
    while (third <= num) {

        // Update the first
        first = second;

        // Update the second
        second = third;

        // Update the third
        third = first + second;
    }

    // Store the Fibonacci number
    // having smaller difference with N
    int ans = (abs(third - num)
               >= abs(second - num))
                  ? second
                  : third;

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int N = 17;
    nearestFibonacci(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the Fibonacci
// number which is nearest to N
static void nearestFibonacci(int num)
{

    // Base Case
    if (num == 0)
    {
        System.out.print(0);
        return;
    }

    // Initialize the first & second
    // terms of the Fibonacci series
    int first = 0, second = 1;

    // Store the third term
    int third = first + second;

    // Iterate until the third term
    // is less than or equal to num
    while (third <= num)
    {

        // Update the first
        first = second;

        // Update the second
        second = third;

        // Update the third
        third = first + second;
    }

    // Store the Fibonacci number
    // having smaller difference with N
    int ans = (Math.abs(third - num) >=
               Math.abs(second - num)) ?
               second : third;

    // Print the result
     System.out.print(ans);
}

// Driver Code
public static void main (String[] args)
{
    int N = 17;

    nearestFibonacci(N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Fibonacci
# number which is nearest to N
def nearestFibonacci(num):

    # Base Case
    if (num == 0):
        print(0)
        return

    # Initialize the first & second
    # terms of the Fibonacci series
    first = 0
    second = 1

    # Store the third term
    third = first + second

    # Iterate until the third term
    # is less than or equal to num
    while (third <= num):

        # Update the first
        first = second

        # Update the second
        second = third

        # Update the third
        third = first + second

    # Store the Fibonacci number
    # having smaller difference with N
    if (abs(third - num) >=
        abs(second - num)):
        ans =  second
    else:
        ans = third

    # Print the result
    print(ans)

# Driver Code
if __name__ == '__main__':

    N = 17

    nearestFibonacci(N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the Fibonacci
// number which is nearest to N
static void nearestFibonacci(int num)
{

    // Base Case
    if (num == 0)
    {
        Console.Write(0);
        return;
    }

    // Initialize the first & second
    // terms of the Fibonacci series
    int first = 0, second = 1;

    // Store the third term
    int third = first + second;

    // Iterate until the third term
    // is less than or equal to num
    while (third <= num)
    {

        // Update the first
        first = second;

        // Update the second
        second = third;

        // Update the third
        third = first + second;
    }

    // Store the Fibonacci number
    // having smaller difference with N
    int ans = (Math.Abs(third - num) >=
              Math.Abs(second - num)) ?
                       second : third;

    // Print the result
     Console.Write(ans);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 17;

    nearestFibonacci(N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the Fibonacci
// number which is nearest to N
function nearestFibonacci(num)
{
    // Base Case
    if (num == 0) {
        document.write(0);
        return;
    }

    // Initialize the first & second
    // terms of the Fibonacci series
    let first = 0, second = 1;

    // Store the third term
    let third = first + second;

    // Iterate until the third term
    // is less than or equal to num
    while (third <= num) {

        // Update the first
        first = second;

        // Update the second
        second = third;

        // Update the third
        third = first + second;
    }

    // Store the Fibonacci number
    // having smaller difference with N
    let ans = (Math.abs(third - num)
               >= Math.abs(second - num))
                  ? second
                  : third;

    // Print the result
    document.write(ans);
}

// Driver Code
    let N = 17;
    nearestFibonacci(N);

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*