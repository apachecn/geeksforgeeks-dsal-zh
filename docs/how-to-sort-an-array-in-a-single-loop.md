# 如何在单个循环中对数组进行排序？

> 原文:[https://www . geesforgeks . org/如何对单循环数组进行排序/](https://www.geeksforgeeks.org/how-to-sort-an-array-in-a-single-loop/)

给定一个大小为 N 的数组，任务是使用单个循环对该数组进行排序。
**<u>数组通常是如何排序的？</u>**
有很多方法可以将数组按升序排序，比如:

*   [选择排序](https://www.geeksforgeeks.org/selection-sort/)
*   [二进制排序](https://www.geeksforgeeks.org/binary-search/)
*   [合并排序](https://www.geeksforgeeks.org/merge-sort/)
*   [基数排序](https://www.geeksforgeeks.org/radix-sort/)
*   [插入输出](https://www.geeksforgeeks.org/insertion-sort/)等

在这些方法中的任何一种中，**使用超过 1 个循环**。
**<u>数组可以使用单个循环排序吗？</u>**
由于所有已知的排序方法都使用 1 个以上的循环，很难想象单个循环也能做到同样的效果。实际上，这样做并非不可能。但这样做不会是最有效的。
**示例 1:** 下面的代码将使用整数元素对数组进行排序。

## C++

```
// C++ code to sort an array of integers
// with the help of single loop
#include<bits/stdc++.h>
using namespace std;

// Function for Sorting the array
// using a single loop
int *sortArrays(int arr[], int length)
{

    // Sorting using a single loop
    for (int j = 0; j < length - 1; j++)
    {
        // Checking the condition for two
        // simultaneous elements of the array
        if (arr[j] > arr[j + 1])
        {
            // Swapping the elements.
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;

            // updating the value of j = -1
            // so after getting updated for j++
            // in the loop it becomes 0 and
            // the loop begins from the start.
            j = -1;
        }
    }
    return arr;
}

// Driver code
int main()
{
    // Declaring an integer array of size 11.
    int arr[] = { 1, 2, 99, 9, 8,
                7, 6, 0, 5, 4, 3 };

    // Printing the original Array.
    int length = sizeof(arr)/sizeof(arr[0]);
    string str;
    for (int i: arr)
    {
        str += to_string(i)+" ";
    }
    cout<<"Original array: ["
                    << str << "]" << endl;

    // Sorting the array using a single loop
    int *arr1;
    arr1 = sortArrays(arr, length);

    // Printing the sorted array.
    string str1;
    for (int i = 0; i < length; i++)
    {
        str1 += to_string(arr1[i])+" ";
    }
    cout << "Sorted array: ["
                    << (str1) << "]";
}

// This code is contributed by Rajout-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to sort an array of integers
// with the help of single loop

import java.util.*;

class Geeks_For_Geeks {

    // Function for Sorting the array
    // using a single loop
    public static int[] sortArrays(int[] arr)
    {

        // Finding the length of array 'arr'
        int length = arr.length;

        // Sorting using a single loop
        for (int j = 0; j < length - 1; j++) {

            // Checking the condition for two
            // simultaneous elements of the array
            if (arr[j] > arr[j + 1]) {

                // Swapping the elements.
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;

                // updating the value of j = -1
                // so after getting updated for j++
                // in the loop it becomes 0 and
                // the loop begins from the start.
                j = -1;
            }
        }

        return arr;
    }

    // Declaring main method
    public static void main(String args[])
    {
        // Declaring an integer array of size 11.
        int arr[] = { 1, 2, 99, 9, 8,
                      7, 6, 0, 5, 4, 3 };

        // Printing the original Array.
        System.out.println("Original array: "
                           + Arrays.toString(arr));

        // Sorting the array using a single loop
        arr = sortArrays(arr);

        // Printing the sorted array.
        System.out.println("Sorted array: "
                           + Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 code to sort an array of integers
# with the help of single loop

# Function for Sorting the array
# using a single loop
def sortArrays(arr):

    # Finding the length of array 'arr'
    length = len(arr)

    # Sorting using a single loop
    j = 0

    while j < length - 1:

        # Checking the condition for two
        # simultaneous elements of the array
        if (arr[j] > arr[j + 1]):

            # Swapping the elements.
            temp = arr[j]
            arr[j] = arr[j + 1]
            arr[j + 1] = temp

            # updating the value of j = -1
            # so after getting updated for j++
            # in the loop it becomes 0 and
            # the loop begins from the start.
            j = -1
        j += 1

    return arr

# Driver Code
if __name__ == '__main__':

    # Declaring an integer array of size 11.
    arr = [1, 2, 99, 9, 8,
           7, 6, 0, 5, 4, 3]

    # Printing the original Array.
    print("Original array: ", arr)

    # Sorting the array using a single loop
    arr = sortArrays(arr)

    # Printing the sorted array.
    print("Sorted array: ", arr)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# code to sort an array of integers
// with the help of single loop
using System;

class GFG
{

    // Function for Sorting the array
    // using a single loop
    public static int[] sortArrays(int[] arr)
    {

        // Finding the length of array 'arr'
        int length = arr.Length;

        // Sorting using a single loop
        for (int j = 0; j < length - 1; j++)
        {

            // Checking the condition for two
            // simultaneous elements of the array
            if (arr[j] > arr[j + 1])
            {

                // Swapping the elements.
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;

                // updating the value of j = -1
                // so after getting updated for j++
                // in the loop it becomes 0 and
                // the loop begins from the start.
                j = -1;
            }
        }
        return arr;
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Declaring an integer array of size 11.
        int []arr = { 1, 2, 99, 9, 8,
                    7, 6, 0, 5, 4, 3 };

        // Printing the original Array.
        Console.WriteLine("Original array: " +
                           String.Join(", ", arr));

        // Sorting the array using a single loop
        arr = sortArrays(arr);

        // Printing the sorted array.
        Console.WriteLine("Sorted array: " +
                           String.Join(", ", arr));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript code to sort an array of integers
// with the help of single loop

// Function for Sorting the array
    // using a single loop
function sortArrays(arr)
{

    // Finding the length of array 'arr'
        let length = arr.length;

        // Sorting using a single loop
        for (let j = 0; j < length - 1; j++) {

            // Checking the condition for two
            // simultaneous elements of the array
            if (arr[j] > arr[j + 1]) {

                // Swapping the elements.
                let temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;

                // updating the value of j = -1
                // so after getting updated for j++
                // in the loop it becomes 0 and
                // the loop begins from the start.
                j = -1;
            }
        }

        return arr;
}

// Declaring main method
let arr=[1, 2, 99, 9, 8,
                      7, 6, 0, 5, 4, 3];
document.write("Original array: ["
                           + (arr).join(", ")+"]<br>");
// Sorting the array using a single loop
arr = sortArrays(arr);

// Printing the sorted array.
document.write("Sorted array: ["
                   + arr.join(", ")+"]<br>");

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Original array: [1, 2, 99, 9, 8, 7, 6, 0, 5, 4, 3]
Sorted array: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 99]
```

**示例 2:** 下面的代码将对字符串数组进行排序。

## C++

```
// C++ code to sort an array of Strings
// with the help of single loop
#include<bits/stdc++.h>
using namespace std;

// Function for Sorting the array using a single loop
char* sortArrays(char arr[], int length)
{
    // Sorting using a single loop
    for (int j = 0; j < length - 1; j++)
    {

        // Type Conversion of char to int.
        int d1 = arr[j];
        int d2 = arr[j + 1];

        // Comparing the ascii code.
        if (d1 > d2)
        {

            // Swapping of the characters
            char temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
            j = -1;
        }
    }
    return arr;
}

// Driver code
int main()
{

    // Declaring a String
    string geeks = "GEEKSFORGEEKS";
    int n = geeks.length();

    // declaring character array
    char arr[n];

    // copying the contents of the
    // string to char array
    for(int i = 0; i < n; i++)
    {
        arr[i] = geeks[i];
    }

    // Printing the original Array.
    cout<<"Original array: [";
    for(int i = 0; i < n; i++)
    {
        cout << arr[i];
        if(i + 1 != n)
        cout<<", ";
    }
    cout << "]" << endl;

    // Sorting the array using a single loop
    char *ansarr;
    ansarr = sortArrays(arr, n);

    // Printing the sorted array.
    cout << "Sorted array: [";
    for(int i = 0; i < n; i++)
    {
        cout << ansarr[i];
        if(i + 1 != n)
        cout << ", ";
    }
    cout << "]" << endl;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to sort an array of Strings
// with the help of single loop

import java.util.*;

class Geeks_For_Geeks {

    // Function for Sorting the array using a single loop
    public static char[] sortArrays(char[] arr)
    {

        // Finding the length of array 'arr'
        int length = arr.length;

        // Sorting using a single loop
        for (int j = 0; j < arr.length - 1; j++) {

            // Type Conversion of char to int.
            int d1 = arr[j];
            int d2 = arr[j + 1];

            // Comparing the ascii code.
            if (d1 > d2) {

                // Swapping of the characters
                char temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                j = -1;
            }
        }

        return arr;
    }

    // Declaring main method
    public static void main(String args[])
    {

        // Declaring a String
        String geeks = "GEEKSFORGEEKS";

        // Declaring a character array
        // to store characters of geeks in it.
        char arr[] = geeks.toCharArray();

        // Printing the original Array.
        System.out.println("Original array: "
                           + Arrays.toString(arr));

        // Sorting the array using a single loop
        arr = sortArrays(arr);

        // Printing the sorted array.
        System.out.println("Sorted array: "
                           + Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 code to sort an array of Strings
# with the help of single loop

# Function for Sorting the array using a single loop
def sortArrays(arr, length):

    # Sorting using a single loop
    j = 0
    while(j < length - 1):

        # Type Conversion of char to int.
        d1 = arr[j]
        d2 = arr[j + 1]

        # Comparing the ascii code.
        if (d1 > d2):

            # Swapping of the characters
            temp = arr[j]
            arr[j] = arr[j + 1]
            arr[j + 1] = temp
            j = -1
        j += 1
    return arr

# Driver code

# Declaring a String
geeks = "GEEKSFORGEEKS"
n = len(geeks)

# declaring character array
arr=[0]*n

# copying the contents of the
# string to char array
for i in range(n):
    arr[i] = geeks[i]

# Printing the original Array.
print("Original array: [",end="")

for i in range(n):
    print(arr[i],end="")

    if (i + 1 != n):
        print(", ",end="")

print("]")

# Sorting the array using a single loop
ansarr = sortArrays(arr, n)

# Printing the sorted array.
print("Sorted array: [",end="")

for i in range(n):
    print(ansarr[i],end="")

    if (i + 1 != n):
        print(", ",end="")

print("]")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# code to sort an array of Strings
// with the help of single loop
using System;

class GFG
{

    // Function for Sorting the array
    // using a single loop
    public static char[] sortArrays(char[] arr)
    {

        // Finding the length of array 'arr'
        int length = arr.Length;

        // Sorting using a single loop
        for (int j = 0; j < arr.Length - 1; j++)
        {

            // Type Conversion of char to int.
            int d1 = arr[j];
            int d2 = arr[j + 1];

            // Comparing the ascii code.
            if (d1 > d2)
            {

                // Swapping of the characters
                char temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                j = -1;
            }
        }
        return arr;
    }

    // Declaring main method
    public static void Main(String []args)
    {

        // Declaring a String
        String geeks = "GEEKSFORGEEKS";

        // Declaring a character array
        // to store characters of geeks in it.
        char []arr = geeks.ToCharArray();

        // Printing the original Array.
        Console.WriteLine("Original array: [" +
                           String.Join(", ", arr) + "]");

        // Sorting the array using a single loop
        arr = sortArrays(arr);

        // Printing the sorted array.
        Console.WriteLine("Sorted array: [" +
                           String.Join(", ", arr) + "]");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript code to sort an array of integers
// with the help of single loop

// Function for Sorting the array
// using a single loop
function sortArrays(arr)
{

        // Finding the length of array 'arr'
        let length = arr.length;

        // Sorting using a single loop
        for (let j = 0; j < length - 1; j++)
        {

            // Type Conversion of char to int.
            let d1 = arr[j];
            let d2 = arr[j + 1];

            // Comparing the ascii code.
            if (d1 > d2)
            {

                // Swapping of the characters
                let temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                j = -1;
            }
        }
        return arr;
    }

            // Declaring a String
        let geeks = "GEEKSFORGEEKS";

        // Declaring a character array
        // to store characters of geeks in it.
        let arr = geeks.split("");

     document.write("Original array: ["
                           + arr.join(", ")+"]<br>");
// Sorting the array using a single loop
arr = sortArrays(arr);

// Printing the sorted array.
document.write("Sorted array: ["
                   + (arr).join(", ")+"]<br>");              

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
Original array: [G, E, E, K, S, F, O, R, G, E, E, K, S]
Sorted array: [E, E, E, E, F, G, G, K, K, O, R, S, S]
```

**<u>单循环排序数组比多循环排序好吗？</u>**
单循环排序虽然看起来更好，但并不是一种高效的方法。以下是使用单循环排序前需要考虑的几点:

*   使用单个循环只会缩短代码
*   排序的时间复杂度在单个循环中不会改变(与多个循环排序相比)
*   单循环排序表明循环数与算法的时间复杂度关系不大。