# GCD 大于 1 的最大子序列

> 原文:[https://www . geesforgeks . org/maximum-subsequel-gcd-greater-1/](https://www.geeksforgeeks.org/largest-subsequence-gcd-greater-1/)

给定一个数组 arr[]，找到最大的子序列，使得所有这些子序列的 GCD 都大于 1。
**例:**

```
Input: 3, 6, 2, 5, 4
Output: 3
Explanation: There are only three elements(6, 
2, 4) having GCD greater than 1 i.e., 2\. So the 
largest subsequence will be 3

Input: 10, 15, 7, 25, 9, 35
Output: 4
```

**天真方法(方法 1)**

简单的方法是逐个生成所有的子序列，然后找到所有这样生成的集合的 GCD。这种方法的问题是它在 2<sup>N</sup>T2 呈指数增长

**迭代方法(方法 2)**

如果我们观察，那么我们会发现，要使 gcd 大于 1，所有这样的元素必须包含大于 1 的公因数，该公因数平均分配所有这些值。为了得到这个因子，我们将从 2 迭代到数组的最大元素，然后检查可除性。

## C++

```
// Simple C++ program to find length of
// the largest subsequence with GCD greater
// than 1.
#include<bits/stdc++.h>

using namespace std;

// Returns length of the largest subsequence
// with GCD more than 1.
int largestGCDSubsequence(int arr[], int n)
{
    int ans = 0;

    // Finding the Maximum value in arr[]
    int maxele = *max_element(arr, arr+n);

    // Iterate from 2 to maximum possible
    // divisor of all give values
    for (int i=2; i<=maxele; ++i)
    {
        int count = 0;
        for (int j=0; j<n; ++j)
        {
            // If we found divisor,
            // increment count
            if (arr[j]%i == 0)
                ++count;
        }
        ans = max(ans, count);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = {3, 6, 2, 5, 4};
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << largestGCDSubsequence(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find length of
// the largest subsequence with GCD greater
// than 1.
import java.util.Arrays;

class GFG {
// Returns length of the largest subsequence
// with GCD more than 1.
static int largestGCDSubsequence(int arr[], int n)
{
    int ans = 0;

    // Finding the Maximum value in arr[]
    int maxele = Arrays.stream(arr).max().getAsInt();;

    // Iterate from 2 to maximum possible
    // divisor of all give values
    for (int i=2; i<=maxele; ++i)
    {
        int count = 0;
        for (int j=0; j<n; ++j)
        {
            // If we found divisor,
            // increment count
            if (arr[j]%i == 0)
                ++count;
        }
        ans = Math.max(ans, count);
    }

    return ans;
}
// Driver program to test above

    public static void main(String[] args) {

        int arr[] = {3, 6, 2, 5, 4};
        int size = arr.length;

        System.out.println(largestGCDSubsequence(arr, size));
    }
}

//this code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Simple Python 3 program to find length of
# the largest subsequence with GCD greater
# than 1.

# Returns length of the largest subsequence
# with GCD more than 1.
def largestGCDSubsequence(arr, n):
    ans = 0

    # Finding the Maximum value in arr[]
    maxele = max(arr)

    # Iterate from 2 to maximum possible
    # divisor of all give values
    for i in range(2, maxele + 1):
        count = 0
        for j in range(n):

            # If we found divisor,
            # increment count
            if (arr[j] % i == 0):
                count += 1
        ans = max(ans, count)

    return ans

# Driver code
if __name__ == '__main__':
    arr = [3, 6, 2, 5, 4]
    size = len(arr)
    print(largestGCDSubsequence(arr, size))

# This code is contributed by Rajput-Ji
```

## C#

```

// Efficient C# program to find length of
// the largest subsequence with GCD greater
// than 1.
using System;
using System.Linq;
public class GFG {
// Returns length of the largest subsequence
// with GCD more than 1.
static int largestGCDSubsequence(int []arr, int n)
{
    int ans = 0;

    // Finding the Maximum value in arr[]
    int maxele = arr.Max();

    // Iterate from 2 to maximum possible
    // divisor of all give values
    for (int i=2; i<=maxele; ++i)
    {
        int count = 0;
        for (int j=0; j<n; ++j)
        {
            // If we found divisor,
            // increment count
            if (arr[j]%i == 0)
                ++count;
        }
        ans = Math.Max(ans, count);
    }

    return ans;
}
// Driver program to test above

    public static void Main() {

        int []arr = {3, 6, 2, 5, 4};
        int size = arr.Length;

        Console.Write(largestGCDSubsequence(arr, size));
    }
}

//this code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find length of
// the largest subsequence with GCD greater
// than 1.

// Returns length of the largest subsequence
// with GCD more than 1.
function largestGCDSubsequence($arr, $n)
{
    $ans = 0;

    // Finding the Maximum value in arr[]
    $maxele = max($arr);

    // Iterate from 2 to maximum possible
    // divisor of all give values
    for ($i = 2; $i <= $maxele; ++$i)
    {
        $count = 0;
        for ($j = 0; $j < $n; ++$j)
        {
            // If we found divisor,
            // increment count
            if ($arr[$j] % $i == 0)
                ++$count;
        }
        $ans = max($ans, $count);
    }

    return $ans;
}

// Driver code
$arr = array(3, 6, 2, 5, 4);
$size = count($arr);
echo largestGCDSubsequence($arr, $size);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Efficient javascript program to find length of
// the largest subsequence with GCD greater
// than 1.

// Returns length of the largest subsequence
    // with GCD more than 1.
    function largestGCDSubsequence(arr , n)
    {
        var ans = 0;

        // Finding the Maximum value in arr
        var maxele =Math.max(...arr);

        // Iterate from 2 to maximum possible
        // divisor of all give values
        for ( var i = 2; i <= maxele; ++i)
        {
            var count = 0;
            for (j = 0; j < n; ++j)
            {

                // If we found divisor,
                // increment count
                if (arr[j] % i == 0)
                    ++count;
            }
            ans = Math.max(ans, count);
        }
        return ans;
    }

    // Driver program to test above
        var arr = [ 3, 6, 2, 5, 4 ];
        var size = arr.length;

        document.write(largestGCDSubsequence(arr, size));

// This code is contributed by aashish1995
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n * max(arr[i])，其中 n 为数组大小。
**辅助空间:** O(1)

**最佳方法(方法 3)**

一种有效的方法是借助厄拉多塞的[筛使用素分解方法。首先，我们将通过预先计算的筛子找到所有元素的最小素除数。之后，我们将标记 arr[]每个元素的所有素除数，方法是借助预先计算的素[]数组对其进行因子分解。
现在我们有了所有数组元素中出现的所有标记素数。最后一步是找到所有这些质因数的最大计数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// Efficient C++ program to find length of
// the largest subsequence with GCD greater
// than 1.
#include<bits/stdc++.h>

using namespace std;

#define MAX 100001

// prime[] for storing smallest prime divisor of element
// count[] for storing the number of times a particular
// divisor occurs in a subsequence
int prime[MAX], countdiv[MAX];

// Simple sieve to find smallest prime factors of numbers
// smaller than MAX
void SieveOfEratosthenes()
{
    for (int i = 2; i * i <= MAX; ++i)
    {
        if (!prime[i])
            for (int j = i * 2; j <= MAX; j += i)
                prime[j] = i;
    }

    // Prime number will have same divisor
    for (int i = 1; i < MAX; ++i)
        if (!prime[i])
            prime[i] = i;
}

// Returns length of the largest subsequence
// with GCD more than 1.
int largestGCDSubsequence(int arr[], int n)
{
    int ans = 0;
    for (int i=0; i < n; ++i)
    {
        int element = arr[i];

        // Fetch total unique prime divisor of element
        while (element > 1)
        {
            int div = prime[element];

            // Increment count[] of Every unique divisor
            // we get till now
            ++countdiv[div];

            // Find maximum frequency of divisor
            ans = max(ans, countdiv[div]);

            while (element % div==0)
                element /= div;
        }
    }

    return ans;
}

// Driver code
int main()
{
    // Pre-compute smallest divisor of all numbers
    SieveOfEratosthenes();

    int arr[] = {10, 15, 7, 25, 9, 35};
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << largestGCDSubsequence(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find length of
// the largest subsequence with GCD greater
// than 1.

class GFG
{
static int MAX = 100001;

// prime[] for storing smallest prime divisor
// of element count[] for storing the number
// of times a particular divisor occurs
// in a subsequence
static int[] prime = new int[MAX + 1];
static int[] countdiv = new int[MAX + 1];

// Simple sieve to find smallest prime
// factors of numbers smaller than MAX
static void SieveOfEratosthenes()
{
    for (int i = 2; i * i <= MAX; ++i)
    {
        if (prime[i] == 0)
            for (int j = i * 2; j <= MAX; j += i)
                prime[j] = i;
    }

    // Prime number will have same divisor
    for (int i = 1; i < MAX; ++i)
        if (prime[i] == 0)
            prime[i] = i;
}

// Returns length of the largest subsequence
// with GCD more than 1.
static int largestGCDSubsequence(int arr[], int n)
{
    int ans = 0;
    for (int i = 0; i < n; ++i)
    {
        int element = arr[i];

        // Fetch total unique prime divisor of element
        while (element > 1)
        {
            int div = prime[element];

            // Increment count[] of Every unique divisor
            // we get till now
            ++countdiv[div];

            // Find maximum frequency of divisor
            ans = Math.max(ans, countdiv[div]);

            while (element % div == 0)
                element /= div;
        }
    }
    return ans;
}

// Driver code
public static void main (String[] args)
{
    // Pre-compute smallest divisor of all numbers
    SieveOfEratosthenes();

    int arr[] = {10, 15, 7, 25, 9, 35};
    int size = arr.length;

    System.out.println(largestGCDSubsequence(arr, size));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Efficient Python3 program to find length
# of the largest subsequence with GCD
# greater than 1.
import math as mt

MAX = 100001

# prime[] for storing smallest
# prime divisor of element
# count[] for storing the number
# of times a particular divisor
# occurs in a subsequence
prime = [0 for i in range(MAX + 1)]
countdiv = [0 for i in range(MAX + 1)]

# Simple sieve to find smallest prime
# factors of numbers smaller than MAX
def SieveOfEratosthenes():

    for i in range(2, mt.ceil(mt.sqrt(MAX + 1))):

        if (prime[i] == 0):
            for j in range(i * 2, MAX + 1, i):
                prime[j] = i

    # Prime number will have same divisor
    for i in range(1, MAX):
        if (prime[i] == 0):
            prime[i] = i

# Returns length of the largest
# subsequence with GCD more than 1.
def largestGCDSubsequence(arr, n):

    ans = 0
    for i in range(n):

        element = arr[i]

        # Fetch total unique prime
        # divisor of element
        while (element > 1):

            div = prime[element]

            # Increment count[] of Every
            # unique divisor we get till now
            countdiv[div] += 1

            # Find maximum frequency of divisor
            ans = max(ans, countdiv[div])

            while (element % div == 0):
                element = element // div

    return ans

# Driver code

# Pre-compute smallest divisor
# of all numbers
SieveOfEratosthenes()

arr= [10, 15, 7, 25, 9, 35]
size = len(arr)
print(largestGCDSubsequence(arr, size))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// Efficient C# program to find length of
// the largest subsequence with GCD greater
// than 1.
using System;

class GFG
{

static int MAX=100001;

// prime[] for storing smallest
// prime divisor of element count[]
// for storing the number of times
// a particular divisor occurs in a subsequence
static int[] prime = new int[MAX + 1];
static int[] countdiv = new int[MAX + 1];

// Simple sieve to find smallest prime
//  factors of numbers smaller than MAX
static void SieveOfEratosthenes()
{
    for (int i = 2; i * i <= MAX; ++i)
    {
        if (prime[i] == 0)
            for (int j = i * 2; j <= MAX; j += i)
                prime[j] = i;
    }

    // Prime number will have same divisor
    for (int i = 1; i < MAX; ++i)
        if (prime[i] == 0)
            prime[i] = i;
}

// Returns length of the largest subsequence
// with GCD more than 1.
static int largestGCDSubsequence(int []arr, int n)
{
    int ans = 0;
    for (int i = 0; i < n; ++i)
    {
        int element = arr[i];

        // Fetch total unique prime divisor of element
        while (element > 1)
        {
            int div = prime[element];

            // Increment count[] of Every unique divisor
            // we get till now
            ++countdiv[div];

            // Find maximum frequency of divisor
            ans = Math.Max(ans, countdiv[div]);

            while (element % div==0)
                element /= div;
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    // Pre-compute smallest
    // divisor of all numbers
    SieveOfEratosthenes();

    int []arr = {10, 15, 7, 25, 9, 35};
    int size = arr.Length;

    Console.WriteLine(largestGCDSubsequence(arr, size));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find length of
// the largest subsequence with GCD greater
// than 1.

$MAX = 10001;

// prime[] for storing smallest prime divisor of element
// count[] for storing the number of times a particular
// divisor occurs in a subsequence
$prime = array_fill(0, $MAX, 0);
$countdiv = array_fill(0, $MAX, 0);

// Simple sieve to find smallest prime factors of numbers
// smaller than MAX
function SieveOfEratosthenes()
{
    global $MAX,$prime;
    for ($i = 2; $i * $i <= $MAX; ++$i)
    {
        if ($prime[$i] == 0)
            for ($j = $i * 2; $j <= $MAX; $j += $i)
                $prime[$j] = $i;
    }

    // Prime number will have same divisor
    for ($i = 1; $i < $MAX; ++$i)
        if ($prime[$i] == 0)
            $prime[$i] = $i;
}

// Returns length of the largest subsequence
// with GCD more than 1.
function largestGCDSubsequence($arr, $n)
{
    global $countdiv,$prime;
    $ans = 0;
    for ($i = 0; $i < $n; ++$i)
    {
        $element = $arr[$i];

        // Fetch total unique prime divisor of element
        while ($element > 1)
        {
            $div = $prime[$element];

            // Increment count[] of Every unique divisor
            // we get till now
            ++$countdiv[$div];

            // Find maximum frequency of divisor
            $ans = max($ans, $countdiv[$div]);

            while ($element % $div == 0)
                $element = (int)($element/$div);
        }
    }

    return $ans;
}

    // Driver code
    // Pre-compute smallest divisor of all numbers
    SieveOfEratosthenes();

    $arr = array(10, 15, 7, 25, 9, 35);
    $size = count($arr);

    echo largestGCDSubsequence($arr, $size);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Efficient Javascript program to find length of
// the largest subsequence with GCD greater
// than 1.

let MAX = 100001;
// prime[] for storing smallest prime divisor
// of element count[] for storing the number
// of times a particular divisor occurs
// in a subsequence
let prime = new Array(MAX + 1);
let countdiv = new Array(MAX + 1);
for(let i=0;i<MAX+1;i++)
{
    prime[i]=0;
    countdiv[i]=0;
}

// Simple sieve to find smallest prime
// factors of numbers smaller than MAX
function SieveOfEratosthenes()
{
    for (let i = 2; i * i <= MAX; ++i)
    {
        if (prime[i] == 0)
            for (let j = i * 2; j <= MAX; j += i)
                prime[j] = i;
    }

    // Prime number will have same divisor
    for (let i = 1; i < MAX; ++i)
        if (prime[i] == 0)
            prime[i] = i;
}

// Returns length of the largest subsequence
// with GCD more than 1.
function largestGCDSubsequence(arr,n)
{
    let ans = 0;
    for (let i = 0; i < n; ++i)
    {
        let element = arr[i];

        // Fetch total unique prime divisor of element
        while (element > 1)
        {
            let div = prime[element];

            // Increment count[] of Every unique divisor
            // we get till now
            ++countdiv[div];

            // Find maximum frequency of divisor
            ans = Math.max(ans, countdiv[div]);

            while (element % div == 0)
                element /= div;
        }
    }
    return ans;
}

// Driver code
// Pre-compute smallest divisor of all numbers
SieveOfEratosthenes();
let arr=[10, 15, 7, 25, 9, 35];
let size = arr.length;
document.write(largestGCDSubsequence(arr, size));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
 4
```

**时间复杂度:**O(n * log(MAX(arr[I]))+MAX * log(log(MAX))
**辅助空间:** O(MAX)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息