# 计算 cos(nθ)值的程序

> 原文:[https://www . geesforgeks . org/program-to-find-of-value-of-cosn/](https://www.geeksforgeeks.org/program-to-find-the-value-of-cosn/)

给定 cos(θ)值和变量![n    ](img/493367f432400add124059588b6d9677.png "Rendered by QuickLaTeX.com")。任务是利用三角函数的性质求 cos(nθ)的值。
**注:** n < = 15。
**例** :

```
Input : cos(Θ) = 0.5, n = 10
Output : -0.5

Input :cos(Θ) = 0.5, n = 3
Output : -0.995523
```

问题可以用[棣莫佛公式定理](https://en.wikipedia.org/wiki/De_Moivre%27s_formula)和[二项式定理](https://en.wikipedia.org/wiki/Binomial_theorem)解决如下:
**利用德莫瓦夫定理，我们有**:

![\begin{align*} \cos(n\theta)+\iota \sin(n\theta)&=(\cos \theta+\iota \sin \theta)^n\\ &=\cos^n \theta +\binom{n}{1} \cos^{n-1} \theta (\iota \sin \theta)+\binom{n}{2} \cos^{n-2} \theta (\iota \sin \theta)^2+\\ & \binom{n}{3} \cos^{n-3} \theta (\iota \sin \theta)^3+ \cdots \\ \end{align*} Equating the result to real part to get the value of $\cos n\theta$ finally, we have\\ $\cos (n \theta)=\binom{n}{0}\cos^{n}\theta \sin^0 \theta-\binom{n}{2}\cos^{n-2}\theta \sin^2 \theta+\binom{n}{4}\cos^{n-4}\theta \sin^4 \theta- \cdots$ \\ \\ As we have value of $\cos \theta$, \\ we can find value of $\sin \theta $\\ $\sin \theta=\sqrt{1-\cos^2 \theta}$    ](img/ffc7efe2cbd7371c54104806903baaea.png "Rendered by QuickLaTeX.com")

现在，sin(θ)和 cos(θ)的值已知。把这些值放在上面的等式中，得到答案。
以下是上述思路的实现:

## C++

```
// CPP program to find the value of cos(n-theta)

#include <bits/stdc++.h>

#define MAX 16

using namespace std;

int nCr[MAX][MAX] = { 0 };

// Function to calculate the binomial
// coefficient upto 15
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

// Function to find the value of cos(n-theta)
double findCosnTheta(double cosTheta, int n)
{
    // find sinTheta from cosTheta
    double sinTheta = sqrt(1 - cosTheta * cosTheta);

    // to store required answer
    double ans = 0;

    // use to toggle sign in sequence.
    int toggle = 1;

    for (int i = 0; i <= n; i += 2) {
        ans = ans + nCr[n][i] * pow(cosTheta, n - i) *
                              pow(sinTheta, i) * toggle;
        toggle = toggle * -1;
    }

    return ans;
}

// Driver code
int main()
{
    binomial();

    double cosTheta = 0.5;

    int n = 10;

    cout << findCosnTheta(cosTheta, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the value of cos(n-theta)

class GFG
{
    static int MAX=16;
    static int[][] nCr=new int[MAX][MAX];

// Function to calculate the binomial
// coefficient upto 15
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

// Function to find the value of cos(n-theta)
static double findCosnTheta(double cosTheta, int n)
{
    // find sinTheta from cosTheta
    double sinTheta = Math.sqrt(1 - cosTheta * cosTheta);

    // to store required answer
    double ans = 0;

    // use to toggle sign in sequence.
    int toggle = 1;

    for (int i = 0; i <= n; i += 2) {
        ans = ans + nCr[n][i] * Math.pow(cosTheta, n - i) *
                            Math.pow(sinTheta, i) * toggle;
        toggle = toggle * -1;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    binomial();

    double cosTheta = 0.5;

    int n = 10;

    System.out.println(String.format("%.5f",findCosnTheta(cosTheta, n)));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find the value of cos(n-theta)

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
def findCosnTheta(cosTheta,n):

    # find sinTheta from cosTheta
    sinTheta = math.sqrt(1 - cosTheta * cosTheta)

    # to store the required answer
    ans = 0

    # use to toggle sign in sequence.
    toggle = 1
    for i in range(0,n+1,2):
        ans = ans + nCr[n][i]*(cosTheta**(n - i)) *(sinTheta**i) * toggle
        toggle = toggle * -1
    return ans

# Driver code
if __name__=='__main__':
    binomial()
    cosTheta = 0.5
    n = 10
    print(findCosnTheta(cosTheta, n))

# this code is contributed by sahilshelangia
```

## C#

```
// C# program to find the value of cos(n-theta)
using System;
public class GFG{
    static int MAX=16;
    static int [,]nCr=new int[MAX,MAX];

    // Function to calculate the binomial
    // coefficient upto 15
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

    // Function to find the value of cos(n-theta)
    static double findCosnTheta(double cosTheta, int n)
    {
        // find sinTheta from cosTheta
        double sinTheta = Math.Sqrt(1 - cosTheta * cosTheta);

        // to store required answer
        double ans = 0;

        // use to toggle sign in sequence.
        int toggle = 1;

        for (int i = 0; i <= n; i += 2) {
            ans = ans + nCr[n,i] * Math.Pow(cosTheta, n - i) *
                                Math.Pow(sinTheta, i) * toggle;
            toggle = toggle * -1;
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        binomial();

        double cosTheta = 0.5;
        int n = 10;
        Console.WriteLine(findCosnTheta(cosTheta, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the value of cos(n-theta)

MAX = 16

var nCr = Array.from(Array(MAX), () => new Array(MAX));

// Function to calculate the binomial
// coefficient upto 15
function binomial()
{
    // use simple DP to find coefficient
    for (var i = 0; i < MAX; i++) {
        for (var j = 0; j <= i; j++) {
            if (j == 0 || j == i)
                nCr[i][j] = 1;
            else
                nCr[i][j] = nCr[i - 1][j] + nCr[i - 1][j - 1];
        }
    }
}

// Function to find the value of cos(n-theta)
function findCosnTheta(cosTheta, n)
{
    // find sinTheta from cosTheta
    var sinTheta = Math.sqrt(1 - cosTheta * cosTheta);

    // to store required answer
    var ans = 0;

    // use to toggle sign in sequence.
    var toggle = 1;

    for (var i = 0; i <= n; i += 2) {
        ans = ans + nCr[n][i] * Math.pow(cosTheta, n - i) *
                            Math.pow(sinTheta, i) * toggle;
        toggle = toggle * -1;
    }

    return ans.toFixed(1);
}

// Driver code
binomial();
var cosTheta = 0.5;
var n = 10;
document.write( findCosnTheta(cosTheta, n));

</script>
```

**Output:** 

```
-0.5
```