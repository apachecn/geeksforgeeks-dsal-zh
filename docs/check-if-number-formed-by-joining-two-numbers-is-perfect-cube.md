# 检查两个数字连接形成的数字是否为完美立方体

> 原文:[https://www . geesforgeks . org/check-if-number-formed-by-join-two-numbers-is-perfect-cube/](https://www.geeksforgeeks.org/check-if-number-formed-by-joining-two-numbers-is-perfect-cube/)

给定两个数字 **a** 和 **b** ，任务是检查 **a** 和 **b** 的拼接是否为[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。
**示例:**

> **输入:** a = 6，b = 4
> **输出:**是
> 连接 6 和 4 = 64。因为 64 (= 4 x 4 x 4)是一个完美的立方体，所以输出是 Yes。
> **输入:** a = 100，b = 1
> **输出:**否
> 串联 100 和 1 = 1001。因为 1001 不是一个完美的立方体，所以输出是 No。

**方法:**由于[追加字符串](https://www.geeksforgeeks.org/methods-to-concatenate-string-in-c-c-with-examples/)比追加数字相对容易，解决这个问题最简单的方法就是[将给定的整数转换成字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)。一旦获得连接的数字，就可以很容易地[检查它是否是一个完美的立方体](https://www.geeksforgeeks.org/perfect-cube/)。
以下是上述办法的实施情况。

## C++

```
// C++ program to check if the
// concatenation of two numbers
// is a perfect cube or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is
// a perfect Cube or not
bool isPerfectCube(int x)
{
    long double cr = round(cbrt(x));

    return (cr * cr * cr == x);
}

// Function to check if
// concatenation of two numbers
// is a perfect cube or not
void checkCube(int a, int b)
{

    // Convert numbers to string
    // using to_string()
    string s1 = to_string(a);
    string s2 = to_string(b);

    // Concatenate the numbers and
    // convert it into integer
    int c = stoi(s1 + s2);

    // Check if concatenated value
    // is perfect cube or not
    if (isPerfectCube(c)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int a = 6;
    int b = 4;

    checkCube(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the
// concatenation of two numbers
// is a perfect cube or not
class GFG {

    // Function to check if a number is
    // a perfect Cube or not
    static boolean isPerfectCube(int x)
    {
        long cr = Math.round(Math.cbrt(x));

        return (cr * cr * cr == x);
    }

    // Function to check if
    // concatenation of two numbers
    // is a perfect cube or not
    static void checkCube(int a, int b)
    {

        // Convert numbers to string
        // using to_string()
        String s1 = Integer.toString(a);
        String s2 = Integer.toString(b);

        // Concatenate the numbers and
        // convert it into integer
        int c = Integer.parseInt(s1 + s2);

        // Check if concatenated value
        // is perfect cube or not
        if (isPerfectCube(c)) {
                System.out.println("Yes");
        }
        else {
                System.out.println("No");
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int a = 6;
        int b = 4;

        checkCube(a, b);  
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python 3 program to check if the
# concatenation of two numbers
# is a perfect cube or not

# Function to check if a number is
# a perfect Cube or not
def isPerfectCube(x):
    x = abs(x)
    return int(round(x ** (1\. / 3))) ** 3 == x

# Function to check if
# concatenation of two numbers
# is a perfect cube or not
def checkCube(a, b):

    # Convert numbers to string
    # using to_string()
    s1 = str(a)
    s2 = str(b)

    # Concatenate the numbers and
    # convert it into integer
    c = int(s1 + s2)

    # Check if concatenated value
    # is perfect cube or not
    if (isPerfectCube(c)):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    a = 6
    b = 4

    checkCube(a, b)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to check if the
// concatenation of two numbers
// is a perfect cube or not
using System;

class GFG {

    // Function to check if a number is
    // a perfect Cube or not
    static bool isPerfectCube(int x)
    {
        double cr = Math.Round(Math.Cbrt(x));

        return (cr * cr * cr == x);
    }

    // Function to check if
    // concatenation of two numbers
    // is a perfect cube or not
    static void checkCube(int a, int b)
    {

        // Convert numbers to string
        // using to_string()
        string s1 = Convert.ToString(a);
        string s2 = Convert.ToString(b);

        // Concatenate the numbers and
        // convert it into integer
        int c = Convert.ToInt32(s1 + s2);

        // Check if concatenated value
        // is perfect cube or not
        if (isPerfectCube(c)) {
                Console.WriteLine("Yes");
        }
        else {
                Console.WriteLine("No");
        }
    }

    // Driver Code
    public static void Main ()
    {
        int a = 6;
        int b = 4;

        checkCube(a, b);
    }
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// JavaScript program to check if the
// concatenation of two numbers
// is a perfect cube or not

// Function to check if a number is
// a perfect Cube or not
function isPerfectCube(x)
{
    var cr = Math.round(Math.cbrt(x));

    return (cr * cr * cr == x);
}

// Function to check if
// concatenation of two numbers
// is a perfect cube or not
function checkCube(a , b)
{

    // Convert numbers to string
    // using to_string()
    s1 = a.toString();
    s2 = b.toString();

    // Concatenate the numbers and
    // convert it into integer
    var c = parseInt(s1 + s2);

    // Check if concatenated value
    // is perfect cube or not
    if (isPerfectCube(c)) {
            document.write("Yes");
    }
    else {
            document.write("No");
    }
}

// Driver Code
var a = 6;
var b = 4;

checkCube(a, b); 

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(cbrt(concate(a，b)))*

***辅助空间:** O(1)*