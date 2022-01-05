# 计算数组中偶数和奇数元素的数量

> 原文:[https://www . geesforgeks . org/count-number-偶数-奇数-elements-array/](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

对于给定的整数数组，计算偶数和奇数元素。

**示例:**

```
Input: 
int arr[5] = {2, 3, 4, 5, 6}
Output: 
Number of even elements = 3    
Number of odd elements = 2  

Input:
int arr[5] = {22, 32, 42, 52, 62}
Output: 
Number of even elements = 5  
Number of odd elements = 0
```

**解:**
我们还可以检查一个数是奇数还是偶数

*   通过对 1 和那个数字进行“与”，如果结果是 1，那么这个数字是奇数，否则是偶数。
*   除以 2。如果一个数不能被 2 整除，那么它就是奇数，否则就是偶数。

在这里，我们将检查一个数字是否是奇数，然后我们将增加奇数计数器，否则我们将增加偶数计数器。

下面是上述方法的实现:

## C++

```
// CPP program to count number of even
// and odd elements in an array
#include <iostream>
using namespace std;

void CountingEvenOdd(int arr[], int arr_size)
{
    int even_count = 0;
    int odd_count = 0;

    // loop to read all the values in the array
    for (int i = 0; i < arr_size; i++) {

          // checking if a number is completely
        // divisible by 2
        if (arr[i] & 1 == 1)
            odd_count++;
        else
            even_count++;
    }

    cout << "Number of even elements = " << even_count
         << "\nNumber of odd elements = " << odd_count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

      // Function Call
    CountingEvenOdd(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to count number of even
// and odd elements in an array
import java.io.*;

class GFG {

    static void CountingEvenOdd(int arr[], int arr_size)
    {
        int even_count = 0;
        int odd_count = 0;

        // loop to read all the values in
        // the array
        for (int i = 0; i < arr_size; i++) {

              // checking if a number is
            // completely divisible by 2
            if ((arr[i] & 1) == 1)
                odd_count++;
            else
                even_count++;
        }

        System.out.println("Number of even"
                           + " elements = " + even_count
                           + " Number of odd elements = "
                           + odd_count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 5, 6 };
        int n = arr.length;

          // Function Call
        CountingEvenOdd(arr, n);
    }
}

// This code is Contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to count number of
# even and odd elements in an array

def CountingEvenOdd(arr, arr_size):
    even_count = 0
    odd_count = 0

    # loop to read all the values
    # in the array
    for i in range(arr_size):

        # checking if a number is
        # completely divisible by 2
        if (arr[i] & 1 == 1):
            odd_count += 1
        else:
            even_count += 1

    print("Number of even elements = ",
          even_count)
    print("Number of odd elements = ",
          odd_count)

# Driver Code
arr = [2, 3, 4, 5, 6]
n = len(arr)

# Function Call
CountingEvenOdd(arr, n)

# This code is contributed by sahishelangia
```

## C#

```
// C# program to count number of even
// and odd elements in an array
using System;

class GFG {

    static void CountingEvenOdd(int[] arr, int arr_size)
    {
        int even_count = 0;
        int odd_count = 0;

        // loop to read all the values in
        // the array
        for (int i = 0; i < arr_size; i++) {

              // checking if a number is
            // completely divisible by 2
            if ((arr[i] & 1) == 1)
                odd_count++;
            else
                even_count++;
        }

        Console.WriteLine("Number of even"
                          + " elements = " + even_count
                          + " Number of odd elements = "
                          + odd_count);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 3, 4, 5, 6 };
        int n = arr.Length;

          // Function Call
        CountingEvenOdd(arr, n);
    }
}

// This code is Contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of even
// and odd elements in an array

function CountingEvenOdd( $arr, $arr_size)
{
    $even_count = 0;        
    $odd_count = 0;            

    // loop to read all the values in
    // the array
    for( $i = 0 ; $i < $arr_size ; $i++)
    {
        // checking if a number is
        // completely divisible by 2
        if ($arr[$i] & 1 == 1)
            $odd_count ++ ;    
        else               
            $even_count ++ ;        
    }

    echo "Number of even elements = " ,
        $even_count," Number of odd " ,
            "elements = " ,$odd_count ;    
}

// Driver Code
    $arr = array(2, 3, 4, 5, 6);
    $n = count($arr);

    // Function Call
    CountingEvenOdd($arr, $n);

// This code is Contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of even
// and odd elements in an array

function CountingEvenOdd(arr, arr_size)
{
    let even_count = 0;
    let odd_count = 0;

    // loop to read all the values in the array
    for (let i = 0; i < arr_size; i++) {

        // checking if a number is completely
        // divisible by 2
        if (arr[i] & 1 == 1)
            odd_count++;
        else
            even_count++;
    }

    document.write("Number of even elements = " + even_count
        + "<br>" + "Number of odd elements = " + odd_count);
}

// Driver Code

    let arr = [ 2, 3, 4, 5, 6 ];
    let n = arr.length;

    // Function Call
    CountingEvenOdd(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
Number of even elements = 3
Number of odd elements = 2
```

**时间复杂度:** O(n)