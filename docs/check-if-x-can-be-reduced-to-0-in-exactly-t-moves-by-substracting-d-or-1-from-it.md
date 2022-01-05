# 通过减去 D 或 1 来检查 X 是否能在精确的 T 移动中减少到 0

> 原文:[https://www . geesforgeks . org/check-if-x-can-reduce-in-0-t-moves-by-减法-d-or-1-from-it/](https://www.geeksforgeeks.org/check-if-x-can-be-reduced-to-0-in-exactly-t-moves-by-substracting-d-or-1-from-it/)

给定一个整数 **X** 、 **D** 和 **T** ，任务是检查是否有可能在精确的 T 次移动中将 X 减少到 0。在每次移动中，X 可以减少 D 或 1。如果可能，打印“是”，否则打印“否”

**示例:**

> **输入:** X = 10，D = 3，T = 6
> **输出:**是
> **解释:**以下是应用的移动-
> X = X–3 = 7
> X = X–3 = 4
> X = X–1 = 3
> X = X–1 = 2
> X = X–1 = 1
> X = X–1 = 0
> 因此可以使 X = 0
> 
> **输入:** X = 10，D = 3，T = 5
> T3】输出:否

**天真的做法:**检查可能的减 D 和减 1 的招式，检查是否能在正好 T 的招式中让 X 变为 0。
**时间复杂度:** O(X)

**有效方法:**给定的问题可以通过以下步骤解决:

*   设 **K** 为 **X** 减 **D** 的次数
*   所以总距离为**K *(D)+(T–K)**，应该等于 **X** 。
    因此等式变为

> = > K *(D–1)+T = X
> =>K *(D–1)= X–T

*   要使有效答案存在，(**X**–**T**)应可被(**D**–1)整除

下面是上述方法的实现:

## C++

```
// C++ Program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check the above problem condition
int possibleReachingSequence(int X, int D, int T)
{
    // Check for base cases
    if (X < T) {
        cout << "NO";
        return 0;
    }
    if (T * D < X) {
        cout << "NO";
        return 0;
    }
    // Check if D - 1 is a divisor of X - T
    if ((X - T) % (D - 1) == 0) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
    return 0;
}

// Driver Code
int main()
{
    int X = 10, D = 3, T = 6;
    possibleReachingSequence(X, D, T);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check the above problem condition
static int possibleReachingSequence(int X, int D, int T)
{
    // Check for base cases
    if (X < T) {
        System.out.println("NO");
        return 0;
    }
    if (T * D < X) {
        System.out.println("NO");
        return 0;
    }
    // Check if D - 1 is a divisor of X - T
    if ((X - T) % (D - 1) == 0) {
        System.out.println("YES");
    }
    else {
        System.out.println("NO");
    }
    return 0;
}

// Driver Code
public static void main(String args[])
{
    int X = 10, D = 3, T = 6;
    possibleReachingSequence(X, D, T);
}
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check the above problem condition
def possibleReachingSequence(X, D, T):

  # Check the base case.
  if X < T:
    return "NO"
  if T*D < X:
    return "NO"

  # check if X-T is a divisor of D-1
  if (X - T) % (D - 1) == 0:
    return "YES"
  return "NO"

# Driver code
X = 10
D = 3
T = 6
print(possibleReachingSequence(X, D, T))

# This code is contributed by maddler.
```

## C#

```
// C# program for the above approach

using System;

public class GFG{

// Function to check the above problem condition
static int possibleReachingSequence(int X, int D, int T)
{
    // Check for base cases
    if (X < T) {
        Console.WriteLine("NO");
        return 0;
    }
    if (T * D < X) {
        Console.WriteLine("NO");
        return 0;
    }
    // Check if D - 1 is a divisor of X - T
    if ((X - T) % (D - 1) == 0) {
        Console.WriteLine("YES");
    }
    else {
        Console.WriteLine("NO");
    }
    return 0;
}

// Driver Code
public static void Main(string []args)
{
    int X = 10, D = 3, T = 6;
    possibleReachingSequence(X, D, T);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript Program to implement the above approach

// Function to check the above problem condition
function possibleReachingSequence(X, D, T)
{

  // Check for base cases
  if (X < T) {
    document.write("NO");
    return 0;
  }
  if (T * D < X) {
    document.write("NO");
    return 0;
  }

  // Check if D - 1 is a divisor of X - T
  if ((X - T) % (D - 1) == 0) {
    document.write("YES");
  } else {
    document.write("NO");
  }
  return 0;
}

// Driver Code

let X = 10,
  D = 3,
  T = 6;
possibleReachingSequence(X, D, T);

// This code is contributed by gfgking.
</script>
```

**Output**

```
YES
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)