# 给定数字的平方位数之和，其位数只有 1

> 原文:[https://www . geeksforgeeks . org/给定数字的平方位数之和，它的位数只有 1/](https://www.geeksforgeeks.org/sum-of-the-digits-of-square-of-the-given-number-which-has-only-1s-as-its-digits/)

给定一个由数字 **1** 组成的字符串**字符串**表示的数字，即 **1，11，111，…** 。任务是找出给定数字平方的位数总和。

**示例:**

> **输入:** str = 11
> **输出:**4
> 11<sup>2</sup>= 121
> 1+2+1 = 4
> 
> **输入:**str = 1111
> T3】输出: 16

**天真法:**求给定数的平方，然后求其位数之和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum
// of the digits of num ^ 2
int squareDigitSum(string number)
{
    int summ = 0;
    int num = stoi(number);

    // Store the square of num
    int squareNum = num * num;

    // Find the sum of its digits
    while(squareNum > 0)
    {
        summ = summ + (squareNum % 10);
        squareNum = squareNum / 10;
    }
    return summ;
}

// Driver code
int main()
{
    string N = "1111";

    cout << squareDigitSum(N);

    return 0;
}

// This code is contributed by Princi Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
// Java implementation of the approach
class GFG
{

// Function to return the sum
// of the digits of num ^ 2
static int squareDigitSum(String number)
{
    int summ = 0;
    int num = Integer.parseInt(number);

    // Store the square of num
    int squareNum = num * num;

    // Find the sum of its digits
    while(squareNum > 0)
    {
        summ = summ + (squareNum % 10);
        squareNum = squareNum / 10;
    }
    return summ;
}

// Driver code
public static void main (String[] args)
{
    String N = "1111";

    System.out.println(squareDigitSum(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum
# of the digits of num ^ 2
def squareDigitSum(num):

    summ = 0
    num = int(num)

    # Store the square of num
    squareNum = num * num

    # Find the sum of its digits
    while squareNum > 0:
        summ = summ + (squareNum % 10)
        squareNum = squareNum//10

    return summ

# Driver code
if __name__ == "__main__":

    N = "1111"
    print(squareDigitSum(N))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the sum
    // of the digits of num ^ 2
    static int squareDigitSum(String number)
    {
        int summ = 0;
        int num = int.Parse(number);

        // Store the square of num
        int squareNum = num * num;

        // Find the sum of its digits
        while(squareNum > 0)
        {
            summ = summ + (squareNum % 10);
            squareNum = squareNum / 10;
        }
        return summ;
    }

    // Driver code
    public static void Main (String[] args)
    {
        String s = "1111";

        Console.WriteLine(squareDigitSum(s));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum
// of the digits of num ^ 2
function squareDigitSum(number)
{
    var summ = 0;
    var num = parseInt(number);

    // Store the square of num
    var squareNum = num * num;

    // Find the sum of its digits
    while (squareNum > 0)
    {
        summ = summ + (squareNum % 10);
        squareNum = parseInt(squareNum / 10);
    }
    return summ;
}

// Driver code
var N = "1111";

document.write(squareDigitSum(N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
16
```

**高效逼近:**可以观察到，在给定数的平方内，序列**【1，2，3，4，5，6，7，9，0】**在左边部分重复，序列**【0，9，8，7，6，5，4，3，2，1】**在右边部分重复。这两个序列都出现 **floor(length(str) / 9)** 次，并且这两个序列的总和是 81，并且数字的平方在最后增加了额外的 **1** 。
所以，所有这些的总和将是**【楼层(长度(str)/9)】* 81+1**。
中间的数字有一个序列，比如如果**长度(str) % 9 = a** ，那么中间的序列就是**【1，2，3……。a、a–1、a–2、… 2]** 。现在可以观察到这部分**【1，2，3】的和。a]** 等于 **(a * (a + 1)) / 2** ，另一部分**【a–1，a–2，… 2】之和为**((a *(a–1))/2)–1**。
**总和** =楼层(长度(str) / 9) * 81 + 1 +(长度(str)% 9)<sup>2</sup>–1 =**楼层(长度(str) / 9) * 81 +(长度(str) % 9) <sup>2</sup>** 。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define lli long long int

// Function to return the sum
// of the digits of num^2
lli squareDigitSum(string s)
{
    // To store the number of 1's
    lli lengthN = s.length();

    // Find the sum of the digits of num^2
    lli result = (lengthN / 9) * 81
                 + pow((lengthN % 9), 2);

    return result;
}

// Driver code
int main()
{
    string s = "1111";

    cout << squareDigitSum(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the sum
    // of the digits of num^2
    static long squareDigitSum(String s)
    {
        // To store the number of 1's
        long lengthN = s.length();

        // Find the sum of the digits of num^2
        long result = (lengthN / 9) * 81 +
                      (long)Math.pow((lengthN % 9), 2);

        return result;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "1111";

        System.out.println(squareDigitSum(s));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum
# of the digits of num ^ 2
def squareDigitSum(num):

    # To store the number of 1's
    lengthN = len(num)

    # Find the sum of the digits of num ^ 2
    result = (lengthN//9)*81 + (lengthN % 9)**2

    return result

# Driver code
if __name__ == "__main__" :

    N = "1111"
    print(squareDigitSum(N))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the sum
// of the digits of num^2
static long squareDigitSum(String s)
{
    // To store the number of 1's
    long lengthN = s.Length;

    // Find the sum of the digits of num^2
    long result = (lengthN / 9) * 81 +
                  (long)Math.Pow((lengthN % 9), 2);

    return result;
}

// Driver code
public static void Main (String[] args)
{
    String s = "1111";

    Console.WriteLine(squareDigitSum(s));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum
// of the digits of num^2
function squareDigitSum(s)
{
    // To store the number of 1's
    let lengthN = s.length;

    // Find the sum of the digits of num^2
    let result = parseInt(lengthN / 9) * 81
                 + Math.pow((lengthN % 9), 2);

    return result;
}

// Driver code
    let s = "1111";

    document.write(squareDigitSum(s));

</script>
```

**Output:** 

```
16
```

**时间复杂度** O(1)