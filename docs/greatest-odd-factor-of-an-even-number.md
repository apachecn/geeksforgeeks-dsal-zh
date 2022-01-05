# 偶数的最大奇数因子

> 原文:[https://www . geesforgeks . org/最大奇数因子/偶数/](https://www.geeksforgeeks.org/greatest-odd-factor-of-an-even-number/)

给定一个偶数 **N** ，任务是找到 **N** 最大可能的奇数因子。

示例:

> **输入:** N = 8642
> **输出:** 4321
> **说明:**
> 这里，8642 的因子为{1，8642，2，4321，29，298，58，149}，其中奇数因子为{1，4321，29，149}，所有奇数因子中最大的奇数因子为 4321。
> 
> **输入:** N = 100
> **输出:** 25
> **说明:**
> 这里，100 的因子是{1，100，2，50，4，25，5，20，10}，其中奇数因子是{1，25，5}，所有奇数因子中最大的奇数因子是 25。

**天真法:**天真法是[找出 N](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 的所有因子，然后从中选出最大的奇因子。
**时间复杂度:** O(sqrt(N))

**有效方法:**这个问题的有效方法是观察每个偶数 **N** 可以表示为:

```
N = 2i*odd_number
```

因此，为了得到最大的奇数，我们需要将给定的数 **N** 除以 **2** ，直到 **N** 成为奇数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print greatest odd factor
int greatestOddFactor(int n)
{
    int pow_2 = (int)(log(n));

    // Initialize i with 1
    int i = 1;

    // Iterate till i <= pow_2
    while (i <= pow_2)
    {

        // Find the pow(2, i)
        int fac_2 = (2 * i);
        if (n % fac_2 == 0)
        {
            // If factor is odd, then
            // print the number and break
            if ((n / fac_2) % 2 == 1)
            {
                return (n / fac_2);
            }
        }

        i += 1;
    }
}

// Driver Code
int main()
{

    // Given Number
    int N = 8642;

    // Function Call
    cout << greatestOddFactor(N);
    return 0;
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to print greatest odd factor
public static int greatestOddFactor(int n)
{
    int pow_2 = (int)(Math.log(n));

    // Initialize i with 1
    int i = 1;

    // Iterate till i <= pow_2
    while (i <= pow_2)
    {

        // Find the pow(2, i)
        int fac_2 = (2 * i);
        if (n % fac_2 == 0)
        {

            // If factor is odd, then
            // print the number and break
            if ((n / fac_2) % 2 == 1)
            {
                return (n / fac_2);
            }
        }
        i += 1;
    }
    return 0;
}

// Driver code
public static void main(String[] args)
{

    // Given Number
    int N = 8642;

    // Function Call
    System.out.println(greatestOddFactor(N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# importing Maths library
import math

# Function to print greatest odd factor
def greatestOddFactor(n):

  pow_2 = int(math.log(n, 2))

# Initialize i with 1
  i = 1

# Iterate till i <= pow_2
  while i <= pow_2:

# find the pow(2, i)
    fac_2 = (2**i)

    if (n % fac_2 == 0) :

      # If factor is odd, then print the
      # number and break
      if ( (n // fac_2) % 2 == 1):
        print(n // fac_2)
        break

    i += 1

# Driver Code

# Given Number
N = 8642

# Function Call
greatestOddFactor(N)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print greatest odd factor
public static int greatestOddFactor(int n)
{
    int pow_2 = (int)(Math.Log(n));

    // Initialize i with 1
    int i = 1;

    // Iterate till i <= pow_2
    while (i <= pow_2)
    {

        // Find the pow(2, i)
        int fac_2 = (2 * i);
        if (n % fac_2 == 0)
        {

            // If factor is odd, then
            // print the number and break
            if ((n / fac_2) % 2 == 1)
            {
                return (n / fac_2);
            }
        }
        i += 1;
    }
    return 0;
}

// Driver code
public static void Main(String[] args)
{

    // Given number
    int N = 8642;

    // Function call
    Console.WriteLine(greatestOddFactor(N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print greatest odd factor
function greatestOddFactor(n)
{
    let pow_2 = (Math.log(n));

    // Initialize i with 1
    let i = 1;

    // Iterate till i <= pow_2
    while (i <= pow_2)
    {

        // Find the pow(2, i)
        let fac_2 = (2 * i);
        if (n % fac_2 == 0)
        {

            // If factor is odd, then
            // print the number and break
            if ((n / fac_2) % 2 == 1)
            {
                return (n / fac_2);
            }
        }
        i += 1;
    }
    return 0;
}

// Driver Code

    // Given Number
    let N = 8642;

    // Function Call
    document.write(greatestOddFactor(N)); ;

</script>
```

**Output:** 

```
4321
```

**时间复杂度:** *O(log2(N))*