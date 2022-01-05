# 检查字符串中不同字符的计数是否为质数

> 原文:[https://www . geesforgeks . org/check-字符串中不同字符的计数是否为质数/](https://www.geeksforgeeks.org/check-whether-count-of-distinct-characters-in-a-string-is-prime-or-not/)

时间复杂度:0((len(str))1/2)

辅助空间:O(len(str))时间复杂度:O((l

给定一串小写英文字母。任务是检查字符串中不同字符的计数是否为质数。

**示例:**

```
Input : str = "geeksforgeeks"
Output :Yes
Explanation: The number of distinct characters in the
string is 7, and 7 is a prime number.

Input : str ="geeks"
Output : No 
```

在这个问题中，首先我们必须[计算字符串](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/)中不同的字符。我们将使用[地图来存储每个字母的频率](https://www.geeksforgeeks.org/java-program-to-count-the-occurrence-of-each-character-in-a-string-using-hashmap/)。下一步是统计不同字符的个数，[检查个数是否为质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。
如果数字是质数，我们会打印是，否则不打印

下面是上述方法的实现:

## C++

```
// C++ program to check whether count of
// distinct characters in a string
// is Prime or not
#include <bits/stdc++.h>
using namespace std;

// Find whether a number is prime or not
bool isPrime(int n)
{
    int i;

    // 1 is not prime
    if (n == 1)
        return false;

    // check if there is any factor or not
    for (i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Count the distinct characters in a string
int countDistinct(string s)
{
    // create a map to store the
    // frequency of characters
    unordered_map<char, int> m;

    // traverse the string
    for (int i = 0; i < s.length(); i++) {
        // increase the frequency of character
        m[s[i]]++;
    }

    return m.size();
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    if (isPrime(countDistinct(str)))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether count of
// distinct characters in a string
// is Prime or not
import java.util.*;

class GFG
{
    // Find whether a number is prime or not
    static boolean isPrime(int n)
    {
        int i;

        // 1 is not prime
        if (n == 1)
            return false;

        // check if there is any factor or not
        for (i = 2; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Count the distinct characters in a string
    static int countDistinct(String s)
    {
        // create a map to store the
        // frequency of characters
        Set<Character> m = new HashSet<Character>();

        // traverse the string
        for (int i = 0; i < s.length(); i++)
        {

            // increase the frequency of character
            m.add(s.charAt(i));

        }

        return m.size();
    }

    // Driver code
    public static void main(String []args)
    {
        String str = "geeksforgeeks";

        if (isPrime(countDistinct(str)))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to check whether
# count of distinct characters in a
# string is Prime or not

# from math library import
# sqrt method
from math import sqrt

# Find whether a number
# is prime or not
def isPrime(n) :

    # 1 is not prime
    if n == 1 :
        return False

    # check if there is any
    # factor or not
    for i in range(2, int(sqrt(n)) + 1) :

        if n % i == 0 :
            return False

    return True

# Count the distinct characters
# in a string
def countDistinct(s) :

    # create a dictionary to store
    # the frequency of characters
    m = {}

    # dictionary with keys and its
    # initialize with value 0
    m = m.fromkeys(s, 0)

    # traverse the string
    for i in range(len(s)) :

        # increase the frequency
        # of character
        m[s[i]] += 1

    return len(m.keys())

# Driver code    
if __name__ == "__main__" :

    str = "geeksforgeeks"

    if isPrime(countDistinct(str)) :
        print("Yes")
    else :
        print("No")

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# program to check whether count of
// distinct characters in a string
// is Prime or not
using System;
using System.Collections.Generic;

class GFG
{
    // Find whether a number is prime or not
    static bool isPrime(int n)
    {
        int i;

        // 1 is not prime
        if (n == 1)
            return false;

        // check if there is any factor or not
        for (i = 2; i <= Math.Sqrt(n); i++)
        {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Count the distinct characters in a string
    static int countDistinct(String s)
    {
        // create a map to store the
        // frequency of characters
        HashSet<char> m = new HashSet<char>();

        // traverse the string
        for (int i = 0; i < s.Length; i++)
        {

            // increase the frequency of character
            m.Add(s[i]);

        }

        return m.Count;
    }

    // Driver code
    public static void Main(String []args)
    {
        String str = "geeksforgeeks";

        if (isPrime(countDistinct(str)))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to check whether count of
// distinct characters in a string
// is Prime or not

// Find whether a number is prime or not
function isPrime(n)
{
    var i;

    // 1 is not prime
    if (n == 1)
        return false;

    // check if there is any factor or not
    for (i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Count the distinct characters in a string
function countDistinct(s)
{
    // create a map to store the
    // frequency of characters
    var m = new Map();

    // traverse the string
    for (var i = 0; i < s.length; i++) {
        // increase the frequency of character
        if(m.has(s[i]))
        {
            m.set(s[i], m[s[i]]+1);
        }
        else
        {
            m.set(s[i],1);
        }
    }

    return m.size;
}

// Driver code
var str = "geeksforgeeks";
if (isPrime(countDistinct(str)))
    document.write( "Yes" );
else
    document.write( "No" );

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
Yes
```

***时间复杂度:** O((len(str)) <sup>1/2</sup> )*

***辅助空间:** O(len(str))*

#### 方法 2:使用计数器功能:

1.  使用计数器功能计算所有元素的频率，频率字典的键数给出计数，并检查它是否是质数。

下面是实现:

## 蟒蛇 3

```
# Python program for the above approach
from collections import Counter
from math import sqrt as sqrt

def isPrime(n):

    # 1 is not prime
    if n == 1:
        return False

    # check if there is any
    # factor or not
    for i in range(2, int(sqrt(n)) + 1):

        if n % i == 0:
            return False

    return True

# Function to count the number of distinct
# characters present in the string
# str and check whether it is prime
def countDis(str):

    # Stores all frequencies
    freq = Counter(str)

    # Return the size of the freq dictionary
    if(isPrime(len(freq))):
        return True
    else:
        return False

# Driver Code
if __name__ == "__main__":

        # Given string S
    S = "geeksforgeeks"

    print(countDis(S))

# This code is contributed by vikkycirus
```

**Output**

```
True
```

**时间复杂度:** O((len(str)) <sup>1/2</sup>

辅助空间:O(len(str))时间复杂度:O((len(str))1/2)

辅助空间:O(len(str)) **输出:**