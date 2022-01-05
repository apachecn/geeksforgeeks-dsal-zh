# K-斐波那契数列

> 原文:[https://www.geeksforgeeks.org/k-fibonacci-series/](https://www.geeksforgeeks.org/k-fibonacci-series/)

给定整数‘K’和‘N’，任务是找到 K-斐波那契数列的第 N 项。

> 在 K–斐波那契数列中，第一个“K”项将是“1”，之后该数列的每个“I”项将是同一数列中前“K”个元素的总和。

**例:**

```
Input: N = 4, K = 2
Output: 3
The K-Fibonacci series for K=2 is 1, 1, 2, 3, ...
And, the 4th element is 3.

Input: N = 5, K = 6
Output: 1
The K-Fibonacci series for K=6 is 1, 1, 1, 1, 1, 1, 6, 11, ...
```

**简单的方法:**

*   首先，将第一个“K”元素初始化为“1”。
*   然后，通过运行从“i-k”到“i-1”的循环来计算先前“K”元素的总和。
*   将 ith 值设置为总和。

**时间复杂度:** O(N*K)
**高效的方法:**

*   首先，将第一个“K”元素初始化为“1”。
*   创建一个名为“sum”的变量，该变量将用“K”初始化。
*   将第(K+1)个元素的值设置为和。
*   将下一个值设置为 Array[I]= sum–Array[I-k-1]+Array[I-1]，然后更新 sum = Array[i]。
*   最后，显示数组的第 n 项。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the Nth
// element of K-Fibonacci series
void solve(int N, int K)
{
    vector<long long int> Array(N + 1, 0);

    // If N is less than K
    // then the element is '1'
    if (N <= K) {
        cout << "1" << endl;
        return;
    }

    long long int i = 0, sum = K;

    // first k elements are 1
    for (i = 1; i <= K; ++i) {
        Array[i] = 1;
    }

    // (K+1)th element is K
    Array[i] = sum;

    // find the elements of the
    // K-Fibonacci series
    for (int i = K + 2; i <= N; ++i) {

        // subtract the element at index i-k-1
        // and add the element at index i-i
        // from the sum (sum contains the sum
        // of previous 'K' elements )
        Array[i] = sum - Array[i - K - 1] + Array[i - 1];

        // set the new sum
        sum = Array[i];
    }
    cout << Array[N] << endl;
}

// Driver code
int main()
{
    long long int N = 4, K = 2;

    // get the Nth value
    // of K-Fibonacci series
    solve(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

public class GFG {

    // Function that finds the Nth
    // element of K-Fibonacci series
    static void solve(int N, int K)
    {
        int Array[] = new int[N + 1];

        // If N is less than K
        // then the element is '1'
        if (N <= K) {
            System.out.println("1") ;
            return;
        }

        int i = 0 ;
        int sum = K;

        // first k elements are 1
        for (i = 1; i <= K; ++i) {
            Array[i] = 1;
        }

        // (K+1)th element is K
        Array[i] = sum;

        // find the elements of the
        // K-Fibonacci series
        for (i = K + 2; i <= N; ++i) {

            // subtract the element at index i-k-1
            // and add the element at index i-i
            // from the sum (sum contains the sum
            // of previous 'K' elements )
            Array[i] = sum - Array[i - K - 1] + Array[i - 1];

            // set the new sum
            sum = Array[i];
        }
        System.out.println(Array[N]);
    }

    public static void main(String args[])
    {
          int N = 4, K = 2;

            // get the Nth value
            // of K-Fibonacci series
            solve(N, K);

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function that finds the Nth
# element of K-Fibonacci series
def solve(N, K) :
    Array = [0] * (N + 1)

    # If N is less than K
    # then the element is '1'
    if (N <= K) :
        print("1")
        return

    i = 0
    sm = K

    # first k elements are 1
    for i in range(1, K + 1) :
        Array[i] = 1

    # (K+1)th element is K
    Array[i + 1] = sm

    # find the elements of the
    # K-Fibonacci series
    for i in range(K + 2, N + 1) :

        # subtract the element at index i-k-1
        # and add the element at index i-i
        # from the sum (sum contains the sum
        # of previous 'K' elements )
        Array[i] = sm - Array[i - K - 1] + Array[i - 1]

        # set the new sum
        sm = Array[i]

    print(Array[N])

# Driver code
N = 4
K = 2

# get the Nth value
# of K-Fibonacci series
solve(N, K)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    // Function that finds the Nth
    // element of K-Fibonacci series
    public static void solve(int N, int K)
    {
        int[] Array = new int[N + 1];

        // If N is less than K
        // then the element is '1'
        if (N <= K)
        {
            Console.WriteLine("1");
            return;
        }

        int i = 0;
        int sum = K;

        // first k elements are 1
        for (i = 1; i <= K; ++i)
        {
            Array[i] = 1;
        }

        // (K+1)th element is K
        Array[i] = sum;

        // find the elements of the
        // K-Fibonacci series
        for (i = K + 2; i <= N; ++i)
        {

            // subtract the element at index i-k-1
            // and add the element at index i-i
            // from the sum (sum contains the sum
            // of previous 'K' elements )
            Array[i] = sum - Array[i - K - 1] +
                                 Array[i - 1];

            // set the new sum
            sum = Array[i];
        }
        Console.WriteLine(Array[N]);
    }

    // Main Method
    public static void Main(string[] args)
    {
        int N = 4, K = 2;

            // get the Nth value
            // of K-Fibonacci series
            solve(N, K);

    }

}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that finds the Nth
// element of K-Fibonacci series
function solve($N, $K)
{
    $Array = array_fill(0, $N + 1, NULL);

    // If N is less than K
    // then the element is '1'
    if ($N <= $K)
    {
        echo "1" ."\n";
        return;
    }

    $i = 0;
    $sum = $K;

    // first k elements are 1
    for ($i = 1; $i <= $K; ++$i)
    {
        $Array[$i] = 1;
    }

    // (K+1)th element is K
    $Array[$i] = $sum;

    // find the elements of the
    // K-Fibonacci series
    for ($i = $K + 2; $i <= $N; ++$i)
    {

        // subtract the element at index i-k-1
        // and add the element at index i-i
        // from the sum (sum contains the sum
        // of previous 'K' elements )
        $Array[$i] = $sum - $Array[$i - $K - 1] +
                            $Array[$i - 1];

        // set the new sum
        $sum = $Array[$i];
    }
    echo $Array[$N] . "\n";
}

// Driver code
$N = 4;
$K = 2;

// get the Nth value
// of K-Fibonacci series
solve($N, $K);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

//Javascript program to find
// next greater number than N

// Function that finds the Nth
// element of K-Fibonacci series
function solve(N, K)
{
    var Arr = new Array(N + 1);

    // If N is less than K
    // then the element is '1'
    if (N <= K) {
       document.write( "1" + "<br>");
        return;
    }

    var i = 0, sum = K;

    // first k elements are 1
    for (i = 1; i <= K; ++i) {
        Arr[i] = 1;
    }

    // (K+1)th element is K
    Arr[i] = sum;

    // find the elements of the
    // K-Fibonacci series
    for (var i = K + 2; i <= N; ++i) {

        // subtract the element at index i-k-1
        // and add the element at index i-i
        // from the sum (sum contains the sum
        // of previous 'K' elements )
        Arr[i] = sum - Arr[i - K - 1] + Arr[i - 1];

        // set the new sum
        sum = Arr[i];
    }
    document.write( Arr[N] + "<br>");
}

var N = 4, K = 2;

    // get the Nth value
    // of K-Fibonacci series
    solve(N, K);

// This code is contributed bby SoumikMondal

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)