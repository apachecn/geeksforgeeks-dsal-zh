# 求除 X^X 的最小数

> 原文:[https://www . geesforgeks . org/find-除以-xx 的最小数/](https://www.geeksforgeeks.org/find-the-smallest-number-that-divides-xx/)

给定一个数 **X** ，求大于 1 的最小数，除以**X<sup>X</sup>T5。在给定的问题中，总是假设 X 大于 1。
**举例:**** 

> **输入:** X = 6
> **输出:** 2
> **说明:** As，6 <sup>6</sup> 等于 46656，可被 2 整除，是其所有除数中最小的。
> **输入:** X = 3
> **输出:** 3
> **解释:** As，3 <sup>3</sup> 等于 27，可被 3 整除，是其所有除数中最小的。

**逼近:**
这个问题的主要观察是，如果一个数 **P** 除 **X** ，那么它也除**X<sup>X</sup>T10】，所以我们不需要计算**X<sup>X</sup>T14】的值。我们需要做的是找到除以 X 的最小数，它将永远是素数。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required smallest number
int SmallestDiv(int n)
{

    for (int i = 2; i * i <= n; i++) {
        // Finding smallest number that divides n
        if (n % i == 0) {

            // i divides n and return this
            // value immediately
            return i;
        }
    }

    // If n is a prime number then answer should be n,
    // As we can't take 1 as our answer.
    return n;
}

// Driver Code
int main()
{

    int X = 385;

    int ans = SmallestDiv(X);
    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG{

// Function to find the
// required smallest number
static int SmallestDiv(int n)
{
    for(int i = 2; i * i <= n; i++)
    {

       // Finding smallest number
       // that divides n
       if (n % i == 0)
       {

           // i divides n and return this
           // value immediately
           return i;
       }
    }

    // If n is a prime number then
    // answer should be n, as we
    // can't take 1 as our answer.
    return n;
}

// Driver Code
public static void main(String[] args)
{
    int X = 385;
    int ans = SmallestDiv(X);

    System.out.print(ans + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find the required smallest number
def SmallestDiv(n):

    i = 2
    while i * i <= n:

        # Finding smallest number that divides n
        if (n % i == 0):

            # i divides n and return this
            # value immediately
            return i
        i += 1

    # If n is a prime number then answer should be n,
    # As we can't take 1 as our answer.
    return n

# Driver Code
if __name__=="__main__":

    X = 385
    ans = SmallestDiv(X)

    print(ans)

# This code is contributed by Yash_R
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

// Function to find the
// required smallest number
static int SmallestDiv(int n)
{
    for(int i = 2; i * i <= n; i++)
    {

       // Finding smallest number
       // that divides n
       if (n % i == 0)
       {

           // i divides n and return this
           // value immediately
           return i;
       }
    }

    // If n is a prime number then
    // answer should be n, as we
    // can't take 1 as our answer.
    return n;
}

// Driver code
public static void Main(String[] args)
{
    int X = 385;
    int ans = SmallestDiv(X);

    Console.Write(ans + "\n");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to find the required smallest number
    function SmallestDiv(n)
    {

        for (let i = 2; i * i <= n; i++) {
            // Finding smallest number that divides n
            if (n % i == 0) {

                // i divides n and return this
                // value immediately
                return i;
            }
        }

        // If n is a prime number then answer should be n,
        // As we can't take 1 as our answer.
        return n;
    }

    let X = 385;

    let ans = SmallestDiv(X);
    document.write(ans + "</br>");

</script>
```

```
Output: 5
```

**时间复杂度:** O(sqrt(X))