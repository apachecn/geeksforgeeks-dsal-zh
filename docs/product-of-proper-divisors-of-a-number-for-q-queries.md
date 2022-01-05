# Q 查询的一个数的适当除数的乘积

> 原文:[https://www . geeksforgeeks . org/q 查询数约数产品/](https://www.geeksforgeeks.org/product-of-proper-divisors-of-a-number-for-q-queries/)

给定一个整数 **N，**任务是为 **Q** 查询找到模 10 <sup>9</sup> + 7 这个数的适当除数的乘积。

**示例:**

> **输入:** Q = 4，arr[] = { 4，6，8，16 }；
> **输出:** 2 6 8 64
> **解释:**
> 4 = > 1，2 = 1 * 2 = 2
> 6 = > 1，2，3 = 1 * 2 * 3 = 6
> 8 = > 1，2，4 = 1 * 2 * 4 = 8
> 16 = > 1，2，4，8 = 1 * 2 * 4 * 8 = 64
> 
> **输入:** arr[] = { 3，6，9，12 }
> **输出:** 1 6 3 144

**方法:**思路是借助厄拉多塞的[筛，预先计算并存储元素的适当除数的乘积。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
#define ll long long int
#define mod 1000000007

using namespace std;

vector<ll> ans(100002, 1);

// Function to precompute the product
// of proper divisors of a number at
// it's corresponding index
void preCompute()
{
    for (int i = 2; i <= 100000 / 2; i++) {
        for (int j = 2 * i; j <= 100000; j += i) {
            ans[j] = (ans[j] * i) % mod;
        }
    }
}

int productOfProperDivi(int num)
{

    // Returning the pre-computed
    // values
    return ans[num];
}

// Driver code
int main()
{
    preCompute();
    int queries = 5;
    int a[queries] = { 4, 6, 8, 16, 36 };

    for (int i = 0; i < queries; i++) {
        cout << productOfProperDivi(a[i])
             << ", ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG
{
    static final int mod = 1000000007;

    static long[] ans = new long[100002];

    // Function to precompute the product
    // of proper divisors of a number at
    // it's corresponding index
    static void preCompute()
    {
        for (int i = 2; i <= 100000 / 2; i++)
        {
            for (int j = 2 * i; j <= 100000; j += i)
            {
                ans[j] = (ans[j] * i) % mod;
            }
        }
    }

    static long productOfProperDivi(int num)
    {

        // Returning the pre-computed
        // values
        return ans[num];
    }

    // Driver code
    public static void main(String[] args)
    {
        Arrays.fill(ans, 1);
        preCompute();
        int queries = 5;
        int[] a = { 4, 6, 8, 16, 36 };

        for (int i = 0; i < queries; i++)
        {
            System.out.print(productOfProperDivi(a[i]) + ", ");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
mod = 1000000007

ans = [1] * (100002)

# Function to precompute the product
# of proper divisors of a number at
# it's corresponding index
def preCompute():

    for i in range(2, 100000 // 2 + 1):
        for j in range(2 * i, 100001, i):
            ans[j] = (ans[j] * i) % mod

def productOfProperDivi(num):

    # Returning the pre-computed
    # values
    return ans[num]

# Driver code
if __name__ == "__main__":

    preCompute()
    queries = 5
    a = [ 4, 6, 8, 16, 36 ]

    for i in range(queries):
        print(productOfProperDivi(a[i]), end = ", ")

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

static readonly int mod = 1000000007;

static long[] ans = new long[100002];

// Function to precompute the product
// of proper divisors of a number at
// it's corresponding index
static void preCompute()
{
    for(int i = 2; i <= 100000 / 2; i++)
    {
        for(int j = 2 * i; j <= 100000; j += i)
        {
            ans[j] = (ans[j] * i) % mod;
        }
    }
}

static long productOfProperDivi(int num)
{

    // Returning the pre-computed
    // values
    return ans[num];
}

// Driver code
public static void Main(String[] args)
{
    for(int i = 0 ; i < 100002; i++)
        ans[i] = 1;

    preCompute();

    int queries = 5;
    int[] a = { 4, 6, 8, 16, 36 };

    for(int i = 0; i < queries; i++)
    {
        Console.Write(productOfProperDivi(a[i]) + ", ");
    }
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

mod = 1000000007

ans = Array(100002).fill(1)

// Function to precompute the product
// of proper divisors of a number at
// it's corresponding index
function preCompute()
{
    for (var i = 2; i <= 100000 / 2; i++) {
        for (var j = 2 * i; j <= 100000; j += i) {
            ans[j] = (ans[j] * i) % mod;
        }
    }
}

function productOfProperDivi(num)
{

    // Returning the pre-computed
    // values
    return ans[num];
}

// Driver code
preCompute();
var queries = 5;
var a = [ 4, 6, 8, 16, 36 ];
for (var i = 0; i < queries; i++) {
    document.write( productOfProperDivi(a[i])
         + ", ");
}

</script>
```

**Output:** 

```
2, 6, 8, 64, 279936,
```