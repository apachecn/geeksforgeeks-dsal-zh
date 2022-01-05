# 不找零购买最少物品并赠送硬币

> 原文:[https://www . geeksforgeeks . org/购买最少不找零赠送硬币的物品/](https://www.geeksforgeeks.org/buy-minimum-items-without-change-and-given-coins/)

你有无限数量的 10 卢比硬币和正好一枚 r 卢比硬币，你需要购买最低成本为 k 的物品，这样你就不会要求零钱。
**例:**

> 输入:k = 15，r = 2
> 输出:2
> 你应该买两根电缆，付 2*15=30 卢比。很明显，你可以不用找零就付这笔钱。
> 输入:k = 237，r = 7
> 输出:1
> 买一根电缆就够了。

很明显，我们可以支付 10 件物品而不需要任何零钱(通过支付所需数量的 10 卢比硬币，并且不使用 r 卢比硬币)。但也许你可以少买几把锤子，不用找零就能付款。请注意，您应该至少购买一件物品。

## C++

```
#include <bits/stdc++.h>
using namespace std;

int minItems(int k, int r)
{
   // See if we can buy less than 10 items
   // Using 10 Rs coins and one r Rs coin
   for (int i = 1; i < 10; i++)
        if ((i * k - r) % 10 == 0 ||
            (i * k) % 10 == 0)
            return i;

    // We can always buy 10 items
    return 10;
}

int main()
{
    int k = 15;
    int r = 2;
    cout << minItems(k, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{
static int minItems(int k, int r)
{

// See if we can buy less than 10 items
// Using 10 Rs coins and one r Rs coin
for (int i = 1; i < 10; i++)
        if ((i * k - r) % 10 == 0 ||
            (i * k) % 10 == 0)
            return i;

    // We can always buy 10 items
    return 10;
}

// Driver Code
public static void main(String args[])
{
    int k = 15;
    int r = 2;
    System.out.println(minItems(k, r));
}
}

// This code is contributed
// by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 implementation of above approach

def minItems(k, r) :

    # See if we can buy less than 10 items
    # Using 10 Rs coins and one r Rs coin
    for i in range(1, 10) :
            if ((i * k - r) % 10 == 0 or
                (i * k) % 10 == 0) :
                return i

    # We can always buy 10 items
    return 10;

# Driver Code
if __name__ == "__main__" :

    k, r = 15 , 2;
    print(minItems(k, r))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
static int minItems(int k, int r)
{

// See if we can buy less than 10 items
// Using 10 Rs coins and one r Rs coin
for (int i = 1; i < 10; i++)
        if ((i * k - r) % 10 == 0 ||
            (i * k) % 10 == 0)
            return i;

    // We can always buy 10 items
    return 10;
}

// Driver Code
public static void Main()
{
    int k = 15;
    int r = 2;
    Console.WriteLine(minItems(k, r));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// See if we can buy less than 10 items
// Using 10 Rs coins and one r Rs coin
function minItems($k, $r)
{
    for ($i = 1; $i < 10; $i++)
    if (($i * $k - $r) % 10 == 0 ||
        ($i * $k) % 10 == 0)
        return $i;

    // We can always buy 10 items
    return 10;
}

// Driver Code
$k = 15;
$r = 2;
echo minItems($k, $r);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript program of the above approach

function minItems(k, r)
{

// See if we can buy less than 10 items
// Using 10 Rs coins and one r Rs coin
for (let i = 1; i < 10; i++)
        if ((i * k - r) % 10 == 0 ||
            (i * k) % 10 == 0)
            return i;

    // We can always buy 10 items
    return 10;
}

// Driver code

    let k = 15;
    let r = 2;
    document.write(minItems(k, r));

</script>
```

**Output:** 

```
2
```