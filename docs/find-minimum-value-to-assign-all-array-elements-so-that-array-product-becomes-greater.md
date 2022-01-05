# 求最小值赋给所有数组元素，使数组乘积变大

> 原文:[https://www . geesforgeks . org/find-最小值-赋值-所有数组元素-使数组-乘积-变大/](https://www.geeksforgeeks.org/find-minimum-value-to-assign-all-array-elements-so-that-array-product-becomes-greater/)

给定一个由 n 个元素组成的数组 arr[]，将给定数组的所有元素更新为某个最小值 x，即 arr[i] = x (0 <= i < n), such that product of all elements of this new array is strictly greater than the product of all elements of the initial array, where 1 <= arr[i] <= 10^10 and 1 <= n <= 10^5
**)示例:**

```
Input  : arr[] = [4, 2, 1, 10, 6]
Output :  4
4 is the smallest value such that 
4 * 4 * 4 * 4 * 4 > 4 * 2 * 1 * 10 * 6

Input  : arr[] = [100, 150, 10000, 123458, 90980454]
Output : 17592
```

**方法 1 : O(n log n)**
我们在 n 的极限上使用二分搜索法，在每个 mid，我们检查 mid <sup>n</sup> 的积是否大于数组的原积。
我们使用产品日志来避免溢出。因此，我们计算当前产品的日志和二分搜索法期间中间 <sup>n</sup> 的日志来比较值。

## C++

```
// C++ program to find minimum value that can
// be assigned to all elements so that product
// becomes greater than current product.
#include<bits/stdc++.h>
#define ll long long
#define ld long double
using namespace std;

ll findMinValue(ll arr[], ll n)
{
    // sort the array to apply Binary search
    sort(arr, arr+n);

    // using log property add every logarithmic
    // value of element to val
    ld val = 0; // where ld is long double
    for (int i=0; i<n; i++)
        val += (ld)(log((ld)(arr[i])));

    // set left and right extremities to find
    // min value
    ll left = arr[0], right = arr[n-1]+1;

    ll ans;
    while (left<=right)
    {
        ll mid = (left+right)/2;

        // multiplying n to mid, to find the
        // correct min value
        ld temp = (ld)n * (ld)(log((ld)(mid)));
        if (val < temp)
        {
            ans = mid;
            right = mid-1;
        }
        else
            left = mid+1;
    }
    return ans;
}

// Driver code
int main()
{
    ll arr[] = {4, 2, 1, 10, 6};
    ll n = sizeof(arr)/sizeof(arr[0]);
    cout << findMinValue(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to find minimum value that can
// be assigned to along elements so that product
// becomes greater than current product.
class GFG1 {

    static long findMinValue(long arr[], int n) {
        // sort the array to apply Binary search
        Arrays.sort(arr);

        // using log property add every logarithmic
        // value of element to val
        double val = 0; // where double is long double
        for (int i = 0; i < n; i++) {
            val += (double) (Math.log((double) (arr[i])));
        }

        // set left and right extremities to find
        // min value
        long left = arr[0], right = arr[n - 1];

        long ans = 0;
        while (left <= right) {
            long mid = (left + right) / 2;

            // multiplying n to mid, to find the
            // correct min value
            double temp = (double) n * (double) (Math.log((double) (mid)));
            if (val < temp) {
                ans = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }

// Driver code
    public static void main(String[] args) {

        long arr[] = {4, 2, 1, 10, 6};
        int n = arr.length;
        System.out.println(findMinValue(arr, n));

    }
}
//This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find minimum
# value that can be assigned to all
# elements so that product becomes
# greater than current product.
import math

def findMinValue(arr, n):

    # sort the array to apply
    # Binary search
    arr.sort()

    # using log property add every
    # logarithmic value of element to val
    val = 0 # where ld is long double
    for i in range(n):
        val += (math.log(arr[i]))

    # set left and right extremities to find
    # min value
    left = arr[0]
    right = arr[n - 1] + 1

    while (left <= right):
        mid = (left + right) // 2

        # multiplying n to mid, to find
        # the correct min value
        temp = n * (math.log(mid))
        if (val < temp):
            ans = mid
            right = mid - 1
        else:
            left = mid + 1
    return ans

# Driver code
if __name__ == "__main__":
    arr = [4, 2, 1, 10, 6]
    n = len(arr)
    print(findMinValue(arr, n) )

# This code is contributed
# by ChitraNayal
```

## C#

```
// C#  program to find minimum value that can
// be assigned to along elements so that product
// becomes greater than current product.

using System;

public class GFG{

    static long findMinValue(long []arr, int n) {
        // sort the array to apply Binary search
        Array.Sort(arr);

        // using log property add every logarithmic
        // value of element to val
        double val = 0; // where double is long double
        for (int i = 0; i < n; i++) {
            val += (double) (Math.Log((double) (arr[i])));
        }

        // set left and right extremities to find
        // min value
        long left = arr[0], right = arr[n - 1];

        long ans = 0;
        while (left <= right) {
            long mid = (left + right) / 2;

            // multiplying n to mid, to find the
            // correct min value
            double temp = (double) n * (double) (Math.Log((double) (mid)));
            if (val < temp) {
                ans = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }

// Driver code
    static public void Main (){
        long []arr = {4, 2, 1, 10, 6};
        int n = arr.Length;
        Console.WriteLine(findMinValue(arr, n));
    }
//This code is contributed by ajit.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum value that can
// be assigned to all elements so that product
// becomes greater than current product.

function findMinValue($arr, $n)
{
    // sort the array to apply Binary search
    sort($arr);

    // using log property add every logarithmic
    // value of element to val
    $val = 0; // where ld is long double
    for ($i = 0; $i < $n; $i++)
        $val += (log($arr[$i]));

    // set left and right extremities
    // to find min value
    $left = $arr[0];
    $right = $arr[$n - 1] + 1;

    $ans = 0;
    while ($left <= $right)
    {
        $mid = (int)($left + $right) / 2;

        // multiplying n to mid, to find
        // the correct min value
        $temp = $n * (log($mid));
        if ($val < $temp)
        {
            $ans = $mid;
            $right = $mid - 1;
        }
        else
            $left = $mid + 1;
    }
    return (floor($ans));
}

// Driver code
$arr = array(4, 2, 1, 10, 6);
$n = sizeof($arr);
echo findMinValue($arr, $n), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum value that can
// be assigned to along elements so that product
// becomes greater than current product.

    function findMinValue(arr,n)
    {
        // sort the array to apply Binary search
        arr.sort(function(a,b){return a-b;});

        // using log property add every logarithmic
        // value of element to val
        let val = 0; // where double is long double
        for (let i = 0; i < n; i++) {
            val +=  (Math.log( (arr[i])));
        }

        // set left and right extremities to find
        // min value
        let left = arr[0], right = arr[n - 1];

        let ans = 0;
        while (left <= right) {
            let mid = Math.floor((left + right) / 2);

            // multiplying n to mid, to find the
            // correct min value
            let temp =  n * (Math.log((mid)));
            if (val < temp) {
                ans = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }

    // Driver code
    let arr=[4, 2, 1, 10, 6];
    let n = arr.length;
    document.write(findMinValue(arr, n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
4
```

**解 2 : O(n)**
通过知道 n 个元素的乘积是 P 的事实，如果我们要求 P 的第 n 个根，要求乘积的第 n 个根，我们可以简单地从数组的 n 个元素的 log 之和除以 n，那么 antilog 的 ceil 将是我们的问题答案，即
ans = ceil(antilog(log(x)/n))
ans = ceil(幂(10，log(x)/n))

## C++

```
// C++ program to find minimum value to assign all
// array elements so that array product becomes greater
#include <bits/stdc++.h>
using namespace std;

// Epsilon value is used at various steps
// to ensure correctness upto 10^15 digits.
#define EPS 1e-15
#define ll long long int

ll findMinValue(ll arr[], ll n)
{
    // add logarithmic value of all elements to sum
    long double sum = 0;
    for (int i=0; i<n; i++)
        sum += (long double)log10(arr[i])+EPS;

    // to find the nth root of sum
    long double xl = (long double)(sum/n+EPS);

    // to find the antilog of xl
    long double res = pow((long double)10.0, (long double)xl) + EPS;
    return (ll)ceil(res+EPS);
}

// Driver code
int main()
{
    ll arr[] = {4, 2, 1, 10, 6};
    ll n  = sizeof(arr)/sizeof(arr[0]);
    printf("%lld", findMinValue(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum value to assign all array
// elements so that array product becomes greater
class GFG{

// Epsilon value is used at various steps
// to ensure correctness upto 10^15 digits.
static double EPS=1E-15;

static double findMinValue(double arr[], double n)
{
    // add logarithmic value of all elements to sum
    double sum = 0;
    for (int i=0; i<n; i++)
        sum += (double)Math.log10(arr[i])+EPS;

    // to find the nth root of sum
    double xl = (double)(sum/n+EPS);

    // to find the antilog of xl
    double res = Math.pow((double)10.0, (double)xl) + EPS;
    return (double)Math.ceil(res+EPS);
}

// Driver code
public static void main(String[] args)
{
    double arr[] = {4, 2, 1, 10, 6};
    double n = arr.length;
    System.out.println(findMinValue(arr, n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Epsilon value is used at various steps
# to ensure correctness upto 10^15 digits.
import math
EPS = 1E-15;

def findMinValue(arr, n):

    # add logarithmic value of all
    # elements to sum
    sum = 0;
    for i in range(n):
        sum += math.log10(arr[i]) + EPS;

    # to find the nth root of sum
    xl = (sum / n + EPS);

    # to find the antilog of xl
    res = math.pow(10.0, xl) + EPS;
    return math.ceil(res + EPS);

# Driver code
arr = [4, 2, 1, 10, 6];
n = len(arr);
print(findMinValue(arr, n));

# This code is contributed by mits
```

## C#

```
// C# program to find minimum value to assign all
// array elements so that array product becomes greater
using System;
class GFG{

// Epsilon value is used at various steps
// to ensure correctness upto 10^15 digits.
static double EPS=1E-15;

static double findMinValue(double[] arr, double n)
{
    // add logarithmic value of all elements to sum
    double sum = 0;
    for (int i=0; i<n; i++)
        sum += (double)Math.Log10(arr[i])+EPS;

    // to find the nth root of sum
    double xl = (double)(sum/n+EPS);

    // to find the antilog of xl
    double res = Math.Pow((double)10.0, (double)xl) + EPS;
    return (double)Math.Ceiling(res+EPS);
}

// Driver code
public static void Main()
{
    double[] arr = {4, 2, 1, 10, 6};
    double n = arr.Length;
    Console.WriteLine(findMinValue(arr, n));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Epsilon value is used at various steps
// to ensure correctness upto 10^15 digits.
$EPS = 1E-15;

function findMinValue($arr, $n)
{
    global $EPS;

    // add logarithmic value of all
    # elements to sum
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += log10($arr[$i]) + $EPS;

    // to find the nth root of sum
    $xl = ($sum / $n + $EPS);

    // to find the antilog of xl
    $res = pow(10.0, $xl) + $EPS;
    return ceil($res + $EPS);
}

// Driver code
$arr = array(4, 2, 1, 10, 6);
$n = count($arr);
print(findMinValue($arr, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to find minimum value to assign all array
// elements so that array product becomes greater   
// Epsilon value is used at various steps
    // to ensure correctness upto 10^15 digits.
    var EPS = 1E-15;

    function findMinValue(arr , n) {
        // add logarithmic value of all elements to sum
        var sum = 0;
        for (i = 0; i < n; i++)
            sum +=  Math.log10(arr[i]) + EPS;

        // to find the nth root of sum
        var xl =  (sum / n + EPS);

        // to find the antilog of xl
        var res = Math.pow( 10.0,  xl) + EPS;
        return Math.ceil(res + EPS);
    }

    // Driver code

        var arr = [ 4, 2, 1, 10, 6 ];
        var n = arr.length;
        document.write(findMinValue(arr, n));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
4
```

本文由 **Abhishek Rajput** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。