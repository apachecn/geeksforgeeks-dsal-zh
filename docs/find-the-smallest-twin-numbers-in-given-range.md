# 找出给定范围内最小的双胞胎

> 原文:[https://www . geesforgeks . org/find-给定范围内最小的双数/](https://www.geeksforgeeks.org/find-the-smallest-twin-numbers-in-given-range/)

给定范围[低]..高]，打印给定范围(包括低和高)内最小的孪生数。两个数是孪生的，如果它们是素数，差是 2。

**示例:**

```
Input:  low = 10,  high = 100
Output: Smallest twins in given range: (11, 13)
Both 11 and 13 are prime numbers and difference 
between them is two, therefore twins.  And these
are the smallest twins in [10..100]

Input:  low = 50,  high = 100
Output: Smallest twins in given range: (59, 61) 
```

一个**简单的解决方法**是从低开始，对于每个数字 x，检查 x 和 x + 2 是否是素数。这里 x 从低到高不等-2。

一个**有效的解决方案**是使用厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

```
1) Create a boolean array "prime[0..high]" and initialize all 
   entries in it as true. A value in prime[i] will finally 
   be false if i is not a prime number, else true.

2) Run a loop from p = 2 to high. 
    a) If prime[p] is true, then p is prime. [See this]
    b) Mark all multiples of p as not prime in prime[]. 

3) Run a loop from low to high and print the first twins
   using prime[] built in step 2\.   
```

以下是上述想法的实现。

## C++

```
// C++ program to find the smallest twin in given range
#include <bits/stdc++.h>
using namespace std;

void printTwins(int low, int high)
{
    // Create a boolean array "prime[0..high]" and initialize
    // all entries it as true. A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    bool prime[high+1], twin = false;
    memset(prime, true, sizeof(prime));

    prime[0] = prime[1] = false;

    // Look for the smallest twin
    for (int p=2; p<=floor(sqrt(high))+1; p++)
    {
        // If p is not marked, then it is a prime
        if (prime[p])
        {
            // Update all multiples of p
            for (int i=p*2; i<=high; i += p)
                prime[i] = false;
        }
    }

    // Now print the smallest twin in range
    for (int i=low; i<=high; i++)
    {
        if (prime[i] && prime[i+2])
        {
            cout << "Smallest twins in given range: ("
                << i << ", " << i+2 << ")";
            twin = true;
            break;
        }
    }

    if (twin == false)
      cout << "No such pair exists" <<endl;
}

// Driver program
int main()
{
    printTwins(10, 100);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest twin in given range

class GFG {

    static void printTwins(int low, int high) {
        // Create a boolean array "prime[0..high]" and initialize
        // all entries it as true. A value in prime[i] will finally
        // be false if i is Not a prime, else true.
        boolean prime[] = new boolean[high + 1], twin = false;
        for (int i = 0; i < prime.length; i++) {
            prime[i] = true;
        }

        prime[0] = prime[1] = false;

        // Look for the smallest twin
        for (int p = 2; p <= Math.floor(Math.sqrt(high)) + 1; p++) {
            // If p is not marked, then it is a prime
            if (prime[p]) {
                // Update all multiples of p
                for (int i = p * 2; i <= high; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Now print the smallest twin in range
        for (int i = low; i <= high; i++) {
            if (prime[i] && prime[i + 2]) {
                int a = i + 2 ;
                System.out.print("Smallest twins in given range: ("
                        + i + ", " + a + ")");
                twin = true;
                break;
            }
        }

        if (twin == false) {
            System.out.println("No such pair exists");
        }
    }

// Driver program
    public static void main(String[] args) {

        printTwins(10, 100);
    }
}
// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# twin in given range
import math

def printTwins(low, high):

    # Create a boolean array "prime[0..high]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True] * (high + 1);
    twin = False;

    prime[0] = prime[1] = False;

    # Look for the smallest twin
    for p in range(2, int(math.floor(
                          math.sqrt(high)) + 2)):

        # If p is not marked, then it
        # is a prime
        if (prime[p]):

            # Update all multiples of p
            for i in range(p * 2, high + 1, p):
                prime[i] = False;

    # Now print the smallest twin in range
    for i in range(low, high + 1):
        if (prime[i] and prime[i + 2]):
            print("Smallest twins in given range: (",
                               i, ",", (i + 2), ")");
            twin = True;
            break;

    if (twin == False):
        print("No such pair exists");

# Driver Code
printTwins(10, 100);

# This code is contributed
# by chandan_jnu
```

## C#

```

// C# program to find the smallest twin in given range

using System;
public class GFG {

    static void printTwins(int low, int high) {
        // Create a boolean array "prime[0..high]" and initialize
        // all entries it as true. A value in prime[i] will finally
        // be false if i is Not a prime, else true.
        bool []prime = new bool[high + 1]; bool twin = false;
        for (int i = 0; i < prime.Length; i++) {
            prime[i] = true;
        }

        prime[0] = prime[1] = false;

        // Look for the smallest twin
        for (int p = 2; p <= Math.Floor(Math.Sqrt(high)) + 1; p++) {
            // If p is not marked, then it is a prime
            if (prime[p]) {
                // Update all multiples of p
                for (int i = p * 2; i <= high; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Now print the smallest twin in range
        for (int i = low; i <= high; i++) {
            if (prime[i] && prime[i + 2]) {
                int a = i + 2 ;
                Console.Write("Smallest twins in given range: ("
                        + i + ", " + a + ")");
                twin = true;
                break;
            }
        }

        if (twin == false) {
            Console.WriteLine("No such pair exists");
        }
    }

// Driver program
    public static void Main() {

        printTwins(10, 100);
    }
}
//this code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the smallest
// twin in given range

function printTwins($low, $high)
{
    // Create a boolean array "prime[0..high]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    $prime = array_fill(0, $high + 1, true);
    $twin = false;

    $prime[0] = $prime[1] = false;

    // Look for the smallest twin
    for ($p = 2; $p <= floor(sqrt($high)) + 1; $p++)
    {
        // If p is not marked, then it is a prime
        if ($prime[$p])
        {
            // Update all multiples of p
            for ($i = $p * 2; $i <= $high; $i += $p)
                $prime[$i] = false;
        }
    }

    // Now print the smallest twin in range
    for ($i = $low; $i <= $high; $i++)
    {
        if ($prime[$i] && $prime[$i + 2])
        {
            print("Smallest twins in given range: ($i, ".
                                          ($i + 2). ")");
            $twin = true;
            break;
        }
    }

    if ($twin == false)
    print("No such pair exists\n");
}

// Driver Code
printTwins(10, 100);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// smallest twin in given range
function printTwins(low, high)
{

    // Create a boolean array "prime[0..high]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    var prime = Array.from({length: high + 1}, (_, i) => 0);
    var twin = false;
    for(i = 0; i < prime.length; i++)
    {
        prime[i] = true;
    }

    prime[0] = prime[1] = false;

    // Look for the smallest twin
    for(p = 2;
        p <= Math.floor(Math.sqrt(high)) + 1;
        p++)
    {

        // If p is not marked, then it is a prime
        if (prime[p])
        {

            // Update all multiples of p
            for(i = p * 2; i <= high; i += p)
            {
                prime[i] = false;
            }
        }
    }

    // Now print the smallest twin in range
    for(i = low; i <= high; i++)
    {
        if (prime[i] && prime[i + 2])
        {
            var a = i + 2 ;
            document.write("Smallest twins in " +
                           "given range: (" + i +
                           ", " + a + ")");
            twin = true;
            break;
        }
    }

    if (twin == false)
    {
        document.write("No such pair exists");
    }
}

// Driver code
printTwins(10, 100);

// This code is contributed by shikhasingrajput

</script>
```

**Output:** 

```
Smallest twins in given range: (11, 13)
```

感谢乌卡什·特里维迪提出这个解决方案。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。