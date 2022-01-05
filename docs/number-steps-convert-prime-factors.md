# 转换为质因数的步数

> 原文:[https://www . geesforgeks . org/number-steps-convert-prime-factors/](https://www.geeksforgeeks.org/number-steps-convert-prime-factors/)

给定 n 个正整数的数组 arr[]。将每个数字表示为它的因子(x * y = arr[i])[这里 x 或 y 不能是 1]，直到它不能进一步表示为 x * y = arr[I]。打印分割所需的步骤数，直到无法进一步表示。

**示例:**

```
Input: 4 4 4
Output: 3
Explanation: 1st step 2 2 4 4 . 
             2nd step 2 2 2 2 4 
             3rd step 2 2 2 2 2 2 

Input: 20 4 
Output: 3
Explanation: 1st step 20 2 2 (2*2 = 4)
             2nd step 2 10 2 2 (2*10 = 20)
             3rd step 2 2 5 2 2, (2*5 = 10)
```

方法是预先计算每个数的质因数。可以使用[筛的实现](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)有效地计算质因数，这需要 **N *对数 N.** 。我们知道一个数可以表示为它的质因数的乘积，我们可以表示它直到它不是 1，所以 1 不算在内，所以如果这个数不是 1，我们计算质因数的个数，然后从中减去 1。

## C++

```
// CPP program to count number of steps
// required to convert an integer array
// to array of factors.
#include <iostream>
using namespace std;

const int MAX = 1000001;

// array to store prime factors
int factor[MAX] = { 0 };

// function to generate all prime factors
// of numbers from 1 to 10^6
void cal_factor()
{
    factor[1] = 1;

    // Initializes all the positions with their value.
    for (int i = 2; i < MAX; i++)
        factor[i] = i;

    // Initializes all multiples of 2 with 2
    for (int i = 4; i < MAX; i += 2)
        factor[i] = 2;

    // A modified version of Sieve of Eratosthenes to
    // store the smallest prime factor that divides
    // every number.
    for (int i = 3; i * i < MAX; i++) {

        // check if it has no prime factor.
        if (factor[i] == i) {

            // Initializes of j starting from i*i
            for (int j = i * i; j < MAX; j += i) {

                // if it has no prime factor before, then
                // stores the smallest prime divisor
                if (factor[j] == j)
                    factor[j] = i;
            }
        }
    }
}

// function to calculate the number of representations
int no_of_representations(int a[], int n)
{
    // keep an count of prime factors
    int count = 0;

    // traverse for every element
    for (int i = 0; i < n; i++) {

        int temp = a[i];
        int flag = 0;

        // count the no of factors
        while (factor[temp] != 1) {
            flag = -1;
            count++;
            temp = temp / factor[temp];
        }

        // subtract 1 if Ai is not 1 as the last step
        // wont be taken into count
        count += flag;
    }

    return count;
}

// driver program to test the above function
int main()
{
    // call sieve to calculate the factors
    cal_factor();

    int a[] = { 4, 4, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << no_of_representations(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of steps
// required to convert an integer array
// to array of factors.

class GFG
{
    static final int MAX = 1000001;

    // array to store prime factors
    static int factor[] = new int[MAX];

    // function to generate all prime factors
    // of numbers from 1 to 10^6
    static void cal_factor() {
    factor[1] = 1;

    // Initializes all the positions
    // with their value.
    for (int i = 2; i < MAX; i++)
    factor[i] = i;

    // Initializes all multiples of 2 with 2
    for (int i = 4; i < MAX; i += 2)
    factor[i] = 2;

    // A modified version of Sieve of Eratosthenes to
    // store the smallest prime factor that divides
    // every number.
    for (int i = 3; i * i < MAX; i++) {

    // check if it has no prime factor.
    if (factor[i] == i) {

        // Initializes of j starting from i*i
        for (int j = i * i; j < MAX; j += i) {

        // if it has no prime factor before, then
        // stores the smallest prime divisor
        if (factor[j] == j)
            factor[j] = i;
        }
    }
    }
}

// function to calculate the
// number of representations
static int no_of_representations(int a[], int n) {

    // keep an count of prime factors
    int count = 0;

    // traverse for every element
    for (int i = 0; i < n; i++) {

    int temp = a[i];
    int flag = 0;

    // count the no of factors
    while (factor[temp] != 1) {
        flag = -1;
        count++;
        temp = temp / factor[temp];
    }

    // subtract 1 if Ai is not 1 as the
    // last step wont be taken into count
    count += flag;
    }

    return count;
}

// Driver code
public static void main(String[] args) {

    // call sieve to calculate the factors
    cal_factor();

    int a[] = {4, 4, 4};
    int n = a.length;

    System.out.print(no_of_representations(a, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to count number
# of steps required to convert an
# integer array to array of factors.
MAX = 1000001

# array to store prime factors
factor = [0] * MAX

# function to generate all prime
# factors of numbers from 1 to 10^6
def cal_factor():

    factor[1] = 1

    # Initializes all the positions
    # with their value.
    for i in range(2, MAX):
        factor[i] = i

    # Initializes all multiples
    # of 2 with 2
    for i in range(4, MAX, 2):
        factor[i] = 2

    # A modified version of Sieve of
    # Eratosthenes to store the smallest
    # prime factor that divides every number.
    i = 3
    while i * i < MAX:

        # check if it has no prime factor.
        if (factor[i] == i) :

            # Initializes of j starting
            # from i*i
            for j in range(i * i, MAX, i) :

                # if it has no prime factor
                # before, then stores the
                # smallest prime divisor
                if (factor[j] == j):
                    factor[j] = i

        i += 1

# function to calculate the
# number of representations
def no_of_representations(a, n):

    # keep an count of prime factors
    count = 0

    # traverse for every element
    for i in range(n) :

        temp = a[i]
        flag = 0

        # count the no of factors
        while (factor[temp] != 1) :
            flag = -1
            count += 1
            temp = temp // factor[temp]

        # subtract 1 if Ai is not 1 as the
        # last step wont be taken into count
        count += flag

    return count

# Driver Code
if __name__ == "__main__":

    # call sieve to calculate the factors
    cal_factor()

    a = [ 4, 4, 4 ]
    n = len(a)

    print(no_of_representations(a, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count number of steps
// required to convert an integer array
// to array of factors.
using System;

class GFG {

    static int MAX = 1000001;

    // array to store prime factors
    static int []factor = new int[MAX];

    // function to generate all prime
    // factors of numbers from 1 to 10^6
    static void cal_factor()
    {
        factor[1] = 1;

        // Initializes all the positions
        // with their value.
        for (int i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of
        // 2 with 2
        for (int i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the
        // smallest prime factor that
        // divides every number.
        for (int i = 3; i * i < MAX; i++)
        {

            // check if it has no prime
            // factor.
            if (factor[i] == i)
            {

                // Initializes of j
                // starting from i*i
                for (int j = i * i;
                           j < MAX; j += i)
                {

                    // if it has no prime
                    // factor before, then
                    // stores the smallest
                    // prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate the
    // number of representations
    static int no_of_representations(
                           int []a, int n)
    {

        // keep an count of prime factors
        int count = 0;

        // traverse for every element
        for (int i = 0; i < n; i++)
        {
            int temp = a[i];
            int flag = 0;

            // count the no of factors
            while (factor[temp] != 1)
            {
                flag = -1;
                count++;
                temp = temp / factor[temp];
            }

            // subtract 1 if Ai is not 1
            // as the last step wont be
            // taken into count
            count += flag;
        }

        return count;
    }

    // Driver code
    public static void Main()
    {

        // call sieve to calculate
        // the factors
        cal_factor();

        int []a = {4, 4, 4};
        int n = a.Length;

        Console.WriteLine(
            no_of_representations(a, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of steps
// required to convert an integer array
// to array of factors.

$MAX = 100001;

// array to store prime factors
$factor = array_fill(0, $MAX + 1, 0);

// function to generate all prime
// factors of numbers from 1 to 10^6
function cal_factor()
{
    global $factor, $MAX;
    $factor[1] = 1;

    // Initializes all the positions
    // with their value.
    for ($i = 2; $i < $MAX; $i++)
        $factor[$i] = $i;

    // Initializes all multiples of 2 with 2
    for ($i = 4; $i < $MAX; $i += 2)
        $factor[$i] = 2;

    // A modified version of Sieve of
    // Eratosthenes to store the smallest
    // prime factor that divides every number.
    for ($i = 3; $i * $i < $MAX; $i++)
    {

        // check if it has no prime factor.
        if ($factor[$i] == $i)
        {

            // Initializes of j starting from i*i
            for ($j = $i * $i; $j < $MAX; $j += $i)
            {

                // if it has no prime factor before, then
                // stores the smallest prime divisor
                if ($factor[$j] == $j)
                    $factor[$j] = $i;
            }
        }
    }
}

// function to calculate the
// number of representations
function no_of_representations($a, $n)
{
    global $factor, $MAX;

    // keep an count of prime factors
    $count = 0;

    // traverse for every element
    for ($i = 0; $i < $n; $i++)
    {

        $temp = $a[$i];
        $flag = 0;

        // count the no of factors
        while ($factor[$temp] != 1) {
            $flag = -1;
            $count++;
            $temp = (int)($temp / $factor[$temp]);
        }

        // subtract 1 if Ai is not 1 as the
        // last step wont be taken into count
        $count += $flag;
    }

    return $count;
}

// Driver Code

// call sieve to calculate the factors
cal_factor();

$a = array( 4, 4, 4 );
$n = count($a);

echo no_of_representations($a, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of steps
// required to convert an integer array
// to array of factors.
let MAX = 1000001;

    // array to store prime factors
    let factor = [];

    // function to generate all prime factors
    // of numbers from 1 to 10^6
    function cal_factor() {
    factor[1] = 1;

    // Initializes all the positions
    // with their value.
    for (let i = 2; i < MAX; i++)
    factor[i] = i;

    // Initializes all multiples of 2 with 2
    for (let i = 4; i < MAX; i += 2)
    factor[i] = 2;

    // A modified version of Sieve of Eratosthenes to
    // store the smallest prime factor that divides
    // every number.
    for (let i = 3; i * i < MAX; i++) {

    // check if it has no prime factor.
    if (factor[i] == i) {

        // Initializes of j starting from i*i
        for (let j = i * i; j < MAX; j += i) {

        // if it has no prime factor before, then
        // stores the smallest prime divisor
        if (factor[j] == j)
            factor[j] = i;
        }
    }
    }
}

// function to calculate the
// number of representations
function no_of_representations(a, n) {

    // keep an count of prime factors
    let count = 0;

    // traverse for every element
    for (let i = 0; i < n; i++) {

    let temp = a[i];
    let flag = 0;

    // count the no of factors
    while (factor[temp] != 1) {
        flag = -1;
        count++;
        temp = temp / factor[temp];
    }

    // subtract 1 if Ai is not 1 as the
    // last step wont be taken into count
    count += flag;
    }

    return count;
}

// Driver code

    // call sieve to calculate the factors
    cal_factor();

    let a = [4, 4, 4];
    let n = a.length;

    document.write(no_of_representations(a, n));

    // This code is contributed by code_hunt.
</script>
```

**输出:**

```
3
```

**时间复杂度:** O( n * log n)

本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。