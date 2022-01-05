# 检查给定的数是否是任意数的阶乘

> 原文:[https://www . geesforgeks . org/check-如果给定的数字是任意数字的阶乘/](https://www.geeksforgeeks.org/check-if-a-given-number-is-factorial-of-any-number/)

给定一个数 n，任务是确定 n 是否可以是某个数 x 的阶乘
**示例:**

```
Input: N = 24
Output: Yes
Explanation: 4! = 24

Input: N = 25
Output: No
```

**进场:**
以下是上述进场的实施:

## C++

```
// C++ implementation for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// the given number is a
// factorial of any number
bool isFactorial(int n)
{
  for (int i = 1;; i++) {
    if (n % i == 0) {
      n /= i;
    }
    else {
      break;
    }
  }

  if (n == 1) {
    return true;
  }
  else {
    return false;
  }
}

// Driver Code
int main()
{
  int n = 24;

  bool ans = isFactorial(n);
  if (ans == 1) {
    cout << "Yes\n";
  }
  else {
    cout << "No\n";
  }

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
class GFG
{

    // Function to check if the given number
    // is a factorial of any number
    static boolean isFactorial(int n)
    {
        for (int i = 1;; i++)
        {
            if (n % i == 0)
            {
                n /= i;
            }
            else
            {
                break;
            }
        }

        if (n == 1)
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 24;
        boolean ans = isFactorial(n);

        if (ans == true)
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check if
# the given number is a
# factorial of any number
def isFactorial(n) :
    i = 1;
    while(True) :

        if (n % i == 0) :
            n //= i;

        else :
            break;

        i += 1;

    if (n == 1) :
        return True;

    else :
        return False;

# Driver Code
if __name__ == "__main__" :
    n = 24;
    ans = isFactorial(n);

    if (ans == 1) :
        print("Yes");

    else :
        print("No");

# This code is contributed by kanugargng
```

## C#

```
// C# implementation for the above approach
using System;

class GFG
{

    // Function to check if the given number
    // is a factorial of any number
    static Boolean isFactorial(int n)
    {
        for (int i = 1;; i++)
        {
            if (n % i == 0)
            {
                n /= i;
            }
            else
            {
                break;
            }
        }

        if (n == 1)
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int n = 24;
        Boolean ans = isFactorial(n);

        if (ans == true)
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation for
// the above approach

// Function to check if
// the given number is a
// factorial of any number
function isFactorial(n)
{
    for (var i = 1;; i++)
    {
        if (n % i == 0)
        {
            n = parseInt(n/i);
        }
        else
        {
            break;
        }
    }

    if (n == 1)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver Code
var n = 24;
var ans = isFactorial(n);
if (ans == 1)
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```