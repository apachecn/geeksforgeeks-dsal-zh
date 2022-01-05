# 找到可用于称量[1，X]

范围内所有重量的最佳重量

> 原文:[https://www . geeksforgeeks . org/find-optimal-weights-哪些可以用来称量范围内的所有重量-1-x/](https://www.geeksforgeeks.org/find-optimal-weights-which-can-be-used-to-weigh-all-the-weights-in-the-range-1-x/)

给定一个整数 **X** ，任务是找到一个最优的砝码组 **{w <sub>1</sub> ，w <sub>2</sub> ，w <sub>3</sub> ，…，w <sub>n</sub> }** ，这样我们就可以使用双面称量天平盘称量/确定从 **1** 到 **X** 的所有砝码。**注意**所有重量必须唯一， **n** 应尽可能最小。
**例:**

> **输入:**X = 7
> T3】输出:1 3 9
> T6】
> 
> | 砝码 | 左侧 | 正面 |
> | --- | --- | --- |
> | one | one | **1** |
> | Two | 2 + **1** | **3** |
> | three | three | **3** |
> | four | four | **1** + **3** |
> | five | 5 + **1** + **3** | **9** |
> | six | 6 + **3** | **9** |
> | seven | 7 + **3** | **1** + **9** |
> 
> **输入:**X = 20
> T3】输出: 1 3 9 27

**进场:**

1.  一种最佳方法是使用 3 的幂的权重，即 **{1，3，9，27，81，243，…}**
2.  通过归纳可以证明，使用 **{1，3，9，27，81，…，pow(3，n)}** ，我们可以平衡从 **1** 到 **(pow(3，n+1)–1)/2**的所有重量。
3.  所以，找到 **n** 的值，这样从 **1** 到 **X** 的所有值都可以平衡并打印结果。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the optimal weights
void findWeights(int X)
{
    int sum = 0;

    // Number of weights required
    int power = 0;

    // Finding the value of required powers of 3
    while (sum < X) {
        sum = pow(3, power + 1) - 1;
        sum /= 2;
        power++;
    }

    // Optimal Weights are powers of 3
    int ans = 1;
    for (int i = 1; i <= power; i++) {
        cout << ans << " ";
        ans = ans * 3;
    }
}

// Driver code
int main()
{
    int X = 2;

    findWeights(X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

public class GFG
{

    // Function to find the optimal weights
    static void findWeights(int X)
    {
        int sum = 0;

        // Number of weights required
        int power = 0;
        int number = 3;

        // Finding the value of required powers of 3
        while (sum < X)
        {
            sum = number - 1;
            sum /= 2;
            power++;
            number *= 3;
        }

        // Optimal Weights are powers of 3
        int ans = 1;
        for (int i = 1; i <= power; i++)
        {
            System.out.print(ans + " ");
            ans = ans * 3;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int X = 2;

        findWeights(X);

    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the optimal weights
def findWeights(X):

    sum = 0

    # Number of weights required
    power = 0

    # Finding the value of required powers of 3
    while (sum < X):
        sum = pow(3, power + 1) - 1
        sum //= 2
        power += 1

    # Optimal Weights are powers of 3
    ans = 1
    for i in range(1, power + 1):
        print(ans, end = " ")
        ans = ans * 3

# Driver code
X = 2

findWeights(X)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the optimal weights
    static void findWeights(int X)
    {
        int sum = 0;

        // Number of weights required
        int power = 0;
        int number = 3;

        // Finding the value of required powers of 3
        while (sum < X)
        {
            sum = number - 1;
            sum /= 2;
            power++;
            number *= 3;
        }

        // Optimal Weights are powers of 3
        int ans = 1;
        for (int i = 1; i <= power; i++)
        {
            Console.Write(ans + " ");
            ans = ans * 3;
        }
    }

    // Driver code
    static public void Main ()
    {
        int X = 2;
        findWeights(X);
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

 // Function to find the optimal weights
function findWeights(X)
{
    let sum = 0;

        // Number of weights required
        let power = 0;
        let number = 3;

        // Finding the value of required powers of 3
        while (sum < X)
        {
            sum = number - 1;
            sum = Math.floor(sum/2);
            power++;
            number *= 3;
        }

        // Optimal Weights are powers of 3
        let ans = 1;
        for (let i = 1; i <= power; i++)
        {
            document.write(ans + " ");
            ans = ans * 3;
        }
}

// Driver code
let X = 2;

findWeights(X);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1 3
```