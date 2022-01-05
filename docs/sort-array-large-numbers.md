# 对一个大数数组进行排序

> 原文:[https://www.geeksforgeeks.org/sort-array-large-numbers/](https://www.geeksforgeeks.org/sort-array-large-numbers/)

给定一个数字数组，其中每个数字都表示为字符串。数字可能非常大(可能不适合 long long int)，任务是对这些数字进行排序。
**例:**

```
Input : arr[] = {"5", "1237637463746732323", "12" };
Output : arr[] = {"5", "12", "1237637463746732323"};

Input : arr[] = {"50", "12", "12", "1"};
Output : arr[] = {"1", "12", "12", "50"};
```

以下是上述想法的实现。

## C++

```
// C++ program to sort large numbers represented
// as strings.
#include<bits/stdc++.h>
using namespace std;

// Returns true if str1 is smaller than str2.
bool compareNumbers(string str1, string str2)
{
    // Calculate lengths of both string
    int n1 = str1.length(), n2 = str2.length();

    if (n1 < n2)
       return true;
    if (n2 < n1)
       return false;

    // If lengths are same
    for (int i=0; i<n1; i++)
    {
       if (str1[i] < str2[i])
          return true;
       if (str1[i] > str2[i])
          return false;
    }

    return false;
}

// Function for sort an array of large numbers
// represented as strings
void sortLargeNumbers(string arr[], int n)
{
   sort(arr, arr+n, compareNumbers);
}

// Driver code
int main()
{
    string arr[] = {"5", "1237637463746732323",
                    "97987", "12" };
    int n = sizeof(arr)/sizeof(arr[0]);

    sortLargeNumbers(arr, n);

    for (int i=0; i<n; i++)
      cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort large numbers represented
// as strings.
import java.io.*;
import java.util.*;

class main
{
    // Function for sort an array of large numbers
    // represented as strings
    static void sortLargeNumbers(String arr[])
    {
        // Refer below post for understanding below expression:
        // https://www.geeksforgeeks.org/lambda-expressions-java-8/
        Arrays.sort(arr, (left, right) ->
        {
            /* If length of left != right, then return
               the diff of the length else  use compareTo
               function to compare values.*/
            if (left.length() != right.length())
                return left.length() - right.length();
             return left.compareTo(right);
        });
    }

    // Driver code
    public static void main(String args[])
    {
        String arr[] = {"5", "1237637463746732323",
                        "97987", "12" };
        sortLargeNumbers(arr);
        for (String s : arr)
            System.out.print(s + " ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to sort large numbers
# represented as strings

# Function for sort an array of large
# numbers represented as strings
def sortLargeNumbers (arr, n):

    arr.sort(key = int)

# Driver Code
if __name__ == '__main__':

    arr = [ "5", "1237637463746732323",
            "97987", "12" ]
    n = len(arr)

    sortLargeNumbers(arr, n)

    for i in arr:
        print(i, end = ' ')

# This code is contributed by himanshu77
```

## C#

```
// C# program to sort large numbers
// represented as strings.
using System;

class GFG
{

    // Function for sort an array of large
    // numbers represented as strings
    static void sortLargeNumbers(String []arr)
    {
        // Refer below post for understanding 
        // below expression:
        // https://www.geeksforgeeks.org/lambda-expressions-java-8/
        for(int i = 0; i < arr.Length - 1; i++)
        {
            /* If length of left != right, then
            return the diff of the length else
            use compareTo function to compare values.*/
            String left = arr[i], right = arr[i + 1];
            if (left.Length > right.Length)
            {
                arr[i] = right;
                arr[i + 1] = left;
                i -= 2;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        String []arr = {"5", "1237637463746732323",
                        "97987", "12" };
        sortLargeNumbers(arr);
        foreach (String s in arr)
            Console.Write(s + " ");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to sort large numbers
// represented as strings.

    // Function for sort an array of large numbers
    // represented as strings
    function sortLargeNumbers(arr)
    {
         // Refer below post for understanding 
        // below expression:
        // https://www.geeksforgeeks.org/lambda-expressions-java-8/
        for(let i = 0; i < arr.length - 1; i++)
        {
            /* If length of left != right, then
            return the diff of the length else
            use compareTo function to compare values.*/
            let left = arr[i], right = arr[i + 1];
            if (left.length > right.length)
            {
                arr[i] = right;
                arr[i + 1] = left;
                i -= 2;
            }
        }
    }

// Driver Code
     let arr = ["5", "1237637463746732323",
                        "97987", "12" ];
        sortLargeNumbers(arr);
        for (let s in arr)
            document.write(arr[s] + " ");

</script>
```

**输出:**

```
5 12 97987 1237637463746732323 
```

**时间复杂度:** O(k * n Log n)，其中 k 为最长数字的长度。这里的假设是 sort()函数使用 O(n Log n)排序算法。
**相似帖:**
[整理大整数](https://www.geeksforgeeks.org/sorting-big-integers/)
本文由 [**丹麦语【KALEM】**](https://www.linkedin.com/in/mohdanishh/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。