# 乘积小于 K 的子阵列数量

> 原文:[https://www . geesforgeks . org/number-subarrays-product-less-k/](https://www.geeksforgeeks.org/number-subarrays-product-less-k/)

给定一个正数数组，计算乘积小于给定数 k 的可能连续子数组的数量

**示例:**

```
Input : arr[] = [1, 2, 3, 4] 
        K = 10
Output : 7
The subarrays are {1}, {2}, {3}, {4}
{1, 2}, {1, 2, 3} and {2, 3}

Input  : arr[] = [1, 9, 2, 8, 6, 4, 3] 
         K = 100
Output : 16

Input  : arr[] = [10, 5, 2, 6] 
         K = 100
Output : 8
```

这个问题的一个**天真的方法**是生成阵列的所有子阵列，然后计算乘积小于 k 的阵列的数量。
下面是上述方法的实现:

## C++

```
// CPP program to count subarrays having
// product less than k.
#include <iostream>
using namespace std;

int countsubarray(int array[], int n, int k)
{
    int count = 0;
    int i, j, mul;

    for (i = 0; i < n; i++) {
        // Counter for single element
        if (array[i] < k)
            count++;

        mul = array[i];

        for (j = i + 1; j < n; j++) {
            // Multiple subarray
            mul = mul * array[j];
            // If this multiple is less
            // than k, then increment
            if (mul < k)
                count++;
            else
                break;
        }
    }

    return count;
}

// Driver Code
int main()
{
    int array[] = { 1, 2, 3, 4 };
    int k = 10;
    int size = sizeof(array) / sizeof(array[0]);
    int count = countsubarray(array, size, k);
    cout << count << "\n";
}

// This code is contributed by  'Dev Agarwal'.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subarrays
// having product less than k.
class GFG {
    static int countsubarray(int array[], int n, int k)
    {
        int count = 0;
        int i, j, mul;

        for (i = 0; i < n; i++) {

            // Counter for single element
            if (array[i] < k)
                count++;

            mul = array[i];

            for (j = i + 1; j < n; j++) {

                // Multiple subarray
                mul = mul * array[j];

                // If this multiple is less
                // than k, then increment
                if (mul < k)
                    count++;
                else
                    break;
            }
        }

        return count;
    }

    // Driver Code
    public static void main(String args[])
    {
        int array[] = { 1, 2, 3, 4 };
        int k = 10;
        int size = array.length;

        int count = countsubarray(array, size, k);
        System.out.print(count);
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to count subarrays
# having product less than k.

def countsubarray(array, n, k):
    count = 0
    for i in range(0, n):

        # Counter for single element
        if array[i] < k:
            count += 1

        mul = array[i]

        for j in range(i + 1, n):

            # Multiple subarray
            mul = mul * array[j]

            # If this multiple is less
            # than k, then increment
            if mul < k:
                count += 1
            else:
                break
    return count

# Driver Code
array = [1, 2, 3, 4]
k = 10
size = len(array)
count = countsubarray(array, size, k)
print(count, end=" ")

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to count subarrays having
// product less than k.
using System;

public class GFG {

    static int countsubarray(int[] array, int n, int k)
    {
        int count = 0;
        int i, j, mul;

        for (i = 0; i < n; i++) {

            // Counter for single element
            if (array[i] < k)
                count++;

            mul = array[i];

            for (j = i + 1; j < n; j++) {

                // Multiple subarray
                mul = mul * array[j];

                // If this multiple is less
                // than k, then increment
                if (mul < k)
                    count++;
                else
                    break;
            }
        }

        return count;
    }

    // Driver Code
    static public void Main()
    {
        int[] array = { 1, 2, 3, 4 };
        int k = 10;
        int size = array.Length;

        int count = countsubarray(array, size, k);

        Console.WriteLine(count);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count subarrays
// having  product less than k.

// function that returns count
function countsubarray($array, $n, $k)
{
    $count = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Counter for single element
        if ($array[$i] < $k)
            $count++;

        $mul = $array[$i];

        for ($j = $i + 1; $j < $n; $j++)
        {

            // Multiple subarray
            $mul = $mul * $array[$j];

            // If this multiple is less
            // than k, then increment
            if ($mul < $k)
                $count++;
            else
                break;
        }
    }

    return $count;
}

// Driver Code
$array = array(1, 2, 3, 4);
$k = 10;
$size = sizeof($array);
$count = countsubarray($array, $size, $k);
echo($count . "\n");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to count subarrays
// having product less than k.

    function countsubarray(array , n , k)
    {
        var count = 0;
        var i, j, mul;

        for (i = 0; i < n; i++)
        {

            // Counter for single element
            if (array[i] < k)
                count++;

            mul = array[i];
            for (j = i + 1; j < n; j++)
            {

                // Multiple subarray
                mul = mul * array[j];

                // If this multiple is less
                // than k, then increment
                if (mul < k)
                    count++;
                else
                    break;
            }
        }
        return count;
    }

    // Driver Code

        var array = [ 1, 2, 3, 4 ];
        var k = 10;
        var size = array.length;

        var count = countsubarray(array, size, k);
        document.write(count);

// This code is contributed by todaysgaurav
</script>
```

**Output**

```
7
```