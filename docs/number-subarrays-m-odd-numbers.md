# m 个奇数子阵的数量

> 原文:[https://www . geesforgeks . org/number-subarrays-m-odd-numbers/](https://www.geeksforgeeks.org/number-subarrays-m-odd-numbers/)

给定一个由 n 个元素和一个整数 m 组成的数组，我们需要编写一个程序来找出数组中恰好包含 m 个奇数的连续子数组的数量。

**示例:**

> **输入:** arr = {2，5，6，9}，m = 2
> **输出:** 2
> **解释:**
> 子阵为【2，5，6，9】
> 和【5，6，9】
> 
> **输入:** arr = {2，2，5，6，9，2，11}，m = 2
> **输出:** 8
> **解释:**
> 子阵为【2，2，5，6，9】，
> 【2，5，6，9】，【5，6，9】，【2，2，5，6，9，2】，
> 【2，5，6，9，2】，【5，6，6，2】

**天真法**:天真法是生成所有可能的子阵，同时检查 m 个奇数的子阵。
以下是上述办法的实施情况:

## C++

```
// CPP program to count the
// Number of subarrays with
// m odd numbers
#include <bits/stdc++.h>
using namespace std;

// function that returns
// the count of subarrays
// with m odd numbers
int countSubarrays(int a[], int n, int m)
{
    int count = 0;

    // traverse for all
    // possible subarrays
    for (int i = 0; i < n; i++)
    {
        int odd = 0;
        for (int j = i; j < n; j++)
        {
            if (a[j] % 2)
                odd++;

            // if count of odd numbers in
            // subarray is m
            if (odd == m)
                count++;
        }
    }
    return count;
}

// Driver Code
int main()
{
    int a[] = { 2, 2, 5, 6, 9, 2, 11 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = 2;

    cout << countSubarrays(a, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of
// subarrays with m odd numbers
import java.util.*;

class GFG {

    // function that returns the count of
    // subarrays with m odd numbers
    static int countSubarrays(int a[], int n, int m)
    {

        int count = 0;

        // traverse for all possible
        // subarrays
        for (int i = 0; i < n; i++)
        {
            int odd = 0;
            for (int j = i; j < n; j++)
            {
                if (a[j] % 2 != 0)
                    odd++;

                // if count of odd numbers
                // in subarray is m
                if (odd == m)
                    count++;
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 2, 5, 6, 9, 2, 11 };
        int n = a.length;
        int m = 2;

        System.out.println(countSubarrays(a, n, m));
    }
}

// This code is contributed by akash1295.
```

## 蟒蛇 3

```
# Python3 program to count the
# Number of subarrays with
# m odd numbers

# function that returns the count
# of subarrays with m odd numbers

def countSubarrays(a, n, m):
    count = 0

    # traverse for all
    # possible subarrays
    for i in range(n):
        odd = 0
        for j in range(i, n):
            if (a[j] % 2):
                odd += 1

            # if count of odd numbers
            # in subarray is m
            if (odd == m):
                count += 1
    return count

# Driver Code
a = [2, 2, 5, 6, 9, 2, 11]
n = len(a)
m = 2

print(countSubarrays(a, n, m))

# This code is contributed by mits
```

## C#

```
// C# program to count the number of
// subarrays with m odd numbers
using System;

class GFG {

    // function that returns the count of
    // subarrays with m odd numbers
    static int countSubarrays(int[] a, int n, int m)
    {

        int count = 0;

        // traverse for all possible
        // subarrays
        for (int i = 0; i < n; i++)
        {
            int odd = 0;
            for (int j = i; j < n; j++)
            {
                if (a[j] % 2 == 0)
                    odd++;

                // if count of odd numbers
                // in subarray is m
                if (odd == m)
                    count++;
            }
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 2, 2, 5, 6, 9, 2, 11 };
        int n = a.Length;
        int m = 2;

        Console.WriteLine(countSubarrays(a, n, m));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the
// Number of subarrays with
// m odd numbers

// function that returns the count
// of subarrays with m odd numbers
function countSubarrays( $a, $n, $m)
{
    $count = 0;

    // traverse for all
    // possible subarrays
    for ( $i = 0; $i < $n; $i++)
    {
        $odd = 0;
        for ( $j = $i; $j < $n; $j++)
        {
            if ($a[$j] % 2)
                $odd++;

            // if count of odd numbers in
            // subarray is m
            if ($odd == $m)
                $count++;
        }
    }
    return $count;
}

// Driver Code
$a = array( 2, 2, 5, 6, 9, 2, 11 );
$n = count($a);
$m = 2;

echo countSubarrays($a, $n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to count the number of
// subarrays with m odd numbers

    // function that returns the count of
    // subarrays with m odd numbers
    function countSubarrays(a,  n, m)
    {

        var count = 0;

        // traverse for all possible
        // subarrays
        for (var i = 0; i < n; i++)
        {
            var odd = 0;
            for (var j = i; j < n; j++)
            {
                if (a[j] % 2 == 0)
                    odd++;

                // if count of odd numbers
                // in subarray is m
                if (odd == m)
                    count++;
            }
        }

        return count;
    }

    // Driver code
        var a = [ 2, 2, 5, 6, 9, 2, 11 ];
        var n = a.length;
        var m = 2;

        document.write(countSubarrays(a, n, m));

// This code is contributed by bunnyram19.

</script>
```

**输出:**

```
8
```

**时间复杂度:** O(n <sup>2</sup>

**有效方法:**一种有效方法是在遍历时，计算**前缀[]** 数组。前缀[i]存储其中有**‘I’**奇数的前缀数。如果数组元素是奇数，我们增加奇数的计数。当奇数的计数超过或等于 m 时，将带有**(奇数-m)**数字的前缀数加到答案中。在每一步奇数> =m 处，我们借助前缀数组计算形成特定索引的子数组的数量。prefix[odd-m]为我们提供了具有“odd-m”奇数的前缀数量，将其添加到计数中以获得直到索引的子阵列数量。
以下是上述方法的实施:

## C++

```
// CPP program to count the Number
// of subarrays with m odd numbers
// O(N) approach
#include <bits/stdc++.h>
using namespace std;

// function that returns the count
// of subarrays with m odd numbers
int countSubarrays(int a[], int n, int m)
{
    int count = 0;
    int prefix[n + 1] = { 0 };
    int odd = 0;

    // traverse in the array
    for (int i = 0; i < n; i++)
    {

        prefix[odd]++;

        // if array element is odd
        if (a[i] & 1)
            odd++;

        // when number of odd elements>=M
        if (odd >= m)
            count += prefix[odd - m];
    }

    return count;
}

// Driver Code
int main()
{
    int a[] = { 2, 2, 5, 6, 9, 2, 11 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = 2;

    cout << countSubarrays(a, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// number of subarrays with
// m odd numbers
import java.util.*;

class GFG {

    // function that returns the count of
    // subarrays with m odd numbers
    public static int countSubarrays(int a[], int n, int m)
    {
        int count = 0;
        int prefix[] = new int[n + 1];
        int odd = 0;

        // Traverse in the array
        for (int i = 0; i < n; i++)
        {
            prefix[odd]++;

            // If array element is odd
            if ((a[i] & 1) == 1)
                odd++;

            // When number of odd
            // elements >= M
            if (odd >= m)
                count += prefix[odd - m];
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 2, 5, 6, 9, 2, 11 };
        int n = a.length;
        int m = 2;

        // Function call
        System.out.println(countSubarrays(a, n, m));
    }
}

// This code is contributed by akash1295.
```

## 蟒蛇 3

```
# Python3 program to count the Number
# of subarrays with m odd numbers
# O(N) approach

# function that returns the count
# of subarrays with m odd numbers

def countSubarrays(a, n, m):
    count = 0
    prefix = [0] * (n+1)
    odd = 0

    # traverse in the array
    for i in range(n):
        prefix[odd] += 1

        # if array element is odd
        if (a[i] & 1):
            odd += 1

        # when number of odd elements>=M
        if (odd >= m):
            count += prefix[odd - m]

    return count

# Driver Code
a = [2, 2, 5, 6, 9, 2, 11]
n = len(a)
m = 2

print(countSubarrays(a, n, m))

# This code is contributed 29Ajaykumar
```

## C#

```
// C# program to count the number of
// subarrays with m odd numbers
using System;

class GFG {

    // function that returns the count of
    // subarrays with m odd numbers
    public static int countSubarrays(int[] a, int n, int m)
    {
        int count = 0;
        int[] prefix = new int[n + 1];
        int odd = 0;

        // traverse in the array
        for (int i = 0; i < n; i++)
        {
            prefix[odd]++;

            // if array element is odd
            if ((a[i] & 1) == 1)
                odd++;

            // when number of odd
            // elements >= M
            if (odd >= m)
                count += prefix[odd - m];
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 2, 2, 5, 6, 9, 2, 11 };
        int n = a.Length;
        int m = 2;

        Console.WriteLine(countSubarrays(a, n, m));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the Number
// of subarrays with m odd numbers
// O(N) approach

// function that returns the count
// of subarrays with m odd numbers
function countSubarrays(&$a, $n, $m)
{
    $count = 0;
    $prefix[$n+1] = array();
    $odd = 0;

    // traverse in the array
    for ($i = 0; $i < $n; $i++)
    {

        $prefix[$odd]++;

        // if array element is odd
        if ($a[$i] & 1)
            $odd++;

        // when number of odd elements>=M
        if ($odd >= $m)
            $count += $prefix[$odd - $m];
    }

    return $count;
}

// Driver Code
$a = array(2, 2, 5, 6, 9, 2, 11 );
$n = sizeof($a);
$m = 2;

echo countSubarrays($a, $n, $m);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript program to count the number of
    // subarrays with m odd numbers

    // function that returns the count of
    // subarrays with m odd numbers
    function countSubarrays(a, n, m)
    {
        let count = 0;
        let prefix = new Array(n + 1);
        prefix.fill(0);
        let odd = 0;

        // traverse in the array
        for (let i = 0; i < n; i++)
        {
            prefix[odd]++;

            // if array element is odd
            if ((a[i] & 1) == 1)
                odd++;

            // when number of odd
            // elements >= M
            if (odd >= m)
                count += prefix[odd - m];
        }

        return count;
    }

    let a = [ 2, 2, 5, 6, 9, 2, 11 ];
    let n = a.length;
    let m = 2;

    document.write(countSubarrays(a, n, m));

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
8
```

**时间复杂度:** O(n)