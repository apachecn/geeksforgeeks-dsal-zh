# 仅由 N 的除数形成的所有子集的乘积之和

> 原文:[https://www . geeksforgeeks . org/所有子集的乘积之和-仅由 n 的除数形成/](https://www.geeksforgeeks.org/sum-of-product-of-all-subsets-formed-by-only-divisors-of-n/)

给定一个数 **N** ，任务是求所有可能子集的元素乘积之和，这些子集仅由 **N** 的除数构成。
**例:**

> **输入:** N = 3
> **输出:** 7
> **说明:**
> 3 的除数是 1 和 3。所有可能的子集都是{1}、{3}、{1，3}。
> 因此，所有可能子集的乘积之和为:
> (1 + 3 + (1 * 3)) = 7。
> **输入:** N = 4
> **输出:** 29
> **说明:**
> 4 的除数为 1、2、4。所有可能的子集都是{1}、{2}、{4}、{1，2}、{1，4}、{2，4}、{1，2，4}。
> 因此，所有可能子集乘积的和为:
> (1+2+4+(1 * 2)+(1 * 4)+(2 * 4)+(1 * 2 * 4))= 29。

**天真方法:**这个问题的天真方法是[从其除数生成所有可能的子集](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)，然后计算每个子集的乘积。计算每个子集的乘积后，将所有乘积相加，找到所需的答案。这种方法的时间复杂度是 **O(2 <sup>D</sup> )** ，其中 D 是 n 的除数
**高效方法:**高效方法背后的思想来自以下观察:

```
Let x and y is the divisor of N. 
Then sum of product of all subsets will be
   = x + y + x * y 
   = x(1 + y) + y + 1 - 1 
   = x(1 + y) + (1 + y) - 1 
   = (x + 1) * (y + 1) - 1
   = (1 + x) * (1 + y) - 1

Now let take three divisors x, y, z. 
Then sum of product of all subsets will be
   = x + y + z + xy + yz + zx + xyz 
   = x + xz + y + yz + xy + xyz + z + 1 - 1
   = x(1 + z) + y(1 + z) + xy(1 + z) + z + 1 - 1
   = (x + y + xy + 1) * (1 + z) - 1 
   = (1 + x) * (1 + y) * (1 + z) - 1
```

显然，从上面的观察，我们可以得出结论，如果 **{D <sub>1</sub> ，D <sub>2</sub> ，D <sub>3</sub> ，… D <sub>n</sub> }** 是 N 的除数，那么要求的答案将是:

```
(D1 + 1) * (D2 + 1) * (D3 + 1) * ... (Dn + 1)
```

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of
// product of all the subsets
// formed by only divisors of N

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of
// product of all the subsets
// formed by only divisors of N
int GetSum(int n)
{

    // Vector to store all the
    // divisors of n
    vector<int> divisors;

    // Loop to find out the
    // divisors of N
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {

            // Both 'i' and 'n/i' are the
            // divisors of n
            divisors.push_back(i);

            // Check if 'i' and 'n/i' are
            // equal or not
            if (i != n / i) {
                divisors.push_back(n / i);
            }
        }
    }

    int ans = 1;

    // Calculating the answer
    for (auto i : divisors) {
        ans *= (i + 1);
    }

    // Excluding the value
    // of the empty set
    ans = ans - 1;

    return ans;
}

// Driver Code
int main()
{

    int N = 4;

    cout << GetSum(N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of product
// of all the subsets formed by only
// divisors of N
import java.util.*;
class GFG {

// Function to find the sum of product
// of all the subsets formed by only
// divisors of N
static int GetSum(int n)
{

    // Vector to store all the
    // divisors of n
    Vector<Integer> divisors = new Vector<Integer>(); 

    // Loop to find out the
    // divisors of N
    for(int i = 1; i * i <= n; i++)
    {
       if (n % i == 0)
       {

           // Both 'i' and 'n/i' are the
           // divisors of n
           divisors.add(i);

           // Check if 'i' and 'n/i' are
           // equal or not
           if (i != n / i)
           {
               divisors.add(n / i);
           }
       }
    }

    int ans = 1;

    // Calculating the answer
    for(int i = 0; i < divisors.size(); i++)
    {
       ans *= (divisors.get(i) + 1);
    }

    // Excluding the value
    // of the empty set
    ans = ans - 1;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    System.out.println(GetSum(N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# product of all the subsets
# formed by only divisors of N

# Function to find the sum of
# product of all the subsets
# formed by only divisors of N
def GetSum(n):

    # Vector to store all the
    # divisors of n
    divisors = []

    # Loop to find out the
    # divisors of N
    i = 1
    while i * i <= n :
        if (n % i == 0):

            # Both 'i' and 'n/i' are the
            # divisors of n
            divisors.append(i)

            # Check if 'i' and 'n/i' are
            # equal or not
            if (i != n // i):
                divisors.append(n // i)

        i += 1
    ans = 1

    # Calculating the answer
    for i in divisors:
        ans *= (i + 1)

    # Excluding the value
    # of the empty set
    ans = ans - 1
    return ans

# Driver Code
if __name__ == "__main__":

    N = 4
    print(GetSum(N))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the sum of product
// of all the subsets formed by only
// divisors of N
using System;
using System.Collections.Generic;

class GFG{

// Function to find the sum of product
// of all the subsets formed by only
// divisors of N
static int GetSum(int n)
{

    // Store all the
    // divisors of n
    List<int> divisors = new List<int>();

    // Loop to find out the
    // divisors of N
    for(int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {

            // Both 'i' and 'n/i' are the
            // divisors of n
            divisors.Add(i);

            // Check if 'i' and 'n/i' are
            // equal or not
            if (i != n / i)
            {
                divisors.Add(n / i);
            }
        }
    }

    int ans = 1;

    // Calculating the answer
    foreach(int i in divisors)
    {
        ans *= (i + 1);
    }

    // Excluding the value
    // of the empty set
    ans = ans - 1;

    return ans;
}

// Driver code
public static void Main()
{
    int N = 4;

    Console.WriteLine(GetSum(N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to find the sum of
// product of all the subsets
// formed by only divisors of N

// Function to find the sum of
// product of all the subsets
// formed by only divisors of N
function GetSum(n)
{

    // Vector to store all the
    // divisors of n
    var divisors = [];

    // Loop to find out the
    // divisors of N
    for (var i = 1; i * i <= n; i++) {
        if (n % i == 0) {

            // Both 'i' and 'n/i' are the
            // divisors of n
            divisors.push(i);

            // Check if 'i' and 'n/i' are
            // equal or not
            if (i != n / i) {
                divisors.push(n / i);
            }
        }
    }

    var ans = 1;

    // Calculating the answer
    for(var i =0; i< divisors.length; i++)
    {
        ans *= (divisors[i]+1);
    }

    // Excluding the value
    // of the empty set
    ans = ans - 1;

    return ans;
}

// Driver Code
var N = 4;
document.write( GetSum(N));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
29
```

**时间复杂度:** *O(sqrt(N))* ，其中 N 为给定数。

**辅助空间:** O(sqrt(N))