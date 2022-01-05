# 根据字符串长度对字符串数组进行排序

> 原文:[https://www . geesforgeks . org/sort-array-strings-resident-string-length/](https://www.geeksforgeeks.org/sort-array-strings-according-string-lengths/)

给我们一个字符串数组，我们需要按照字符串长度的递增顺序对数组进行排序。
**例:**

```
Input : {"GeeksforGeeeks", "I", "from", "am"}
Output : I am from GeeksforGeeks

Input :  {"You", "are", "beautiful", "looking"}
Output : You are looking beautiful
```

一个**简单的解决方案**是编写我们自己的排序函数，比较字符串长度来决定哪个字符串应该先出现。下面是使用[插入排序](https://www.geeksforgeeks.org/insertion-sort/)对数组进行排序的实现。

## C++

```
// C++ program to sort an Array of
// Strings according to their lengths
#include<iostream>
using namespace std;

// Function to print the sorted array of string
void printArraystring(string,int);

// Function to Sort the array of string
// according to lengths. This function
// implements Insertion Sort.
void sort(string s[], int n)
{
    for (int i=1 ;i<n; i++)
    {
        string temp = s[i];

        // Insert s[j] at its correct position
        int j = i - 1;
        while (j >= 0 && temp.length() < s[j].length())
        {
            s[j+1] = s[j];
            j--;
        }
        s[j+1] = temp;
    }
}

// Function to print the sorted array of string
void printArraystring(string str[], int n)
{
    for (int i=0; i<n; i++)
        cout << str[i] << " ";
}

// Driver function
int main()
{
    string arr[] = {"GeeksforGeeks", "I", "from", "am"};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Function to perform sorting
    sort(arr, n);

    // Calling the function to print result
    printArraystring(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an Array of
// Strings according to their lengths
import java.util.*;

class solution
{

// Function to print the sorted array of string
// void printArraystring(string,int);

// Function to Sort the array of string
// according to lengths. This function
// implements Insertion Sort.
static void sort(String []s, int n)
{
    for (int i=1 ;i<n; i++)
    {
        String temp = s[i];

        // Insert s[j] at its correct position
        int j = i - 1;
        while (j >= 0 && temp.length() < s[j].length())
        {
            s[j+1] = s[j];
            j--;
        }
        s[j+1] = temp;
    }
}

// Function to print the sorted array of string
static void printArraystring(String str[], int n)
{
    for (int i=0; i<n; i++)
        System.out.print(str[i]+" ");
}

// Driver function
public static void main(String args[])
{
    String []arr = {"GeeksforGeeks", "I", "from", "am"};
    int n = arr.length;

    // Function to perform sorting
    sort(arr,n);
    // Calling the function to print result
    printArraystring(arr, n);

}
}
```

## 蟒蛇 3

```
# Python3 program to sort an Array of
# Strings according to their lengths

# Function to print the sorted array of string
def printArraystring(string, n):
    for i in range(n):
        print(string[i], end = " ")

# Function to Sort the array of string
# according to lengths. This function
# implements Insertion Sort.
def sort(s, n):
    for i in range(1, n):
        temp = s[i]

        # Insert s[j] at its correct position
        j = i - 1
        while j >= 0 and len(temp) < len(s[j]):
            s[j + 1] = s[j]
            j -= 1

        s[j + 1] = temp

# Driver code
if __name__ == "__main__":
    arr = ["GeeksforGeeks", "I", "from", "am"]
    n = len(arr)

    # Function to perform sorting
    sort(arr, n)

    # Calling the function to print result
    printArraystring(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```

// C# program to sort an Array of
// Strings according to their lengths
using System;

public class solution{

    // Function to print the sorted array of string
    // void printArraystring(string,int);

    // Function to Sort the array of string
    // according to lengths. This function
    // implements Insertion Sort.
    static void sort(String []s, int n)
    {
        for (int i=1 ;i<n; i++)
        {
            String temp = s[i];

            // Insert s[j] at its correct position
            int j = i - 1;
            while (j >= 0 && temp.Length < s[j].Length)
            {
                s[j+1] = s[j];
                j--;
            }
            s[j+1] = temp;
        }
    }

    // Function to print the sorted array of string
    static void printArraystring(String []str, int n)
    {
        for (int i=0; i<n; i++)
            Console.Write(str[i]+" ");
    }

    // Driver function
    public static void Main()
    {
        String []arr = {"GeeksforGeeks", "I", "from", "am"};
        int n = arr.Length;

        // Function to perform sorting
        sort(arr,n);
        // Calling the function to print result
        printArraystring(arr, n);

    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to sort an Array of
    // Strings according to their lengths

    // Function to print the sorted array of string
    // void printArraystring(string,int);

    // Function to Sort the array of string
    // according to lengths. This function
    // implements Insertion Sort.
    function sort(s, n)
    {
        for (let i = 1 ; i < n; i++)
        {
            let temp = s[i];

            // Insert s[j] at its correct position
            let j = i - 1;
            while (j >= 0 && temp.length < s[j].length)
            {
                s[j + 1] = s[j];
                j--;
            }
            s[j + 1] = temp;
        }
    }

    // Function to print the sorted array of string
    function printArraystring(str, n)
    {
        for (let i = 0; i < n; i++)
            document.write(str[i]+" ");
    }

    let arr = ["GeeksforGeeks", "I", "from", "am"];
    let n = arr.length;

    // Function to perform sorting
    sort(arr,n);
    // Calling the function to print result
    printArraystring(arr, n);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output**

```
I am from GeeksforGeeks 
```

一个**更好的解决方案**是使用 C++、Java 等编程语言提供的排序函数。这些函数还允许我们编写自己的自定义比较器。下面是使用 [C++ STL 排序函数](https://www.geeksforgeeks.org/sort-c-stl/)的 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <bits/stdc++.h>
using namespace  std;

// Function to check the small string
bool compare(string &s1,string &s2)
{
    return s1.size() < s2.size();
}

// Function to print the sorted array of string
void printArraystring(string str[], int n)
{
    for (int i=0; i<n; i++)
        cout << str[i] << " ";
}

// Driver function
int main()
{
    string arr[] = {"GeeksforGeeks", "I", "from", "am"};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Function to perform sorting
    sort(arr, arr+n, compare);

    // Calling the function to print result
    printArraystring(arr, n);

    return 0;
}
```

**Output**

```
I am from GeeksforGeeks 
```

### 方法 2:使用 python 中的 sorted()函数的简化解决方案

1.  以字符串为列表。
2.  使用 python 中的排序函数，提供 key 作为 len。

下面是实现:

## 蟒蛇 3

```
# Python code for the above approach
def printsorted(arr):

    # Sorting using sorted function
    # providing key as len
    print(*sorted(arr, key=len))

# Driver code
arr = ["GeeksforGeeks", "I", "from", "am"]

# Passing list to printsorted function
printsorted(arr)

# this code is contributed by vikkycirus
```

**Output**

```
I am from GeeksforGeeks
```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。