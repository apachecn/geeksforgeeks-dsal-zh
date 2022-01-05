# 不求平方根检查一个数是否是完美平方

> 原文:[https://www . geeksforgeeks . org/check-a-number-if-perfect-square-not-find-平方根/](https://www.geeksforgeeks.org/check-if-a-number-is-perfect-square-without-finding-square-root/)

不求平方根，检查一个数是否是完美的平方。

**示例:**

> 输入:n = 36
> 输出:是
> 
> 输入:n = 12
> 输出:否

我们已经讨论了一种方法来[检查一个数是否是完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。

**方法 1:**
想法是运行一个从 i = 1 到 floor(sqrt(n))的循环，然后检查平方是否等于 n。

## C++

```
// C++ program to check if a number is perfect
// square without finding square root
#include <bits/stdc++.h>
using namespace std;

bool isPerfectSquare(int n)
{
    for (int i = 1; i * i <= n; i++) {

        // If (i * i = n)
        if ((n % i == 0) && (n / i == i)) {
            return true;
        }
    }
    return false;
}

// Driver code
int main()
{
    long long int n = 36;
    if (isPerfectSquare(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is perfect
// square without finding the square root
public class GfG {

    static boolean isPerfectSquare(int n)
    {
        for (int i = 1; i * i <= n; i++) {

            // If (i * i = n)
            if ((n % i == 0) && (n / i == i)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args)
    {

        int n = 36;

        if (isPerfectSquare(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program to check if a number is
# perfect square without finding square root

# from math import sqrt function

def isPerfectSquare(n) :

    i = 1
    while(i * i<= n):

        # If (i * i = n)
        if ((n % i == 0) and (n / i == i)):
            return True

        i = i + 1
    return False

# Driver code
if __name__ == "__main__" :

    n = 36
    if (isPerfectSquare(n)):
        print("Yes, it is a perfect square.")
    else :
        print("No, it is not a perfect square.")

    # This code is contributed by Ryuga
```

## C#

```
// C# program to check if a number is perfect
// square without finding the square root
using System;

public class GfG {

    static bool isPerfectSquare(int n)
    {
        for (int i = 1; i * i <= n; i++) {

            // If (i * i = n)
            if ((n % i == 0) && (n / i == i)) {
                return true;
            }
        }
        return false;
    }

    public static void Main()
    {

        int n = 36;

        if (isPerfectSquare(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}
/*This code is contributed by Rajput-Ji*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number is perfect
// square without finding square root

function isPerfectSquare($n)
{
    for ($i = 1; $i * $i <= $n; $i++) {

        // If (i * i = n)
        if (($n % $i == 0) && ($n / $i == $i)) {
            return true;
        }
    }
    return false;
}

// Driver code
$n = 36;
if (isPerfectSquare($n))
    echo "Yes";    
else
    echo "No";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// JavaScript program to check if a number is perfect
// square without finding square root

function isPerfectSquare(n)
{
    for (let i = 1; i * i <= n; i++) {

        // If (i * i = n)
        if ((n % i == 0) && (Math.floor(n / i) == i)) {
            return true;
        }
    }
    return false;
}

// Driver code

    let n = 36;
    if (isPerfectSquare(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(sqrt(N))

**方法二:**
想法是用二分搜索法找到一个 1 到 n 范围内的数，其平方等于 n，这样在每次迭代中问题陈述减少到一半[1 到 n/2-1 或 n/2 到 n]。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Program to find if x is a
// perfect square.
bool isPerfectSquare(int x)
{ 
    long long left = 1, right = x;

    while (left <= right)
    {
        long long mid = (left + right) / 2;

        // Check if mid is perfect square
        if (mid * mid == x)
        {
            return true;
        }

        // Mid is small -> go right to increase mid
        if (mid * mid < x)
        {
            left = mid + 1;
        }

        // Mid is large -> to left to decrease mid
        else
        {
            right = mid - 1;
        }
    }
    return false;
}

// Driver Code
int main()
{
    int x = 2500;

    // Function Call
    if (isPerfectSquare(x))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG
{

    // Program to find if x is a
    // perfect square.
    static boolean isPerfectSquare(int num)
    {
        long left = 1, right = num;

        while (left <= right)
        {
            long mid = (left + right) / 2;

            // Check if mid is perfect square
            if (mid * mid == num)
            {
                return true;
            }

            // Mid is small -> go right to increase mid
            if (mid * mid < num)
            {
                left = mid + 1;
            }

            // Mid is large -> to left to decrease mid
            else
            {
                right = mid - 1;
            }
        }
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 2500;

        // Function Call
        if (isPerfectSquare(x))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## 蟒蛇 3

```
# Python program for above approach

# Program to find if x is a
# perfect square.
def isPerfectSquare(x):

    left = 1
    right = x

    while (left <= right):

        mid = (left + right) >> 1

        # Check if mid is perfect square
        if ((mid * mid) == x):
            return True

        # Mid is small -> go right to increase mid
        if (mid * mid < x):
            left = mid + 1

        # Mid is large -> to left to decrease mid
        else:
            right = mid - 1
    return False

# Driver code
if __name__ == "__main__":

  x = 2500

  # Function Call
  if (isPerfectSquare(x)):
      print("Yes")
  else:
      print("No")
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Program to find if x is a
// perfect square.
static bool isPerfectSquare(int x)
{
  long left = 1, right = x;

  while (left <= right)
  {
    long mid = (left + right) / 2;

    // Check if mid is perfect
    // square
    if (mid * mid == x)
    {
      return true;
    }

    // Mid is small -> go right to
    // increase mid
    if (mid * mid < x)
    {
      left = mid + 1;
    }

    // Mid is large -> to left
    // to decrease mid
    else
    {
      right = mid - 1;
    }
  }
  return false;
}

// Driver code
public static void Main(string[] args)
{
  int x = 2500;

  // Function Call
  if (isPerfectSquare(x))
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Program to find if x is a
// perfect square.
function isPerfectSquare(x)
{ 
    let left = 1, right = x;

    while (left <= right)
    {
        let mid = parseInt((left + right) / 2);

        // Check if mid is perfect square
        if (mid * mid == x)
        {
            return true;
        }

        // Mid is small -> go right to increase mid
        if (mid * mid < x)
        {
            left = mid + 1;
        }

        // Mid is large -> to left to decrease mid
        else
        {
            right = mid - 1;
        }
    }
    return false;
}

// Driver Code
let x = 2500;

// Function Call
if (isPerfectSquare(x))
    document.write("Yes");
else
    document.write("Yes");

// This code is contributed by rishavmahato348

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(log(N))
**空间** **复杂度:** O(1)