# 求解单变量线性方程

> 原文:[https://www . geesforgeks . org/求解单变量线性方程/](https://www.geeksforgeeks.org/solve-the-linear-equation-of-single-variable/)

给定一个线性方程，任务是找到所用变量的值。该方程只包含“+”、“-”运算、变量及其系数。

1.  如果方程没有解，返回“无解”。
2.  如果方程有无穷多个解，返回“无穷多个解”。
3.  如果方程只有一个解，确保 x 的值是整数。

**示例:**

```
Input : "x + 5 - 3 + x = 6 + x - 2"
Output : "x = 2"

Input : "x = x"
Output : "Infinite solutions"

Input: "2x = x"
Output: "x = 0"

Input: "x = x + 2"
Output: "No solution"

```

**方法:**思路是用两个指针更新两个参数:所用变量的系数和总和。在“=”的左侧和右侧，对每个数字使用相反的符号，由符号变量处理，一旦看到“=”，符号变量将翻转。

现在，在唯一解的情况下，有效总数和系数的比值给出了所需的结果。在无限解的情况下，有效总数和系数都为零，例如 x + 1 = x + 1。在无解的情况下，x 的系数原来是零，但有效总数是非零的。

## C++

```
// CPP program to solve the given equation
#include <bits/stdc++.h>
using namespace std;

// Function to solve the given equation
string solveEquation(string equation)
{
    int n = equation.size(), sign = 1, coeff = 0;
    int total = 0, i = 0;

    // Traverse the equation
    for (int j = 0; j < n; j++) {
        if (equation[j] == '+' || equation[j] == '-') {
            if (j > i)
                total += sign * stoi(equation.substr(i, j - i));
            i = j;
        }

        // For cases such as: x, -x, +x
        else if (equation[j] == 'x') {
            if ((i == j) || equation[j - 1] == '+')
                coeff += sign;
            else if (equation[j - 1] == '-')
                coeff -= sign;
            else
                coeff += sign * stoi(equation.substr(i, j - i));
            i = j + 1;
        }

        // Flip sign once '=' is seen
        else if (equation[j] == '=') {
            if (j > i)
                total += sign * stoi(equation.substr(i, j - i));
            sign = -1;
            i = j + 1;
        }
    }

    // There may be a number left in the end
    if (i < n)
        total += sign * stoi(equation.substr(i));

    // For infinite solutions
    if (coeff == 0 && total == 0)
        return "Infinite solutions";

    // For no solution
    if (coeff == 0 && total)
        return "No solution";

    // x = total sum / coeff of x
    // '-' sign indicates moving
    // numeric value to right hand side
    int ans = -total / coeff;
    return "x=" + to_string(ans);
}

// Driver code
int main()
{
    string equation = "x+5-3+x=6+x-2";
    cout << solveEquation(equation);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve
// the given equation
import java.io.*;

class GFG
{
// Function to solve 
// the given equation
static String solveEquation(String equation)
{
    int n = equation.length(), 
        sign = 1, coeff = 0;
    int total = 0, i = 0;

    // Traverse the equation
    for (int j = 0; j < n; j++) 
    {
        if (equation.charAt(j) == '+' || 
            equation.charAt(j) == '-')
        {
            if (j > i)
                total += sign * 
                         Integer.parseInt(
                                 equation.substring(i, j));
            i = j;
        }

        // For cases such 
        // as: x, -x, +x
        else if (equation.charAt(j) == 'x')
        {
            if ((i == j) || 
                 equation.charAt(j - 1) == '+')
                coeff += sign;

            else if (equation.charAt(j - 1) == '-')
                coeff -= sign;

            else
                coeff += sign * 
                         Integer.parseInt(
                                 equation.substring(i, j));
            i = j + 1;
        }

        // Flip sign once 
        // '=' is seen
        else if (equation.charAt(j) == '=') 
        {
            if (j > i)
                total += sign * 
                         Integer.parseInt(
                                 equation.substring(i, j));
            sign = -1;
            i = j + 1;
        }
    }

    // There may be a 
    // number left in the end
    if (i < n)
        total = total + 
                sign * 
                Integer.parseInt(
                        equation.substring(i));

    // For infinite
    // solutions
    if (coeff == 0 && 
        total == 0)
        return "Infinite solutions";

    // For no solution
    if (coeff == 0 && 
        total != 0)
        return "No solution";

    // x = total sum / coeff 
    // of x '-' sign indicates 
    // moving numeric value to 
    // right hand side
    int ans = -total / coeff;
    return (Integer.toString(ans));
}

// Driver code
public static void main(String args[])
{
    String equation = new String("x+5-3+x=6+x-2");
    System.out.print("x = " + 
                      solveEquation(equation));
}
}

// This code is contributed by 
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python program to solve
# the given equation

# def to solve 
# the given equation
def solveEquation(equation) :

    n = len(equation) 
    sign = 1
    coeff = 0
    total = 0
    i = 0

    # Traverse the equation
    for j in range(0, n) :

        if (equation[j] == '+' or
            equation[j] == '-') :

            if (j > i) :
                total = (total + sign * 
                         int(equation[i: j]))
            i = j

        # For cases such 
        # as: x, -x, +x
        elif (equation[j] == 'x') :

            if ((i == j) or
                equation[j - 1] == '+') :
                coeff += sign
            elif (equation[j - 1] == '-') :
                coeff = coeff - sign
            else :
                coeff = (coeff + sign * 
                         int(equation[i: j]))
            i = j + 1

        # Flip sign once 
        # '=' is seen
        elif (equation[j] == '=') :

            if (j > i) :
                total = (total + sign * 
                         int(equation[i: j]))
            sign = -1
            i = j + 1

    # There may be a number
    # left in the end
    if (i < n) :
        total = (total + sign * 
                 int(equation[i: len(equation)]))

    # For infinite solutions
    if (coeff == 0 and
        total == 0) :
        return "Infinite solutions"

    # For no solution
    if (coeff == 0 and total) :
        return "No solution"

    # x = total sum / coeff of x
    # '-' sign indicates moving
    # numeric value to right hand side
    ans = -total / coeff
    return int(ans)

# Driver code
equation = "x+5-3+x=6+x-2"
print ("x = {}" . 
        format(solveEquation(equation)))

# This code is contributed by 
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to solve
// the given equation
using System;

class GFG
{
    // Function to solve 
    // the given equation
    static string solveEquation(string equation)
    {
        int n = equation.Length, 
            sign = 1, coeff = 0;
        int total = 0, i = 0;

        // Traverse the equation
        for (int j = 0; j < n; j++) 
        {
            if (equation[j] == '+' || 
                equation[j] == '-')
            {
                if (j > i)
                    total += sign * 
                             Int32.Parse(
                             equation.Substring(i, j - i));
                i = j;
            }

            // For cases such 
            // as: x, -x, +x
            else if (equation[j] == 'x')
            {
                if ((i == j) || 
                     equation[j - 1] == '+')
                    coeff += sign;

                else if (equation[j - 1] == '-')
                    coeff -= sign;

                else
                    coeff += sign * 
                             Int32.Parse(
                             equation.Substring(i, j - i));
                i = j + 1;
            }

            // Flip sign once 
            // '=' is seen
            else if (equation[j] == '=') 
            {
                if (j > i)
                    total += sign * 
                             Int32.Parse(
                             equation.Substring(i, j - i));
                sign = -1;
                i = j + 1;
            }
        }

        // There may be a 
        // number left in the end
        if (i < n)
            total += sign * 
                     Int32.Parse(
                     equation.Substring(i));

        // For infinite
        // solutions
        if (coeff == 0 && total == 0)
            return "Infinite solutions";

        // For no solution
        if (coeff == 0 && total != 0)
            return "No solution";

        // x = total sum / coeff 
        // of x '-' sign indicates 
        // moving numeric value to 
        // right hand side
        int ans = -total / coeff;
        return "x = " + ans.ToString();
    }

    // Driver code
    static void Main()
    {
        string equation = "x+5-3+x=6+x-2";
        Console.Write(solveEquation(equation));
    }
}

// This code is contributed by 
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to solve
// the given equation

// Function to solve 
// the given equation
function solveEquation($equation)
{
    $n = strlen($equation); 
    $sign = 1; $coeff = 0;
    $total = 0; $i = 0;

    // Traverse the equation
    for ($j = 0; $j < $n; $j++) 
    {
        if ($equation[$j] == '+' || 
            $equation[$j] == '-')
        {
            if ($j > $i)
                $total += $sign * 
                          intval(substr($equation, 
                                        $i, $j - $i));
            $i = $j;
        }

        // For cases such 
        // as: x, -x, +x
        else if ($equation[$j] == 'x') 
        {
            if (($i == $j) || 
                 $equation[$j - 1] == '+')
                $coeff += $sign;
            else if ($equation[$j - 1] == '-')
                $coeff -= $sign;
            else
                $coeff += $sign * 
                          intval(substr($equation, 
                                        $i, $j - $i));
            $i = $j + 1;
        }

        // Flip sign once 
        // '=' is seen
        else if ($equation[$j] == '=') 
        {
            if ($j > $i)
                $total += $sign * 
                          intval(substr($equation, 
                                        $i, $j - $i));
            $sign = -1;
            $i = $j + 1;
        }
    }

    // There may be a number
    // left in the end
    if ($i < $n)
        $total += $sign * 
                  intval(substr($equation, $i));

    // For infinite solutions
    if ($coeff == 0 && 
        $total == 0)
        return "Infinite solutions";

    // For no solution
    if ($coeff == 0 && $total)
        return "No solution";

    // x = total sum / coeff of x
    // '-' sign indicates moving
    // numeric value to right hand side
    $ans = -$total / $coeff;
    return "x = " . $ans;
}

// Driver code
$equation = "x+5-3+x=6+x-2";
echo (solveEquation($equation));

// This code is contributed by 
// Manish Shaw(manishshaw1)
?>
```

**Output:**

```
x = 2

```

**时间复杂度:** O(n)，其中 n 为方程串的长度。
**辅助空间:** O(1)