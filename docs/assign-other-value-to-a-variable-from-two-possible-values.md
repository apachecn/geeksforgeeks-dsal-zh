# 从两个可能的值中为变量指定另一个值

> 原文:[https://www . geeksforgeeks . org/将其他值赋给两个可能值中的一个变量/](https://www.geeksforgeeks.org/assign-other-value-to-a-variable-from-two-possible-values/)

假设一个变量 x 只能有两个可能的值 a 和 b，并且您希望将当前值以外的值赋给 x。在不使用任何条件运算符的情况下高效地执行。
注意:我们不允许检查 x 的当前值。
**示例:**

> 输入:a = 10，b = 15，x = a
> 输出:x = 15
> 解释 x = 10，目前 x 有 a 的值(也就是 10)，我们需要改成 15。
> 输入:a = 9，b = 11，x = b
> 输出:x = 9

我们可以用 if 条件来解决这个问题，但是我们不能这么做。

```
if (x == a) 
   x = b;
else x = a;
```

我们可以使用三元运算符，它也检查 x 的当前值，并在此基础上分配新值。所以我们也不能使用这种方法

```
x = x == a ? b : a;
```

但是，我们不允许检查 x 的值，所以上述解决方案都不起作用。
**解决方案 1:** 仅使用算术运算符，我们可以执行此操作

```
x = a + b - x
```

这样，x 的内容将在每次执行时在 a 和 b 之间交替

## C++

```
// CPP program to change value of x
// according to its current value.
#include <bits/stdc++.h>
using namespace std;

// Function to alternate the values
void alternate(int& a, int& b, int& x)
{
    x = a + b - x;
}

// Main function
int main()
{
    int a = -10;
    int b = 15;
    int x = a;
    cout << "x is : " << x;

    alternate(a, b, x);

    cout << "\nAfter change ";
    cout << "\nx is : " << x;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change value of x
// according to its current value.
import java.util.*;

class solution
{

// Function to alternate the values
static void alternate(int a, int b, int x)
{
    x = a + b - x;
    System.out.println("After change"+"\n"+" x is : "+x);
}

// Main function
public static void main(String args[])
{
    int a = -10;
    int b = 15;
    int x = a;
    System.out.println("x is : "+x);
    alternate(a, b, x);
}
}
```

## 蟒蛇 3

```
# Python3 program to change value
# of x according to its current value.

# Function to alternate the values
def alternate(a,b,x):
    x = a+b-x
    print("After change x is:",x)

# Driver code
if __name__=='__main__':
    a = -10
    b = 15
    x = a
    print("x is:",x)
    alternate(a,b,x)

# This code is contributed by
# Shrikant13
```

## C#

```
// C# program to change value of x
// according to its current value.

using System;
class gfg
{
 // Function to alternate the values
 public void alternate(ref int a, ref int b, ref int x)
   //'ref' indicates the references
 {
    x = a + b - x;
 }
}

// Main function
class geek
{
 public static int Main()
 {
    gfg g = new gfg();
    int a = -10;
    int b = 15;
    int x = a;
    Console.WriteLine("x is : {0}" , x);

    g.alternate(ref a, ref b, ref x);

    Console.WriteLine ("After change ");
    Console.WriteLine("x is : {0}", x);
    return 0;
 }
}
//This code is contributed by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to change value of x
// according to its current value.

// Function to alternate the values
function alternate (&$a, &$b, &$x)
{
    $x = $a + $b - $x;
}

// Driver Code
$a = -10;
$b = 15;
$x = $a;
echo "x is : ", $x;

alternate($a, $b, $x);

echo "\nAfter change ";
echo "\nx is : ", $x;

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to change value of x
// according to its current value.

    // Function to alternate the values
    function alternate(a , b , x) {
        x = a + b - x;
        document.write("After change" + "<br/>" + " x is : " + x);
    }

    // Main function

        var a = -10;
        var b = 15;
        var x = a;
        document.write("x is : " + x+"<br/>");
        alternate(a, b, x);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
x is : -10
After change 
x is : 15
```

**时间复杂度:**该方法的时间复杂度为 O(1)
**空间复杂度:**该方法的空间复杂度为 O(1)
**解决方案 2:** 一种更好更有效的方法是使用按位异或运算。
x = a^b^x

## C++

```
// CPP program to change value of x
// according to its current value.
#include <bits/stdc++.h>
using namespace std;

// Function to alternate the values
void alternate(int& a, int& b, int& x)
{
    x = a ^ b ^ x;
}

// Main function
int main()
{
    int a = -10;
    int b = 15;
    int x = a;
    cout << "x is : " << x;

    alternate(a, b, x);

    cout << "\nAfter exchange ";
    cout << "\nx is : " << x;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change value of x
// according to its current value.

class GFG {
// Function to alternate the values

    static int alternate(int a, int b, int x) {
        return x = a ^ b ^ x;
    }

// Main function
    public static void main(String[] args) {
        int a = -10;
        int b = 15;
        int x = a;
        System.out.print("x is : " + x);

        x = alternate(a, b, x);

        System.out.print("\nAfter exchange ");
        System.out.print("\nx is : " + x);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to change value of x
# according to its current value.

# Function to alternate the values
def alternate(a, b, x):
    x = a ^ b ^ x
    print("After exchange")
    print("x is", x)

# Driver code
a = -10
b = 15
x = a
print("x is", x)
alternate(a, b, x)

# This code is contributed
# by Shrikant13
```

## C#

```

// C# program to change value of x
// according to its current value.
using System;
public class GFG {
// Function to alternate the values

    static int alternate(int a, int b, int x) {
        return x = a ^ b ^ x;
    }

// Main function
    public static void Main() {
        int a = -10;
        int b = 15;
        int x = a;
        Console.Write("x is : " + x);

        x = alternate(a, b, x);

        Console.Write("\nAfter exchange ");
        Console.Write("\nx is : " + x);

    }
}
/*This code is contributed by Rajput-Ji*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to change value of x
// according to its current value.

// Function to alternate the values
function alternate(&$a, &$b, &$x)
{
    $x = $a ^ $b ^ $x;
}

// Driver Code
$a = -10;
$b = 15;
$x = $a;
echo "x is : ", $x;

alternate($a, $b, $x);

echo "\nAfter exchange ";
echo "\nx is : ", $x;

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to change value of x
// according to its current value.

// Function to alternate the values

    function alternate(a , b , x) {
        return x = a ^ b ^ x;
    }

    // Main function

        var a = -10;
        var b = 15;
        var x = a;
        document.write("x is : " + x);

        x = alternate(a, b, x);

        document.write("<br/>After exchange ");
        document.write("<br/>x is : " + x);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
x is : -10
After exchange 
x is : 15
```

**时间复杂度:**该方法的时间复杂度为 O(1)
T3】空间复杂度:该方法的空间复杂度为 O(1)