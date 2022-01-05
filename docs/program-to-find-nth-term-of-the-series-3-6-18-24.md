# 程序寻找系列 3，6，18，24 的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-series-3-6-18-24/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-the-series-3-6-18-24/)

给定一个数字 n，任务是编写一个程序来寻找下面系列中的第 n 项:

```
3, 6, 18, 24, 45, 54...(Nth term)
```

**例:**

```
Input: N = 5
Output: 45
Explanation:
For N = 5,
Nth term = ( N * ( (N/2) + ( (N%2) * 2) + N ) 
         = ( 5 * ( (5/2) + ( (5%2) * 2) + 5 ) 
         = ( 5 * ( 2 + ( 1 * 2) + 5 )
         = 45

Input : 6 
Output : 54
```

**本系列广义第 n 项:**

```
Nth term = ( N * ( (N/2) + ((N%2) * 2) + N )
```

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term of the series:
// 3, 6, 18, 24, 45, 54...

#include <iostream>
using namespace std;

// function to calculate Nth term of series
int nthTerm(int N)
{
    // By using above formula
    return (N * ((N / 2) + ((N % 2) * 2) + N));
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
        return (N * ((N / 2) + ((N % 2) * 2) + N));
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
# 3, 6, 18, 24, 45, 54...

# function to calculate Nth term of series
def nthTerm( N):
    # By using above formula
    return (N * ((N // 2) + ((N % 2) * 2) + N))

# Driver Function

# get the value of N
if __name__=='__main__':
    N = 5

    # Calculate and print the Nth term
    print( "Nth term for N = ", N ," : ", nthTerm(N))

# This code is contributed by ash264
```

## C#

```
// C# program to find N-th
// term of the series:
// 3, 6, 18, 24, 45, 54...
using System;

class GFG
{
public int nthTerm(int N)
{
    // By using above formula
    return (N * ((N / 2) +
           ((N % 2) * 2) + N));
}

// Driver Code
public static void Main()
{

    // get the value of N
    int N = 5;

    // create object of Class Nth
    GFG a = new GFG();

    // Calculate and print the Nth term
    Console.WriteLine("Nth term for N = " +
                                N + " : " +
                             a.nthTerm(N));
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find N-th term
// of the series: 3, 6, 18, 24, 45, 54...

// Function to calculate Nth term of series

function nthTerm($N)
{
    // By using abeove formula
    return ($N * ((int)($N / 2) +
          (($N % 2) * 2) + $N));
}

// Driver code

// get the value of nthTerm
$N = 5;

// Calculate and print the Nth term
echo "Nth term for N = ", $N,
     " : ", nthTerm($N);

// This code is contributed by
// Shashank_Sharma
?>
```

## java 描述语言

```
<script>
// JavaScript program to find N-th term of the series:
// 3, 6, 18, 24, 45, 54...

// function to calculate Nth term of series
function nthTerm( N)
{
    // By using above formula
    return parseInt(N * (parseInt(N / 2) + ((N % 2) * 2) + N));
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
Nth term for N = 5 : 45
```

**时间复杂度:** O(1)