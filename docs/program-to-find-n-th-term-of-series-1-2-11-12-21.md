# 求数列 1、2、11、12、21 的第 N 项的程序。

> 原文:[https://www . geesforgeks . org/program-to-find-n-th-term-of-series-1-2-11-12-21/](https://www.geeksforgeeks.org/program-to-find-n-th-term-of-series-1-2-11-12-21/)

给定一个数字 N，任务是找到数列的第 N 项:

> 1、2、11、12、21……

**例:**

```
Input : N = 2
Output : 2

Input : N = 5
Output : 21
```

**方法:**
这个想法是基于最后一个数字的值在序列中交替的事实。例如，如果第 I 个数字的最后一位是 1，那么第(i-1)个和第(i+1)个数字的最后一位必须是 2。
因此，创建一个大小为(n+1)的数组，并将 1 和 2(这两个总是系列的前两个元素)推送给它。

> 因此数组的第 I 项为:
> 1)如果 I 为奇数，
> arr[I]= arr[I/2]* 10+1；
> 2)如果我是偶数，
> arr[I]= arr[(I/2)-1]* 10+2；

终于回来了。
以下是上述思路的实现:

## C++

```
// C++ program to find
// the N-th term in the series
// 1, 2, 11, 12, 21...

#include <bits/stdc++.h>
using namespace std;

// Function to find N-th number in series
int printNthElement(int N)
{
    // create an array of size (N+1)
    int arr[N + 1];
    arr[1] = 1;
    arr[2] = 2;

    for (int i = 3; i <= N; i++) {
        // If i is odd
        if (i % 2 != 0) {

            arr[i] = arr[i / 2] * 10 + 1;
        }
        else {

            arr[i] = arr[(i / 2) - 1] * 10 + 2;
        }
    }
    return arr[N];
}

// Driver code
int main()
{

    // Get N
    int N = 5;

    // Get Nth term
    cout << printNthElement(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the N-th term in the series
// 1, 2, 11, 12, 21...

class FindNth {

    // Function to find n-th number in series
    static int printNthElement(int n)
    {
        // create an array of size (n+1)
        int arr[] = new int[n + 1];
        arr[1] = 1;
        arr[2] = 2;

        for (int i = 3; i <= n; i++) {
            // If i is odd
            if (i % 2 != 0)
                arr[i] = arr[i / 2] * 10 + 1;
            else
                arr[i] = arr[(i / 2) - 1] * 10 + 2;
        }
        return arr[n];
    }

    // main function
    public static void main(String[] args)
    {
        int n = 5;

        System.out.println(printNthElement(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# the N-th term in the series
# 1, 2, 11, 12, 21...

# Return n-th number in series
def printNthElement(n) : 

    # create an array of size (n + 1) 
    arr =[0] * (n + 1); 
    arr[1] = 1
    arr[2] = 2

    for i in range(3, n + 1) : 
        # If i is odd 
        if (i % 2 != 0) : 
            arr[i] = arr[i // 2] * 10 + 1
        else : 
            arr[i] = arr[(i // 2) - 1] * 10 + 2

    return arr[n] 

# Driver code 
n = 5
print(printNthElement(n)) 
```

## C#

```
// C# program to find
// the N-th term in the series
// 1, 2, 11, 12, 21...
using System;

class GFG
{

// Function to find n-th
// number in series
static int printNthElement(int n)
{
    // create an array of size (n+1)
    int []arr = new int[n + 1];
    arr[1] = 1;
    arr[2] = 2;

    for (int i = 3; i <= n; i++)
    {
        // If i is odd
        if (i % 2 != 0)
            arr[i] = arr[i / 2] * 10 + 1;
        else
            arr[i] = arr[(i / 2) - 1] * 10 + 2;
    }
    return arr[n];
}

// Driver Code
public static void Main()
{
    int n = 5;

    Console.WriteLine(printNthElement(n));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the N-th term in the series
// 1, 2, 11, 12, 21...

// Function to find N-th
// number in series
function printNthElement($N)
{
    // create an array of size (N+1)
    $arr = array($N + 1);
    $arr[1] = 1;
    $arr[2] = 2;

    for ( $i = 3; $i <= $N; $i++)
    {
        // If i is odd
        if ($i % 2 != 0)
        {

            $arr[$i] = $arr[$i / 2] *
                            10 + 1;
        }
        else
        {

            $arr[$i] = $arr[($i / 2) - 1] *    
                                  10 + 2;
        }
    }
    return $arr[$N];
}

// Driver code
$N = 5;

// Get Nth term
echo printNthElement($N);

// This code is contributed
// by Mahadev99
?>
```

## java 描述语言

```
<script>
    // Javascript program to find
    // the N-th term in the series
    // 1, 2, 11, 12, 21...

    // Function to find n-th number in series
    function printNthElement(n)
    {
        // create an array of size (n+1)
        let arr = new Array(n + 1);
        arr[1] = 1;
        arr[2] = 2;

        for (let i = 3; i <= n; i++) {
            // If i is odd
            if (i % 2 != 0)
                arr[i] = arr[parseInt(i / 2, 10)] * 10 + 1;
            else
                arr[i] = arr[parseInt(i / 2, 10) - 1] * 10 + 2;
        }
        return arr[n];
    }

    let n = 5;

      document.write(printNthElement(n));

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
21
```