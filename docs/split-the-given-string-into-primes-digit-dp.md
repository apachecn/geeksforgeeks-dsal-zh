# 将给定的字符串拆分成素数:数字 DP

> 原文:[https://www . geesforgeks . org/将给定字符串拆分为素数位数 dp/](https://www.geeksforgeeks.org/split-the-given-string-into-primes-digit-dp/)

给定一个代表大数的字符串 **str** ，任务是找到给定字符串可以划分的最小段数，使得每个段都是在 **1 到 10<sup>6</sup>T5】范围内的素数。**

**示例:**

> **输入:** str = "13499315"
> **输出:** 3
> **说明:**
> 编号可以分段为【13499，31，5】
> 
> **输入:** str = "43"
> **输出:** 1
> **说明:**
> 数字可分段为【43】

**天真方法:**想法是考虑每个前缀最多 6 位数(因为给出的素数小于 10 <sup>6</sup> )并检查它是否是素数。如果前缀是质数，则递归调用函数来检查剩余的字符串。如果返回非负数，则认为这是一种可能的排列。如果所有可能的组合都没有返回正数，则打印-1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
#include <string>
using namespace std;

// Function to check whether a string
// is a prime number or not
bool checkPrime(string number)
{
    int num = stoi(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A recursive function to find the minimum
// number of segments the given string can
// be divided such that every segment is a prime
int splitIntoPrimes(string number)
{
    // If the number is null
    if (number.length() == 0)
        return 0;

    // checkPrime function is called to check if
    // the number is a prime or not.
    if (number.length() <= 6 and checkPrime(number))
        return 1;

    else {
        int numLen = number.length();

        // A very large number denoting maximum
        int ans = 1000000;

        // Consider a minimum of 6 and length
        // since the primes are less than 10 ^ 6
        for (int i = 1; i <= 6 && i <= numLen; i++) {
            if (checkPrime(number.substr(0, i))) {

                // Recursively call the function
                // to check for the remaining string
                int val = splitIntoPrimes(number.substr(i));
                if (val != -1) {

                    // Evaluating minimum splits
                    // into Primes for the suffix
                    ans = min(ans, 1 + val);
                }
            }
        }

        // Checks if no combination found
        if (ans == 1000000)
            return -1;
        return ans;
    }
}

// Driver code
int main()
{
    cout << splitIntoPrimes("13499315") << "\n";
    cout << splitIntoPrimes("43") << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to check whether a String
// is a prime number or not
static boolean checkPrime(String number)
{
    int num = Integer.valueOf(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A recursive function to find the minimum
// number of segments the given String can
// be divided such that every segment is a prime
static int splitIntoPrimes(String number)
{
    // If the number is null
    if (number.length() == 0)
        return 0;

    // checkPrime function is called to check if
    // the number is a prime or not.
    if (number.length() <= 6 && checkPrime(number))
        return 1;

    else {
        int numLen = number.length();

        // A very large number denoting maximum
        int ans = 1000000;

        // Consider a minimum of 6 and length
        // since the primes are less than 10 ^ 6
        for (int i = 1; i <= 6 && i <= numLen; i++) {
            if (checkPrime(number.substring(0, i))) {

                // Recursively call the function
                // to check for the remaining String
                int val = splitIntoPrimes(number.substring(i));
                if (val != -1) {

                    // Evaluating minimum splits
                    // into Primes for the suffix
                    ans = Math.min(ans, 1 + val);
                }
            }
        }

        // Checks if no combination found
        if (ans == 1000000)
            return -1;
        return ans;
    }
}

// Driver code
public static void main(String[] args)
{
    System.out.print(splitIntoPrimes("13499315")+ "\n");
    System.out.print(splitIntoPrimes("43")+ "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check whether a string
# is a prime number or not
def checkPrime(number) :   
      num = int(number)
      for i in range(2, int(num**0.5)) :
            if((num % i) == 0) :
                 return False
      return True

# A recursive function to find the minimum
# number of segments the given string can
# be divided such that every segment is a prime
def splitIntoPrimes(number) :
      # If the number is null
      if( number == '' ) :
           return 0

      # checkPrime function is called to check if
      # the number is a prime or not.
      if( len(number)<= 6 and checkPrime(number) ) : 
           return 1
      else :
           numLen = len(number)

           # A very large number denoting maximum
           ans = 1000000

           # Consider a minimum of 6 and length
           # since the primes are less than 10 ^ 6
           for i in range( 1, (min( 6, numLen ) + 1) ) :   
                 if( checkPrime( number[:i] ) ) :

                        # Recursively call the function
                        # to check for the remaining string
                        val = splitIntoPrimes( number[i:] )
                        if(val != -1) :

                               # Evaluating minimum splits
                               # into Primes for the suffix
                               ans = min(ans, 1 + val)  

           # Checks if no combination found 
           if( ans == 1000000 ) :  
                 return -1
           return ans

# Driver code
print(splitIntoPrimes("13499315"))
print(splitIntoPrimes("43"))
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to check whether a String
// is a prime number or not
static bool checkPrime(String number)
{
    int num = Int32.Parse(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A recursive function to find the minimum
// number of segments the given String can
// be divided such that every segment is a prime
static int splitIntoPrimes(String number)
{
    // If the number is null
    if (number.Length == 0)
        return 0;

    // checkPrime function is called to check if
    // the number is a prime or not.
    if (number.Length <= 6 && checkPrime(number))
        return 1;

    else {
        int numLen = number.Length;

        // A very large number denoting maximum
        int ans = 1000000;

        // Consider a minimum of 6 and length
        // since the primes are less than 10 ^ 6
        for (int i = 1; i <= 6 && i <= numLen; i++) {
            if (checkPrime(number.Substring(0, i))) {

                // Recursively call the function
                // to check for the remaining String
                int val = splitIntoPrimes(number.Substring(i));
                if (val != -1) {

                    // Evaluating minimum splits
                    // into Primes for the suffix
                    ans = Math.Min(ans, 1 + val);
                }
            }
        }

        // Checks if no combination found
        if (ans == 1000000)
            return -1;
        return ans;
    }
}

// Driver code
public static void Main(String[] args)
{
    Console.Write(splitIntoPrimes("13499315")+ "\n");
    Console.Write(splitIntoPrimes("43")+ "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to check whether a string
// is a prime number or not
function checkPrime(number)
{
    let num = String(number);
    for (let i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A recursive function to find the minimum
// number of segments the given string can
// be divided such that every segment is a prime
function splitIntoPrimes(number)
{
    // If the number is null
    if (number.length == 0)
        return 0;

    // checkPrime function is called to check if
    // the number is a prime or not.
    if (number.length <= 6 && checkPrime(number))
        return 1;

    else {
        let numLen = number.length;

        // A very large number denoting maximum
        let ans = 1000000;

        // Consider a minimum of 6 and length
        // since the primes are less than 10 ^ 6
        for (let i = 1; i <= 6 && i <= numLen; i++) {
            if (checkPrime(number.substr(0, i))) {

                // Recursively call the function
                // to check for the remaining string
                let val = splitIntoPrimes(number.substr(i));
                if (val != -1) {

                    // Evaluating minimum splits
                    // into Primes for the suffix
                    ans = Math.min(ans, 1 + val);
                }
            }
        }

        // Checks if no combination found
        if (ans == 1000000)
            return -1;
        return ans;
    }
}

// Driver code

document.write(splitIntoPrimes("13499315") + "<br>");
document.write(splitIntoPrimes("43") + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
3
1
```

**时间复杂度:**

*   上述方法的时间复杂度为 **O(N <sup>5/2</sup> )** ，其中 N 是输入字符串的长度。
*   递归寻找所有可能组合的复杂度为 **O(N <sup>2</sup> )** 。
*   对于每个组合，为了检查该数是否为质数，使用额外的 **O(N <sup>0.5</sup> )** 时间。
*   这使得时间复杂度 **O(N <sup>5/2</sup> )** 。

**动态规划方法:**给定的问题表现出重叠的子问题性质。因此，动态规划可以有效地解决这个问题。
定义并使用了一个 **splitDP[]** 数组，其中 splitDP[i]表示长度为“I”的前缀字符串中将其分解为素数细分所需的最小分割数。
splitDP[]数组的填充方式如下:

*   for 循环用于遍历给定字符串的所有索引。
*   对于上述循环中的每个索引“I”，从 1 到 6 迭代另一个循环，以检查来自第(i + j) <sup>个索引的子串是否形成素数。</sup>
*   如果它形成一个质数，那么 splitDP[]处的值更新为:

```
splitDP[i + j] = min(splitDP[i + j], 1 + splitDP[i]);
```

*   更新数组的所有值后，最后一个索引处的值是整个字符串的最小拆分数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a string
// is a prime number or not
bool checkPrime(string number)
{
    int num = stoi(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A function to find the minimum
// number of segments the given string
// can be divided such that every
// segment is a prime
int splitIntoPrimes(string number)
{
    int numLen = number.length();

    // Declare a splitdp[] array
    // and initialize to -1
    int splitDP[numLen + 1];
    memset(splitDP, -1, sizeof(splitDP));

    // Build the DP table in
    // a bottom-up manner
    for (int i = 1; i <= numLen; i++) {

        // Initially Check if the entire prefix is Prime
        if (i <= 6 && checkPrime(number.substr(0, i)))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining string from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (int j = 1; j <= 6 && i + j <= numLen; j++) {

                // To check if the substring from i to j
                // is a prime number or not
                if (checkPrime(number.substr(i, j))) {

                    // If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire string
    return splitDP[numLen];
}

// Driver code
int main()
{
    cout << splitIntoPrimes("13499315") << "\n";
    cout << splitIntoPrimes("43") << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;

class GFG{

// Function to check whether a String
// is a prime number or not
static boolean checkPrime(String number)
{
    if(number.length()==0)
        return true;
    int num = Integer.parseInt(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A function to find the minimum
// number of segments the given String
// can be divided such that every
// segment is a prime
static int splitIntoPrimes(String number)
{
    int numLen = number.length();

    // Declare a splitdp[] array
    // and initialize to -1
    int []splitDP = new int[numLen + 1];
    Arrays.fill(splitDP, -1);

    // Build the DP table in
    // a bottom-up manner
    for (int i = 1; i <= numLen; i++) {

        // Initially Check if the entire prefix is Prime
        if (i <= 6 && checkPrime(number.substring(0, i)))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining String from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (int j = 1; j <= 6 && i + j <= numLen; j++) {

                // To check if the subString from i to j
                // is a prime number or not
                if (checkPrime(number.substring(i, i+j))) {

                    // If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = Math.min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire String
    return splitDP[numLen];
}

// Driver code
public static void main(String[] args)
{
    System.out.print(splitIntoPrimes("13499315")+ "\n");
    System.out.print(splitIntoPrimes("43")+ "\n");
}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach
from math import sqrt

# Function to check whether a string
# is a prime number or not
def checkPrime(number):
    if(len(number) == 0):
        return True
    num = int(number)
    for i in range(2,int(sqrt(num)) + 1, 1):
        if ((num % i) == 0):
            return False
    return True

# A function to find the minimum
# number of segments the given string
# can be divided such that every
# segment is a prime
def splitIntoPrimes(number):
    numLen = len(number)

    # Declare a splitdp[] array
    # and initialize to -1
    splitDP = [-1 for i in range(numLen + 1)]

    # Build the DP table in
    # a bottom-up manner
    for i in range(1, numLen + 1, 1):

        # Initially Check if the entire prefix is Prime
        if (i <= 6 and checkPrime(number[0:i])):
            splitDP[i] = 1

        # If the Given Prefix can be split into Primes
        # then for the remaining string from i to j
        # Check if Prime. If yes calculate
        # the minimum split till j
        if (splitDP[i] != -1):
            j = 1
            while(j <= 6 and i + j <= numLen):

                # To check if the substring from i to j
                # is a prime number or not
                if (checkPrime(number[i:i+j])):

                    # If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1):
                        splitDP[i + j] = 1 + splitDP[i]
                    else:
                        splitDP[i + j] = min(splitDP[i + j], 1 + splitDP[i])
                j += 1

    # Return the minimum number of splits
    # for the entire string
    return splitDP[numLen]

# Driver code
if __name__ == '__main__':
    print(splitIntoPrimes("13499315"))
    print(splitIntoPrimes("43"))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to check whether a String
// is a prime number or not
static bool checkPrime(String number)
{
    if(number.Length==0)
        return true;
    int num = Int32.Parse(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return true;
}

// A function to find the minimum
// number of segments the given String
// can be divided such that every
// segment is a prime
static int splitIntoPrimes(String number)
{
    int numLen = number.Length;

    // Declare a splitdp[] array
    // and initialize to -1
    int []splitDP = new int[numLen + 1];
    for (int i = 0; i <= numLen; i++)
        splitDP[i] = -1;

    // Build the DP table in
    // a bottom-up manner
    for (int i = 1; i <= numLen; i++) {

        // Initially Check if the entire prefix is Prime
        if (i <= 6 && checkPrime(number.Substring(0, i)))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining String from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (int j = 1; j <= 6 && i + j <= numLen; j++) {

                // To check if the subString from i to j
                // is a prime number or not
                if (checkPrime(number.Substring(i, j))) {

                    // If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = Math.Min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire String
    return splitDP[numLen];
}

// Driver code
public static void Main(String[] args)
{
    Console.Write(splitIntoPrimes("13499315")+ "\n");
    Console.Write(splitIntoPrimes("43")+ "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check whether a String
// is a prime number or not
function checkPrime(number)
{
    if (number.length == 0)
        return true;

    let num = parseInt(number);
    for(let i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;

    return true;
}

// A function to find the minimum
// number of segments the given String
// can be divided such that every
// segment is a prime
function splitIntoPrimes(number)
{
    let numLen = number.length;

    // Declare a splitdp[] array
    // and initialize to -1
    let splitDP = new Array(numLen + 1);
    for(let i = 0; i < splitDP.length; i++)
    {
        splitDP[i] = -1;
    }

    // Build the DP table in
    // a bottom-up manner
    for(let i = 1; i <= numLen; i++)
    {

        // Initially Check if the entire prefix is Prime
        if (i <= 6 && checkPrime(number.substring(0, i)))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining String from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1)
        {
            for(let j = 1;
                    j <= 6 && i + j <= numLen;
                    j++)
            {

                // To check if the subString from i to j
                // is a prime number or not
                if (checkPrime(number.substring(i, i + j)))
                {

                    // If it is a prime, then update the
                    // dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = Math.min(
                            splitDP[i + j],
                                    1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire String
    return splitDP[numLen];
}

// Driver code
document.write(splitIntoPrimes("13499315") + "<br>");
document.write(splitIntoPrimes("43") + "<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
1
```

**时间复杂度:**

*   上述方法的时间复杂度为 **O(N <sup>3/2</sup> )** ，其中 N 是输入字符串的长度。
*   遍历所有索引的时间为 **O(N)** 。
*   因为内部 for 循环对于每个索引运行的次数是恒定的，所以它的运行时间可以被认为是恒定的。
*   对于每个指数，检查数字是否为质数的时间为 **O(N <sup>0.5</sup> )** 。
*   因此，整体时间复杂度为 **O(N <sup>3/2</sup> )** 。

**优化动态规划法:**利用厄拉多塞的概念[筛预先计算并存储一个数是否为素数，降低每次迭代检查一个数的时间复杂度，可以进一步优化上述方法。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to precompute all the primes
// upto 1000000 and store it in a set
// using Sieve of Eratosthenes
void getPrimesFromSeive(set<string>& primes)
{
    bool prime[1000001];
    memset(prime, true, sizeof(prime));
    prime[0] = prime[1] = false;
    for (int i = 2; i * i <= 1000000; i++) {
        if (prime[i] == true) {
            for (int j = i * i; j <= 1000000; j += i)
                prime[j] = false;
        }
    }

    // Here to_string() is used
    // for converting int to string
    for (int i = 2; i <= 1000000; i++) {
        if (prime[i] == true)
            primes.insert(to_string(i));
    }
}

// A function to find the minimum
// number of segments the given string
// can be divided such that every
// segment is a prime
int splitIntoPrimes(string number)
{
    int numLen = number.length();

    // Declare a splitdp[] array
    // and initialize to -1
    int splitDP[numLen + 1];
    memset(splitDP, -1, sizeof(splitDP));

    // Call sieve function to store primes in
    // primes array
    set<string> primes;
    getPrimesFromSeive(primes);

    // Build the DP table in a bottom-up manner
    for (int i = 1; i <= numLen; i++) {

        // If the prefix is prime then the prefix
        // will be found in the prime set
        if (i <= 6 && (primes.find(number.substr(0, i))
                       != primes.end()))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining string from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (int j = 1; j <= 6 && i + j <= numLen; j++) {

                // To check if the substring from i to j
                // is a prime number or not
                if (primes.find(number.substr(i, j))
                    != primes.end()) {

                    // If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire string
    return splitDP[numLen];
}

int main()
{
    cout << splitIntoPrimes("13499315") << "\n";
    cout << splitIntoPrimes("43") << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;

class GFG{

// Function to precompute all the primes
// upto 1000000 and store it in a set
// using Sieve of Eratosthenes
static void getPrimesFromSeive(HashSet<String> primes)
{
    boolean []prime = new boolean[1000001];
    Arrays.fill(prime, true);
    prime[0] = prime[1] = false;
    for (int i = 2; i * i <= 1000000; i++) {
        if (prime[i] == true) {
            for (int j = i * i; j <= 1000000; j += i)
                prime[j] = false;
        }
    }

    // Here to_String() is used
    // for converting int to String
    for (int i = 2; i <= 1000000; i++) {
        if (prime[i] == true)
            primes.add(String.valueOf(i));
    }
}

// A function to find the minimum
// number of segments the given String
// can be divided such that every
// segment is a prime
static int splitIntoPrimes(String number)
{
    int numLen = number.length();

    // Declare a splitdp[] array
    // and initialize to -1
    int []splitDP = new int[numLen + 1];
    Arrays.fill(splitDP, -1);

    // Call sieve function to store primes in
    // primes array
    HashSet<String> primes = new HashSet<String>();
    getPrimesFromSeive(primes);

    // Build the DP table in a bottom-up manner
    for (int i = 1; i <= numLen; i++) {

        // If the prefix is prime then the prefix
        // will be found in the prime set
        if (i <= 6 && (primes.contains(number.substring(0, i))))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining String from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (int j = 1; j <= 6 && i + j <= numLen; j++) {

                // To check if the subString from i to j
                // is a prime number or not
                if (primes.contains(number.substring(i, i+j))) {

                    // If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = Math.min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire String
    return splitDP[numLen];
}

public static void main(String[] args)
{
    System.out.print(splitIntoPrimes("13499315")+ "\n");
    System.out.print(splitIntoPrimes("43")+ "\n");
}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to precompute all the primes
# upto 1000000 and store it in a set
# using Sieve of Eratosthenes
def getPrimesFromSeive(primes):

    prime = [True] * (1000001)
    prime[0], prime[1] = False, False
    i = 2
    while (i * i <= 1000000):
        if (prime[i] == True):
            for j in range(i * i, 1000001, i):
                prime[j] = False
        i += 1

    # Here str() is used for
    # converting int to string
    for i in range(2, 1000001):
        if (prime[i] == True):
            primes.append(str(i))

# A function to find the minimum
# number of segments the given string
# can be divided such that every
# segment is a prime
def splitIntoPrimes(number):

    numLen = len(number)

    # Declare a splitdp[] array
    # and initialize to -1
    splitDP = [-1] * (numLen + 1)

    # Call sieve function to store
    # primes in primes array
    primes = []
    getPrimesFromSeive(primes)

    # Build the DP table in a bottom-up manner
    for i in range(1, numLen + 1):

        # If the prefix is prime then the prefix
        # will be found in the prime set
        if (i <= 6 and (number[0 : i] in primes)):
            splitDP[i] = 1

        # If the Given Prefix can be split into Primes
        # then for the remaining string from i to j
        # Check if Prime. If yes calculate
        # the minimum split till j
        if (splitDP[i] != -1):
            j = 1
            while (j <= 6 and (i + j <= numLen)):

                # To check if the substring from i to j
                # is a prime number or not
                if (number[i : i + j] in primes):

                    # If it is a prime, then
                    # update the dp array
                    if (splitDP[i + j] == -1):
                        splitDP[i + j] = 1 + splitDP[i]
                    else:
                        splitDP[i + j] = min(splitDP[i + j],
                                         1 + splitDP[i])

                j += 1

    # Return the minimum number of
    # splits for the entire string
    return splitDP[numLen]

# Driver code
print(splitIntoPrimes("13499315"))
print(splitIntoPrimes("43"))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to precompute all the primes
// upto 1000000 and store it in a set
// using Sieve of Eratosthenes
static void getPrimesFromSeive(HashSet<String> primes)
{
    bool []prime = new bool[1000001];

    for(int i = 0; i < 1000001; i++)
       prime[i] = true;
    prime[0] = prime[1] = false;

    for(int i = 2; i * i <= 1000000; i++)
    {
       if (prime[i] == true)
       {
           for(int j = i * i; j <= 1000000; j += i)
              prime[j] = false;
       }
    }

    // Converting int to String
    for(int i = 2; i <= 1000000; i++)
    {
       if (prime[i] == true)
           primes.Add(String.Join("", i));
    }
}

// A function to find the minimum
// number of segments the given String
// can be divided such that every
// segment is a prime
static int splitIntoPrimes(String number)
{
    int numLen = number.Length;

    // Declare a splitdp[] array
    // and initialize to -1
    int []splitDP = new int[numLen + 1];
    for(int i = 0; i < numLen + 1; i++)
       splitDP[i] = -1;

    // Call sieve function to store primes
    // in primes array
    HashSet<String> primes = new HashSet<String>();
    getPrimesFromSeive(primes);

    // Build the DP table in a bottom-up manner
    for(int i = 1; i <= numLen; i++)
    {

       // If the prefix is prime then the prefix
       // will be found in the prime set
       if (i <= 6 && (primes.Contains
                     (number.Substring(0, i))))
           splitDP[i] = 1;

       // If the given prefix can be split into
       // primes, then for the remaining String
       // from i to j check if prime. If yes
       // calculate the minimum split till j
       if (splitDP[i] != -1)
       {
           for(int j = 1; j <= 6 && i + j <= numLen; j++)
           {

              // To check if the subString from
              // i to j is a prime number or not
              if (primes.Contains(number.Substring(i, j)))
              {

                  // If it is a prime, then update
                  // the dp array
                  if (splitDP[i + j] == -1)
                      splitDP[i + j] = 1 + splitDP[i];
                  else
                      splitDP[i + j] = Math.Min(splitDP[i + j],
                                            1 + splitDP[i]);
              }
           }
       }
    }

    // Return the minimum number of
    // splits for the entire String
    return splitDP[numLen];
}

public static void Main(String[] args)
{
    Console.Write(splitIntoPrimes("13499315") + "\n");
    Console.Write(splitIntoPrimes("43") + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to precompute all the primes
// upto 1000000 and store it in a set
// using Sieve of Eratosthenes
function getPrimesFromSeive(primes)
{
    let prime = new Array(1000001);
    for(let i=0;i<prime.length;i++)
    {
        prime[i]=true;
    }
    prime[0] = prime[1] = false;
    for (let i = 2; i * i <= 1000000; i++) {
        if (prime[i] == true) {
            for (let j = i * i; j <= 1000000; j += i)
                prime[j] = false;
        }
    }

    // Here to_String() is used
    // for converting int to String
    for (let i = 2; i <= 1000000; i++) {
        if (prime[i] == true)
            primes.add((i).toString());
    }
}

// A function to find the minimum
// number of segments the given String
// can be divided such that every
// segment is a prime
function splitIntoPrimes(number)
{
    let numLen = number.length;

    // Declare a splitdp[] array
    // and initialize to -1
    let splitDP = new Array(numLen + 1);
    for(let i=0;i<splitDP.length;i++)
    {
        splitDP[i]=-1;
    }

    // Call sieve function to store primes in
    // primes array
    let primes = new Set();
    getPrimesFromSeive(primes);

    // Build the DP table in a bottom-up manner
    for (let i = 1; i <= numLen; i++) {

        // If the prefix is prime then the prefix
        // will be found in the prime set
        if (i <= 6 && (primes.has(number.substring(0, i))))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Primes
        // then for the remaining String from i to j
        // Check if Prime. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (let j = 1; j <= 6 && i + j <= numLen; j++) {

                // To check if the subString from i to j
                // is a prime number or not
                if (primes.has(number.substring(i, i+j))) {

                    // If it is a prime, then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];
                    else
                        splitDP[i + j] = Math.min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire String
    return splitDP[numLen];
}

document.write(splitIntoPrimes("13499315")+ "<br>");
document.write(splitIntoPrimes("43")+ "<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
3
1
```

**时间复杂度:**

*   这是最有效的方法，因为这在 **O(N)** 时间复杂度中运行，其中 N 是输入字符串的长度。
*   由于厄拉多塞的筛子运行时间为 **O(N*log(log(N)))** ，素数列表最多为 10 个 <sup>6</sup> ，因此可以计算预计算复杂度。但是，由于对于任何数量的字符串，这都只执行一次，因此在计算时间复杂度时不计算在内。