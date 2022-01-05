# 素性测试|第 5 集(使用卢卡斯-莱默系列)

> 原文:[https://www . geesforgeks . org/primality-test-set-5 using-Lucas-lehmer-series/](https://www.geeksforgeeks.org/primality-test-set-5using-lucas-lehmer-series/)

在本文中，我们将讨论 Lucas-Lehmer 级数，该级数用于检查形式 2<sup>p</sup>–1 的素数的素性，其中 p 是整数。
首先，我们来看看什么是 Lucas-Lehmer 系列。
卢卡斯-莱默系列可以表示为:

![\[s_i = \left \{ \begin{tabular}{c} 4 \hspace{1.4cm} when i = 0; \\ s_{i-1}^2 - 2 \hspace{.5cm} otherwise. \end{tabular} \]       ](img/914d1aa847764cd03e7b831eeb16b12f.png "Rendered by QuickLaTeX.com")

因此该系列为:
项 0: 4、
项 1:4 * 4–2 = 14、
项 2:14 * 14–2 = 194、
项 3:194 * 194–2 = 37634、
项 4:37634 * 37634–2 = 1416317954、……等等。
下面是找出卢卡斯-莱默系列前 n 个术语的程序。

## C++

```
// C++ program to find out Lucas-Lehmer series.
#include <iostream>
#include <vector>
using namespace std;

// Function to find out first n terms
// (considering 4 as 0th term) of
// Lucas-Lehmer series.
void LucasLehmer(int n) {

  // the 0th term of the series is 4.
  unsigned long long current_val = 4;

  // create an array to store the terms.
  vector<unsigned long long> series;

  // compute each term and add it to the array.
  series.push_back(current_val);
  for (int i = 0; i < n; i++) {
    current_val = current_val * current_val - 2;
    series.push_back(current_val);
  }

  // print out the terms one by one.
  for (int i = 0; i <= n; i++)
    cout << "Term " << i << ": "
        << series[i] << endl; 
}

// Driver program
int main() {
  int n = 5;
  LucasLehmer(n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out
// Lucas-Lehmer series.
import java.util.*;

class GFG
{

    // Function to find out
    // first n terms(considering
    // 4 as 0th term) of Lucas-
    // Lehmer series.
    static void LucasLehmer(int n)
    {

        // the 0th term of
        // the series is 4.
        long current_val = 4;

        // create an array
        // to store the terms.
        ArrayList<Long> series = new ArrayList<>();

         // compute each term
        // and add it to the array.
        series.add(current_val);
        for (int i = 0; i < n; i++)
        {
            current_val = current_val
                    * current_val - 2;
            series.add(current_val);
        }

        // print out the
       // terms one by one.
        for (int i = 0; i <= n; i++)
        {
            System.out.println("Term " + i
                    + ": " + series.get(i));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int n = 5;
        LucasLehmer(n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find out Lucas-Lehmer series.

# Function to find out first n terms
# (considering 4 as 0th term) of
# Lucas-Lehmer series.
def LucasLehmer(n):

  # the 0th term of the series is 4.
  current_val = 4;

  # create an array to store the terms.
  series = []

  # compute each term and add it to the array.
  series.append(current_val)

  for i in range(n):
    current_val = current_val * current_val - 2;
    series.append(current_val);

  # print out the terms one by one.
  for i in range(n + 1):
      print("Term", i, ":", series[i])

# Driver program
if __name__=='__main__':

  n = 5;
  LucasLehmer(n);

# This code is contributed by pratham76.
```

## C#

```
// C# program to find out
// Lucas-Lehmer series.
using System;
using System.Collections.Generic;

class GFG
{

// Function to find out
// first n terms(considering
// 4 as 0th term) of Lucas-
// Lehmer series.
static void LucasLehmer(int n)
{

// the 0th term of
// the series is 4.
long current_val = 4;

// create an array
// to store the terms.
List<long> series = new List<long>();

// compute each term
// and add it to the array.
series.Add(current_val);
for (int i = 0; i < n; i++)
{
    current_val = current_val *
                  current_val - 2;
    series.Add(current_val);
}

// print out the
// terms one by one.
for (int i = 0; i <= n; i++)
    Console.WriteLine("Term " + i +
                      ": " + series[i]);
}

// Driver Code
static void Main()
{
    int n = 5;
    LucasLehmer(n);
}
}

// This code is contributed by
// ManishShaw(manishshaw1)
```

## java 描述语言

```
<script>
// Javascript program to find out
// Lucas-Lehmer series.

// Function to find out
    // first n terms(considering
    // 4 as 0th term) of Lucas-
    // Lehmer series.
function LucasLehmer(n)
{

    // the 0th term of
        // the series is 4.
        let current_val = 4;

        // create an array
        // to store the terms.
        let series = [];

         // compute each term
        // and add it to the array.
        series.push(current_val);
        for (let i = 0; i < n; i++)
        {
            current_val = (current_val
                    * current_val) - 2;
            series.push(current_val);
        }

        // print out the
       // terms one by one.
        for (let i = 0; i <= n; i++)
        {
            document.write("Term " + i
                    + ": " + series[i]+"<br>");
        }
}

// Driver Code
let n = 5;
LucasLehmer(n);

// This code is contributed by rag2127
</script>
```

**输出:**

```
Term 0: 4
Term 1: 14
Term 2: 194
Term 3: 37634
Term 4: 1416317954
Term 5: 2005956546822746114
```

我们可以用字符串来存储数列的大数字。
**现在****这个 Lucas-Lehmer 系列和质数有什么关系？**

> 1.首先，我们只能检查那些我们可以表示为，x =(2<sup>p</sup>–1)的数的素性，其中 p 是整数。
> 2。现在我们要找出卢卡斯-莱默系列的第(p-1)项。
> 3。如果这个项是 x 的倍数，那么 x 就是质数。
> 4。当 x 很大，即 p 很大时，我们可能很难求出级数的第(p-1)项。
> 不如说我们能做什么:
> 1。从第 0 项开始计算 Lucas-Lehmer 级数，而是存储整个项，只存储 s[i]%x(即以 x 为模的项)。
> 2。使用前一项计算该修改系列的下一个数字。s[I]=(s[I-1]<sup>2</sup>–2)% x .
> 3。计算到第(p-1)项。
> 4。如果第(p-1)项是 0，那么 x 是素数，否则不是。因此，s[p-1]必须为 0 才能成为 x =(2<sup>p</sup>–1)质数。

示例:

```
Is 2^7 - 1 = 127 is a prime?
        so here x = 127, p = 7-1 = 6.
        Hence the modified Lucas-Lehmer series is:
        term 1: 4,
        term 2: (4*4 - 2) % 127 = 14,
        term 3: (14*14 - 2) % 127 = 67,
        term 4: (67*67 - 2) % 127 = 42,
        term 5: (42*42 - 2) % 127 = 111,
        term 6: (111*111) % 127 = 0.
        Here the 6th term is 0 so 127 is a prime number.
```

**检查 2^p-1 是否为质数的代码**

## C++

```
// CPP program to check for primality using
// Lucas-Lehmer series.
#include <cmath>
#include <iostream>
using namespace std;

// Function to check whether (2^p - 1)
// is prime or not.
bool isPrime(int p) {

  // generate the number
  long long checkNumber = pow(2, p) - 1;

  // First number of the series
  long long nextval = 4 % checkNumber;

  // Generate the rest (p-2) terms
  // of the series.
  for (int i = 1; i < p - 1; i++)
    nextval = (nextval * nextval - 2) % checkNumber; 

  // now if the (p-1)th term is
  // 0 return true else false.
  return (nextval == 0);
}

// Driver Program
int main() {
  // Check whether 2^p-1 is prime or not.
  int p = 7;

  long long checkNumber = pow(2, p) - 1;

  if (isPrime(p))
    cout << checkNumber << " is Prime.";
  else
    cout << checkNumber << " is not Prime.";

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check for primality using
// Lucas-Lehmer series.

class GFG{
// Function to check whether (2^p - 1)
// is prime or not.
static boolean isPrime(int p) {

// generate the number
double checkNumber = Math.pow(2, p) - 1;

// First number of the series
double nextval = 4 % checkNumber;

// Generate the rest (p-2) terms
// of the series.
for (int i = 1; i < p - 1; i++)
    nextval = (nextval * nextval - 2) % checkNumber;

// now if the (p-1)th term is
// 0 return true else false.
return (nextval == 0);
}

// Driver Program
public static void main(String[] args) {
// Check whether 2^p-1 is prime or not.
int p = 7;
double checkNumber = Math.pow(2, p) - 1;

if (isPrime(p))
    System.out.println((int)checkNumber+" is Prime.");
else
    System.out.println((int)checkNumber+" is not Prime.");

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 Program to check for primality
# using Lucas-Lehmer series.

# Function to check whether (2^p - 1)
# is prime or not.
def isPrime(p):

    # generate the number
    checkNumber = 2 ** p - 1

    # First number of the series
    nextval = 4 % checkNumber

    # Generate the rest (p-2) terms
    # of the series
    for i in range(1, p - 1):
        nextval = (nextval * nextval - 2) % checkNumber

    # now if the (p-1) the term is
    # 0 return true else false.
    if (nextval == 0): return True
    else: return False

# Driver Code

# Check whetherr 2^(p-1)
# is prime or not.
p = 7
checkNumber = 2 ** p - 1

if isPrime(p):
    print(checkNumber, 'is Prime.')
else:
    print(checkNumber, 'is not Prime')

# This code is contributed by egoista.
```

## C#

```
// C# program to check for primality using
// Lucas-Lehmer series.
using System;

class GFG{
// Function to check whether (2^p - 1)
// is prime or not.
static bool isPrime(int p) {

// generate the number
double checkNumber = Math.Pow(2, p) - 1;

// First number of the series
double nextval = 4 % checkNumber;

// Generate the rest (p-2) terms
// of the series.
for (int i = 1; i < p - 1; i++)
    nextval = (nextval * nextval - 2) % checkNumber;

// now if the (p-1)th term is
// 0 return true else false.
return (nextval == 0);
}

// Driver Program
static void Main() {
// Check whether 2^p-1 is prime or not.
int p = 7;
double checkNumber = Math.Pow(2, p) - 1;

if (isPrime(p))
    Console.WriteLine((int)checkNumber+" is Prime.");
else
    Console.WriteLine((int)checkNumber+" is not Prime.");

}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check for
// primality using Lucas-
// Lehmer series.

// Function to check whether
/// (2^p - 1) is prime or not.
function isPrime($p)
{

    // generate the number
        $checkNumber = pow(2, $p) - 1;

    // First number of the series
        $nextval = 4 % $checkNumber;

    // Generate the rest (p-2) terms
    // of the series.
    for ($i = 1; $i < $p - 1; $i++)
        $nextval = ($nextval * $nextval - 2) %
                                 $checkNumber;

    // now if the (p-1)th term is
    // 0 return true else false.
    return ($nextval == 0);
}

    // Driver Code
    // Check whether 2^p-1 is
    // prime or not.
    $p = 7;
    $checkNumber = pow(2, $p) - 1;
    if (isPrime($p))
        echo $checkNumber , " is Prime.";
    else
        echo $checkNumber , " is not Prime.";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check for primality using
    // Lucas-Lehmer series.

    // Function to check whether (2^p - 1)
    // is prime or not.
    function isPrime(p) {

        // generate the number
        let checkNumber = Math.pow(2, p) - 1;

        // First number of the series
        let nextval = 4 % checkNumber;

        // Generate the rest (p-2) terms
        // of the series.
        for (let i = 1; i < p - 1; i++)
            nextval = (nextval * nextval - 2) % checkNumber;

        // now if the (p-1)th term is
        // 0 return true else false.
        return (nextval == 0);
    }

    // Check whether 2^p-1 is prime or not.
    let p = 7;
    let checkNumber = Math.pow(2, p) - 1;

    if (isPrime(p))
        document.write(checkNumber+" is Prime.");
    else
        document.write(checkNumber+" is not Prime.");

</script>
```

**输出:**

```
127 is Prime.
```

撰写本文时最大的素数是(2^(77232917)–1(发现于 2017-12-26)。它有 23249425 个数字。这些质数的发现方式与上面讨论的相同。要找出这种大素数，需要巨大的计算能力和几个月的处理。
一个有趣的事实是，为了检查这么多大质数，p 也取质数。在处理之后，如果它发现数字 x 不是质数，那么 p 被作为下一个质数，并且运行相同的过程。