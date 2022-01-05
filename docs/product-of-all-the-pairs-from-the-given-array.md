# 给定数组中所有对的乘积

> 原文:[https://www . geeksforgeeks . org/给定阵列的所有配对产品/](https://www.geeksforgeeks.org/product-of-all-the-pairs-from-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从给定的数组中找出所有可能的对的乘积，例如:

*   **(arr[i]，arr[i])** 也被认为是有效对。
*   **(arr[i]、arr[j])** 和 **(arr[j]、arr[i])** 被认为是两个不同的对。

打印结果答案模数 10^9+7.

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 16
> **解释:**
> 所有有效对为(1，1)、(1，2)、(2，1)和(2，2)。
> 因此，1 * 1 * 1 * 2 * 2 * 1 * 2 * 2 = 16
> 
> **输入:** arr[] = {1，2，3}
> **输出:** 46656
> **解释:**
> 所有有效对为(1，1)，(1，2)，(1，3)，(2，1)，(2，2)，(2，3)，(3，1)，(3，2)和(3，3)。
> 因此该产品为 1 * 1 * 1 * * 2 * 1 * 3 * 2 * 1 * 2 * 2 * 2 * 3 * 3 * 1 * 3 * 2 * 3 * 3 = 46656

**天真方法:**解决上述问题的天真方法是找到所有可能的对，并计算每对元素的乘积。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// product of all the pairs from
// the given array

#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007

// Function to return the product of
// the elements of all possible pairs
// from the array
int productPairs(int arr[], int n)
{

    // To store the required product
    int product = 1;

    // Nested loop to calculate all
    // possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // Multiply the product of
            // the elements of the
            // current pair
            product *= (arr[i] % mod
                        * arr[j] % mod)
                       % mod;
            product = product % mod;
        }
    }

    // Return the final result
    return product % mod;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << productPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// product of all the pairs from
// the given array
import java.util.*;

class GFG{

static final int mod = 1000000007;

// Function to return the product of
// the elements of all possible pairs
// from the array
static int productPairs(int arr[], int n)
{

    // To store the required product
    int product = 1;

    // Nested loop to calculate all
    // possible pairs
    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < n; j++)
       {

          // Multiply the product
          // of the elements of the
          // current pair
          product *= (arr[i] % mod *
                      arr[j] % mod) % mod;
          product = product % mod;
       }
    }

    // Return the final result
    return product % mod;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    System.out.print(productPairs(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the
# product of all the pairs from
# the given array
mod = 1000000007;

# Function to return the product of
# the elements of all possible pairs
# from the array
def productPairs(arr, n):

    # To store the required product
    product = 1;

    # Nested loop to calculate all
    # possible pairs
    for i in range(n):
        for j in range(n):

            # Multiply the product
            # of the elements of the
            # current pair
            product *= (arr[i] % mod *
                        arr[j] % mod) % mod;
            product = product % mod;

    # Return the final result
    return product % mod;

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3];
    n = len(arr);

    print(productPairs(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to find the
// product of all the pairs from
// the given array
using System;
class GFG{

static readonly int mod = 1000000007;

// Function to return the product of
// the elements of all possible pairs
// from the array
static int productPairs(int []arr, int n)
{

    // To store the required product
    int product = 1;

    // Nested loop to calculate all
    // possible pairs
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Multiply the product
            // of the elements of the
            // current pair
            product *= (arr[i] % mod *
                        arr[j] % mod) % mod;
            product = product % mod;
        }
    }

    // Return the readonly result
    return product % mod;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3 };
    int n = arr.Length;

    Console.Write(productPairs(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

//Javascript implementation to find the
// product of all the pairs from
// the given array

mod = 1000000007

// Function to return the product of
// the elements of all possible pairs
// from the array
function productPairs(arr, n)
{

    // To store the required product
    let product = 1;

    // Nested loop to calculate all
    // possible pairs
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {

            // Multiply the product of
            // the elements of the
            // current pair
            product *= (arr[i] % mod
                        * arr[j] % mod)
                    % mod;
            product = product % mod;
        }
    }

    // Return the final result
    return product % mod;
}

// Driver code
    let arr = [ 1, 2, 3 ];

    let n = arr.length;

    document.write(productPairs(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 46656 

**时间复杂度:** *O(N <sup>2</sup> )*

**高效方法:**我们可以观察到，每个元素作为一对 **(X，Y)** 的元素之一，恰好出现 **(2 * N)** 次。正好 **N** 倍为 **X** ，正好 **N** 倍为 **Y** 。

下面是上述方法的实现:

## C++

```
// C++ implementation to Find the product
// of all the pairs from the given array
#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007
#define ll long long int

// Function to calculate
// (x^y)%1000000007
int power(int x, unsigned int y)
{
    int p = 1000000007;

    // Initialize result
    int res = 1;

    // Update x if it is more than
    // or equal to p
    x = x % p;

    while (y > 0) {
        // If y is odd, multiply x
        // with result
        if (y & 1)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }

    // Return the final result
    return res;
}

// Function to return the product
// of the elements of all possible
// pairs from the array
ll productPairs(ll arr[], ll n)
{

    // To store the required product
    ll product = 1;

    // Iterate for every element
    // of the array
    for (int i = 0; i < n; i++) {

        // Each element appears (2 * n) times
        product
            = (product
               % mod
               * (int)power(
                     arr[i], (2 * n))
               % mod)
              % mod;
    }

    return product % mod;
}

// Driver code
int main()
{
    ll arr[] = { 1, 2, 3 };
    ll n = sizeof(arr) / sizeof(arr[0]);

    cout << productPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find the product
// of all the pairs from the given array
import java.util.*;

class GFG{
static final int mod = 1000000007;

// Function to calculate
// (x^y)%1000000007
static int power(int x, int y)
{
    int p = 1000000007;

    // Initialize result
    int res = 1;

    // Update x if it is more than
    // or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if (y % 2 == 1)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }

    // Return the final result
    return res;
}

// Function to return the product
// of the elements of all possible
// pairs from the array
static int productPairs(int arr[], int n)
{

    // To store the required product
    int product = 1;

    // Iterate for every element
    // of the array
    for (int i = 0; i < n; i++)
    {

        // Each element appears (2 * n) times
        product = (product % mod *
                  (int)power(arr[i],
                            (2 * n)) % mod) % mod;
    }

    return product % mod;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    System.out.print(productPairs(arr, n));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to Find the product
# of all the pairs from the given array
mod = 1000000007

# Function to calculate
# (x^y)%1000000007
def power(x, y):

    p = 1000000007

    # Initialize result
    res = 1

    # Update x if it is more than
    # or equal to p
    x = x % p

    while (y > 0):

        # If y is odd, multiply x
        # with result
        if ((y & 1) != 0):
            res = (res * x) % p

        y = y >> 1
        x = (x * x) % p

    # Return the final result
    return res

# Function to return the product
# of the elements of all possible
# pairs from the array
def productPairs(arr, n):

    # To store the required product
    product = 1

    # Iterate for every element
    # of the array
    for i in range(n):

        # Each element appears (2 * n) times
        product = (product % mod *
          (int)(power(arr[i], (2 * n))) %
                            mod) % mod

    return (product % mod)

# Driver code
arr = [ 1, 2, 3 ]
n = len(arr)

print(productPairs(arr, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to Find the product
// of all the pairs from the given array
using System;
class GFG{
const int mod = 1000000007;

// Function to calculate
// (x^y)%1000000007
static int power(int x, int y)
{
    int p = 1000000007;

    // Initialize result
    int res = 1;

    // Update x if it is more than
    // or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if (y % 2 == 1)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }

    // Return the final result
    return res;
}

// Function to return the product
// of the elements of all possible
// pairs from the array
static int productPairs(int []arr, int n)
{

    // To store the required product
    int product = 1;

    // Iterate for every element
    // of the array
    for (int i = 0; i < n; i++)
    {

        // Each element appears (2 * n) times
        product = (product % mod *
                  (int)power(arr[i],
                            (2 * n)) % mod) % mod;
    }

    return product % mod;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 2, 3 };
    int n = arr.Length;

    Console.Write(productPairs(arr, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to Find the product
// of all the pairs from the given array

let mod = 1000000007;

// Function to calculate
// (x^y)%1000000007
function power(x, y)
{
    let p = 1000000007;

    // Initialize result
    let res = 1;

    // Update x if it is more than
    // or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if (y % 2 == 1)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }

    // Return the final result
    return res;
}

// Function to return the product
// of the elements of all possible
// pairs from the array
function productPairs(arr, n)
{

    // To store the required product
    let product = 1;

    // Iterate for every element
    // of the array
    for (let i = 0; i < n; i++)
    {

        // Each element appears (2 * n) times
        product = (product % mod *
                  power(arr[i],
                            (2 * n)) % mod) % mod;
    }

    return product % mod;
}

  // Driver Code

    let arr = [ 1, 2, 3 ];
    let n = arr.length;

    document.write(productPairs(arr, n));

</script>
```

**Output:** 46656 

**时间复杂度:**T2【O(N)T4】