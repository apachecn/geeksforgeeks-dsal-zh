# 检查一个数字奇数位的位数之和是否能被 K 整除

> 原文:[https://www . geeksforgeeks . org/check-数字奇数位的数字总和是否可被 k 整除/](https://www.geeksforgeeks.org/check-whether-sum-of-digits-at-odd-places-of-a-number-is-divisible-by-k/)

给定两个整数‘N’和‘K’，任务是找出‘N’在其奇数位(从右到左)的位数之和，并检查该和是否能被‘K’整除。如果可分，输出*是*，否则输出*否*。

**示例:**

> **输入:** N = 4325，K = 4
> **输出:** YES
> 自，3 + 5 = 8，可被 4 整除。
> 
> **输入:** N = 1209，K = 3
> T3】输出:否

**进场:**

*   求奇数位(从右到左)的“N”位数之和。
*   然后通过取其与“K”的模来检查和的可除性。
*   如果它是可分的，则输出“是”，否则输出“否”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// function that checks the
// divisibility of the sum
// of the digits at odd places
// of the given number
bool SumDivisible(int n, int k)
{
    int sum = 0, position = 1;
    while (n > 0) {

        // if position is odd
        if (position % 2 == 1)
            sum += n % 10;
        n = n / 10;
        position++;
    }

    if (sum % k == 0)
        return true;
    return false;
}

// Driver code
int main()
{
    int n = 592452;
    int k = 3;

    if (SumDivisible(n, k))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// function that checks the
// divisibility of the sum
// of the digits at odd places
// of the given number
static boolean SumDivisible(int n, int k)
{
    int sum = 0, position = 1;
    while (n > 0) {

        // if position is odd
        if (position % 2 == 1)
            sum += n % 10;
        n = n / 10;
        position++;
    }

    if (sum % k == 0)
        return true;
    return false;
}

// Driver code
public static void main(String arr[])
{
    int n = 592452;
    int k = 3;

    if (SumDivisible(n, k))
        System.out.println("YES");
    else
        System.out.println("NO");

}
}
//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# function that checks the divisibility
# of the sum of the digits at odd places
# of the given number
def SumDivisible(n, k):

    sum = 0
    position = 1
    while (n > 0) :

        # if position is odd
        if (position % 2 == 1):
            sum += n % 10
        n = n // 10
        position += 1

    if (sum % k == 0):
        return True
    return False

# Driver code
if __name__ =="__main__":
    n = 592452
    k = 3

    if (SumDivisible(n, k)):
        print("YES")
    else:
        print("NO")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// function that checks the
// divisibility of the sum
// of the digits at odd places
// of the given number
static bool SumDivisible(int n, int k)
{
    int sum = 0, position = 1;
    while (n > 0)
    {

        // if position is odd
        if (position % 2 == 1)
            sum += n % 10;
        n = n / 10;
        position++;
    }

    if (sum % k == 0)
        return true;
    return false;
}

// Driver code
static public void Main ()
{
    int n = 592452;
    int k = 3;

    if (SumDivisible(n, k))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// function that checks the divisibility
// of the sum of the digits at odd places
// of the given number
function SumDivisible($n, $k)
{
    $sum = 0;
    $position = 1;
    while ($n > 0)
    {

        // if position is odd
        if ($position % 2 == 1)
            $sum += $n % 10;
        $n = (int)$n / 10;
        $position++;
    }

    if ($sum % $k == 0)
        return true;
    return false;
}

// Driver code
$n = 592452;
$k = 3;

if (SumDivisible($n, $k))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// function that checks the
// divisibility of the sum
// of the digits at odd places
// of the given number
function SumDivisible(n, k)
{
    let sum = 0, position = 1;
    while (n > 0) {

        // if position is odd
        if (position % 2 == 1)
            sum += n % 10;
        n = Math.floor(n / 10);
        position++;
    }

    if (sum % k == 0)
        return true;
    return false;
}

// Driver code

    let n = 592452;
    let k = 3;

    if (SumDivisible(n, k))
        document.write("YES");
    else
        document.write("NO");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
YES
```

#### 方法 2:使用 string()方法:

1.  将整数转换为字符串，然后遍历该字符串，并通过将其存储在 sum 中来查找所有奇数索引的总和。
2.  如果总和能被 k 整除，则返回真否则返回假。

下面是实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

bool sumDivisible(int n, int k)
{
    int sum = 0;

    // Converting integer to string
    string num = to_string(n);
    int i;

    // Traversing the string
    for (i = 0; i < num.size(); i++) {
        if (i % 2 != 0) {
            sum = sum + (num[i] - '0');
        }
    }

    if (sum % k == 0) {
        return true;
    }
    else {
        return false;
    }
}

// Driver code
int main()
{
    int n = 592452;
    int k = 3;
    if (sumDivisible(n, k)) {
        cout << ("YES");
    }
    else {
        cout << ("NO");
    }
    return 0;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.io.*;
class GFG
{
static boolean sumDivisible(int n, int k)
{
    int sum = 0;

    // Converting integer to string
    String num = Integer.toString(n);
    int i;

    // Traversing the string
    for (i = 0; i < num.length(); i++) {
        if (i % 2 != 0) {
            sum = sum + (num.charAt(i) - '0');
        }
    }

    if (sum % k == 0) {
        return true;
    }
    else {
        return false;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 592452;
    int k = 3;
    if (sumDivisible(n, k)) {
        System.out.println("YES");
    }
    else {
        System.out.println("NO");
    }
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

def sumDivisible(n, k):
    sum = 0

    # Converting integer to string
    num = str(n)

    # Traversing the string
    for i in range(len(num)):
        if(i % 2 != 0):
            sum = sum+int(num[i])

    if sum % k == 0:
        return True
    return False

# Driver code
n = 592452
k = 3
if sumDivisible(n, k) == True:
    print("YES")
else:
    print("NO")

# This code is contributed by vikkycirus
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG
{
static bool sumDivisible(int n, int k)
{
    int sum = 0;

    // Converting integer to string
    string num = n.ToString();
    int i;

    // Traversing the string
    for (i = 0; i < num.Length; i++) {
        if (i % 2 != 0) {
            sum = sum + (num[i] - '0');
        }
    }

    if (sum % k == 0) {
        return true;
    }
    else {
        return false;
    }
}

// Driver code
static public void Main ()
{
    int n = 592452;
    int k = 3;
    if (sumDivisible(n, k)) {
        Console.Write("YES");
    }
    else {
        Console.Write("NO");
    }
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// javascript implementation of the
// above approach

function sumDivisible(n, k){
    var sum = 0

    // Converting integer to string
    var num = n.toString()

    // Traversing the string
    for(var i=0 ; i < num.length ; i++) {
        if(i % 2 != 0) {
            sum = sum + Number(num[i])
        }
    }

    if (sum % k == 0){
        return true;
    }
    else{
    return false;
    }
}

// Driver code
var n = 592452
var k = 3
if(sumDivisible(n, k)){
    document.write("YES");
}
else{
    document.write("NO");
}

</script>
```

**输出:**

```
Yes
```