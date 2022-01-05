# 检查给定范围内是否有 GCD 可被 k 整除的配对

> 原文:[https://www . geeksforgeeks . org/check-如果给定范围内有任何一对带 gcd 的可被 k 整除/](https://www.geeksforgeeks.org/check-if-there-is-any-pair-in-a-given-range-with-gcd-is-divisible-by-k/)

给定一个范围，我们需要检查 GCD 可被 k 整除的段中是否有它们的任意对
T1】示例:T3】

```
Input : l=4, r=6, k=2
Output : YES
There are two numbers 4 and 6 whose GCD is 2 which is divisible by 2.

Input : l=3 r=5 k=4
Output : NO
Their is no such pair whose gcd is divisible by 5.
```

基本上我们需要在 l 到 r 的范围内对这样的数进行计数，这样它们就可以被 k 整除。因为如果我们选择任何两个这样的数，那么它们的 gcd 也是 k 的倍数。现在，如果这样的数的计数大于 1，那么我们就可以形成一对，否则就不可能形成一对(x，y)使得 gcd(x，y)可以被 k 整除。
下面是上面方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to count such possible numbers
bool Check_is_possible(int l, int r, int k)
{
    int count = 0;

    for (int i = l; i <= r; i++) {

        // if i is divisible by k
        if (i % k == 0)
            count++;
    }

    // if count of such numbers
    // is greater than one
    return (count > 1);
}

// Driver code
int main()
{
    int l = 4, r = 12;
    int k = 5;

    if (Check_is_possible(l, r, k))
        cout << "YES\n";
    else
        cout << "NO\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// function to count such
// possible numbers

class GFG {

    public boolean Check_is_possible(int l, int r,
            int k) {
        int count = 0;

        for (int i = l; i <= r; i++) {

            // if i is divisible by k
            if (i % k == 0) {
                count++;
            }
        }

        // if count of such numbers
        // is greater than one
        return (count > 1);
    }

    public static void main(String[] args) {
        GFG g = new GFG();
        int l = 4, r = 12;
        int k = 5;

        if (g.Check_is_possible(l, r, k)) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }

    }
}
// This code is contributed by RAJPUT-JI
```

## 蟒蛇 3

```
# function to count such possible numbers
def Check_is_possible(l, r, k):

    count = 0;

    for i in range(l, r + 1):

        # if i is divisible by k
        if (i % k == 0):
            count += 1;

    # if count of such numbers
    # is greater than one
    return (count > 1);

# Driver code
l = 4;
r = 12;
k = 5;
if (Check_is_possible(l, r, k)):
    print("YES");
else:
    print("NO");

# This code is contributed by mits
```

## C#

```
using System;

// function to count such
// possible numbers
class GFG
{
public bool Check_is_possible(int l, int r,
                              int k)
{
    int count = 0;

    for (int i = l; i <= r; i++)
    {

        // if i is divisible by k
        if (i % k == 0)
            count++;
    }

    // if count of such numbers
    // is greater than one
    return (count > 1);
}

// Driver code
public static void Main()
{
    GFG g = new GFG();
    int l = 4, r = 12;
    int k = 5;

    if (g.Check_is_possible(l, r, k))
        Console.WriteLine("YES\n");
    else
    Console.WriteLine("NO\n");
}
}

// This code is contributed
// by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// function to count such possible numbers
function Check_is_possible($l, $r, $k)
{
    $count = 0;

    for ($i = $l; $i <= $r; $i++)
    {

        // if i is divisible by k
        if ($i % $k == 0)
            $count++;
    }

    // if count of such numbers
    // is greater than one
    return ($count > 1);
}

// Driver code
$l = 4; $r = 12;
$k = 5;

if (Check_is_possible($l, $r, $k))
    echo "YES\n";
else
    echo "NO\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// function to count such
// possible numbers
    function Check_is_possible(l , r , k) {
        var count = 0;

        for (i = l; i <= r; i++) {

            // if i is divisible by k
            if (i % k == 0) {
                count++;
            }
        }

        // if count of such numbers
        // is greater than one
        return (count > 1);
    }

        var l = 4, r = 12;
        var k = 5;

        if (Check_is_possible(l, r, k)) {
            document.write("YES");
        } else {
            document.write("NO");
        }

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
YES
```

**时间复杂度:O(r–l+1)**
一个**高效的解决方案**基于这里[讨论的高效方法](https://www.geeksforgeeks.org/count-numbers-divisible-m-given-range/)。

## C++

```
// C++ program to count the numbers divisible
// by k in a given range
#include <bits/stdc++.h>
using namespace std;

// Returns count of numbers in [l r] that
// are divisible by k.
int Check_is_possible(int l, int r, int k)
{
    int div_count = (r / k) - (l / k);

    // Add 1 explicitly as l is divisible by k
    if (l % k == 0)
        div_count++;

    // l is not divisible by k
    return (div_count > 1);
}

// Driver Code
int main()
{
    int l = 30, r = 70, k = 10;

    if (Check_is_possible(l, r, k))
        cout << "YES\n";
    else
        cout << "NO\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the numbers divisible
// by k in a given range

class GFG {

// Returns count of numbers in [l r] that
// are divisible by k.
    static boolean Check_is_possible(int l, int r, int k) {
        int div_count = (r / k) - (l / k);

        // Add 1 explicitly as l is divisible by k
        if (l % k == 0) {
            div_count++;
        }

        // l is not divisible by k
        return (div_count > 1);
    }

// Driver Code
    public static void main(String[] args) {
        int l = 30, r = 70, k = 10;
        if (Check_is_possible(l, r, k)) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }

    }
}
// This code is contributed by RAJPUT-JI
```

## 蟒蛇 3

```
# Python3 program to count the numbers
# divisible by k in a given range

# Returns count of numbers in [l r]
# that are divisible by k.
def Check_is_possible(l, r, k):

    div_count = (r // k) - (l // k)

    # Add 1 explicitly as l is
    # divisible by k
    if l % k == 0:
        div_count += 1

    # l is not divisible by k
    return div_count > 1

# Driver Code
if __name__ == "__main__":

    l, r, k = 30, 70, 10

    if Check_is_possible(l, r, k) == True:
        print("YES")
    else:
        print("NO")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to count the numbers divisible
// by k in a given range
using System;

public class GFG {

// Returns count of numbers in [l r] that
// are divisible by k.
    static bool Check_is_possible(int l, int r, int k) {
        int div_count = (r / k) - (l / k);

        // Add 1 explicitly as l is divisible by k
        if (l % k == 0) {
            div_count++;
        }

        // l is not divisible by k
        return (div_count > 1);
    }

// Driver Code
    public static void Main() {
        int l = 30, r = 70, k = 10;
        if (Check_is_possible(l, r, k)) {
            Console.WriteLine("YES");
        } else {
            Console.WriteLine("NO");
        }

    }
}
// This code is contributed by RAJPUT-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the numbers
// divisible by k in a given range

// Returns count of numbers in [l r]
// that are divisible by k.
function Check_is_possible($l, $r, $k)
{
    $div_count = (int)($r / $k) -
                 (int)($l / $k);

    // Add 1 explicitly as l
    // is divisible by k
    if ($l % $k == 0)
        $div_count++;

    // l is not divisible by k
    return ($div_count > 1);
}

// Driver Code
$l = 30;
$r = 70;
$k = 10;

if (Check_is_possible($l, $r, $k))
    echo "YES\n";
else
    echo "NO\n";

// This Code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count the numbers divisible
// by k in a given range
    // Returns count of numbers in [l r] that
    // are divisible by k.
    function Check_is_possible(l , r , k)
    {
        var div_count = (r / k) - (l / k);

        // Add 1 explicitly as l is divisible by k
        if (l % k == 0) {
            div_count++;
        }

        // l is not divisible by k
        return (div_count > 1);
    }

    // Driver Code

        var l = 30, r = 70, k = 10;
        if (Check_is_possible(l, r, k)) {
            document.write("YES");
        } else {
            document.write("NO");
        }

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
YES
```