# 写一个计算幂(x，n)

的程序

> 原文:[https://www . geesforgeks . org/write-a-c-program-to-compute-powxn/](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)

给定两个整数 x 和 n，写一个函数计算 x <sup>n</sup> 。我们可以假设 x 和 n 很小，溢出不会发生。

![program to calculate pow(x,n)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/program-to-calculate-powxn-1024x512.png)

**示例:**

```
Input : x = 2, n = 3
Output : 8

Input : x = 7, n = 2
Output : 49
```

**下方解将问题划分为大小为 y/2 的子问题，并递归调用子问题。**

## C++

```
// C++ program to calculate pow(x,n)
#include<iostream>
using namespace std;
class gfg
{

/* Function to calculate x raised to the power y */
public:
int power(int x, unsigned int y)
{
    if (y == 0)
        return 1;
    else if (y % 2 == 0)
        return power(x, y / 2) * power(x, y / 2);
    else
        return x * power(x, y / 2) * power(x, y / 2);
}
};

/* Driver code */
int main()
{
    gfg g;
    int x = 2;
    unsigned int y = 3;

    cout << g.power(x, y);
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
#include<stdio.h>

/* Function to calculate x raised to the power y */
int power(int x, unsigned int y)
{
    if (y == 0)
        return 1;
    else if (y%2 == 0)
        return power(x, y/2)*power(x, y/2);
    else
        return x*power(x, y/2)*power(x, y/2);
}

/* Program to test function power */
int main()
{
    int x = 2;
    unsigned int y = 3;

    printf("%d", power(x, y));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {
    /* Function to calculate x raised to the power y */
    static int power(int x, int y)
    {
        if (y == 0)
            return 1;
        else if (y % 2 == 0)
            return power(x, y / 2) * power(x, y / 2);
        else
            return x * power(x, y / 2) * power(x, y / 2);
    }

    /* Program to test function power */
    public static void main(String[] args)
    {
        int x = 2;
        int y = 3;

        System.out.printf("%d", power(x, y));
    }
}

// This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program to calculate pow(x,n)

# Function to calculate x
# raised to the power y 
def power(x, y):

    if (y == 0): return 1
    elif (int(y % 2) == 0):
        return (power(x, int(y / 2)) *
               power(x, int(y / 2)))
    else:
        return (x * power(x, int(y / 2)) *
                   power(x, int(y / 2)))

# Driver Code
x = 2; y = 3
print(power(x, y))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
using System;

public class GFG {

    // Function to calculate x raised to the power y
    static int power(int x, int y)
    {
        if (y == 0)
            return 1;
        else if (y % 2 == 0)
            return power(x, y / 2) * power(x, y / 2);
        else
            return x * power(x, y / 2) * power(x, y / 2);
    }

    // Program to test function power
    public static void Main()
    {
        int x = 2;
        int y = 3;

        Console.Write(power(x, y));
    }
}

// This code is contributed by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to calculate x 
// raised to the power y
function power($x, $y)
{
    if ($y == 0)
        return 1;
    else if ($y % 2 == 0)
        return power($x, (int)$y / 2) * 
               power($x, (int)$y / 2);
    else
        return $x * power($x, (int)$y / 2) * 
                    power($x, (int)$y / 2);
}

// Driver Code
$x = 2;
$y = 3;

echo power($x, $y);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to calculate pow(x,n)

// Function to calculate x
// raised to the power y 
function power(x, y)
{
    if (y == 0)
        return 1;
    else if (y % 2 == 0)
        return power(x, parseInt(y / 2, 10)) *
               power(x, parseInt(y / 2, 10));
    else
        return x * power(x, parseInt(y / 2, 10)) *
                   power(x, parseInt(y / 2, 10));
}

// Driver code
let x = 2;
let y = 3;

document.write(power(x, y));

// This code is contributed by mukesh07

</script>
```

**输出:**

```
8
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)

**算法范式:**分而治之。
上述函数只需计算一次幂(x，y/2)并存储即可优化为 O(logn)。

## C++

```
/* Function to calculate x raised to the power y in O(logn)*/
int power(int x, unsigned int y)
{
    int temp;
    if( y == 0)
        return 1;
    temp = power(x, y / 2);
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// This code is contributed by Shubhamsingh10
```

## C

```
/* Function to calculate x raised to the power y in O(logn)*/
int power(int x, unsigned int y)
{
    int temp;
    if( y == 0)
        return 1;
    temp = power(x, y/2);
    if (y%2 == 0)
        return temp*temp;
    else
        return x*temp*temp;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Function to calculate x raised to the power y in O(logn)*/
static int power(int x, int y) 
{ 
    int temp; 
    if( y == 0) 
        return 1; 
    temp = power(x, y / 2); 
    if (y % 2 == 0) 
        return temp*temp; 
    else
        return x*temp*temp; 
} 

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Function to calculate x raised to the power y in O(logn)
def power(x,y):
    temp = 0
    if( y == 0):
        return 1
    temp = power(x, int(y / 2))
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;

# This code is contributed by avanitrachhadiya2155
```

## C#

```
/* Function to calculate x raised to the power y in O(logn)*/
static int power(int x, int y) 
{ 
    int temp; 
    if( y == 0) 
        return 1; 
    temp = power(x, y / 2); 
    if (y % 2 == 0) 
        return temp*temp; 
    else
        return x*temp*temp; 
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

/* Function to calculate x raised to the power y in O(logn)*/
function power(x , y) 
{ 
    var temp; 
    if( y == 0) 
        return 1; 
    temp = power(x, y / 2); 
    if (y % 2 == 0) 
        return temp*temp; 
    else
        return x*temp*temp; 
} 

// This code is contributed by todaysgaurav

</script>
```

**优化解的时间复杂度:** O(logn)

**辅助空间:** O(1)

让我们把幂函数推广到负 y 和浮点 x。

## C++

```
/* Extended version of power function 
that can work for float x and negative y*/
#include <bits/stdc++.h>
using namespace std;

float power(float x, int y) 
{ 
    float temp; 
    if(y == 0) 
        return 1; 
    temp = power(x, y / 2); 
    if (y % 2 == 0) 
        return temp * temp; 
    else
    { 
        if(y > 0) 
            return x * temp * temp; 
        else
            return (temp * temp) / x; 
    } 
} 

// Driver Code
int main() 
{ 
    float x = 2; 
    int y = -3; 
    cout << power(x, y); 
    return 0; 
} 

// This is code is contributed 
// by rathbhupendra
```

## C

```
/* Extended version of power function that can work
 for float x and negative y*/
#include<stdio.h>

float power(float x, int y)
{
    float temp;
    if( y == 0)
       return 1;
    temp = power(x, y/2);       
    if (y%2 == 0)
        return temp*temp;
    else
    {
        if(y > 0)
            return x*temp*temp;
        else
            return (temp*temp)/x;
    }
}  

/* Program to test function power */
int main()
{
    float x = 2;
    int y = -3;
    printf("%f", power(x, y));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java code for extended version of power function
that can work for float x and negative y */
class GFG {

    static float power(float x, int y)
    {
        float temp;
        if( y == 0)
            return 1;
        temp = power(x, y/2); 

        if (y%2 == 0)
            return temp*temp;
        else
        {
            if(y > 0)
                return x * temp * temp;
            else
                return (temp * temp) / x;
        }
    } 

    /* Program to test function power */
    public static void main(String[] args)
    {
        float x = 2;
        int y = -3;
        System.out.printf("%f", power(x, y));
    }
}

// This code is contributed by  Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python3 code for extended version
# of power function that can work
# for float x and negative y

def power(x, y):

    if(y == 0): return 1
    temp = power(x, int(y / 2)) 

    if (y % 2 == 0):
        return temp * temp
    else:
        if(y > 0): return x * temp * temp
        else: return (temp * temp) / x

# Driver Code
x, y = 2, -3
print('%.6f' %(power(x, y)))

# This code is contributed by Smitha Dinesh Semwal. 
```

## C#

```
// C# code for extended version of power function
// that can work for float x and negative y

using System;

public class GFG{

    static float power(float x, int y)
    {
        float temp;

        if( y == 0)
            return 1;
        temp = power(x, y/2); 

        if (y % 2 == 0)
            return temp * temp;
        else
        {
            if(y > 0)
                return x * temp * temp;
            else
                return (temp * temp) / x;
        }
    } 

    // Program to test function power 
    public static void Main()
    {
        float x = 2;
        int y = -3;

        Console.Write(power(x, y));
    }
}

// This code is contributed by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Extended version of power
// function that can work
// for float x and negative y

function power($x, $y)
{
    $temp;
    if( $y == 0)
    return 1;
    $temp = power($x, $y / 2);     
    if ($y % 2 == 0)
        return $temp * $temp;
    else
    {
        if($y > 0)
            return $x * 
                   $temp * $temp;
        else
            return ($temp * 
                    $temp) / $x;
    }
} 

// Driver Code
$x = 2;
$y = -3;
echo power($x, $y);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript code for extended 
// version of power function that
// can work for var x and negative y
function power(x, y)
{
    var temp;

    if (y == 0)
        return 1;

    temp = power(x, parseInt(y / 2));

    if (y % 2 == 0)
        return temp * temp;
    else
    {
        if (y > 0)
            return x * temp * temp;
        else
            return (temp * temp) / x;
    }
}

// Driver code
var x = 2;
var y = -3;

document.write( power(x, y).toFixed(6));

// This code is contributed by aashish1995

</script>
```

**输出:**

```
0.125000
```

**时间复杂度:** O(log|n|)

**辅助空间:** O(1)

**使用递归:**

这种方法几乎类似于迭代求解

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int power(int x, int y)
{

    // If x^0 return 1
    if (y == 0)
        return 1;

    // If we need to find of 0^y
    if (x == 0)
        return 0;

    // For all other cases
    return x * power(x, y - 1);
}

// Driver Code
int main()
{
    int x = 2;
    int y = 3;

    cout << (power(x, y));
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    public static int power(int x, int y)
    {

        // If x^0 return 1
        if (y == 0)
            return 1;

        // If we need to find of 0^y
        if (x == 0)
            return 0;

        // For all other cases
        return x * power(x, y - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int x = 2;
        int y = 3;

        System.out.println(power(x, y));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
def power(x, y):

    # If x^0 return 1
    if (y == 0):
        return 1

    # If we need to find of 0^y
    if (x == 0):
        return 0

    # For all other cases
    return x * power(x, y - 1)

# Driver Code
x = 2
y = 3

print(power(x, y))

# This code is contributed by shivani.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

public static int power(int x, int y)
{

    // If x^0 return 1
    if (y == 0)
        return 1;

    // If we need to find of 0^y
    if (x == 0)
        return 0;

    // For all other cases
    return x * power(x, y - 1);
}

// Driver Code
public static void Main(String[] args)
{
    int x = 2;
    int y = 3;

    Console.WriteLine(power(x, y));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// javascript program for the above approach
    function power(x , y) {

        // If x^0 return 1
        if (y == 0)
            return 1;

        // If we need to find of 0^y
        if (x == 0)
            return 0;

        // For all other cases
        return x * power(x, y - 1);
    }

    // Driver Code

        var x = 2;
        var y = 3;

        document.write(power(x, y));

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
8
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**使用 java 的 Math.pow()函数:**

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int power(int x, int y)
{

    // return type of pow() 
    // function is double
    return (int)pow(x, y);
}

// Driver Code
int main()
{
    int x = 2;
    int y = 3;

    cout << (power(x, y));
}

// This code is contributed by hemantraj712.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    public static int power(int x, int y)
    {

        // Math.pow() is a function that
        // return floating number
        return (int)Math.pow(x, y);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int x = 2;
        int y = 3;

        System.out.println(power(x, y));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
def power(x, y):

    # Return type of pow() 
    # function is double
    return pow(x, y)

# Driver Code
x = 2
y = 3

print(power(x, y))

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach

using System;

public class GFG {

    public static int power(int x, int y)
    {

        // Math.pow() is a function that
        // return floating number
        return (int)Math.Pow(x, y);
    }

    // Driver code
    static public void Main()
    {
        int x = 2;
        int y = 3;

        Console.WriteLine(power(x, y));
    }
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    function power( x, y)
    {

        // Math.pow() is a function that
        // return floating number
        return parseInt(Math.pow(x, y));
    }

    // Driver Code

        let x = 2;
        let y = 3;

        document.write(power(x, y));

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
8
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**非递归方法:**对于新手来说，这是一个非常高效的方法，因为新手觉得很难理解迭代递归调用。这个方法也需要 **T(n)= O(log(n))** 的复杂度。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int power(int x, int y)
{
    int result = 1;
    while (y > 0) {
        if (y % 2 == 0) // y is even
        {
            x = x * x;
            y = y / 2;
        }
        else // y isn't even
        {
            result = result * x;
            y = y - 1;
        }
    }
    return result;
}

// Driver Code
int main()
{
    int x = 2;
    int y = 3;

    cout << (power(x, y));
    return 0;
}

// This code is contributed by Madhav Mohan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

static int power(int x, int y)
{
    int result = 1;

    while (y > 0) 
    {

        // y is even
        if (y % 2 == 0) 
        {
            x = x * x;
            y = y / 2;
        }

        // y isn't even
        else 
        {
            result = result * x;
            y = y - 1;
        }
    }
    return result;
}

// Driver Code
public static void main(String[] args) 
{
    int x = 2;
    int y = 3;

    System.out.println(power(x, y));
}
}

// This code is contributed by hritikrommie
```

## 蟒蛇 3

```
# Python program for the above approach
def power( x, y):

    result = 1
    while (y > 0): 
        if (y % 2 == 0): 
        # y is even

            x = x * x
            y = y / 2

        else:
        # y isn't even

            result = result * x
            y = y - 1

    return result

# Driver Code
x = 2
y = 3
print((power(x, y)))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for above approach
using System;

class GFG{

static int power(int x, int y)
{
    int result = 1;

    while (y > 0) 
    {

        // y is even
        if (y % 2 == 0) 
        {
            x = x * x;
            y = y / 2;
        }

        // y isn't even
        else 
        {
            result = result * x;
            y = y - 1;
        }
    }
    return result;
}

// Driver Code
public static void Main(String[] args) 
{
    int x = 2;
    int y = 3;

    Console.Write(power(x, y));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program for the above approach

function power(x,y)
{
    let result = 1;
    while (y > 0) {
        if (y % 2 == 0) // y is even
        {
            x = x * x;
            y = Math.floor(y / 2);
        }
        else // y isn't even
        {
            result = result * x;
            y = y - 1;
        }
    }
    return result;
}

// Driver Code
let x = 2;
let y = 3;
document.write(power(x, y))

// This code is contributed by rag2127
</script>
```

**Output**

```
8
```

***时间复杂度:** O(log <sub>2</sub> y)*

***辅助空间:** O(1)*

[**为 pow(x，y)**](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/)
[**写一个迭代的 O(Log y)函数求幂(模运算中的幂)**](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)
如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。