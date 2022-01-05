# 找出不能用给定数字表示的最小正数

> 原文:[https://www . geesforgeks . org/find-最小的正数-不能用给定的数字表示/](https://www.geeksforgeeks.org/find-the-smallest-positive-number-which-can-not-be-represented-by-given-digits/)

给定大小为 **10** 的数组 **arr[]** ，其中 **arr[i]** 表示数字 **i** 的频率。任务是找到不能用给定数字表示的最小正数。
**举例:**

> **输入:** arr[] = {2，1，1，4，0，6，3，2，2，2}
> **输出:** 4
> 由于第 4 位数字的计数为 0。所以 4 不能做。
> **输入:** arr[] = {0，1，1，1，1，1，1，1，1}
> **输出:** 10
> 由于第 0 位数字的计数为 0。所以不能做的最小正整数是 10。
> **输入:** arr[] = {2，2，1，2，1，1，3，1，1，1}
> **输出:** 22
> 为了得到 22，我们需要两个 2，但这里 2 的计数只有 1。

**进场:**

1.  从第一个索引开始计算数组中的最小值，并存储它的索引。
2.  现在将最小值与第 0 个索引处的值进行比较。
3.  如果它在第 0 个索引处的值小于最小值，则不能表示为 10、100、1000。
4.  如果它的值大于最小值，则循环到第一个最小值索引，并简单地打印它的索引值。

以下是上述方法的实现:

## C++

```
// CPP program to find the smallest positive
// number which can not be represented by given digits
#include<bits/stdc++.h>
using namespace std;

// Function to find the smallest positive
// number which can not be represented by given digits
void expressDigit(int arr[], int n){

    int min = 9, index = 0, temp = 0;

    // Storing the count of 0 digit
    // or store the value at 0th index
    temp = arr[0];

    // Calculates the min value in the array starting
    // from 1st index and also store it index.
    for(int i = 1; i < 10; i++){

        if(arr[i] < min){
            min = arr[i];
            index = i;
        }
    }

    // Now compare the min value with the
    // value at 0th index.

    // If its value at 0th index is less than min value
    // than either 10, 100, 1000 ... can't be expressed
    if(temp < min)
    {
        cout << 1;
        for(int i = 1; i <= temp + 1; i++)
            cout << 0;
    }

    // If it value is greater than min value than
    // iterate the loop upto first min value index
    // and simply print it index value.
    else
    {
        for(int i = 0; i < min; i++)
            cout << index;

        cout << index;
    }
}

// Driver code
int main()
{
    int arr[] = {2, 2, 1, 2, 1, 1, 3, 1, 1, 1};

    // Value of N is always 10 as we take digit from 0 to 9
    int N = 10;

    // Calling function
    expressDigit(arr, N);

    return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest positive
// number which can not be represented by given digits
import java.util.*;

class GFG
{

// Function to find the smallest positive
// number which can not be represented by given digits
static void expressDigit(int arr[], int n)
{
    int min = 9, index = 0, temp = 0;

    // Storing the count of 0 digit
    // or store the value at 0th index
    temp = arr[0];

    // Calculates the min value in the array starting
    // from 1st index and also store it index.
    for(int i = 1; i < 10; i++)
    {
        if(arr[i] < min)
        {
            min = arr[i];
            index = i;
        }
    }

    // Now compare the min value with the
    // value at 0th index.

    // If its value at 0th index is less than min value
    // than either 10, 100, 1000 ... can't be expressed
    if(temp < min)
    {
        System.out.print(1);
        for(int i = 1; i <= temp + 1; i++)
            System.out.print(0);
    }

    // If it value is greater than min value than
    // iterate the loop upto first min value index
    // and simply print it index value.
    else
    {
        for(int i = 0; i < min; i++)
            System.out.print(index);

        System.out.print(index);
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {2, 2, 1, 2, 1, 1, 3, 1, 1, 1};

    // Value of N is always 10
    // as we take digit from 0 to 9
    int N = 10;

    // Calling function
    expressDigit(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the
# smallest positive number which
# can not be represented by given digits

# Function to find the smallest
# positive number which can not be
# represented by given digits
def expressDigit(arr, n):

    min = 9
    index = 0

    temp = 0

    # Storing the count of 0 digit
    # or store the value at 0th index
    temp = arr[0]

    # Calculates the min value in
    # the array starting from
    # 1st index and also store its index.
    for i in range(1, 10):

        if(arr[i] < min):
            min = arr[i]
            index = i

    # Now compare the min value with the
    # value at 0th index.

    # If its value at 0th index is
    # less than min value than either
    # 10, 100, 1000 ... can't be expressed
    if(temp < min):
        print(1, end = "")
        for i in range(1, temp + 1):
            print(0, end = "")

    # If its value is greater than
    # min value then iterate the loop
    # upto first min value index and
    # simply print its index value.
    else:
        for i in range(min):
            print(index, end = "")

        print(index)

# Driver code
arr = [2, 2, 1, 2, 1,
       1, 3, 1, 1, 1]

# Value of N is always 10
# as we take digit from 0 to 9
N = 10

# Calling function
expressDigit(arr, N)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the smallest positive
// number which can not be represented by given digits
using System;

class GFG
{

// Function to find the smallest positive
// number which can not be represented by given digits
static void expressDigit(int []arr, int n)
{
    int min = 9, index = 0, temp = 0;

    // Storing the count of 0 digit
    // or store the value at 0th index
    temp = arr[0];

    // Calculates the min value in the array starting
    // from 1st index and also store it index.
    for(int i = 1; i < 10; i++)
    {
        if(arr[i] < min)
        {
            min = arr[i];
            index = i;
        }
    }

    // Now compare the min value with the
    // value at 0th index.

    // If its value at 0th index is less than min value
    // than either 10, 100, 1000 ... can't be expressed
    if(temp < min)
    {
        Console.Write(1);
        for(int i = 1; i <= temp + 1; i++)
            Console.Write(0);
    }

    // If it value is greater than min value than
    // iterate the loop upto first min value index
    // and simply print it index value.
    else
    {
        for(int i = 0; i < min; i++)
            Console.Write(index);

        Console.Write(index);
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {2, 2, 1, 2, 1, 1, 3, 1, 1, 1};

    // Value of N is always 10
    // as we take digit from 0 to 9
    int N = 10;

    // Calling function
    expressDigit(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to find the smallest positive
// number which can not be represented by given digits

    // Function to find the smallest positive
    // number which can not be represented by given digits
    function expressDigit(arr, n)
    {
        var min = 9, index = 0, temp = 0;

        // Storing the count of 0 digit
        // or store the value at 0th index
        temp = arr[0];

        // Calculates the min value in the array starting
        // from 1st index and also store it index.
        for (i = 1; i < 10; i++)
        {
            if (arr[i] < min)
            {
                min = arr[i];
                index = i;
            }
        }

        // Now compare the min value with the
        // value at 0th index.

        // If its value at 0th index is less than min value
        // than either 10, 100, 1000 ... can't be expressed
        if (temp < min)
        {
            document.write(1);
            for (i = 1; i <= temp + 1; i++)
                document.write(0);
        }

        // If it value is greater than min value than
        // iterate the loop upto first min value index
        // and simply prvar it index value.
        else {
            for (i = 0; i < min; i++)
                document.write(index);

            document.write(index);
        }
    }

    // Driver code
        var arr = [ 2, 2, 1, 2, 1, 1, 3, 1, 1, 1 ];

        // Value of N is always 10
        // as we take digit from 0 to 9
        var N = 10;

        // Calling function
        expressDigit(arr, N);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
22
```