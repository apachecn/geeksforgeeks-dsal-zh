# K 的最小值，使得第一个 K 自然数的立方之和大于或等于 N

> 原文:[https://www . geesforgeks . org/k 的最小值，即第一个 k 的立方之和自然数大于等于 n/](https://www.geeksforgeeks.org/minimum-value-of-k-such-that-sum-of-cubes-of-first-k-natural-number-is-greater-than-equal-to-n/)

给定一个数 **N** ，任务是找到最小值 **K** ，使得第一个 **K** 自然数的立方之和大于或等于 **N** 。
**举例:**

> **输入:** N = 100
> **输出:** 4
> **解释:**
> 前 4 个自然数的立方之和为 100 等于 N = 100
> **输入:** N = 15
> **输出:** 3
> **解释:**
> 前 2 个自然数的立方之和为 9 小于 K = 15 且

**天真方法:**这个问题的天真方法是运行一个循环，从中找出立方体的和。每当总和超过 N 值时，从循环中断开。
以下是上述办法的实施情况:

## C++

```
// C++ program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
#include <bits/stdc++.h>
using namespace std;

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
int naive_find_x(int N)
{

    // Variable to store the
    // sum of cubes
    int c = 0, i;

    // Loop to find the number
    // K
    for(i = 1; i < N; i++)
    {
        c += i * i * i;

        // If C is just greater then
        // N, then break the loop
        if (c >= N)
            break;
    }
    return i;
}

// Driver code
int main()
{
    int N = 100;
    cout << naive_find_x(N);
    return 0;
}

// This code is contributed by sapnasingh4991
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
class GFG {

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
static int naive_find_x(int N)
{

    // Variable to store the
    // sum of cubes
    int c = 0, i;

    // Loop to find the number
    // K
    for(i = 1; i < N; i++)
    {
       c += i * i * i;

       // If C is just greater then
       // N, then break the loop
       if (c >= N)
           break;
    }
    return i;
}

// Driver code
public static void main(String[] args)
{
    int N = 100;

    System.out.println(naive_find_x(N));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to determine the
# minimum value of K such that the
# sum of cubes of first K
# natural number is greater than
# or equal to N

# Function to determine the
# minimum value of K such that the
# sum of cubes of first K
# natural number is greater than
# or equal to N
def naive_find_x(N):

    # Variable to store the
    # sum of cubes
    c = 0

    # Loop to find the number
    # K
    for i in range(1, N):

        c += i*i*i

        # If C is just greater then
        # N, then break the loop
        if c>= N:
            break

    return i

# Driver code
if __name__ == "__main__":

    N = 100
    print(naive_find_x(N))
```

## C#

```
// C# program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
using System;

class GFG {

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
static int naive_find_x(int N)
{

    // Variable to store the
    // sum of cubes
    int c = 0, i;

    // Loop to find the number
    // K
    for(i = 1; i < N; i++)
    {
    c += i * i * i;

    // If C is just greater then
    // N, then break the loop
    if (c >= N)
        break;
    }
    return i;
}

// Driver code
public static void Main(String[] args)
{
    int N = 100;

    Console.WriteLine(naive_find_x(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
function naive_find_x(N)
{

    // Variable to store the
    // sum of cubes
    var c = 0, i;

    // Loop to find the number
    // K
    for(i = 1; i < N; i++)
    {
       c += i * i * i;

       // If C is just greater then
       // N, then break the loop
       if (c >= N)
           break;
    }
    return i;
}

// Driver code
var N = 100;
document.write(naive_find_x(N));

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(K)，其中 K 是需要找到的数字。*
**有效方法:**需要进行的一个观察是立方体前 N 个自然数的和由公式给出:

```
sum = ((N * (N + 1))/2)2
```

这是一个单调递增的函数。所以思路是应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)求 k 的值，如果某个数‘I’的和大于 N，那么我们就知道答案小于等于‘I’。所以，迭代到左半部分。否则，遍历右半部分。
以下是上述办法的实施情况:

## C++

```
// C++ program to determine the
// minimum value of K such that
// the sum of cubes of first K
// natural number is greater than
// or equal to N
#include <bits/stdc++.h>
using namespace std;

// Function to determine the
// minimum value of K such that
// the sum of cubes of first K
// natural number is greater than
// or equal to N
int binary_searched_find_x(int k)
{

    // Left bound
    int l = 0;

    // Right bound
    int r = k;

    // Variable to store the
    // answer
    int ans = 0;

    // Applying binary search
    while (l <= r)
    {

        // Calculating mid value
        // of the range
        int mid = l + (r - l) / 2;

        if (pow(((mid * (mid + 1)) / 2), 2) >= k)
        {

            // If the sum of cubes of
            // first mid natural numbers
            // is greater than equal to N
            // iterate the left half
            ans = mid;
            r = mid - 1;
        }
        else
        {

            // Sum of cubes of first
            // mid natural numbers is
            // less than N, then move
            // to the right segment
            l = mid + 1;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int N = 100;

    cout << binary_searched_find_x(N);
    return 0;
}

// This code is contributed by shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
class GFG{

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
static int binary_searched_find_x(int k)
{

    // Left bound
    int l = 0;

    // Right bound
    int r = k;

    // Variable to store the
    // answer
    int ans = 0;

    // Applying binary search
    while (l <= r)
    {

        // Calculating mid value
        // of the range
        int mid = l + (r - l) / 2;

        if (Math.pow(((mid * (mid + 1)) / 2), 2) >= k)
        {

            // If the sum of cubes of
            // first mid natural numbers
            // is greater than equal to N
            // iterate the left half
            ans = mid;
            r = mid - 1;
        }
        else
        {

            // Sum of cubes of first
            // mid natural numbers is
            // less than N, then move
            // to the right segment
            l = mid + 1;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 100;
    System.out.println(binary_searched_find_x(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to determine the
# minimum value of K such that the
# sum of cubes of first K
# natural number is greater than
# or equal to N

# Function to determine the
# minimum value of K such that the
# sum of cubes of first K
# natural number is greater than
# or equal to N
def binary_searched_find_x(k):

    # Left bound
    l = 0

    # Right bound
    r = k

    # Variable to store the
    # answer
    ans = 0

    # Applying binary search
    while l<= r:

        # Calculating mid value
        # of the range
        mid = l+(r-l)//2

        if ((mid*(mid + 1))//2)**2>= k:

             # If the sum of cubes of
             # first mid natural numbers
             # is greater than equal to N
             # iterate the left half
             ans = mid
             r = mid-1

        else:

             # Sum of cubes of first
             # mid natural numbers is
             # less than N, then move
             # to the right segment
             l = mid + 1    

    return ans   

# Driver code
if __name__ == "__main__":
    N = 100
    print(binary_searched_find_x(N))
```

## C#

```
// C# program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
using System;
class GFG{

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
static int binary_searched_find_x(int k)
{

    // Left bound
    int l = 0;

    // Right bound
    int r = k;

    // Variable to store the
    // answer
    int ans = 0;

    // Applying binary search
    while (l <= r)
    {

        // Calculating mid value
        // of the range
        int mid = l + (r - l) / 2;

        if (Math.Pow(((mid * (mid + 1)) / 2), 2) >= k)
        {

            // If the sum of cubes of
            // first mid natural numbers
            // is greater than equal to N
            // iterate the left half
            ans = mid;
            r = mid - 1;
        }
        else
        {

            // Sum of cubes of first
            // mid natural numbers is
            // less than N, then move
            // to the right segment
            l = mid + 1;
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int N = 100;
    Console.Write(binary_searched_find_x(N));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>
// javascript program to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N

// Function to determine the
// minimum value of K such that the
// sum of cubes of first K
// natural number is greater than
// or equal to N
function binary_searched_find_x(k)
{

    // Left bound
    var l = 0;

    // Right bound
    var r = k;

    // Variable to store the
    // answer
    var ans = 0;

    // Applying binary search
    while (l <= r)
    {

        // Calculating mid value
        // of the range
        var mid = parseInt(l + (r - l) / 2);

        if (Math.pow(((mid * (mid + 1)) / 2), 2) >= k)
        {

            // If the sum of cubes of
            // first mid natural numbers
            // is greater than equal to N
            // iterate the left half
            ans = mid;
            r = mid - 1;
        }
        else
        {

            // Sum of cubes of first
            // mid natural numbers is
            // less than N, then move
            // to the right segment
            l = mid + 1;
        }
    }
    return ans;
}

// Driver code
var N = 100;
document.write(binary_searched_find_x(N));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log(K))。*