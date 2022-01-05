# 将分数拆分为分子为 1 的多个分数的和

> 原文:[https://www . geeksforgeeks . org/将分数拆分为分子为 1 的多个分数之和/](https://www.geeksforgeeks.org/split-the-fraction-into-sum-of-multiple-fractions-having-numerator-as-1/)

给定两个正整数 **N** 和 **D** ，将一个[分数](https://www.geeksforgeeks.org/tag/fraction/)表示为 **N/D** ，任务是将该分数分解为分子为 **1** 的多个分数之和。

**示例:**

> **输入:** n = 4，d = 5
> **输出:** 1/2，1/4，1/20
> **说明:** 1/2 + 1/4 + 1/20 = 4/5
> 
> **输入:** n = 15，d = 16
> T3】输出: 1/2，1/3，1/10，1/240

**方法:**想法是所有形式 **n/d** 的正[分数](https://www.geeksforgeeks.org/tag/fraction/)可以写成不同单位[分数](https://www.geeksforgeeks.org/tag/fraction/)的和。通过去掉最大单位[分数](https://www.geeksforgeeks.org/tag/fraction/) **1/x** 直到[分数](https://www.geeksforgeeks.org/tag/fraction/)达到**零**可以找到答案，其中 x 可以作为[上限](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) **(d/n)。**找到单位分数后，将分数更新为**n/d–1/x**所以每一步 **n** 变为 **nx-d** 和 **d** 变为 **dx** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to split the fraction into
// distinct unit fraction
vector<string> FractionSplit(long long n, long long d)
{

    // To store answer
    vector<string> UnitFactions;

    // While numerator is positive
    while (n > 0) {

        // Finding x = ceil(d/n)
        long long x = (d + n - 1) / n;

        // Add 1/x to list of ans
        string s = "1/" + to_string(x);
        UnitFactions.push_back(s);

        // Update fraction
        n = n * x - d;
        d = d * x;
    }
    return UnitFactions;
}

// Driver Code
int main()
{
    // Given Input
    long long n = 13, d = 18;

    // Function Call
    auto res = FractionSplit(n, d);

    // Print Answer
    for (string s : res)
        cout << s << ", ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Vector;

public class GFG {

    // Function to split the fraction into
    // distinct unit fraction
    static Vector<String> FractionSplit(long n, long d)
    {

        // To store answer
        Vector<String> UnitFactions = new Vector<>();

        // While numerator is positive
        while (n > 0) {

            // Finding x = ceil(d/n)
            long x = (d + n - 1) / n;

            // Add 1/x to list of ans
            String s = "1/" + String.valueOf(x);
            UnitFactions.add(s);

            // Update fraction
            n = n * x - d;
            d = d * x;
        }
        return UnitFactions;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given Input
        long n = 13, d = 18;

        // Function Call
        Vector<String> res = FractionSplit(n, d);

        // Print Answer
        for (String s : res)
            System.out.print(s + ", ");
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to split the fraction into
# distinct unit fraction
def FractionSplit(n, d):

    # To store answer
    UnitFactions = []

    # While numerator is positive
    while (n > 0):

        # Finding x = ceil(d/n)
        x = (d + n - 1) // n

        # Add 1/x to list of ans
        s = "1/" + str(x)
        UnitFactions.append(s);

        # Update fraction
        n = n * x - d;
        d = d * x
    return UnitFactions;

# Driver Code

# Given Input
n = 13;
d = 18;

# Function Call
res = FractionSplit(n, d);

# Print Answer
for s in res:
    print(s + ", ", end=" ");

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to split the fraction into
// distinct unit fraction
static List<string> FractionSplit(long n, long d)
{

    // To store answer
    List<string> UnitFactions = new List<string>();

    // While numerator is positive
    while (n > 0)
    {

        // Finding x = ceil(d/n)
        long x = (d + n - 1) / n;

        // Add 1/x to list of ans
        string s = "1/" + x.ToString();
        UnitFactions.Add(s);

        // Update fraction
        n = n * x - d;
        d = d * x;
    }
    return UnitFactions;
}

// Driver code
public static void Main(string[] args)
{

    // Given Input
    long n = 13, d = 18;

    // Function Call
    List<string> res = FractionSplit(n, d);

    // Print Answer
    foreach(string s in res)
        Console.Write(s + ", ");
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to split the fraction into
// distinct unit fraction
function FractionSplit(n, d) {

    // To store answer
    let UnitFactions = [];

    // While numerator is positive
    while (n > 0) {

        // Finding x = ceil(d/n)
        let x = Math.floor((d + n - 1) / n);

        // Add 1/x to list of ans
        let s = "1/" + String(x);
        UnitFactions.push(s);

        // Update fraction
        n = n * x - d;
        d = d * x;
    }
    return UnitFactions;
}

// Driver Code

// Given Input
let n = 13, d = 18;

// Function Call
let res = FractionSplit(n, d);

// Print Answer
for (let s of res)
    document.write(s + ", ");

// This code is contributed by gfgking.
</script>
```

**Output**

```
1/2, 1/5, 1/45, 
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)