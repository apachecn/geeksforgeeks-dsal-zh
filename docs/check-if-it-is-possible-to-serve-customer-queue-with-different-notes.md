# 检查是否可以为不同票据的客户队列服务

> 原文:[https://www . geeksforgeeks . org/check-如果可能的话-服务客户-不同备注排队/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-serve-customer-queue-with-different-notes/)

给定票据“25”和一个整数数组“arr”的成本，数组“arr”保存队列中的人所拥有的票据值(25”、“50”或“100”个卢比。注释)。
任务是从 0 Rs 开始，寻找是否有可能将门票按顺序卖给民众。
**例:**

```
Input: arr = {25, 25, 50, 50}
Output: YES
You can give the 25 you received from the 1st customer 
to the 3rd customer and then the 25 from the 2nd customer to the 4th.

Input: arr = {25, 100}
Output: NO
It is not possible to return the change to the 2nd customer.
```

**方法:**记录 Rs 的数量。25 和 Rs。50 个音符，我们目前分别有‘c25’和‘c50’。没有必要记录卢比的数量。100 张纸币，因为我们不能退还给任何顾客。现在有 3 种可能:

*   如果客户支付 Rs。25:增量 c25，什么都不用退给客户。
*   如果客户支付 Rs。50 卢比。25 必须返还给客户，检查 c25 是否> 0，然后增加 c50 并减少 c25。
*   如果客户支付 Rs。100:卢比。75 英镑必须退还给顾客。有两种方法可以做到这一点，要么使用一个 Rs。50 和一个 Rs。25 个音符或使用三个 Rs。25 张纸币。我们更喜欢第一种方式，这样如果将来有人用 Rs。50 来了，我们还剩下 25 个。检查是否可能，并相应地减少计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns
// true is selling of
// the tickets is possible
bool isSellingPossible(int n, int a[])
{
    int i, c25 = 0, c50 = 0;
    for (i = 0; i < n; i++) {

        // Nothing to return
        // to the customer
        if (a[i] == 25)
            c25++;
        else if (a[i] == 50) {
            c50++;

            // Check if 25 can be
            // returned to customer.
            if (c25 == 0)
                break;
            c25--;
        }
        else {

            // Try returning one
            // 50 and one 25
            if (c50 > 0 && c25 > 0) {
                c50--;
                c25--;
            }

            // Try returning three 25
            else if (c25 >= 3)
                c25 -= 3;
            else
                break;
        }
    }

    // If the loop did not break,
    // all the tickets were sold
    if (i == n)
        return true;
    else
        return false;
}

// Driver Program to
// test above function
int main()
{
    int a[] = { 25, 25, 50, 100 };
    int n = sizeof(a) / sizeof(a[0]);

    if (isSellingPossible(n, a)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
// Function that returns
// true is selling of
// the tickets is possible
static boolean isSellingPossible(int n,
                                 int a[])
{
    int i, c25 = 0, c50 = 0;
    for (i = 0; i < n; i++)
    {

        // Nothing to return
        // to the customer
        if (a[i] == 25)
            c25++;
        else if (a[i] == 50)
        {
            c50++;

            // Check if 25 can be
            // returned to customer.
            if (c25 == 0)
                break;
            c25--;
        }
        else
        {

            // Try returning one
            // 50 and one 25
            if (c50 > 0 && c25 > 0)
            {
                c50--;
                c25--;
            }

            // Try returning three 25
            else if (c25 >= 3)
                c25 -= 3;
            else
                break;
        }
    }

    // If the loop did not break,
    // all the tickets were sold
    if (i == n)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String []args)
{
    int a[] = { 25, 25, 50, 100 };
    int n = a.length;

    if (isSellingPossible(n, a))
    {
        System.out.println("YES");
    }
    else
    {
        System.out.println("NO");
    }
}
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true is selling
# of the tickets is possible
def isSellingPossible(n, a):

    c25 = 0;
    c50 = 0;
    i = 0;
    while(i < n):

        # Nothing to return to the customer
        if (a[i] == 25):
            c25 += 1;
        elif (a[i] == 50):

            c50 += 1;

            # Check if 25 can be returned
            # to customer.
            if (c25 == 0):
                break;
            c25 -= 1;

        else:

            # Try returning one
            # 50 and one 25
            if (c50 > 0 and c25 > 0):

                c50 -= 1;
                c25 -= 1;

            # Try returning three 25
            elif (c25 >= 3):
                c25 -= 3;
            else:
                break;
        i += 1;

    # If the loop did not break,
    # all the tickets were sold
    if (i == n):
        return True;
    else:
        return False;

# Driver Code
a = [ 25, 25, 50, 100 ];
n = len(a);

if (isSellingPossible(n, a)):
    print("YES");
else:
    print("NO");

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function that returns
// true is selling of
// the tickets is possible
static bool isSellingPossible(int n, int []a)
{
    int i, c25 = 0, c50 = 0;
    for (i = 0; i < n; i++)
    {

        // Nothing to return
        // to the customer
        if (a[i] == 25)
            c25++;
        else if (a[i] == 50)
        {
            c50++;

            // Check if 25 can be
            // returned to customer.
            if (c25 == 0)
                break;
            c25--;
        }
        else
        {

            // Try returning one
            // 50 and one 25
            if (c50 > 0 && c25 > 0)
            {
                c50--;
                c25--;
            }

            // Try returning three 25
            else if (c25 >= 3)
                c25 -= 3;
            else
                break;
        }
    }

    // If the loop did not break,
    // all the tickets were sold
    if (i == n)
        return true;
    else
        return false;
}

// Driver Code
public static void Main()
{
    int []a = { 25, 25, 50, 100 };
    int n = a.Length;

    if (isSellingPossible(n, a))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns
// true is selling of
// the tickets is possible
function isSellingPossible($n, $a)
{
    $c25 = 0;
    $c50 = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Nothing to return
        // to the customer
        if ($a[$i] == 25)
            $c25++;
        else if ($a[$i] == 50)
        {
            $c50++;

            // Check if 25 can be
            // returned to customer.
            if ($c25 == 0)
                break;
            $c25--;
        }
        else
        {

            // Try returning one
            // 50 and one 25
            if ($c50 > 0 && $c25 > 0)
            {
                $c50--;
                $c25--;
            }

            // Try returning three 25
            else if ($c25 >= 3)
                $c25 -= 3;
            else
                break;
        }
    }

    // If the loop did not break,
    // all the tickets were sold
    if ($i == $n)
        return true;
    else
        return false;
}

// Driver Code
$a = array( 25, 25, 50, 100 );
$n = sizeof($a);

if (isSellingPossible($n, $a))
{
    echo "YES";
}
else
{
    echo "NO";
}

// This code is contributed
// by ihritik
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns
// true is selling of
// the tickets is possible
function isSellingPossible(n, a)
{
    let i, c25 = 0, c50 = 0;
    for (i = 0; i < n; i++)
    {

        // Nothing to return
        // to the customer
        if (a[i] == 25)
            c25++;
        else if (a[i] == 50)
        {
            c50++;

            // Check if 25 can be
            // returned to customer.
            if (c25 == 0)
                break;
            c25--;
        }
        else
        {

            // Try returning one
            // 50 and one 25
            if (c50 > 0 && c25 > 0)
            {
                c50--;
                c25--;
            }

            // Try returning three 25
            else if (c25 >= 3)
                c25 -= 3;
            else
                break;
        }
    }

    // If the loop did not break,
    // all the tickets were sold
    if (i == n)
        return true;
    else
        return false;
}

// driver code

        let a = [ 25, 25, 50, 100 ];
    let n = a.length;

    if (isSellingPossible(n, a))
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)