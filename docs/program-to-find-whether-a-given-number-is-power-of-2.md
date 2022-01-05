# 程序判断给定的数是否为 2 的幂

> 原文:[https://www . geesforgeks . org/program-to-find-给定的数字是否是 2 的幂/](https://www.geeksforgeeks.org/program-to-find-whether-a-given-number-is-power-of-2/)

给定一个正整数，写一个函数，看看它是否是 2 的幂。
**例:**

```
Input : n = 4
Output : Yes
22 = 4

Input : n = 7
Output : No

Input : n = 32
Output : Yes
25 = 32
```

**1。**一个简单的方法是简单地取基数为 2 的数的对数，如果你得到一个整数，那么这个数就是 2 的幂

## C++

```
// C++ Program to find whether a
// no is power of two
#include<bits/stdc++.h>
using namespace std;

// Function to check if x is power of 2
bool isPowerOfTwo(int n)
{
   if(n==0)
   return false;

   return (ceil(log2(n)) == floor(log2(n)));
}

// Driver program
int main()
{
    isPowerOfTwo(31)? cout<<"Yes"<<endl: cout<<"No"<<endl;
    isPowerOfTwo(64)? cout<<"Yes"<<endl: cout<<"No"<<endl;

    return 0;
}

// This code is contributed by Surendra_Gangwar
```

## C

```
// C Program to find whether a
// no is power of two
#include<stdio.h>
#include<stdbool.h>
#include<math.h>

/* Function to check if x is power of 2*/
bool isPowerOfTwo(int n)
{
   if(n==0)
   return false;

   return (ceil(log2(n)) == floor(log2(n)));
}

// Driver program
int main()
{
    isPowerOfTwo(31)? printf("Yes\n"): printf("No\n");
    isPowerOfTwo(64)? printf("Yes\n"): printf("No\n");
    return 0;
}

// This code is contributed by bibhudhendra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find whether a
// no is power of two
class GFG
{
/* Function to check if x is power of 2*/
static boolean isPowerOfTwo(int n)
{
    if(n==0)
    return false;

return (int)(Math.ceil((Math.log(n) / Math.log(2)))) ==
       (int)(Math.floor(((Math.log(n) / Math.log(2)))));
}

// Driver Code
public static void main(String[] args)
{
    if(isPowerOfTwo(31))
    System.out.println("Yes");
    else
    System.out.println("No");

    if(isPowerOfTwo(64))
    System.out.println("Yes");
    else
    System.out.println("No");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 Program to find
# whether a no is
# power of two
import math

# Function to check
# Log base 2
def Log2(x):
    if x == 0:
        return false;

    return (math.log10(x) /
            math.log10(2));

# Function to check
# if x is power of 2
def isPowerOfTwo(n):
    return (math.ceil(Log2(n)) ==
            math.floor(Log2(n)));

# Driver Code
if(isPowerOfTwo(31)):
    print("Yes");
else:
    print("No");

if(isPowerOfTwo(64)):
    print("Yes");
else:
    print("No");

# This code is contributed
# by mits
```

## C#

```
// C# Program to find whether
// a no is power of two
using System;

class GFG
{

/* Function to check if
   x is power of 2*/
static bool isPowerOfTwo(int n)
{

    if(n==0)
     return false;

    return (int)(Math.Ceiling((Math.Log(n) /
                               Math.Log(2)))) ==
           (int)(Math.Floor(((Math.Log(n) /
                              Math.Log(2)))));
}

// Driver Code
public static void Main()
{
    if(isPowerOfTwo(31))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    if(isPowerOfTwo(64))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// whether a no is
// power of two

// Function to check
// Log base 2
function Log2($x)
{
    return (log10($x) /
            log10(2));
}

// Function to check
// if x is power of 2
function isPowerOfTwo($n)
{
    return (ceil(Log2($n)) ==
            floor(Log2($n)));
}

// Driver Code
if(isPowerOfTwo(31))
echo "Yes\n";
else
echo "No\n";

if(isPowerOfTwo(64))
echo "Yes\n";
else
echo "No\n";

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>
// javascript Program to find whether a
// no is power of two

    /* Function to check if x is power of 2 */
    function isPowerOfTwo(n)
    {
        if (n == 0)
            return false;

        return parseInt( (Math.ceil((Math.log(n) / Math.log(2))))) == parseInt( (Math.floor(((Math.log(n) / Math.log(2))))));
    }

    // Driver Code

    if (isPowerOfTwo(31))
        document.write("Yes<br/>");
    else
        document.write("No<br/>");

    if (isPowerOfTwo(64))
        document.write("Yes<br/>");
    else
        document.write("No<br/>");

// This code is contributed by shikhasingrajput.
</script>
```

**输出:**

```
No
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)

**2。**另一种解决方法是继续将数除以 2，即迭代做 n = n/2。在任何迭代中，如果 n%2 变成非零，并且 n 不是 1，那么 n 不是 2 的幂。如果 n 变成 1，那么它就是 2 的幂。

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* Function to check if x is power of 2*/
bool isPowerOfTwo(int n)
{
    if (n == 0)
        return 0;
    while (n != 1)
    {
        if (n%2 != 0)
            return 0;
        n = n/2;
    }
    return 1;
}

/*Driver code*/
int main()
{
    isPowerOfTwo(31)? cout<<"Yes\n": cout<<"No\n";
    isPowerOfTwo(64)? cout<<"Yes\n": cout<<"No\n";
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#include<stdbool.h>

/* Function to check if x is power of 2*/
bool isPowerOfTwo(int n)
{
  if (n == 0)
    return 0;
  while (n != 1)
  {
      if (n%2 != 0)
         return 0;
      n = n/2;
  }
  return 1;
}

/*Driver program to test above function*/
int main()
{
  isPowerOfTwo(31)? printf("Yes\n"): printf("No\n");
  isPowerOfTwo(64)? printf("Yes\n"): printf("No\n");
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find whether
// a no is power of two
import java.io.*;

class GFG {

    // Function to check if
    // x is power of 2
    static boolean isPowerOfTwo(int n)
    {
        if (n == 0)
            return false;

        while (n != 1)
        {
            if (n % 2 != 0)
                return false;
            n = n / 2;
        }
        return true;
    }

    // Driver program
    public static void main(String args[])
    {
        if (isPowerOfTwo(31))
            System.out.println("Yes");
        else
            System.out.println("No");

        if (isPowerOfTwo(64))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Nikita tiwari.
```

## 蟒蛇 3

```
# Python program to check if given
# number is power of 2 or not

# Function to check if x is power of 2
def isPowerOfTwo(n):
    if (n == 0):
        return False
    while (n != 1):
            if (n % 2 != 0):
                return False
            n = n // 2

    return True

# Driver code
if(isPowerOfTwo(31)):
    print('Yes')
else:
    print('No')
if(isPowerOfTwo(64)):
    print('Yes')
else:
    print('No')

# This code is contributed by Danish Raza
```

## C#

```
// C# program to find whether
// a no is power of two
using System;

class GFG
{

    // Function to check if
    // x is power of 2
    static bool isPowerOfTwo(int n)
    {
        if (n == 0)
            return false;

        while (n != 1) {
            if (n % 2 != 0)
                return false;

            n = n / 2;
        }
        return true;
    }

    // Driver program
    public static void Main()
    {
        Console.WriteLine(isPowerOfTwo(31) ? "Yes" : "No");
        Console.WriteLine(isPowerOfTwo(64) ? "Yes" : "No");

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Function to check if
// x is power of 2
function isPowerOfTwo($n)
{
if ($n == 0)
    return 0;
while ($n != 1)
{
    if ($n % 2 != 0)
        return 0;
    $n = $n / 2;
}
return 1;
}

// Driver Code
if(isPowerOfTwo(31))
    echo "Yes\n";
else
    echo "No\n";

if(isPowerOfTwo(64))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>

    /* Function to check if x is power of 2*/
    function isPowerOfTwo(n)
    {
        if (n == 0)
            return 0;
        while (n != 1)
        {
            if (n%2 != 0)
                return 0;
            n = n/2;
        }
        return 1;
    } 

    isPowerOfTwo(31)? document.write("Yes" + "</br>"): document.write("No" + "</br>");
    isPowerOfTwo(64)? document.write("Yes"): document.write("No");

</script>
```

**输出:**

```
No
Yes
```

***时间复杂度:** O(log <sub>2</sub> n)*

***辅助空间:** O(1)*

**3。**另一种方法是使用这个简单的递归解。它使用与上述迭代解决方案相同的逻辑，但使用递归而不是迭代。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function which checks whether a
// number is a power of 2
bool powerOf2(int n)
{
    // base cases
    // '1' is the only odd number
    // which is a power of 2(2^0)
    if (n == 1)
      return true;

    // all other odd numbers are not powers of 2
    else if (n % 2 != 0 || n ==0)
      return false;

    // recursive function call
    return powerOf2(n / 2);
}

// Driver Code
int main()
{
    int n = 64;//True
    int m = 12;//False

    if (powerOf2(n) == 1)
      cout << "True" << endl;

    else cout << "False" << endl;

    if (powerOf2(m) == 1)
      cout << "True" << endl;

    else
      cout << "False" << endl;
}

//code contributed by Moukthik a.k.a rowdyninja
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function which checks
// whether a number is a
// power of 2
static boolean powerOf2(int n)
{
  // base cases
  // '1' is the only odd number
  // which is a power of 2(2^0)
  if (n == 1)
    return true;

  // all other odd numbers are
  // not powers of 2
  else if (n % 2 != 0 ||
           n ==0)
    return false;

  // recursive function call
  return powerOf2(n / 2);
}

// Driver Code
public static void main(String[] args)
{
  //True
  int n = 64;

  //False
  int m = 12;

  if (powerOf2(n) == true)
    System.out.print("True" + "\n");
  else System.out.print("False" + "\n");

  if (powerOf2(m) == true)
    System.out.print("True" + "\n");
  else
    System.out.print("False" + "\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program for above approach

# function which checks whether a
# number is a power of 2
def powerof2(n):

    # base cases
    # '1' is the only odd number
    # which is a power of 2(2^0)
    if n == 1:
        return True

    # all other odd numbers are not powers of 2
    elif n%2 != 0 or n == 0:
        return False

    #recursive function call
    return powerof2(n/2)

# Driver Code
if __name__ == "__main__":

  print(powerof2(64)) #True
  print(powerof2(12)) #False

#code contributed by Moukthik a.k.a rowdyninja
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function which checks whether a
// number is a power of 2
static bool powerOf2(int n)
{

    // Base cases
    // '1' is the only odd number
    // which is a power of 2(2^0)
    if (n == 1)
      return true;

    // All other odd numbers
    // are not powers of 2
    else if (n % 2 != 0 || n == 0)
      return false;

    // Recursive function call
    return powerOf2(n / 2);
}

// Driver code
static void Main()
{

    int n = 64;//True
    int m = 12;//False

    if (powerOf2(n))
    {
        Console.Write("True" + "\n");
    }
    else
    {
        Console.Write("False" + "\n");
    }

    if (powerOf2(m))
    {
        Console.Write("True");
    }
    else
    {
        Console.Write("False");
    }
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// javascript program for
// the above approach

// Function which checks
// whether a number is a
// power of 2

function powerOf2(n)
{
  // base cases
  // '1' is the only odd number
  // which is a power of 2(2^0)
  if (n == 1)
    return true;

  // all other odd numbers are
  // not powers of 2
  else if (n % 2 != 0 ||
           n ==0)
    return false;

  // recursive function call
  return powerOf2(n / 2);
}

// Driver Code
//True
var n = 64;

//False
var m = 12;

if (powerOf2(n) == true)
  document.write("True" + "\n");
else document.write("False" + "\n");

if (powerOf2(m) == true)
  document.write("True" + "\n");
else
  document.write("False" + "\n");

// This code contributed by shikhasingrajput

</script>
```

**Output**

```
True
False
```

***时间复杂度:** O(log <sub>2</sub> n)*

***辅助空间:** O(原木 <sub>2</sub> n)*

**4。**两个数的所有幂都只有一位集。所以计算设定位数，如果你得到 1，那么这个数就是 2 的幂。请参见[对整数中的设定位进行计数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)对设定位进行计数。

**5。**如果我们将 2 的幂减 1，那么在唯一设置的位被设置之后，所有未设置的位都被设置；并且设置位变为未设置。
例如，对于 4 ( 100)和 16(10000)，在减去 1
3–>011
15–>01111 之后，我们得到以下结果

所以，如果一个数 n 是 2 的幂，那么 n 和 n-1 的位&将为零。根据 n&(n-1)的值，我们可以说 n 是 2 的幂或不是 2 的幂。当 n 为 0 时，表达式 n&(n-1)将不起作用。同样为了处理这种情况，我们的表达式将变成 n&(！n&(n-1))。

下面是这个方法的实现。

时间复杂度:0(1)

空间复杂性:0(1)

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define bool int

/* Function to check if x is power of 2*/
bool isPowerOfTwo (int x)
{
    /* First x in the below expression is for the case when x is 0 */
    return x && (!(x&(x-1)));
}

/*Driver code*/
int main()
{
    isPowerOfTwo(31)? cout<<"Yes\n": cout<<"No\n";
    isPowerOfTwo(64)? cout<<"Yes\n": cout<<"No\n";
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#define bool int

/* Function to check if x is power of 2*/
bool isPowerOfTwo (int x)
{
  /* First x in the below expression is for the case when x is 0 */
  return x && (!(x&(x-1)));
}

/*Driver program to test above function*/
int main()
{
  isPowerOfTwo(31)? printf("Yes\n"): printf("No\n");
  isPowerOfTwo(64)? printf("Yes\n"): printf("No\n");
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to efficiently
// check for power for 2

class Test
{
    /* Method to check if x is power of 2*/
    static boolean isPowerOfTwo (int x)
    {
      /* First x in the below expression is
        for the case when x is 0 */
        return x!=0 && ((x&(x-1)) == 0);

    }

    // Driver method
    public static void main(String[] args)
    {
         System.out.println(isPowerOfTwo(31) ? "Yes" : "No");
         System.out.println(isPowerOfTwo(64) ? "Yes" : "No");

    }
}
// This program is contributed by Gaurav Miglani   
```

## 计算机编程语言

```
# Python program to check if given
# number is power of 2 or not

# Function to check if x is power of 2
def isPowerOfTwo (x):

    # First x in the below expression
    # is for the case when x is 0
    return (x and (not(x & (x - 1))) )

# Driver code
if(isPowerOfTwo(31)):
    print('Yes')
else:
    print('No')

if(isPowerOfTwo(64)):
    print('Yes')
else:
    print('No')

# This code is contributed by Danish Raza   
```

## C#

```
// C# program to efficiently
// check for power for 2
using System;

class GFG
{
    // Method to check if x is power of 2
    static bool isPowerOfTwo (int x)
    {
        // First x in the below expression 
        // is for the case when x is 0
        return x != 0 && ((x & (x - 1)) == 0);

    }

    // Driver method
    public static void Main()
    {
        Console.WriteLine(isPowerOfTwo(31) ? "Yes" : "No");
        Console.WriteLine(isPowerOfTwo(64) ? "Yes" : "No");

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to efficiently
// check for power for 2

// Function to check if
// x is power of 2
function isPowerOfTwo ($x)
{
// First x in the below expression
// is for the case when x is 0
return $x && (!($x & ($x - 1)));
}

// Driver Code
if(isPowerOfTwo(31))
    echo "Yes\n" ;
else
    echo "No\n";

if(isPowerOfTwo(64))
    echo "Yes\n" ;
else
    echo "No\n";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript program to efficiently
// check for power for 2  

/* Method to check if x is power of 2*/
    function isPowerOfTwo (x)
    {
      /* First x in the below expression is
        for the case when x is 0 */
        return x!=0 && ((x&(x-1)) == 0);

    }

// Driver method
document.write(isPowerOfTwo(31) ? "Yes" : "No");
document.write("<br>"+(isPowerOfTwo(64) ? "Yes" : "No"));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
No
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**6** 。另一种方法是使用逻辑找到给定数字的最右边的位组。

## C++

```
#include <iostream>
using namespace std;

/* Function to check if x is power of 2*/
bool isPowerofTwo(long long n)
{
    if (n == 0)
        return 0;
    if ((n & (~(n - 1))) == n)
        return 1;
    return 0;
}
/*Driver code*/
int main()
{

    isPowerofTwo(30) ? cout << "Yes\n" : cout << "No\n";
    isPowerofTwo(128) ? cout << "Yes\n" : cout << "No\n";
    return 0;
}
// This code is contributed by Sachin
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;

class GFG {

    // Function to check if x is power of 2
    static boolean isPowerofTwo(int n)
    {
        if (n == 0)
            return false;
        if ((n & (~(n - 1))) == n)
            return true;
        return false;
    }
    public static void main(String[] args)
    {
        if (isPowerofTwo(30) == true)
            System.out.println("Yes");
        else
            System.out.println("No");

          if (isPowerofTwo(128) == true)
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by rajsanghavi9.
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to check if x is power of 2*/
def isPowerofTwo(n):

    if (n == 0):
        return 0
    if ((n & (~(n - 1))) == n):
        return 1
    return 0

# Driver code
if(isPowerofTwo(30)):
    print('Yes')
else:
    print('No')

if(isPowerofTwo(128)):
    print('Yes')
else:
    print('No')

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program of the above approach

using System;
public class GFG {

    // Function to check if x is power of 2
    static bool isPowerofTwo(int n)
    {
        if (n == 0)
            return false;
        if ((n & (~(n - 1))) == n)
            return true;
        return false;
    }
    public static void Main(String[] args)
    {
        if (isPowerofTwo(30) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

          if (isPowerofTwo(128) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

    }
}

// This code contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to check if x is power of 2
    function isPowerofTwo(n)
    {
        if (n == 0)
            return false;
        if ((n & (~(n - 1))) == n)
            return true;
        return false;
    }

        if (isPowerofTwo(30) == true)
            document.write("Yes<br/>");
        else
            document.write("No<br/>");

          if (isPowerofTwo(128) == true)
            document.write("Yes<br/>");
        else
            document.write("No<br/>");

// This code is contributed by umadevi9616
</script>
```

**Output**

```
No
Yes
```

***时间复杂度:** O(1)*

***空间复杂度:** O(1)*

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。