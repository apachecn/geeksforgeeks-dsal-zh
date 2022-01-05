# 阵列中异常的数量

> 原文:[https://www . geesforgeks . org/阵列中异常数量/](https://www.geeksforgeeks.org/number-of-anomalies-in-an-array/)

给定一个由 N 个整数组成的数组。异常是一个数，它和数组中其他数的绝对差大于 K，其中 K 是给定的正整数。找出异常的数量。

**示例:**

```
Input : arr[] = {1, 3, 5}, k = 1
Output : 3
Explanation:
All the numbers in the array are anamolies because 
For the number 1 abs(1-3)=2, abs(1-5)=4 which all are greater than 1,
For the number 3 abs(3-1)=2, abs(3-5)=2 which all are again greater than 1
For the number 5 abs(5-1)=4, abs(5-3)=2 which all are again greater than 1
So there are 3 anamolies.

Input : arr[] = {7, 1, 8}, k = 5
Output : 1
```

**简单方法:**
我们只需检查每个数字是否满足给定的条件，即与其他每个数字的绝对差值是否大于 K。

## C++

```
// A simple C++ solution to count anomalies in
// an array.
#include<iostream>
using namespace std;

int countAnomalies(int arr[], int n, int k)
{
   int res = 0;
   for (int i=0; i<n; i++)
   {
      int j;
      for (j=0; j<n; j++)
         if (i != j && abs(arr[i] - arr[j]) <= k)
              break;

      if (j == n)
         res++;
   }
   return res;
}

int main()
{
   int arr[] = {7, 1, 8}, k = 5;
   int n = sizeof(arr)/sizeof(arr[0]);
   cout << countAnomalies(arr, n, k);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple java solution to count
// anomalies in an array.
class GFG
{
static int countAnomalies(int arr[],
                          int n, int k)
{
    int res = 0;
    for (int i = 0; i < n; i++)
    {
        int j;
        for (j = 0; j < n; j++)
            if (i != j && Math.abs(arr[i] -
                                   arr[j]) <= k)
                break;

        if (j == n)
            res++;
    }
    return res;
}

// Driver code
public static void main(String args[])
{
    int arr[] = {7, 1, 8}, k = 5;
    int n = arr.length;
    System.out.println(countAnomalies(arr, n, k));
}
}

// This code is contributed by ANKITRAI1
```

## 蟒蛇 3

```
# A simple Python3 solution to
# count anomalies in an array.

def countAnomalies(arr, n, k):

    res = 0
    for i in range(0, n):

        j = 0
        while j < n:
            if i != j and abs(arr[i] - arr[j]) <= k:
                break

            j += 1

        if j == n:
            res += 1

    return res

# Driver Code
if __name__ == "__main__":

    arr = [7, 1, 8]
    k = 5
    n = len(arr)
    print(countAnomalies(arr, n, k))

# This code is contributed by Rituraj Jain
```

## C#

```
// A simple C# solution to count
// anomalies in an array.
using System;

class GFG
{
static int countAnomalies(int[] arr,
                          int n, int k)
{
    int res = 0;
    for (int i = 0; i < n; i++)
    {
        int j;
        for (j = 0; j < n; j++)
            if (i != j && Math.Abs(arr[i] -
                                arr[j]) <= k)
                break;

        if (j == n)
            res++;
    }
    return res;
}

// Driver code
public static void Main()
{
    int[] arr = {7, 1, 8};
    int k = 5;
    int n = arr.Length;
    Console.WriteLine(countAnomalies(arr, n, k));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP solution to count
// anomalies in an array.
function countAnomalies(&$arr, $n, $k)
{
    $res = 0;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
            if ($i != $j && abs($arr[$i] -
                                $arr[$j]) <= $k)
                break;

        if ($j == $n)
            $res++;
    }
    return $res;
}

// Driver Code
$arr = array(7, 1, 8);
$k = 5;
$n = sizeof($arr);
echo countAnomalies($arr, $n, $k);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// A simple javascript solution to count
// anomalies in an array.
function countAnomalies(arr,n,k)
{
    let res = 0;
    for (let i = 0; i < n; i++)
    {
        let j;
        for (j = 0; j < n; j++)
            if (i != j && Math.abs(arr[i] -
                                   arr[j]) <= k)
                break;

        if (j == n)
            res++;
    }
    return res;
}

// Driver code
let arr=[7, 1, 8];
let  k = 5;
let n = arr.length;
document.write(countAnomalies(arr, n, k));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1
```