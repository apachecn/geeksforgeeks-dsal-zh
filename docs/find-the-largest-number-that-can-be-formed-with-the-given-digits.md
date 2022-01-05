# 找出给定数字能组成的最大数字

> 原文:[https://www . geeksforgeeks . org/find-给定数字可以形成的最大数字/](https://www.geeksforgeeks.org/find-the-largest-number-that-can-be-formed-with-the-given-digits/)

给定一个代表数字的整数数组 arr[]。任务是编写一个程序，用这些数字产生最大可能的数字。
**注**:数组中的数字在 0 到 9 之间。即 0 < arr[i] < 9。
T4【示例】T5:

```
Input : arr[] = {4, 7, 9, 2, 3}
Output : Largest number: 97432 

Input : arr[] = {8, 6, 0, 4, 6, 4, 2, 7}
Output : Largest number: 87664420 
```

**朴素方法**:朴素方法是将给定的数字数组按照**降序**排序，然后使用数组中的数字组成数字，保持数字在数字中的顺序与排序后的数组相同。
时间复杂度:O(N logN)，其中 N 为位数。
以下是上述思路的实现:

## C++

```
// C++ program to generate largest possible
// number with given digits
#include <bits/stdc++.h>

using namespace std;

// Function to generate largest possible
// number with given digits
int findMaxNum(int arr[], int n)
{  
    // sort the given array in
    // descending order
    sort(arr, arr+n, greater<int>());

    int num = arr[0];

    // generate the number
    for(int i=1; i<n; i++)
    {
        num = num*10 + arr[i];
    }

    return num;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 0};

    int n = sizeof(arr)/sizeof(arr[0]);

    cout<<findMaxNum(arr,n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate largest
// possible number with given digits
import java.*;
import java.util.Arrays;

class GFG
{
// Function to generate largest
// possible number with given digits
static int findMaxNum(int arr[], int n)
{
    // sort the given array in
    // ascending order and then
    // traverse into descending
    Arrays.sort(arr);

    int num = arr[0];

    // generate the number
    for(int i = n - 1; i >= 0; i--)
    {
        num = num * 10 + arr[i];
    }

    return num;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {1, 2, 3, 4, 5, 0};

    int n = arr.length;

    System.out.println(findMaxNum(arr, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to generate largest possible
# number with given digits

# Function to generate largest possible
# number with given digits
def findMaxNum(arr,n) :

    # sort the given array in
    # descending order
    arr.sort(reverse = True)

    # initialize num with starting
    # element of an arr
    num = arr[0]

    # generate the number
    for i in range(1,n) :
        num = num * 10 + arr[i]

    return num

# Driver code
if __name__ == "__main__" :

    arr = [1,2,3,4,5,0]

    n = len(arr)

    print(findMaxNum(arr,n))

```

## C#

```
// C#  program to generate largest
// possible number with given digits
using System;

public class GFG{
    // Function to generate largest
// possible number with given digits
static int findMaxNum(int []arr, int n)
{
    // sort the given array in
    // ascending order and then
    // traverse into descending
    Array.Sort(arr);

    int num = arr[0];

    // generate the number
    for(int i = n - 1; i >= 0; i--)
    {
        num = num * 10 + arr[i];
    }

    return num;
}

// Driver code
    static public void Main (){
    int []arr = {1, 2, 3, 4, 5, 0};
    int n = arr.Length;
    Console.WriteLine(findMaxNum(arr, n));
}
}

// This code is contributed by Sachin..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate
// largest possible number
// with given digits

// Function to generate
// largest possible number
// with given digits
function findMaxNum(&$arr, $n)
{
    // sort the given array
    // in descending order
    rsort($arr);

    $num = $arr[0];

    // generate the number
    for($i = 1; $i < $n; $i++)
    {
        $num = $num * 10 + $arr[$i];
    }

    return $num;
}

// Driver code
$arr = array(1, 2, 3, 4, 5, 0);
$n = sizeof($arr);
echo findMaxNum($arr,$n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to generate largest possible
// number with given digits

// Function to generate largest possible
// number with given digits
function findMaxNum(arr, n)
{
    // sort the given array in
    // descending order
    arr.sort(function(a,b){return b-a;});

    var num = arr[0];

    // generate the number
    for(var i=1; i<n; i++)
    {
        num = num*10 + arr[i];
    }

    return num;
}

// Driver code
var arr = [1, 2, 3, 4, 5, 0];

var n = arr.length;

document.write(findMaxNum(arr,n));

</script>
```

**Output:** 

```
543210
```