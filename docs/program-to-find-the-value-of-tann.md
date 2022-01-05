# 计算 tan(nθ)值的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-value-of-tann/](https://www.geeksforgeeks.org/program-to-find-the-value-of-tann/)

给定 tan(θ)值和变量 n <=15\. The task is to find the value of tan(nΘ) using property of trigonometric functions.
**示例** :

```
Input: tan(Θ) = 0.3, n = 10
Output: -2.15283

Input: tan(Θ) = 0.3, n = 5
Output: 0.37293
```

问题可以用[棣莫佛公式定理](https://en.wikipedia.org/wiki/De_Moivre%27s_formula)和[二项式定理](https://en.wikipedia.org/wiki/Binomial_theorem)解决如下:
**利用德莫瓦夫定理，我们有**:

![\begin{align*} \cos(n\theta)+\iota \sin(n\theta)&=(\cos \theta+\iota \sin \theta)^n\\ &=\cos^n \theta +\binom{n}{1} \cos^{n-1} \theta (\iota \sin \theta)+\binom{n}{2} \cos^{n-2} \theta (\iota \sin \theta)^2+\\ & \binom{n}{3} \cos^{n-3} \theta (\iota \sin \theta)^3+ \cdots \\ \end{align*} Equating the result to real part to get the value of $\cos n\theta$ finally, we got-\\ $\cos (n \theta)=\binom{n}{0}\cos^{n}\theta \sin^0 \theta-\binom{n}{2}\cos^{n-2}\theta \sin^2 \theta+\binom{n}{4}\cos^{n-4}\theta \sin^4 \theta- \cdots$ \\ Equating the result to imaginary part to get the value of $\sin n\theta$ finally, we got-\\ $\sin (n \theta)=\binom{n}{1}\cos^{n-1}\theta \sin^1 \theta-\binom{n}{3}\cos^{n-3}\theta \sin^3 \theta+\binom{n}{5}\cos^{n-5}\theta \sin^5 \theta- \cdots$ \\ \\ As we know, $\tan n\theta=\frac{\sin n\theta}{\cos n\theta}$ \\ Put the value of $\sin n\theta $ and $\cos n\theta$, We get\\ $\tan n\theta=\frac{\binom{n}{1}\cos^{n-1}\theta \sin^1 \theta-\binom{n}{3}\cos^{n-3}\theta \sin^3 \theta+\binom{n}{5}\cos^{n-5}\theta \sin^5 \theta- \cdots}{\binom{n}{0}\cos^{n}\theta \sin^0 \theta-\binom{n}{2}\cos^{n-2}\theta \sin^2 \theta+\binom{n}{4}\cos^{n-4}\theta \sin^4 \theta- \cdots}$ \\ Dividing numerator and denomenator by $\cos^n \theta$\\ $\tan n\theta=\frac{\binom{n}{1}\tan^1 \theta-\binom{n}{3}\tan^3 \theta+\binom{n}{5}\tan^5 \theta-\cdots}{1-\binom{n}{2}\tan^2 \theta+\binom{n}{4}\tan^4 \theta-\binom{n}{6}\tan^6 \theta+\cdots}$ As we have value of $\tan \theta$, \\ Put in final equation-    ](img/f8b5544fc2a4278471450511d6c8825e.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program to find the value 
// of cos(n-theta) 

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
double findTanNTheta(double tanTheta, ll n)
{
    // store required answer
    double ans = 0, numerator = 0, denominator = 0;

    // use to toggle sign in sequence.
    ll toggle = 1;

    // calculate numerator
    for (int i = 1; i <= n; i += 2) {
        numerator = numerator + nCr[n][i] * pow(tanTheta, i) * toggle;
        toggle = toggle * -1;
    }

    // calculate denominator
    denominator = 1;
    toggle = -1;

    for (int i = 2; i <= n; i += 2) {
        numerator = numerator + nCr[n][i] * pow(tanTheta, i) * toggle;
        toggle = toggle * -1;
    }

    ans = numerator / denominator;

    return ans;
}

// Driver code.
int main()
{
    binomial();
    double tanTheta = 0.3;

    ll n = 10;

    cout << findTanNTheta(tanTheta, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the value 
// of cos(n-theta) 
public class GFG {

    private static final int MAX = 16 ;
    static long nCr[][] = new long [MAX][MAX] ;

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
    static double findTanNTheta(double tanTheta, int n) 
    { 
        // store required answer 
        double ans = 0, numerator = 0, denominator = 0; 

        // use to toggle sign in sequence. 
        long toggle = 1; 

        // calculate numerator 
        for (int i = 1; i <= n; i += 2) { 
            numerator = numerator + nCr[n][i] * Math.pow(tanTheta, i) * toggle; 
            toggle = toggle * -1; 
        } 

        // calculate denominator 
        denominator = 1; 
        toggle = -1; 

        for (int i = 2; i <= n; i += 2) { 
            numerator = numerator + nCr[n][i] * Math.pow(tanTheta, i) * toggle; 
            toggle = toggle * -1; 
        } 

        ans = numerator / denominator; 

        return ans; 
    }

    // Driver code
    public static void main(String args[])
    {
        binomial(); 
        double tanTheta = 0.3; 
        int n = 10; 
        System.out.println(findTanNTheta(tanTheta, n));
    }
// This code is contributed by ANKITRAI1 
}
```

## 蟒蛇 3

```
# Python3 program to find the value 
# of cos(n-theta) 

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
def findTanNTheta(tanTheta,n): 

    # store required answer
    numerator=0
    denominator=1

    # to store required answer 
    ans = 0

    # use to toggle sign in sequence. 
    toggle = 1

    # calculate numerator
    for i in range(1,n+1,2): 
        numerator = (numerator + nCr[n][i]*
                    (tanTheta**(i)) * toggle) 
        toggle = toggle * -1
    # calculate denominator 
    toggle=-1
    for i in range(2,n+1,2): 
        numerator = (numerator + nCr[n][i]*
                    (tanTheta**i) * toggle) 
        toggle = toggle * -1
    ans=numerator/denominator
    return ans

# Driver code 
if __name__=='__main__': 
    binomial() 
    tanTheta = 0.3
    n = 10
    print(findTanNTheta(tanTheta, n)) 

# this code is contributed by sahilshelangia 
```

## C#

```
// C# program to find the value 
// of cos(n-theta) 

using System;
public class GFG {

    private static int MAX = 16 ;
    static long[,] nCr = new long [MAX,MAX] ;

    // This function use to calculate the 
    // binomial coefficient upto 15 
    static void binomial() 
    { 

        // use simple DP to find coefficient 
        for (int i = 0; i < MAX; i++) { 
            for (int j = 0; j <= i; j++) { 
                if (j == 0 || j == i) 
                    nCr[i,j] = 1; 
                else
                    nCr[i,j] = nCr[i - 1,j] + nCr[i - 1,j - 1]; 
            } 
        } 
    } 

    // Function to find the value of 
    static double findTanNTheta(double tanTheta, int n) 
    { 
        // store required answer 
        double ans = 0, numerator = 0, denominator = 0; 

        // use to toggle sign in sequence. 
        long toggle = 1; 

        // calculate numerator 
        for (int i = 1; i <= n; i += 2) { 
            numerator = numerator + nCr[n,i] * Math.Pow(tanTheta, i) * toggle; 
            toggle = toggle * -1; 
        } 

        // calculate denominator 
        denominator = 1; 
        toggle = -1; 

        for (int i = 2; i <= n; i += 2) { 
            numerator = numerator + nCr[n,i] * Math.Pow(tanTheta, i) * toggle; 
            toggle = toggle * -1; 
        } 

        ans = numerator / denominator; 

        return ans; 
    }

    // Driver code
    public static void Main()
    {
        binomial(); 
        double tanTheta = 0.3; 
        int n = 10; 
        Console.Write(findTanNTheta(tanTheta, n));
    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the value 
// of cos(n-theta) 

$MAX=16;
$nCr=array_fill(0, $MAX, array_fill(0, $MAX, 0));

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
function findTanNTheta($tanTheta, $n)
{
    global $MAX,$nCr;
    // store required answer
    $ans = 0;
    $numerator = 0;
    $denominator = 0;

    // use to toggle sign in sequence.
    $toggle = 1;

    // calculate numerator
    for ($i = 1; $i <= $n; $i += 2) {
        $numerator = $numerator + $nCr[$n][$i] * pow($tanTheta, $i) * $toggle;
        $toggle = $toggle * -1;
    }

    // calculate denominator
    $denominator = 1;
    $toggle = -1;

    for ($i = 2; $i <= $n; $i += 2) {
        $numerator = $numerator + $nCr[$n][$i] * pow($tanTheta, $i) * $toggle;
        $toggle = $toggle * -1;
    }

    $ans = $numerator / $denominator;

    return $ans;
}

// Driver code.

    binomial();
    $tanTheta = 0.3;

    $n = 10;

    echo findTanNTheta($tanTheta, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the value
// of cos(n-theta)

MAX = 16
var nCr = Array.from(Array(MAX), ()=> new Array(MAX));

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
function findTanNTheta(tanTheta, n)
{
    // store required answer
    ans = 0, numerator = 0, denominator = 0;

    // use to toggle sign in sequence.
    toggle = 1;

    // calculate numerator
    for (var i = 1; i <= n; i += 2) {
        numerator = numerator + nCr[n][i] * 
        Math.pow(tanTheta, i) * toggle;
        toggle = toggle * -1;
    }

    // calculate denominator
    denominator = 1;
    toggle = -1;

    for (var i = 2; i <= n; i += 2) {
        numerator = numerator + nCr[n][i] * 
        Math.pow(tanTheta, i) * toggle;
        toggle = toggle * -1;
    }

    ans = numerator / denominator;

    return ans.toFixed(5);
}

// Driver code.
binomial();
var tanTheta = 0.3;
var n = 10;
document.write( findTanNTheta(tanTheta, n));

</script>
```

**Output:** 

```
-2.15283
```