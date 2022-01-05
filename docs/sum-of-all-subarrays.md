# 所有子阵列之和|集合 1

> 原文:[https://www.geeksforgeeks.org/sum-of-all-subarrays/](https://www.geeksforgeeks.org/sum-of-all-subarrays/)

给定大小为 n 的整数数组“arr[]”，求给定数组的所有子数组的和。

**示例:**

```
Input   : arr[] = {1, 2, 3}
Output  : 20
Explanation : {1} + {2} + {3} + {2 + 3} + 
              {1 + 2} + {1 + 2 + 3} = 20

Input  : arr[] = {1, 2, 3, 4}
Output : 50
```

**方法 1(简单解法)**
一个简单的解法是[生成所有子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并计算它们的和。

以下是上述想法的实现。

## C++

```
// Simple C++ program to compute sum of
// subarray elements
#include<bits/stdc++.h>
using namespace std;

// Computes sum all sub-array
long int SubArraySum(int arr[], int n)
{
    long int result = 0,temp=0;

    // Pick starting point
    for (int i=0; i <n; i++)
    {
        // Pick ending point
        temp=0;
        for (int j=i; j<n; j++)
        {
            // sum subarray between current
            // starting and ending points
            temp+=arr[j];
            result += temp ;
        }
    }
    return result ;
}

// driver program to test above function
int main()
{
    int arr[] = {1, 2, 3} ;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Sum of SubArray : "
          << SubArraySum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to compute sum of
// subarray elements
class GFG {

    // Computes sum all sub-array
    public static long SubArraySum(int arr[], int n)
    {
        long result = 0,temp=0;

        // Pick starting point
        for (int i = 0; i < n; i ++)
        {
            // Pick ending point
            temp=0;
            for (int j = i; j < n; j ++)
            {
                // sum subarray between current
                // starting and ending points
                temp+=arr[j];
                result += temp ;
            }
        }
        return result ;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3} ;
        int n = arr.length;
        System.out.println("Sum of SubArray : " +
                          SubArraySum(arr, n));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to compute
# sum of subarray elements

# Computes sum all sub-array
def SubArraySum(arr, n):
    temp,result = 0,0

    # Pick starting point
    for i in range(0, n):

        # Pick ending point
        temp=0;
        for j in range(i, n):

            # sum subarray between
            # current starting and
            # ending points
            temp+=arr[j]
            result += temp
    return result

# driver program
arr = [1, 2, 3]
n = len(arr)
print ("Sum of SubArray :"
       ,SubArraySum(arr, n))

# This code is contributed by
# TheGameOf256.
```

## C#

```
// Simple C# program to compute sum of
// subarray elements
using System;

class GFG {

    // Computes sum all sub-array
    public static long SubArraySum(int []arr,
                                      int n)
    {
        long result = 0,temp=0;

        // Pick starting point
        for (int i = 0; i < n; i ++)
        {
            // Pick ending point
            temp=0;
            for (int j = i; j < n; j ++)
            {

                // sum subarray between current
                // starting and ending points
                temp+=arr[j];
                result += temp ;
            }
        }
        return result ;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3} ;
        int n = arr.Length;
        Console.Write("Sum of SubArray : " +
                        SubArraySum(arr, n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to
// compute sum of subarray
// elements Computes sum
// all sub-array

function SubArraySum($arr, $n)
{
    $result = 0;
    $temp=0;
    // Pick starting point
    for ($i = 0; $i < $n; $i++)
    {
        // Pick ending point
        $temp=0;
        for ($j = $i; $j < $n; $j++)
        {
            // sum subarray between
            // current starting and
            // ending points
            $temp+=$arr[$j]
            $result += $temp ;
        }
    }
    return $result ;
}

// Driver Code
$arr = array(1, 2, 3) ;
$n = sizeof($arr);
echo "Sum of SubArray : ",
    SubArraySum($arr, $n),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Simple Javascript program to compute sum of
// subarray elements

// Computes sum all sub-array
function SubArraySum(arr, n)
{
    let result = 0,temp=0;

    // Pick starting point
    for (let i=0; i <n; i++)
    {
        // Pick ending point
        temp=0;
        for (let j=i; j<n; j++)
        {
            // sum subarray between current
            // starting and ending points
            temp+=arr[j];
            result += temp ;
        }
    }
    return result ;
}

// driver program to test above function

    let arr = [1, 2, 3] ;
    let n = arr.length;
    document.write("Sum of SubArray : "
    + SubArraySum(arr, n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Sum of SubArray : 20
```

**时间复杂度:** O(n <sup>2</sup>

**方法 2(有效解)**
如果我们仔细观察，那么我们观察到一个模式。举个例子

```
arr[] = [1, 2, 3], n = 3
All subarrays :  [1], [1, 2], [1, 2, 3], 
                 [2], [2, 3], [3]
here first element 'arr[0]' appears 3 times    
     second element 'arr[1]' appears 4 times  
     third element 'arr[2]' appears 3 times

Every element arr[i] appears in two types of subsets:
i)  In subarrays beginning with arr[i]. There are 
    (n-i) such subsets. For example [2] appears
    in [2] and [2, 3].
ii) In (n-i)*i subarrays where this element is not
    first element. For example [2] appears in 
    [1, 2] and [1, 2, 3].

Total of above (i) and (ii) = (n-i) + (n-i)*i 
                            = (n-i)(i+1)

For arr[] = {1, 2, 3}, sum of subarrays is:
  arr[0] * ( 0 + 1 ) * ( 3 - 0 ) + 
  arr[1] * ( 1 + 1 ) * ( 3 - 1 ) +
  arr[2] * ( 2 + 1 ) * ( 3 - 2 ) 

= 1*3 + 2*4 + 3*3 
= 20
```

以下是上述想法的实现。

## C++

```
// Efficient C++ program to compute sum of
// subarray elements
#include<bits/stdc++.h>
using namespace std;

//function compute sum all sub-array
long int SubArraySum( int arr[] , int n )
{
    long int result = 0;

    // computing sum of subarray using formula
    for (int i=0; i<n; i++)
        result += (arr[i] * (i+1) * (n-i));

    // return all subarray sum
    return result ;
}

// driver program to test above function
int main()
{
    int arr[] = {1, 2, 3} ;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Sum of SubArray : "
         << SubArraySum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to compute sum of
// subarray elements
class GFG {

    //function compute sum all sub-array
    public static long SubArraySum( int arr[] , int n )
    {
        long result = 0;

        // computing sum of subarray using formula
        for (int i=0; i<n; i++)
            result += (arr[i] * (i+1) * (n-i));

        // return all subarray sum
        return result ;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3} ;
        int n = arr.length;
        System.out.println("Sum of SubArray " +
                           SubArraySum(arr, n));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
#Python3 code to compute
# sum of subarray elements

#function compute sum
# all sub-array
def SubArraySum(arr, n ):
    result = 0

    # computing sum of subarray
    # using formula
    for i in range(0, n):
        result += (arr[i] * (i+1) * (n-i))

    # return all subarray sum
    return result

# driver program
arr = [1, 2, 3]
n = len(arr)
print ("Sum of SubArray : ",
      SubArraySum(arr, n))

# This code is contributed by
# TheGameOf256.
```

## C#

```
// Efficient C# program
// to compute sum of
// subarray elements
using System;

class GFG
{

    // function compute
    // sum all sub-array
    public static long SubArraySum(int []arr ,
                                   int n )
    {
        long result = 0;

        // computing sum of
        // subarray using formula
        for (int i = 0; i < n; i++)
            result += (arr[i] *
                      (i + 1) * (n - i));

        // return all subarray sum
        return result ;
    }

    // Driver code
    static public void Main ()
    {
        int []arr = {1, 2, 3} ;
        int n = arr.Length;
        Console.WriteLine("Sum of SubArray: " +
                          SubArraySum(arr, n));
    }
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to compute
// sum of subarray elements

//function compute sum all sub-array
function SubArraySum($arr , $n)
{
    $result = 0;

    // computing sum of subarray
    // using formula
    for ($i = 0; $i < $n; $i++)
        $result += ($arr[$i] *
                    ($i + 1) *
                    ($n - $i));

    // return all subarray sum
    return $result ;
}

// Driver Code
$arr = array(1, 2, 3) ;
$n = sizeof($arr);
echo "Sum of SubArray : ",
      SubArraySum($arr, $n) ,"\n";

#This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program
// to compute sum of subarray elements

// Function compute
// sum all sub-array
function SubArraySum(arr, n)
{
    let result = 0;

    // Computing sum of
    // subarray using formula
    for(let i = 0; i < n; i++)
        result += (arr[i] * (i + 1) *
                            (n - i));

    // Return all subarray sum
    return result ;
}

// Driver code
let arr = [ 1, 2, 3 ];
let n = arr.length;

document.write("Sum of SubArray : " +
               SubArraySum(arr, n));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
Sum of SubArray : 20
```

**时间复杂度:** O(n)
**参考:**
[https://www . quora . com/Can-we-find-of-of-O-n-Time 中的所有子数组之和](https://www.quora.com/Can-we-find-the-sum-of-all-sub-arrays-of-an-integer-array-in-O-n-time)
[**一个数组的所有子序列之和**](https://www.geeksforgeeks.org/sum-of-all-subsequences-of-an-array/)
本文由 [**Nishant Singh**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。