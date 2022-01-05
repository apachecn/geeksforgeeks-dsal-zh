# 给定数字位数总和程序

> 原文:[https://www . geesforgeks . org/给定数字的位数总和程序/](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)

给定一个数，求其位数的和。

**示例:**

```
Input : n = 687
Output : 21

Input : n = 12
Output : 3
```

**给定数字位数总和的一般算法:**

1.  拿到号码
2.  声明一个变量来存储总和，并将其设置为 0
3.  重复接下来的两个步骤，直到数字不为 0
4.  在余数“%”运算符的帮助下，通过除以 10 得到数字最右边的数字，并将其相加。
5.  在“/”运算符的帮助下，将数字除以 10，去掉最右边的数字。
6.  打印或返回总和

下面是求数字总和的方法。
**1。迭代:**

## C++

```
// C program to compute sum of digits in
// number.
#include <iostream>
using namespace std;

/* Function to get sum of digits */
class gfg {
public:
    int getSum(int n)
    {
        int sum = 0;
        while (n != 0) {
            sum = sum + n % 10;
            n = n / 10;
        }
        return sum;
    }
};

// Driver code
int main()
{
    gfg g;
    int n = 687;
    cout << g.getSum(n);
    return 0;
}
// This code is contributed by Soumik
```

## C

```
// C program to compute sum of digits in
// number.
#include <stdio.h>

/* Function to get sum of digits */
int getSum(int n)
{
    int sum = 0;
    while (n != 0) {
        sum = sum + n % 10;
        n = n / 10;
    }
    return sum;
}

// Driver code
int main()
{
    int n = 687;
    printf(" %d ", getSum(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute
// sum of digits in number.
import java.io.*;

class GFG {

    /* Function to get sum of digits */
    static int getSum(int n)
    {
        int sum = 0;

        while (n != 0) {
            sum = sum + n % 10;
            n = n / 10;
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 687;

        System.out.println(getSum(n));
    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Python 3 program to
# compute sum of digits in
# number.

# Function to get sum of digits

def getSum(n):

    sum = 0
    while (n != 0):

        sum = sum + int(n % 10)
        n = int(n/10)

    return sum

# Driver code
n = 687
print(getSum(n))
```

## C#

```
// C# program to compute
// sum of digits in number.
using System;

class GFG {
    /* Function to get sum of digits */
    static int getSum(int n)
    {
        int sum = 0;

        while (n != 0) {
            sum = sum + n % 10;
            n = n / 10;
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int n = 687;
        Console.Write(getSum(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code to compute sum
// of digits in number.

// Function to get
// $sum of digits
function getsum($n)
{
    $sum = 0;
    while ($n != 0)
    {
        $sum = $sum + $n % 10;
        $n = $n/10;
    }
    return $sum;
}

// Driver Code
$n = 687;
$res = getsum($n);
echo("$res");

// This code is contributed by
// Smitha Dinesh Semwal.
?>
```

## java 描述语言

```
<script>

// Javascript program to compute sum of digits in
// number.

/* Function to get sum of digits */
function getSum(n)
{
    var sum = 0;
    while (n != 0) {
        sum = sum + n % 10;
        n = parseInt(n / 10);
    }
    return sum;
}

// Driver code
var n = 687;
document.write(getSum(n));

</script>
```

**Output**

```
21
```

**如何在一条** **单线上计算？**
下面的函数有三行而不是一行，但是它计算的是一行的总和。如果我们将指针传递给 sum，它可以成为单行函数。

## C++

```
#include <iostream>
using namespace std;

/* Function to get sum of digits */
class gfg {
public:
    int getSum(int n)
    {
        int sum;

        /* Single line that calculates sum */
        for (sum = 0; n > 0; sum += n % 10, n /= 10)
            ;

        return sum;
    }
};

// Driver code
int main()
{
    gfg g;
    int n = 687;
    cout << g.getSum(n);
    return 0;
}
// This code is contributed by Soumik
```

## C

```
#include <stdio.h>

/* Function to get sum of digits */
int getSum(int n)
{
    int sum;

    /* Single line that calculates sum */
    for (sum = 0; n > 0; sum += n % 10, n /= 10)
        ;

    return sum;
}

// Driver code
int main()
{
    int n = 687;
    printf(" %d ", getSum(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute
// sum of digits in number.
import java.io.*;

class GFG {

    /* Function to get sum of digits */
    static int getSum(int n)
    {
        int sum;

        /* Single line that calculates sum */
        for (sum = 0; n > 0; sum += n % 10, n /= 10)
            ;

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 687;

        System.out.println(getSum(n));
    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Function to get sum of digits

def getSum(n):

    sum = 0

    # Single line that calculates sum
    while(n > 0):
        sum += int(n % 10)
        n = int(n/10)

    return sum

# Driver code
n = 687
print(getSum(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to compute
// sum of digits in number.
using System;

class GFG {
    static int getSum(int n)
    {
        int sum;

        /* Single line that calculates sum */
        for (sum = 0; n > 0; sum += n % 10, n /= 10)
            ;

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int n = 687;
        Console.Write(getSum(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code for Sum the
// digits of a given number

// Function to get sum of digits
function getsum($n)
{

    // Single line that calculates $sum
    for ($sum = 0; $n > 0; $sum += $n % 10,
                                  $n /= 10);
    return $sum;
}

// Driver Code
$n = 687;
echo(getsum($n));

// This code is contributed by
// Smitha Dinesh Semwal.
?>
```

## java 描述语言

```
<script>

// Javascript program to compute
// sum of digits in number.

// Function to get sum of digits
function getSum(n)
{
    let sum;

    // Single line that calculates sum
    for(sum = 0; n > 0;
        sum += n % 10,
        n = parseInt(n / 10))
        ;
    return sum;
}

// Driver code
let n = 687;

document.write(getSum(n));

// This code is contributed by subhammahato348

</script>
```

**Output**

```
21
```

**2。递归**
感谢艾莎提供以下递归解决方案。

算法:

```
1) Get the number
2) Get the remainder and pass the next remaining digits
3) Get the rightmost digit of the number with help of the remainder '%' operator by dividing it by 10 and add it to sum.
   Divide the number by 10 with help of '/' operator to remove the rightmost digit.
4) Check the base case with n = 0
5) Print or return the sum
```

## C++

```
// C++ program to compute
// sum of digits in number.
#include <iostream>
using namespace std;
class gfg {
public:
    int sumDigits(int no)
    {
        if(no == 0){
          return 0 ;
        }

        return (no % 10) + sumDigits(no / 10) ;
    }
};

// Driver code
int main(void)
{
    gfg g;
    cout << g.sumDigits(687);
    return 0;
}
```

## C

```
// C program to compute
// sum of digits in number.
#include <stdio.h>

int sumDigits(int no)
{
  if(no == 0){
    return 0 ;
  }

  return (no % 10) + sumDigits(no / 10) ;
}

int main()
{
    printf("%d", sumDigits(687));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute
// sum of digits in number.
import java.io.*;

class GFG {

    /* Function to get sum of digits */
    static int sumDigits(int no)
    {
        if(no == 0){
          return 0 ;
        }

        return (no % 10) + sumDigits(no / 10) ;
     }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(sumDigits(687));
    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Python program to compute
# sum of digits in number.

def sumDigits(no):
    return 0 if no == 0 else int(no % 10) + sumDigits(int(no/10))

# Driver code
print(sumDigits(687))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to compute
// sum of digits in number.
using System;

class GFG {
    /* Function to get sum of digits */
    static int sumDigits(int no)
    {
        return no == 0 ? 0 : no % 10 + sumDigits(no / 10);
    }

    // Driver code
    public static void Main()
    {
        Console.Write(sumDigits(687));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute
// sum of digits in number.
function sumDigits($no)
{
return $no == 0 ? 0 : $no % 10 +
                      sumDigits($no / 10) ;
}

// Driver Code
echo sumDigits(687);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// Program to compute
// sum of digits in number
  // Function to get sum of digits

     function sumDigits(no)
     {
        if(no == 0){
          return 0 ;
        }

        return (no % 10) + sumDigits(parseInt(no/10)) ;
      }

// Driver code
      document.write(sumDigits(687));

// This is code is contributed by simranarora5sos
</script>
```

**Output**

```
21
```

**3。以输入为字符串**

当那个数的位数超过 10 <sup>19</sup> 时，由于 long long int 的范围不满足给定的数，所以我们不能把那个数当作整数。因此，将输入作为一个字符串，从开始到字符串的长度运行一个循环，并增加该字符的总和(在本例中是数字)

下面是上述方法的实现

## C++14

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;
int getSum(string str)
{
    int sum = 0;

    // Traversing through the string
    for (int i = 0; i < str.length(); i++) {
        // Since ascii value of
        // numbers starts from 48
        // so we subtract it from sum
        sum = sum + str[i] - 48;
    }
    return sum;
}

// Driver Code
int main()
{
    string st = "123456789123456789123422";
    cout << getSum(st);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
class GFG {

    static int getSum(String str)
    {
        int sum = 0;

        // Traversing through the string
        for (int i = 0; i < str.length(); i++) {

            // Since ascii value of
            // numbers starts from 48
            // so we subtract it from sum
            sum = sum + str.charAt(i) - 48;
        }
        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String st = "123456789123456789123422";
        System.out.print(getSum(st));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python implementation of the above approach
def getSum(n):
    # Initializing sum to 0
    sum = 0
    # Traversing through string
    for i in n:
        # Converting char to int
        sum = sum + int(i)

    return sum

n = "123456789123456789123422"
print(getSum(n))
```

## C#

```
// C# implementation of the above approach
using System;
public class GFG {
    static int getSum(String str)
    {
        int sum = 0;

        // Traversing through the string
        for (int i = 0; i < str.Length; i++) {

            // Since ascii value of
            // numbers starts from 48
            // so we subtract it from sum
            sum = sum + str[i] - 48;
        }
        return sum;
    }

    // Driver Code
    static public void Main()
    {
        String st = "123456789123456789123422";
        Console.Write(getSum(st));
    }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

function getSum(str)
{
    let sum = 0;

    // Traversing through the string
    for (let i = 0; i < str.length; i++)
    {

        // Since ascii value of
        // numbers starts from 48
        // so we subtract it from sum
        sum = sum + parseInt(str[i]);
    }
    return sum;
}

// Driver Code
let st = "123456789123456789123422";
document.write(getSum(st));

// This code is contributed by subhammahato348.
</script>
```

**Output**

```
104
```

4.**使用尾部递归**

这个问题也可以用尾部递归来解决。这里有一个解决方法。

1.向函数添加另一个变量“Val”，并将其初始化为(val = 0)

2.每次调用该函数时，将 mod 值(n%10)作为“(n%10)+val”添加到变量中，这是 n 中的最后一位。同时将变量 n 作为 n/10 传递。

3.所以在第一次调用时，它会有最后一个数字。当我们将 n/10 作为 n 传递时，它会一直跟随，直到 n 减少到一位数。

4.n<10 是基本情况，因此当 n < 10 时，将 n 加到变量中，因为它是最后一个数字，并返回数字总和的值

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check sum
// of digit using tail recursion
int sum_of_digit(int n, int val)
{
    if (n < 10)
    {
        val = val + n;
        return val;
    }
    return sum_of_digit(n / 10, (n % 10) + val);
}

// Driver code
int main()
{
    int num = 12345;
    int result = sum_of_digit(num, 0);

    cout << "Sum of digits is " << result;

    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class sum_of_digits {

    // Function to check sum
    // of digit using tail recursion
    static int sum_of_digit(int n, int val)
    {
        if (n < 10) {
            val = val + n;
            return val;
        }
        return sum_of_digit(n / 10, (n % 10) + val);
    }

    // Driven Program to check above
    public static void main(String args[])
    {
        int num = 12345;
        int result = sum_of_digit(num, 0);
        System.out.println("Sum of digits is " + result);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check sum
# of digit using tail recursion
def sum_of_digit(n, val):

    if (n < 10):
        val = val + n
        return val

    return sum_of_digit(n // 10, (n % 10) + val)

# Driver code
num = 12345
result = sum_of_digit(num, 0)

print("Sum of digits is", result)

# This code is contributed by subhammahato348
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check sum
// of digit using tail recursion
static int sum_of_digit(int n, int val)
{
    if (n < 10)
    {
        val = val + n;
        return val;
    }
    return sum_of_digit(n / 10, (n % 10) + val);
}

// Driver code
public static void Main()
{
    int num = 12345;
    int result = sum_of_digit(num, 0);

    Console.Write("Sum of digits is " + result);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check sum
// of digit using tail recursion
function sum_of_digit(n, val)
{
    if (n < 10)
    {
        val = val + n;
        return val;
    }
    return sum_of_digit(parseInt(n / 10),
    (n % 10) + val);
}

// Driver code
    let num = 12345;
    let result = sum_of_digit(num, 0);

    document.write("Sum of digits is " + result);

// This code is contributed by subhammahato348

</script>
```

**Output**

```
Sum of digits is 15
```

如果您发现上述代码/算法不正确，请写评论，或者找到更好的方法来解决相同的问题。