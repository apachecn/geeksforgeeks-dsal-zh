# 所有 N 位回文数字之和

> 原文:[https://www . geeksforgeeks . org/所有 n 位数字的总和回文数字/](https://www.geeksforgeeks.org/sum-of-all-n-digit-palindrome-numbers/)

给定一个数字 N，任务是找出所有 N 位回文的和。

**示例:**

```
Input: N = 2
Output: 495
Explanation: 
11 + 22 + 33 + 44 + 55 +
66 + 77 + 88 + 99
= 495

Input: N = 7
Output: 49500000000 
```

**天真的方法:**
运行一个从 10^(n-1)到 10^(n)–1 的循环，检查当前数字是否回文。如果它为答案增加了价值。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check
// palindrome
bool isPalindrome(string& s)
{
    int left = 0, right = s.size() - 1;
    while (left <= right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Function to calculate
// the sum of n-digit
// palindrome
long long getSum(int n)
{

    int start = pow(10, n - 1);
    int end = pow(10, n) - 1;

    long long sum = 0;

    // Run a loop to check
    // all possible palindrome
    for (int i = start; i <= end; i++) {
        string s = to_string(i);
        // If palindrome
        // append sum
        if (isPalindrome(s)) {
            sum += i;
        }
    }

    return sum;
}

// Driver code
int main()
{

    int n = 1;
    long long ans = getSum(n);
    cout << ans << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG
{

// Function to check
// palindrome
static boolean isPalindrome(String s)
{
    int left = 0, right = s.length() - 1;
    while (left <= right)
    {
        if (s.charAt(left) != s.charAt(right))
        {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Function to calculate
// the sum of n-digit
// palindrome
static long getSum(int n)
{

    int start = (int) Math.pow(10, n - 1);
    int end = (int) (Math.pow(10, n) - 1);

    long sum = 0;

    // Run a loop to check
    // all possible palindrome
    for (int i = start; i <= end; i++)
    {
        String s = String.valueOf(i);

        // If palindrome
        // append sum
        if (isPalindrome(s))
        {
            sum += i;
        }
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 1;
    long ans = getSum(n);
    System.out.print(ans);
}
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python program for the above approach
import math

# Function to check
# palindrome
def isPalindrome(s):
    left = 0
    right = len(s) - 1
    while (left <= right):
        if (s[left] != s[right]):
            return False

        left = left + 1
        right = right - 1

    return True

# Function to calculate
# the sum of n-digit
# palindrome
def getSum(n):
    start = int(math.pow(10, n - 1))
    end = int(math.pow(10, n)) - 1

    sum = 0

    # Run a loop to check
    # all possible palindrome
    for i in range(start, end + 1):
        s = str(i)

        # If palindrome
        # append sum
        if (isPalindrome(s)):
            sum = sum + i

    return sum

# Driver code

n = 1
ans = getSum(n)
print(ans)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to check
    // palindrome
    static bool isPalindrome(string s)
    {
        int left = 0, right = s.Length - 1;
        while (left <= right)
        {
            if (s[left] != s[right])
            {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    // Function to calculate
    // the sum of n-digit
    // palindrome
    static long getSum(int n)
    {

        int start = (int) Math.Pow(10, n - 1);
        int end = (int) (Math.Pow(10, n) - 1);

        long sum = 0;

        // Run a loop to check
        // all possible palindrome
        for (int i = start; i <= end; i++)
        {
            string s = i.ToString();;

            // If palindrome
            // append sum
            if (isPalindrome(s))
            {
                sum += i;
            }
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int n = 1;
        long ans = getSum(n);
        Console.Write(ans);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach

// Function to check
// palindrome
function isPalindrome(s)
{
    var left = 0, right = s.length - 1;
    while (left <= right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Function to calculate
// the sum of n-digit
// palindrome
function getSum(n)
{

    var start = Math.pow(10, n - 1);
    var end = Math.pow(10, n) - 1;

    var sum = 0;

    // Run a loop to check
    // all possible palindrome
    for (var i = start; i <= end; i++) {
        var s = (i.toString());
        // If palindrome
        // append sum
        if (isPalindrome(s)) {
            sum += i;
        }
    }

    return sum;
}

// Driver code
var n = 1;
var ans = getSum(n);
document.write( ans + "<br>");

</script>
```

**Output:** 

```
45
```

**时间复杂度:** O(n*log(n))

**有效方法:**
仔细观察 n 位回文的和，形成一个数列，即 45，495，49500，495000，4950000，49500000，49500000。因此，通过推导出一个数学公式，我们得到 n = 1 sum = 45，n>1 put sum =(99/2)*10^n-1*10^(n-1)/2

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// sum of n digit number
long double getSum(int n)
{

    long double sum = 0;
    // Corner case
    if (n == 1) {
        sum = 45.0;
    }
    // Using above approach
    else {
        sum = (99.0 / 2.0) * pow(10, n - 1)
              * pow(10, (n - 1) / 2);
    }
    return sum;
}

// Driver code
int main()
{

    int n = 3;
    long double ans = getSum(n);
    cout << setprecision(12) << ans << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach

class GFG
{

    // Function to calculate
    // sum of n digit number
    static double getSum(int n)
    {

        double sum = 0;

        // Corner case
        if (n == 1)
        {
            sum = 45.0;
        }

        // Using above approach
        else
        {
            sum = (99.0 / 2.0) *
                    Math.pow(10, n - 1) *
                    Math.pow(10, (n - 1) / 2);
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        double ans = getSum(n);
        System.out.print(ans);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python program for
# the above approach

# Function to calculate
# sum of n digit number
def getSum(n):

    sum = 0;

    # Corner case
    if (n == 1):
        sum = 45.0;

    # Using above approach
    else:
        sum = (99.0 / 2.0) * pow(10, n - 1)\
        * pow(10, (n - 1) / 2);

    return sum;

# Driver code
if __name__ == '__main__':
    n = 3;
    ans = int(getSum(n));
    print(ans);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for
// the above approach
using System;

class GFG
{

    // Function to calculate
    // sum of n digit number
    static double getSum(int n)
    {
        double sum = 0;

        // Corner case
        if (n == 1)
        {
            sum = 45.0;
        }

        // Using above approach
        else
        {
            sum = (99.0 / 2.0) *
                    Math.Pow(10, n - 1) *
                    Math.Pow(10, (n - 1) / 2);
        }
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 3;
        double ans = getSum(n);
        Console.Write(ans);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to calculate
// sum of n digit number
function getSum(n)
{

    var sum = 0;
    // Corner case
    if (n == 1) {
        sum = 45.0;
    }
    // Using above approach
    else {
        sum = (99.0 / 2.0) * Math.pow(10, n - 1)
              * Math.pow(10, parseInt((n - 1) / 2));
    }
    return sum;
}

// Driver code
var n = 3;
var ans = getSum(n);
document.write(ans + "<br>");

</script>
```

**Output:** 

```
49500
```

**时间复杂度:** O(1)