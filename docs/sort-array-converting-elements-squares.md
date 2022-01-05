# 将元素转换为方块后对数组进行排序

> 原文:[https://www . geesforgeks . org/sort-array-converting-elements-squares/](https://www.geeksforgeeks.org/sort-array-converting-elements-squares/)

给定一个排序的正负整数数组“arr[]”。任务是对数组中数字的平方进行排序。
**例:**

```
Input  : arr[] =  {-6, -3, -1, 2, 4, 5}
Output : 1, 4, 9, 16, 25, 36 

Input  : arr[] = {-5, -4, -2, 0, 1}
Output : 0, 1, 4, 16, 25
```

**简单的解决方法**是先将每个数组元素转换成它的平方，然后应用任意“O(nlogn)”排序算法对数组元素进行排序。

下面是上述想法的实现

## C++

```
// C++ program to Sort square of the numbers
// of the array
#include <bits/stdc++.h>
using namespace std;

// Function to sort an square array
void sortSquares(int arr[], int n)
{
    // First convert each array elements
    // into its square
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] * arr[i];

    // Sort an array using "sort STL function "
    sort(arr, arr + n);
}

// Driver program to test above function
int main()
{
    int arr[] = { -6, -3, -1, 2, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Before sort " << endl;
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    sortSquares(arr, n);

    cout << "\nAfter Sort " << endl;
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Sort square of the numbers
// of the array
import java.util.*;
import java.io.*;

class GFG {
    // Function to sort an square array
    public static void sortSquares(int arr[])
    {
        int n = arr.length;

        // First convert each array elements
        // into its square
        for (int i = 0; i < n; i++)
            arr[i] = arr[i] * arr[i];

        // Sort an array using "inbuild sort function"
        // in Arrays class.
        Arrays.sort(arr);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int arr[] = { -6, -3, -1, 2, 4, 5 };
        int n = arr.length;

        System.out.println("Before sort ");
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");

        sortSquares(arr);
        System.out.println("");
        System.out.println("After Sort ");
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}
```

## 蟒蛇 3

```
# Python program to Sort square
# of the numbers of the array

# Function to sort an square array
def sortSquare(arr, n):

    # First convert each array
    # elements into its square
    for i in range(n):
        arr[i]= arr[i] * arr[i]
    arr.sort()

# Driver code
arr = [-6, -3, -1, 2, 4, 5]
n = len(arr)

print("Before sort")
for i in range(n):
    print(arr[i], end = " ")

print("\n")

sortSquare(arr, n)

print("After sort")
for i in range(n):
    print(arr[i], end = " ")

# This code is contributed by
# Shrikant13
```

## C#

```
// C# program to Sort square
// of the numbers of the array
using System;

class GFG {

    // Function to sort
    // an square array
    public static void sortSquares(int[] arr)
    {
        int n = arr.Length;

        // First convert each array
        // elements into its square
        for (int i = 0; i < n; i++)
            arr[i] = arr[i] * arr[i];

        // Sort an array using
        // "inbuild sort function"
        // in Arrays class.
        Array.Sort(arr);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { -6, -3, -1,
                      2, 4, 5 };
        int n = arr.Length;

        Console.WriteLine("Before sort ");
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");

        sortSquares(arr);
        Console.WriteLine("");
        Console.WriteLine("After Sort ");

        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to sort an square array
    function sortSquares(arr)
    {
        let n = arr.length;

        // First convert each array elements
        // into its square
        for (let i = 0; i < n; i++)
            arr[i] = arr[i] * arr[i];

        // Sort an array using "inbuild sort function"
        // in Arrays class.
        arr.sort();
    }

// Driver Code
    let arr = [ -6, -3, -1, 2, 4, 5 ];
    let n = arr.length;

    document.write("Before sort " + "<br/>");
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");

    sortSquares(arr);
    document.write("" + "<br/>");
    document.write("After Sort " + "<br/>");
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
Before sort 
-6 -3 -1 2 4 5 
After Sort 
1 4 9 16 25 36
```

**时间复杂度:** O(n log n)

**高效的解决方案**是基于给定数组已经排序的事实。我们做以下两步。

1.  将数组分成两部分“负和正”。
2.  使用[合并功能](https://www.geeksforgeeks.org/merge-sort/)将两个排序数组合并为一个排序数组。

以下是上述想法的实现。

## C++

```
// C++ program to Sort square of the numbers of the array
#include <bits/stdc++.h>
using namespace std;

// function to sort array after doing squares of elements
void sortSquares(int arr[], int n)
{
    // first divide array into negative and positive part
    int K = 0;
    for (K = 0; K < n; K++)
        if (arr[K] >= 0)
            break;

    // Now do the same process that we learnt
    // in merge sort to merge two sorted array
    // here both two half are sorted and we traverse
    // first half in reverse manner because
    // first half contains negative elements
    int i = K - 1; // Initial index of first half
    int j = K; // Initial index of second half
    int ind = 0; // Initial index of temp array

    // store sorted array
    int temp[n];
    while (i >= 0 && j < n) {
        if (arr[i] * arr[i] < arr[j] * arr[j]) {
            temp[ind] = arr[i] * arr[i];
            i--;
        }
        else {
            temp[ind] = arr[j] * arr[j];
            j++;
        }
        ind++;
    }

    /* Copy the remaining elements of first half */
    while (i >= 0) {
        temp[ind] = arr[i] * arr[i];
        i--;
        ind++;
    }

    /* Copy the remaining elements of second half */
    while (j < n) {
        temp[ind] = arr[j] * arr[j];
        j++;
        ind++;
    }

    // copy 'temp' array into original array
    for (int i = 0; i < n; i++)
        arr[i] = temp[i];
}

// Driver program to test above function
int main()
{
    int arr[] = { -6, -3, -1, 2, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Before sort " << endl;
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    sortSquares(arr, n);

    cout << "\nAfter Sort " << endl;
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Sort square of the numbers
// of the array
import java.util.*;
import java.io.*;

class GFG {
    // Function to sort an square array
    public static void sortSquares(int arr[])
    {
        int n = arr.length;
        // first divide the array into negative and positive part
        int k;
        for (k = 0; k < n; k++) {
            if (arr[k] >= 0)
                break;
        }

        // Now do the same process that we learnt
        // in merge sort to merge two sorted arrays
        // here both two halves are sorted and we traverse
        // first half in reverse manner because
        // first half contains negative elements
        int i = k - 1; // Initial index of first half
        int j = k; // Initial index of second half
        int ind = 0; // Initial index of temp array

        int[] temp = new int[n];
        while (i >= 0 && j < n) {
            if (arr[i] * arr[i] < arr[j] * arr[j]) {
                temp[ind] = arr[i] * arr[i];
                i--;
            }
            else {

                temp[ind] = arr[j] * arr[j];
                j++;
            }
            ind++;
        }

        while (i >= 0) {
            temp[ind++] = arr[i] * arr[i];
            i--;
        }
        while (j < n) {
            temp[ind++] = arr[j] * arr[j];
            j++;
        }

        // copy 'temp' array into original array
        for (int x = 0; x < n; x++)
            arr[x] = temp[x];
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int arr[] = { -6, -3, -1, 2, 4, 5 };
        int n = arr.length;

        System.out.println("Before sort ");
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");

        sortSquares(arr);
        System.out.println("");
        System.out.println("After Sort ");
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to Sort square of the numbers of the array

# function to sort array after doing squares of elements
def sortSquares(arr, n):

    # first divide array into  negative and positive part
    K = 0
    for K in range(n):
        if (arr[K] >= 0 ):
            break

    # Now do the same process that we learnt
    # in merge sort to merge to two sorted array
    # here both two halves are sorted and we traverse
    # first half in reverse manner because
    # first half contains negative elements
    i = K - 1 # Initial index of first half
    j = K # Initial index of second half
    ind = 0 # Initial index of temp array

    # store sorted array
    temp = [0]*n
    while (i >= 0 and j < n):

        if (arr[i] * arr[i] < arr[j] * arr[j]):
            temp[ind] = arr[i] * arr[i]
            i -= 1

        else:

            temp[ind] = arr[j] * arr[j]
            j += 1

        ind += 1

    ''' Copy the remaining elements of first half '''
    while (i >= 0):

        temp[ind] = arr[i] * arr[i]
        i -= 1
        ind += 1

    ''' Copy the remaining elements of second half '''
    while (j < n):
        temp[ind] = arr[j] * arr[j]
        j += 1
        ind += 1

    # copy 'temp' array into original array
    for i in range(n):
        arr[i] = temp[i]

# Driver code
arr = [-6, -3, -1, 2, 4, 5 ]
n = len(arr)

print("Before sort ")
for i in range(n):
    print(arr[i], end =" " )

sortSquares(arr, n)
print("\nAfter Sort ")
for i in range(n):
    print(arr[i], end =" " )

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to Sort square of the numbers
// of the array
using System;

class GFG {

    // Function to sort an square array
    public static void sortSquares(int[] arr)
    {
        int n = arr.Length;

        // first divide array into negative and positive part
        int k;
        for (k = 0; k < n; k++) {
            if (arr[k] >= 0)
                break;
        }

        // Now do the same process that we learnt
        // in merge sort to merge to two sorted array
        // here both two halves are sorted and we traverse
        // first half in reverse manner because
        // first half contains negative elements
        int i = k - 1; // Initial index of first half
        int j = k; // Initial index of second half
        int ind = 0; // Initial index of temp array

        int[] temp = new int[n];
        while (i >= 0 && j < n) {
            if (arr[i] * arr[i] < arr[j] * arr[j]) {
                temp[ind] = arr[i] * arr[i];
                i--;
            }
            else {
                temp[ind] = arr[j] * arr[j];
                j++;
            }
            ind++;
        }

        while (i >= 0) {
            temp[ind++] = arr[i] * arr[i];
            i--;
        }
        while (j < n) {
            temp[ind++] = arr[j] * arr[j];
            j++;
        }

        // copy 'temp' array into original array
        for (int x = 0; x < n; x++)
            arr[x] = temp[x];
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { -6, -3, -1, 2, 4, 5 };
        int n = arr.Length;

        Console.WriteLine("Before sort ");
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");

        sortSquares(arr);
        Console.WriteLine("");
        Console.WriteLine("After Sort ");
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to Sort
// square of the numbers
// of the array

    // Function to sort an square array
    function sortSquares(arr)
    {
        let n = arr.length;
        // first dived array into part
        // negative and positive
        let k;
        for (k = 0; k < n; k++) {
            if (arr[k] >= 0)
                break;
        }

        // Now do the same process that we learn
        // in merge sort to merge to two sorted array
        // here both two half are sorted and we traverse
        // first half in reverse meaner because
        // first half contain negative element

        let i = k - 1; // Initial index of first half
        let j = k; // Initial index of second half
        let ind = 0; // Initial index of temp array

        let temp = new Array(n);
        while (i >= 0 && j < n) {
            if (arr[i] * arr[i] < arr[j] * arr[j]) {
                temp[ind] = arr[i] * arr[i];
                i--;
            }
            else {

                temp[ind] = arr[j] * arr[j];
                j++;
            }
            ind++;
        }

        while (i >= 0) {
            temp[ind++] = arr[i] * arr[i];
            i--;
        }
        while (j < n) {
            temp[ind++] = arr[j] * arr[j];
            j++;
        }

        // copy 'temp' array into original array
        for (let x = 0; x < n; x++)
            arr[x] = temp[x];
    }

    // Driver program to test above function
    let arr=[ -6, -3, -1, 2, 4, 5 ];
    let n = arr.length;
    document.write("Before sort <br>");
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");

    sortSquares(arr);
    document.write("<br>");
    document.write("After Sort <br>");
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");

    // This code is contributed by rag2127

</script>
```

**输出**

```
Before sort 
-6 -3 -1 2 4 5 
After Sort 
1 4 9 16 25 36
```

**时间复杂度:**O(n)
T3】空间复杂度: O(n)

**方法 3–**
另一个有效的解决方案是基于双指针方法，因为数组已经排序了，我们可以比较第一个和最后一个元素来检查哪个更大，然后继续处理结果。

**算法–**

*   初始化左=0 和右=n-1
*   如果 abs(左)> = abs(右)，则在结果数组的末尾存储 square(arr[左])
    ，并递增左指针
*   否则将 square(arr[right])存储在结果数组中，并递减右指针
*   结果数组的递减索引

## C++

```
// CPP code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort an square array
void sortSquares(vector<int>& arr, int n)
{
    int left = 0, right = n - 1;
    int result[n];

    // Iterate from n - 1 to 0
    for (int index = n - 1; index >= 0; index--) {

        // Check if abs(arr[left]) is greater
        // than arr[right]
        if (abs(arr[left]) > arr[right]) {
            result[index] = arr[left] * arr[left];
            left++;
        }
        else {
            result[index] = arr[right] * arr[right];
            right--;
        }
    }
    for (int i = 0; i < n; i++)
        arr[i] = result[i];
}

// Driver Code
int main()
{
    vector<int> arr;
    arr.push_back(-6);
    arr.push_back(-3);
    arr.push_back(-1);
    arr.push_back(2);
    arr.push_back(4);
    arr.push_back(5);

    int n = 6;

    cout << "Before sort " << endl;
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    sortSquares(arr, n);
    cout << endl;
    cout << "After Sort " << endl;
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}

// this code is contributed by Manu Pathria
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Sort square of
// the numbers of the array
import java.util.*;
import java.io.*;

class GFG{

// Function to sort an square array
public static void sortSquares(int arr[])
{
    int n = arr.length, left = 0,
        right = n - 1;

    int result[] = new int[n];

    for(int index = n - 1; index >= 0; index--)
    {
        if (Math.abs(arr[left]) > arr[right])
        {
            result[index] = arr[left] * arr[left];
            left++;
        }
        else
        {
            result[index] = arr[right] * arr[right];
            right--;
        }
    }
    for(int i = 0; i < n; i++)
        arr[i] = result[i];
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { -6, -3, -1, 2, 4, 5 };
    int n = arr.length;

    System.out.println("Before sort ");
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");

    sortSquares(arr);
    System.out.println("");
    System.out.println("After Sort ");
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
}

// This code is contributed by jinalparmar2382
```

## 蟒蛇 3

```
# Python3 program to Sort square of the numbers of the array

# function to sort array after doing squares of elements
def sortSquares(arr, n):
    left, right = 0, n - 1
    index = n - 1
    result = [0 for x in arr]

    while index >= 0:

        if abs(arr[left]) >= abs(arr[right]):
            result[index] = arr[left] * arr[left]
            left += 1
        else:
            result[index] = arr[right] * arr[right]
            right -= 1
        index -= 1

    for i in range(n):
        arr[i] = result[i]

# Driver code
arr = [-6, -3, -1, 2, 4, 5 ]
n = len(arr)

print("Before sort ")
for i in range(n):
    print(arr[i], end =" " )

sortSquares(arr, n)
print("\nAfter Sort ")
for i in range(n):
    print(arr[i], end =" " )
```

## C#

```
// C# program to Sort square of
// the numbers of the array
using System;
class GFG{

// Function to sort an square array
public static void sortSquares(int [] arr)
{
  int n = arr.Length, left = 0,
  right = n - 1;
  int []result = new int[n];

  for(int index = n - 1;
          index >= 0; index--)
  {
    if (Math.Abs(arr[left]) >
        arr[right])
    {
      result[index] = arr[left] *
                      arr[left];
      left++;
    }
    else
    {
      result[index] = arr[right] *
                      arr[right];
      right--;
    }
  }
  for(int i = 0; i < n; i++)
    arr[i] = result[i];
}

// Driver code
public static void Main(string[] args)
{
  int []arr = {-6, -3, -1, 2, 4, 5};
  int n = arr.Length;
  Console.WriteLine("Before sort ");

  for(int i = 0; i < n; i++)
    Console.Write(arr[i] + " ");

  sortSquares(arr);
  Console.WriteLine("");
  Console.WriteLine("After Sort ");

  for(int i = 0; i < n; i++)
    Console.Write(arr[i] + " ");
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
    // Javascript program to Sort square of
    // the numbers of the array

    // Function to sort an square array
    function sortSquares(arr)
    {
      let n = arr.length, left = 0,
      right = n - 1;
      let result = new Array(n);
      result.fill(0);

      for(let index = n - 1; index >= 0; index--)
      {
        if (Math.abs(arr[left]) >
            arr[right])
        {
          result[index] = arr[left] *
                          arr[left];
          left++;
        }
        else
        {
          result[index] = arr[right] *
                          arr[right];
          right--;
        }
      }
      for(let i = 0; i < n; i++)
        arr[i] = result[i];
    }

    let arr = [-6, -3, -1, 2, 4, 5];
    let n = arr.length;
    document.write("Before sort " + "</br>");

    for(let i = 0; i < n; i++)
      document.write(arr[i] + " ");

    sortSquares(arr);
    document.write("</br>");
    document.write("After Sort " + "</br>");

    for(let i = 0; i < n; i++)
      document.write(arr[i] + " ");

 // This code is contributed by rameshtravel07.
</script>
```

**输出**

```
Before sort 
-6 -3 -1 2 4 5 
After Sort 
1 4 9 16 25 36
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。