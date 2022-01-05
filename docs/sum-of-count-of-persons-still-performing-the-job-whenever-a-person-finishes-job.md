# 每当一个人完成工作时，仍在执行工作的人数总和

> 原文:[https://www . geesforgeks . org/每当有人完成工作时仍在执行工作的人数总和/](https://www.geeksforgeeks.org/sum-of-count-of-persons-still-performing-the-job-whenever-a-person-finishes-job/)

给定两个表示人数的整数 **P** 和一个正整数 **K** 。每个人都被分配了同样的工作，而完成这项工作只需要 **K** 个小时。给出了一个条件，即所有人都可以在 **X** 小时的间隔内开始准确地执行他们的工作。每当**之前的**人员完成其工作时，计算仍在执行工作的人数。任务是找到这些计数的**和**。

**示例:**

> **输入:** P = 4，K = 6，X = 3
> **输出:** 5
> **说明:**让四人为 P <sub>1</sub> ，P <sub>2</sub> ，P <sub>3</sub> ，P <sub>4</sub>
> 
> *   P <sub>1</sub> 从 0 开始，到 6 结束
> *   p<sub>2</sub>3 点开始，9 点结束
> *   p<sub>3</sub>6 点开始，12 点结束
> *   p<sub>4</sub>9 点开始，15 点结束
> 
> 所以，当 P <sub>1</sub> 结束时，P <sub>2</sub> 和 P <sub>3</sub> 开始执行各自的工作，计数为 P <sub>1</sub> = 2
> 当 P <sub>2</sub> 结束时，P <sub>3</sub> 和 P <sub>4</sub> 开始执行各自的工作，计数为 P <sub>2</sub> = 2
> 当 P <sub>3</sub> 结束时，只有 P <sub>开始执行各自的工作 计数为 P <sub>3</sub> = 1
> 当 P <sub>4</sub> 结束时，此时没有人开始，所以计数为 P <sub>4</sub> = 0
> 因此，总计数= (2 + 2 + 1 + 0) = 5</sub>
> 
> **输入:** P = 9，K = 72，X = 8
> T3】输出: 36

**方法:**给定的问题可以用[数学](https://www.geeksforgeeks.org/what-is-the-importance-of-mathematics-in-computer-science/)的概念分析问题来解决。按照以下步骤解决问题:

*   找到**总人数**的**最小值**，不包括第一个(因为 P <sub>1</sub> 总是从 0 开始)和 **K/X** ，将其存储在一个变量中，比如 **a** 。
*   检查 a 是否等于 0
    *   如果是，返回 0。
    *   否则，通过数学公式计算总数。
*   返回计数的最终总和作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of count
// of persons that are still
// performing the job
int countPersons(int P, int K, int X)
{
    // Find the minimum of total persons
    // excluding the first one and K/X
    int a = min(P - 1, K / X);

    // If a is equal to 0, return 0
    if (a == 0) {
        return 0;
    }

    // Else calculate the total sum of
    // count by the making a formula
    int ans = max(0,
                  a * (a - 1) / 2)
              + a * (P - a);

    // Return the sum of count
    return ans;
}

// Driver Code
int main()
{
    int P = 22, K = 9, X = 1;

    cout << countPersons(P, K, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG {

// Function to find the sum of count
// of persons that are still
// performing the job
static int countPersons(int P, int K, int X)
{
    // Find the minimum of total persons
    // excluding the first one and K/X
    int a = Math.min(P - 1, K / X);

    // If a is equal to 0, return 0
    if (a == 0) {
        return 0;
    }

    // Else calculate the total sum of
    // count by the making a formula
    int ans = Math.max(0,
                  a * (a - 1) / 2)
              + a * (P - a);

    // Return the sum of count
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int P = 22, K = 9, X = 1;
    System.out.println(countPersons(P, K, X));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the sum of count
# of persons that are still
# performing the job
def countPersons(P, K, X):

    # Find the minimum of total persons
    # excluding the first one and K/X
    a = min(P - 1, K / X)

    # If a is equal to 0, return 0
    if a == 0:
        return 0

    # Else calculate the total sum of
    # count by the making a formula
    ans = max(0,
              a * (a - 1) / 2)

    # Return the sum of count
    return ans + a * (P - a)

# Driver Code
if __name__ == "__main__":
    P = 22
    K = 9
    X = 1
    print(int(countPersons(P, K, X)))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
class GFG {

// Function to find the sum of count
// of persons that are still
// performing the job
static int countPersons(int P, int K, int X)
{
    // Find the minimum of total persons
    // excluding the first one and K/X
    int a = Math.Min(P - 1, K / X);

    // If a is equal to 0, return 0
    if (a == 0) {
        return 0;
    }

    // Else calculate the total sum of
    // count by the making a formula
    int ans = Math.Max(0,
                  a * (a - 1) / 2)
              + a * (P - a);

    // Return the sum of count
    return ans;
}

// Driver Code
public static void Main()
{
    int P = 22, K = 9, X = 1;
    Console.Write(countPersons(P, K, X));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to find the sum of count
// of persons that are still
// performing the job
function countPersons(P, K, X)
{
    // Find the minimum of total persons
    // excluding the first one and K/X
    let a = Math.min(P - 1, K / X);

    // If a is equal to 0, return 0
    if (a == 0) {
        return 0;
    }

    // Else calculate the total sum of
    // count by the making a formula
    let ans = Math.max(0,
                  a * (a - 1) / 2)
              + a * (P - a);

    // Return the sum of count
    return ans;
}

// Driver Code
let P = 22, K = 9, X = 1;
document.write(countPersons(P, K, X));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
153
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)