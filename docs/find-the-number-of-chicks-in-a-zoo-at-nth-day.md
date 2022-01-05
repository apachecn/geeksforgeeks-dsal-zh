# 计算第 n 天动物园里小鸡的数量

> 原文:[https://www . geeksforgeeks . org/find-第 n 天动物园的小鸡数量/](https://www.geeksforgeeks.org/find-the-number-of-chicks-in-a-zoo-at-nth-day/)

考虑到动物园只有一只小鸡。一只小鸡每天生 2 只小鸡，小鸡的预期寿命是 6 天。任务是找到第 N天的小鸡数量。
**例:**

> **输入:** N = 3
> **输出:** 9
> 第一天:1 只小鸡
> 第二天:1 + 2 = 3
> 第三天:3 + 6 = 9
> **输入:** N = 12
> **输出:** 173988

**简单做法:**假设一只小鸡的预期寿命是 6 天，那么直到第 6 天都不会有小鸡死亡。当天每天的人口将是前一天的 3 倍。还有一点需要注意的是，当天出生的小鸡不算在当天，而是在第二天计算，变化从第七天开始。所以主要计算从第七天开始。
**第七天:**第一天的小鸡死了，所以根据人工计算是 726 只。
**第八天:**第(8-6)天，即第二天出生的两只新生雏鸡死亡。这将影响当前人口的 2/3。这个人口需要从前一天的人口中扣除，因为今天，也就是第 8 天会有更多的新生儿出生，所以我们不能直接从今天的人口中扣除。因为那天出生的新生儿，这个数字会增加三倍。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the number
// of chicks on the nth day
ll getChicks(int n)
{

    // Size of dp[] has to be
    // at least 6 (1-based indexing)
    int size = max(n, 7);
    ll dp[size];

    dp[0] = 0;
    dp[1] = 1;

    // Every day current population
    // will be three times of the previous day
    for (int i = 2; i <= 6; i++) {
        dp[i] = dp[i - 1] * 3;
    }

    // Manually calculated value
    dp[7] = 726;

    // From 8th day onwards
    for (int i = 8; i <= n; i++) {

        // Chick population decreases by 2/3 everyday.
        // For 8th day on [i-6] i.e 2nd day population
        // was 3 and so 2 new born die on the 6th day
        // and so on for the upcoming days
        dp[i] = (dp[i - 1] - (2 * dp[i - 6] / 3)) * 3;
    }

    return dp[n];
}

// Driver code
int main()
{
    int n = 3;

    cout << getChicks(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

public class GFG {

// Function to return the number
// of chicks on the nth day
static long getChicks(int n)
{

    // Size of dp[] has to be
    // at least 6 (1-based indexing)
    int size = Math.max(n, 7);
    long []dp = new long[size];

    dp[0] = 0;
    dp[1] = 1;

    // Every day current population
    // will be three times of the previous day
    for (int i = 2; i < 6; i++) {
        dp[i] = dp[i - 1] * 3;
    }

    // Manually calculated value
    dp[6] = 726;

    // From 8th day onwards
    for (int i = 8; i <= n; i++) {

        // Chick population decreases by 2/3 everyday.
        // For 8th day on [i-6] i.e 2nd day population
        // was 3 and so 2 new born die on the 6th day
        // and so on for the upcoming days
        dp[i] = (dp[i - 1] - (2 * dp[i - 6] / 3)) * 3;
    }

    return dp[n];
}

// Driver code
public static void main(String[] args) {
int n = 3;

    System.out.println(getChicks(n));
    }
}
// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```

# Python implementation of the approach

# Function to return the number
# of chicks on the nth day
def getChicks(n):

    # Size of dp[] has to be
    # at least 6 (1-based indexing)
    size = max(n, 7);
    dp = [0]*size;

    dp[0] = 0;
    dp[1] = 1;

    # Every day current population
    # will be three times of the previous day
    for i in range(2,7):
        dp[i] = dp[i - 1] * 3;

    # Manually calculated value
    dp[6] = 726;

    # From 8th day onwards
    for i in range(8,n+1):

        # Chick population decreases by 2/3 everyday.
        # For 8th day on [i-6] i.e 2nd day population
        # was 3 and so 2 new born die on the 6th day
        # and so on for the upcoming days
        dp[i] = (dp[i - 1] - (2 * dp[i - 6] // 3)) * 3;

    return dp[n];

# Driver code
n = 3;

print(getChicks(n));

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number
// of chicks on the nth day
static long getChicks(int n)
{

    // Size of dp[] has to be
    // at least 6 (1-based indexing)
    int size = Math.Max(n, 7);
    long []dp = new long[size];

    dp[0] = 0;
    dp[1] = 1;

    // Every day current population
    // will be three times of the previous day
    for (int i = 2; i < 6; i++)
    {
        dp[i] = dp[i - 1] * 3;
    }

    // Manually calculated value
    dp[6] = 726;

    // From 8th day onwards
    for (int i = 8; i <= n; i++)
    {

        // Chick population decreases by 2/3 everyday.
        // For 8th day on [i-6] i.e 2nd day population
        // was 3 and so 2 new born die on the 6th day
        // and so on for the upcoming days
        dp[i] = (dp[i - 1] - (2 * dp[i - 6] / 3)) * 3;
    }

    return dp[n];
}

// Driver code
static public void Main ()
{

    int n = 3;
    Console.WriteLine(getChicks(n));
}
}

// This code has been contributed by @Tushil..
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the number
    // of chicks on the nth day
    function getChicks(n)
    {

        // Size of dp[] has to be
        // at least 6 (1-based indexing)
        let size = Math.max(n, 7);
        let dp = new Array(size);
        dp.fill(0);

        dp[0] = 0;
        dp[1] = 1;

        // Every day current population
        // will be three times of the previous day
        for (let i = 2; i < 6; i++)
        {
            dp[i] = dp[i - 1] * 3;
        }

        // Manually calculated value
        dp[6] = 726;

        // From 8th day onwards
        for (let i = 8; i <= n; i++)
        {

            // Chick population decreases by 2/3 everyday.
            // For 8th day on [i-6] i.e 2nd day population
            // was 3 and so 2 new born die on the 6th day
            // and so on for the upcoming days
            dp[i] = (dp[i - 1] -
            (2 * parseInt(dp[i - 6] / 3, 10))) * 3;
        }

        return dp[n];
    }

    let n = 3;
    document.write(getChicks(n));

</script>
```

**Output:** 

```
9
```

**有效方法:**如果你仔细观察，你可以观察到一个模式，即动物园中第 N 天的小鸡数量可以直接使用公式**幂(3，N–1)**来计算。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the number
// of chicks on the nth day
ll getChicks(int n)
{

    ll chicks = (ll)pow(3, n - 1);

    return chicks;
}

// Driver code
int main()
{
    int n = 3;

    cout << getChicks(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the number
// of chicks on the nth day
static int getChicks(int n)
{

    int chicks = (int)Math.pow(3, n - 1);

    return chicks;
}

// Driver code
public static void main (String[] args)
{

    int n = 3;
    System.out.println (getChicks(n));
}
}

// This code is contributed by Tushil.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the number
# of chicks on the nth day
def getChicks( n):

    chicks = pow(3, n - 1)

    return chicks

# Driver code
if __name__ == "__main__":
    n = 3

    print ( getChicks(n))

# This code is contributed by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number
    // of chicks on the nth day
    static int getChicks(int n)
    {

        int chicks = (int)Math.Pow(3, n - 1);

        return chicks;
    }

    // Driver code
    public static void Main()
    {

        int n = 3;
        Console.WriteLine(getChicks(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the number
    // of chicks on the nth day
    function getChicks(n)
    {

        let chicks = Math.pow(3, n - 1);

        return chicks;
    }

    let n = 3;
      document.write(getChicks(n));

</script>
```

**Output:** 

```
9
```