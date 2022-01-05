# 寻找隐藏号码的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-hidden-number/](https://www.geeksforgeeks.org/program-to-find-the-hidden-number/)

给定一个由![n   ](img/9568f18f8a74cc2f215afd053ad828dd.png "Rendered by QuickLaTeX.com")个整数组成的数组，任务是找到另一个整数![x   ](img/7af94c6fbe791dbc443f7dd499ff3372.png "Rendered by QuickLaTeX.com")，这样，如果数组中的所有元素都从数字![x   ](img/7af94c6fbe791dbc443f7dd499ff3372.png "Rendered by QuickLaTeX.com")中单独减去，那么所有差值的总和应该等于 0。如果有这样的整数，打印![x   ](img/7af94c6fbe791dbc443f7dd499ff3372.png "Rendered by QuickLaTeX.com")的值，否则打印![-1   ](img/08cd7dd9fe8c5a6ffb3e0afce0fed36f.png "Rendered by QuickLaTeX.com")。
**例**

```
Input: arr[] = {1, 2, 3}
Output: 2
Explanation: 
Substracting all the elements of arrays from 2,
The sum of difference is:
1 + 0 + (-1) = 0.
```

**解法**:思路是计算数组的总和，除以数组的大小。如果数组的和完全可以被它的大小整除，那么从这个除法运算中得到的商就是所需的隐藏数。
以下是上述思路的实现:

## C++

```
// C++ Program to find the
// hidden number

#include <iostream>
using namespace std;

    // Driver Code

int main() {
        // Getting the size of array
        int n = 3;

        // Getting the array of size n
        int a[] = { 1, 2, 3 };

        // Solution
        int i = 0;

        // Finding sum of the array elements
        long sum = 0;
        for (i = 0; i < n; i++) {
            sum += a[i];
        }

        // Dividing sum by size n
        long x = sum / n;

        // Print x, if found
        if (x * n == sum)
            cout<<x<<endl;
        else
            cout<<("-1")<<endl;

    return 0;
    // This code is contributed
// by shashank
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// hidden number

public class GFG {

    // Driver Code
    public static void main(String args[])
    {

        // Getting the size of array
        int n = 3;

        // Getting the array of size n
        int a[] = { 1, 2, 3 };

        // Solution
        int i = 0;

        // Finding sum of the array elements
        long sum = 0;
        for (i = 0; i < n; i++) {
            sum += a[i];
        }

        // Dividing sum by size n
        long x = sum / n;

        // Print x, if found
        if (x * n == sum)
            System.out.println(x);
        else
            System.out.println("-1");
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to find the
# hidden number

# Driver Code
if __name__ == "__main__":

    # Getting the size of array
    n = 3

    # Getting the array of size n
    a = [ 1, 2, 3 ]

    # Solution
    i = 0

    # Finding sum of the .
    # array elements
    sum = 0
    for i in range(n):
        sum += a[i]

    # Dividing sum by size n
    x = sum // n

    # Print x, if found
    if (x * n == sum):
        print(x)
    else:
        print("-1")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# Program to find the
// hidden number
using System;

class GFG
{

// Driver Code
public static void Main()
{

    // Getting the size of array
    int n = 3;

    // Getting the array of size n
    int []a = { 1, 2, 3 };

    // Solution
    int i = 0;

    // Finding sum of the
    // array elements
    long sum = 0;
    for (i = 0; i < n; i++)
    {
        sum += a[i];
    }

    // Dividing sum by size n
    long x = sum / n;

    // Print x, if found
    if (x * n == sum)
        Console.WriteLine(x);
    else
        Console.WriteLine("-1");
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// hidden number

// Driver Code

// Getting the size of array
$n = 3;

// Getting the array of size n
$a = array( 1, 2, 3 );

// Solution
$i = 0;

// Finding sum of the array elements
$sum = 0;
for ($i = 0; $i < $n; $i++)
{
    $sum += $a[$i];
}

// Dividing sum by size n
$x = $sum / $n;

// Print x, if found
if ($x * $n == $sum)
echo($x);
else
echo("-1");

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find the
// hidden number

    // Driver Code
    // Getting the size of array
    let n = 3;
    // Getting the array of size n
    let a=[1, 2, 3];

    // Solution
    let i = 0;

    // Finding sum of the array elements
    let sum = 0;
    for (i = 0; i < n; i++) {
            sum += a[i];
        }

        // Dividing sum by size n
        let x = sum / n;

        // Print x, if found
        if (x * n == sum)
            document.write(x);
        else
            document.write("-1");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```