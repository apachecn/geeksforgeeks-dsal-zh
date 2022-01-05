# 使用递归打印三角形和菱形图案的程序

> 原文:[https://www . geesforgeks . org/programs-to-print-triangle-and-diamond-patterns-use-recursion/](https://www.geeksforgeeks.org/programs-to-print-triangle-and-diamond-patterns-using-recursion/)

本文旨在给出一个用于模式打印的[递归实现](https://www.geeksforgeeks.org/recursion/)。

1.  **模式 1:**
    **示例:**

```
Input: 5
Output: 
* * * * *   * * * * * 
* * * *       * * * * 
* * *           * * * 
* *               * * 
*                   *
```

1.  实施:t1

## C++

```
// Program to print the given pattern

#include <iostream>
using namespace std;
void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    cout << "* ";
    print_asterisk(asterisk - 1);
}
void print_space(int space)
{
    if (space == 0)
        return;
    cout << " "
         << " ";
    print_space(space - 1);
}

// function to print the pattern
void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    cout << endl;

    // recursively calling pattern()
    pattern(n - 1, num);
}

// driver function
int main()
{
    int n = 5;
    pattern(n, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to print the given pattern
import java.util.*;
class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    System.out.print("* ");
    print_asterisk(asterisk - 1);
}
static void print_space(int space)
{
    if (space == 0)
        return;
    System.out.print(" ");
    System.out.print(" ");
    print_space(space - 1);
}

// function to print the pattern
static void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    System.out.print("\n");

    // recursively calling pattern()
    pattern(n - 1, num);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Program to print the given pattern
def print_asterisk(asterisk):
    if (asterisk == 0):
        return;
    print("* ", end = "");
    print_asterisk(asterisk - 1);

def print_space(space):
    if (space == 0):
        return;
    print(" ", end = "");
    print(" ", end = "");
    print_space(space - 1);

# function to print the pattern
def pattern(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    print("");

    # recursively calling pattern()
    pattern(n - 1, num);

# Driver Code
if __name__ == '__main__':
    n = 5;
    pattern(n, n);

# This code is contributed by Princi Singh
```

## C#

```
// C# Program to print the given pattern
using System;

class GFG
{

static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    Console.Write("* ");
    print_asterisk(asterisk - 1);
}

static void print_space(int space)
{
    if (space == 0)
        return;
    Console.Write(" ");
    Console.Write(" ");
    print_space(space - 1);
}

// function to print the pattern
static void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    Console.Write("\n");

    // recursively calling pattern()
    pattern(n - 1, num);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

      // JavaScript Program to print the
      // given pattern

      function print_asterisk(asterisk)
      {
        if (asterisk === 0) return;
        document.write("*  ");
        print_asterisk(asterisk - 1);
      }

      function print_space(space)
      {
        if (space === 0) return;
        document.write("  " + "  ");
        print_space(space - 1);
      }

      // function to print the pattern
      function pattern(n, num)
      {
        // base case
        if (n === 0) return;
        print_asterisk(n);
        print_space(2 * (num - n) + 1);
        print_asterisk(n);
        document.write("<br>");

        // recursively calling pattern()
        pattern(n - 1, num);
      }

      // driver function
      var n = 5;
      pattern(n, n);

</script>
```

1.  **输出:**

```
* * * * *   * * * * * 
* * * *       * * * * 
* * *           * * * 
* *               * * 
*                   * 
```

2.  **模式 2:**
    **示例:**

```
Input: 5
Output: 
*                   * 
* *               * * 
* * *           * * * 
* * * *       * * * * 
* * * * *   * * * * *
```

1.  实施:t1

## C++

```
// Program to print the given pattern

#include <iostream>
using namespace std;
void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    cout << "* ";
    print_asterisk(asterisk - 1);
}
void print_space(int space)
{
    if (space == 0)
        return;
    cout << " "
         << " ";
    print_space(space - 1);
}

// function to print the pattern
void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    cout << endl;

    // recursively calling pattern()
    pattern(n - 1, num);
}

// driver function
int main()
{
    int n = 5;
    pattern(n, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to print the given pattern
class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    System.out.print("* ");
    print_asterisk(asterisk - 1);
}
static void print_space(int space)
{
    if (space == 0)
        return;
    System.out.print(" ");
    System.out.print(" ");
    print_space(space - 1);
}

// function to print the pattern
static void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    System.out.println();

    // recursively calling pattern()
    pattern(n - 1, num);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Program to print the given pattern
def print_asterisk(asterisk):
    if (asterisk == 0):
        return;
    print("*", end = " ");
    print_asterisk(asterisk - 1);

def print_space(space):
    if (space == 0):
        return;
    print(" ", end = "");
    print(" ", end = "");
    print_space(space - 1);

# function to print the pattern
def pattern(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    print();

    # recursively calling pattern()
    pattern(n - 1, num);

# Driver Code
if __name__ == '__main__':
    n = 5;
    pattern(n, n);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to print the given pattern
using System;

class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    Console.Write("* ");
    print_asterisk(asterisk - 1);
}

static void print_space(int space)
{
    if (space == 0)
        return;
    Console.Write(" ");
    Console.Write(" ");
    print_space(space - 1);
}

// function to print the pattern
static void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    Console.WriteLine();

    // recursively calling pattern()
    pattern(n - 1, num);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Program to print the given pattern
function print_asterisk(asterisk)
{
    if (asterisk == 0)
        return;
    document.write("* ");
    print_asterisk(asterisk - 1);
}
function print_space(space)
{
    if (space == 0)
        return;
    document.write(" ", " ", " ");
    print_space(space - 1);
}

// function to print the pattern
function pattern(n, num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n + 1);
    print_asterisk(num - n + 1);
    document.write("<br>");

    // recursively calling pattern()
    pattern(n - 1, num);
}

// driver function
var n = 5;
pattern(n, n);

// This code is contributed by Shubham Singh

</script>
```

1.  **输出:**

```
*                   * 
* *               * * 
* * *           * * * 
* * * *       * * * * 
* * * * *   * * * * * 
```

2.  **模式 3:**
    **示例:**

```
Input: 5
Output: 
    * * * * *
    * * * *  
    * * *    
    * *      
    *        
    *        
    * *      
    * * *    
    * * * *  
    * * * * *
```

1.  实施:t1

## C++

```
// Program to print the given pattern

#include <iostream>
using namespace std;
void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    cout << "* ";
    print_asterisk(asterisk - 1);
}

// function to print the upper-half of the pattern
void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    cout << endl;

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
void pattern_lower(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    cout << endl;

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// driver function
int main()
{
    int n = 5;
    pattern(n, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to print the given pattern
class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    System.out.print("* ");
    print_asterisk(asterisk - 1);
}

// function to print the upper-half of the pattern
static void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    System.out.println();

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
static void pattern_lower(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    System.out.println();

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
static void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print the given pattern
def print_asterisk(asterisk):
    if (asterisk == 0):
        return;
    print("*", end = " ");
    print_asterisk(asterisk - 1);

# function to print the
# upper-half of the pattern
def pattern_upper(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(n);
    print();

    # recursively calling pattern_upper()
    pattern_upper(n - 1, num);

# function to print the
# lower-half of the pattern
def pattern_lower(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(num - n + 1);
    print();

    # recursively calling pattern_lower()
    pattern_lower(n - 1, num);

# function to print the pattern
def pattern(n, num):
    pattern_upper(n, num);
    pattern_lower(n - 1, num);

# Driver Code
if __name__ == '__main__':
    n = 5;
    pattern(n, n);

# This code is contributed by Rajput-Ji
```

## C#

```
// Program to print the given pattern
using System;

class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    Console.Write("* ");
    print_asterisk(asterisk - 1);
}

// function to print the upper-half of the pattern
static void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    Console.WriteLine();

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
static void pattern_lower(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    Console.WriteLine();

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
static void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Program to print the given pattern

    function print_asterisk(asterisk) {
        if (asterisk == 0)
            return;
        document.write("* ");
        print_asterisk(asterisk - 1);
    }

    // function to print the upper-half of the pattern
    function pattern_upper(n , num) {
        // base case
        if (n == 0)
            return;
        print_asterisk(n);
        document.write("<br/>");

        // recursively calling pattern_upper()
        pattern_upper(n - 1, num);
    }

    // function to print the lower-half of the pattern
    function pattern_lower(n , num) {
        // base case
        if (n == 0)
            return;
        print_asterisk(num - n + 1);
        document.write("<br/>");

        // recursively calling pattern_lower()
        pattern_lower(n - 1, num);
    }

    // function to print the pattern
    function pattern(n , num) {
        pattern_upper(n, num);
        pattern_lower(n - 1, num);
    }

    // Driver Code

        var n = 5;
        pattern(n, n);

// This code is contributed by aashish1995

</script>
```

1.  **输出:**

```
    * * * * *
    * * * *  
    * * *    
    * *      
    *        
    *        
    * *      
    * * *    
    * * * *  
    * * * * *
```

2.  **模式 4:**
    **示例:**

```
Input: 5
Output: 
* * * * *   * * * * * 
* * * *       * * * * 
* * *           * * * 
* *               * * 
*                   * 
* *               * * 
* * *           * * * 
* * * *       * * * * 
* * * * *   * * * * * 
```

1.  实施:t1

## C++

```
// Program to print the given pattern

#include <iostream>
using namespace std;
void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    cout << "* ";
    print_asterisk(asterisk - 1);
}
void print_space(int space)
{
    if (space == 0)
        return;
    cout << " "
         << " ";
    print_space(space - 1);
}

// function to print the upper-half of the pattern
void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    cout << endl;

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
void pattern_lower(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    cout << endl;

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// driver function
int main()
{
    int n = 5;
    pattern(n, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print the given pattern
import java.util.*;

class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    System.out.print("* ");
    print_asterisk(asterisk - 1);
}

static void print_space(int space)
{
    if (space == 0)
        return;
    System.out.print(" ");
    System.out.print(" ");
    print_space(space - 1);
}

// function to print the upper-half of the pattern
static void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    System.out.print("\n");

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
static void pattern_lower(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    System.out.print("\n");

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
static void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// driver function
public static void main(String[] args)
{
    int n = 5;
    pattern(n, n);   
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print the given pattern
def print_asterisk(asterisk):

    if (asterisk == 0):
        return;
    print("* ", end = "");
    print_asterisk(asterisk - 1);

def print_space(space):

    if (space == 0):
        return;
    print(" ", end = "");
    print(" ", end = "");
    print_space(space - 1);

# function to print the upper-half of the pattern
def pattern_upper(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    print();

    # recursively calling pattern_upper()
    pattern_upper(n - 1, num);

# function to print the lower-half of the pattern
def pattern_lower(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    print();

    # recursively calling pattern_lower()
    pattern_lower(n - 1, num);

# function to print the pattern
def pattern(n, num):

    pattern_upper(n, num);
    pattern_lower(n - 1, num);

# Driver Code
if __name__ == '__main__':
    n = 5;
    pattern(n, n);

# This code is contributed by Rajput Ji
```

## C#

```
// C# Program to print the given pattern
using System;

class GFG
{
static void print_asterisk(int asterisk)
{
    if (asterisk == 0)
        return;
    Console.Write("* ");
    print_asterisk(asterisk - 1);
}

static void print_space(int space)
{
    if (space == 0)
        return;
    Console.Write(" ");
    Console.Write(" ");
    print_space(space - 1);
}

// function to print the upper-half of the pattern
static void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    Console.Write("\n");

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
static void pattern_lower(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    Console.Write("\n");

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
static void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Program to print the given pattern

function print_asterisk(asterisk)
{
    if (asterisk == 0)
        return;
    document.write("* ");
    print_asterisk(asterisk - 1);
}
function print_space(space)
{
    if (space == 0)
        return;
    document.write(" ", " ", " ");
    print_space(space - 1);
}

// function to print the upper-half of the pattern
function pattern_upper( n,  num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    document.write("<br>");

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
function pattern_lower(n, num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    document.write("<br>");

    // recursively calling pattern_lower()
    pattern_lower(n - 1, num);
}

// function to print the pattern
function pattern(n, num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// driver function
n = 5;
pattern(n, n);

// This code is contributed by shubham singh

</script>
```

1.  **输出:**

```
* * * * *   * * * * * 
* * * *       * * * * 
* * *           * * * 
* *               * * 
*                   * 
* *               * * 
* * *           * * * 
* * * *       * * * * 
* * * * *   * * * * * 
```

2.  **图案 5:**
    **示例:**

```
Input: 5
Output: 
*                   * 
* *               * * 
* * *           * * * 
* * * *       * * * * 
* * * * *   * * * * * 
* * * *       * * * * 
* * *           * * * 
* *               * * 
*                   * 
```

1.  实施:t1

## C++

```
// Program to print the given pattern

#include <iostream>
using namespace std;
void print_asterisk(int asterisk)
{
    // base case
    if (asterisk == 0)
        return;
    cout << "* ";
    print_asterisk(asterisk - 1);
}
void print_space(int space)
{
    // base case
    if (space == 0)
        return;
    cout << " "
         << " ";
    print_space(space - 1);
}

// function to print the upper-half of the pattern
void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    cout << endl;

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
void pattern_lower(int n, int num)
{
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    cout << endl;

    // recursively calling pattern_lower(
    pattern_lower(n - 1, num);
}

// function to print the pattern
void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// driver function
int main()
{
    int n = 5;
    pattern(n, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the given pattern
class GFG
{

static void print_asterisk(int asterisk)
{
    // base case
    if (asterisk == 0)
        return;
    System.out.print("* ");
    print_asterisk(asterisk - 1);
}

static void print_space(int space)
{
    // base case
    if (space == 0)
        return;
    System.out.print(" ");
    System.out.print(" ");
    print_space(space - 1);
}

// function to print the upper-half of the pattern
static void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    System.out.println();

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
static void pattern_lower(int n, int num)
{
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    System.out.println();

    // recursively calling pattern_lower(
    pattern_lower(n - 1, num);
}

// function to print the pattern
static void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print the given pattern
def print_asterisk(asterisk):

    # base case
    if (asterisk == 0):
        return;
    print("* ", end = "");
    print_asterisk(asterisk - 1);

def print_space(space):

    # base case
    if (space == 0):
        return;
    print(" ", end = "");
    print(" ", end = "");
    print_space(space - 1);

# function to print the
# upper-half of the pattern
def pattern_upper(n, num):

    # base case
    if (n == 0):
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    print();

    # recursively calling pattern_upper()
    pattern_upper(n - 1, num);

# function to print the lower-half
# of the pattern
def pattern_lower(n, num):

    if (n == 0):
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    print();

    # recursively calling pattern_lower(
    pattern_lower(n - 1, num);

# function to print the pattern
def pattern(n, num):

    pattern_upper(n, num);
    pattern_lower(n - 1, num);

# Driver Code
if __name__ == '__main__':
    n = 5;
    pattern(n, n);

# This code is contributed by Princi Raj
```

## C#

```
// C# program to print the given pattern
using System;

class GFG
{
static void print_asterisk(int asterisk)
{
    // base case
    if (asterisk == 0)
        return;
    Console.Write("* ");
    print_asterisk(asterisk - 1);
}

static void print_space(int space)
{
    // base case
    if (space == 0)
        return;
    Console.Write(" ");
    Console.Write(" ");
    print_space(space - 1);
}

// function to print
// the upper-half of the pattern
static void pattern_upper(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    Console.WriteLine();

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
static void pattern_lower(int n, int num)
{
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    Console.WriteLine();

    // recursively calling pattern_lower(
    pattern_lower(n - 1, num);
}

// function to print the pattern
static void pattern(int n, int num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Java program to print the given pattern

function print_asterisk(asterisk)
{
    // base case
    if (asterisk == 0)
        return;
    document.write("*  ");
    print_asterisk(asterisk - 1);
}

function print_space(space)
{
    // base case
    if (space == 0)
        return;
    document.write("  ");
    document.write("  ");
    print_space(space - 1);
}

// function to print the upper-half of the pattern
function pattern_upper(n,num)
{
    // base case
    if (n == 0)
        return;
    print_asterisk(num - n + 1);
    print_space(2 * n - 1);
    print_asterisk(num - n + 1);
    document.write("<br>");

    // recursively calling pattern_upper()
    pattern_upper(n - 1, num);
}

// function to print the lower-half of the pattern
function pattern_lower(n,num)
{
    if (n == 0)
        return;
    print_asterisk(n);
    print_space(2 * (num - n) + 1);
    print_asterisk(n);
    document.write("<br>");

    // recursively calling pattern_lower(
    pattern_lower(n - 1, num);
}

// function to print the pattern
function pattern(n,num)
{
    pattern_upper(n, num);
    pattern_lower(n - 1, num);
}

// Driver Code
let n = 5;
pattern(n, n);

// This code is contributed by rag2127
</script>
```

1.  **输出:**

```
*                   * 
* *               * * 
* * *           * * * 
* * * *       * * * * 
* * * * *   * * * * * 
* * * *       * * * * 
* * *           * * * 
* *               * * 
*                   * 
```