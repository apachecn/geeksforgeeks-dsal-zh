# 计算给定二进制数组中可被 x 整除的所有前缀

> 原文:[https://www . geesforgeks . org/count-给定二进制数组中可被 x 整除的所有前缀/](https://www.geeksforgeeks.org/count-all-prefixes-of-the-given-binary-array-which-are-divisible-by-x/)

给定一个二进制数组 **arr[]** 和一个整数 **x** ，任务是计算给定数组中可被 **x** 整除的所有前缀。
**注:**从 **arr[0]** 到 **arr[i]** 的 i <sup>th</sup> 前缀解释为二进制数(从最高有效位到最低有效位。)
**例:**

> **输入:** arr[] = {0，1，0，1，1}，x = 5
> **输出:**2
> 0 = 0
> 01 = 1
> 010 = 2
> 0101 = 5
> 01011 = 11
> 0 和 0101 是唯一可被 5 整除的前缀。
> **输入:** arr[] = {1，0，1，0，1，1，0}，x = 2
> **输出:** 3

**天真方法:**从 **0** 迭代到 **i** 将每个二进制前缀转换为十进制，并检查该数是否可被 **x** 整除。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of total
// binary prefix which are divisible by x
int CntDivbyX(int arr[], int n, int x)
{

    // Initialize with zero
    int number = 0;
    int count = 0;

    for (int i = 0; i < n; i++) {

        // Convert all prefixes to decimal
        number = number * 2 + arr[i];

        // If number is divisible by x
        // then increase count
        if ((number % x == 0))
            count += 1;
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 1, 0, 1, 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 2;
    cout << CntDivbyX(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

    // Function to return the count of total
    // binary prefix which are divisible by x
    static int CntDivbyX(int arr[], int n, int x)
    {

        // Initialize with zero
        int number = 0;
        int count = 0;

        for (int i = 0; i < n; i++)
        {

            // Convert all prefixes to decimal
            number = number * 2 + arr[i];

            // If number is divisible by x
            // then increase count
            if ((number % x == 0))
                count += 1;
        }

        return count;
    }

    // Driver Code
    public static void main(String []args)
    {

        int arr[] = { 1, 0, 1, 0, 1, 1, 0 };
        int n = arr.length;
        int x = 2;
        System.out.println(CntDivbyX(arr, n, x));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count of total
# binary prefix which are divisible by x
def CntDivbyX(arr, n, x):

    # Initialize with zero
    number = 0
    count = 0

    for i in range(n):

        # Convert all prefixes to decimal
        number = number * 2 + arr[i]

        # If number is divisible by x
        # then increase count
        if ((number % x == 0)):
            count += 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [1, 0, 1, 0, 1, 1, 0]
    n = len(arr)
    x = 2
    print(CntDivbyX(arr, n, x))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the count of total
    // binary prefix which are divisible by x
    static int CntDivbyX(int[] arr, int n, int x)
    {

        // Initialize with zero
        int number = 0;
        int count = 0;

        for (int i = 0; i < n; i++)
        {

            // Convert all prefixes to decimal
            number = number * 2 + arr[i];

            // If number is divisible by x
            // then increase count
            if ((number % x == 0))
                count += 1;
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {

        int[] arr = { 1, 0, 1, 0, 1, 1, 0 };
        int n = arr.Length;
        int x = 2;
        Console.WriteLine(CntDivbyX(arr, n, x));
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of total
// binary prefix which are divisible by x
function CntDivbyX($arr, $n, $x)
{

    // Initialize with zero
    $number = 0;
    $count = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Convert all prefixes to decimal
        $number = $number * 2 + $arr[$i];

        // If number is divisible by x
        // then increase count
        if (($number % $x == 0))
            $count += 1;
    }

    return $count;
}

// Driver code
$arr = array(1, 0, 1, 0, 1, 1, 0);
$n = sizeof($arr);
$x = 2;
echo CntDivbyX($arr, $n, $x);

// This code is contributed by Akanksha Rai
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of total
// binary prefix which are divisible by x
function CntDivbyX(arr, n, x)
{

    // Initialize with zero
    let number = 0;
    let count = 0;

    for (let i = 0; i < n; i++) {

        // Convert all prefixes to decimal
        number = number * 2 + arr[i];

        // If number is divisible by x
        // then increase count
        if ((number % x == 0))
            count += 1;
    }

    return count;
}

// Driver code
    let arr = [ 1, 0, 1, 0, 1, 1, 0 ];
    let n = arr.length;
    let x = 2;
    document.write(CntDivbyX(arr, n, x));

</script>
```

**Output:** 

```
3
```

**高效方法:**正如我们在上面的方法中看到的，我们将每个二进制前缀转换为十进制数，如 **0，01，010，0101……。**但是随着 n(数组的大小)值的增加，结果数将会非常大，no 将超出数据类型的范围，因此我们可以利用模块化属性。
代替做 **number = number * 2 + arr[ i ]** ，我们可以做得更好作为**number =(number * 2+arr[I])% x**
**说明:**我们从 **number = 0** 开始，反复做 **number = number * 2 + arr[ i ]** ，然后在每次迭代中我们会得到上述序列的一个新项。

> A = {1，0，1，0，1，1，0 }
> “1”= 0 * 2+1 = 1
> “10”= 1 * 2+0 = 2
> “101”= 2 * 2+1 = 5
> “1010”= 5 * 2+0 = 10
> “10101”= 10 * 2+1 = 21
> “101011”= 21 * 2+1 = 43
> “11

因为我们在每一步都重复地取这个数的余数，所以在每一步，我们都有， **newNum = oldNum * 2 + arr[i]** 。根据模运算规则 **(a * b + c) % m** 与 **((a * b) % m + c % m) % m** 相同。所以不管 **oldNum** 是余数还是原数，答案都是正确的。
注:类似文章在此讨论。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of total
// binary prefix which are divisible by x
int CntDivbyX(int arr[], int n, int x)
{

    // Initialize with zero
    int number = 0;
    int count = 0;

    for (int i = 0; i < n; i++) {

        // Instead of converting all prefixes
        // to decimal, take reminder with x
        number = (number * 2 + arr[i]) % x;

        // If number is divisible by x
        // then reminder = 0
        if (number == 0)
            count += 1;
    }

    return count;
}

// Driver code
int main()
{

    int arr[] = { 1, 0, 1, 0, 1, 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 2;
    cout << CntDivbyX(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of total
    // binary prefix which are divisible by x
    public static int CntDivbyX(int arr[], int n, int x)
    {

        // Initialize with zero
        int number = 0;
        int count = 0;

        for (int i = 0; i < n; i++) {

            // Instead of converting all prefixes
            // to decimal, take reminder with x
            number = (number * 2 + arr[i]) % x;

            // If number is divisible by x
            // then reminder = 0
            if (number == 0)
                count += 1;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 0, 1, 0, 1, 1, 0 };
        int n = 7;
        int x = 2;
        System.out.print(CntDivbyX(arr, n, x));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of total
# binary prefix which are divisible by x
def CntDivbyX(arr, n, x):

    number = 0

    count = 0

    for i in range (0, n):

        # Instead of converting all prefixes
        # to decimal, take reminder with x
        number = ( number * 2 + arr[i] ) % x

        # If number is divisible by x
        # then reminder = 0
        if number == 0:
            count += 1

    return count

# Driver code
arr = [1, 0, 1, 0, 1, 1, 0]
n = 7
x = 2
print( CntDivbyX(arr, n, x) )
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of total
    // binary prefix which are divisible by x
    public static int CntDivbyX(int []arr, int n, int x)
    {

        // Initialize with zero
        int number = 0;
        int count = 0;

        for (int i = 0; i < n; i++)
        {

            // Instead of converting all prefixes
            // to decimal, take reminder with x
            number = (number * 2 + arr[i]) % x;

            // If number is divisible by x
            // then reminder = 0
            if (number == 0)
                count += 1;
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 0, 1, 0, 1, 1, 0 };
        int n = 7;
        int x = 2;

        Console.Write(CntDivbyX(arr, n, x));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of total
// binary prefix which are divisible by x
function CntDivbyX($arr, $n, $x)
{

    // Initialize with zero
    $number = 0;
    $count1 = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Instead of converting all prefixes
        // to decimal, take reminder with x
        $number = ($number * 2 + $arr[$i]) % $x;

        // If number is divisible by x
        // then reminder = 0
        if ($number == 0)
            $count1 += 1;
    }

    return $count1;
}

// Driver code
$arr = array(1, 0, 1, 0, 1, 1, 0);
$n = sizeof($arr);
$x = 2;
echo CntDivbyX($arr, $n, $x);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of total
// binary prefix which are divisible by x
function CntDivbyX(arr, n, x)
{

    // Initialize with zero
    let number = 0;
    let count = 0;

    for (let i = 0; i < n; i++) {

        // Instead of converting all prefixes
        // to decimal, take reminder with x
        number = (number * 2 + arr[i]) % x;

        // If number is divisible by x
        // then reminder = 0
        if (number == 0)
            count += 1;
    }

    return count;
}

// Driver code

    let arr = [ 1, 0, 1, 0, 1, 1, 0 ];
    let n = arr.length;
    let x = 2;
    document.write(CntDivbyX(arr, n, x));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)