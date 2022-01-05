# 求 sin(nθ)值的程序

> 原文:[https://www . geesforgeks . org/program-to-find-value-of-sinn/](https://www.geeksforgeeks.org/program-to-find-the-value-of-sinn/)

给定 sin(θ)的值和变量 n <=15\. The task is to find the value of sin(nΘ) using property of trigonometric functions.
**示例** :

```
Input: sin(Θ)=0.5, n=1
Output: 0.5

Input: sin(Θ)=0.5, n=10
Output: -0.866025
```

**方法:**这个问题可以用[棣莫佛公式定理](https://en.wikipedia.org/wiki/De_Moivre%27s_formula)和[二项式定理](https://en.wikipedia.org/wiki/Binomial_theorem)来解决

![\begin{document} Using De-Moivre's theorem, we have- \begin{align*} \cos(n\theta)+\iota \sin(n\theta)&=(\cos \theta+\iota \sin \theta)^n\\ &=\cos^n \theta +\binom{n}{1} \cos^{n-1} \theta (\iota \sin \theta)+\binom{n}{2} \cos^{n-2} \theta (\iota \sin \theta)^2+\\ & \binom{n}{3} \cos^{n-3} \theta (\iota \sin \theta)^3+ \cdots \\ \end{align*} Equating the result to imaginary part to get the value of $\sin n\theta$ finally, we got-\\ $\sin (n \theta)=\binom{n}{1}\cos^{n-1}\theta \sin \theta-\binom{n}{3}\cos^{n-3}\theta \sin^3 \theta+\binom{n}{5}\cos^{n-5}\theta \sin^5 \theta- \cdots$\\ As we have value of $\sin \theta$, \\ we can find value of $\cos \theta $\\ $\cos \theta=\sqrt{1-\sin^2 \theta}$ \end{document}   ](img/41da49a8f279112a2a7d73da96a14adc.png "Rendered by QuickLaTeX.com")

现在，我们有 sin(θ)和 cos(θ)。把这个值放在等式中，得到你的答案。
以下是上述方法的实施:

## C++

```
// C++ Program to find the value of sin(n?)
#include <bits/stdc++.h>
#define ll long long int
#define MAX 16
using namespace std;
ll nCr[MAX][MAX] = { 0 };

// This function use to calculate the
// binomial coefficient upto 15
void binomial()
{
    // use simple DP to find coefficient
    for (int i = 0; i < MAX; i++) {
        for (int j = 0; j <= i; j++) {
            if (j == 0 || j == i)
                nCr[i][j] = 1;
            else
                nCr[i][j] = nCr[i - 1][j] + nCr[i - 1][j - 1];
        }
    }
}

// Function to find the value of
double findCosNTheta(double sinTheta, ll n)
{
    // find cosTheta from sinTheta
    double cosTheta = sqrt(1 - sinTheta * sinTheta);

    // store required answer
    double ans = 0;
    // use to toggle sign in sequence.
    ll toggle = 1;
    for (int i = 1; i <= n; i += 2) {
        ans = ans + nCr[n][i] * pow(cosTheta, n - i) 
                        * pow(sinTheta, i) * toggle;
        toggle = toggle * -1;
    }
    return ans;
}

// Driver code.
int main()
{
    binomial();
    double sinTheta = 0.5;
    ll n = 10;

    cout << findCosNTheta(sinTheta, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the value of sin(n?)

public class GFG {

    private static final int MAX = 16;
    static long nCr[][] = new long [MAX][MAX];

    // This function use to calculate the 
    // binomial coefficient upto 15 
    static void binomial() 
    { 
        // use simple DP to find coefficient 
        for (int i = 0; i < MAX; i++) { 
            for (int j = 0; j <= i; j++) { 
                if (j == 0 || j == i) 
                    nCr[i][j] = 1; 
                else
                    nCr[i][j] = nCr[i - 1][j] + nCr[i - 1][j - 1]; 
            } 
        } 
    } 

    // Function to find the value of 
    static double findCosNTheta(double sinTheta, int n) 
    { 
        // find cosTheta from sinTheta 
        double cosTheta = Math.sqrt(1 - sinTheta * sinTheta); 

        // store required answer 
        double ans = 0; 
        // use to toggle sign in sequence. 
        long toggle = 1; 
        for (int i = 1; i <= n; i += 2) { 
            ans = ans + nCr[n][i] * Math.pow(cosTheta, n - i) 
                            * Math.pow(sinTheta, i) * toggle; 
            toggle = toggle * -1; 
        } 
        return ans; 
    } 

    // Driver code 
    public static void main (String args[]){
            binomial(); 
            double sinTheta = 0.5; 
            int n = 10; 

            System.out.println(findCosNTheta(sinTheta, n));
    }

// This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to find the 
# value of sin(n-theta) 

import math 
MAX=16
nCr=[[0 for i in range(MAX)] for i in range(MAX)] 

# Function to calculate the binomial 
# coefficient upto 15 
def binomial(): 

    # use simple DP to find coefficient 
    for i in range(MAX): 
        for j in range(0,i+1): 
            if j == 0 or j == i: 
                nCr[i][j] = 1
            else: 
                nCr[i][j] = nCr[i - 1][j] + nCr[i - 1][j - 1] 

# Function to find the value of cos(n-theta) 
def findCosNTheta(sinTheta,n): 

    # find sinTheta from sinTheta 
    cosTheta = math.sqrt(1 - sinTheta * sinTheta) 

    # to store required answer 
    ans = 0

    # use to toggle sign in sequence. 
    toggle = 1
    for i in range(1,n+1,2): 
        ans = (ans + nCr[n][i]*(cosTheta**(n - i)) 
              *(sinTheta**i) * toggle) 
        toggle = toggle * -1
    return ans 

# Driver code 
if __name__=='__main__': 
    binomial() 
    sinTheta = 0.5
    n = 10
    print(findCosNTheta(sinTheta, n)) 

# this code is contributed by sahilshelangia 
```

## C#

```
// C# Program to find the value of sin(n?)
using System;

class GFG 
{

private static int MAX = 16;
static long[,] nCr = new long [MAX, MAX];

// This function use to calculate the 
// binomial coefficient upto 15 
static void binomial() 
{ 
    // use simple DP to find coefficient 
    for (int i = 0; i < MAX; i++) 
    { 
        for (int j = 0; j <= i; j++) 
        { 
            if (j == 0 || j == i) 
                nCr[i, j] = 1; 
            else 
                nCr[i, j] = nCr[i - 1, j] + 
                            nCr[i - 1, j - 1]; 
        } 
    } 
} 

// Function to find the value of cos(n-theta) 
static double findCosNTheta(double sinTheta, int n) 
{ 
    // find cosTheta from sinTheta 
    double cosTheta = Math.Sqrt(1 - sinTheta * 
                                    sinTheta); 

    // store required answer 
    double ans = 0; 

    // use to toggle sign in sequence. 
    long toggle = 1; 
    for (int i = 1; i <= n; i += 2) 
    { 
        ans = ans + nCr[n, i] * Math.Pow(cosTheta, n - i) *
                                Math.Pow(sinTheta, i) * toggle; 
        toggle = toggle * -1; 
    } 
    return ans; 
} 

// Driver code 
public static void Main ()
{
    binomial(); 
    double sinTheta = 0.5; 
    int n = 10; 

    Console.Write(findCosNTheta(sinTheta, n));
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the value of sin(n?)
$MAX=16;
$nCr=array_fill(0,$MAX,array_fill(0,$MAX,0));

// This function use to calculate the
// binomial coefficient upto 15
function binomial()
{
    global $MAX,$nCr;
    // use simple DP to find coefficient
    for ($i = 0; $i < $MAX; $i++) {
        for ($j = 0; $j <= $i; $j++) {
            if ($j == 0 || $j == $i)
                $nCr[$i][$j] = 1;
            else
                $nCr[$i][$j] = $nCr[$i - 1][$j] + $nCr[$i - 1][$j - 1];
        }
    }
}

// Function to find the value of
function findCosNTheta($sinTheta,$n)
{
    global $MAX,$nCr;
    // find cosTheta from sinTheta
    $cosTheta = sqrt(1 - $sinTheta * $sinTheta);

    // store required answer
    $ans = 0;
    // use to toggle sign in sequence.
    $toggle = 1;
    for ($i = 1; $i <= $n; $i += 2) {
        $ans = $ans + $nCr[$n][$i] * pow($cosTheta, $n - $i) 
                        * pow($sinTheta, $i) * $toggle;
        $toggle = $toggle * -1;
    }
    return $ans;
}

// Driver code.

    binomial();
    $sinTheta = 0.5;
    $n = 10;

    echo findCosNTheta($sinTheta, $n);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the value of sin(n?)
MAX = 16
var nCr = Array.from(Array(MAX), () => new Array(MAX));

// This function use to calculate the
// binomial coefficient upto 15
function binomial()
{
    // use simple DP to find coefficient
    for (var i = 0; i < MAX; i++) {
        for (var j = 0; j <= i; j++) {
            if (j == 0 || j == i)
                nCr[i][j] = 1;
            else
                nCr[i][j] = nCr[i - 1][j] + 
                nCr[i - 1][j - 1];
        }
    }
}

// Function to find the value of
function findCosNTheta(sinTheta, n)
{
    // find cosTheta from sinTheta
    var cosTheta = Math.sqrt(1 - sinTheta * sinTheta);

    // store required answer
    var ans = 0;
    // use to toggle sign in sequence.
    var toggle = 1;
    for (var i = 1; i <= n; i += 2) {
        ans = ans + nCr[n][i] * Math.pow(cosTheta, n - i)
                        * Math.pow(sinTheta, i) * toggle;
        toggle = toggle * -1;
    }
    return ans.toFixed(6);
}

// Driver code.
binomial();
var sinTheta = 0.5;
var n = 10;
document.write( findCosNTheta(sinTheta, n));

</script>
```

**Output:** 

```
-0.866025
```