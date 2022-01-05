# 大于 n 的最小数，可以表示为 k 的不同幂的和

> 原文:[https://www . geesforgeks . org/最小大于 n 的数可以表示为 k 的不同幂的和/](https://www.geeksforgeeks.org/smallest-number-greater-than-n-that-can-be-represented-as-a-sum-of-distinct-power-of-k/)

给定一个数字 **n** 和值 **k** ，任务是找到最小的 **m** (m > =n)，这样 m 可以表示为 k 的不同幂的和。

**示例:**

> **输入:** n = 5，k = 5
> **输出:** 5
> **说明:** 5 = 5 <sup>1</sup>
> 
> **输入:** n = 29，k = 5
> **输出:** 30
> 说明:30 = 5 <sup>1</sup> + 5 <sup>2</sup>

**进场:**

1.  存储 n 的 k 元(基 k)表示。然后遍历基 k 表示的每个元素。
2.  如果这个位置的基 k 表示是 1 或 0，那么继续。如果大于 1，则意味着 k 的当前幂出现不止一次。
3.  在这种情况下，该幂被加 k (k 的位置值)次，这使得它多一次幂(((k-1)+1)。k<sup>x</sup>= k . k<sup>x</sup>= k<sup>x+1</sup>。
4.  因为必须找到最小的数，所以在这一步之后，k 的所有低次幂都被减少到 0，因为相加(k-b)k<sup>x</sup>(b =基础 k 表示中该位置的值)已经使大于前一个数。
5.  最后，将数字转换回十进制形式。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
#define pb push_back

// Function to find the smallest number
// greater than or equal to n represented
// as the sum of distinct powers of k
void greaterK(ll n, ll k)
{

    // Vector P to store the base k
    // representation of the number
    vector<ll> p;
    ll x = n;
    while (x) {
        p.pb(x % k);
        x /= k;
    }
    int idx = 0;
    for (ll i = 0; i < (ll)p.size() - 1; ++i) {
        if (p[i] >= 2) {

            // If the representation is >=2, then
            // this power of k has to be added
            // once again and then increase the
            // next power of k and make the
            // current power 0

            p[i] = 0;
            p[i + 1]++;

            // Reduce all the lower power of
            // k to 0

            for (int j = idx; j < i; ++j) {
                p[j] = 0;
            }
            idx = i + 1;
        }

        if (p[i] == k) {
            p[i] = 0;
            p[i + 1]++;
        }
    }
    ll j = (ll)p.size() - 1;

    // Check if the most significant
    // bit also satisfy the above
    // conditions

    if (p[j] >= 2) {
        for (auto& i : p)
            i = 0;
        p.pb(1);
    }
    ll ans = 0;

    // Converting back from the
    // k-nary representation to
    // decimal form.
    for (ll i = p.size() - 1; i >= 0; --i) {
        ans = ans * k + p[i];
    }
    cout << ans << endl;
}

int main()
{
    ll n = 29, k = 7;
    greaterK(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the smallest number
// greater than or equal to n represented
// as the sum of distinct powers of k
static void greaterK(int n, int k)
{

    // Vector P to store the base k
    // representation of the number
    int []p = new int[String.valueOf(n).length() + 2];
    int index = 0;
    int x = n;
    while (x > 0)
    {
        p[index]=(int) (x % k);
        x /= k;
        index++;
    }
    int idx = 0;
    for (int i = 0; i < p.length - 1; ++i)
    {
        if (p[i] >= 2)
        {

            // If the representation is >=2, then
            // this power of k has to be added
            // once again and then increase the
            // next power of k and make the
            // current power 0
            p[i] = 0;
            p[i + 1]++;

            // Reduce all the lower power of
            // k to 0
            for (int j = idx; j < i; ++j)
            {
                p[j] = 0;
            }
            idx = i + 1;
        }

        if (p[i] == k)
        {
            p[i] = 0;
            p[i + 1]++;
        }
    }
    int j = p.length - 1;

    // Check if the most significant
    // bit also satisfy the above
    // conditions
    if (p[j] >= 2)
    {
        p[index] = 1;
        index++;
    }
    int ans = 0;

    // Converting back from the
    // k-nary representation to
    // decimal form.
    for (int i = p.length - 1; i >= 0; --i)
    {
        ans = ans * k + p[i];
    }
    System.out.print(ans +"\n");
}

// Driver code
public static void main(String[] args)
{
    int n = 29, k = 7;
    greaterK(n, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the smallest number
# greater than or equal to n represented
# as the sum of distinct powers of k
def greaterK(n, k):

    # Vector P to store the base k
    # representation of the number
    index = 0
    p = [0 for i in range(n + 2)]
    x = n
    while (x > 0):
        p[index] = x % k
        x //= k
        index += 1

    idx = 0
    for i in range(0,len(p)-1, 1):
        if (p[i] >= 2):

            # If the representation is >=2, then
            # this power of k has to be added
            # once again and then increase the
            # next power of k and make the
            # current power 0
            p[i] = 0
            p[i + 1] += 1

            # Reduce all the lower power of
            # k to 0
            for j in range(idx, i, 1):
                p[j] = 0

            idx = i + 1

        if (p[i] == k):
            p[i] = 0
            p[i + 1] += 1

    j = len(p) - 1

    # Check if the most significant
    # bit also satisfy the above
    # conditions
    if (p[j] >= 2):
        p[index] = 1
        index += 1
    ans = 0

    # Converting back from the
    # k-nary representation to
    # decimal form.
    i = len(p)-1
    while(i>= 0):
        ans = ans * k + p[i]
        i -= 1
    print(ans)

if __name__ == '__main__':
    n = 29
    k = 7
    greaterK(n, k)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the smallest number
// greater than or equal to n represented
// as the sum of distinct powers of k
static void greaterK(int n, int k)
{

    // List P to store the base k
    // representation of the number
    int []p = new int[String.Join("",n).Length + 2];
    int index = 0;
    int x = n;
    int j;
    while (x > 0)
    {
        p[index] = (int) (x % k);
        x /= k;
        index++;
    }
    int idx = 0;
    for (int i = 0; i < p.Length - 1; ++i)
    {
        if (p[i] >= 2)
        {

            // If the representation is >=2, then
            // this power of k has to be added
            // once again and then increase the
            // next power of k and make the
            // current power 0
            p[i] = 0;
            p[i + 1]++;

            // Reduce all the lower power of
            // k to 0
            for (j = idx; j < i; ++j)
            {
                p[j] = 0;
            }
            idx = i + 1;
        }

        if (p[i] == k)
        {
            p[i] = 0;
            p[i + 1]++;
        }
    }
    j = p.Length - 1;

    // Check if the most significant
    // bit also satisfy the above
    // conditions
    if (p[j] >= 2)
    {
        p[index] = 1;
        index++;
    }
    int ans = 0;

    // Converting back from the
    // k-nary representation to
    // decimal form.
    for (int i = p.Length - 1; i >= 0; --i)
    {
        ans = ans * k + p[i];
    }
    Console.Write(ans +"\n");
}

// Driver code
public static void Main(String[] args)
{
    int n = 29, k = 7;
    greaterK(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to find the smallest number
// greater than or equal to n represented
// as the sum of distinct powers of k
function greaterK(n, k) {

    // Vector P to store the base k
    // representation of the number
    let p = new Array(String(n).length + 2).fill(0);
    let index = 0;
    let x = n;
    while (x > 0) {
        p[index] = (x % k);
        x = Math.floor(x / k);
        index++;
    }
    let idx = 0;
    for (let i = 0; i < p.length - 1; ++i) {
        if (p[i] >= 2) {

            // If the representation is >=2, then
            // this power of k has to be added
            // once again and then increase the
            // next power of k and make the
            // current power 0
            p[i] = 0;
            p[i + 1]++;

            // Reduce all the lower power of
            // k to 0
            for (let j = idx; j < i; ++j) {
                p[j] = 0;
            }
            idx = i + 1;
        }

        if (p[i] == k) {
            p[i] = 0;
            p[i + 1]++;
        }
    }
    let j = p.length - 1;

    // Check if the most significant
    // bit also satisfy the above
    // conditions
    if (p[j] >= 2) {
        p[index] = 1;
        index++;
    }
    let ans = 0;

    // Converting back from the
    // k-nary representation to
    // decimal form.
    for (let i = p.length - 1; i >= 0; --i) {
        ans = ans * k + p[i];
    }
    document.write(ans + "<br>");
}

// Driver code

let n = 29, k = 7;
greaterK(n, k);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
49
```