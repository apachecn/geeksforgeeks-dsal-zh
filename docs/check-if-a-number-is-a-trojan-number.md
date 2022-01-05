# 检查一个号码是否是木马号码

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-特洛伊-number/](https://www.geeksforgeeks.org/check-if-a-number-is-a-trojan-number/)

给定一个数字![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")。任务是检查 N 是否是木马号码。
**木马号**是一个属于[强号](https://www.geeksforgeeks.org/program-to-check-strong-number/)但不是完美力量的号。如果对于 N 的每个素除数或因子 p，p2 也是一个除数，那么 N 就是一个强数。换句话说，每个质因数至少出现两次。
所有木马号都很强。但是，并不是所有的强号都是木马号:只有那些不能表示为 m <sup>k</sup> 的，其中 m 和 k 都是大于 1 的正整数。
**示例** :

```
Input : N = 108
Output : YES

Input : N = 8
Output : NO
```

这个想法是存储每个质因数的计数，如果计数大于 2，那么它将是一个**强数**。
这个部分很容易通过筛[素因子分解计算出来。
下一步是检查给定的数字是否不能表示为 x <sup>y</sup> 。要检查一个数字是否为**完美功率**请参考](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)[这篇](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-xy-x-raised-to-power-y/)文章。
以下是上述问题的实现:

## C++

```
// CPP program to check if a number is
// Trojan Number or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// can be expressed as x^y
bool isPerfectPower(int n)
{
    if (n == 1)
        return true;

    // Try all numbers from 2 to sqrt(n) as base
    for (int x = 2; x <= sqrt(n); x++) {
        int y = 2;
        int p = pow(x, y);

        // Keep increasing y while power 'p'
        // is smaller than n.
        while (p <= n && p > 0) {
            if (p == n)
                return true;
            y++;
            p = pow(x, y);
        }
    }
    return false;
}

// Function to check if a number is Strong
bool isStrongNumber(int n)
{
    unordered_map<int, int> count;
    while (n % 2 == 0) {
        n = n / 2;
        count[2]++;
    }

    // count the number for each prime factor
    for (int i = 3; i <= sqrt(n); i += 2) {
        while (n % i == 0) {
            n = n / i;
            count[i]++;
        }
    }

    if (n > 2)
        count[n]++;

    int flag = 0;

    for (auto b : count) {

        // minimum number of prime divisors
        // should be 2
        if (b.second == 1) {
            flag = 1;
            break;
        }
    }

    if (flag == 1)
        return false;
    else
        return true;
}

// Function to check if a number
// is Trojan Number
bool isTrojan(int n)
{
    if (!isPerfectPower(n) && isStrongNumber(n))
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int n = 108;

    if (isTrojan(n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// Trojan Number or not
import java.util.*;

class GFG
{

    // Function to check if a number
    // can be expressed as x^y
    static boolean isPerfectPower(int n)
    {
        if (n == 1)
        {
            return true;
        }

        // Try all numbers from 2 to sqrt(n) as base
        for (int x = 2; x <= Math.sqrt(n); x++)
        {
            int y = 2;
            int p = (int) Math.pow(x, y);

            // Keep increasing y while power 'p'
            // is smaller than n.
            while (p <= n && p > 0)
            {
                if (p == n)
                {
                    return true;
                }
                y++;
                p = (int) Math.pow(x, y);
            }
        }
        return false;
    }

    // Function to check if a number is Strong
    static boolean isStrongNumber(int n)
    {
        HashMap<Integer,
                Integer> count = new HashMap<Integer,
                                             Integer>();
        while (n % 2 == 0)
        {
            n = n / 2;
            if (count.containsKey(2))
            {
                count.put(2, count.get(2) + 1);
            }
            else
            {
                count.put(2, 1);
            }
        }

        // count the number for each prime factor
        for (int i = 3; i <= Math.sqrt(n); i += 2)
        {
            while (n % i == 0)
            {
                n = n / i;
                if (count.containsKey(i))
                {
                    count.put(i, count.get(i) + 1);
                }
                else
                {
                    count.put(i, 1);
                }
            }
        }

        if (n > 2)
        {
            if (count.containsKey(n))
            {
                count.put(n, count.get(n) + 1);
            }
            else
            {
                count.put(n, 1);
            }
        }

        int flag = 0;

        for (Map.Entry<Integer,
                       Integer> b : count.entrySet())
        {

            // minimum number of prime divisors
            // should be 2
            if (b.getValue() == 1)
            {
                flag = 1;
                break;
            }
        }

        if (flag == 1)
        {
            return false;
        }
        else
        {
            return true;
        }
    }

    // Function to check if a number
    // is Trojan Number
    static boolean isTrojan(int n)
    {
        if (!isPerfectPower(n) && isStrongNumber(n))
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 108;

        if (isTrojan(n))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to check if a number
# is Trojan Number or not
from math import sqrt, pow

# Function to check if a number
# can be expressed as x^y
def isPerfectPower(n):
    if n == 1:
        return True

    # Try all numbers from 2 to
    # sqrt(n) as base
    for x in range(2, int(sqrt(n)) + 1):
        y = 2
        p = pow(x, y)

        # Keep increasing y while power
        # 'p' is smaller than n.
        while p <= n and p > 0:
            if p == n:
                return True
            y += 1
            p = pow(x, y)

    return False

# Function to check if a number
# is Strong
def isStrongNumber(n):
    count = {i:0 for i in range(n)}
    while n % 2 == 0:
        n = n // 2
        count[2] += 1

    # count the number for each
    # prime factor
    for i in range(3,int(sqrt(n)) + 1, 2):
        while n % i == 0:
            n = n // i
            count[i] += 1

    if n > 2:
        count[n] += 1

    flag = 0

    for key,value in count.items():

        # minimum number of prime
        # divisors should be 2
        if value == 1:
            flag = 1
            break

    if flag == 1:
        return False
    return True

# Function to check if a number
# is Trojan Number
def isTrojan(n):
    return isPerfectPower(n) == False and isStrongNumber(n)

# Driver Code
if __name__ == '__main__':
    n = 108

    if (isTrojan(n)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check if a number is
// Trojan Number or not
using System;
using System.Collections.Generic;

class GFG
{

    // Function to check if a number
    // can be expressed as x^y
    static bool isPerfectPower(int n)
    {
        if (n == 1)
        {
            return true;
        }

        // Try all numbers from 2 to sqrt(n) as base
        for (int x = 2; x <= Math.Sqrt(n); x++)
        {
            int y = 2;
            int p = (int) Math.Pow(x, y);

            // Keep increasing y while power 'p'
            // is smaller than n.
            while (p <= n && p > 0)
            {
                if (p == n)
                {
                    return true;
                }
                y++;
                p = (int) Math.Pow(x, y);
            }
        }
        return false;
    }

    // Function to check if a number is Strong
    static bool isStrongNumber(int n)
    {
        Dictionary<int,
                   int> count = new Dictionary<int,
                                               int>();
        while (n % 2 == 0)
        {
            n = n / 2;
            if (count.ContainsKey(2))
            {
                count[2] = count[2] + 1;
            }
            else
            {
                count.Add(2, 1);
            }
        }

        // count the number for each prime factor
        for (int i = 3; i <= Math.Sqrt(n); i += 2)
        {
            while (n % i == 0)
            {
                n = n / i;
                if (count.ContainsKey(i))
                {
                    count[i] = count[i] + 1;
                }
                else
                {
                    count.Add(i, 1);
                }
            }
        }

        if (n > 2)
        {
            if (count.ContainsKey(n))
            {
                count[n] = count[n] + 1;
            }
            else
            {
                count.Add(n, 1);
            }
        }

        int flag = 0;

        foreach(KeyValuePair<int, int> b in count)
        {

            // minimum number of prime divisors
            // should be 2
            if (b.Value == 1)
            {
                flag = 1;
                break;
            }
        }

        if (flag == 1)
        {
            return false;
        }
        else
        {
            return true;
        }
    }

    // Function to check if a number
    // is Trojan Number
    static bool isTrojan(int n)
    {
        if (!isPerfectPower(n) &&
             isStrongNumber(n))
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 108;

        if (isTrojan(n))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript program to check if a number is
// Trojan Number or not

    // Function to check if a number
    // can be expressed as x^y
    function isPerfectPower(n) {
        if (n == 1) {
            return true;
        }

        // Try all numbers from 2 to sqrt(n) as base
        for (var x = 2; x <= Math.sqrt(n); x++) {
            var y = 2;
            var p = parseInt( Math.pow(x, y));

            // Keep increasing y while power 'p'
            // is smaller than n.
            while (p <= n && p > 0) {
                if (p == n) {
                    return true;
                }
                y++;
                p = parseInt( Math.pow(x, y));
            }
        }
        return false;
    }

    // Function to check if a number is Strong
    function isStrongNumber(n) {
        var count = new Map();
        while (n % 2 == 0) {
            n = n / 2;
            if (count.has(2)) {
                count.set(2, count.get(2) + 1);
            } else {
                count.set(2, 1);
            }
        }

        // count the number for each prime factor
        for (var i = 3; i <= Math.sqrt(n); i += 2) {
            while (n % i == 0) {
                n = n / i;
                if (count.has(i)) {
                    count.set(i, count.get(i) + 1);
                } else {
                    count.set(i, 1);
                }
            }
        }

        if (n > 2) {
            if (count.has(n)) {
                count.set(n, count.get(n) + 1);
            } else {
                count.set(n, 1);
            }
        }

        var flag = 0;
 const iterator = count[Symbol.iterator]();
    let itr = iterator.next()
    for (let i = 0; i < count.size; i++) {
        console.log(itr.value, itr.done)
        if (itr.value == 1) {
                flag = 1;
                break;
            }
        itr = iterator.next()
    }

        if (flag == 1) {
            return false;
        } else {
            return true;
        }
    }

    // Function to check if a number
    // is Trojan Number
    function isTrojan(n) {
        if (!isPerfectPower(n) && isStrongNumber(n)) {
            return true;
        } else {
            return false;
        }
    }

    // Driver Code

        var n = 108;

        if (isTrojan(n)) {
            document.write("Yes");
        } else {
            document.write("No");
        }

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
YES
```