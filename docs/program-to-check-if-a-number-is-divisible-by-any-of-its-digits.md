# 检查一个数字是否能被它的任何一个数字整除的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果一个数字可以被它的任何一个数字整除/](https://www.geeksforgeeks.org/program-to-check-if-a-number-is-divisible-by-any-of-its-digits/)

给定一个整数 **N** 其中![1 \leq n \leq 10^{18}              ](img/42f92184a7549ae9e4bbc1b8d1195a62.png "Rendered by QuickLaTeX.com")。任务是检查这个数是否不能被它的任何一个数字整除。如果给定的数字 N 可以被它的任何一个数字整除，则打印“是”，否则打印“否”。

**示例:**

```
Input : N = 5115
Output : YES
Explanation: 5115 is divisible by both 1 and 5.
So print YES.

Input : 27
Output : NO
Explanation: 27 is not divisible by 2 or 7
```

**方法:**解决问题的思路是把数字的位数一个一个地提取出来，检查这个数字是否能被它的任意一个位数整除。如果它能被它的任何一个数字整除，则打印“是”，否则打印“否”

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if given number is divisible
// by any of its digits
string isDivisible(long long int n)
{
    long long int temp = n;

    // check if any of digit divides n
    while (n) {
        int k = n % 10;

        // check if K divides N
        if (temp % k == 0)
            return "YES";

        n /= 10;
    }

    return "NO";
}

// Driver Code
int main()
{
    long long int n = 9876543;

    cout << isDivisible(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG
{

    // Function to check if given number is divisible
    // by any of its digits
    static String isDivisible(int n)
    {
        int temp = n;

        // check if any of digit divides n
        while (n > 0)
        {
            int k = n % 10;

            // check if K divides N
            if (temp % k == 0)
            {
                return "YES";
            }
            n /= 10;
        }

        return "NO";
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 9876543;
        System.out.println(isDivisible(n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program implementation of above approach

# Function to check if given number is
# divisible by any of its digits
def isDivisible(n):
    temp = n

    # check if any of digit divides n
    while(n):
        k = n % 10

        # check if K divides N
        if(temp % k == 0):
            return "YES"

        n /= 10;

    # Number is not divisible by
    # any of digits
    return "NO"

# Driver Code
n = 9876543
print(isDivisible(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to check if given number is divisible
    // by any of its digits
    static String isDivisible(int n)
    {
        int temp = n;

        // check if any of digit divides n
        while (n > 0)
        {
            int k = n % 10;

            // check if K divides N
            if (temp % k == 0)
            {
                return "YES";
            }
            n /= 10;
        }

        return "NO";
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 9876543;
        Console.WriteLine(isDivisible(n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check if given number
// is divisible by any of its digits
function isDivisible($n)
{
    $temp = $n;

    // check if any of digit divides n
    while ($n)
    {
        $k = $n % 10;

        // check if K divides N
        if ($temp % $k == 0)
            return "YES";

        $n = floor($n / 10);
    }

    return "NO";
}

// Driver Code
$n = 9876543;

echo isDivisible($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to check if given number
// is divisible by any of its digits
function isDivisible(n)
{
    temp = n;

    // Check if any of digit divides n
    while (n)
    {
        k = n % 10;

        // Check if K divides N
        if (temp % k == 0)
            return "YES";

        n = Math.floor(n / 10);
    }

    return "NO";
}

// Driver Code
let n = 9876543;

document.write(isDivisible(n));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
YES
```

**时间复杂度** : O(log(N))
**辅助空间** : O(1)

#### 方法 2:使用字符串:

*   我们必须通过取一个新的变量把给定的数字转换成字符串。
*   穿过绳子，
*   将字符转换为整数(数字)
*   检查该数字是否能被其任何数字整除，然后打印“是”，否则打印“否”

下面是上述方法的实现:

## C++

```
//C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

string getResult(int n)
 {

    // Converting integer to string
    string st = to_string(n);

    // Traversing the string
    for (int i = 0; i < st.length(); i++)
    {

        //find the actual digit
        int d = st[i] - 48;

      // If the number is divisible by
        // digits then return yes
        if(n % d == 0)
        {

            return "Yes";
        }
    }

    // If no digits are dividing the
    // number then return no
    return "No";
}

// Driver Code
int main()
{
int n = 9876543;

// passing this number to get result function
cout<<getResult(n);

}

// this code is contributed by SoumiikMondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAva implementation of above approach
import java.io.*;

class GFG{
static String getResult(int n)
 {

    // Converting integer to string
    String st = Integer.toString(n);

    // Traversing the string
    for (int i = 0; i < st.length(); i++)
    {

        //find the actual digit
        int d = st.charAt(i) - 48;

      // If the number is divisible by
        // digits then return yes
        if(n % d == 0)
        {

            return "Yes";
        }
    }

    // If no digits are dividing the
    // number then return no
    return "No";
}

// Driver Code
public static void main(String[] args)
    {
int n = 9876543;

// passing this number to get result function
System.out.println(getResult(n));
}
}

// this code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python implementation of above approach
def getResult(n):

    # Converting integer to string
    st = str(n)

    # Traversing the string
    for i in st:

        # If the number is divisible by
        # digits then return yes
        if(n % int(i) == 0):
            return 'Yes'

    # If no digits are dividing the
    # number then return no
    return 'No'

# Driver Code
n = 9876543

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

    // Converting integer to string
    string st = n.ToString();

    // Traversing the string
    for (int i = 0; i < st.Length; i++)
    {

        //find the actual digit
        int d = st[i] - 48;

      // If the number is divisible by
        // digits then return yes
        if(n % d == 0)
        {

            return "Yes";
        }
    }

    // If no digits are dividing the
    // number then return no
    return "No";
}

// Driver Code
public static void Main(String[] args)
{
   int n = 9876543;

   // passing this number to get result function
   Console.Write(getResult(n));
}
}

// this code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

function getResult(n)
{
    // Converting integer to string
    let st = n.toString();

    // Traversing the string
    for (let i = 0; i < st.length; i++)
    {

        //find the actual digit
        let d = st[i].charCodeAt(0) - 48;

      // If the number is divisible by
        // digits then return yes
        if(n % d == 0)
        {

            return "Yes";
        }
    }

    // If no digits are dividing the
    // number then return no
    return "No";
}

// Driver Code
let n = 9876543;

// passing this number to get result function
document.write(getResult(n));

// This code is contributed by unknown2108

</script>
```

#### 输出:

```
Yes
```