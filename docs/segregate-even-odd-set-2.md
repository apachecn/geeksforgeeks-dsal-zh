# 隔离偶数和奇数|设置 2

> 原文:[https://www.geeksforgeeks.org/segregate-even-odd-set-2/](https://www.geeksforgeeks.org/segregate-even-odd-set-2/)

给定一个整数数组，隔离数组中的偶数和奇数。所有的偶数应该先出现，然后是奇数。
示例:

```
Input : 1 9 5 3 2 6 7 11
Output : 6 2 3 5 2 9 11 1

Input : 1 3 2 4 7 6 9 10
Output : 10 2 6 4 7 9 3 1
```

我们已经在[中讨论了一种分离偶数和奇数](https://www.geeksforgeeks.org/segregate-even-and-odd-numbers/)的方法。在这篇文章中，讨论了一种不同的更简单的方法，它使用了一个额外的数组。
T3】进场:T5】1。从数组的左边和右边开始两个指针。
2。创建一个与给定大小相同的新数组。
3。如果左边或右边的元素是偶数，那么把它放在数组的前面。

## C++

```
// CPP code to segregate even odd
// numbers in an array
#include <bits/stdc++.h>
using namespace std;

// Function to segregate even odd numbers
void arrayEvenAndOdd(int arr[], int n) {

  int b[n];  // To store result
  int k = 0, l = n - 1, i, j;
  for (i = 0, j = n - 1; i < j; i++, j--) {

    if (arr[i] % 2 == 0) {
      b[k] = arr[i];
      k++;
    } else {
      b[l] = arr[i];
      l--;
    }

    if (arr[j] % 2 == 0) {
      b[k] = arr[j];
      k++;
    } else {
      b[l] = arr[j];
      l--;
    }
  }

  // for i == j in case of odd length
  b[i] = arr[i];

  // Printing segregated array
  for (int i = 0; i < n; i++)
     cout << b[i] << " "; 
}

// Driver code
int main() {
  int arr[] = {1, 3, 2, 4, 7, 6, 9, 10};
  int n = sizeof(arr) / sizeof(int);
  arrayEvenAndOdd(arr, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to segregate even odd
// numbers in an array
import java.util.Arrays;

class arr
{
    // Function to segregate even odd numbers
    static void arrayEvenAndOdd(int arr[], int n)
    {
        // To store result
        int b[] = new int[n];
        int k = 0, l = n - 1, i, j;
        for (i = 0, j = n - 1; i < j; i++, j--)
        {

            if (arr[i] % 2 == 0)
            {
                b[k] = arr[i];
                k++;
            }
            else
            {
                b[l] = arr[i];
                l--;
            }

            if (arr[j] % 2 == 0)
            {
                b[k] = arr[j];
                k++;
            }
            else
            {
                b[l] = arr[j];
                l--;
            }
        }

        // for i == j in case of odd length
        b[i] = arr[i];

        // Printing segregated array
        for (i = 0; i < n; i++)
        {
            System.out.print(b[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 3, 2, 4, 7, 6, 9, 10};
        int n = arr.length;
        arrayEvenAndOdd(arr, n);
    }
}

// This code is contributed
// by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 code to segregate even odd
# numbers in an array

# Function to segregate even odd numbers
def arrayEvenAndOdd(arr,n): 

    b = [0] * n  # To store result
    k = 0
    l = n - 1
    i = 0
    j = n-1
    while(i < j):
        if (arr[i] % 2 == 0): 
            b[k] = arr[i]
            k+=1
        else: 
            b[l] = arr[i]
            l-=1
        if (arr[j] % 2 == 0): 
            b[k] = arr[j]
            k+=1
        else: 
            b[l] = arr[j]
            l-=1
        i+=1
        j-=1

    # for i == j in case of odd length
    b[i] = arr[i]

    # Printing segregated array
    for i in range(0, n):
        print(b[i],end=" ") 

# Driver code
arr =  [1, 3, 2, 4, 7, 6, 9, 10] 
n = len(arr)

arrayEvenAndOdd(arr, n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# code to segregate even odd
// numbers in an array
using System;

class GFG {

    // Function to segregate even odd numbers
    static void arrayEvenAndOdd(int []arr, int n)
    {

        // To store result
        int []b = new int[n];
        int k = 0, l = n - 1, i, j;
        for (i = 0, j = n - 1; i < j; i++, j--)
        {

            if (arr[i] % 2 == 0)
            {
                b[k] = arr[i];
                k++;
            }
            else
            {
                b[l] = arr[i];
                l--;
            }

            if (arr[j] % 2 == 0)
            {
                b[k] = arr[j];
                k++;
            }
            else
            {
                b[l] = arr[j];
                l--;
            }
        }

        // for i == j in case of odd length
        b[i] = arr[i];

        // Printing segregated array
        for (i = 0; i < n; i++)
        {
            Console.Write(b[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 3, 2, 4, 7, 6, 9, 10};
        int n = arr.Length;
        arrayEvenAndOdd(arr, n);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
// Java  scriptcode to segregate even odd
// numbers in an array

    // Function to segregate even odd numbers
    function arrayEvenAndOdd(arr,n)
    {
        // To store result
        let b=[n];
        let k = 0, l = n - 1, i, j;
        for (i = 0, j = n - 1; i < j; i++, j--)
        {

            if (arr[i] % 2 == 0)
            {
                b[k] = arr[i];
                k++;
            }
            else
            {
                b[l] = arr[i];
                l--;
            }

            if (arr[j] % 2 == 0)
            {
                b[k] = arr[j];
                k++;
            }
            else
            {
                b[l] = arr[j];
                l--;
            }
        }

        // for i == j in case of odd length
        b[i] = arr[i];

        // Printing segregated array
        for (i = 0; i < n; i++)
        {
            document.write(b[i] + " ");
        }
    }

    // Driver code

        let arr = [1, 3, 2, 4, 7, 6, 9, 10];
        let n = arr.length;
        arrayEvenAndOdd(arr, n);

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
10 2 6 4 7 9 3 1
```

时间复杂度:O(n/2)
辅助空间:O(n)