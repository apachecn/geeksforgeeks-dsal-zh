# 寻找具有最大位“与”和位“或”的子序列

> 原文:[https://www . geesforgeks . org/find-subseries-with-maximum-bitwise-and-bitwise-or/](https://www.geeksforgeeks.org/find-subsequences-with-maximum-bitwise-and-and-bitwise-or/)

给定 n 个元素的数组。任务是通过选择数组的两个子序列(不一定不同)来打印最大和，使得第一个子序列的所有元素的按位“与”和第二个子序列的所有元素的按位“或”之和最大。

**示例:**

```
Input: arr[] = {3, 5, 6, 1}
Output: 13
We get maximum AND value by choosing 6 only and maximum OR value by choosing all (3 | 5 | 6 | 1) = 7\. So the result is 6 + 7 = 13.

Input: arr[] = {3, 3}
Output: 6
```

**方法:**最大“或”是所有数字的“或”，最大“与”是数组中的最大元素。这是因为如果(x | y) > = x，y 和(x & y) < =x，y.

## C++

```
//C++ implementation of above approach
#include<bits/stdc++.h>

using namespace std;

//function to find the maximum sum
void maxSum(int a[],int n)
{
    int maxAnd=0;

    //Maximum And is maximum element
    for(int i=0;i<n;i++)
        maxAnd=max(maxAnd,a[i]);

    //Maximum OR is bitwise OR of all
    int maxOR=0;
    for(int i=0;i<n;i++)
    {
        maxOR=maxOR|a[i];
    }

    cout<<maxAnd+maxOR;
}

//Driver code
int main()
{
    int a[]={3,5,6,1};

    int n=sizeof(a)/sizeof(a[0]);

    maxSum(a,n);
}

//This code is contributed by Mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java implementation of the above approach
// Function to find the maximum sum
class GFG {

    static void maxSum(int[] a, int n) {

        // Maximum AND is maximum element
        int maxAnd = Arrays.stream(a).max().getAsInt();

        // Maximum OR is bitwise OR of all.
        int maxOR = 0;
        for (int i = 0; i < n; i++) {
            maxOR |= a[i];
        }
        System.out.println((maxAnd + maxOR));

// Driver code
    }

    public static void main(String[] args) {

        int n = 4;
        int[] a = {3, 5, 6, 1};
        maxSum(a, n);
    }
}

//This code contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to find the maximum sum
def maxSum(a, n):

    # Maximum AND is maximum element
    maxAnd = max(a)

    # Maximum OR is bitwise OR of all.
    maxOR = 0
    for i in range(n):
        maxOR|= a[i]

    print(maxAnd + maxOR)

# Driver code
n = 4
a = [3, 5, 6, 1]
maxSum(a, n)
```

## C#

```
// C# implementation of the above approach

using System;
using System.Linq;
public class GFG {

    // Function to find the maximum sum
    static void maxSum(int []a, int n) {

        // Maximum AND is maximum element
        int maxAnd = a.Max();
        // Maximum OR is bitwise OR of all.
        int maxOR = 0;
        for (int i = 0; i < n; i++) {
            maxOR |= a[i];
        }
        Console.Write((maxAnd + maxOR));

// Driver code
    }

    public static void Main() {

        int n = 4;
        int[] a = {3, 5, 6, 1};
        maxSum(a, n);
    }
}

//This code contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to find the maximum sum
function maxSum($a, $n)
{

    // Maximum AND is maximum element
    $maxAnd = max($a);

    // Maximum OR is bitwise OR of all.
    $maxOR = 0;
    for($i = 0; $i < $n; $i++)
        $maxOR|= $a[$i];

    print($maxAnd + $maxOR);
}

// Driver code
$n = 4;
$a = array(3, 5, 6, 1);
maxSum($a, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the maximum sum
function maxSum(a, n)
{

    // Maximum AND is maximum element
    var maxAnd = Math.max(...a);

    // Maximum OR is bitwise OR of all.
    var maxOR = 0;
    for(var i = 0; i < n; i++)
    {
        maxOR |= a[i];
    }
    document.write((maxAnd + maxOR));
}

// Driver code
var n = 4;
var a = [ 3, 5, 6, 1];

maxSum(a, n);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
13
```