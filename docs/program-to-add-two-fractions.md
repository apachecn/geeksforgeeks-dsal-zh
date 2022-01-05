# 程序添加两个分数

> 原文:[https://www.geeksforgeeks.org/program-to-add-two-fractions/](https://www.geeksforgeeks.org/program-to-add-two-fractions/)

加两个分数 a/b 和 c/d，用最简单的形式打印答案。
**例:**

```
Input:  1/2 + 3/2
Output: 2/1

Input:  1/3 + 3/9
Output: 2/3

Input:  1/5 + 3/15
Output: 2/5
```

**两个分数相加的算法**

*   通过找到两个分母的最小公倍数来找到公分母。
*   改变分数，使其具有相同的分母，并将两项相加。
*   通过将分子和分母除以最大公因数，将得到的最终分数简化为更简单的形式。

## C++

```
// C++ program to add 2 fractions
#include<bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Function to convert the obtained fraction
// into it's simplest form
void lowest(int &den3, int &num3)
{
    // Finding gcd of both terms
    int common_factor = gcd(num3,den3);

    // Converting both terms into simpler
    // terms by dividing them by common factor
    den3 = den3/common_factor;
    num3 = num3/common_factor;
}

//Function to add two fractions
void addFraction(int num1, int den1, int num2,
                 int den2, int &num3, int &den3)
{
    // Finding gcd of den1 and den2
    den3 = gcd(den1,den2);

    // Denominator of final fraction obtained
    // finding LCM of den1 and den2
    // LCM * GCD = a * b
    den3 = (den1*den2) / den3;

    // Changing the fractions to have same denominator
    // Numerator of the final fraction obtained
    num3 = (num1)*(den3/den1) + (num2)*(den3/den2);

    // Calling function to convert final fraction
    // into it's simplest form
    lowest(den3,num3);
}

// Driver program
int main()
{
    int num1=1, den1=500, num2=2, den2=1500, den3, num3;
    addFraction(num1, den1, num2, den2, num3, den3);
    printf("%d/%d + %d/%d is equal to %d/%d\n", num1, den1,
                                   num2, den2, num3, den3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add 2 fractions

class GFG{
// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Function to convert the obtained fraction
// into it's simplest form
static void lowest(int den3, int num3)
{
    // Finding gcd of both terms
    int common_factor = gcd(num3,den3);

    // Converting both terms into simpler
    // terms by dividing them by common factor
    den3 = den3/common_factor;
    num3 = num3/common_factor;
    System.out.println(num3+"/"+den3);
}

//Function to add two fractions
static void addFraction(int num1, int den1,
                        int num2, int den2)
{
    // Finding gcd of den1 and den2
    int den3 = gcd(den1,den2);

    // Denominator of final fraction obtained
    // finding LCM of den1 and den2
    // LCM * GCD = a * b
    den3 = (den1*den2) / den3;

    // Changing the fractions to have same denominator
    // Numerator of the final fraction obtained
    int num3 = (num1)*(den3/den1) + (num2)*(den3/den2);

    // Calling function to convert final fraction
    // into it's simplest form
    lowest(den3,num3);
}

// Driver program
public static void main(String[] args)
{
    int num1=1, den1=500, num2=2, den2=1500;
    System.out.print(num1+"/"+den1+" + "+num2+"/"+den2+" is equal to ");
    addFraction(num1, den1, num2, den2);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to add 2 fractions

# Function to return gcd of a and b
def gcd(a, b):
    if (a == 0):
        return b;
    return gcd(b % a, a);

# Function to convert the obtained
# fraction into it's simplest form
def lowest(den3, num3):

    # Finding gcd of both terms
    common_factor = gcd(num3, den3);

    # Converting both terms
    # into simpler terms by
    # dividing them by common factor
    den3 = int(den3 / common_factor);
    num3 = int(num3 / common_factor);
    print(num3, "/", den3);

# Function to add two fractions
def addFraction(num1, den1, num2, den2):

    # Finding gcd of den1 and den2
    den3 = gcd(den1, den2);

    # Denominator of final
    # fraction obtained finding
    # LCM of den1 and den2
    # LCM * GCD = a * b
    den3 = (den1 * den2) / den3;

    # Changing the fractions to
    # have same denominator Numerator
    # of the final fraction obtained
    num3 = ((num1) * (den3 / den1) +
            (num2) * (den3 / den2));

    # Calling function to convert
    # final fraction into it's
    # simplest form
    lowest(den3, num3);

# Driver Code
num1 = 1; den1 = 500;
num2 = 2; den2 = 1500;

print(num1, "/", den1, " + ", num2, "/",
      den2, " is equal to ", end = "");
addFraction(num1, den1, num2, den2);

# This code is contributed by mits
```

## C#

```
// C# program to add 2 fractions

class GFG{
// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Function to convert the obtained fraction
// into it's simplest form
static void lowest(int den3, int num3)
{
    // Finding gcd of both terms
    int common_factor = gcd(num3,den3);

    // Converting both terms into simpler
    // terms by dividing them by common factor
    den3 = den3/common_factor;
    num3 = num3/common_factor;
    System.Console.WriteLine(num3+"/"+den3);
}

//Function to add two fractions
static void addFraction(int num1, int den1, int num2, int den2)
{
    // Finding gcd of den1 and den2
    int den3 = gcd(den1,den2);

    // Denominator of final fraction obtained
    // finding LCM of den1 and den2
    // LCM * GCD = a * b
    den3 = (den1*den2) / den3;

    // Changing the fractions to have same denominator
    // Numerator of the final fraction obtained
    int num3 = (num1)*(den3/den1) + (num2)*(den3/den2);

    // Calling function to convert final fraction
    // into it's simplest form
    lowest(den3,num3);
}

// Driver program
public static void Main()
{
    int num1=1, den1=500, num2=2, den2=1500;
    System.Console.Write(num1+"/"+den1+" + "+num2+"/"+den2+" is equal to ");
    addFraction(num1, den1, num2, den2);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to add
// 2 fractions

// Function to return
// gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to convert the
// obtained fraction into
// it's simplest form
function lowest(&$den3, &$num3)
{
    // Finding gcd of both terms
    $common_factor = gcd($num3, $den3);

    // Converting both terms 
    // into simpler terms by
    // dividing them by common factor

    $den3 = (int)$den3 / $common_factor;
    $num3 = (int) $num3 / $common_factor;
}

// Function to add
// two fractions
function addFraction($num1, $den1, $num2,
                     $den2, &$num3, &$den3)
{
    // Finding gcd of den1 and den2
    $den3 = gcd($den1, $den2);

    // Denominator of final
    // fraction obtained finding
    // LCM of den1 and den2
    // LCM * GCD = a * b
    $den3 = ($den1 * $den2) / $den3;

    // Changing the fractions to
    // have same denominator Numerator
    // of the final fraction obtained
    $num3 = ($num1) * ($den3 / $den1) +
            ($num2) * ($den3 / $den2);

    // Calling function to convert
    // final fraction into it's
    // simplest form
    lowest($den3, $num3);
}

// Driver Code
$num1 = 1; $den1 = 500;
$num2 = 2; $den2 = 1500;
$den3; $num3;
addFraction($num1, $den1, $num2,
            $den2, $num3, $den3);
echo $num1, "/", $den1, " + ",
     $num2,"/", $den2, " is equal to ",
               $num3, "/", $den3, "\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to add 2 fractions

// Function to return gcd of a and b

const gcd = (a, b) => {
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to convert the 
// obtained fraction into 
// it's simplest form

const lowest = (den3, num3) => {
    // Finding gcd of both terms
    let common_factor = gcd(num3, den3);

    // Converting both terms  
    // into simpler terms by 
    // dividing them by common factor 

    den3 = parseInt(den3 / common_factor);
    num3 = parseInt(num3 / common_factor);

    document.write(`${num3}/${den3}`)
}

// Function to add two fractions
const addFraction = (num1, den1, num2, den2) => {
    // Finding gcd of den1 and den2
    let den3 = gcd(den1, den2);

    // Denominator of final 
    // fraction obtained finding 
    // LCM of den1 and den2
    // LCM * GCD = a * b 
    den3 = (den1 * den2) / den3;

    // Changing the fractions to 
    // have same denominator Numerator
    // of the final fraction obtained
    let num3 = ((num1) * (den3 / den1) +
            (num2) * (den3 / den2));

    // Calling function to convert 
    // final fraction into it's 
    // simplest form
    lowest(den3, num3);
}

// Driver Code
let num1 = 1;
let den1 = 500; 
let num2 = 2;
let den2 = 1500; 

document.write(`${num1}/${den1} + ${num2}/${den2} is equal to `);

addFraction(num1, den1, num2, den2);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1/500 + 2/1500 is equal to 1/300
```

使用库函数做同样的事情，见下文。
[c++中的比率操纵|集 1(算术)](https://www.geeksforgeeks.org/ratio-manipulations-in-c-set-1-arithmetic/)
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。