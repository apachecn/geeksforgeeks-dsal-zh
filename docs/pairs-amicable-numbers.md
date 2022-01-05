# 友好号码对

> 原文:[https://www.geeksforgeeks.org/pairs-amicable-numbers/](https://www.geeksforgeeks.org/pairs-amicable-numbers/)

给定一个整数数组，打印数组中形成[友好对](https://en.wikipedia.org/wiki/Amicable_numbers)的对的数量。如果第一个数等于第二个数的除数之和，如果第二个数等于第一个数的除数之和，则两个数是友好的。
**例:**

```
Input  : arr[] = {220, 284, 1184, 1210, 2, 5}
Output : 2
Explanation : (220, 284) and (1184, 1210) 
              form amicable pair

Input  : arr[] = {2620, 2924, 5020, 5564, 6232, 6368}
Output : 3
Explanation : (2620, 2924), (5020, 5564) and (6232, 6368)
              forms amicable pair
```

一个简单的解决方案是遍历每一对，检查它们是否形成友好的一对，如果是，我们增加计数。

## C++

```
// A simple C++ program to count
// amicable pairs in an array.
#include <bits/stdc++.h>
using namespace std;

// Calculate the sum
// of proper divisors
int sumOfDiv(int x)
{
    // 1 is a proper divisor
    int sum = 1;
    for (int i = 2; i <= sqrt(x); i++)
    {
        if (x % i == 0)
        {
            sum += i;

            // To handle perfect squares
            if (x / i != i)
                sum += x / i;
        }
    }
    return sum;
}

// Check if pair is amicable
bool isAmicable(int a, int b)
{
    return (sumOfDiv(a) == b &&
            sumOfDiv(b) == a);
}

// This function prints pair
// of amicable pairs present
// in the input array
int countPairs(int arr[], int n)
{
    int count = 0;

    // Iterate through each
    // pair, and find if it
    // an amicable pair
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (isAmicable(arr[i], arr[j]))
                count++;

    return count;
}

// Driver code
int main()
{
    int arr1[] = { 220, 284, 1184,
                   1210, 2, 5 };
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    cout << countPairs(arr1, n1)
         << endl;

    int arr2[] = { 2620, 2924, 5020,
                   5564, 6232, 6368 };
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    cout << countPairs(arr2, n2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to count
// amicable pairs in an array.
import java.io.*;

class GFG
{

    // Calculate the sum
    // of proper divisors
    static int sumOfDiv(int x)
    {

        // 1 is a proper divisor
        int sum = 1;
        for (int i = 2; i <= Math.sqrt(x); i++)
        {
            if (x % i == 0)
            {
                sum += i;

                // To handle perfect squares
                if (x / i != i)
                    sum += x / i;
            }
        }

        return sum;
    }

    // Check if pair is amicable
    static boolean isAmicable(int a, int b)
    {
        return (sumOfDiv(a) == b &&
                sumOfDiv(b) == a);
    }

    // This function prints pair
    //  of amicable pairs present
    // in the input array
    static int countPairs(int arr[], int n)
    {
        int count = 0;

        // Iterate through each pair,
        // and find if it an amicable pair
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (isAmicable(arr[i], arr[j]))
                    count++;

        return count;
    }

    // Driver code
    public static void main(String args[])
    {

        int arr1[] = { 220, 284, 1184,
                       1210, 2, 5 };
        int n1 = arr1.length;

        System.out.println(countPairs(arr1, n1));

        int arr2[] = { 2620, 2924, 5020,
                       5564, 6232, 6368 };
        int n2 = arr2.length;

        System.out.println(countPairs(arr2, n2));
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python3 program to count
# amicable pairs in an array

# Calculate the sum
# of proper divisors
def sumOfDiv(x):
    sum = 1
    for i in range(2, x):
        if x % i == 0:
            sum += i
    return sum

# Check if pair is amicable
def isAmicable(a, b):
    if sumOfDiv(a) == b and sumOfDiv(b) == a:
        return True
    else:
        return False

# This function prints pair
# of amicable pairs present
# in the input array
def countPairs(arr, n):
    count = 0
    for i in range(0, n):
        for j in range(i + 1, n):
            if isAmicable(arr[i], arr[j]):
                count = count + 1
    return count

# Driver Code
arr1 = [220, 284, 1184,
        1210, 2, 5]
n1 = len(arr1)
print(countPairs(arr1, n1))

arr2 = [2620, 2924, 5020,
        5564, 6232, 6368]
n2 = len(arr2)
print(countPairs(arr2, n2))

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// A simple C# program to count
// amicable pairs in an array.
using System;

class GFG
{

    // Calculate the sum
    // of proper divisors
    static int sumOfDiv(int x)
    {

        // 1 is a proper divisor
        int sum = 1;
        for (int i = 2; i <= Math.Sqrt(x); i++)
        {
            if (x % i == 0)
            {
                sum += i;

                // To handle perfect squares
                if (x / i != i)
                    sum += x / i;
            }
        }

        return sum;
    }

    // Check if pair is amicable
    static bool isAmicable(int a, int b)
    {
        return (sumOfDiv(a) == b &&
                sumOfDiv(b) == a);
    }

    // This function prints pair
    // of amicable pairs present
    // in the input array
    static int countPairs(int []arr, int n)
    {
        int count = 0;

        // Iterate through each pair,
        // and find if it an amicable pair
        for (int i = 0; i < n; i++)

            for (int j = i + 1; j < n; j++)
                if (isAmicable(arr[i], arr[j]))
                    count++;

        return count;
    }

    // Driver code
    public static void Main()
    {

        int []arr1 = {220, 284, 1184,
                      1210, 2, 5};
        int n1 = arr1.Length;

        Console.WriteLine(countPairs(arr1, n1));

        int []arr2 = {2620, 2924, 5020,
                      5564, 6232, 6368};
        int n2 = arr2.Length;

        Console.WriteLine(countPairs(arr2, n2));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to count
// amicable pairs in an array.

// Calculate the sum
// of proper divisors
function sumOfDiv( $x)
{
    // 1 is a proper divisor
    $sum = 1;
    for ( $i = 2; $i <= sqrt($x); $i++)
    {
        if ($x % $i == 0)
        {
            $sum += $i;

            // To handle perfect squares
            if ($x / $i != $i)
                $sum += $x / $i;
        }
    }
    return $sum;
}

// Check if pair is amicable
function isAmicable( $a, $b)
{
    return (sumOfDiv($a) == $b and
            sumOfDiv($b) == $a);
}

// This function prints pair
// of amicable pairs present
// in the input array
function countPairs( $arr, $n)
{
    $count = 0;

    // Iterate through each pair,
    // and find if it an amicable pair
    for ( $i = 0; $i < $n; $i++)
        for ( $j = $i + 1; $j < $n; $j++)
            if (isAmicable($arr[$i], $arr[$j]))
                $count++;

    return $count;
}

// Driver code
$arr1 = array( 220, 284, 1184,
               1210, 2, 5 );
$n1 = count($arr1);
echo countPairs($arr1, $n1),"\n";

$arr2 = array( 2620, 2924, 5020,
               5564, 6232, 6368 );
$n2 = count($arr2);
echo countPairs($arr2, $n2);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // A simple Javascript program to count
    // amicable pairs in an array.

    // Calculate the sum
    // of proper divisors
    function sumOfDiv(x)
    {

        // 1 is a proper divisor
        let sum = 1;
        for (let i = 2; i <= Math.sqrt(x); i++)
        {
            if (x % i == 0)
            {
                sum += i;

                // To handle perfect squares
                if (parseInt(x / i, 10) != i)
                    sum += parseInt(x / i, 10);
            }
        }

        return sum;
    }

    // Check if pair is amicable
    function isAmicable(a, b)
    {
        return (sumOfDiv(a) == b &&
                sumOfDiv(b) == a);
    }

    // This function prints pair
    // of amicable pairs present
    // in the input array
    function countPairs(arr, n)
    {
        let count = 0;

        // Iterate through each pair,
        // and find if it an amicable pair
        for (let i = 0; i < n; i++)

            for (let j = i + 1; j < n; j++)
                if (isAmicable(arr[i], arr[j]))
                    count++;

        return count;
    }

    let arr1 = [220, 284, 1184, 1210, 2, 5];
    let n1 = arr1.length;

    document.write(countPairs(arr1, n1) + "</br>");

    let arr2 = [2620, 2924, 5020, 5564, 6232, 6368];
    let n2 = arr2.length;

    document.write(countPairs(arr2, n2));

</script>
```

**输出:**

```
2
3
```

一个**有效的解决方案**是将数字保存在一个地图中，对于每个数字，我们找到其适当除数的和，并检查它是否也存在于数组中。如果存在，我们可以检查它们是否构成友好的一对。
这样，复杂性将大大降低。下面是同样的 C++程序。

## C++

```
// Efficient C++ program to count
// Amicable pairs in an array.
#include <bits/stdc++.h>
using namespace std;

// Calculate the sum
// of proper divisors
int sumOfDiv(int x)
{
    // 1 is a proper divisor
    int sum = 1;
    for (int i = 2; i <= sqrt(x); i++)
    {
        if (x % i == 0) {
            sum += i;

            // To handle perfect squares
            if (x / i != i)
                sum += x / i;
        }
    }
    return sum;
}

// Check if pair is amicable
bool isAmicable(int a, int b)
{
    return (sumOfDiv(a) == b &&
            sumOfDiv(b) == a);
}

// This function prints count
// of amicable pairs present
// in the input array
int countPairs(int arr[], int n)
{
    // Map to store the numbers
    unordered_set<int> s;
    int count = 0;
    for (int i = 0; i < n; i++)
        s.insert(arr[i]);

    // Iterate through each number,
    // and find the sum of proper
    // divisors and check if it's
    // also present in the array
    for (int i = 0; i < n; i++)
    {
        if (s.find(sumOfDiv(arr[i])) != s.end())
        {
            // It's sum of proper divisors
            int sum = sumOfDiv(arr[i]);
            if (isAmicable(arr[i], sum))
                count++;
        }
    }

    // As the pairs are counted
    // twice, thus divide by 2
    return count / 2;
}

// Driver code
int main()
{
    int arr1[] = { 220, 284, 1184,
                   1210, 2, 5 };
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    cout << countPairs(arr1, n1)
         << endl;

    int arr2[] = { 2620, 2924, 5020,
                   5564, 6232, 6368 };
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    cout << countPairs(arr2, n2)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to count
// Amicable pairs in an array.
import java.util.*;

class GFG
{

// Calculate the sum
// of proper divisors
static int sumOfDiv(int x)
{
    // 1 is a proper divisor
    int sum = 1;
    for (int i = 2; i <= Math.sqrt(x); i++)
    {
        if (x % i == 0)
        {
            sum += i;

            // To handle perfect squares
            if (x / i != i)
                sum += x / i;
        }
    }
    return sum;
}

// Check if pair is amicable
static boolean isAmicable(int a, int b)
{
    return (sumOfDiv(a) == b &&
            sumOfDiv(b) == a);
}

// This function prints count
// of amicable pairs present
// in the input array
static int countPairs(int arr[], int n)
{
    // Map to store the numbers
    HashSet<Integer> s = new HashSet<Integer>();
    int count = 0;
    for (int i = 0; i < n; i++)
        s.add(arr[i]);

    // Iterate through each number,
    // and find the sum of proper
    // divisors and check if it's
    // also present in the array
    for (int i = 0; i < n; i++)
    {
        if (s.contains(sumOfDiv(arr[i])))
        {
            // It's sum of proper divisors
            int sum = sumOfDiv(arr[i]);
            if (isAmicable(arr[i], sum))
                count++;
        }
    }

    // As the pairs are counted
    // twice, thus divide by 2
    return count / 2;
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 220, 284, 1184,
                   1210, 2, 5 };
    int n1 = arr1.length;
    System.out.println(countPairs(arr1, n1));

    int arr2[] = { 2620, 2924, 5020,
                   5564, 6232, 6368 };
    int n2 = arr2.length;
    System.out.println(countPairs(arr2, n2));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Efficient Python3 program to count
# Amicable pairs in an array.
import math

# Calculating the sum
# of proper divisors
def sumOfDiv(x):

    # 1 is a proper divisor
    sum = 1;
    for i in range(2,int(math.sqrt(x))):
        if x % i==0:
            sum += i

            # To handle perfect squares
            if i != x/i:
                sum += x/i
    return int(sum);

# check if pair is ambicle
def isAmbicle(a, b):
    return (sumOfDiv(a) == b and
            sumOfDiv(b) == a)

# This function prints count
# of amicable pairs present
# in the input array
def countPairs(arr,n):

    # Map to store the numbers
    s = set()
    count = 0
    for i in range(n):
        s.add(arr[i])

    # Iterate through each number,
    # and find the sum of proper
    # divisors and check if it's
    # also present in the array
    for i in range(n):    
        if sumOfDiv(arr[i]) in s:

            # It's sum of proper divisors
            sum = sumOfDiv(arr[i])
            if isAmbicle(arr[i], sum):
                count += 1       

    # As the pairs are counted
    # twice, thus divide by 2
    return int(count/2);

# Driver Code
arr1 = [220, 284, 1184,
        1210, 2, 5]
n1 = len(arr1)
print(countPairs(arr1, n1))

arr2 = [2620, 2924, 5020,
        5564, 6232, 6368]
n2 = len(arr2)
print(countPairs(arr2, n2))

# This code is contributed
# by Naveen Babbar
```

## C#

```
// Efficient C# program to count
// Amicable pairs in an array.
using System;
using System.Collections.Generic;

class GFG
{

// Calculate the sum
// of proper divisors
static int sumOfDiv(int x)
{
    // 1 is a proper divisor
    int sum = 1;
    for (int i = 2; i <= Math.Sqrt(x); i++)
    {
        if (x % i == 0)
        {
            sum += i;

            // To handle perfect squares
            if (x / i != i)
                sum += x / i;
        }
    }
    return sum;
}

// Check if pair is amicable
static Boolean isAmicable(int a, int b)
{
    return (sumOfDiv(a) == b &&
            sumOfDiv(b) == a);
}

// This function prints count
// of amicable pairs present
// in the input array
static int countPairs(int []arr, int n)
{
    // Map to store the numbers
    HashSet<int> s = new HashSet<int>();
    int count = 0;
    for (int i = 0; i < n; i++)
        s.Add(arr[i]);

    // Iterate through each number,
    // and find the sum of proper
    // divisors and check if it's
    // also present in the array
    for (int i = 0; i < n; i++)
    {
        if (s.Contains(sumOfDiv(arr[i])))
        {
            // It's sum of proper divisors
            int sum = sumOfDiv(arr[i]);
            if (isAmicable(arr[i], sum))
                count++;
        }
    }

    // As the pairs are counted
    // twice, thus divide by 2
    return count / 2;
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = { 220, 284, 1184,
                   1210, 2, 5 };
    int n1 = arr1.Length;
    Console.WriteLine(countPairs(arr1, n1));

    int []arr2 = { 2620, 2924, 5020,
                   5564, 6232, 6368 };
    int n2 = arr2.Length;
    Console.WriteLine(countPairs(arr2, n2));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

//  JavaScript program to count
// Amicable pairs in an array.

// Calculate the sum
// of proper divisors
function sumOfDiv(x)
{
    // 1 is a proper divisor
    let sum = 1;
    for (let i = 2; i <= Math.sqrt(x); i++)
    {
        if (x % i == 0)
        {
            sum += i;

            // To handle perfect squares
            if (x / i != i)
                sum += x / i;
        }
    }
    return sum;
}

// Check if pair is amicable
function isAmicable(a, b)
{
    return (sumOfDiv(a) == b &&
            sumOfDiv(b) == a);
}

// This function prlets count
// of amicable pairs present
// in the input array
function countPairs(arr, n)
{
    // Map to store the numbers
    let s = new Set();
    let count = 0;
    for (let i = 0; i < n; i++)
        s.add(arr[i]);

    // Iterate through each number,
    // and find the sum of proper
    // divisors and check if it's
    // also present in the array
    for (let i = 0; i < n; i++)
    {
        if (s.has(sumOfDiv(arr[i])))
        {
            // It's sum of proper divisors
            let sum = sumOfDiv(arr[i]);
            if (isAmicable(arr[i], sum))
                count++;
        }
    }

    // As the pairs are counted
    // twice, thus divide by 2
    return  Math.floor(count / 2);
}

    // Driver code    

    let arr1 = [ 220, 284, 1184,
                   1210, 2, 5 ];
    let n1 = arr1.length;
    document.write(countPairs(arr1, n1) + "<br/>");

    let arr2 = [ 2620, 2924, 5020,
                   5564, 6232, 6368 ];
    let n2 = arr2.length;
    document.write(countPairs(arr2, n2) + "<br/>");

</script>
```

**输出:**

```
2
3
```

本文由 [**Ashutosh Kumar**](https://in.linkedin.com/in/ashutosh-kumar-9527a7105) 投稿，如果你喜欢 GeeksforGeeks 并且愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。