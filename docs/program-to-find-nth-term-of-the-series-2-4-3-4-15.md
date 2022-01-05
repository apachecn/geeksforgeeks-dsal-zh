# 程序寻找数列 2，4，3，4，15 的第 n 项…

> 原文:[https://www . geesforgeks . org/program-to-find-第 n 个系列术语-2-4-3-4-15/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-the-series-2-4-3-4-15/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

```
2, 4, 3, 4, 15...
```

**例:**

```
Input: N = 5
Output: 15
Explanation:
For N = 5,
Nth term = ( N * ( (N%2) + (N%3) ) 
         = ( 5 * ( (5%2) + (5%3) ) 
         = ( 5 * ( 1 + 2 )
         = 15

Input: N = 4 
Output: 4
```

**本系列广义第 n 项:**

```
Nth term = ( N * ( (N%2) + (N%3) ) )
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 2, 4, 3, 4, 15...

#include <iostream>
using namespace std;

// function to calculate Nth term of series
int nthTerm(int N)
{
    // By using above formula
    return (N * ((N % 2) + (N % 3)));
}

// Driver Function
int main()
{

    // get the value of N
    int N = 5;

    // Calculate and print the Nth term
    cout << "Nth term for N = "
         << N << " : "
         << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

// Class to calculate Nth term of series
class Nth {
    public int nthTerm(int N)
    {
        // By using above formula
        return (N * ((N % 2) + (N % 3)));
    }
}

// Main class for main method
class GFG {

    public static void main(String[] args)
    {

        // get the value of N
        int N = 5;

        // create object of Class Nth
        Nth a = new Nth();

        // Calculate and print the Nth term
        System.out.println("Nth term for N = "
                           + N + " : "
                           + a.nthTerm(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find N-th term of the series:
# 2, 4, 3, 4, 15...

# function to calculate Nth term of series
def nthTerm( N):

    # By using above formula
    return (N * ((N % 2) + (N % 3)))

# Driver Function

# get the value of N
if __name__=='__main__':
    N = 5

    # Calculate and print the Nth term
    print("Nth term for N = ", N , " : ",nthTerm(N))

# This code is contributed by ash264
```

## C#

```
// C# program to find
// N-th term of the series:
// 2, 4, 3, 4, 15...
using System;

class GFG
{
public int nthTerm(int N)
{
    // By using above formula
    return (N * ((N % 2) + (N % 3)));
}

public static void Main()
{

    // get the value of N
    int N = 5;

    GFG a = new GFG();

    // Calculate and print the Nth term
    Console.Write("Nth term for N = " +
                            N + " : " +
                         a.nthTerm(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term of the series:
// 2, 4, 3, 4, 15...

function nthTerm($N)
{
    return ($N * (($N % 2) + ($N % 3)));
}

// Driver code
$N = 5 ;

echo "Nth term for N = " . $N .
          " : " . nthTerm($N) ;

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>
// JavaScript program to find N-th term of the series:
// 2, 4, 3, 4, 15...

// function to calculate Nth term of series
function nthTerm( N)
{
    // By using above formula
    return (N * ((N % 2) + (N % 3)));
}

// Driver Function

    // get the value of N
    let N = 5;

    // Calculate and print the Nth term
    document.write( "Nth term for N = "
         + N +" : "
         + nthTerm(N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
Nth term for N = 5 : 15
```

**时间复杂度** : O(1)