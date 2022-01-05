# 一个 N 位数是回文的概率

> 原文:[https://www . geesforgeks . org/概率-a-n-数字-number-is-回文/](https://www.geeksforgeeks.org/probability-that-a-n-digit-number-is-palindrome/)

给定一个整数 **N** ，任务是找出一个数为 **N** 的数是回文的概率。
数字可能有前导零。
**例:**

> **输入:** N = 5
> **输出:** 1 / 100
> **输入:** N = 6
> **输出:** 1 / 1000

**解决方案:**

*   由于允许前导零，因此 **N** 位数的总数为**10<sup>N</sup>T5。**
*   当第一个 **N/2** 数字与最后一个 **N/2** 数字以相反的顺序匹配时，数字就是回文。
*   对于偶数位数，我们可以先选择 **N/2** 位，然后复制它们形成剩余的 **N/2** 位，这样我们就可以选择(N)/2 位。
*   对于奇数个数字，我们可以首先选择 **(N-1)/2** 个数字，然后复制它们以形成其余的 **(N-1)/2** 个数字，因此我们可以选择 **(N+1)/2** 个数字。
*   所以一个 **N** 数字是回文的概率是 **10 <sup>天花板(N / 2 )</sup> / 10 <sup>N</sup> 或者 1 / 10 <sup>地板(N / 2 )</sup>**

以下是实施办法:

## C++

```
// C++ code of above approach
#include <bits/stdc++.h>
using namespace std;

// Find the probability that a
// n digit number is palindrome
void solve(int n)
{
    int n_2 = n / 2;

    // Denominator
    string den;
    den = "1";

    // Assign 10^(floor(n/2)) to
    // denominator
    while (n_2--)
        den += '0';

    // Display the answer
    cout << 1 << "/" << den << "\n";
}

// Driver code
int main()
{

    int N = 5;

    solve(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code of above approach
import java.util.*;

class GFG
{

// Find the probability that a
// n digit number is palindrome
static void solve(int n)
{
    int n_2 = n / 2;

    // Denominator
    String den;
    den = "1";

    // Assign 10^(floor(n/2)) to
    // denominator
    while (n_2-- > 0)
        den += '0';

    // Display the answer
    System.out.println(1 + "/" + den);
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    solve(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code of above approach

# Find the probability that a
# n digit number is palindrome
def solve(n) :

    n_2 = n // 2;

    # Denominator
    den = "1";

    # Assign 10^(floor(n/2)) to
    # denominator
    while (n_2) :
        den += '0';

        n_2 -= 1

    # Display the answer
    print(str(1) + "/" + str(den))

# Driver code
if __name__ == "__main__" :

    N = 5;

    solve(N);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Find the probability that a
// n digit number is palindrome
static void solve(int n)
{
    int n_2 = n / 2;

    // Denominator
    String den;
    den = "1";

    // Assign 10^(floor(n/2)) to
    // denominator
    while (n_2-- > 0)
        den += '0';

    // Display the answer
    Console.WriteLine(1 + "/" + den);
}

// Driver code
public static void Main(String[] args)
{
    int N = 5;

    solve(N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Find the probability that a
    // n digit number is palindrome
    function solve(n)
    {
        let n_2 = parseInt(n / 2, 10);

        // Denominator
        let den;
        den = "1";

        // Assign 10^(floor(n/2)) to
        // denominator
        while (n_2-- > 0)
            den += '0';

        // Display the answer
        document.write(1 + "/" + den + "</br>");
    }

    let N = 5;

    solve(N);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
1/100
```