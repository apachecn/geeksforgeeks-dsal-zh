# 稀疏搜索

> 原文:[https://www.geeksforgeeks.org/sparse-search/](https://www.geeksforgeeks.org/sparse-search/)

给定一个散布着空字符串的字符串排序数组，编写一个方法来查找给定字符串的位置。
示例:

```
Input : arr[] = {"for", "geeks", "", "", "", "", "ide", 
                      "practice", "", "", "", "quiz"}
          x = "geeks"
Output : 1

Input : arr[] = {"for", "geeks", "", "", "", "", "ide", 
                      "practice", "", "", "", "quiz"}, 
          x = "ds"
Output : -1
```

如果没有空弦，我们就可以简单地演奏二分搜索法。稍加修改，我们仍然可以使用二分搜索法。如果我们的**中间是空的**我们只需要移动中间到最近的**非空弦**。
以下是上述方法的一个实现。

## C++

```
// C++ program to implement binary search
// in a sparse array.
#include <bits/stdc++.h>
using namespace std;

/* Binary Search in an array with blanks */
int binarySearch(string *arr, int low, int high, string x) {
  if (low > high)
    return -1;

  int mid = (low + high) / 2;

  /*Modified Part*/
  if (arr[mid] == "") {
    int left = mid - 1;
    int right = mid + 1;

    /*Search for both side for a non empty string*/
    while (1) {

      /* No non-empty string on both sides */
      if (left < low && right > high)
        return -1;

      if (left >= low && arr[left] != "") {
        mid = left;
        break;
      }

      else if (right <= high && arr[right] != "") {
        mid = right;
        break;
      }

      left--;
      right++;
    }
  }

  /* Normal Binary Search */
  if (arr[mid] == x)
    return mid;
  else if (arr[mid] > x)
    return binarySearch(arr, low, mid - 1, x);
  else
    return binarySearch(arr, mid + 1, high, x);
}

int sparseSearch(string arr[], string x, int n) {
  return binarySearch(arr, 0, n - 1, x);
}

int main() {
  ios_base::sync_with_stdio(false);

  string arr[] = {"for", "geeks", "", "", "", "", "ide",
                      "practice", "", "", "", "quiz"};
  string x = "geeks";
  int n = sizeof(arr) / sizeof(arr[0]);
  int index = sparseSearch(arr, x, n);
  if (index != -1)
    cout << x << " found at index " << index << "\n";
  else
    cout << x << " not found\n";
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement binary search
// in a sparse array.

class solution
{

// Binary Search in an array with blanks
static int binarySearch(String arr[], int low, int high, String x) {
if (low > high)
    return -1;

int mid = (low + high) / 2;

//Modified Part
if (arr[mid] == "") {
    int left = mid - 1;
    int right = mid + 1;

    /*Search for both side for a non empty string*/
    while (true) {

    /* No non-empty string on both sides */
    if (left < low && right > high)
        return -1;

    if (left >= low && arr[left] != "") {
        mid = left;
        break;
    }

    else if (right <= high && arr[right] != "") {
        mid = right;
        break;
    }

    left--;
    right++;
    }
}

/* Normal Binary Search */
if (arr[mid] == x)
    return mid;
else if (x.compareTo(arr[mid]) < 0)
    return binarySearch(arr, low, mid - 1, x);
else
    return binarySearch(arr, mid + 1, high, x);
}

static int sparseSearch(String arr[], String x, int n) {
return binarySearch(arr, 0, n - 1, x);
}

public static void main(String args[]) {

String arr[] = {"for", "geeks", "", "", "", "", "ide",
                    "practice", "", "", "", "quiz"};
String x = "geeks";
int n = x.length();
int index = sparseSearch(arr, x, n);
if (index != -1)
    System.out.println(x+ " found at index "+index);
else
    System.out.println(x+" not found");

}
}

// This code is implemented by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to implement binary search
#  in a sparse array

def sparseSearch(arr , key , low , high):

    left = 0; right = 0

    while low <= high:

            mid = low + (high - low) // 2

            if arr[mid] == '':
                left = mid - 1
                right = mid + 1

                while True:

                    # Check for out of bounds
                    if left < low and right > high:
                        return -1

                    elif left >= low and arr[left] != '':
                        # Search left
                        mid = left
                        break

                    elif right <= high and arr[right] != '':
                        # Search right
                        mid = right
                        break

                    left -= 1
                    right += 1

            if arr[mid] == key:
                print('Found string {} at index {}'.format
                     (arr[mid] , mid))
                return mid

            # Classical Binary search
            # search left
            elif arr[mid] > key:
                high = mid - 1

            # search right
            elif arr[mid] < key:
                low = mid + 1

    return -1

if __name__ == '__main__':

    arr = ["for", "geeks", "", "", "", "", "ide",
           "practice", "", "", "", "quiz"]                
    key = 'geeks'

    low = 0
    high = len(arr) - 1

    sparseSearch(arr , key , low , high)

# This is  Code contributed by
# Ashwin Viswanathan
# Additional Updates by Meghna Natraj
```

## C#

```
// C# program to implement binary search
// in a sparse array.
using System;
using System.Collections.Generic;

class GFG{

// Binary Search in an array with blanks
static int binarySearch(string []arr, int low,
                        int high, string x)
{
    if (low > high)
        return -1;

    int mid = (low + high) / 2;

    // Modified Part
    if (arr[mid] == "")
    {
        int left = mid - 1;
        int right = mid + 1;

        // Search for both side for
        // a non empty string
        while (true)
        {

            // No non-empty string on both sides
            if (left < low && right > high)
                return -1;

            if (left >= low && arr[left] != "")
            {
                mid = left;
                break;
            }

            else if (right <= high &&
                arr[right] != "")
            {
                mid = right;
                break;
            }

            left--;
            right++;
        }
    }

    // Normal Binary Search
    if (arr[mid] == x)
        return mid;

    else if (x.CompareTo(arr[mid]) < 0)
        return binarySearch(arr, low,
                            mid - 1, x);
    else
        return binarySearch(arr, mid + 1,
                           high, x);
}

static int sparseSearch(string []arr,
                        string x, int n)
{
    return binarySearch(arr, 0, n - 1, x);
}

// Driver Code
public static void Main(string[] args)
{
    string []arr = { "for", "geeks", "", "",
                     "", "", "ide",  "practice",
                     "", "", "", "quiz"};

    string x = "geeks";
    int n = x.Length;

    int index = sparseSearch(arr, x, n);

    if (index != -1)
        Console.Write(x + " found at index " +
                      index);
    else
        Console.Write(x + " not found");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to implement binary search
// in a sparse array.

// Binary Search in an array with blanks
function binarySearch(arr, low, high, x) {
    if (low > high)
        return -1;

    let mid = Math.floor((low + high) / 2);

    // Modified Part
    if (arr[mid] == "")
    {
        let left = mid - 1;
        let right = mid + 1;

        /*Search for both side for a non empty string*/
        while (true) {

            /* No non-empty string on both sides */
            if (left < low && right > high)
                return -1;

            if (left >= low && arr[left] != "") {
                mid = left;
                break;
            }

            else if (right <= high && arr[right] != "") {
                mid = right;
                break;
            }

            left--;
            right++;
        }
    }

    /* Normal Binary Search */
    if (arr[mid] == x)
        return mid;
    else if (arr[mid] > x)
        return binarySearch(arr, low, mid - 1, x);
    else
        return binarySearch(arr, mid + 1, high, x);
}

function sparseSearch(arr, x, n) {
    return binarySearch(arr, 0, n - 1, x);
}

let arr = ["for", "geeks", "", "", "", "", "ide",
    "practice", "", "", "", "quiz"];
let x = "geeks";
let n = x.length;
let index = sparseSearch(arr, x, n);
if (index != -1)
    document.write(x + " found at index " + index);
else
    document.write(x + " not found");

// This code is implemented by
// _saurabh_jaiswal
</script>
```

**Output:** 

```
geeks found at index 1
```

https://youtu.be/HS03UxTx

-ua〔t0〕