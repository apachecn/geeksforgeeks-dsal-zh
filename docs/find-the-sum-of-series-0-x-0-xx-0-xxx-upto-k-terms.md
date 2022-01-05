# 求数列 0 的和。X + 0。XX + 0。XXX +…最多 k 个条款

> 原文:[https://www . geesforgeks . org/find-the-sum-series-0-x-0-xx-0-XXX-up-k-terms/](https://www.geeksforgeeks.org/find-the-sum-of-series-0-x-0-xx-0-xxx-upto-k-terms/)

给定一系列 k 项，其中“X”是 0-9 之间的任何值，“k”是任何正整数。任务是求给定数列的和:

> 0.X + 0。XX + 0。XXX +…最多“k”个术语

**示例** :

```
Input: x = 4 , k = 10
Output : 4.39506

Input: x = 9 , k = 20
Output: 19.8889
```

**解说:**
![$ Result = 0.x + 0.xx + 0.xxx + ...\, up\, to\, k\, terms\\ = x/9(0.9 + 0.99 + 0.999 +... up \, to\, k\, terms)\\ = x/9[(1 - 0.1) + (1 - 0.01) + (1-0.001) + ...\, up\, \, to \, k\, terms]\\ = x/9[(1 + 1 + 1... \, upto\, k \, terms) - (1/10 + 1/100 + 1/1000 + ...\, upto\, k \, terms)]\\ = x/9[n - 0.1 * (1 - (0.1)^k)/(1 - 0.1)]\\ = x/81[9k - 1 + (10)^{-n}]\\ $  ](img/766e52cbf6fe9f669dfd15e6c93a45d0.png "Rendered by QuickLaTeX.com")

## C++

```
// C++ program for sum of the series
// 0.x,  0.xx, 0.xxx, ... upto k terms
#include <bits/stdc++.h>
using namespace std;

// function which return the sum of series
float sumOfSeries(int x, int k)
{
    return (float(x) / 81) * (9 * k - 1 + pow(10, (-1) * k));
}

// Driver code
int main()
{
    int x = 9;
    int k = 20;
    cout << sumOfSeries(x, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for sum of the series
// 0.x,  0.xx, 0.xxx, ... upto k terms

public class GFG {

    // function which return the sum of series
    static float sumOfSeries(int x, int k)
    {
       float y = (float) (((float)(x) / 81) * (9 * k - 1 + Math.pow(10, (-1) * k)));
       return y ;
    }

    // Driver code
    public static void main (String args[]){
         int x = 9;
         int k = 20;
         System.out.println(sumOfSeries(x, k));
    }

// This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
#Python3 program for sum of series
#0.x, 0.xx, 0.xxx, ... upto k terms

#function which return the sum of series
def sumOfSeries(x, k):

    return (float(x)/81) * (9 * k - 1 + 10**( (-1)*k ) )

#Driver code
if __name__=='__main__':
    x = 9
    k = 20
    print(sumOfSeries(x, k))
# This code is contributed by Shashank Sharma
```

## C#

```
// C# program for sum of the series
// 0.x, 0.xx, 0.xxx, ... upto k terms
using System;

class GFG
{

// function which return
// the sum of series
static float sumOfSeries(int x, int k)
{
    float y = (float)(((float)(x) / 81) *
              (9 * k - 1 + Math.Pow(10, (-1) * k)));
    return y ;
}

// Driver code
public static void Main ()
{
    int x = 9;
    int k = 20;
    Console.Write(sumOfSeries(x, k));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for sum of the series
// 0.x, 0.xx, 0.xxx, ... upto k terms

// function which return the
// sum of series
function sumOfSeries($x, $k)
{
    return (($x) / 81) * (9 * $k - 1 +
                      pow(10, (-1) * $k));
}

// Driver code
$x = 9;
$k = 20;
echo sumOfSeries($x, $k);

// This code is contributed
// by inder_verma.
?>
```

## java 描述语言

```
<script>

// javascript program for sum of the series
// 0.x,  0.xx, 0.xxx, ... upto k terms

// function which return the sum of series
function sumOfSeries(x , k)
{
   var y =  (((x) / 81) * (9 * k - 1 + Math.pow(10, (-1) * k)));
   return y ;
}

// Driver code

 var x = 9;
 var k = 20;
 document.write(sumOfSeries(x, k));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
19.8889
```