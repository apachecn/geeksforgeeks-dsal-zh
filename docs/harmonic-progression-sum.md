# 调和级数和

> 原文:[https://www.geeksforgeeks.org/harmonic-progression-sum/](https://www.geeksforgeeks.org/harmonic-progression-sum/)

给定级数“a”的第一个元素，元素“d”和级数“n”中的项数之间的共同区别，其中![n, d, a \in [1, 100000]  ](img/5fc63782871a778074444e99f09f4e98.png "Rendered by QuickLaTeX.com")。任务是利用上述信息生成调和级数。
**例:**

```
Input : a = 12, d = 12, n = 5 
Output : Harmonic Progression :
         1/12 1/24 1/36 1/48 1/60 

         Sum of the generated harmonic 
         progression : 0.19

         Sum of the generated harmonic 
         progression using approximation :0.19    
```

[算术级数:](https://en.wikipedia.org/wiki/Arithmetic_progression)在算术级数(AP)或算术序列中，是一个数字序列，使得连续项之间的差是恒定的。
[调和级数:](https://en.wikipedia.org/wiki/Harmonic_progression_(mathematics))调和级数(或调和序列)是通过取算术级数的倒数而形成的级数。
现在，我们需要生成这个调和级数。我们甚至要计算生成序列的总和。
1。生成 HP 或 1/AP 是一个简单的任务。AP 中的第 n 项= a + (n-1)d .利用这个公式，我们可以很容易地生成序列。
2。计算这个级数或序列的和可能是一项耗时的任务。我们可以在生成这个序列时迭代，或者我们可以使用一些近似值，并得出一个公式，该公式将为我们提供精确到小数点后几位的值。下面是一个近似公式。

> sum = 1/d(ln(2a+(2n–1)d)/(2a–d))

以上公式详见[brilliant.org](https://brilliant.org/wiki/harmonic-progression/)。
以下是上述公式的实现。

## C++

```
// C++ code to generate Harmonic Progression
// and calculate the sum of the progression.
#include <bits/stdc++.h>
using namespace std;

// Function that generates the harmonic progression
// and calculates the sum of its elements by iterating.
double generateAP(int a, int d, int n, int AP[])
{
    double sum = 0;
    for (int i = 1; i <= n; i++)
    {

        // HP = 1/AP
        // In AP, ith term is calculated by a+(i-1)d;
        AP[i] = (a + (i - 1) * d);

        // Calculating the sum.
        sum += (double)1 / (double)((a + (i - 1) * d));
    }
    return sum;
}

// Function that uses riemenn sum method to calculate
// the approximate sum of HP in O(1) time complexity
double sumApproximation(int a, int d, int n)
{
    return log((2 * a + (2 * n - 1) * d) /
                            (2 * a - d)) / d;
}

// Driver code
int main()
{
    int a = 12, d = 12, n = 5;
    int AP[n + 5] ;

    // Generating AP from the above data
    double sum = generateAP(a, d, n, AP);

    // Generating HP from the generated AP
    cout<<"Harmonic Progression :"<<endl;
    for (int i = 1; i <= n; i++)
        cout << "1/" << AP[i] << " ";
    cout << endl;
    string str = "";
    str = str + to_string(sum);
    str = str.substr(0, 4);

    cout<< "Sum of the generated"
            <<" harmonic progression : " << str << endl;
    sum = sumApproximation(a, d, n);

    str = "";
    str = str + to_string(sum);
    str = str.substr(0, 4);
    cout << "Sum of the generated "
    << "harmonic progression using approximation : "
                                        << str;
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate Harmonic Progression
// and calculate the sum of the progression.
import java.util.*;
import java.lang.*;

class GeeksforGeeks {

    // Function that generates the harmonic progression
    // and calculates the sum of its elements by iterating.
    static double generateAP(int a, int d, int n, int AP[])
    {
        double sum = 0;
        for (int i = 1; i <= n; i++) {

            // HP = 1/AP
            // In AP, ith term is calculated by a+(i-1)d;
            AP[i] = (a + (i - 1) * d);

            // Calculating the sum.
            sum += (double)1 / (double)((a + (i - 1) * d));
        }
        return sum;
    }

    // Function that uses riemenn sum method to calculate
    // the approximate sum of HP in O(1) time complexity
    static double sumApproximation(int a, int d, int n)
    {

        return Math.log((2 * a + (2 * n - 1) * d) /
                                 (2 * a - d)) / d;
    }

    public static void main(String args[])
    {
        int a = 12, d = 12, n = 5;
        int AP[] = new int[n + 5];

        // Generating AP from the above data
        double sum = generateAP(a, d, n, AP);

        // Generating HP from the generated AP
        System.out.println("Harmonic Progression :");
        for (int i = 1; i <= n; i++)
            System.out.print("1/" + AP[i] + " ");
        System.out.println();
        String str = "";
        str = str + sum;
        str = str.substring(0, 4);

        System.out.println("Sum of the generated" +
                  " harmonic progression : " + str);
        sum = sumApproximation(a, d, n);

        str = "";
        str = str + sum;
        str = str.substring(0, 4);
        System.out.println("Sum of the generated " +
           "harmonic progression using approximation : "
                                              + str);
    }
}
```

## 蟒蛇 3

```
# Python3 code to generate Harmonic Progression
# and calculate the sum of the progression.
import math

# Function that generates the harmonic
# progression and calculates the sum of
# its elements by iterating.
n = 5;
AP = [0] * (n + 5);

def generateAP(a, d, n):
    sum = 0;
    for i in range(1, n + 1):

        # HP = 1/AP
        # In AP, ith term is calculated
        # by a+(i-1)d;
        AP[i] = (a + (i - 1) * d);

        # Calculating the sum.
        sum += float(1) / float((a + (i - 1) * d));
    return sum;

# Function that uses riemenn sum method to calculate
# the approximate sum of HP in O(1) time complexity
def sumApproximation(a, d, n):

        return math.log((2 * a + (2 * n - 1) * d) /
                                 (2 * a - d)) / d;

# Driver Code
a = 12;
d = 12;
#n = 5;

# Generating AP from the above data
sum = generateAP(a, d, n);

# Generating HP from the generated AP
print("Harmonic Progression :");
for i in range(1, n + 1):
    print("1 /", AP[i], end = " ");
print("");
str1 = "";
str1 = str1 + str(sum);
str1 = str1[0:4];

print("Sum of the generated harmonic",
               "progression :", str1);
sum = sumApproximation(a, d, n);

str1 = "";
str1 = str1 + str(sum);
str1 = str1[0:4];
print("Sum of the generated harmonic",
      "progression using approximation :", str1);

# This code is contributed by mits    
```

## C#

```
// C# code to generate Harmonic
// Progression and calculate
// the sum of the progression.
using System;

class GFG
{
    // Function that generates
    // the harmonic progression
    // and calculates the sum of
    // its elements by iterating.
    static double generateAP(int a, int d,
                             int n, int []AP)
    {
        double sum = 0;
        for (int i = 1; i <= n; i++)
        {

            // HP = 1/AP
            // In AP, ith term is
            // calculated by a+(i-1)d;
            AP[i] = (a + (i - 1) * d);

            // Calculating the sum.
            sum += (double)1 /
                   (double)((a + (i - 1) * d));
        }
        return sum;
    }

    // Function that uses riemenn
    // sum method to calculate
    // the approximate sum of HP
    // in O(1) time complexity
    static double sumApproximation(int a,
                                   int d, int n)
    {

        return Math.Log((2 * a +
                        (2 * n - 1) * d) /
                        (2 * a - d)) / d;
    }

    // Driver code
    static void Main()
    {
        int a = 12, d = 12, n = 5;
        int []AP = new int[n + 5];

        // Generating AP from
        // the above data
        double sum = generateAP(a, d, n, AP);

        // Generating HP from
        // the generated AP
        Console.WriteLine("Harmonic Progression :");
        for (int i = 1; i <= n; i++)
            Console.Write("1/" + AP[i] + " ");
        Console.WriteLine();
        String str = "";
        str = str + sum;
        str = str.Substring(0, 4);

        Console.WriteLine("Sum of the generated" +
                " harmonic progression : " + str);
        sum = sumApproximation(a, d, n);

        str = "";
        str = str + sum;
        str = str.Substring(0, 4);
        Console.WriteLine("Sum of the generated " +
        "harmonic progression using approximation : "
                                            + str);
    }
}

// This code is contributed by
// ManishShaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to generate Harmonic Progression
// and calculate the sum of the progression.

    // Function that generates the harmonic progression
    // and calculates the sum of its elements by iterating.
    function generateAP($a, $d, $n, &$AP)
    {
        $sum = 0;
        for ($i = 1; $i <= $n; $i++) {

            // HP = 1/AP
            // In AP, ith term is calculated by a+(i-1)d;
            $AP[$i] = ($a + ($i - 1) * $d);

            // Calculating the sum.
            $sum += (double)1 / (double)(($a + ($i - 1) * $d));
        }
        return $sum;
    }

    // Function that uses riemenn sum method to calculate
    // the approximate sum of HP in O(1) time complexity
    function sumApproximation($a, $d, $n)
    {

        return log((2 * $a + (2 * $n - 1) * $d) /
                                (2 * $a - $d)) / $d;
    }

// Drive main
        $a = 12;
        $d = 12;
        $n = 5;
        $AP = array_fill(0,$n + 5,0);

        // Generating AP from the above data
        $sum = generateAP($a, $d, $n, $AP);

        // Generating HP from the generated AP
        echo "Harmonic Progression :\n";
        for ($i = 1; $i <= $n; $i++)
            echo "1/".$AP[$i]." ";
        echo "\n";
        $str = "";
        $str = $str.strval($sum);
        $str = substr($str,0, 4);

        echo "Sum of the generated".
                " harmonic progression : ".$str;
        $sum = sumApproximation($a, $d, $n);

        $str = "";
        $str = $str + strval($sum);
        $str = substr($str,0, 4);
        echo "\nSum of the generated ".
        "harmonic progression using approximation : ".$str;

// this code is contributed by mits                                           
?>
```

## java 描述语言

```
<script>

// JavaScript code to generate Harmonic Progression
// and calculate the sum of the progression.

    // Function that generates the harmonic progression
    // and calculates the sum of its elements by iterating.
    function generateAP(a, d, n, AP)
    {
        let sum = 0;
        for (let i = 1; i <= n; i++) {

            // HP = 1/AP
            // In AP, ith term is calculated by a+(i-1)d;
            AP[i] = (a + (i - 1) * d);

            // Calculating the sum.
            sum += 1 / ((a + (i - 1) * d));
        }
        return sum;
    }

    // Function that uses riemenn sum method to calculate
    // the approximate sum of HP in O(1) time complexity
    function sumApproximation(a, d, n)
    {

        return Math.log((2 * a + (2 * n - 1) * d) /
                                 (2 * a - d)) / d;
    }

// Driver code   

        let a = 12, d = 12, n = 5;
        let AP = [];

        // Generating AP from the above data
        let sum = generateAP(a, d, n, AP);

        // Generating HP from the generated AP
        document.write("Harmonic Progression :" + "<br/>");
        for (let i = 1; i <= n; i++)
            document.write("1/" + AP[i] + " ");
        document.write("<br/>");
        let str = "";
        str = str + sum;
        str = str.substring(0, 4);

        document.write("Sum of the generated" +
                  " harmonic progression : " + str + "<br/>");
        sum = sumApproximation(a, d, n);

        str = "";
        str = str + sum;
        str = str.substring(0, 4);
        document.write("Sum of the generated " +
           "harmonic progression using approximation : "
                                              + str + "<br/>");

</script>
```

**输出:**

```
Harmonic Progression :
1/12 1/24 1/36 1/48 1/60 
Sum of the generated harmonic progression : 0.19
Sum of the generated harmonic progression using approximation :0.19
```