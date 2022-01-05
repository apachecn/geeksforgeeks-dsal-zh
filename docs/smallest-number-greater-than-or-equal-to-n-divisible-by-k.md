# 大于或等于可被 K 整除的 N 的最小数

> 原文:[https://www . geesforgeks . org/最小数大于或等于 n 可被 k 整除/](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-n-divisible-by-k/)

给定一个数 N 和一个数 K，任务是找出大于或等于 N 的最小的可被 K 整除的数
**例:**

```
Input: N = 45, K = 6
Output: 48
48 is the smallest number greater than or equal to 45
which is divisible by 6.

Input: N = 11, K = 3
Output: 12
```

**方法:**思路是 N+K 除以 K，余数为 0 则打印 **N** 否则打印**N+K–余数**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest number
// greater than or equal to N
// that is divisible by k
int findNum(int N, int K)
{
    int rem = (N + K) % K;

    if (rem == 0)
        return N;
    else
        return N + K - rem;
}

// Driver code
int main()
{
    int N = 45, K = 6;

    cout << "Smallest number greater than or equal to " << N
         << "\nthat is divisible by " << K << " is " << findNum(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG{

    // Function to find the smallest number
    // greater than or equal to N
    // that is divisible by k
    static int findNum(int N, int K)
    {
        int rem = (N + K) % K;

        if (rem == 0)
            return N;
        else
            return N + K - rem;
    }

     // Driver Code
     public static void main(String []args){

        int N = 45, K = 6;

    System.out.println("Smallest number greater than or equal to " + N
          +"\nthat is divisible by " + K + " is " + findNum(N, K));

     }
     // This code is contributed by ANKITRAI1
}
```

## 计算机编程语言

```
# Python 3 implementation of the
# above approach

# Function to find the smallest number
# greater than or equal to N
# that is divisible by k
def findNum(N, K):
    rem = (N + K) % K;

    if (rem == 0):
        return N
    else:
        return (N + K - rem)

# Driver Code
N = 45
K = 6
print('Smallest number greater than',
                   'or equal to' , N,
           'that is divisible by', K,
               'is' , findNum(45, 6))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the above approach

public class GFG{

    // Function to find the smallest number
    // greater than or equal to N
    // that is divisible by k
    static int findNum(int N, int K)
    {
        int rem = (N + K) % K;

        if (rem == 0)
            return N;
        else
            return N + K - rem;
    }

    // Driver Code
    static void Main(){

        int N = 45, K = 6;

    System.Console.WriteLine("Smallest number greater than or equal to " + N
        +"\nthat is divisible by " + K + " is " + findNum(N, K));

    }
    // This code is contributed by mits
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the smallest number
// greater than or equal to N that is
// divisible by k
function findNum($N, $K)
{
    $rem = ($N + $K) % $K;

    if ($rem == 0)
        return $N;
    else
        return $N + $K - $rem;
}

// Driver code
$N = 45; $K = 6;

echo "Smallest number greater than " .
                   "or equal to ", $N;
echo "\nthat is divisible by " , $K ,
            " is " , findNum($N, $K);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// javascript implementation of the above approach

// Function to find the smallest number
    // greater than or equal to N
    // that is divisible by k
    function findNum(N , K)
    {
        var rem = (N + K) % K;

        if (rem == 0)
            return N;
        else
            return N + K - rem;
    }   
// Driver Code

var N = 45, K = 6;

document.write("Smallest number greater than or equal to " + N
  +"<br>that is divisible by " + K + " is " + findNum(N, K));

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
Smallest number greater than or equal to 45
that is divisible by 6 is 48
```