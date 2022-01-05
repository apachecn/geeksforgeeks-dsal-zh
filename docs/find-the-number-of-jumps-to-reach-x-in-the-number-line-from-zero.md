# 从零开始在数字线中找到达到 X 的跳跃次数

> 原文:[https://www . geeksforgeeks . org/find-the-number-of-jump-to-reach-x-in-line-from-zero/](https://www.geeksforgeeks.org/find-the-number-of-jumps-to-reach-x-in-the-number-line-from-zero/)

给定一个整数 X。任务是找到从零开始到达数字线中的点 X 的跳跃次数。
**注**:第一跳的长度可以是一个单位，每一次连续的跳跃都会比前一次跳跃的长度正好长一个单位。每次跳跃允许向左或向右。
**示例:**

```
Input : X = 8
Output : 4
Explanation : 
0 -> -1 -> 1 -> 4-> 8 are possible stages.

Input : X = 9
Output : 5
Explanation : 
0 -> -1 -> -3 -> 0 -> 4-> 9 are 
possible stages
```

**走近**:仔细观察，很容易说:

*   如果你总是朝着正确的方向跳，那么在 **n** 跳之后，你将会到达*T3】p= 1+2+3+4+…+n .*
*   在这 n 次跳跃中的任何一次，如果你在第 k 次跳跃中没有向右跳跃，而是向左跳跃(k<=n), you would be at point ***p–2k***)。
*   此外，通过仔细选择向左跳和向右跳，在 n 次跳跃后，您可以位于 n * (n + 1) / 2 和–( n * (n + 1) / 2)之间的任意点，具有与 n *(n+1)/2 相同的奇偶性。

记住以上几点，你必须做的是模拟跳跃过程，总是向右跳跃，如果在某个时刻，你已经到达了一个与 X 具有相同奇偶性的点，并且处于或超过 X，你就会有你的答案。
以下是上述方法的实现:

## C++

```
// C++ program to find the number of jumps
// to reach X in the number line from zero

#include <bits/stdc++.h>
using namespace std;

// Utility function to calculate sum
// of numbers from 1 to x
int getsum(int x)
{
    return (x * (x + 1)) / 2;
}

// Function to find the number of jumps
// to reach X in the number line from zero
int countJumps(int n)
{
    // First make number positive
    // Answer will be same either it is
    // Positive or negative
    n = abs(n);

    // To store required answer
    int ans = 0;

    // Continue till number is lesser or not in same parity
    while (getsum(ans) < n or (getsum(ans) - n) & 1)
        ans++;

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int n = 9;

    cout << countJumps(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of jumps
// to reach X in the number line from zero

class GFG
{

// Utility function to calculate sum
// of numbers from 1 to x
static int getsum(int x)
{
    return (x * (x + 1)) / 2;
}

// Function to find the number of jumps
// to reach X in the number line from zero
static int countJumps(int n)
{
    // First make number positive
    // Answer will be same either it is
    // Positive or negative
    n = Math.abs(n);

    // To store required answer
    int ans = 0;

    // Continue till number is lesser
    // or not in same parity
    while (getsum(ans) < n ||
         ((getsum(ans) - n) & 1) > 0)
        ans++;

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String args[])
{
    int n = 9;

    System.out.println(countJumps(n));
}
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 program to find the number of jumps
# to reach X in the number line from zero

# Utility function to calculate sum
# of numbers from 1 to x
def getsum(x):
    return int((x * (x + 1)) / 2)

# Function to find the number of jumps
# to reach X in the number line from zero
def countJumps(n):

    # First make number positive
    # Answer will be same either it is
    # Positive or negative
    n = abs(n)

    # To store the required answer
    ans = 0

    # Continue till number is lesser
    # or not in same parity
    while (getsum(ans) < n or
          (getsum(ans) - n) & 1):
        ans += 1

    # Return the required answer
    return ans

# Driver code
if __name__ == '__main__':
    n = 9

    print(countJumps(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the number of jumps
// to reach X in the number line from zero
using System;

class GFG
{

// Utility function to calculate sum
// of numbers from 1 to x
static int getsum(int x)
{
    return (x * (x + 1)) / 2;
}

// Function to find the number of jumps
// to reach X in the number line from zero
static int countJumps(int n)
{
    // First make number positive
    // Answer will be same either it is
    // Positive or negative
    n = Math.Abs(n);

    // To store required answer
    int ans = 0;

    // Continue till number is lesser or not in same parity
    while (getsum(ans) < n || ((getsum(ans) - n) & 1)>0)
        ans++;

    // Return the required answer
    return ans;
}

// Driver code
static void Main()
{
    int n = 9;

    Console.WriteLine(countJumps(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of jumps
// to reach X in the number line from zero

// Utility function to calculate sum
// of numbers from 1 to x
function getsum($x)
{
    return ($x * ($x + 1)) / 2;
}

// Function to find the number of jumps
// to reach X in the number line from zero
function countJumps($n)
{
    // First make number positive
    // Answer will be same either it is
    // Positive or negative
    $n = abs($n);

    // To store required answer
    $ans = 0;

    // Continue till number is lesser
    // or not in same parity
    while (getsum($ans) < $n or
          (getsum($ans) - $n) & 1)
        $ans++;

    // Return the required answer
    return $ans;
}

// Driver code
$n = 9;

echo countJumps($n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number of jumps
// to reach X in the number line from zero

// Utility function to calculate sum
// of numbers from 1 to x
function getsum(x)
{
    return (x * (x + 1)) / 2;
}

// Function to find the number of jumps
// to reach X in the number line from zero
function countJumps(n)
{
    // First make number positive
    // Answer will be same either it is
    // Positive or negative
    n = Math.abs(n);

    // To store required answer
    let ans = 0;

    // Continue till number is lesser
    // or not in same parity
    while (getsum(ans) < n ||
         ((getsum(ans) - n) & 1) > 0)
        ans++;

    // Return the required answer
    return ans;
}    

// Driver Code

      let n = 9;

    document.write(countJumps(n));

</script>
```

**Output:** 

```
5
```