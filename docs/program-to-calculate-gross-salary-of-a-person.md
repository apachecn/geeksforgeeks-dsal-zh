# 计算一个人工资总额的程序

> 原文:[https://www . geeksforgeeks . org/计算毛工资程序/](https://www.geeksforgeeks.org/program-to-calculate-gross-salary-of-a-person/)

给定一个整数**基本**和一个字符**等级**，分别表示一个人的基本工资和等级，任务是找到这个人的总工资。

**总工资:**在加上 DA、HRA 和其他津贴后计算的最终工资。总薪资的公式定义如下:

> 总薪资=基本+ HRA + DA +允许–PF
> 此处，HRA =基本的 20%
> DA =基本的 50%
> 如果等级= 'A'
> 允许= 1700 如果等级= 'B'
> 允许= 1300 如果等级= 'C'
> PF =基本的 11%

**示例:**

> **输入:**基础= 10000，等级= ' A '
> T3】输出: 17600
> 
> **输入:**基础= 4567，等级= ' B '
> T3】输出: 8762

**方法:**思路是根据等级找到津贴，然后根据基本工资计算 HRA、DA、PF。以下是人力资源评估、人力资源开发和人力资源绩效的计算说明:

*   **HRA:** 房租补贴为基本工资的 20%；

> HRA =基本工资* 0.20

*   **DA:** 日津贴为基本工资的 50%；

> DA =基本工资* 0.5

*   **PF:** 公积金是基本工资的 11%。

> PF =基本工资* 0.11

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// salary of the person
int computeSalary(int basic,
                char grade)
{
    int allowance;
    double hra, da, pf;

    hra = 0.2 * basic;
    da = 0.5 * basic;
    pf = 0.11 * basic;

    // Condition to compute the
    // allowance for the person
    if (grade == 'A') {
        allowance = 1700;
    }
    else if (grade == 'B') {
        allowance = 1500;
    }
    else {
        allowance = 1300;
    }
    int gross;

    // Calculate gross salary
    gross = round(basic + hra + da + allowance - pf);
    return gross;
}

// Driver Code
int main()
{
    int basic = 10000;
    char grade = 'A';

    cout << computeSalary(basic, grade);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to calculate the
// salary of the person
static int computeSalary(int basic,
                        char grade)
{
    double allowance;
    double hra, da, pf;

    hra = 0.2 * basic;
    da = 0.5 * basic;
    pf = 0.11 * basic;

    // Condition to compute the
    // allowance for the person
    if (grade == 'A')
    {
        allowance = 1700.0;
    }
    else if (grade == 'B')
    {
        allowance = 1500.0;
    }
    else
    {
        allowance = 1300.0;
    }
    double gross;

    // Calculate gross salary
    gross = Math.round(basic + hra + da +
                         allowance - pf);

    return (int)gross;
}

// Driver Code
public static void main (String[] args)
{
    int basic = 10000;
    char grade = 'A';

    // Function call
    System.out.println(computeSalary(basic, grade));
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the
# salary of the person
def computeSalary( basic, grade):

    hra = 0.2 * basic
    da = 0.5 * basic
    pf = 0.11 * basic

    # Condition to compute the
    # allowance for the person
    if grade == 'A':
        allowance = 1700.0
    elif grade == 'B':
        allowance = 1500.0
    else:
        allowance = 1300.0;

    gross = round(basic + hra + da +
                    allowance - pf)

    return gross

# Driver code
if __name__ == '__main__':

    basic = 10000
    grade = 'A'

    # Function call
    print(computeSalary(basic, grade));

# This code is contributed by jana_sayantan
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate the
// salary of the person
static int computeSalary(int basic,
                        char grade)
{
    double allowance;
    double hra, da, pf;

    hra = 0.2 * basic;
    da = 0.5 * basic;
    pf = 0.11 * basic;

    // Condition to compute the
    // allowance for the person
    if (grade == 'A')
    {
        allowance = 1700.0;
    }
    else if (grade == 'B')
    {
        allowance = 1500.0;
    }
    else
    {
        allowance = 1300.0;
    }
    double gross;

    // Calculate gross salary
    gross = Math.Round(basic + hra + da +
                         allowance - pf);

    return (int)gross;
}

// Driver Code
public static void Main (String[] args)
{
    int basic = 10000;
    char grade = 'A';

    // Function call
    Console.WriteLine(computeSalary(basic, grade));
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to calculate the
// salary of the person
function computeSalary(basic,
                        grade)
{
    let allowance;
    let hra, da, pf;

    hra = 0.2 * basic;
    da = 0.5 * basic;
    pf = 0.11 * basic;

    // Condition to compute the
    // allowance for the person
    if (grade == 'A')
    {
        allowance = 1700.0;
    }
    else if (grade == 'B')
    {
        allowance = 1500.0;
    }
    else
    {
        allowance = 1300.0;
    }
    let gross;

    // Calculate gross salary
    gross = Math.round(basic + hra + da +
                         allowance - pf);

    return gross;
}

// Driver code
    let basic = 10000;
    let grade = 'A';

    // Function call
    document.write(computeSalary(basic, grade));

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
17600
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*