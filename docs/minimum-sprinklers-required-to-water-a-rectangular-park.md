# 给矩形公园浇水所需的最小洒水装置

> 原文:[https://www . geeksforgeeks . org/最小洒水装置-要求水到矩形公园/](https://www.geeksforgeeks.org/minimum-sprinklers-required-to-water-a-rectangular-park/)

给定具有 **N** 行和 **M** 列的 **N * M** 矩形公园，公园的每个单元是单位面积的正方形，单元之间的边界被称为六边形，并且可以在六边形的中间放置洒水器。任务是找到给整个公园浇水所需的最小喷头数量。

**示例:**

> **输入:** N = 3 M = 3
> **输出:** 5
> **说明:**
> 前两列需要 3 个洒水喷头，最后一列我们肯定要用 2 个洒水喷头给最后一列浇水。
> 
> **输入:** N = 5 M = 3
> **输出:** 8
> **说明:**
> 前两列需要 5 个洒水喷头，最后一列我们必然要用 3 个洒水喷头给最后一列洒水。

**进场:**

1.  在做了一些观察后，可以指出一件事，即对于每两个**柱， **N** 洒水喷头是必需的，因为我们可以将它们放置在两个柱之间。**
2.  如果 **M** 为偶数，那么显然需要 **N* (M / 2)** 喷头。
3.  但是如果 **M** 是奇数，那么**M–1**列的解可以使用偶数列公式来计算，对于最后一列，添加 **( N + 1) / 2** 洒水喷头来浇灌最后一列，而不管 N 是奇数还是偶数。

## C++

```
// C++ program to find the
// minimum number sprinklers
// required to water the park.

#include <iostream>
using namespace std;
typedef long long int ll;

// Function to find the
// minimum number sprinklers
// required to water the park.
void solve(int N, int M)
{

    // General requirements of
    // sprinklers
    ll ans = (N) * (M / 2);

    // if M is odd then add
    // one additional sprinklers
    if (M % 2 == 1) {
        ans += (N + 1) / 2;
    }

    cout << ans << endl;
}

// Driver code
int main()
{
    int N, M;
    N = 5;
    M = 3;
    solve(N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number sprinklers required
// to cover the park
class GFG{

// Function to find the minimum
// number sprinklers required
// to water the park.
public static int solve(int n, int m)
{

    // General requirements of sprinklers
    int ans = n * (m / 2);

    // If M is odd then add one
    // additional sprinklers
    if (m % 2 == 1)
    {
        ans += (n + 1) / 2;
    }
    return ans;
}

// Driver code
public static void main(String args[])
{
    int N = 5;
    int M = 3;

    System.out.println(solve(N, M));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to find the
# minimum number sprinklers
# required to water the park.

# Function to find the
# minimum number sprinklers
# required to water the park.
def solve(N, M) :

    # General requirements of
    # sprinklers
    ans = int((N) * int(M / 2))

    # if M is odd then add
    # one additional sprinklers
    if (M % 2 == 1):
        ans += int((N + 1) / 2)

    print(ans)

# Driver code
N = 5
M = 3
solve(N, M)

# This code is contributed by yatinagg
```

## C#

```
// C# program to find minimum
// number sprinklers required
// to cover the park
using System;

class GFG{

// Function to find the minimum
// number sprinklers required
// to water the park.
public static int solve(int n, int m)
{

    // General requirements of sprinklers
    int ans = n * (m / 2);

    // If M is odd then add one
    // additional sprinklers
    if (m % 2 == 1)
    {
        ans += (n + 1) / 2;
    }
    return ans;
}

// Driver code
public static void Main(String []args)
{
    int N = 5;
    int M = 3;

    Console.WriteLine(solve(N, M));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program to find the
// minimum number sprinklers
// required to water the park.

// Function to find the
// minimum number sprinklers
// required to water the park.
function solve(N, M)
{

    // General requirements of
    // sprinklers
    var ans = (N) * parseInt((M / 2));

    // if M is odd then add
    // one additional sprinklers
    if (M % 2 == 1) {
        ans += parseInt((N + 1) / 2);
    }

    document.write(ans);
}

// Driver code
    var N, M;
    N = 5;
    M = 3;
    solve(N, M);

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**输出:**

```
8
```