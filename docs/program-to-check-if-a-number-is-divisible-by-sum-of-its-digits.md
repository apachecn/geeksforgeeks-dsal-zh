# 检查一个数是否能被它的数字的和整除的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果一个数被其位数的和整除/](https://www.geeksforgeeks.org/program-to-check-if-a-number-is-divisible-by-sum-of-its-digits/)

给定一个整数 N，任务是检查这个数是否能被它的位数之和整除。如果可分，则打印“是”，否则打印“否”。

**示例:**

```
Input: N = 12 
Output: YES
Explanation: 
    As sum of digits of 12 = 1 + 2 = 3
    and 12 is divisible by 3 
    So the output is YES

Input: N = 123
Output: NO
```

**做法:**解决问题的思路是提取数字的位数并相加。然后检查这个数是否能被它的数字之和整除。如果是可分的，则打印是，否则打印否
以下是上述方法的实现:

**实施:**

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check
// if the given number is divisible
// by sum of its digits
string isDivisible(long long int n)
{
    long long int temp = n;

    // Find sum of digits
    int sum = 0;
    while (n) {
        int k = n % 10;
        sum += k;
        n /= 10;
    }

    // check if sum of digits divides n
    if (temp % sum == 0)
        return "YES";

    return "NO";
}

// Driver Code
int main()
{
    long long int n = 123;

    cout << isDivisible(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

    // Function to check if the
    // given number is divisible
    // by sum of its digits
    static String isDivisible(long n)
    {
        long temp = n;

        // Find sum of digits
        int sum = 0;
        while (n != 0)
        {
            int k = (int) n % 10;
            sum += k;
            n /= 10;
        }

        // check if sum of digits divides n
        if (temp % sum == 0)
            return "YES";

        return "NO";
    }

    // Driver Code
    public static void main(String []args)
    {
        long n = 123;
        System.out.println(isDivisible(n));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to check if the given number
# is divisible by sum of its digits
def isDivisible(n):

    temp = n

    # Find sum of digits
    sum = 0;
    while (n):

        k = n % 10;
        sum += k;
        n /= 10;

    # check if sum of digits divides n
    if (temp % sum == 0):
        return "YES";

    return "NO";

# Driver Code
n = 123;

print(isDivisible(n));

# This code is contributed by
# Akanksha Rai
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to check if the
    // given number is divisible
    // by sum of its digits
    static String isDivisible(long n)
    {
        long temp = n;

        // Find sum of digits
        int sum = 0;
        while (n != 0)
        {
            int k = (int) n % 10;
            sum += k;
            n /= 10;
        }

        // check if sum of digits divides n
        if (temp % sum == 0)
            return "YES";

        return "NO";
    }

    // Driver Code
    public static void Main()
    {
        long n = 123;
        Console.WriteLine(isDivisible(n));
    }
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check if the given number
// is divisible by sum of its digits
function isDivisible($n)
{
    $temp = $n;

    // Find sum of digits
    $sum = 0;
    while ($n)
    {
        $k = $n % 10;
        $sum += $k;
        $n = (int)($n / 10);
    }

    // check if sum of digits divides n
    if ($temp % $sum == 0)
        return "YES";

    return "NO";
}

// Driver Code
$n = 123;
print(isDivisible($n));

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to check if the given number
// is divisible by sum of its digits
function isDivisible(n)
{
    temp = n;

    // Find sum of digits
    sum = 0;

    while (n)
    {
        k = n % 10;
        sum += k;
        n = parseInt(n / 10);
    }

    // Check if sum of digits divides n
    if (temp % sum == 0)
        return "YES";

    return "NO";
}

// Driver Code
let n = 123;

document.write(isDivisible(n));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
NO
```

#### 方法 2:使用字符串:

*   通过接受一个新变量，将给定的数字转换为字符串。
*   遍历字符串，将每个元素转换为整数，并将其相加。
*   如果数字可被和整除，则打印“是”
*   否则打印否

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

string getResult(long long int n)
{

    // Converting integer to String
    string st = std::to_string(n);

    // Initialising sum to 0
    int sum = 0;

    // Traversing through the String
    for(char i : st)
    {

        // Converting character to int
        sum = sum + (int) i;
    }

    // Comparing number and sum
    if (n % sum == 0)
        return "Yes";
    else
        return "No";
}

// Driver Code
int main()
{
    int n = 123;

    // Passing this number to get result function
    cout << getResult(n);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG{

static String getResult(int n)
{

    // Converting integer to String
    String st = String.valueOf(n);

    // Initialising sum to 0
    int sum = 0;

    // Traversing through the String
    for(char i : st.toCharArray())
    {

        // Converting character to int
        sum = sum + (int) i;
    }

    // Comparing number and sum
    if (n % sum == 0)
        return "Yes";
    else
        return "No";
}

// Driver Code
public static void main(String[] args)
{
    int n = 123;

    // Passing this number to get result function
    System.out.println(getResult(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of above approach
def getResult(n):

    # Converting integer to string
    st = str(n)

    # Initialising sum to 0
    sum = 0
    length = len(st)

    # Traversing through the string
    for i in st:

        # Converting character to int
        sum = sum + int(i)

    # Comparing number and sum
    if (n % sum == 0):
        return "Yes"
    else:
        return "No"

# Driver Code
n = 123
# passing this number to get result function
print(getResult(n))

# this code is contributed by vikkycirus
```

## C#

```
// C# implementation of above approach
using System;
public class GFG{

static String getResult(int n)
{

    // Converting integer to String
    String st = String.Join("",n);

    // Initialising sum to 0
    int sum = 0;

    // Traversing through the String
    foreach(char i in st.ToCharArray())
    {

        // Converting character to int
        sum = sum + (int) i;
    }

    // Comparing number and sum
    if (n % sum == 0)
        return "Yes";
    else
        return "No";
}

// Driver Code
public static void Main(String[] args)
{
    int n = 123;

    // Passing this number to get result function
    Console.WriteLine(getResult(n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

function getResult(n)
{
    // Converting integer to String
    let st = (n).toString();

    // Initialising sum to 0
    let sum = 0;

    // Traversing through the String
    for(let i of st.split(""))
    {

        // Converting character to int
        sum = sum + parseInt(i);
    }

    // Comparing number and sum
    if (n % sum == 0)
        return "Yes";
    else
        return "No";
}

// Driver Code
let n = 123;

// Passing this number to get result function
document.write(getResult(n)+"<br>");

// This code is contributed by unknown2108

</script>
```

#### 输出:

```
No
```

#### 时间复杂度:0(N)