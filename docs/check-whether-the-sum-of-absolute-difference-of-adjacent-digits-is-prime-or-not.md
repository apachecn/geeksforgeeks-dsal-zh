# 检查相邻数字的绝对差之和是否为素数

> 原文:[https://www . geesforgeks . org/check-相邻数字的绝对差之和是否为质数/](https://www.geeksforgeeks.org/check-whether-the-sum-of-absolute-difference-of-adjacent-digits-is-prime-or-not/)

给定一个数字 a **N** ，任务是检查相邻数字的绝对差之和是否为素数。

**示例:**

```
Input: N = 142 
Output: Prime
Sum = |1-4| + |4-2| = 5 i.e. prime.

Input: N = 347
Output: Not prime 
```

**逼近**:求相邻数字的绝对差之和，然后检查该和是否为[素数](https://www.geeksforgeeks.org/prime-numbers/)。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>

using namespace std;

// Function to check for a prime number
bool Prime(int n){

    if( n == 1){
        return false;
            }
    for (int i=2;i*i<=n;i++){
        if (n % i == 0)
            return false;
                    }
    return true;
}

// Function to find the sum of array
bool checkSumPrime(string st){
    int summ = 0;
    for (int i=1;i<st.size();i++)
        summ+= abs(st[i-1]-st[i]);

    if(Prime(summ))
        return true;
    else
        return false;
}

// Driver code
int main(){

    int num = 142;

    string s= "142";

    if (checkSumPrime(s))
        cout<<"Prime\n";
    else
        cout<<"Not Prime\n";

return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to check for a prime number
    static boolean Prime(int n)
    {
        if (n == 1)
            return false;
        for (int i = 2; i * i <= n; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    // Function to find the sum of array
    static boolean checkSumPrime(String str)
    {
        int summ = 0;
        for (int i = 1; i < str.length(); i++)
            summ += Math.abs(str.charAt(i - 1) -
                             str.charAt(i));

        if (Prime(summ))
            return true;
        else
            return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int num = 142;
        String str = "142";
        if (checkSumPrime(str))
            System.out.println("Prime");
        else
            System.out.println("Not Prime");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import math as mt

# Function to check for a prime number
def Prime(n):

    if n == 1:
        return False

    for i in range(2, mt.ceil(mt.sqrt(n + 1))):
        if n % i == 0:
            return False
    return True

# Function to find the sum of array
def checkSumPrime(string):
    summ = 0
    for i in range(1, len(string)):
        summ += abs(int(string[i - 1]) -
                    int(string[i]))

    if Prime(summ):
        return True
    else:
        return False

# Driver code
num = 142

string = str(num)

s = [i for i in string]

if checkSumPrime(s):
    print("Prime")
else:
    print("Not Prime\n")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to check for a prime number
    static bool Prime(int n)
    {
        if (n == 1)
            return false;
        for (int i = 2; i * i <= n; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    // Function to find the sum of array
    static bool checkSumPrime(String str)
    {
        int summ = 0;
        for (int i = 1; i < str.Length; i++)
            summ += Math.Abs(str[i - 1] -
                             str[i]);

        if (Prime(summ))
            return true;
        else
            return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "142";
        if (checkSumPrime(str))
            Console.WriteLine("Prime");
        else
            Console.WriteLine("Not Prime");
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check for a prime number
function Prime(n)
{
    if (n == 1)
        return false;

    for(let i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find the sum of array
function checkSumPrime(str)
{
    let summ = 0;
    for(let i = 1; i < str.length; i++)
        summ += Math.abs(str[i - 1]-
                         str[i]);

    if (Prime(summ))
        return true;
    else
        return false;
}

// Driver Code
let num = 142;
let str = "142";

if (checkSumPrime(str))
    document.write("Prime");
else
    document.write("Not Prime");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Prime
```

***时间复杂度:** O(和 <sup>1/2</sup> ，其中****和**是数字*位数的和

***辅助空间:** O(1)*