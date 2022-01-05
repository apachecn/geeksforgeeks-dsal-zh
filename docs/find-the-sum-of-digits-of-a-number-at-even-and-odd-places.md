# 求一个数在偶数和奇数处的位数之和

> 原文:[https://www . geeksforgeeks . org/find-奇数和偶数位置的数字总和/](https://www.geeksforgeeks.org/find-the-sum-of-digits-of-a-number-at-even-and-odd-places/)

给定一个数 **N** ，任务是求一个数在偶数和奇数位的位数之和。

**示例:**

> **输入:** N = 54873
> **输出:**
> 和奇数= 16
> 和偶数= 11
> 
> **输入:** N = 457892
> **输出:**
> 和奇数= 20
> 和偶数= 15

**进场:**

*   首先，计算给定数字的倒数。
*   对于反数，我们应用模数运算符并提取它的最后一位数字，这实际上是一个数的第一位数字，因此它是奇数位数字。
*   下一个数字将是偶数位置的数字，我们可以轮流取和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the reverse of a number
int reverse(int n)
{
    int rev = 0;
    while (n != 0) {
        rev = (rev * 10) + (n % 10);
        n /= 10;
    }
    return rev;
}

// Function to find the sum of the odd
// and even positioned digits in a number
void getSum(int n)
{
    n = reverse(n);
    int sumOdd = 0, sumEven = 0, c = 1;

    while (n != 0) {

        // If c is even number then it means
        // digit extracted is at even place
        if (c % 2 == 0)
            sumEven += n % 10;
        else
            sumOdd += n % 10;
        n /= 10;
        c++;
    }

    cout << "Sum odd = " << sumOdd << "\n";
    cout << "Sum even = " << sumEven;
}

// Driver code
int main()
{
    int n = 457892;
    getSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the reverse of a number
    static int reverse(int n)
    {
        int rev = 0;
        while (n != 0) {
            rev = (rev * 10) + (n % 10);
            n /= 10;
        }
        return rev;
    }

    // Function to find the sum of the odd
    // and even positioned digits in a number
    static void getSum(int n)
    {
        n = reverse(n);
        int sumOdd = 0, sumEven = 0, c = 1;

        while (n != 0) {

            // If c is even number then it means
            // digit extracted is at even place
            if (c % 2 == 0)
                sumEven += n % 10;
            else
                sumOdd += n % 10;
            n /= 10;
            c++;
        }

        System.out.println("Sum odd = " + sumOdd);
        System.out.println("Sum even = " + sumEven);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 457892;
        getSum(n);
    }
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# reverse of a number
def reverse(n):
    rev = 0
    while (n != 0):
        rev = (rev * 10) + (n % 10)
        n //= 10
    return rev

# Function to find the sum of the odd
# and even positioned digits in a number
def getSum(n):

    n = reverse(n)
    sumOdd = 0
    sumEven = 0
    c = 1

    while (n != 0):

        # If c is even number then it means
        # digit extracted is at even place
        if (c % 2 == 0):
            sumEven += n % 10
        else:
            sumOdd += n % 10
        n //= 10
        c += 1

    print("Sum odd =", sumOdd)
    print("Sum even =", sumEven)

# Driver code
n = 457892
getSum(n)

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the reverse of a number
    static int reverse(int n)
    {
        int rev = 0;
        while (n != 0) {
            rev = (rev * 10) + (n % 10);
            n /= 10;
        }
        return rev;
    }

    // Function to find the sum of the odd
    // and even positioned digits in a number
    static void getSum(int n)
    {
        n = reverse(n);
        int sumOdd = 0, sumEven = 0, c = 1;

        while (n != 0) {

            // If c is even number then it means
            // digit extracted is at even place
            if (c % 2 == 0)
                sumEven += n % 10;
            else
                sumOdd += n % 10;
            n /= 10;
            c++;
        }

        Console.WriteLine("Sum odd = " + sumOdd);
        Console.WriteLine("Sum even = " + sumEven);
    }

    // Driver code
    public static void Main()
    {
        int n = 457892;
        getSum(n);
    }
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the reverse of a number
function reverse($n)
{
    $rev = 0;
    while ($n != 0)
    {
        $rev = ($rev * 10) + ($n % 10);
        $n = floor($n / 10);
    }
    return $rev;
}

// Function to find the sum of the odd
// and even positioned digits in a number
function getSum($n)
{
    $n = reverse($n);
    $sumOdd = 0; $sumEven = 0; $c = 1;

    while ($n != 0)
    {

        // If c is even number then it means
        // digit extracted is at even place
        if ($c % 2 == 0)
            $sumEven += $n % 10;
        else
            $sumOdd += $n % 10;

        $n = floor($n / 10);
        $c++;
    }

    echo "Sum odd = ", $sumOdd, "\n";
    echo "Sum even = ", $sumEven;
}

// Driver code
$n = 457892;
getSum($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

//JavaScript implementation of the approach

    // Function to return the
    // reverse of a number
    function reverse(n) {
    let rev = 0;
    while (n != 0) {
        rev = (rev * 10) + (n % 10);
        n = Math.floor(n / 10);
    }
    return rev;
}

    // Function to find the sum of the odd
    // and even positioned digits in a number
    function getSum(n) {
        n = reverse(n);
        let sumOdd = 0, sumEven = 0, c = 1;

        while (n != 0) {

        // If c is even number then it means
        // digit extracted is at even place
        if (c % 2 == 0)
            sumEven += n % 10;
        else
            sumOdd += n % 10;
        n = Math.floor(n / 10);
        c++;
    }

    document.write("Sum odd = " + sumOdd);
    document.write("<br>");
    document.write("Sum even = " + sumEven);
}
      let n = 457892;
      // function call
      getSum(n);

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
Sum odd = 20
Sum even = 15
```

**另一种方法:**不用倒号就能解决问题。我们可以从数字的末尾一个接一个地提取所有的数字。如果原始数字是奇数，那么最后一个数字必须是奇数，否则它将是偶数。处理完一个数字后，我们可以将状态从奇数反转为偶数，反之亦然。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the odd
// and even positioned digits in a number
void getSum(int n)
{

    // If n is odd then the last digit
    // will be odd positioned
    bool isOdd = (n % 2 == 1) ? true : false;

    // To store the respective sums
    int sumOdd = 0, sumEven = 0;

    // While there are digits left process
    while (n != 0) {

        // If current digit is odd positioned
        if (isOdd)
            sumOdd += n % 10;

        // Even positioned digit
        else
            sumEven += n % 10;

        // Invert state
        isOdd = !isOdd;

        // Remove last digit
        n /= 10;
    }

    cout << "Sum odd = " << sumOdd << "\n";
    cout << "Sum even = " << sumEven;
}

// Driver code
int main()
{
    int n = 457892;
    getSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the sum of the odd
// and even positioned digits in a number
static void getSum(int n)
{

    // If n is odd then the last digit
    // will be odd positioned
    boolean isOdd = (n % 2 == 1) ? true : false;

    // To store the respective sums
    int sumOdd = 0, sumEven = 0;

    // While there are digits left process
    while (n != 0)
    {

        // If current digit is odd positioned
        if (isOdd)
            sumOdd += n % 10;

        // Even positioned digit
        else
            sumEven += n % 10;

        // Invert state
        isOdd = !isOdd;

        // Remove last digit
        n /= 10;
    }
    System.out.println("Sum odd = " + sumOdd);
    System.out.println("Sum even = " + sumEven);
}

// Driver code
public static void main(String[] args)
{
    int n = 457892;
    getSum(n);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the sum of the odd
# and even positioned digits in a number
def getSum(n):

    # If n is odd then the last digit
    # will be odd positioned
    if (n % 2 == 1) :
        isOdd = True
    else:
        isOdd = False

    # To store the respective sums
    sumOdd = 0
    sumEven = 0

    # While there are digits left process
    while (n != 0) :

        # If current digit is odd positioned
        if (isOdd):
            sumOdd += n % 10

        # Even positioned digit
        else:
            sumEven += n % 10

        # Invert state
        isOdd = not isOdd

        # Remove last digit
        n //= 10

    print( "Sum odd = " , sumOdd )
    print("Sum even = " ,sumEven)

# Driver code
if __name__ =="__main__":
    n = 457892
    getSum(n)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the sum of the odd
// and even positioned digits in a number
static void getSum(int n)
{

    // If n is odd then the last digit
    // will be odd positioned
    bool isOdd = (n % 2 == 1) ? true : false;

    // To store the respective sums
    int sumOdd = 0, sumEven = 0;

    // While there are digits left process
    while (n != 0)
    {

        // If current digit is odd positioned
        if (isOdd)
            sumOdd += n % 10;

        // Even positioned digit
        else
            sumEven += n % 10;

        // Invert state
        isOdd = !isOdd;

        // Remove last digit
        n /= 10;
    }
    Console.WriteLine("Sum odd = " + sumOdd);
    Console.Write("Sum even = " + sumEven);
}

// Driver code   
static public void Main ()
{
    int n = 457892;

    getSum(n);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the sum of the odd
// and even positioned digits in a number
function getSum(n)
{

    // If n is odd then the last digit
    // will be odd positioned
    let isOdd = (n % 2 == 1) ? true : false;

    // To store the respective sums
    let sumOdd = 0, sumEven = 0;

    // While there are digits left process
    while (n != 0) {

        // If current digit is odd positioned
        if (isOdd)
            sumOdd += n % 10;

        // Even positioned digit
        else
            sumEven += n % 10;

        // Invert state
        isOdd = !isOdd;

        // Remove last digit
        n = Math.floor(n/10);
    }

    document.write("Sum odd = " + sumOdd + "<br>");
    document.write("Sum even = " + sumEven);
}

// Driver code

    let n = 457892;
    getSum(n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Sum odd = 20
Sum even = 15
```

#### 方法 3:使用 string()方法:

1.  将整数转换为字符串。遍历字符串，将所有偶数索引和存储在一个变量中，所有奇数索引和存储在另一个变量中。

下面是实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the odd
// and even positioned digits in a number
void getSum(int n)
{

    // To store the respective sums
    int sumOdd = 0, sumEven = 0;

    // Converting integer to string
    string num = to_string(n);

    // Traversing the string
    for(int i = 0; i < num.size(); i++)
    {
        if (i % 2 == 0)
            sumOdd = sumOdd + (int(num[i]) - 48);
        else
            sumEven = sumEven + (int(num[i]) - 48);
    }
    cout << "Sum odd = " << sumOdd << "\n";
    cout << "Sum even = " << sumEven << "\n";
}

// Driver code
int main()
{
    int n = 457892;
    getSum(n);

    return 0;
}

// This code is contributed by souravmahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

class GFG{

static void getSum(int n)
{
    // To store the respective sum
    int sumOdd = 0;
    int sumEven = 0;

    // Converting integer to String
    String num = String.valueOf(n);

    // Traversing the String
    for(int i = 0; i < num.length(); i++)
        if (i % 2 == 0)
            sumOdd = sumOdd + (num.charAt(i) - '0');
        else
            sumEven = sumEven + (num.charAt(i) - '0');

    System.out.println("Sum odd = " + sumOdd);
    System.out.println("Sum even = " + sumEven);
}

// Driver code
public static void main(String[] args)
{
    int n = 457892;
    getSum(n);
}
}

// Code contributed by swarnalii
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the sum of the odd
# and even positioned digits in a number
def getSum(n):

    # To store the respective sums
    sumOdd = 0
    sumEven = 0

    # Converting integer to string
    num = str(n)

    # Traversing the string
    for i in range(len(num)):
        if(i % 2 == 0):
            sumOdd = sumOdd+int(num[i])
        else:
            sumEven = sumEven+int(num[i])

    print("Sum odd = ", sumOdd)
    print("Sum even = ", sumEven)

# Driver code
if __name__ == "__main__":
    n = 457892
    getSum(n)

# This code is contributed by vikkycirus
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

static void getSum(int n)
{

    // To store the respective sum
    int sumOdd = 0;
    int sumEven = 0;

    // Converting integer to String
    String num = n.ToString();

    // Traversing the String
    for(int i = 0; i < num.Length; i++)
        if (i % 2 == 0)
            sumOdd = sumOdd + (num[i] - '0');
        else
            sumEven = sumEven + (num[i] - '0');

    Console.WriteLine("Sum odd = " + sumOdd);
    Console.WriteLine("Sum even = " + sumEven);
}

// Driver code
public static void Main()
{
    int n = 457892;
    getSum(n);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

function getSum(n)
{
    // To store the respective sum
    let sumOdd = 0;
    let sumEven = 0;

    // Converting integer to String
    let num = (n).toString();

    // Traversing the String
    for(let i = 0; i < num.length; i++)
        if (i % 2 == 0)
            sumOdd = sumOdd + (num[i] - '0');
        else
            sumEven = sumEven + (num[i] - '0');

    document.write("Sum odd = " + sumOdd+"<br>");
    document.write("Sum even = " + sumEven+"<br>");
}

// Driver code
let n = 457892;
getSum(n);

// This code is contributed by unknown2108
</script>
```

**输出:**

```
Sum odd = 20
Sum even = 15
```