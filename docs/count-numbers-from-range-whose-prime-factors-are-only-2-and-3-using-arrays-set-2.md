# 使用数组|集合 2

从质因数只有 2 和 3 的范围中计数数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-from-from-thin-prime-factors-only-2-and-3-use-array-set-2/](https://www.geeksforgeeks.org/count-numbers-from-range-whose-prime-factors-are-only-2-and-3-using-arrays-set-2/)

给定两个正整数 **L 和 R** ，任务是计算范围**【L，R】**中的元素，其**素因子只有 2 和 3** 。
**举例:**

> **输入:** L = 1，R = 10
> **输出:** 6
> **说明:**
> 2 = 2
> 3 = 3
> 4 = 2 * 2
> 6 = 2 * 3
> 8 = 2 * 2 * 2
> 9 = 3 * 3
> **输入:** L = 100，R = 200
> **输出:** 5

更简单的方法，参考[从质因数只有 2 和 3 的范围内计数](https://www.geeksforgeeks.org/count-numbers-from-range-whose-prime-factors-are-only-2-and-3/)。
**方法:**
要优化解决问题，请遵循以下步骤:

*   [将 2](https://www.geeksforgeeks.org/powers-2-required-sum/) 的所有**小于等于 R** 的幂存储在一个数组**幂 2【】**中。
*   同样，将所有小于或等于 R 的 3 的幂**存储在另一个数组**幂 3【】**中。**
*   初始化第三个数组 **power23[]** ，并存储 **power2[]** 的每个元素与小于或等于 **R** 的 **power3[]** 的每个元素的成对乘积。
*   现在对于任何范围**【L，R】**，我们将简单地迭代数组**power 23【】**并计算范围**【L，R】**中的数字。

以下是上述方法的实现:

## C++

```
// C++ program to count the elements
// in the range [L, R] whose prime
// factors are only 2 and 3.

#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function which will calculate the
// elements in the given range
void calc_ans(ll l, ll r)
{

    vector<ll> power2, power3;

    // Store the current power of 2
    ll mul2 = 1;
    while (mul2 <= r) {
        power2.push_back(mul2);
        mul2 *= 2;
    }

    // Store the current power of 3
    ll mul3 = 1;
    while (mul3 <= r) {
        power3.push_back(mul3);
        mul3 *= 3;
    }

    // power23[] will store pairwise product of
    // elements of power2 and power3 that are <=r
    vector<ll> power23;

    for (int x = 0; x < power2.size(); x++) {
        for (int y = 0; y < power3.size(); y++) {

            ll mul = power2[x] * power3[y];
            if (mul == 1)
                continue;

            // Insert in power23][]
            // only if mul<=r
            if (mul <= r)
                power23.push_back(mul);
        }
    }

    // Store the required answer
    ll ans = 0;
    for (ll x : power23) {
        if (x >= l && x <= r)
            ans++;
    }

    // Print the result
    cout << ans << endl;
}

// Driver code
int main()
{

    ll l = 1, r = 10;

    calc_ans(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the elements
// in the range [L, R] whose prime
// factors are only 2 and 3.
import java.util.*;
class GFG{

// Function which will calculate the
// elements in the given range
static void calc_ans(int l, int r)
{

    Vector<Integer> power2 = new Vector<Integer>(),
                    power3 = new Vector<Integer>();

    // Store the current power of 2
    int mul2 = 1;
    while (mul2 <= r)
    {
        power2.add(mul2);
        mul2 *= 2;
    }

    // Store the current power of 3
    int mul3 = 1;
    while (mul3 <= r)
    {
        power3.add(mul3);
        mul3 *= 3;
    }

    // power23[] will store pairwise product of
    // elements of power2 and power3 that are <=r
    Vector<Integer> power23 = new Vector<Integer>();

    for (int x = 0; x < power2.size(); x++)
    {
        for (int y = 0; y < power3.size(); y++)
        {
            int mul = power2.get(x) *
                      power3.get(y);
            if (mul == 1)
                continue;

            // Insert in power23][]
            // only if mul<=r
            if (mul <= r)
                power23.add(mul);
        }
    }

    // Store the required answer
    int ans = 0;
    for (int x : power23)
    {
        if (x >= l && x <= r)
            ans++;
    }

    // Print the result
    System.out.print(ans + "\n");
}

// Driver code
public static void main(String[] args)
{
    int l = 1, r = 10;

    calc_ans(l, r);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count the elements
# in the range [L, R] whose prime
# factors are only 2 and 3.

# Function which will calculate the
# elements in the given range
def calc_ans(l, r):

    power2 = []; power3 = [];

    # Store the current power of 2
    mul2 = 1;
    while (mul2 <= r):
        power2.append(mul2);
        mul2 *= 2;

    # Store the current power of 3
    mul3 = 1;
    while (mul3 <= r):
        power3.append(mul3);
        mul3 *= 3;

    # power23[] will store pairwise
    # product of elements of power2
    # and power3 that are <=r
    power23 = [];

    for x in range(len(power2)):
        for y in range(len(power3)):

            mul = power2[x] * power3[y];
            if (mul == 1):
                continue;

            # Insert in power23][]
            # only if mul<=r
            if (mul <= r):
                power23.append(mul);

    # Store the required answer
    ans = 0;
    for x in power23:
        if (x >= l and x <= r):
            ans += 1;

    # Print the result
    print(ans);

# Driver code
if __name__ == "__main__":

    l = 1; r = 10;

    calc_ans(l, r);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to count the elements
// in the range [L, R] whose prime
// factors are only 2 and 3.
using System;
using System.Collections.Generic;

class GFG{

// Function which will calculate the
// elements in the given range
static void calc_ans(int l, int r)
{

    List<int> power2 = new List<int>(),
              power3 = new List<int>();

    // Store the current power of 2
    int mul2 = 1;
    while (mul2 <= r)
    {
        power2.Add(mul2);
        mul2 *= 2;
    }

    // Store the current power of 3
    int mul3 = 1;
    while (mul3 <= r)
    {
        power3.Add(mul3);
        mul3 *= 3;
    }

    // power23[] will store pairwise product of
    // elements of power2 and power3 that are <=r
    List<int> power23 = new List<int>();

    for (int x = 0; x < power2.Count; x++)
    {
        for (int y = 0; y < power3.Count; y++)
        {
            int mul = power2[x] *
                      power3[y];
            if (mul == 1)
                continue;

            // Insert in power23,]
            // only if mul<=r
            if (mul <= r)
                power23.Add(mul);
        }
    }

    // Store the required answer
    int ans = 0;
    foreach (int x in power23)
    {
        if (x >= l && x <= r)
            ans++;
    }

    // Print the result
    Console.Write(ans + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int l = 1, r = 10;

    calc_ans(l, r);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to count the elements
// in the range [L, R] whose prime
// factors are only 2 and 3.

// Function which will calculate the
// elements in the given range
function calc_ans(l, r)
{

    var power2 = [], power3 = [];

    // Store the current power of 2
    var mul2 = 1;
    while (mul2 <= r) {
        power2.push(mul2);
        mul2 *= 2;
    }

    // Store the current power of 3
    var mul3 = 1;
    while (mul3 <= r) {
        power3.push(mul3);
        mul3 *= 3;
    }

    // power23[] will store pairwise product of
    // elements of power2 and power3 that are <=r
    var power23 = [];

    for (var x = 0; x < power2.length; x++) {
        for (var y = 0; y < power3.length; y++) {

            var mul = power2[x] * power3[y];
            if (mul == 1)
                continue;

            // Insert in power23][]
            // only if mul<=r
            if (mul <= r)
                power23.push(mul);
        }
    }

    // Store the required answer
    var ans = 0;
    power23.forEach(x => {

        if (x >= l && x <= r)
            ans++;
    });

    // Print the result
    document.write( ans );
}

// Driver code
var l = 1, r = 10;
calc_ans(l, r);

</script>
```

**Output:** 

```
6
```

**时间复杂度:***O(log<sub>2</sub>(R)* log<sub>3</sub>(R))*
**注:**该方法可以进一步优化。存储 2 和 3 的幂后，可以使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)计算答案，而不是生成所有的数字