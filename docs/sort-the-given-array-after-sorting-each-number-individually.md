# 对每个数字单独排序后，对给定的数组进行排序

> 原文:[https://www . geesforgeks . org/sort-给定数组-排序后-每个数字-单独/](https://www.geeksforgeeks.org/sort-the-given-array-after-sorting-each-number-individually/)

给定一个大小为 **N** 的数组 **arr** ，任务是对数组中每个元素的数字进行排序，然后按非递减顺序对数组进行排序。排序后打印数组。

**示例:**

> **输入:** arr[] = {514，34，41，39}
> **输出:** 41 43 93 541
> **解释:**
> 对数组的每个元素进行排序:arr[] = {145，34，14，39}
> 对数组进行排序:arr[] = {14，34，39，145}
> 
> **输入:** arr[] = {3，1，9，4}
> **输出:** 1 3 4 9

**方法:**按照以下步骤解决这个问题:

1.  创建一个函数**到字符串**，该函数将接受整数 **N** 作为参数，并将返回字符串形式的 **N** 。
2.  将函数**中数组 **arr** 的每个元素传递给字符串**将其转换为字符串。对该字符串进行排序，并将其转换回整数。之后，用数组 **arr** 中转换后的整数替换每个元素。
3.  根据以上观察，对数组 **arr** 进行排序，打印答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print array in non-decreasing order
void printArray(int arr[], int N)
{
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";
}

// Function to convert an integer to string
string toString(int N)
{
    string s;
    while (N > 0) {
        s += (N % 10) + '0';
        N /= 10;
    }

    if (s.size() == 0) {
        s = "0";
    }

    return s;
}

// Function to sort each element of the array
// in non-descreasing order of its digits
void digitSort(int arr[], int N)
{

    // Travering each element to sort
    for (int i = 0; i < N; i++) {

        // Converting number to string
        string s = toString(arr[i]);

        // Sorting string
        sort(s.begin(), s.end());

        // Converting string to integer
        arr[i] = stoi(s);
    }

    // Sorting array
    sort(arr, arr + N);

    // Printing array
    printArray(arr, N);
}

// Driver Code
int main()
{
    int arr[] = { 514, 34, 41, 39 };
    int N = sizeof(arr) / sizeof(arr[0]);
    digitSort(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to print array in non-decreasing order
static void printArray(int arr[], int N)
{
    for (int i = 0; i < N; i++)
        System.out.print(arr[i] + " ");
}

// Function to convert an integer to String
static String toString(int N)
{
    String s = "";
    while (N > 0) {
        s += String.valueOf((N % 10)) + '0';
        N /= 10;
    }

    if (s.length() == 0) {
        s = "0";
    }

    return s;
}

// Function to sort each element of the array
// in non-descreasing order of its digits
static void digitSort(int arr[], int N)
{

    // Travering each element to sort
    for (int i = 0; i < N; i++) {

        // Converting number to String
        String s = toString(arr[i]);

        // Sorting String
        s = sort(s);

        // Converting String to integer
        arr[i] = Integer.valueOf(s);
    }

    // Sorting array
    Arrays.sort(arr);

    // Printing array
    printArray(arr, N);
}
static String sort(String inputString)
{

    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 514, 34, 41, 39 };
    int N = arr.length;
    digitSort(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to print array in non-decreasing order
def printArray(arr, N):

    for i in range(0, N):
        print(arr[i], end=" ")

# Function to convert an integer to string
def toString(N):

    s = ""
    while (N > 0):
        s += chr(int(N % 10) + ord('0'))
        N /= 10

    if (len(s) == 0):
        s = "0"

    return s

# Function to sort each element of the array
# in non-descreasing order of its digits
def digitSort(arr, N):

    # Travering each element to sort
    for i in range(0, N):

        # Converting number to string
        s = toString(arr[i])

        # Sorting string
        s = list(s)
        s.sort()
        s = ''.join(s)

        # Converting string to integer
        arr[i] = int(s)

        # Sorting array
    arr.sort()

    # Printing array
    printArray(arr, N)

# Driver Code
if __name__ == "__main__":

    arr = [514, 34, 41, 39]
    N = len(arr)
    digitSort(arr, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// Java program for the above approach
using System;
using System.Collections;
class GFG
{

// Function to print array in non-decreasing order
static void printArray(int []arr, int N)
{
    for (int i = 0; i < N; i++)
        Console.Write(arr[i] + " ");
}

// Function to convert an integer to string
static String toString(int N)
{
    string s = "";
    while (N > 0) {
        int val = N % 10;
        s += val.ToString();
        N /= 10;
    }

    if (s.Length == 0) {
        s = "0";
    }

    return s;
}

// Function to sort each element of the array
// in non-descreasing order of its digits
static void digitSort(int []arr, int N)
{

    int []ans = new int[N];

    // Travering each element to sort
    for (int i = 0; i < N; i++) {

        // Converting number to string
        String s = toString(arr[i]);

        char []ch = s.ToCharArray();
        Array.Sort(ch);
        ans[i] = Int32.Parse(String.Join("",ch));

        // Converting string to integer
        arr[i] = Int32.Parse(s);
    }

    // Sorting array
    Array.Sort(ans);

    // Printing array
    printArray(ans, N);
}

// Driver Code
public static void Main()
{
    int []arr = { 514, 34, 41, 39 };
    int N = arr.Length;
    digitSort(arr, N);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print array in
// non-decreasing order
function printArray(arr, N)
{
    for(let i = 0; i < N; i++)
        document.write(arr[i] + " ");
}

// Function to convert an integer to string
function toString(N)
{
    let s = "";
    while (N > 0)
    {
        s = s + (N % 10).toString();
        N = Math.floor(N / 10);
    }

    if (s.length == 0)
    {
        s = "0";
    }
    return s;
}

// Function to sort each element of the array
// in non-descreasing order of its digits
function digitSort(arr, N)
{

    // Travering each element to sort
    for(let i = 0; i < N; i++)
    {

        // Converting number to string
        let s = arr[i].toString();

        // Sorting string
        st = s.split('')
        st.sort(function (a, b){
            return a.charCodeAt(0) -
                   b.charCodeAt(0); });
        s = '';

        for(let i = 0; i < st.length; i++)
        {
            s = s + st[i];
        }

        // Converting string to integer
        arr[i] = parseInt(s);
    }

    // Sorting array
    arr.sort(function(a, b){ return a - b })

    // Printing array
    printArray(arr, N);
}

// Driver Code
let arr = [ 514, 34, 41, 39 ];
let N = arr.length;

digitSort(arr, N);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
14 34 39 145 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)