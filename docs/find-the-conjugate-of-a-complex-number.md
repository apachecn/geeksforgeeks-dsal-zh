# 求复数的共轭

> 原文:[https://www . geeksforgeeks . org/find-复数共轭/](https://www.geeksforgeeks.org/find-the-conjugate-of-a-complex-number/)

给定一个字符串形式的复数 **str** ，任务是确定这个[复数](https://www.geeksforgeeks.org/complex-numbers-in-python-set-1-introduction/)的共轭。
**例:**

```
Input: str = "3 - 4i"
Output: 3 + 4i

Input: str = "6 - 5i"
Output: 6 + 5i
```

**方法:**如果只有一个复数的虚部符号不同，则称该复数为另一个复数的共轭。

```
If complex number = x + iy

Conjugate of this complex number = x - iy
```

**以下是上述方法的实现:**

## C++

```
// C++ implementation to Find the
// conjugate of a complex number
#include <bits/stdc++.h>
using namespace std;

// Function to find conjugate
// of a complex number
void solve(string s)
{
    string z = s;
    int l = s.length();
    int i;

    if (s.find('+') < l) {

        // store index of '+'
        i = s.find('+');

        replace(s.begin(),
                s.end(),
                '+', '-');
    }
    else {

        // store index of '-'
        i = s.find('-');

        replace(s.begin(),
                s.end(),
                '-', '+');
    }

    // print the result
    cout << "Conjugate of "
         << z << " = "
         << s << endl;
}

// Driver code
int main()
{

    // initialise the complex number
    string s = "3-4i";

    solve(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find the
// conjugate of a complex number

class GFG
{
    // Function to find conjugate
    // of a complex number
    static void solve(String s)
    {
        String z = s;
        int l = s.length();
        int i;
        String str;

        if (s.indexOf('+') != -1) {

            // store index of '+'
            i = s.indexOf('+');

            str = s.replace('+', '-');
        }
        else {

            // store index of '-'
            i = s.indexOf('-');

            str = s.replace('-', '+');
        }

        // print the result
        System.out.println("Conjugate of "
             + z + " = "
             + str);
    }

    // Driver code
    public static void main(String []args)
    {

        // initialise the complex number
        String s = "3-4i";

        solve(s);
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to Find the
# conjugate of a complex number

# Function to find conjugate
# of a complex number
def solve(s):
    z = s
    l = len(s)
    i = 0
    if (s.find('+') != -1):

        # store index of '+'
        i = s.find('+')

        s = s.replace('+', '-')
    else:
        # store index of '-'
        i = s.find('-')

        s = s.replace('-', '+',1)

    # print the result
    print("Conjugate of ",z," = ",s)

# Driver code

# initialise the complex number
s = "3-4i"
solve(s)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to find the
// conjugate of a complex number
using System;

class GFG{

// Function to find conjugate
// of a complex number
static void solve(String s)
{
    String z = s;
    int l = s.Length;
    int i;
    String str;

    if (s.IndexOf('+') != -1)
    {

        // Store index of '+'
        i = s.IndexOf('+');

        str = s.Replace('+', '-');
    }
    else
    {

        // Store index of '-'
        i = s.IndexOf('-');

        str = s.Replace('-', '+');
    }

    // print the result
    Console.WriteLine("Conjugate of "+ z +
                      " = " + str);
}

// Driver code
public static void Main(String []args)
{

    // Initialise the complex number
    String s = "3-4i";

    solve(s);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to find conjugate
// of a complex number
function solve(s)
{
    let z = s;
    var l = s.length;
    var i;

    if (s.indexOf('+') != -1) {

        // store index of '+'
        i = s.indexOf('+');

        s = s.replace('+', '-');
    }
    else {

        // store index of '-'
        i = s.indexOf('-');

        s = s.replace('-', '+');
    }

    // print the result
    document.write("Conjugate of "+z+" = "+s+"<br>");
}

// Driver Code
// Array of points
let s = "3-4i";
solve(s);
</script>
```

**Output:** 

```
Conjugate of 3-4i = 3+4i
```

时间复杂度:O(|s|)

辅助空间:0(1)