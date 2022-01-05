# 给表示为数组的数字加 1 |递归方法

> 原文:[https://www . geesforgeks . org/add-1-number-presented-array/](https://www.geeksforgeeks.org/add-1-number-represented-array/)

给定一个代表数字的数组，给数组加 1。假设一个数组包含元素[1，2，3，4]，那么这个数组代表十进制数 1234，因此加 1 会得到 1235。所以新数组将是[1，2，3，5]。
示例:

```
Input :  [1, 2, 3, 4]
Output : [1, 2, 3, 5]

Input :  [1, 2, 9, 9]
Output : [1, 3, 0, 0]

Input:  [9, 9, 9, 9]
Output: [1, 0, 0, 0, 0]
```

**进场:**
1。如果数组的最后一个元素小于 9，则加 1。
2。如果它是 9，那么使它为 0，并为数组的剩余元素递归。

## C++

```
// C++ Program to add 1 to an array
// representing a number
#include <bits/stdc++.h>
using namespace std;

// function to add one and print the array
void sum(int arr[], int n)
{

 int i = n;

 // if array element is less than 9, then
 // simply add 1 to this.
 if(arr[i] < 9)
 {
     arr[i] = arr[i] + 1;
     return;
 }

 // if array element is greater than 9,
 // replace it with 0 and decrement i
    arr[i] = 0;
    i--;

    // recursive function
    sum(arr, i);
}

// driver code
int main()
{
    // number of elements in array
    int n = 4;

    // array elements, index of array
    // should be 1 based, hence, 0 is
    // added here at arr[0]
    int arr[] = {0, 1, 9, 3, 9};

    // function calling
    sum(arr, n);

    // If 1 was appended at head
    // of array then, print it
    if(arr[0] > 0)
        cout << arr[0] << ", ";

    // print the array elements
    // after adding one
    for(int i = 1; i <= n; i++)
    {
            cout << arr[i];

            if(i < n)
                cout << ", ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to add 1 to an array
// representing a number
import java.io.*;

public class GFG {

    // function to add one and print the array
    void sum(int[] arr, int n)
    {
        int i = n;

        // if array element is less than 9, then
        // simply add 1 to this.
        if (arr[i] < 9) {
            arr[i] = arr[i] + 1;
            return;
        }

        // if array element is greater than 9,
        // replace it with 0 and decrement i
        arr[i] = 0;
        i--;

        // recursive function
        sum(arr, i);
    }

    // driver code
    static public void main(String[] args)
    {
        GFG obj = new GFG();

        // number of elements in array
        int n = 4;

        // array elements, index of array
        // should be 1 based, hence, 0 is
        // added here at arr[0]
        int arr[] = {0, 1, 9, 3, 9};

        obj.sum(arr, n);

        // If 1 was appended at head
        // of array then, print it
        if (arr[0] > 0)
            System.out.print(arr[0] + ", ");

        int i;
        for (i = 1; i <= n; i++) {
            System.out.print(arr[i]);

            if (i < n)
                System.out.print(", ");
        }

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 Program to add 1 to an
# array representing a number

# function to add one and print
# the array
def sum(arr, n):

    i = n

    # if array element is less than
    # 9, then simply add 1 to this.
    if(arr[i] < 9):

        arr[i] = arr[i] + 1
        return

    # if array element is greater
    # than 9, replace it with 0
    # and decrement i
    arr[i] = 0
    i -= 1

    # recursive function
    sum(arr, i)

# driver code
# number of elements in array
n = 4

# array elements, index of array
# should be 1 based, hence, 0 is
# added here at arr[0]
arr = [0, 1, 9, 3, 9]

# function calling
sum(arr, n)

# If 1 was appended at head
# of array then, print it
if(arr[0] > 0):
    print(arr[0], ", ", end="")

# print the array elements
# after adding one
for i in range(1, n+1):

    print(arr[i], end="")
    if(i < n):
        print(", ", end="")

# This code is contributed by
# Smitha Semwal
```

## C#

```
// C# Program to add 1 to an array
// representing a number
using System;

public class GFG {

    // function to add one and print the array
    void sum(int []arr, int n){

    int i = n;

    // if array element is less than 9, then
    // simply add 1 to this.
    if(arr[i] < 9)
    {
      arr[i] = arr[i] + 1;
      return;
    }

    // if array element is greater than 9,
    // replace it with 0 and decrement i
    arr[i] = 0;
    i--;

    // recursive function
    sum(arr, i);
}

    // driver code
    static public void Main ()
    {
      GFG obj =new GFG();

    // number of elements in array
    int n = 4;

    // array elements, index of array
    // should be 1 based, hence, 0 is
    // added here at arr[0]
    int []arr = {0, 1, 9, 3, 9};

    // function calling
    obj.sum(arr, n);

    // If 1 was appended at head
    // of array then, print it
    if(arr[0] > 0)
        Console.Write(arr[0] + ", ");
    int i;
    // print the array elements
    // after adding one
    for( i = 1; i <= n; i++)
    {
        Console.Write(arr[i]);

        if(i < n)
            Console.Write(", ");
    }

    }
}
```

## java 描述语言

```
<script>
// JavaScript Program to add 1 to an array
// representing a number

// function to add one and print the array
function sum(arr, n)
{

 var i = n;

 // if array element is less than 9, then
 // simply add 1 to this.
 if(arr[i] < 9)
 {
     arr[i] = arr[i] + 1;
     return;
 }

 // if array element is greater than 9,
 // replace it with 0 and decrement i
    arr[i] = 0;
    i--;

    // recursive function
    sum(arr, i);
}

// Driver code

    // number of elements in array
    var n = 4;

    // array elements, index of array
    // should be 1 based, hence, 0 is
    // added here at arr[0]
    arr = [0, 1, 9, 3, 9]

    // function calling
    sum(arr, n);

    // If 1 was appended at head
    // of array then, print it
    if(arr[0] > 0)
        document.write(arr[0] + ", ");

    // print the array elements
    // after adding one
    for(var i = 1; i <= n; i++)
    {
            document.write(arr[i]);    
            if(i < n)
                document.write(", ");
    }

// This code is contributed by rdtank.
    </script>
```

输出:

```
1, 9, 4, 0
```