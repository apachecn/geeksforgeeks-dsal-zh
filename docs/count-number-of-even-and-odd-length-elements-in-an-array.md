# 计算数组中偶数和奇数长度元素的数量

> 原文:[https://www . geeksforgeeks . org/count-数组中偶数和奇数长度元素的数量/](https://www.geeksforgeeks.org/count-number-of-even-and-odd-length-elements-in-an-array/)

给定一个由大小为 **N** 的整数组成的数组 **arr[]** ，任务是找到具有偶数和奇数长度的数组的数字元素。
**例:**

> **输入:** arr[] = {14，735，3333，223222}
> **输出:**偶数长度元素个数= 3
> 奇数长度元素个数= 1
> **输入:** arr[] = {1121，322，32，14783，44}
> **输出:**偶数长度元素个数= 3
> 奇数长度元素个数= 2【T0

**方法:**要计算偶数长度或奇数长度的位数，[将每个数字转换成一个字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)。然后检查长度是奇数还是偶数。最后，分别打印偶数长度和奇数长度的计数。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the count
// number of even and odd
// length elements in an Array

#include <bits/stdc++.h>
using namespace std;

// Function to find the number elements of
// the array having even length and odd.
void EvenOddLength(int arr[], int n)
{
    // Store numbers with even length
    int even = 0;

    for (int i = 0; i < n; i++) {

        // Conversion of integer to string
        string x = to_string(arr[i]);

        if (x.length() % 2 == 0)
            even++;
    }

    cout << "Number of even "
         << "length elements = "
         << even << endl;
    cout << "Number of odd "
         << "length elements = "
         << n - even << endl;
}

// Driver code
int main()
{
    int arr[] = { 12, 44, 213, 232, 3433 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    EvenOddLength(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// number of even and odd
// length elements in an Array
import java.util.*;
class GFG{

// Function to find the number elements of
// the array having even length and odd.
    static void EvenOddLength(int arr[], int n)
    {
        // Store numbers with even length
        int even = 0;

        for (int i = 0; i < n; i++) {

            // Conversion of integer to string
            String x = Integer.toString(arr[i]);

            if (x.length() % 2 == 0)
                even++;
        }

        System.out.println("Number of even length elements = "+even);
        System.out.println("Number of odd length elements = "+(n - even));
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 12, 44, 213, 232, 3433 };
        int n = arr.length;

        // Function call
        EvenOddLength(arr, n);

    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to find the count
# number of even and odd
# length elements in an Array

# Function to find the number elements of
# the array having even length and odd.
def EvenOddLength(arr, n):

    # Store numbers with even length
    even = 0

    for i in range(n):

        # Conversion of integer to string
        x = str(arr[i])

        if (len(x) % 2 == 0):
            even += 1

    print( "Number of even length elements = ", even)
    print( "Number of odd length elements = ", n - even)

# Driver code
if __name__ == '__main__':
    arr= [12, 44, 213, 232, 3433]
    n = len(arr)

    # Function call
    EvenOddLength(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the count
// number of even and odd
// length elements in an Array
using System;

class GFG{

// Function to find the number elements of
// the array having even length and odd.
    static void EvenOddLength(int []arr, int n)
    {
        // Store numbers with even length
        int even = 0;

        for (int i = 0; i < n; i++) {

            // Conversion of integer to string
            String x = arr[i].ToString();

            if (x.Length % 2 == 0)
                even++;
        }

        Console.WriteLine("Number of even length elements = "+even);
        Console.WriteLine("Number of odd length elements = "+(n - even));
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 12, 44, 213, 232, 3433 };
        int n = arr.Length;

        // Function call
        EvenOddLength(arr, n);

    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the count
// number of even and odd
// length elements in an Array

// Function to find the number elements of
// the array having even length and odd.
function EvenOddLength(arr, n)
{

    // Store numbers with even length
    let even = 0;

    for (let i = 0; i < n; i++)
    {

        // Conversion of integer to string
        let x = arr[i].toString();

        if ((x.length) % 2 == 0)
            even++;
    }

    document.write("Number of even "
        + "length elements = "
        + even + "<br>");
    document.write("Number of odd "
        + "length elements = ");
    document.write(n - even + "<br>");
}

// Driver code
    let arr = [ 12, 44, 213, 232, 3433 ];
    let n = arr.length;

    // Function call
    EvenOddLength(arr, n);

// This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
Number of even length elements = 3
Number of odd length elements = 2
```