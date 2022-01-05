# 交换四个没有临时变量的变量

> 原文:[https://www . geesforgeks . org/swapping-四变量无临时变量/](https://www.geeksforgeeks.org/swapping-four-variables-without-temporary-variable/)

假设我们有四个变量 **a，b，c，d** ，我们希望以如下方式执行这些变量的**交换**
T5】a = b，b = c，c = d，d = a
而不使用任何其他**第五个或临时变量**

**解决方案:**
**第一步。**交换 **a** 和 **b** 而不使用任何其他变量
**a = a+b**
**b = a–b**
**a = a–b**

**第二步。**交换 **b** 和 **c** 而不使用任何其他变量
**b = b+c**
T10】c = b–c
T13】b = b–c

**第三步。**交换 **c** 和 **d** 而不使用任何其他变量
**c = c+d**
T10】d = c–d
T13】c = c–d

**示例:**

```
Input : a = 1, b = 2, c = 3, d = 4
Output :After swapping 
        a = 2, b = 3, c = 4, d = 1

Input :a = 6, b = 9, c = 10, d = 50
Output : After swapping : a = 9, b = 10, c = 50, d = 6
```

先决条件:[交换两个无临时变量的变量](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)，[交换三个无临时变量的变量](https://www.geeksforgeeks.org/swap-three-variables-without-using-temporary-variable/)

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to swap 4 variables without
// using temporary variable.
#include <bits/stdc++.h>
using namespace std;

void swap(int a, int b, int c, int d)
{
    // swapping a and b variables
    a = a + b;
    b = a - b;
    a = a - b;

    // swapping b and c variables
    b = b + c;
    c = b - c;
    b = b - c;

    // swapping c and d variables
    c = c + d;
    d = c - d;
    c = c - d;

    cout << "values after swapping are : " << endl;
    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
    cout << "c = " << c << endl;
    cout << "d = " << d << endl;
}

// Driver code
int main()
{
    // initialising variables
    int a = 1;
    int b = 2;
    int c = 3;
    int d = 4;

    cout << "Values before swapping are :" << endl;
    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
    cout << "c = " << c << endl;
    cout << "d = " << d << endl << endl;

    // Function call
    swap(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap 4 variables
// without using temporary variable.
class GFG {

    static void swap(int a, int b, int c, int d)
    {

        // swapping a and b variables
        a = a + b;
        b = a - b;
        a = a - b;

        // swapping b and c variables
        b = b + c;
        c = b - c;
        b = b - c;

        // swapping c and d variables
        c = c + d;
        d = c - d;
        c = c - d;

        System.out.println("values after "
                           + "swapping are : ");
        System.out.println("a = " + a);
        System.out.println("b = " + b);
        System.out.println("c = " + c);
        System.out.println("d = " + d);
    }

    // Driver code
    public static void main(String[] args)
    {

        // initialising variables
        int a = 1;
        int b = 2;
        int c = 3;
        int d = 4;

        System.out.println("values before "
                           + "swapping are : ");
        System.out.println("a = " + a);
        System.out.println("b = " + b);
        System.out.println("c = " + c);
        System.out.println("d = " + d);
        System.out.println("");

        // Function call
        swap(a, b, c, d);
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python 3 program to swap 4 variables
# without using temporary variable.

def swap(a, b, c, d):

    # swapping a and b variables
    a = a + b
    b = a - b
    a = a - b

    # swapping b and c variables
    b = b + c
    c = b - c
    b = b - c

    # swapping c and d variables
    c = c + d
    d = c - d
    c = c - d

    print("values after swapping are : ")
    print("a = ", a)
    print("b = ", b)
    print("c = ", c)
    print("d = ", d)

# Driver code

# initialising variables
a = 1
b = 2
c = 3
d = 4

print("values before swapping are : ")
print("a = ", a)
print("b = ", b)
print("c = ", c)
print("d = ", d)
print("")

# Function call
swap(a, b, c, d)

# This code is contributed by Smitha.
```

## C#

```
// C# program to swap 4 variables
// without using temporary variable.
using System;

class GFG {

    static void swap(int a, int b, int c, int d)
    {
        // swapping a and b variables
        a = a + b;
        b = a - b;
        a = a - b;

        // swapping b and c variables
        b = b + c;
        c = b - c;
        b = b - c;

        // swapping c and d variables
        c = c + d;
        d = c - d;
        c = c - d;

        Console.WriteLine("values after "
                          + "swapping are : ");
        Console.WriteLine("a = " + a);
        Console.WriteLine("b = " + b);
        Console.WriteLine("c = " + c);
        Console.WriteLine("d = " + d);
    }

    // Driver Code
    public static void Main()
    {

        // initialising variables
        int a = 1;
        int b = 2;
        int c = 3;
        int d = 4;

        Console.WriteLine("values before "
                          + "swapping are : ");
        Console.WriteLine("a = " + a);
        Console.WriteLine("b = " + b);
        Console.WriteLine("c = " + c);
        Console.WriteLine("d = " + d);
        Console.WriteLine("");

        // Function call
        swap(a, b, c, d);
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to swap 4 variables
// without using temporary variable

function swap($a, $b, $c, $d)
{

    // swapping a and b variables
    $a = $a + $b;
    $b = $a - $b;
    $a = $a - $b;

    // swapping b and c variables
    $b = $b + $c;
    $c = $b - $c;
    $b = $b - $c;

    // swapping c and d variables
    $c = $c + $d;
    $d = $c - $d;
    $c = $c - $d;

    echo "values after swapping are : ","\n";
    echo "a = " , $a ,"\n";
    echo "b = " , $b ,"\n";
    echo "c = " ,$c ,"\n";
    echo "d = " , $d ,"\n";
}

    // Driver Code
    // initialising variables
    $a = 1;
    $b = 2;
    $c = 3;
    $d = 4;

    echo "Values before swapping are :" ,"\n";
    echo "a = " , $a ,"\n";
    echo "b = " ,$b,"\n";
    echo "c = " , $c ,"\n";
    echo "d = " , $d ,"\n","\n";

    // Function call
    swap($a, $b, $c, $d);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript program to swap 4 variables
    // without using temporary variable.

    function swap(a, b, c, d)
    {
        // swapping a and b variables
        a = a + b;
        b = a - b;
        a = a - b;

        // swapping b and c variables
        b = b + c;
        c = b - c;
        b = b - c;

        // swapping c and d variables
        c = c + d;
        d = c - d;
        c = c - d;

        document.write("values after swapping are : " + "</br>");
        document.write("a = " + a + "</br>");
        document.write("b = " + b + "</br>");
        document.write("c = " + c + "</br>");
        document.write("d = " + d);
    }

    // initialising variables
    let a = 1;
    let b = 2;
    let c = 3;
    let d = 4;

    document.write("values before swapping are : " + "</br>");
    document.write("a = " + a + "</br>");
    document.write("b = " + b + "</br>");
    document.write("c = " + c + "</br>");
    document.write("d = " + d + "</br>");
    document.write("" + "</br>");

    // Function call
    swap(a, b, c, d);

</script>
```

**Output**

```
Values before swapping are :
a = 1
b = 2
c = 3
d = 4

values after swapping are : 
a = 2
b = 3
c = 4
d = 1
```