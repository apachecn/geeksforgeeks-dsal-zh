# 计算中位数也存在于同一子集中的子集数量

> 原文:[https://www . geesforgeks . org/count-子集数-其中值也存在于同一个子集中/](https://www.geeksforgeeks.org/count-number-of-subsets-whose-median-is-also-present-in-the-same-subset/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是计算我们可以从给定数组元素中选择一个子集的方式的数量，使得所选子集的中值也作为元素出现在子集中。因为这个数字可能很大，所以以 1000000007 为模进行计算。
**例:**

> **输入:** arr[] = {2，3，2}
> **输出:** 5
> {2}、{3}、{2}、{2，2}和{2，3，2}都是可能的有效子集。
> **输入:** arr[] = {1，4，2，2，3，5}
> **输出:** 36

**进场:**

*   奇数大小的每个子集都有它的中值出现在子集里，所以，我们可以直接在答案上加上 2<sup>N–1</sup>。
*   对于偶数大小的子集，当且仅当中间两个元素相等时，将选择该子集。
*   我们需要计算具有相等中间元素的偶数大小的子集的数量。

**简单的解决方案**将是迭代每对相等的元素(I，j)，使得 A[i] = A[j]，并迭代从 X = 1 到 N 的子集的大小 2 * X。使具有两个固定中间元素的大小 X 的子集的方法的数量正好是我们可以从[1，I–1]中选择 X–1 元素和从[j + 1，N]中选择 X–1 元素的方法的数量的乘积。
这个解决方案需要迭代每一对(I，j)，每一对需要 O(N <sup>2</sup> 时间和 O(N)时间，导致整体时间复杂度 O(N <sup>3</sup> )
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <iostream>
using namespace std;
long long mod = 1000000007;

// Function to return the factorial of a number
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to return the value of nCr
int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to return a raised to the power n
// with complexity O(log(n))
long long powmod(long long a, long long n)
{
    if (!n)
        return 1;
    long long pt = powmod(a, n / 2);
    pt = (pt * pt) % mod;
    if (n % 2)
        return (pt * a) % mod;
    else
        return pt;
}

// Function to return the number of sub-sets
// whose median is also present in the set
long long CountSubset(int* arr, int n)
{

    // Number of odd length sub-sets
    long long ans = powmod(2, n - 1);

    // Sort the array
    sort(arr, arr + n);
    for (int i = 0; i < n; ++i) {
        int j = i + 1;

        // Checking each element for leftmost middle
        // element while they are equal
        while (j < n && arr[j] == arr[i]) {

            // Calculate the number of elements in
            // right of rightmost middle element
            int r = n - 1 - j;

            // Calculate the number of elements in
            // left of leftmost middle element
            int l = i;

            // Add selected even length subsets
            // to the answer
            ans = (ans + nCr(l + r, l)) % mod;
            j++;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << CountSubset(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    static long mod = 1000000007;

    // Function to return the factorial of a number
    static int fact(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to return the value of nCr
    static int nCr(int n, int r)
    {
        return fact(n) / (fact(r) * fact(n - r));
    }

    // Function to return a raised to the power n
    // with complexity O(log(n))
    static long powmod(long a, long n)
    {
        if (n == 0)
            return 1;
        long pt = powmod(a, n / 2);
        pt = (pt * pt) % mod;
        if (n % 2 == 1)
            return (pt * a) % mod;
        else
            return pt;
    }

    // Function to return the number of sub-sets
    // whose median is also present in the set
    static long CountSubset(int[] arr, int n)
    {

        // Number of odd length sub-sets
        long ans = powmod(2, n - 1);

        // Sort the array
        Arrays.sort(arr);
        for (int i = 0; i < n; ++i) {
            int j = i + 1;

            // Checking each element for leftmost middle
            // element while they are equal
            while (j < n && arr[j] == arr[i]) {

                // Calculate the number of elements in
                // right of rightmost middle element
                int r = n - 1 - j;

                // Calculate the number of elements in
                // left of leftmost middle element
                int l = i;

                // Add selected even length subsets
                // to the answer
                ans = (ans + nCr(l + r, l)) % mod;
                j++;
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 2 };
        int n = arr.length;
        System.out.println(CountSubset(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
mod = 1000000007

# Function to return
# the factorial of a number
def fact(n):
    res = 1
    for i in range(2, n + 1):
        res = res * i
    return res

# Function to return the value of nCr
def nCr(n, r):
    return int(fact(n) / (fact(r) *
                          fact(n - r)))

# Function to return 'a' raised to the power n
# with complexity O(log(n))
def powmod(a, n):
    if (n == 0):
        return 1
    pt = powmod(a, int(n / 2))
    pt = (pt * pt) % mod
    if (n % 2):
        return (pt * a) % mod
    else:
        return pt

# Function to return the number of sub-sets
# whose median is also present in the set
def CountSubset(arr, n):

    # Number of odd length sub-sets
    ans = powmod(2, n - 1)

    # Sort the array
    arr.sort(reverse = False)
    for i in range(n):
        j = i + 1

        # Checking each element for leftmost middle
        # element while they are equal
        while (j < n and arr[j] == arr[i]):

            # Calculate the number of elements in
            # right of rightmost middle element
            r = n - 1 - j

            # Calculate the number of elements in
            # left of leftmost middle element
            l = i

            # Add selected even length subsets
            # to the answer
            ans = (ans + nCr(l + r, l)) % mod
            j += 1

    return ans

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 2]
    n = len(arr)
    print(CountSubset(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    static long mod = 1000000007;

    // Function to return the factorial of a number
    static int fact(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to return the value of nCr
    static int nCr(int n, int r)
    {
        return fact(n) / (fact(r) * fact(n - r));
    }

    // Function to return a raised to the power n
    // with complexity O(log(n))
    static long powmod(long a, long n)
    {
        if (n == 0)
            return 1;
        long pt = powmod(a, n / 2);
        pt = (pt * pt) % mod;
        if (n % 2 == 1)
            return (pt * a) % mod;
        else
            return pt;
    }

    // Function to return the number of sub-sets
    // whose median is also present in the set
    static long CountSubset(int[] arr, int n)
    {

        // Number of odd length sub-sets
        long ans = powmod(2, n - 1);

        // Sort the array
        Array.Sort(arr);
        for (int i = 0; i < n; ++i) {
            int j = i + 1;

            // Checking each element for leftmost middle
            // element while they are equal
            while (j < n && arr[j] == arr[i]) {

                // Calculate the number of elements in
                // right of rightmost middle element
                int r = n - 1 - j;

                // Calculate the number of elements in
                // left of leftmost middle element
                int l = i;

                // Add selected even length subsets
                // to the answer
                ans = (ans + nCr(l + r, l)) % mod;
                j++;
            }
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 2, 3, 2 };
        int n = arr.Length;
        Console.WriteLine(CountSubset(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$mod = 1000000007;

// Function to return the factorial of a number
function fact($n)
{

    $res = 1;
    for ($i = 2; $i <= $n; $i++)
        $res = $res * $i;
    return $res;
}

// Function to return the value of nCr
function nCr($n, $r)
{
    return fact($n) / (fact($r) * fact($n - $r));
}

// Function to return a raised to the power n
// with complexity O(log(n))
function powmod($a, $n)
{
    global $mod;
    if ($n == 0)
        return 1;
    $pt = powmod($a, $n / 2);
    $pt = ($pt * $pt) % $mod;
    if ($n % 2 == 1)
        return ($pt * $a) % $mod;
    else
        return $pt;
}

// Function to return the number of sub-sets
// whose median is also present in the set
function CountSubset( $arr, $n)
{
    global $mod;

    // Number of odd length sub-sets
    $ans = powmod(2, $n - 1);

    // Sort the array
    sort($arr, 0);
    for ($i = 0; $i < $n; ++$i)
    {
        $j = $i + 1;

        // Checking each element for leftmost middle
        // element while they are equal
        while ($j < $n && $arr[$j] == $arr[$i])
        {

            // Calculate the number of elements in
            // right of rightmost middle element
            $r = $n - 1 - $j;

            // Calculate the number of elements in
            // left of leftmost middle element
            $l = $i;

            // Add selected even length subsets
            // to the answer
            $ans = ($ans + nCr($l + $r, $l)) % $mod;
            $j++;
        }
    }

    return $ans;
}

// Driver code
{
    $arr = array(2, 3, 2 );
    $n = sizeof($arr);
    echo(CountSubset($arr, $n));
}

// This code has been contributed by Code_Mech.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

const mod = 1000000007;

// Function to return the factorial of a number
function fact(n)
{
    let res = 1;
    for (let i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to return the value of nCr
function nCr(n, r)
{
    return parseInt(fact(n) / (fact(r) * fact(n - r)));
}

// Function to return a raised to the power n
// with complexity O(log(n))
function powmod(a, n)
{
    if (!n)
        return 1;
    let pt = powmod(a, parseInt(n / 2));
    pt = (pt * pt) % mod;
    if (n % 2)
        return (pt * a) % mod;
    else
        return pt;
}

// Function to return the number of sub-sets
// whose median is also present in the set
function CountSubset(arr, n)
{

    // Number of odd length sub-sets
    let ans = powmod(2, n - 1);

    // Sort the array
    arr.sort();
    for (let i = 0; i < n; ++i) {
        let j = i + 1;

        // Checking each element for leftmost middle
        // element while they are equal
        while (j < n && arr[j] == arr[i]) {

            // Calculate the number of elements in
            // right of rightmost middle element
            let r = n - 1 - j;

            // Calculate the number of elements in
            // left of leftmost middle element
            let l = i;

            // Add selected even length subsets
            // to the answer
            ans = (ans + nCr(l + r, l)) % mod;
            j++;
        }
    }

    return ans;
}

// Driver code
    let arr = [ 2, 3, 2 ];
    let n = arr.length;
    document.write(CountSubset(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N <sup>3</sup> )
如果我们将帕斯卡三角形存储在二维数组中，上述方法的时间复杂度可以降低到 O(N <sup>2</sup> )。所以，现在我们不必一次又一次地计算阶乘。在这里阅读更多关于帕斯卡三角[的内容。
以下是上述方法的实施:](https://www.geeksforgeeks.org/pascal-triangle/) 

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <iostream>
using namespace std;
long long mod = 1000000007;
long long arr[1001][1001];

// Function to store pascal triangle in 2-d array
void Preprocess()
{
    arr[0][0] = 1;
    for (int i = 1; i <= 1000; ++i) {
        arr[i][0] = 1;
        for (int j = 1; j < i; ++j) {
            arr[i][j] = (arr[i - 1][j - 1] + arr[i - 1][j]) % mod;
        }
        arr[i][i] = 1;
    }
}

// Function to return a raised to the power n
// with complexity O(log(n))
long long powmod(long long a, long long n)
{
    if (!n)
        return 1;
    long long pt = powmod(a, n / 2);
    pt = (pt * pt) % mod;
    if (n % 2)
        return (pt * a) % mod;
    else
        return pt;
}

// Function to return the number of sub-sets
// whose median is also present in the set
long long CountSubset(int* val, int n)
{

    // Number of odd length sub-sets
    long long ans = powmod(2, n - 1);

    // Sort the array
    sort(val, val + n);
    for (int i = 0; i < n; ++i) {
        int j = i + 1;

        // Checking each element for leftmost middle
        // element while they are equal
        while (j < n && val[j] == val[i]) {

            // Calculate the number of elements in
            // right of rightmost middle element
            int r = n - 1 - j;

            // Calculate the number of elements in
            // left of leftmost middle element
            int l = i;

            // Add selected even length subsets
            // to the answer
            ans = (ans + arr[l + r][l]) % mod;
            j++;
        }
    }

    return ans;
}

// Driver code
int main()
{
    Preprocess();
    int val[] = { 2, 3, 2 };
    int n = sizeof(val) / sizeof(val[0]);
    cout << CountSubset(val, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG
{

    static long mod = 1000000007;
    static long[][] arr = new long[1001][1001];

    // Function to store pascal triangle in 2-d array
    static void Preprocess()
    {
        arr[0][0] = 1;
        for (int i = 1; i <= 1000; ++i)
        {
            arr[i][0] = 1;
            for (int j = 1; j < i; ++j)
            {
                arr[i][j] = (arr[i - 1][j - 1] + arr[i - 1][j]) % mod;
            }
            arr[i][i] = 1;
        }
    }

    // Function to return a raised to the power n
    // with complexity O(log(n))
    static long powmod(long a, long n)
    {
        if (n == 0)
        {
            return 1;
        }
        long pt = powmod(a, n / 2);
        pt = (pt * pt) % mod;
        if (n % 2 == 1)
        {
            return (pt * a) % mod;
        }
        else
        {
            return pt;
        }
    }

    // Function to return the number of sub-sets
    // whose median is also present in the set
    static long CountSubset(int[] val, int n)
    {

        // Number of odd length sub-sets
        long ans = powmod(2, n - 1);

        // Sort the array
        Arrays.sort(val);
        for (int i = 0; i < n; ++i)
        {
            int j = i + 1;

            // Checking each element for leftmost middle
            // element while they are equal
            while (j < n && val[j] == val[i])
            {

                // Calculate the number of elements in
                // right of rightmost middle element
                int r = n - 1 - j;

                // Calculate the number of elements in
                // left of leftmost middle element
                int l = i;

                // Add selected even length subsets
                // to the answer
                ans = (ans + arr[l + r][l]) % mod;
                j++;
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        Preprocess();
        int val[] = {2, 3, 2};
        int n = val.length;

        System.out.println(CountSubset(val, n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 1000000007
arr = [[None for i in range(1001)] for j in range(1001)]

# Function to store pascal triangle in 2-d array
def Preprocess():

    arr[0][0] = 1
    for i in range(1, 1001): 
        arr[i][0] = 1
        for j in range(1, i): 
            arr[i][j] = (arr[i - 1][j - 1] + arr[i - 1][j]) % mod

        arr[i][i] = 1

# Function to return a raised to the power n
# with complexity O(log(n))
def powmod(a, n):

    if not n:
        return 1
    pt = powmod(a, n // 2)
    pt = (pt * pt) % mod
    if n % 2:
        return (pt * a) % mod
    else:
        return pt

# Function to return the number of sub-sets
# whose median is also present in the set
def CountSubset(val, n):

    # Number of odd length sub-sets
    ans = powmod(2, n - 1)

    # Sort the array
    val.sort()
    for i in range(0, n): 
        j = i + 1

        # Checking each element for leftmost middle
        # element while they are equal
        while j < n and val[j] == val[i]: 

            # Calculate the number of elements in
            # right of rightmost middle element
            r = n - 1 - j

            # Calculate the number of elements in
            # left of leftmost middle element
            l = i

            # Add selected even length
            # subsets to the answer
            ans = (ans + arr[l + r][l]) % mod
            j += 1

    return ans

# Driver code
if __name__ == "__main__":

    Preprocess()
    val = [2, 3, 2]
    n = len(val)
    print(CountSubset(val, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static long mod = 1000000007;
    static long [,]arr = new long[1001,1001];

    // Function to store pascal triangle in 2-d array
    static void Preprocess()
    {
        arr[0,0] = 1;
        for (int i = 1; i <= 1000; ++i)
        {
            arr[i,0] = 1;
            for (int j = 1; j < i; ++j)
            {
                arr[i,j] = (arr[i - 1,j - 1] + arr[i - 1,j]) % mod;
            }
            arr[i,i] = 1;
        }
    }

    // Function to return a raised to the power n
    // with complexity O(log(n))
    static long powmod(long a, long n)
    {
        if (n == 0)
        {
            return 1;
        }
        long pt = powmod(a, n / 2);
        pt = (pt * pt) % mod;
        if (n % 2 == 1)
        {
            return (pt * a) % mod;
        }
        else
        {
            return pt;
        }
    }

    // Function to return the number of sub-sets
    // whose median is also present in the set
    static long CountSubset(int[] val, int n)
    {

        // Number of odd length sub-sets
        long ans = powmod(2, n - 1);

        // Sort the array
        Array.Sort(val);
        for (int i = 0; i < n; ++i)
        {
            int j = i + 1;

            // Checking each element for leftmost middle
            // element while they are equal
            while (j < n && val[j] == val[i])
            {

                // Calculate the number of elements in
                // right of rightmost middle element
                int r = n - 1 - j;

                // Calculate the number of elements in
                // left of leftmost middle element
                int l = i;

                // Add selected even length subsets
                // to the answer
                ans = (ans + arr[l + r,l]) % mod;
                j++;
            }
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        Preprocess();
        int []val = {2, 3, 2};
        int n = val.Length;

        Console.WriteLine(CountSubset(val, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Js implementation of the approach
let mod = 1000000007;
let arr = [];
for(let i = 0;i<1001;i++){
   arr[i] = [];
   for(let j = 0;j<1001;j++){
        arr[i][j] = 0;
   }
}

// Function to store pascal triangle in 2-d array
function Preprocess()
{
    arr[0][0] = 1;
    for (let i = 1; i <= 1000; ++i) {
        arr[i][0] = 1;
        for (let j = 1; j < i; ++j) {
            arr[i][j] = (arr[i - 1][j - 1] + arr[i - 1][j]) % mod;
        }
        arr[i][i] = 1;
    }
}

// Function to return a raised to the power n
// with complexity O(log(n))
function powmod( a,  n)
{
    if (!n)
        return 1;
    let pt = powmod(a, Math.floor(n / 2));
    pt = (pt * pt) % mod;
    if (n % 2)
        return (pt * a) % mod;
    else
        return pt;
}

// Function to return the number of sub-sets
// whose median is also present in the set
function CountSubset( val, n)
{

    // Number of odd length sub-sets
    let ans = powmod(2, n - 1);

    // Sort the array
    val.sort(function(a,b){return a-b});
    for (let i = 0; i < n; ++i) {
        let j = i + 1;

        // Checking each element for leftmost middle
        // element while they are equal
        while (j < n && val[j] == val[i]) {

            // Calculate the number of elements in
            // right of rightmost middle element
            let r = n - 1 - j;

            // Calculate the number of elements in
            // left of leftmost middle element
            let l = i;

            // Add selected even length subsets
            // to the answer
            ans = (ans + arr[l + r][l]) % mod;
            j++;
        }
    }

    return ans;
}

// Driver code
Preprocess();
    let val = [ 2, 3, 2 ];
    let n =val.length;
    document.write( CountSubset(val, n),'<br>');

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N <sup>2</sup> )