# 方式数 N 可分为四部分构成矩形

> 原文:[https://www . geesforgeks . org/路数-n-可分为四部分构建矩形/](https://www.geeksforgeeks.org/number-of-ways-n-can-be-divided-into-four-parts-to-construct-a-rectangle/)

给定一个整数 **N** ，任务是将数字分成四个部分，这样被分割的部分可以用来构造一个矩形，而不是正方形。找出有多少种方法，这样就可以满足条件将数除。
**例:**

> **输入:** N = 8
> **输出:** 1
> **输入:** N = 10
> **输出:** 2

**方法:**由于数字必须被分割，这样矩形由被分割的四个部分组成，所以**如果数字是奇数**，那么**的路数将为零**，因为矩形的**周长总是偶数**
现在，如果 **n 是偶数**，那么只有**(n–2)/4**的路数来分割数字，例如，
如果必须将 8 分成四份，那么只有**(8–2)/4 = 1**路，即**【1，1，3，3】**，没有其他路。 因为你只能取**边长<= n/2–1**组成一个有效的矩形，然后从那些**n/2–1**的矩形中再除以 2，避免重复计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// required number of ways
int cntWays(int n)
{
    if (n % 2 == 1) {
        return 0;
    }
    else {
        return (n - 2) / 4;
    }
}

// Driver code
int main()
{
    int n = 18;

    cout << cntWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the
    // required number of ways
    static int cntWays(int n)
    {
        if (n % 2 == 1)
        {
            return 0;
        }
        else
        {
            return (n - 2) / 4;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 18;

        System.out.println(cntWays(n));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the
# required number of ways
def cntWays(n) :
    if n % 2 == 1 :
        return 0
    else:
        return (n - 2) // 4

# Driver code
n = 18
print(cntWays(n))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // required number of ways
    static int cntWays(int n)
    {
        if (n % 2 == 1)
        {
            return 0;
        }
        else
        {
            return (n - 2) / 4;
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 18;

        Console.WriteLine(cntWays(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the
// required number of ways
function cntWays(n)
{
    if (n % 2 == 1)
    {
        return 0;
    }
    else
    {
        return (n - 2) / 4;
    }
}

// Driver code

var n = 18;

document.write(cntWays(n));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(1)