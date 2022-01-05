# 如果给定平均值，找出数组中缺少的整数

> 原文:[https://www . geesforgeks . org/find-missing-integer-array-mean-given/](https://www.geeksforgeeks.org/find-missing-integer-array-mean-given/)

给定大小为 N-1 的数组和 N 个元素的平均值(未给出一个元素)。我们需要找到数组中缺少的值 X。
示例:

```
Input : a[] = {2, 4, 20}
       Mean = 9
Output : Missing Element = 10 
Explanation : Mean of (2, 4, 20, 10) is
(2 + 4 + 20 + 10)/4 = 9
```

让 **x** 成为缺失元素
均值=(a<sub>1</sub>+a<sub>2</sub>+a<sub>3</sub>..+ X +..a<sub>n</sub>/n .
So(a<sub>1</sub>+a<sub>2</sub>+a<sub>3</sub>..+ X +..a <sub>N</sub> ) =均值*N .
缺失元素 x =(均值* N –( a<sub>1</sub>+a<sub>2</sub>+a<sub>3</sub>…。a<sub>N</sub>)

## C++

```
// C++ program to find missing element in a
// given array from mean.
#include <bits/stdc++.h>
using namespace std;

// Size of a[] is N - 1 (one element missing)
int findMissing(int a[], int N, int mean)
{
  // Find sum of array elements
  int sum = 0;
  for (int i = 0; i < N - 1; i++)
    sum += a[i]; 

  return (mean * N) - sum;
}

int main() {
  int a[] = {25, 65, 80};
  int mean = 50;
  int n = sizeof(a)/sizeof(a[0]);
  cout << "The missing element : "
       << findMissing(a, n+1, mean)  << endl;
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find missing element
// in a given array from mean.
import java.io.*;

class GFG
{
    // Size of a[] is N - 1 (one element missing)
    public static int findMissing(int a[], int N, int mean)
    {
        // Find sum of array elements
        int sum = 0;
        for (int i = 0; i < N - 1; i++)
        sum += a[i];

        return (mean * N) - sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = {25, 65, 80};
        int mean = 50;
        int n = a.length;
        System.out.println("The missing element : "
                           + findMissing(a, n + 1, mean));

    }
}

// This code is contributed by upendra bartwal
```

## 蟒蛇 3

```
# Python3 code to find missing element
# in a given array from mean.

# Size of a[] is N - 1
# (one element missing)
def findMissing( a , N , mean ):

    # Find sum of array elements
    sum = 0
    for i in range(N - 1):
        sum += a[i]

    return (mean * N) - sum

# Driver Code
a = [25, 65, 80]
mean = 50
n = len(a)
print("The missing element : ", end = '')
print(findMissing(a, n+1, mean))

# This code is contributed by Sharad Bhardwaj.
```

## C#

```
// C# program to find missing element
// in a given array from mean.
using System;

class GFG {

    // Size of a[] is N - 1
    // (one element missing)
    public static int findMissing(int[] a, int N, int mean)
    {

        // Find sum of array elements
        int sum = 0;
        for (int i = 0; i < N - 1; i++)
            sum += a[i];

        return (mean * N) - sum;
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 25, 65, 80 };
        int mean = 50;
        int n = a.Length;
        Console.WriteLine("The missing element : "
                    + findMissing(a, n + 1, mean));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find missing
// element in a given array
// from mean.

// Size of a[] is N - 1
// (one element missing)
function findMissing($a, $N, $mean)
{

    // Find sum of array elements
    $sum = 0;
    for ($i = 0; $i < $N - 1; $i++)
        $sum += $a[$i];

    return ($mean * $N) - $sum;
}

// Driver Code
$a = array(25, 65, 80);
$mean = 50;
$n = count($a);
echo "The missing element : "
    .findMissing($a, $n + 1, $mean);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// missing element in a
// given array from mean.

// Size of a[] is N - 1
// (one element missing)
function findMissing( a, N, mean)
{
// Find sum of array elements
let sum = 0;
for (let i = 0; i < N - 1; i++)
    sum += a[i];

return (mean * N) - sum;
}

    // Driver Code

    let a = [25, 65, 80];
    let mean = 50;
    let n = a.length;
    document.write("The missing element : "
        + findMissing(a, n+1, mean) + "</br>");

</script>
```

**输出:**

```
The missing element : 30
```