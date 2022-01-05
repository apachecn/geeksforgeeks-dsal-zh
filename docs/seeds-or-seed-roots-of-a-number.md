# 若干种子(或种子根)

> 原文:[https://www . geesforgeks . org/seeds-or-seed-root-of-a-number/](https://www.geeksforgeeks.org/seeds-or-seed-roots-of-a-number/)

数字 n 的种子是一个数字 x，这样 x 与它的数字相乘等于 n。任务是找到给定数字 n 的所有种子。如果没有种子存在，那么打印相同的种子。
**例:**

```
Input  : n = 138
Output : 23 
23 is a seed of 138 because
23*2*3 is equal to 138

Input : n = 4977
Output : 79 711 
79 is a seed of 4977 because
79 * 7 * 9 = 4977.
711 is also a seed of 4977 because
711 * 1 * 1 * 7 = 4977

Input  : n = 9
Output : No seed exists

Input  : n = 738
Output : 123 
```

**史诗中问**

这个想法是遍历从 1 到 n/2 的所有数字。对于每一个被遍历的数字，求该数字的乘积。下面程序中的一个重要优化是避免数字乘积的重复计算。我们将产品存储在一个数组中。如果一个产品已经被计算过，我们就返回它，否则我们就计算它。
下面是想法的实现。

## C++

```
// C++ program to find Seed of a number
#include <bits/stdc++.h>
using namespace std;
const int MAX = 10000;

int prodDig[MAX];

// Stores product of digits of x in prodDig[x]
int getDigitProduct(int x)
{
    // If x has single digit
    if (x < 10)
      return x;

    // If digit product is already computed
    if (prodDig[x] != 0)
       return prodDig[x];

    // If digit product is not computed before.
    int prod = (x % 10) * getDigitProduct(x/10);

    return (prodDig[x] = prod);
}

// Prints all seeds of n
void findSeed(int n)
{
    // Find all seeds using prodDig[]
    vector<int> res;
    for (int i=1; i<=n/2; i++)
        if (i*getDigitProduct(i) == n)
            res.push_back(i);

    // If there was no seed
    if (res.size() == 0)
    {
        cout << "NO seed exists\n";
        return;
    }

    // Print seeds
    for (int i=0; i<res.size(); i++)
        cout << res[i] << " ";
}

// Driver code
int main()
{
    long long int n = 138;
    findSeed(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Seed of a number
import java.util.*;

class GFg{
static int MAX = 10000;
static int[] prodDig=new int[MAX];

// Stores product of digits of x in prodDig[x]
static int getDigitProduct(int x)
{
    // If x has single digit
    if (x < 10)
    return x;

    // If digit product is already computed
    if (prodDig[x] != 0)
    return prodDig[x];

    // If digit product is not computed before.
    int prod = (x % 10) * getDigitProduct(x/10);

    return (prodDig[x] = prod);
}

// Prints all seeds of n
static void findSeed(int n)
{
    // Find all seeds using prodDig[]
    List<Integer> res = new ArrayList<Integer>();
    for (int i=1; i<=n/2; i++)
        if (i*getDigitProduct(i) == n)
            res.add(i);

    // If there was no seed
    if (res.size() == 0)
    {
        System.out.println("NO seed exists");
        return;
    }

    // Print seeds
    for (int i=0; i<res.size(); i++)
        System.out.print(res.get(i)+" ");
}

// Driver code
public static void main(String[] args)
{
    int n = 138;
    findSeed(n);

}
}
// this code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find Seed of a number

MAX = 10000;

prodDig = [0] * MAX;

# Stores product of digits of
# x in prodDig[x]
def getDigitProduct(x):

    # If x has single digit
    if (x < 10):
        return x;

    # If digit product is already computed
    if (prodDig[x] != 0):
        return prodDig[x];

    # If digit product is not computed before.
    prod = (int(x % 10) *
            getDigitProduct(int(x / 10)));

    prodDig[x] = prod;
    return prod;

# Prints all seeds of n
def findSeed(n):

    # Find all seeds using prodDig[]
    res = [];
    for i in range(1, int(n / 2 + 2)):
        if (i * getDigitProduct(i) == n):
            res.append(i);

    # If there was no seed
    if (len(res) == 0):
        print("NO seed exists");
        return;

    # Print seeds
    for i in range(len(res)):
        print(res[i], end = " ");

# Driver code
n = 138;
findSeed(n);

# This code is contributed by mits
```

## C#

```
// C# program to find Seed of a number
using System;
using System.Collections;

class GFG{

static int MAX = 10000;
static int[] prodDig=new int[MAX];

// Stores product of digits of x in prodDig[x]
static int getDigitProduct(int x)
{
    // If x has single digit
    if (x < 10)
    return x;

    // If digit product is already computed
    if (prodDig[x] != 0)
    return prodDig[x];

    // If digit product is not computed before.
    int prod = (x % 10) * getDigitProduct(x/10);

    return (prodDig[x] = prod);
}

// Prints all seeds of n
static void findSeed(int n)
{
    // Find all seeds using prodDig[]
    ArrayList res = new ArrayList();
    for (int i=1; i<=n/2; i++)
        if (i*getDigitProduct(i) == n)
            res.Add(i);

    // If there was no seed
    if (res.Count == 0)
    {
        Console.WriteLine("NO seed exists");
        return;
    }

    // Print seeds
    for (int i=0; i<res.Count; i++)
        Console.WriteLine(res[i]+" ");
}

// Driver code
static void Main()
{
    int n = 138;
    findSeed(n);

}
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Seed of a number

$MAX = 10000;

$prodDig = array_fill(0, $MAX, 0);

// Stores product of digits of x in prodDig[x]
function getDigitProduct($x)
{
    global $prodDig;

    // If x has single digit
    if ($x < 10)
    return $x;

    // If digit product is already computed
    if ($prodDig[$x] != 0)
    return $prodDig[$x];

    // If digit product is not computed before.
    $prod = (int)($x % 10) *
                  getDigitProduct((int)($x / 10));

    $prodDig[$x] = $prod;
    return $prod;
}

// Prints all seeds of n
function findSeed($n)
{
    // Find all seeds using prodDig[]
    $res = array();
    for ($i = 1; $i <= (int)($n / 2 + 1); $i++)
        if ($i * getDigitProduct($i) == $n)
            array_push($res, $i);

    // If there was no seed
    if (count($res) == 0)
    {
        echo "NO seed exists\n";
        return;
    }

    // Print seeds
    for ($i = 0; $i < count($res); $i++)
        echo $res[$i] . " ";
}

// Driver code
$n = 138;
findSeed($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find Seed of a number

var MAX = 10000;
var prodDig=Array.from({length: MAX}, (_, i) => 0);

// Stores product of digits of x in prodDig[x]
function getDigitProduct(x)
{
    // If x has single digit
    if (x < 10)
    return x;

    // If digit product is already computed
    if (prodDig[x] != 0)
    return prodDig[x];

    // If digit product is not computed before.
    var prod = (x % 10) *
    getDigitProduct(parseInt(x/10));

    return (prodDig[x] = prod);
}

// Prints all seeds of n
function findSeed(n)
{
    // Find all seeds using prodDig
    var res = [];

    for (var i=1; i<=parseInt(n/2); i++)
        if (i*getDigitProduct(i) == n)
            res.push(i);

    // If there was no seed
    if (res.length == 0)
    {
        document.write("NO seed exists");
        return;
    }

    // Print seeds
    for (i=0; i<res.length; i++)
        document.write(res[i]+" ");
}

// Driver code
var n = 138;
findSeed(n);

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
23
```

**进一步优化:**
我们可以进一步优化上面的代码。这个想法是，只有当我能被 n 整除时，才能调用 getDigitProduct(i)，具体实现请参考[https://ide.geeksforgeeks.org/oLYduu](https://ide.geeksforgeeks.org/oLYduu)。
本文由[拉克什·库马尔](https://www.facebook.com/Rakesh2raj)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。