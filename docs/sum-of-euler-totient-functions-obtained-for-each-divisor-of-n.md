# 对于 N 的每个除数获得的欧拉全能性函数的和

> 原文:[https://www . geeksforgeeks . org/欧拉全能性函数之和-n 的每个除数获得/](https://www.geeksforgeeks.org/sum-of-euler-totient-functions-obtained-for-each-divisor-of-n/)

给定一个正整数 **N** ，任务是求给定数 **N** 的所有[除数的](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function-for-all-numbers-smaller-than-or-equal-to-n/)的和。

***例:***

> ***输入:** N = 3*
> ***输出:** 3*
> ***解释:***
> *3 的除数为{1，3}。值 1 和 3 的欧拉全能函数分别为 1 和 2。*
> *因此，要求的和为 1 + 2 = 3。*
> 
> ***输入:**N = 6*
> T5**输出:** 6

**天真法:**给定的问题可以通过[求出**N**T5 的所有除数，然后打印出每个除数的](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)的值之和作为结果来解决。

***时间复杂度:** O(N * sqrt(N))*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以利用欧拉全能函数的性质进行优化，该性质规定所有除数的[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)的所有值之和为 **N** 。

因此 **N** 的欧拉全能函数的所有值之和就是数本身。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find the sum of Euler
// Totient Function of divisors of N
int sumOfDivisors(int N)
{
    // Return the value of N
    return N;
}

// Driver Code
int main()
{
    int N = 5;
    cout << sumOfDivisors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the sum of Euler
    // Totient Function of divisors of N
    static int sumOfDivisors(int N)
    {
        // Return the value of N
        return N;
    }
    // Driver code
    public static void main(String[] args)
    {
        int N = 5;
        System.out.println(sumOfDivisors(N));
    }
}
// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of Euler
# Totient Function of divisors of N
def sumOfDivisors(N):

    # Return the value of N
    return N

# Driver Code
if __name__ == '__main__':

    N = 5

    print (sumOfDivisors(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find the sum of Euler
    // Totient Function of divisors of N
    static int sumOfDivisors(int N)
    {
        // Return the value of N
        return N;
    }

// Driver code
static void Main()
{
     int N = 5;
     Console.Write(sumOfDivisors(N));

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Js program for the above approach

    // Function to find the sum of Euler
    // Totient Function of divisors of N
    function sumOfDivisors(N){

        // Return the value of N
        return N;
    }

    // Driver Code
    let N = 5;
    document.write(sumOfDivisors(N));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)