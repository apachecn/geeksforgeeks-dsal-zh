# 检查一个号码是否为弗拉维乌斯号码

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-flavius-number/](https://www.geeksforgeeks.org/check-if-a-number-is-flavius-number/)

给定一系列从 **1** 到**无穷大**的整数和一个数字 **N** 。
任务是在每第**次**次迭代时，从剩余系列中移除每第 **(i + 1)个**元素，并发现系列中是否存在给定数量的 **N** 。
**弗拉维乌斯编号** :

> 弗拉维乌斯筛中的数字被称为弗拉维乌斯数字。
> Flavius 筛选从自然数开始，并继续重复以下步骤:
> 在第 k 次筛选步骤中，移除第(k-1)次筛选步骤后剩余的 N 个自然数序列中的每一个(k+1)项。
> 例如:1、3、7、13、19、27、39、49、

**例:**

> **输入:** N = 17
> **输出:** N0
> **系列第 I 次迭代后**
> 1)。1、3、5、7、9、11、13、15、17、…
> 2)。1、3、7、9、13、15、19、21、25、……
> 3)。1、3、7、13、15、19、25、……
> 4)。1, 3, 7, 13, 19, 27, ….
> **输入:** N = 3
> **输出:**是

**进场:**

*   如果给定的数字是偶数，答案就是“不”。因为在第一次迭代中，所有的偶数都从数列中去掉了。
*   重复这个过程。
    *   否则移除第一次迭代中移除的元素数量，即数量的 1/2，然后检查
        如果它能被 3 整除，答案应该是“否”，否则减去之前移除的数量，即数量的 1/3，以此类推。
    *   对所有迭代重复上述步骤，直到我们得到答案。

以下是实施办法:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Return the number is
// Flavious Number or not
bool Survives(int n)
{
    int i;

    // index i starts from 2 because
    // at 1st iteration every 2nd
    // element was remove and keep
    // going for k-th iteration
    for (int i = 2;; i++) {
        if (i > n)
            return true;
        if (n % i == 0)
            return false;

        // removing the elements which are
        // already removed at kth iteration
        n -= n / i;
    }
}

// Driver Code
int main()
{
    int n = 17;
    if (Survives(n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Return the number is
// Flavious Number or not
static boolean Survives(int n)
{

    // index i starts from 2 because
    // at 1st iteration every 2nd
    // element was remove and keep
    // going for k-th iteration
    for (int i = 2;; i++)
    {
        if (i > n)
            return true;
        if (n % i == 0)
            return false;

        // removing the elements which are
        // already removed at kth iteration
        n -= n / i;
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 17;
    if (Survives(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Return the number is
# Flavious Number or not
def Survives(n) :

    # index i starts from 2 because
    # at 1st iteration every 2nd
    # element was remove and keep
    # going for k-th iteration
    i = 2
    while(True) :

        if (i > n) :
            return True;

        if (n % i == 0) :
            return False;

        # removing the elements which are
        # already removed at kth iteration
        n -= n // i;
        i += 1

# Driver Code
if __name__ == "__main__" :

    n = 17;

    if (Survives(n)) :
        print("Yes");

    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Return the number is
// Flavious Number or not
static bool Survives(int n)
{

    // index i starts from 2 because
    // at 1st iteration every 2nd
    // element was remove and keep
    // going for k-th iteration
    for (int i = 2;; i++)
    {
        if (i > n)
            return true;
        if (n % i == 0)
            return false;

        // removing the elements which are
        // already removed at kth iteration
        n -= n / i;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n = 17;
    if (Survives(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation

// Return the number is
// Flavious Number or not
function Survives(n)
{
    let i;

    // index i starts from 2 because
    // at 1st iteration every 2nd
    // element was remove and keep
    // going for k-th iteration
    for (let i = 2;; i++) {
        if (i > n)
            return true;
        if (n % i == 0)
            return false;

        // removing the elements which are
        // already removed at kth iteration
        n -= parseInt(n / i);
    }
}

// Driver Code
    let n = 17;
    if (Survives(n))
        document.write("Yes<br>");
    else
        document.write("No<br>");

</script>
```

**Output:** 

```
No
```