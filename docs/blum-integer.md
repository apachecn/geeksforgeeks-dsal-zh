# 【Blum 整数】

> 原文:[https://www.geeksforgeeks.org/blum-integer/](https://www.geeksforgeeks.org/blum-integer/)

[Blum Integer](https://en.wikipedia.org/wiki/Blum_integer) 是一个[半素数](https://en.wikipedia.org/wiki/Semiprime)数，假设 p 和 q 是两个因子(即 n = p * q)，它们(p 和 q)的形式为 4t + 3，其中 t 是某个整数。
前几个 Blum 整数是 21，33，57，69，77，93，129，133，141，161，177，…

**注:**由于两个因子都应该是半素数的条件，偶数不能是 Blum 整数，20 以下的数字也不能是，
所以我们只要查一个大于 20 的奇数是不是 Blum 整数就可以了。

**示例:**

```
Input: 33
Output: Yes
Explanation: 33 = 3 * 11, 3 and 11 are both 
semi-primes as well as of the form 4t + 3 
for t = 0, 2

Input: 77
Output:  Yes
Explanation: 77 = 7 * 11, 7 and 11 both are 
semi-prime as well as of the form 4t + 3 
for t = 1, 2

Input: 25
Output: No
Explanation: 25 = 5*5, 5 and 5 are both 
semi-prime  but are not of the form 4t 
+ 3, Hence 25 is not a Blum integer.
```

**方法:**对于给定的大于 20 的奇数，我们计算从 1 到该奇数的素数。如果我们找到任何一个素数，它除了那个奇整数，它的商都是质数，对于某个整数遵循 4t + 3 的形式，那么给定的奇整数就是 Blum Integer。

下面是上述方法的实现:

## C++

```
// CPP program to check if a number is a Blum
// integer
#include <bits/stdc++.h>
using namespace std;

// Function to cheek if number is Blum Integer
bool isBlumInteger(int n)
{
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    // to store prime numbers from 2 to n
    for (int i = 2; i * i <= n; i++) {

        // If prime[i] is not
        // changed, then it is a prime
        if (prime[i] == true) {

            // Update all multiples of p
            for (int j = i * 2; j <= n; j += i)
                prime[j] = false;
        }
    }

    // to check if the given odd integer
    // is Blum Integer or not
    for (int i = 2; i <= n; i++) {
        if (prime[i]) {

            // checking the factors
            // are of 4t+3 form or not
            if ((n % i == 0) && ((i - 3) % 4) == 0) {
                int q = n / i;
                return (q != i && prime[q] &&
                           (q - 3) % 4 == 0);
            }
        }
    }

    return false;
}

// driver code
int main()
{
    // give odd integer greater than 20
    int n = 249;

    if (isBlumInteger(n))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check If
// a number is a Blum integer
import java.util.*;
class GFG {
    public static boolean isBlumInteger(int n)
    {
        boolean prime[] = new boolean[n + 1];
        for (int i = 0; i < n; i++)
            prime[i] = true;

        // to store prime numbers from 2 to n
        for (int i = 2; i * i <= n; i++) {

            // If prime[i] is not changed,
            // then it is a prime
            if (prime[i] == true) {

                // Update all multiples of p
                for (int j = i * 2; j <= n; j += i)
                    prime[j] = false;
            }
        }

        // to check if the given odd integer
        // is Blum Integer or not
        for (int i = 2; i <= n; i++) {
            if (prime[i]) {

                // checking the factors are
                // of 4t + 3 form or not
                if ((n % i == 0) && ((i - 3) % 4) == 0) {
                    int q = n / i;
                    return (q != i && prime[q] &&
                            (q - 3) % 4 == 0);
                }
            }
        }
        return false;
    }

    // driver code
    public static void main(String[] args)
    {
        // give odd integer greater than 20
        int n = 249;

        if (isBlumInteger(n) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# python 3 program to check if a
# number is a Blum integer

# Function to cheek if number
# is Blum Integer
def isBlumInteger(n):

    prime = [True]*(n + 1)

    # to store prime numbers from 2 to n
    i = 2
    while (i * i <= n):

        # If prime[i] is not
        # changed, then it is a prime
        if (prime[i] == True) :

            # Update all multiples of p
            for j in range(i * 2, n + 1, i):
                prime[j] = False
        i = i + 1

    # to check if the given odd integer
    # is Blum Integer or not
    for i in range(2, n + 1) :
        if (prime[i]) :

            # checking the factors
            # are of 4t+3 form or not
            if ((n % i == 0) and
                        ((i - 3) % 4) == 0):
                q = int(n / i)
                return (q != i and prime[q]
                       and (q - 3) % 4 == 0)

    return False

# driver code
# give odd integer greater than 20
n = 249
if (isBlumInteger(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha.
```

## C#

```
// C# implementation to check If
// a number is a Blum integer
using System;

class GFG {

    public static bool isBlumInteger(int n)
    {
        bool[] prime = new bool[n + 1];
        for (int i = 0; i < n; i++)
            prime[i] = true;

        // to store prime numbers from 2 to n
        for (int i = 2; i * i <= n; i++) {

            // If prime[i] is not changed,
            // then it is a prime
            if (prime[i] == true) {

                // Update all multiples of p
                for (int j = i * 2; j <= n; j += i)
                    prime[j] = false;
            }
        }

        // to check if the given odd integer
        // is Blum Integer or not
        for (int i = 2; i <= n; i++) {
            if (prime[i]) {

                // checking the factors are
                // of 4t + 3 form or not
                if ((n % i == 0) && ((i - 3) % 4) == 0)
                {
                    int q = n / i;
                    return (q != i && prime[q] &&
                           (q - 3) % 4 == 0);
                }
            }
        }
        return false;
    }

    // Driver code
    static public void Main ()
    {
        // give odd integer greater than 20
        int n = 249;

        if (isBlumInteger(n) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// number is a Blum integer

// Function to cheek if
// number is Blum Integer
function isBlumInteger($n)
{
    $prime = array_fill(0, $n + 1, true);

    // to store prime
    // numbers from 2 to n
    for ($i = 2; $i * $i <= $n; $i++)
    {

        // If prime[i] is not
        // changed, then it is a prime
        if ($prime[$i] == true)
        {

            // Update all multiples of p
            for ($j = $i * 2; $j <= $n; $j += $i)
                $prime[$j] = false;
        }
    }

    // to check if the given
    // odd integer is Blum
    // Integer or not
    for ($i = 2; $i <= $n; $i++)
    {
        if ($prime[$i])
        {

            // checking the factors
            // are of 4t+3 form or not
            if (($n % $i == 0) &&
               (($i - 3) % 4) == 0)
            {
                $q = (int)$n / $i;
                return ($q != $i && $prime[$q] &&
                             ($q - 3) % 4 == 0);
            }
        }
    }

    return false;
}

// Driver code

// give odd integer
// greater than 20
$n = 249;

if (isBlumInteger($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to check If
// a number is a Blum integer
function isBlumInteger(n)
{
    let prime = new Array(n + 1);
    for(let i = 0; i < n; i++)
        prime[i] = true;

    // To store prime numbers from 2 to n
    for(let i = 2; i * i <= n; i++)
    {

        // If prime[i] is not changed,
        // then it is a prime
        if (prime[i] == true)
        {

            // Update all multiples of p
            for(let j = i * 2; j <= n; j += i)
                prime[j] = false;
        }
    }

    // To check if the given odd integer
    // is Blum Integer or not
    for(let i = 2; i <= n; i++)
    {
        if (prime[i])
        {

            // Checking the factors are
            // of 4t + 3 form or not
            if ((n % i == 0) && ((i - 3) % 4) == 0)
            {
                let q = parseInt(n / i, 10);
                return (q != i && prime[q] &&
                       (q - 3) % 4 == 0);
            }
        }
    }
    return false;
}

// Driver code

// Give odd integer greater than 20
let n = 249;

if (isBlumInteger(n) == true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by decode2207

</script>
```

**Output:** 

```
Yes
```