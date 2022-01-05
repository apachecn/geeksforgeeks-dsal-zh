# 总和小于 K 的子阵列数量

> 原文:[https://www.geeksforgeeks.org/number-subarrays-sum-less-k/](https://www.geeksforgeeks.org/number-subarrays-sum-less-k/)

给定一个非负数和一个非负数 k 的数组，求和小于 k 的子数组的个数。我们可以假设没有溢出。
**例:**

```
Input : arr[] = {2, 5, 6}
        K = 10
Output : 4
The subarrays are {2}, {5}, {6} and
{2, 5},

Input : arr[] = {1, 11, 2, 3, 15}
        K = 10
Output : 4
{1}, {2}, {3} and {2, 3}
```

一个**简单的解决方案**是生成阵列的所有子阵列，然后统计和小于 k 的阵列数量
下面是上述方法的实现:

## C++

```
// CPP program to count
// subarrays having sum
// less than k.
#include <bits/stdc++.h>
using namespace std;

// Function to find number
// of subarrays having sum
// less than k.
int countSubarray(int arr[],
                  int n, int k)
{
    int count = 0;

    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {

            // If sum is less than k
            // then update sum and
            // increment count
            if (sum + arr[j] < k) {
                sum = arr[j] + sum;
                count++;
            }
            else {
                break;
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    int array[] = { 1, 11, 2, 3, 15 };
    int k = 10;
    int size = sizeof(array) / sizeof(array[0]);
    int count = countSubarray(array, size, k);
    cout << count << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subarrays
// having sum less than k.
import java.io.*;

class GFG {

    // Function to find number of
    // subarrays having sum less than k.
    static int countSubarray(int arr[],
                             int n, int k)
    {
        int count = 0;

        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {

                // If sum is less than
                // k then update sum and
                // increment count
                if (sum + arr[j] < k) {
                    sum = arr[j] + sum;
                    count++;
                }
                else {
                    break;
                }
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int array[] = { 1, 11, 2, 3, 15 };
        int k = 10;
        int size = array.length;
        int count = countSubarray(array, size, k);
        System.out.println(count);
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# python program to count subarrays
# having sum less than k.

# Function to find number of subarrays
# having sum less than k.
def countSubarray(arr, n, k):
    count = 0

    for i in range(0, n):
        sum = 0;
        for j in range(i, n):

            # If sum is less than k
            # then update sum and
            # increment count
            if (sum + arr[j] < k):
                sum = arr[j] + sum
                count+= 1
            else:
                break
    return count;

# Driver Code
array = [1, 11, 2, 3, 15]
k = 10
size = len(array)
count = countSubarray(array, size, k);
print(count)

# This code is contributed by Sam007
```

## C#

```
// C# program to count subarrays
// having sum less than k.
using System;

class GFG {

    // Function to find number
    // of subarrays having sum
    // less than k.
    static int countSubarray(int[] arr,
                             int n, int k)
    {
        int count = 0;

        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {

                // If sum is less than k
                // then update sum and
                // increment count
                if (sum + arr[j] < k) {
                    sum = arr[j] + sum;
                    count++;
                }
                else {
                    break;
                }
            }
        }
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] array = { 1, 11, 2, 3, 15 };
        int k = 10;
        int size = array.Length;
        int count = countSubarray(array, size, k);
        Console.WriteLine(count);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// subarrays having sum
// less than k.

// Function to find number 
// of subarrays having sum
// less than k.
function countSubarray($arr, $n, $k)
{
    $count = 0;

    for ($i = 0; $i < $n; $i++)
    {
    $sum = 0;
        for ($j = $i; $j < $n; $j++)
        {

            // If sum is less than
            // k then update sum and
            // increment count
            if ($sum + $arr[$j] < $k)
            {
                $sum = $arr[$j] + $sum;
                $count++;
            }
            else
            {
                break;
            }
        }
    }

    return $count;
}

// Driver Code
$array = array(1, 11, 2, 3, 15);
$k = 10;
$size = sizeof($array);
$count = countSubarray($array, $size, $k);
echo $count, "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to count subarrays
// having sum less than k.

    // Function to find number of
    // subarrays having sum less than k.
    function countSubarray(arr , n , k)
    {
        var count = 0;

        for (i = 0; i < n; i++)
        {
            var sum = 0;
            for (j = i; j < n; j++)
            {

                // If sum is less than
                // k then update sum and
                // increment count
                if (sum + arr[j] < k)
                {
                    sum = arr[j] + sum;
                    count++;
                }
                else
                {
                    break;
                }
            }
        }
        return count;
    }

    // Driver Code
        var array = [ 1, 11, 2, 3, 15 ];
        var k = 10;
        var size = array.length;
        var count = countSubarray(array, size, k);
        document.write(count);

// This code is contributed by Rajput-Ji
</script>
```

**Output :** 

```
4
```