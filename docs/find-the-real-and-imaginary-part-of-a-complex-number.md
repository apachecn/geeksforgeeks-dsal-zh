# 求复数的实部和虚部

> 原文:[https://www . geesforgeks . org/find-复数的实部和虚部/](https://www.geeksforgeeks.org/find-the-real-and-imaginary-part-of-a-complex-number/)

给定一个复数 **Z** ，任务是确定这个复数的实部和虚部。
**例:**

> **输入:** z = 3 + 4i
> **输出:**实部:3，虚部:4
> **输入:**z = 6–8i
> **输出:**实部:6，虚部:8

**逼近:**一个复数可以表示为 **Z = x + yi** ，其中 **x** 为实部， **y** 为虚部。
我们将按照以下步骤分离出实部和虚部

1.  找出字符串中 **+** 或**–**运算符的索引
2.  实部将是从索引 **0** 到长度**(运算符的索引–1)**的子串
3.  虚部将是从索引**(运算符+ 1 的索引)**到**(字符串长度–运算符的索引–2)**的子字符串

**执行:**

## C++

```
// C++ program to find the real and
// imaginary parts of a Complex Number
#include <bits/stdc++.h>
using namespace std;

// Function to find real and imaginary
// parts of a complex number
void findRealAndImag(string s)
{
    // string length stored in variable l
    int l = s.length();

    // variable for the index of the separator
    int i;

    // Storing the index of '+'
    if (s.find('+') < l) {
        i = s.find('+');
    }
    // else storing the index of '-'
    else {
        i = s.find('-');
    }

    // Finding the real part
    // of the complex number
    string real = s.substr(0, i);

    // Finding the imaginary part
    // of the complex number
    string imaginary = s.substr(i + 1, l - i - 2);

    cout << "Real part: " << real << "\n";
    cout << "Imaginary part: "
         << imaginary << "\n";
}

// Driver code
int main()
{
    string s = "3+4i";

    findRealAndImag(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the real and
// imaginary parts of a Complex Number
class GFG
{
    // Function to find real and imaginary
    // parts of a complex number
    static void findRealAndImag(String s)
    {
        // string length stored in variable l
        int l = s.length();

        // variable for the index of the separator
        int i;

        // Storing the index of '+'
        if (s.indexOf('+') != -1) {
            i = s.indexOf('+');
        }

        // else storing the index of '-'
        else {
            i = s.indexOf('-');
        }

        // Finding the real part
        // of the complex number
        String real = s.substring(0, i);

        // Finding the imaginary part
        // of the complex number
        String imaginary = s.substring(i + 1, l - 1);

        System.out.println("Real part: " + real );
        System.out.println("Imaginary part: "+
              imaginary);
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "3+4i";

        findRealAndImag(s);

    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to find the real and
# imaginary parts of a Complex Number

# Function to find real and imaginary
# parts of a complex number
def findRealAndImag(s) :

    # string length stored in variable l
    l = len(s)

    # variable for the index of the separator
    i = 0

    # Storing the index of '+'
    if (s.find('+') != -1):
        i = s.find('+')
    # else storing the index of '-'
    else:
        i = s.find('-');

    # Finding the real part
    # of the complex number
    real = s[:i]

    # Finding the imaginary part
    # of the complex number
    imaginary = s[i + 1:l  - 1]

    print("Real part:", real)
    print("Imaginary part:", imaginary)

# Driver code
s = "3+4i";

findRealAndImag(s);

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find the real and
// imaginary parts of a Complex Number
using System;

class GFG
{
    // Function to find real and imaginary
    // parts of a complex number
    static void findRealAndImag(String s)
    {
        // string length stored in variable l
        int l = s.Length;

        // variable for the index of the separator
        int i;

        // Storing the index of '+'
        if (s.IndexOf('+') != -1) {
            i = s.IndexOf('+');
        }

        // else storing the index of '-'
        else {
            i = s.IndexOf('-');
        }

        // Finding the real part
        // of the complex number
        String real = s.Substring(0, i);

        // Finding the imaginary part
        // of the complex number
        String imaginary = s.Substring(i + 1, l - i - 2);

        Console.WriteLine("Real part: " + real );
        Console.WriteLine("Imaginary part: "+
              imaginary);
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "3+4i";

        findRealAndImag(s);

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the real and
// imaginary parts of a Complex Number

    // Function to find real and imaginary
    // parts of a complex number
    function findRealAndImag(s)
    {
        // string length stored in variable l
        let l = s.length - 1;

        // variable for the index of the separator
        let i;

        // Storing the index of '+'
        if (s.indexOf('+') != -1) {
            i = s.indexOf('+');
        }

        // else storing the index of '-'
        else {
            i = s.indexOf('-');
        }

        // Finding the real part
        // of the complex number
        let real = s.substr(0, i);

        // Finding the imaginary part
        // of the complex number
        let imaginary = s.substr(i + 1, l - 2 );

        document.write("Real part: " + real +"<br/>" );
        document.write("Imaginary part: "+
              imaginary);
    }

// Driver code

    let s = "3+4i";

    findRealAndImag(s);

</script>
```

**Output:** 

```
Real part: 3
Imaginary part: 4
```

**性能分析** s:

*   **时间复杂度**:在上面的方法中，由于不管字符串的长度如何，我们都在进行恒定数量的操作，因此时间复杂度为 **O(1)**
*   **辅助空间复杂度**:在上面的方法中，除了几个变量之外，我们没有使用任何额外的空间。所以辅助空间的复杂度是 **O(1)**