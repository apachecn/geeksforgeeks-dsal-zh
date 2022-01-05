# 寻找数组中 GCD 最大的对

> 原文:[https://www.geeksforgeeks.org/find-pair-maximum-gcd-array/](https://www.geeksforgeeks.org/find-pair-maximum-gcd-array/)

给我们一个正整数数组。找到阵列中 GCD 最大的对。
**例:**

```
Input : arr[] : { 1 2 3 4 5 }
Output : 2
Explanation : Pair {2, 4} has GCD 2 which is highest. Other pairs have a GCD of 1.

Input : arr[] : { 2 3 4 8 8 11 12 }
Output : 8
Explanation : Pair {8, 8} has GCD 8 which is highest.
```

**方法 1(蛮力)**:解决这个问题最简单的方法就是用两个循环生成数组所有可能的元素对，同时计算比较 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。我们可以使用[扩展欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)来有效地计算两个数的 GCD。
**时间复杂度** : O(N^2 * log(max(a，b)))
这里，log(max(a，b))是计算 a 和 b 的 GCD 的时间复杂度。
**方法 2:(高效)**在这个方法中，我们维护一个计数数组来存储每个元素的除数。我们将遍历给定的数组，对于每个元素，我们将在计数数组的索引处计算它的除数和增量。计算除数的过程将花费 O(sqrt(arr[i])时间，其中 arr[i]是索引 I 处给定数组中的元素。在整个遍历之后，我们可以简单地从最后一个索引遍历计数数组到索引 1。如果我们发现一个指数的值大于 1，那么这意味着它是 2 个元素的除数，也是最大 GCD。
以下是上述方法的实施:

## C++

```
// C++ Code to find pair with
// maximum GCD in an array
#include <bits/stdc++.h>

using namespace std;

// function to find GCD of pair with
// max GCD in the array
int findMaxGCD(int arr[], int n)
{
    // Computing highest element
    int high = 0;
    for (int i = 0; i < n; i++)
        high = max(high, arr[i]);

    // Array to store the count of divisors
    // i.e. Potential GCDs
    int divisors[high + 1] = { 0 };

    // Iterating over every element
    for (int i = 0; i < n; i++)
    {
        // Calculating all the divisors
        for (int j = 1; j <= sqrt(arr[i]); j++)
        {
            // Divisor found
            if (arr[i] % j == 0)
            {
                // Incrementing count for divisor
                divisors[j]++;

                // Element/divisor is also a divisor
                // Checking if both divisors are
                // not same
                if (j != arr[i] / j)
                    divisors[arr[i] / j]++;
            }
        }
    }

    // Checking the highest potential GCD
    for (int i = high; i >= 1; i--)

        // If this divisor can divide at least 2
        // numbers, it is a GCD of at least 1 pair
        if (divisors[i] > 1)
            return i;   
}

// Driver code
int main()
{
    // Array in which pair with max GCD
    // is to be found
    int arr[] = { 1, 2, 4, 8, 8, 12 };

    // Size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMaxGCD(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Find pair with maximum GCD in an array
class GFG {

    // function to find GCD of pair with
    // max GCD in the array
    public static int findMaxGCD(int arr[], int n)
    {
        // Computing highest element
        int high = 0;
        for (int i = 0; i < n; i++)
            high = Math.max(high, arr[i]);

        // Array to store the count of divisors
        // i.e. Potential GCDs
        int divisors[] =new int[high + 1];

        // Iterating over every element
        for (int i = 0; i < n; i++)
        {
            // Calculating all the divisors
            for (int j = 1; j <= Math.sqrt(arr[i]); j++)
            {
                // Divisor found
                if (arr[i] % j == 0)
                {
                    // Incrementing count for divisor
                    divisors[j]++;

                    // Element/divisor is also a divisor
                    // Checking if both divisors are
                    // not same
                    if (j != arr[i] / j)
                        divisors[arr[i] / j]++;
                }
            }
        }

        // Checking the highest potential GCD
        for (int i = high; i >= 1; i--)

            // If this divisor can divide at least 2
            // numbers, it is a GCD of at least 1 pair
            if (divisors[i] > 1)
                return i;
        return 1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        // Array in which pair with max GCD
        // is to be found
        int arr[] = { 1, 2, 4, 8, 8, 12 };

        // Size of array
        int n = arr.length;

        System.out.println(findMaxGCD(arr,n));
    }
  }

// This code is contributed by Arnav Kr. Mandal.
```

## 计算机编程语言

```
# Python program to Find pair with
# maximum GCD in an array
import math

# function to find GCD of pair with
# max GCD in the array
def findMaxGCD(arr, n) :

    # Computing highest element
    high = 0
    i = 0
    while i < n :
        high = max(high, arr[i])
        i = i + 1

    # Array to store the count of divisors
    # i.e. Potential GCDs
    divisors = [0] * (high + 1)

    # Iterating over every element
    i = 0
    while i < n :

        # Calculating all the divisors
        j = 1
        while j <= math.sqrt(arr[i]) :

            # Divisor found
            if (arr[i] % j == 0) :

                # Incrementing count for divisor
                divisors[j]= divisors[j]+1

                # Element/divisor is also a divisor
                # Checking if both divisors are
                # not same
                if (j != arr[i] / j) :
                    divisors[arr[i] / j] = divisors[arr[i] / j]
                                          + 1

            j = j + 1

        i = i + 1           

    # Checking the highest potential GCD
    i = high
    while i >= 1 :

        # If this divisor can divide at least 2
        # numbers, it is a GCD of at least 1 pair
        if (divisors[i] > 1) :
            return i
        i = i - 1
    return 1

# Driver code

# Array in which pair with max GCD
# is to be found
arr = [ 1, 2, 4, 8, 8, 12 ]

# Size of array
n = len(arr)

print findMaxGCD(arr,n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Code for Find pair with
// maximum GCD in an array
using System;

class GFG {

    // Function to find GCD of pair
    // with max GCD in the array
    public static int findMaxGCD(int []arr,
                                 int n)
    {
        // Computing highest element
        int high = 0;
        for (int i = 0; i < n; i++)
            high = Math.Max(high, arr[i]);

        // Array to store the count of
        // divisors i.e. Potential GCDs
        int []divisors =new int[high + 1];

        // Iterating over every element
        for (int i = 0; i < n; i++)
        {
            // Calculating all the divisors
            for (int j = 1; j <=
                 Math.Sqrt(arr[i]); j++)
            {
                // Divisor found
                if (arr[i] % j == 0)
                {
                    // Incrementing count
                    // for divisor
                    divisors[j]++;

                    // Element / divisor is also
                    // a divisor Checking if both
                    // divisors are not same
                    if (j != arr[i] / j)
                        divisors[arr[i] / j]++;
                }
            }
        }

        // Checking the highest potential GCD
        for (int i = high; i >= 1; i--)

            // If this divisor can divide at
            // least 2 numbers, it is a
            // GCD of at least 1 pair
            if (divisors[i] > 1)
                return i;
        return 1;
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Array in which pair with
        // max GCD is to be found
        int []arr = {1, 2, 4, 8, 8, 12};

        // Size of array
        int n = arr.Length;

        Console.WriteLine(findMaxGCD(arr,n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code for Find pair with
// maximum GCD in an array

// Function to find GCD
// of pair with max GCD
// in the array
function findMaxGCD($arr, $n)
{
    // Computing highest element
    $high = 0;
    for ($i = 0; $i < $n; $i++)
        $high = max($high, $arr[$i]);

    // Array to store the
    // count of divisors
    // i.e. Potential GCDs
    $divisors = array_fill(0, $high + 1, 0);

    // Iterating over every element
    for ($i = 0; $i < $n; $i++)
    {
        // Calculating all
        // the divisors
        for ($j = 1;
             $j <= (int)(sqrt($arr[$i])); $j++)
        {
            // Divisor found
            if ($arr[$i] % $j == 0)
            {
                // Incrementing count
                // for divisor
                $divisors[$j]++;

                // Element/divisor is also
                // a divisor Checking if
                // both divisors are not same
                if ($j != (int)($arr[$i] / $j))
                    $divisors[(int)($arr[$i] / $j)]++;
            }
        }
    }

    // Checking the highest
    // potential GCD
    for ($i = $high; $i >= 1; $i--)

        // If this divisor can divide
        // at least 2 numbers, it is
        // a GCD of at least 1 pair
        if ($divisors[$i] > 1)
            return $i;
}

// Driver code

// Array in which pair
// with max GCD is to
// be found
$arr = array( 1, 2, 4, 8, 8, 12 );

// Size of array
$n = sizeof($arr);

echo findMaxGCD($arr,$n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript Code for Find pair with
// maximum GCD in an array

// function to find GCD of pair with
// max GCD in the array
function findMaxGCD(arr , n)
{
    // Computing highest element
    var high = 0;
    for (var i = 0; i < n; i++)
        high = Math.max(high, arr[i]);

    // Array to store the count of divisors
    // i.e. Potential GCDs
    var divisors =
    Array.from({length: high + 1}, (_, i) => 0);

    // Iterating over every element
    for (var i = 0; i < n; i++)
    {
        // Calculating all the divisors
        for (var j = 1; j <= Math.sqrt(arr[i]); j++)
        {
            // Divisor found
            if (arr[i] % j == 0)
            {
                // Incrementing count for divisor
                divisors[j]++;

                // Element/divisor is also a divisor
                // Checking if both divisors are
                // not same
                if (j != arr[i] / j)
                    divisors[arr[i] / j]++;
            }
        }
    }

    // Checking the highest potential GCD
    for (var i = high; i >= 1; i--)

        // If this divisor can divide at least 2
        // numbers, it is a GCD of at least 1 pair
        if (divisors[i] > 1)
            return i;
    return 1;
}

/* Driver program to test above function */
 // Array in which pair with max GCD
// is to be found
    var arr = [ 1, 2, 4, 8, 8, 12 ];

    // Size of array
    var n = arr.length;

    document.write(findMaxGCD(arr,n));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
8
```

**时间复杂度** : O(N * sqrt(arr[i]) + H，其中 arr[i]表示数组的元素，H 表示数组的最大数。
**方法 3(最有效率)**:这个方法是基于厄拉多塞的[筛的思路。
首先我们来解决一个比较简单的问题，给定一个值 X，我们要判断一对是否有等于 X 的 GCD，这可以通过检查数组中有多少元素是 X 的倍数来完成，如果这样的倍数的个数大于 1，那么 X 将是某一对的 GCD。
现在对于 GCD 最大的对，我们维护一个原始数组的计数数组。我们的方法是基于上述问题，用类似筛子的方法进行循环。下面是这种方法的分步算法:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

1.  将“I”从 MAX(最大数组元素)迭代到 1。
2.  将“j”从“I”迭代到 MAX。我们将检查索引“j”处的计数数组是否为 1。
3.  每次用“I”递增索引“j”。这样，我们可以检查
    i、2i、3i 等等。
4.  如果我们在计数数组中得到 1 的两倍，这意味着**存在 I 的 2 倍**。这使它成为最高的 GCD。

以下是上述方法的实现:

## C++

```
// C++ Code to
// Find pair with
// maximum GCD in
// an array
#include <bits/stdc++.h>
using namespace std;

// function to find
// GCD of pair with
// max GCD in the
// array
int findMaxGCD(int arr[], int n)
{
    // Calculating MAX in array
    int high = 0;
    for (int i = 0; i < n; i++)
        high = max(high, arr[i]);

    // Maintaining count array
    int count[high + 1] = {0};
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    // Variable to store the
    // multiples of a number
    int counter = 0;

    // Iterating from MAX to 1
    // GCD is always between
    // MAX and 1\. The first
    // GCD found will be the
    // highest as we are
    // decrementing the potential
    // GCD
    for (int i = high; i >= 1; i--)
    {
        int j = i;
       counter = 0;

        // Iterating from current
        // potential GCD
        // till it is less than
        // MAX
        while (j <= high)
        {
            // A multiple found

            if(count[j] >=2)
               return j;

           else if (count[j] == 1)        
                counter++;        

            // Incrementing potential
            // GCD by itself
            // To check i, 2i, 3i....
            j += i;

            // 2 multiples found,
            // max GCD found
            if (counter == 2)        
                return i;
        }
    }
}

// Driver code
int main()
{
    // Array in which pair
    // with max GCD is to
    // be found
    int arr[] = { 1, 2, 4, 8, 8, 12 };

    // Size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMaxGCD(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code to
// Find pair with
// maximum GCD in
// an array

class GFG {

    // function to find
    // GCD of pair with
    // max GCD in the
    // array
    public static int findMaxGCD(int arr[], int n)
    {
        // Calculating MAX in
        // array
        int high = 0;
        for (int i = 0; i < n; i++)
            high = Math.max(high, arr[i]);

        // Maintaining count array
        int count[]=new int[high + 1];
        for (int i = 0; i < n; i++)
            count[arr[i]]++;

        // Variable to store
        // the multiples of
        // a number
        int counter = 0;

        // Iterating from MAX
        // to 1 GCD is always
        // between MAX and 1
        // The first GCD found
        // will be the highest
        // as we are decrementing
        // the potential GCD
        for (int i = high; i >= 1; i--)
        {
            int j = i;

            // Iterating from current
            // potential GCD till it
            // is less than MAX
            while (j <= high)
            {
                // A multiple found
                if (count[j]>0)    
                    counter+=count[j];        

                // Incrementing potential
                // GCD by itself
                // To check i, 2i, 3i....
                j += i;

                // 2 multiples found,
                // max GCD found
                if (counter == 2)        
                    return i;
            }
            counter=0;
        }
    return 1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        // Array in which pair
        // with max GCD is to
        // be found
        int arr[] = {1, 2, 4, 8, 8, 12};

        // Size of array
        int n = arr.length;

        System.out.println(findMaxGCD(arr,n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 Code to
# Find pair with
# maximum GCD in
# an array

# function to find
# GCD of pair with
# max GCD in the
# array
def findMaxGCD(arr, n) :

    # Calculating MAX in
    # array
    high = 0
    for i in range(0, n) :
        high = max(high, arr[i])

    # Maintaining count array
    count = [0] * (high + 1)
    for i in range(0, n) :
        count[arr[i]]+=1

    # Variable to store the
    # multiples of a number
    counter = 0

    # Iterating from MAX
    # to 1 GCD is always
    # between MAX and 1
    # The first GCD found
    # will be the highest
    # as we are decrementing
    # the potential GCD
    for i in range(high, 0, -1) :
        j = i

        # Iterating from current
        # potential GCD till it
        # is less than MAX
        while (j <= high) :

            # A multiple found
            if (count[j] >0) :
                counter+=count[j]   

            # Incrementing potential
            # GCD by itself
            # To check i, 2i, 3i....
            j += i

            # 2 multiples found,
            # max GCD found
            if (counter == 2) :
                return i
        counter=0

# Driver code

# Array in which pair
# with max GCD is to
# be found
arr = [1, 2, 4, 8, 8, 12]
# Size of array
n = len(arr)
print(findMaxGCD(arr, n))

#This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Code to find pair with
// maximum GCD in an array
using System;

class GFG {

    // function to find GCD
    // of pair with max
    // max GCD in the array
    public static int findMaxGCD(int []arr,
                                int n)
    {
        // Calculating Max
        // in array
        int high = 0;
        for (int i = 0; i < n; i++)
            high = Math.Max(high, arr[i]);

        // Maintaining count array
        int []count=new int[high + 1];
        for (int i = 0; i < n; i++)
            count[arr[i]]++;

        // Variable to store
        // the multiples of
        // a number
        int counter = 0;

        // Iterating from MAX
        // to 1 GCD is always
        // between MAX and 1
        // The first GCD found
        // will be the highest
        // as we are decrementing
        // the potential GCD
        for (int i = high; i >= 1; i--)
        {
            int j = i;

            // Iterating from current
            // potential GCD till it
            // is less than MAX
            while (j <= high)
            {
                // A multiple found
                if (count[j]>0)    
                    counter+=count[j];    

                // Incrementing potential
                // GCD by itself
                // To check i, 2i, 3i....
                j += i;

                // 2 multiples found,
                // max GCD found
                if (counter == 2)    
                    return i;
            }
            counter=0;
        }
    return 1;
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Array in which pair
        // with max GCD is to
        // be found
        int []arr = {1, 2, 4, 8, 8, 12};

        // Size of array
        int n = arr.Length;

        Console.WriteLine(findMaxGCD(arr,n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code to Find pair with maximum
// GCD in an array

// function to find GCD of pair with
// max GCD in the array
function findMaxGCD($arr, $n)
{
    // Calculating MAX in array
    $high = 0;
    for ($i = 0; $i < $n; $i++)
        $high = max($high, $arr[$i]);

    // Maintaining count array
    $count = array_fill(0, $high + 1, 0);
    for ($i = 0; $i < $n; $i++)
        $count[$arr[$i]]++;

    // Variable to store the multiples
    // of a number
    $counter = 0;

    // Iterating from MAX to 1 GCD is always
    // between MAX and 1\. The first GCD found
    // will be the highest as we are decrementing
    // the potential GCD
    for ($i = $high; $i >= 1; $i--)
    {
        $j = $i;
        $counter = 0;

        // Iterating from current potential GCD
        // till it is less than MAX
        while ($j <= $high)
        {
            // A multiple found

            if($count[$j] >= 2)
            return $j;

        else if ($count[$j] == 1)    
                $counter++;    

            // Incrementing potential GCD by itself
            // To check i, 2i, 3i....
            $j += $i;

            // 2 multiples found, max GCD found
            if ($counter == 2)    
                return $i;
        }
    }
}

// Driver code

// Array in which pair with max GCD
// is to be found
$arr = array( 1, 2, 4, 8, 8, 12 );

// Size of array
$n = count($arr);

print(findMaxGCD($arr, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript Code to
// Find pair with
// maximum GCD in
// an array

    // function to find
    // GCD of pair with
    // max GCD in the
    // array
    function findMaxGCD(arr , n)
    {

        // Calculating MAX in
        // array
        var high = 0;
        for (let i = 0; i < n; i++)
            high = Math.max(high, arr[i]);

        // Maintaining count array
         var count = Array(high + 1).fill(0);
    for (let i = 0; i < n; i++)
        count[arr[i]]++;

        // Variable to store
        // the multiples of
        // a number
        var counter = 0;

        // Iterating from MAX
        // to 1 GCD is always
        // between MAX and 1
        // The first GCD found
        // will be the highest
        // as we are decrementing
        // the potential GCD
        for (let i = high; i >= 1; i--)
        {
            var j = i;

            // Iterating from current
            // potential GCD till it
            // is less than MAX
            while (j <= high)
            {

                // A multiple found
                if (count[j] > 0)
                    counter += count[j];

                // Incrementing potential
                // GCD by itself
                // To check i, 2i, 3i....
                j += i;

                // 2 multiples found,
                // max GCD found
                if (counter == 2)
                    return i;
            }
            counter = 0;
        }
        return 1;
    }

    /* Driver program to test above function */

        // Array in which pair
        // with max GCD is to
        // be found
        var arr = [ 1, 2, 4, 8, 8, 12 ];

        // Size of array
        var n = arr.length;
        document.write(findMaxGCD(arr, n));

// This code is contributed by aashish1995
</script>
```

**输出:**

```
8
```

**时间复杂度**:这种方法的时间复杂度直到一个被称为狄利克雷除数问题的开放问题。
本文由 [**罗希特·塔普利亚尔**](https://www.linkedin.com/in/rohit-thapliyal-515b5913a/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。