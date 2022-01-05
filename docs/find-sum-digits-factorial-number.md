# 求一个数的阶乘的位数之和

> 原文:[https://www . geesforgeks . org/find-sum-digits-factorial-number/](https://www.geeksforgeeks.org/find-sum-digits-factorial-number/)

给定一个数字 n，编写代码来计算这个数字的阶乘中的数字总和。给定 n ≤ 5000

**示例:**

```
Input : 10
Output : 27

Input : 100
Output : 648
```

不可能存储 100 这样大的数字！在某些数据类型下，想法是在向量中存储一个非常大的数。

```
1) Create a vector to store factorial digits and
   initialize it with 1.
2) One by one multiply numbers from 1 to n to 
   the vector. We use school mathematics for this
   purpose.
3) Sum all the elements in vector and return the sum.
```

## C++

```
// C++ program to find sum of digits in factorial
// of a number
#include <bits/stdc++.h>
using namespace std;

// Function to multiply x with large number
// stored in vector v. Result is stored in v.
void multiply(vector<int> &v, int x)
{
    int carry = 0, res;
    int size = v.size();
    for (int i = 0 ; i < size ; i++)
    {
        // Calculate res + prev carry
        int res = carry + v[i] * x;

        // updation at ith position
        v[i] = res % 10;
        carry = res / 10;
    }
    while (carry != 0)
    {
        v.push_back(carry % 10);
        carry /= 10;
    }
}

// Returns sum of digits in n!
int findSumOfDigits(int n)
{
    vector<int> v;     // create a vector of type int
    v.push_back(1);    // adds 1 to the end

    // One by one multiply i to current vector
    // and update the vector.
    for (int i=1; i<=n; i++)
        multiply(v, i);

    // Find sum of digits in vector v[]
    int sum = 0;
    int size = v.size();
    for (int i = 0 ; i < size ; i++)
        sum += v[i];
    return sum;
}

// Driver code
int main()
{
    int n = 1000;
    cout << findSumOfDigits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of digits in factorial
// of a number
import java.util.*;
class GFG{
// Function to multiply x with large number
// stored in vector v. Result is stored in v.
static ArrayList<Integer> v=new ArrayList<Integer>();
static void multiply(int x)
{
    int carry = 0;
    int size = v.size();
    for (int i = 0 ; i < size ; i++)
    {
        // Calculate res + prev carry
        int res = carry + v.get(i) * x;

        // updation at ith position
        v.set(i,res % 10);
        carry = res / 10;
    }
    while (carry != 0)
    {
        v.add(carry % 10);
        carry /= 10;
    }
}

// Returns sum of digits in n!
static int findSumOfDigits(int n)
{
    v.add(1); // adds 1 to the end

    // One by one multiply i to current vector
    // and update the vector.
    for (int i=1; i<=n; i++)
        multiply(i);

    // Find sum of digits in vector v[]
    int sum = 0;
    int size = v.size();
    for (int i = 0 ; i < size ; i++)
        sum += v.get(i);
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 1000;
    System.out.println(findSumOfDigits(n));
}
}
// this code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find sum of digits
# in factorial of a number

# Function to multiply x with large number
# stored in vector v. Result is stored in v.
def multiply(v, x):
    carry = 0
    size = len(v)
    for i in range(size):

        # Calculate res + prev carry
        res = carry + v[i] * x

        # updation at ith position
        v[i] = res % 10
        carry = res // 10

    while (carry != 0):
        v.append(carry % 10)
        carry //= 10

# Returns sum of digits in n!
def findSumOfDigits( n):
    v = []     # create a vector of type int
    v.append(1) # adds 1 to the end

    # One by one multiply i to current
    # vector and update the vector.
    for i in range(1, n + 1):
        multiply(v, i)

    # Find sum of digits in vector v[]
    sum = 0
    size = len(v)
    for i in range(size):
        sum += v[i]
    return sum

# Driver code
if __name__ == "__main__":

    n = 1000
    print(findSumOfDigits(n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find sum of digits in factorial
// of a number
using System;
using System.Collections;
class GFG{
// Function to multiply x with large number
// stored in vector v. Result is stored in v.
static ArrayList v=new ArrayList();
static void multiply(int x)
{
    int carry = 0;
    int size = v.Count;
    for (int i = 0 ; i < size ; i++)
    {
        // Calculate res + prev carry
        int res = carry + (int)v[i] * x;

        // updation at ith position
        v[i] = res % 10;
        carry = res / 10;
    }
    while (carry != 0)
    {
        v.Add(carry % 10);
        carry /= 10;
    }
}

// Returns sum of digits in n!
static int findSumOfDigits(int n)
{
    v.Add(1); // adds 1 to the end

    // One by one multiply i to current vector
    // and update the vector.
    for (int i=1; i<=n; i++)
        multiply(i);

    // Find sum of digits in vector v[]
    int sum = 0;
    int size = v.Count;
    for (int i = 0 ; i < size ; i++)
        sum += (int)v[i];
    return sum;
}

// Driver code
static void Main()
{
    int n = 1000;
    Console.WriteLine(findSumOfDigits(n));
}
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of digits in
// factorial of a number

// Function to multiply x with large number
// stored in vector v. Result is stored in v.
function multiply(&$v, $x)
{
    $carry = 0;
    $size = count($v);
    for ($i = 0 ; $i < $size ; $i++)
    {
        // Calculate res + prev carry
        $res = $carry + $v[$i] * $x;

        // updation at ith position
        $v[$i] = $res % 10;
        $carry = (int)($res / 10);
    }
    while ($carry != 0)
    {
        array_push($v, $carry % 10);
        $carry = (int)($carry / 10);
    }
}

// Returns sum of digits in n!
function findSumOfDigits($n)
{
    $v = array(); // create a vector of type int
    array_push($v, 1); // adds 1 to the end

    // One by one multiply i to current vector
    // and update the vector.
    for ($i = 1; $i <= $n; $i++)
        multiply($v, $i);

    // Find sum of digits in vector v[]
    $sum = 0;
    $size = count($v);
    for ($i = 0 ; $i < $size ; $i++)
        $sum += $v[$i];
    return $sum;
}

// Driver code
$n = 1000;
print(findSumOfDigits($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find sum of digits in factorial
// of a number

    // Function to multiply x with large number
    // stored in vector v. Result is stored in v.
    let v=[];
    function multiply(x)
    {
        let carry = 0;
    let size = v.length;
    for (let i = 0 ; i < size ; i++)
    {
        // Calculate res + prev carry
        let res = carry + v[i] * x;

        // updation at ith position
        v[i]=res % 10;
        carry = Math.floor(res / 10);
    }
    while (carry != 0)
    {
        v.push(carry % 10);
        carry = Math.floor(carry/10);
    }
    }

    // Returns sum of digits in n!
    function findSumOfDigits(n)
    {
        v.push(1); // adds 1 to the end

    // One by one multiply i to current vector
    // and update the vector.
    for (let i=1; i<=n; i++)
        multiply(i);

    // Find sum of digits in vector v[]
    let sum = 0;
    let size = v.length;
    for (let i = 0 ; i < size ; i++)
        sum += v[i];
    return sum;
    }

    // Driver code
    let n = 1000;
    document.write(findSumOfDigits(n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
10539
```