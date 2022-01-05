# 乘积可被 k 整除的最小子阵列

> 原文:[https://www . geesforgeks . org/minist-subarray-product-除尽-k/](https://www.geeksforgeeks.org/smallest-subarray-product-divisible-k/)

给定一组非负数，求乘积为 k 的倍数的最小子阵列的长度。
**示例:**

```
Input : arr[] = {1, 9, 16, 5, 4, 3, 2}   
        k = 720
Output: 3
The smallest subarray is {9, 16, 5} whose
product is 720.

Input : arr[] = {1, 2, 4, 5, 6}
        K = 96
Output : No such subarray exists
```

想法很简单。我们遍历所有子阵列。对于每个子阵列，我们计算其产品。如果乘积是 k 的倍数，我们检查子阵列的长度是否小于当前结果。

## C++

```
// C++ program to find smallest subarray
// with product divisible by k.
#include <bits/stdc++.h>
using namespace std;

// function to find the subarray of
// minimum length and end of sub array
int findsubArray(int arr[], int k)
{
    // find the length of array
    int n = 7;

    // try of every sub array whether it
    // result in multiple of k or not if it
    // is store it in the result
    // and find for the minimum using
    // dynamic programming
    int res = n + 1;

    for (int i = 0; i < n; i++) {

        // Find minimum length product
        // beginning with arr[i].
        int curr_prod = 1;

        for (int j = i; j < n; j++) {            
            curr_prod = curr_prod * arr[j];            

            if (curr_prod % k == 0 && res
                                > (j - i + 1))
            {
                res = min(res, j - i + 1);
                break;
            }
        }
    }

    return (res == n + 1) ? 0 : res;
}

// driver Function
int main(void)
{
    int array[] = { 1, 9, 16, 5, 4, 3, 2 };
    int k = 720;
    int answer = findsubArray(array, k);

    if (answer != 0)
        cout<<answer<<"\n";
    else
        cout<<"No Such subarray exists."<<"\n";

    return 0;
}

// This code is contributed by Nikita Tiwari.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest subarray
// with product divisible by k.
import java.util.*;

// function to find the subarray of
// minimum length and end of sub array
public class findSubArray {

    public static int findsubArray(int arr[], int k)
    {
        // find the length of array
        int n = arr.length;

        // try of every sub array whether it result
        // in multiple of k or not if it
        // is store it in the result
        // and find for the minimum using
        // dynamic programming
        int res = n+1;
        for (int i = 0; i < n; i++) {

            // Find minimum length product beginning
            // with arr[i].
            int curr_prod = 1;
            for (int j = i; j < n; j++) {               
                curr_prod = curr_prod * arr[j];               
                if (curr_prod % k == 0 && res > (j-i+1))
                {
                    res = Math.min(res, j-i+1);  
                    break;
                }
            }
        }
        return (res == n+1)? 0 : res;
    }

    // driver Function
    public static void main(String[] args)
    {
        int array[] = { 1, 9, 16, 5, 4, 3, 2 };
        int k = 720;
        int answer = findsubArray(array, k);
        if (answer != 0)
            System.out.println(answer);
        else
            System.out.println("No Such subarray exists.");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find smallest
# subarray with product divisible by k.

# function to find the subarray of
# minimum length and end of sub array
def findsubArray(arr, k) :

    # find the length of array
    n= len(arr)

    # try of every sub array whether it
    # result in multiple of k or not if
    # it is store it in the result
    # and find for the minimum using
    # dynamic programming
    res = n+1
    for i in range(0,n) :

        # Find minimum length product
        # beginning with arr[i].
        curr_prod = 1
        for j in range( i, n):
            curr_prod = curr_prod * arr[j]        
            if (curr_prod % k == 0 and
                     res > (j - i + 1)) :
                res = min(res, j - i + 1)
                break

    if(res == n + 1) :
        return 0
    else :
        return res

# driver Function
array = [1, 9, 16, 5, 4, 3, 2 ]
k = 720
answer = findsubArray(array, k)
if (answer != 0):
    print(answer)
else :
    print("No Such subarray exists.")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find smallest subarray
// with product divisible by k.
using System;

public class GFG {

    // function to find the subarray of
    // minimum length and end of sub array
    public static int findsubArray(int []arr, int k)
    {
        // find the length of array
        int n = arr.Length;

        // try of every sub array whether it result
        // in multiple of k or not if it
        // is store it in the result
        // and find for the minimum using
        // dynamic programming
        int res = n+1;
        for (int i = 0; i < n; i++) {

            // Find minimum length product beginning
            // with arr[i].
            int curr_prod = 1;
            for (int j = i; j < n; j++) {

                curr_prod = curr_prod * arr[j];   

                if (curr_prod % k == 0 && res > (j-i+1))
                {
                    res = Math.Min(res, j-i+1);
                    break;
                }
            }
        }

        return (res == n+1) ? 0 : res;
    }

    // driver Function
    public static void Main()
    {
        int []array = { 1, 9, 16, 5, 4, 3, 2 };
        int k = 720;
        int answer = findsubArray(array, k);
        if (answer != 0)
            Console.WriteLine(answer);
        else
            Console.WriteLine("No Such subarray"
                                  + " exists.");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest subarray
// with product divisible by k.

// function to find the subarray of
// minimum length and end of sub array
function findsubArray($arr, $k)
{

    // find the length of array
    $n = 7;

    // try of every sub array
    // whether it result in
    // multiple of k or not if
    // it is store it in the
    // result and find for the
    // minimum using dynamic
    // programming
    $res = $n + 1;

    for ($i = 0; $i < $n; $i++) {

        // Find minimum length product
        // beginning with arr[i].
        $curr_prod = 1;

        for ($j = $i; $j < $n; $j++) {            
            $curr_prod = $curr_prod * $arr[$j];            

            if ($curr_prod % $k == 0 &&
                $res > ($j - $i + 1))
            {
                $res = min($res, $j - $i + 1);
                break;
            }
        }
    }

    return ($res == $n + 1) ? 0 : $res;
}

    // Driver Code
    $arr = array(1, 9, 16, 5, 4, 3, 2);
    $k = 720;
    $answer = findsubArray($arr, $k);

    if ($answer != 0)
        echo $answer."\n";
    else
        echo "No Such subarray exists."."\n";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to find smallest subarray
    // with product divisible by k.

    // function to find the subarray of
    // minimum length and end of sub array
    function findsubArray(arr, k)
    {
        // find the length of array
        let n = arr.length;

        // try of every sub array whether it result
        // in multiple of k or not if it
        // is store it in the result
        // and find for the minimum using
        // dynamic programming
        let res = n+1;
        for (let i = 0; i < n; i++) {

            // Find minimum length product beginning
            // with arr[i].
            let curr_prod = 1;
            for (let j = i; j < n; j++) {

                curr_prod = curr_prod * arr[j];   

                if (curr_prod % k == 0 && res > (j-i+1))
                {
                    res = Math.min(res, j-i+1);
                    break;
                }
            }
        }

        return (res == n+1) ? 0 : res;
    }

    let array = [ 1, 9, 16, 5, 4, 3, 2 ];
    let k = 720;
    let answer = findsubArray(array, k);
    if (answer != 0)
      document.write(answer);
    else
      document.write("No Such subarray"
                        + " exists.");

</script>
```

**Output:** 

```
3
```

时间复杂度= O(n^2)