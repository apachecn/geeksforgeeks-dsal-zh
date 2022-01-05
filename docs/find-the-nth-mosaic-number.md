# 找到第 n 个马赛克号

> 原文:[https://www.geeksforgeeks.org/find-the-nth-mosaic-number/](https://www.geeksforgeeks.org/find-the-nth-mosaic-number/)

给定一个整数 **N** ，任务是找到**N<sup>th</sup>T5[马赛克号](http://oeis.org/A000026)。一个马赛克号可以表示如下:
如果**N = A<sup>A</sup>* B<sup>B</sup>* C<sup>C</sup>…**其中 **A** ， **B** ， **C** ..是 **N** 的质因数，那么第 N 个马赛克号将是**A * A * B * B * C * C……**。**

**示例:**

> **输入:** N = 8
> **输出:** 6
> 8 可以表示为 2 <sup>3</sup> 。
> 所以，第 8 个<sup>马赛克号将是 2 * 3 = 6</sup>
> 
> **输入:** N = 36
> **输出:** 24
> 36 可表示为 2 <sup>2</sup> * 3 <sup>2</sup> 。
> 2 * 2 * 3 * 2 = 24

**方法:**我们必须通过将数除以因子，直到因子除以数，来找到数中所有的素因子以及因子的幂。第**号<sup>号</sup>号**镶嵌号将是已发现的主要因素及其力量的产物。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth mosaic number
int mosaic(int n)
{
    int i, ans = 1;

    // Iterate from 2 to the number
    for (i = 2; i <= n; i++) {

        // If i is the factor of n
        if (n % i == 0 && n > 0) {
            int count = 0;

            // Find the count where i^count
            // is a factor of n
            while (n % i == 0) {

                // Divide the number by i
                n /= i;

                // Increase the count
                count++;
            }

            // Multiply the answer with
            // count and i
            ans *= count * i;
        }
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    int n = 36;
    cout << mosaic(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the nth mosaic number
static int mosaic(int n)
{
    int i, ans = 1;

    // Iterate from 2 to the number
    for (i = 2; i <= n; i++)
    {

        // If i is the factor of n
        if (n % i == 0 && n > 0)
        {
            int count = 0;

            // Find the count where i^count
            // is a factor of n
            while (n % i == 0)
            {

                // Divide the number by i
                n /= i;

                // Increase the count
                count++;
            }

            // Multiply the answer with
            // count and i
            ans *= count * i;
        }
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main (String[] args)
{

    int n = 36;
    System.out.println (mosaic(n));
}
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the nth mosaic number
def mosaic(n):

    i=0
    ans = 1

    # Iterate from 2 to the number
    for i in range(2,n+1):

        # If i is the factor of n
        if (n % i == 0 and n > 0):
            count = 0

            # Find the count where i^count
            # is a factor of n
            while (n % i == 0):

                # Divide the number by i
                n //= i

                # Increase the count
                count+=1

            # Multiply the answer with
            # count and i
            ans *= count * i

    # Return the answer
    return ans

# Driver code

n = 36
print(mosaic(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the nth mosaic number
static int mosaic(int n)
{
    int i, ans = 1;

    // Iterate from 2 to the number
    for (i = 2; i <= n; i++)
    {

        // If i is the factor of n
        if (n % i == 0 && n > 0)
        {
            int count = 0;

            // Find the count where i^count
            // is a factor of n
            while (n % i == 0)
            {

                // Divide the number by i
                n /= i;

                // Increase the count
                count++;
            }

            // Multiply the answer with
            // count and i
            ans *= count * i;
        }
    }

    // Return the answer
    return ans;
}

// Driver code
static public void Main ()
{
    int n = 36;
    Console.WriteLine(mosaic(n));
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the nth mosaic number
function mosaic(n)
{
    let i, ans = 1;

    // Iterate from 2 to the number
    for(i = 2; i <= n; i++)
    {

        // If i is the factor of n
        if (n % i == 0 && n > 0)
        {
            let count = 0;

            // Find the count where i^count
            // is a factor of n
            while (n % i == 0)
            {

                // Divide the number by i
                n = parseInt(n / i, 10);

                // Increase the count
                count++;
            }

            // Multiply the answer with
            // count and i
            ans *= count * i;
        }
    }

    // Return the answer
    return ans;
}

// Driver code
let n = 36;
document.write(mosaic(n));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
24
```