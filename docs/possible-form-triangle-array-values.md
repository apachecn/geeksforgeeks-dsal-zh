# 可以从数组值

形成三角形

> 原文:[https://www . geesforgeks . org/可能形式-三角形-数组-值/](https://www.geeksforgeeks.org/possible-form-triangle-array-values/)

给定一个整数数组，我们需要找出是否有可能使用数组值作为边来构造至少一个非[退化](https://en.wikipedia.org/wiki/Degeneracy_(mathematics)#Triangle)三角形。换句话说，我们需要找出 3 个这样的数组索引，它们可以成为非退化三角形的边。
**例:**

```
Input : [4, 1, 2]
Output : No 
No triangle is possible from given
array values

Input : [5, 4, 3, 1, 2]
Output : Yes
Sides of possible triangle are 2 3 4
```

对于非退化三角形，其边应遵循这些约束，

```
A + B > C    and     
B + C > A    and
C + A > B
where A, B and C are length of sides of the triangle.
```

任务是从数组中找到满足上述条件的任何三元组。
一个**简单的解决方案**是生成所有的三元组，对于每个三元组，通过检查以上三个条件来检查它是否形成三角形。
一种**高效解决方案**是使用分拣。首先，我们对数组进行排序，然后我们循环一次，如果任何三元组满足 arr[i] + arr[i+1] > arr[i+2]，我们将检查该数组的三个连续元素，然后我们将输出该三元组作为最终结果。
***为什么只检查 3 个连续的元素就行了，而不是尝试排序数组的所有可能的三元组？***
假设我们在索引 I，3 个线段是 arr[i]、arr[i + 1]和 arr[i + 2]，关系 arr[i]<arr[i+1]<arr[i+2]，如果它们不能形成非退化三角形，那么长度为 arr[i-1]、arr[I+1]和 arr[I+2]或 arr[I]的线段， arr[i+1]和 arr[i+3]也不能形成非退化三角形，因为在第一种情况下 arr[i-1]和 arr[i+1]之和将甚至小于 arr[i]和 arr[i+1]之和，在第二种情况下 arr[i]和 arr[i+1]之和必须小于 arr[i+3]，所以我们不需要尝试所有的组合，我们将只尝试排序形式的数组的 3 个连续索引。
下面解的总复杂度为 O(n log n)

## C++

```
// C++ program to find if it
// is possible to form a
// triangle from array values
#include <bits/stdc++.h>
using namespace std;

// Method prints possible
// triangle when array values
// are taken as sides
bool isPossibleTriangle(int arr[],
                        int N)
{
    // If number of elements are
    // less than 3, then no
    // triangle is possible
    if (N < 3)
    return false;

    // first sort the array
    sort(arr, arr + N);

    // loop for all 3
    // consecutive triplets
    for (int i = 0; i < N - 2; i++)

        // If triplet satisfies
        // triangle condition, break
        if (arr[i] + arr[i + 1] > arr[i + 2])
            return true;
return false;
}

// Driver Code
int main()
{
    int arr[] = {5, 4, 3, 1, 2};
    int N = sizeof(arr) / sizeof(int);

    isPossibleTriangle(arr, N) ? cout << "Yes" :
                                 cout << "No";
    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to find if it is
// possible to form a triangle
// from array values
import java.io.*;
import java.util.Arrays;

class GFG
{

    // Method prints possible
    // triangle when array values
    // are taken as sides
    static boolean isPossibleTriangle(int []arr,
                                      int N)
    {

        // If number of elements are
        // less than 3, then no
        // triangle is possible
        if (N < 3)
            return false;

        // first sort the array
        Arrays.sort(arr);

        // loop for all 3
        // consecutive triplets
        for (int i = 0; i < N - 2; i++)

            // If triplet satisfies
            // triangle condition, break
            if (arr[i] + arr[i + 1] > arr[i + 2])
                return true;

        return false;
    }

    // Driver Code
    static public void main (String[] args)
    {
        int []arr = {5, 4, 3, 1, 2};
        int N = arr.length;

        if(isPossibleTriangle(arr, N))
            System.out.println("Yes" );
        else
            System.out.println("No");
    }
}

// This code is contributed by vt_m.
```

## 计算机编程语言

```
# Python3 code to find if
# it is possible to form a
# triangle from array values

# Method prints possible
# triangle when array
# values are taken as sides
def isPossibleTriangle (arr , N):

    # If number of elements
    # are less than 3, then
    # no triangle is possible
    if N < 3:
        return False

    # first sort the array
    arr.sort()

    # loop for all 3
    # consecutive triplets
    for i in range(N - 2):

        # If triplet satisfies triangle
        # condition, break
        if arr[i] + arr[i + 1] > arr[i + 2]:
            return True

# Driver Code
arr = [5, 4, 3, 1, 2]
N = len(arr)
print("Yes" if isPossibleTriangle(arr, N) else "No")

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find if
// it is possible to form
// a triangle from array values
using System;

class GFG
{

    // Method prints possible
    // triangle when array values
    // are taken as sides
    static bool isPossibleTriangle(int []arr,
                                   int N)
    {
        // If number of elements
        // are less than 3, then
        // no triangle is possible
        if (N < 3)
            return false;

        // first sort the array
        Array.Sort(arr);

        // loop for all 3
        // consecutive triplets
        for (int i = 0; i < N - 2; i++)

            // If triplet satisfies triangle
            // condition, break
            if (arr[i] + arr[i + 1] > arr[i + 2])
                return true;

        return false;
    }

    // Driver Code
    static public void Main ()
    {
        int []arr = {5, 4, 3, 1, 2};
        int N = arr.Length;

        if(isPossibleTriangle(arr, N))
            Console.WriteLine("Yes" );
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if
// it is possible to form
// a triangle from array values

// Method prints possible
// triangle when array values
// are taken as sides
function isPossibleTriangle( $arr, $N)
{
    // If number of elements are
    // less than 3, then no
    // triangle is possible
    if ($N < 3)
    return false;

    // first sort the array
    sort($arr);

    // loop for all 3
    // consecutive triplets
    for ( $i = 0; $i < $N - 2; $i++)

        // If triplet satisfies triangle
        // condition, break
        if ($arr[$i] + $arr[$i + 1] > $arr[$i + 2])
            return true;
}

// Driver Code
$arr = array(5, 4, 3, 1, 2);
$N = count($arr);

if(isPossibleTriangle($arr,$N))
echo "Yes" ;
else               
echo "No";

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>
// Javascript program to find if it is
// possible to form a triangle
// from array values

    // Method prints possible
    // triangle when array values
    // are taken as sides
    function isPossibleTriangle(arr, N)
    {

        // If number of elements are
        // less than 3, then no
        // triangle is possible
        if (N < 3)
            return false;

        // first sort the array
        arr.sort();

        // loop for all 3
        // consecutive triplets
        for (let i = 0; i < N - 2; i++)

            // If triplet satisfies
            // triangle condition, break
            if (arr[i] + arr[i + 1] > arr[i + 2])
                return true;

        return false;
    }

// Driver code   

        let arr = [5, 4, 3, 1, 2];
        let N = arr.length;

        if(isPossibleTriangle(arr, N))
            document.write("Yes" );
        else
            document.write("No");

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
Yes
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。