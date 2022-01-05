# 检查甲、乙类物品是否都能放在 N 个货架上

> 原文:[https://www . geeksforgeeks . org/check-如果 a 和 b 类型的所有对象都可以放置在 n 个货架上/](https://www.geeksforgeeks.org/check-if-all-objects-of-type-a-and-b-can-be-placed-on-n-shelves/)

给定两个整数 **A** 和 **B** ，代表两种不同类型对象的计数，以及另一个整数 **N** ，代表货架数量，任务是将所有对象放置在给定的 N 个货架中，遵守以下规则:

*   任何架子都不能同时包含类型-A 和类型-B 对象。
*   没有架子能容纳超过甲类 **K** 物体或乙类 **L** 物体

如果可以将所有物品放入 N 个货架，打印**“是”**。否则，打印**“否”**。
**例:**

> **输入:** A = 3，B = 3，N = 3，K = 4，M = 2
> **输出:** YES
> **说明:**
> 3 个 A 型物品可以放在 1 个货架上，因为最大限制是 4 个。
> 3 个 B 型物品可以放在 2 个货架上，因为最大限制是 2 个。
> 由于所需的盘架数量不超过 N，因此可以进行分配。
> **输入:** A = 6，B = 7，N = 3，K = 4，L = 5
> **输出:**否
> **说明:**
> 6 个 A 型物品需要 2 个货架，因为最大限制是 4 个。
> 7 个 B 型物品需要 2 个货架，最大限量为 5 个。
> 由于所需的盘架数量超过 N，因此无法分配。

**进场:**
要解决这个问题，我们需要统计放置所有物品所需的最小货架数量，检查是否超过 **N** 。按照以下步骤操作:

*   计算放置**A 型**物品所需的最小物品数量，比如**需要一个**。由于，**K**A 型物品最多只能放在一个货架上，因此出现了以下两种情况:
    1.  如果 *A 可以被 K* 整除，那么所有的 A 型物品都可以放在 **A / K** 货架上。
    2.  否则 **A % K** 物品需要放在 1 个货架上，其余放在 **A / K** 货架上。因此这种情况下需要 **A/ K + 1** 货架。
*   同样，计算放置 B 型物品所需的最小货架数量，比如**需要**。

*   如果**需要 a +需要 b** 超过 **N** ，则无法分配。否则，是有可能的。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return if allocation
// is possible or not
bool isPossible(int A, int B, int N,
                int K, int L)
{
    // Stores the shelves needed
    // for items of type-A and type-B
    int needa, needb;

    // Find number of shelves
    // needed for items of type-A
    if (A % K == 0)

        // Fill A / K shelves fully
        // by the items of type-A
        needa = A / K;

    // Otherwise
    else

        // Fill A / L shelves fully
        // and add remaining to an
        // extra shelf
        needa = A / K + 1;

    // Find number of shelves
    // needed for items of type-B
    if (B % L == 0)

        // Fill B / L shelves fully
        // by the items of type-B
        needb = B / L;

    else

        // Fill B / L shelves fully
        // and add remaining to an
        // an extra shelf
        needb = B / L + 1;

    // Total shelves needed
    int total = needa + needb;

    // If required shelves exceed N
    if (total > N)
        return false;
    else
        return true;
}

// Driver Program
int main()
{
    int A = 3, B = 3, N = 3;
    int K = 4, M = 2;

    if (isPossible(A, B, N, K, M))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to return if allocation
// is possible or not
static boolean isPossible(int A, int B,
                          int N, int K,
                          int L)
{

    // Stores the shelves needed
    // for items of type-A and type-B
    int needa, needb;

    // Find number of shelves
    // needed for items of type-A
    if (A % K == 0)

        // Fill A / K shelves fully
        // by the items of type-A
        needa = A / K;

    // Otherwise
    else

        // Fill A / L shelves fully
        // and add remaining to an
        // extra shelf
        needa = A / K + 1;

    // Find number of shelves
    // needed for items of type-B
    if (B % L == 0)

        // Fill B / L shelves fully
        // by the items of type-B
        needb = B / L;

    else

        // Fill B / L shelves fully
        // and add remaining to an
        // an extra shelf
        needb = B / L + 1;

    // Total shelves needed
    int total = needa + needb;

    // If required shelves exceed N
    if (total > N)
        return false;
    else
        return true;
}

// Driver code
public static void main(String[] args)
{
    int A = 3, B = 3, N = 3;
    int K = 4, M = 2;

    if (isPossible(A, B, N, K, M))
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to return if allocation
# is possible or not
def isPossible(A, B, N, K, L):

    # Stores the shelves needed
    # for items of type-A and type-B
    needa = 0
    needb = 0

    # Find number of shelves
    # needed for items of type-A
    if (A % K == 0):

        # Fill A / K shelves fully
        # by the items of type-A
        needa = A // K;

    # Otherwise
    else:

        # Fill A / L shelves fully
        # and add remaining to an
        # extra shelf
        needa = A // K + 1

    # Find number of shelves
    # needed for items of type-B
    if (B % L == 0):

        # Fill B / L shelves fully
        # by the items of type-B
        needb = B // L

    else:

        # Fill B / L shelves fully
        # and add remaining to an
        # an extra shelf
        needb = B // L + 1

    # Total shelves needed
    total = needa + needb

    # If required shelves exceed N
    if (total > N):
        return False
    else:
        return True

# Driver Code       
if __name__=='__main__':

    A, B, N = 3, 3, 3
    K, M = 4, 2

    if (isPossible(A, B, N, K, M)):
        print('YES')
    else:
        print('NO')

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to return if allocation
// is possible or not
static bool isPossible(int A, int B,
                       int N, int K,
                       int L)
{

    // Stores the shelves needed
    // for items of type-A and type-B
    int needa, needb;

    // Find number of shelves
    // needed for items of type-A
    if (A % K == 0)

        // Fill A / K shelves fully
        // by the items of type-A
        needa = A / K;

    // Otherwise
    else

        // Fill A / L shelves fully
        // and add remaining to an
        // extra shelf
        needa = A / K + 1;

    // Find number of shelves
    // needed for items of type-B
    if (B % L == 0)

        // Fill B / L shelves fully
        // by the items of type-B
        needb = B / L;

    else

        // Fill B / L shelves fully
        // and add remaining to an
        // an extra shelf
        needb = B / L + 1;

    // Total shelves needed
    int total = needa + needb;

    // If required shelves exceed N
    if (total > N)
        return false;
    else
        return true;
}

// Driver code
public static void Main(String[] args)
{
    int A = 3, B = 3, N = 3;
    int K = 4, M = 2;

    if (isPossible(A, B, N, K, M))
        Console.Write("YES" + "\n");
    else
        Console.Write("NO" + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to return if allocation
// is possible or not
function isPossible(A, B, N, K, L)
{

    // Stores the shelves needed
    // for items of type-A and type-B
    let needa, needb;

    // Find number of shelves
    // needed for items of type-A
    if (A % K == 0)

        // Fill A / K shelves fully
        // by the items of type-A
        needa =  Math.floor(A / K);

    // Otherwise
    else

        // Fill A / L shelves fully
        // and add remaining to an
        // extra shelf
        needa =  Math.floor(A / K) + 1;

    // Find number of shelves
    // needed for items of type-B
    if (B % L == 0)

        // Fill B / L shelves fully
        // by the items of type-B
        needb = Math.floor(B / L);

    else

        // Fill B / L shelves fully
        // and add remaining to an
        // an extra shelf
        needb =  Math.floor(B / L) + 1;

    // Total shelves needed
    let total = needa + needb;

    // If required shelves exceed N
    if (total > N)
        return false;
    else
        return true;
}

// Driver code

    let A = 3, B = 3, N = 3;
    let K = 4, M = 2;

    if (isPossible(A, B, N, K, M))
        document.write("YES" + "<br/>");
    else
        document.write("NO" + "<br/>");

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*