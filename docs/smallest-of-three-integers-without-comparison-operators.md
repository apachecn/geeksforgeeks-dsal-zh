# 无比较运算符的三个整数中最小的

> 原文:[https://www . geeksforgeeks . org/不带比较运算符的三个整数中的最小值/](https://www.geeksforgeeks.org/smallest-of-three-integers-without-comparison-operators/)

编写一个程序，在不使用任何比较运算符的情况下，找出三个整数中最小的一个。
让 3 个输入数字为 x，y，z.
**方法 1(重复减法)**
取一个计数器变量 c，用 0 初始化。在一个循环中，反复用 1 减去 x、y 和 z，然后增加 c。先变成 0 的数是最小的。循环结束后，c 将保持最小值 3。

## C++

```
// C++ program to find Smallest
// of three integers without
// comparison operators
#include <bits/stdc++.h>
using namespace std;
int smallest(int x, int y, int z)
{
    int c = 0;
    while (x && y && z) {
        x--;
        y--;
        z--;
        c++;
    }
    return c;
}

// Driver Code
int main()
{
    int x = 12, y = 15, z = 5;
    cout << "Minimum of 3 numbers is "
         << smallest(x, y, z);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to find Smallest
// of three integers without
// comparison operators
#include <stdio.h>

int smallest(int x, int y, int z)
{
    int c = 0;
    while (x && y && z) {
        x--;
        y--;
        z--;
        c++;
    }
    return c;
}

int main()
{
    int x = 12, y = 15, z = 5;
    printf("Minimum of 3 numbers is %d", smallest(x, y, z));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Smallest
// of three integers without
// comparison operators
class GFG {

    static int smallest(int x, int y, int z)
    {
        int c = 0;

        while (x != 0 && y != 0 && z != 0) {
            x--;
            y--;
            z--;
            c++;
        }

        return c;
    }

    public static void main(String[] args)
    {
        int x = 12, y = 15, z = 5;

        System.out.printf("Minimum of 3"
                              + " numbers is %d",
                          smallest(x, y, z));
    }
}

// This code is contributed by  Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python3 program to find Smallest
# of three integers without
# comparison operators

def smallest(x, y, z):
    c = 0

    while ( x and y and z ):
        x = x-1
        y = y-1
        z = z-1
        c = c + 1

    return c

# Driver Code
x = 12
y = 15
z = 5
print("Minimum of 3 numbers is",
       smallest(x, y, z))

# This code is contributed by Anshika Goyal
```

## C#

```
// C# program to find Smallest of three
// integers without comparison operators
using System;

class GFG {
    static int smallest(int x, int y, int z)
    {
        int c = 0;

        while (x != 0 && y != 0 && z != 0) {
            x--;
            y--;
            z--;
            c++;
        }

        return c;
    }

    // Driver Code
    public static void Main()
    {
        int x = 12, y = 15, z = 5;

        Console.Write("Minimum of 3"
                      + " numbers is " + smallest(x, y, z));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find Smallest
// of three integers without
// comparison operators
function smallest($x, $y, $z)
{
    $c = 0;
    while ( $x && $y && $z )
    {
        $x--; $y--; $z--; $c++;
    }

    return $c;
}

// Driver code
$x = 12;
$y = 15;
$z = 5;
echo "Minimum of 3 numbers is ".
             smallest($x, $y, $z);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript program to find Smallest
// of three integers without
// comparison operators

function smallest(x, y, z)
{
    let c = 0;
    while (x && y && z) {
        x--;
        y--;
        z--;
        c++;
    }
    return c;
}

// Driver Code

let x = 12, y = 15, z = 5;
document.write("Minimum of 3 numbers is "
    + smallest(x, y, z));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
Minimum of 3 numbers is 5
```

这种方法不适用于负数。方法 2 也适用于负数。
**方法二(使用比特运算)**
使用[这个帖子的方法二求两个数的最小值](https://www.geeksforgeeks.org/compute-the-minimum-or-maximum-max-of-two-integers-without-branching/)(我们不能使用方法一，因为方法一使用比较运算符)。一旦我们有了找到最少 2 个数字的功能，我们就可以用它来找到最少 3 个数字。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define CHAR_BIT 8

/*Function to find minimum of x and y*/
int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >> (sizeof(int) * CHAR_BIT - 1)));
}

/* Function to find minimum of 3 numbers x, y and z*/
int smallest(int x, int y, int z)
{
    return min(x, min(y, z));
}

// Driver code
int main()
{
    int x = 12, y = 15, z = 5;
    cout << "Minimum of 3 numbers is "  << smallest(x, y, z);
    return 0;
}

// This code is contributed by Code_Mech.
```

## C

```
// C implementation of above approach
#include <stdio.h>
#define CHAR_BIT 8

/*Function to find minimum of x and y*/
int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >> (sizeof(int) * CHAR_BIT - 1)));
}

/* Function to find minimum of 3 numbers x, y and z*/
int smallest(int x, int y, int z)
{
    return min(x, min(y, z));
}

int main()
{
    int x = 12, y = 15, z = 5;
    printf("Minimum of 3 numbers is %d", smallest(x, y, z));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

static int CHAR_BIT = 8;

// Function to find minimum of x and y
static int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >>
               ((Integer.SIZE/8) * CHAR_BIT - 1)));
}

// Function to find minimum of 3 numbers x, y and z
static int smallest(int x, int y, int z)
{
    return Math.min(x, Math.min(y, z));
}

// Driver code
public static void main (String[] args)
{
    int x = 12, y = 15, z = 5;
    System.out.println("Minimum of 3 numbers is " +
                                smallest(x, y, z));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of above approach
CHAR_BIT = 8

# Function to find minimum of x and y
def min(x, y):
    return y + ((x - y) & \
               ((x - y) >> (32 * CHAR_BIT - 1)))

# Function to find minimum
# of 3 numbers x, y and z
def smallest(x, y, z):
    return min(x, min(y, z))

# Driver code
x = 12
y = 15
z = 5
print("Minimum of 3 numbers is ",
               smallest(x, y, z))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

static int CHAR_BIT=8;

/*Function to find minimum of x and y*/
static int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >> (sizeof(int) * CHAR_BIT - 1)));
}

/* Function to find minimum of 3 numbers x, y and z*/
static int smallest(int x, int y, int z)
{
    return Math.Min(x, Math.Min(y, z));
}

// Driver code
static void Main()
{
    int x = 12, y = 15, z = 5;
    Console.WriteLine("Minimum of 3 numbers is "+smallest(x, y, z));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

    let CHAR_BIT = 8;
    // Function to find minimum of x and y
    function min(x,y)
    {
        return y + ((x - y) & ((x - y) >> (32 * CHAR_BIT - 1)))
    }
    // Function to find minimum of 3 numbers x, y and z
    function smallest(x,y,z)
    {
         return Math.min(x, Math.min(y, z));
    }

    // Driver code
    let  x = 12, y = 15, z = 5;

    document.write("Minimum of 3 numbers is " +
                                smallest(x, y, z));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Minimum of 3 numbers is 5
```

**方法 3(使用除法运算符)**
我们也可以使用除法运算符来寻找两个数字的最小值。如果(a/b)的值为零，则 b 大于 a，否则 a 大于 a。感谢 [gopinath](https://www.geeksforgeeks.org/smallest-of-three-integers-without-comparison-operators/#comment-15324) 和 [Vignesh](http://in.linkedin.com/in/vignesh4430) 提出这个方法。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Using division operator to find
// minimum of three numbers
int smallest(int x, int y, int z)
{
    if (!(y / x)) // Same as "if (y < x)"
        return (!(y / z)) ? y : z;
    return (!(x / z)) ? x : z;
}

int main()
{
    int x = 78, y = 88, z = 68;
    cout << "Minimum of 3 numbers is " << smallest(x, y, z);
    return 0;
}
// this code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>

// Using division operator to find
// minimum of three numbers
int smallest(int x, int y, int z)
{
    if (!(y / x)) // Same as "if (y < x)"
        return (!(y / z)) ? y : z;
    return (!(x / z)) ? x : z;
}

int main()
{
    int x = 78, y = 88, z = 68;
    printf("Minimum of 3 numbers is %d", smallest(x, y, z));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of above approach
class GfG {

    // Using division operator to
    // find minimum of three numbers
    static int smallest(int x, int y, int z)
    {
        if ((y / x) != 1) // Same as "if (y < x)"
            return ((y / z) != 1) ? y : z;
        return ((x / z) != 1) ? x : z;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 78, y = 88, z = 68;
        System.out.printf("Minimum of 3 numbers"
                              + " is %d",
                          smallest(x, y, z));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Using division operator to find
# minimum of three numbers
def smallest(x, y, z):

    if (not (y / x)): # Same as "if (y < x)"
        return y if (not (y / z)) else z
    return x if (not (x / z)) else z

# Driver Code
if __name__== "__main__":

    x = 78
    y = 88
    z = 68
    print("Minimum of 3 numbers is",
                  smallest(x, y, z))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program of above approach
using System;
public class GfG {

    // Using division operator to
    // find minimum of three numbers
    static int smallest(int x, int y, int z)
    {
        if ((y / x) != 1) // Same as "if (y < x)"
            return ((y / z) != 1) ? y : z;
        return ((x / z) != 1) ? x : z;
    }

    // Driver code
    public static void Main()
    {
        int x = 78, y = 88, z = 68;
        Console.Write("Minimum of 3 numbers"
                          + " is {0}",
                      smallest(x, y, z));
    }
}
/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Using division operator to find
// minimum of three numbers
function smallest(x, y, z)
{
    if (!(y / x)) // Same as "if (y < x)"
        return (!(y / z)) ? y : z;
    return (!(x / z)) ? x : z;
}

    let x = 78, y = 88, z = 68;
    document.write("Minimum of 3 numbers is " + smallest(x, y, z));

// This is code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Minimum of 3 numbers is 68
```

如果您发现上述代码/算法不正确，请写评论，或者找到其他方法解决相同的问题。