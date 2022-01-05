# 找到包含所有元素顺序相同的最小子阵列

> 原文:[https://www . geesforgeks . org/find-minist-subarray-contains-elements-order/](https://www.geeksforgeeks.org/find-smallest-subarray-contains-elements-order/)

给定两个大小为 m 和 n 的整数数组，任务是在包含第二个数组所有元素的第一个数组中找到最小长度的子数组。
注意:第二个数组的元素可能以不连续的方式出现在大数组中，但顺序必须相同。(m < n )
**例:**

```
Input :  A[] = {2, 2, 4, 5, 8, 9}  
         B[] = {2, 5, 9}  
Output : 5
Smallest subarray of A[] that contains all
elements of B[] is {2, 4, 5, 8, 9} which is
of size 5.

Input :  A[] = {5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7}  
         B[] = {5, 5, 7}  
Output : 3
```

**方法 1(幼稚)**

一个简单的解决方案是生成给定阵列的所有子阵列，并检查每个子阵列是否包含另一个阵列的元素。最后，返回包含另一个数组的子数组的最小长度。
下面是上面思路的实现。

## C++

```
// CPP program to find smallest length
// subarray that contains all elements
// of another array.
#include <bits/stdc++.h>
using namespace std;

// function return the minimum length of sub_array
int minimumSubArray(int A[], int n, int B[], int m)
{
    int result = INT_MAX;

    // Pick starting point
    for (int i = 0; i < n; i++) {

        // Pick ending point
        for (int j = i; j < n; j++) {

            // k is index in first array and
            // 'index' is index in second array.
            int k, index = 0;
            for (k = i; k <= j; k++) {
                if (A[k] == B[index])
                    index++;
                if (index == m)
                    break;
            }

            // update minimum length sub_array
            if (index == m && result > k - i + 1)
              result = (k == n) ? k - i : k - i + 1;
        }
    }

    // return minimum length subarray
    return result;
}

// driver program to test above function
int main()
{
    int A[] = { 5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7 };
    int B[] = { 5, 5, 7 };
    int n = sizeof(A)/sizeof(A[0]);
    int m = sizeof(B)/sizeof(B[0]);
    cout << minimumSubArray(A, n, B, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest length
// subarray that contains all elements
// of another array.
import java.io.*;

class GFG {

// function return the minimum length
// of sub_array
static int minimumSubArray(int A[], int n,
                           int B[], int m)
{
    int result = Integer.MAX_VALUE;

    // Pick starting point
    for (int i = 0; i < n; i++) {

        // Pick ending point
        for (int j = i; j < n; j++) {

            // k is index in first array
            // and 'index' is index in
            // second array.
            int k, index = 0;
            for (k = i; k <= j; k++) {
                if (A[k] == B[index])
                    index++;
                if (index == m)
                    break;
            }

            // update minimum length sub_array
            if (index == m && result > k - i + 1)
            result = (k == n) ? k - i : k - i + 1;
        }
    }

    // return minimum length subarray
    return result;
}

// driver program to test above function
public static void main(String[] args)
{
    int A[] = { 5, 6, 5, 2, 7, 5,
                6, 7, 5, 5, 7 };
    int B[] = { 5, 5, 7 };
    int n = A.length;
    int m = B.length;
    System.out.println(minimumSubArray(A, n, B, m));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to find smallest
# length subarray that contains all
# elements of another array.

# function return the minimum length
# of sub_array
def minimumSubArray(A, n, B, m) :
    result = 10000000

    # Pick starting point
    for i in range(0, n) :

        # Pick ending point
        for j in range(0,n) :

            # k is index in first array and
            # 'index' is index in second array.
            index = 0
            for k in range(i, j + 1) :
                if (A[k] == B[index]) :
                    index=index + 1
                if (index == m) :
                    break

            # update minimum length sub_array
            if (index == m and result > k - i + 1) :
                if (k == n) :
                    result =  k - i
                else :
                    result = k - i + 1

    # return minimum length subarray
    return result

# driver program to test above function
A = [ 5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7 ]
B = [ 5, 5, 7 ]
n = len(A)
m = len(B)
print(minimumSubArray(A, n, B, m))

#This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to find smallest length
// subarray that contains all elements
// of another array.
using System;

class GFG {

// function return the minimum
// length of sub_array
static int minimumSubArray(int []A, int n,
                           int []B, int m)
{
    int result = int.MaxValue;

    // Pick starting point
    for (int i = 0; i < n; i++) {

        // Pick ending point
        for (int j = i; j < n; j++) {

            // k is index in first array
            // and 'index' is index in
            // second array.
            int k, index = 0;
            for (k = i; k <= j; k++) {
                if (A[k] == B[index])
                    index++;
                if (index == m)
                    break;
            }

            // update minimum length sub_array
            if (index == m && result > k - i + 1)
            result = (k == n) ? k - i : k - i + 1;
        }
    }

    // return minimum length subarray
    return result;
}

  // Driver code
  public static void Main()
  {
    int []A = { 5, 6, 5, 2, 7, 5,
                 6, 7, 5, 5, 7 };
    int []B = { 5, 5, 7 };
    int n = A.Length;
    int m = B.Length;
    Console.Write(minimumSubArray(A, n, B, m));
  }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest length
// subarray that contains all elements
// of another array.

// function return the minimum
// length of sub_array
function minimumSubArray($A, $n, $B, $m)
{

    $result = PHP_INT_MAX;

    // Pick starting point
    for ($i = 0; $i < $n; $i++)
    {

        // Pick ending point
        for ( $j = $i; $j < $n; $j++)
        {

            // k is index in first array and
            // 'index' is index in second array.
            $k; $index = 0;
            for ($k = $i; $k <= $j; $k++)
            {
                if ($A[$k] == $B[$index])
                    $index++;
                if ($index == $m)
                    break;
            }

            // update minimum length
            // sub_array
            if ($index == $m && $result > $k - $i + 1)
            $result = ($k == $n) ? $k - $i : $k - $i + 1;
        }
    }

    // return minimum length subarray
    return $result;
}

    // Driver Code
    $A = array(5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7);
    $B = array(5, 5, 7);
    $n = count($A);
    $m = count($B);
    echo minimumSubArray($A, $n, $B, $m);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find smallest length
// subarray that contains all elements
// of another array.

// function return the minimum length of sub_array
function minimumSubArray(A, n, B, m)
{
    var result = 1000000000;

    // Pick starting point
    for (var i = 0; i < n; i++) {

        // Pick ending point
        for (var j = i; j < n; j++) {

            // k is index in first array and
            // 'index' is index in second array.
            var k, index = 0;
            for (k = i; k <= j; k++) {
                if (A[k] == B[index])
                    index++;
                if (index == m)
                    break;
            }

            // update minimum length sub_array
            if (index == m && result > k - i + 1)
              result = (k == n) ? k - i : k - i + 1;
        }
    }

    // return minimum length subarray
    return result;
}

// driver program to test above function
var A = [ 5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7 ];
var B = [ 5, 5, 7 ];
var n = A.length;
var m = B.length;
document.write( minimumSubArray(A, n, B, m));

// This code is contributed by noob2000.
</script>
```

输出:

```
3
```

时间复杂度:O(n <sup>3</sup> )
辅助空间:O(1)

**方法 2(高效)**

方法 2 是方法 1 的优化版本。这里我们只考虑第一个元素与第二个数组的第一个元素匹配的子数组。如果第一个元素匹配，那么我们匹配 Main_array 中第二个数组的其余元素，如果所有元素匹配，那么如果需要，我们更新长度。最后，我们返回子数组的最小长度。
以下是上述思路的实现:

## C++

```
// C++ program to find smallest length
// subarray that contains all elements
// of another array.
#include <bits/stdc++.h>
using namespace std;

// Returns the minimum length of sub_array
int minimumSubArray(int A[], int n, int B[],
                                     int m)
{
    int result = INT_MAX;

    // Traverse main_array element
    for (int i = 0; i < n - m + 1; i++)
    {
        // Pick only those subarray of main_array
        // whose first element match with the
        // first element of second_array
        if (A[i] == B[0]) {

            // initialize starting of both
            // subarrays
            int j = 0, index = i;
            for (; index < n; index++) {
                if (A[index] == B[j])
                    j++;

                // if we found all elements of
                // second array
                if (j == m)
                    break;
            }

            // update minimum length sub_array
            if (j == m && result > index - i + 1)
              result = (index == n) ? index - i : index - i + 1;
    }
}

    // return minimum length subarray
    return result;
}

// driver program to test above function
int main()
{
    int A[] = { 5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7 };
    int B[] = { 5, 5, 7 };
    int n = sizeof(A)/sizeof(A[0]);
    int m = sizeof(B)/sizeof(B[0]);
    cout << minimumSubArray(A, n, B, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest length
// subarray that contains all elements
// of another array.
import java.io.*;

class GFG {

// Returns the minimum length of sub_array
static int minimumSubArray(int A[], int n,
                           int B[], int m)
{
    int result = Integer.MAX_VALUE;

    // Traverse main_array element
    for (int i = 0; i < n - m + 1; i++)
    {
        // Pick only those subarray of
        // main_array whose first element
        // match with the first element
        // of second_array
        if (A[i] == B[0]) {

            // initialize starting of
            // both subarrays
            int j = 0, index = i;
            for (; index < n; index++) {
                if (A[index] == B[j])
                    j++;

                // if we found all elements
                // of second array
                if (j == m)
                    break;
            }

            // update minimum length sub_array
            if (j == m && result > index - i + 1)
            result = (index == n) ? index - i :
                                 index - i + 1;
    }

    }

    // return minimum length subarray
    return result;
}

// driver program to test above function
public static void main(String[] args)
{
    int A[] = { 5, 6, 5, 2, 7, 5,
                6, 7, 5, 5, 7 };
    int B[] = { 5, 5, 7 };
    int n = A.length;
    int m = B.length;
    System.out.println(minimumSubArray(A, n,
                                     B, m));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to find smallest length
# subarray that contains all elements
# of another array.

# Returns the minimum length of sub_array
def minimumSubArray( A,n, B, m) :
    result = 1000000

    # Traverse main_array element
    for i in range(0, n - m + 1) :

        # Pick only those subarray of main_array
        # whose first element match with the
        # first element of second_array
        if (A[i] == B[0]) :

            # initialize starting of both
            # subarrays
            j = 0
            index = i
            for index in range(i, n) :
                if (A[index] == B[j]) :
                    j = j+1

                # if we found all elements
                # of second array
                if (j == m) :
                    break

            # update minimum length sub_array
            if (j == m and result > index - i + 1) :
                if(index == n) :
                    result = index - i
                else:
                    result = index - i + 1

    # return minimum length subarray
    return result

# driver program to test above function
A = [ 5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7 ]
B = [ 5, 5, 7 ]
n = len(A)
m = len(B)
print(minimumSubArray(A, n, B, m))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find smallest length
// subarray that contains all elements
// of another array.
using System;

class GFG {

// Returns the minimum length of sub_array
static int minimumSubArray(int []A, int n,
                           int []B, int m)
{
    int result = int.MaxValue;

    // Traverse main_array element
    for (int i = 0; i < n - m + 1; i++)
    {
        // Pick only those subarray of
        // main_array whose first element
        // match with the first element
        // of second_array
        if (A[i] == B[0]) {

            // initialize starting of
            // both subarrays
            int j = 0, index = i;
            for (; index < n; index++)
            {
                if (A[index] == B[j])
                    j++;

                // if we found all elements
                // of second array
                if (j == m)
                    break;
            }

            // update minimum length sub_array
            if (j == m && result > index - i + 1)
            result = (index == n) ? index - i :
                                index - i + 1;
    }
    }

    // return minimum length subarray
    return result;
}

  // Driver code
  public static void Main()
  {
    int []A = { 5, 6, 5, 2, 7, 5,
                 6, 7, 5, 5, 7 };
    int []B = { 5, 5, 7 };
    int n = A.Length;
    int m = B.Length;
    Console.Write(minimumSubArray(A, n, B, m));
  }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest length
// subarray that contains all elements
// of another array.

// Returns the minimum length of sub_array
function minimumSubArray(&$A, $n, &$B, $m)
{
    $result = PHP_INT_MAX;

    // Traverse main_array element
    for ($i = 0; $i < $n - $m + 1; $i++)
    {
        // Pick only those subarray of main_array
        // whose first element match with the
        // first element of second_array
        if ($A[$i] == $B[0])
        {

            // initialize starting of both
            // subarrays
            $j = 0;
            $index = $i;
            for ($index = $i; $index < $n; $index++)
            {
                if ($A[$index] == $B[$j])
                    $j++;

                // if we found all elements of
                // second array
                if ($j == $m)
                    break;
            }

            // update minimum length sub_array
            if ($j == $m && $result > $index - $i + 1)
            $result = ($index == $n) ?
                         $index - $i :
                         $index - $i + 1;
        }
    }

    // return minimum length subarray
    return $result;
}

// Driver Code
$A = array(5, 6, 5, 2, 7, 5,
              6, 7, 5, 5, 7 );
$B = array(5, 5, 7 );
$n = sizeof($A);
$m = sizeof($B);
echo(minimumSubArray($A, $n, $B, $m));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript program to find smallest length
    // subarray that contains all elements
    // of another array.

    // Returns the minimum length of sub_array
    function minimumSubArray(A, n, B, m)
    {
        let result = Number.MAX_VALUE;

        // Traverse main_array element
        for (let i = 0; i < n - m + 1; i++)
        {
            // Pick only those subarray of
            // main_array whose first element
            // match with the first element
            // of second_array
            if (A[i] == B[0]) {

                // initialize starting of
                // both subarrays
                let j = 0, index = i;
                for (; index < n; index++)
                {
                    if (A[index] == B[j])
                        j++;

                    // if we found all elements
                    // of second array
                    if (j == m)
                        break;
                }

                // update minimum length sub_array
                if (j == m && result > index - i + 1)
                result = (index == n) ? index - i :
                                    index - i + 1;
        }
        }

        // return minimum length subarray
        return result;
    }

    let A = [ 5, 6, 5, 2, 7, 5, 6, 7, 5, 5, 7 ];
    let B = [ 5, 5, 7 ];
    let n = A.length;
    let m = B.length;
    document.write(minimumSubArray(A, n, B, m));

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
3
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(1)