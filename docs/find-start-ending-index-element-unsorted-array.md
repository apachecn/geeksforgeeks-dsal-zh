# 查找未排序数组中元素的开始和结束索引

> 原文:[https://www . geesforgeks . org/find-start-end-index-element-unsorted-array/](https://www.geeksforgeeks.org/find-start-ending-index-element-unsorted-array/)

给定一个整数数组，任务是找到给定键的开始和结束位置。

**示例:**

```
Input : arr[] = {1, 2, 3, 4, 5, 5}
      Key = 5
Output :  Start index: 4
      Last index: 5
Explanation: Starting index where 5
is present is 4 and ending address is 5.

Input :arr[] = {1, 3, 7, 8, 6}, 
      Key = 2
Output : Key not present in array

Input :arr[] = {1, 8, 7, 8, 6}, 
      Key = 7
Output : Only one occurrence of 
key is present at index 2
```

我们从头开始遍历数组，找到第一个匹配项。如果元素存在，那么我们也从头到尾遍历以查找最后一次出现。

## C++

```
// CPP program to find starting and ending
// indexes of repeated numbers in an array
#include <iostream>
using namespace std;

// Function to find starting and end index
void findIndex(int a[], int n, int key)
{
    int start = -1;

    // Traverse from beginning to find
    // first occurrence
    for (int i = 0; i < n; i++) {
        if (a[i] == key) {
            start = i;
            break;
        }
    }

    if (start == -1) {
        cout << "Key not present in array";
        return;
    }

    // Traverse from end to find last
    // occurrence.
    int end = start;
    for (int i = n - 1; i >= start; i--) {
        if (a[i] == key) {
            end = i;
            break;
        }
    }
    if (start == end)
        cout << "Only one key is present at index : "
             << start;
    else {
        cout << "Start index: " << start;
        cout << "nLast index: " << end;
    }
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 7, 8, 8, 9, 8, 0, 0, 0, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    // Key to find
    int key = 8;

    // Calling function
    findIndex(a, n, key);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find starting and ending
// indexes of repeated numbers in an array

class Test {
    // Function to find starting and end index
    static void findIndex(int a[], int n, int key)
    {
        int start = -1;

        // Traverse from beginning to find
        // first occurrence
        for (int i = 0; i < n; i++) {
            if (a[i] == key) {
                start = i;
                break;
            }
        }

        if (start == -1) {
            System.out.println("Key not present in array");
            return;
        }

        // Traverse from end to find last
        // occurrence.
        int end = start;
        for (int i = n - 1; i >= start; i--) {
            if (a[i] == key) {
                end = i;
                break;
            }
        }
        if (start == end)
            System.out.println("Only one key is present at index : " + start);
        else {
            System.out.println("Start index: " + start);
            System.out.println("Last index: " + end);
        }
    }

    // Driver method
    public static void main(String args[])
    {
        int a[] = { 1, 2, 7, 8, 8, 9, 8, 0, 0, 0, 8 };

        // Key to find
        int key = 8;

        // Calling method
        findIndex(a, a.length, key);
    }
}
```

## 蟒蛇 3

```
# Python3 code to find starting and ending
# indexes of repeated numbers in an array

# Function to find starting and end index
def findIndex (a, n, key ):
    start = -1

    # Traverse from beginning to find
    # first occurrence
    for i in range(n):
        if a[i] == key:
            start = i
            break

    if start == -1:
        print("Key not present in array")
        return 0

    # Traverse from end to find last
    # occurrence.
    end = start
    for i in range(n-1, start - 1, -1):
        if a[i] == key:
            end = i
            break
    if start == end:
        print("Only one key is present at index : ", start)
    else:
        print("Start index: ", start)
        print("Last index: ", end)

# Driver Code
a = [1, 2, 7, 8, 8, 9, 8, 0, 0, 0, 8]
n = len(a)

# Key to find
key = 8

# Calling function
findIndex(a, n, key)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find starting and ending
// indexes of repeated numbers in an array
using System;

class GFG {

    // Function to find starting and
    // end index
    static void findIndex(int[] a, int n,
                          int key)
    {
        int start = -1;

        // Traverse from beginning to
        // find first occurrence
        for (int i = 0; i < n; i++) {
            if (a[i] == key) {
                start = i;
                break;
            }
        }

        if (start == -1) {
            Console.WriteLine("Key not "
                              + "present in array");
            return;
        }

        // Traverse from end to find last
        // occurrence.
        int end = start;
        for (int i = n - 1; i >= start; i--) {
            if (a[i] == key) {
                end = i;
                break;
            }
        }
        if (start == end)
            Console.WriteLine("Only one key is"
                              + " present at index : "
                              + start);
        else {
            Console.WriteLine("Start index: "
                              + start);

            Console.WriteLine("Last index: "
                              + end);
        }
    }

    // Driver method
    public static void Main()
    {
        int[] a = { 1, 2, 7, 8, 8, 9,
                    8, 0, 0, 0, 8 };

        // Key to find
        int key = 8;

        // Calling method
        findIndex(a, a.Length, key);
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find starting and ending
// indexes of repeated numbers in an array

// Function to find starting and end index

function findIndex($arr, $find){

    // To store the atrting and
    // the ending index of the key
    $start = -1;
    $end = -1;

    // For every element of the given array
    foreach ($arr as $key => $value) {

        // If current element is equal
        // to the given key
        if($find === $value){

            // If starting index hasn't been set
            if($start==-1)
                $start = $key;
            $end = $key;
        }
    }

    // If key is not present in the array
    if($start==-1){
        return "Key not present in array";
    }
    if($end == $start){
        return "Only one key is present "." at index : ". $start;
    }
    return "Start index: ".$start. "\nLast index: ".$end;
}

// Driver code
$a = array(1, 2, 7, 8, 8, 9, 8, 0, 0, 0, 8);

// Key to find
$key = 8;

// Calling function
echo findIndex($a, $key);
?>
```

## java 描述语言

```
<script>

// Javascript program to find starting and ending
// indexes of repeated numbers in an array

// Function to find starting and end index
function findIndex(a, n, key)
{
    let start = -1;

    // Traverse from beginning to find
    // first occurrence
    for (let i = 0; i < n; i++) {
        if (a[i] == key) {
            start = i;
            break;
        }
    }

    if (start == -1) {
        document.write("Key not present in array");
        return;
    }

    // Traverse from end to find last
    // occurrence.
    let end = start;
    for (let i = n - 1; i >= start; i--) {
        if (a[i] == key) {
            end = i;
            break;
        }
    }
    if (start == end)
        document.write("Only one key is present at index : "
            + start);
    else {
        document.write("Start index: " + start);
        document.write("<br>" + "Last index: " + end);
    }
}

// Driver Code

    let a = [ 1, 2, 7, 8, 8, 9, 8, 0, 0, 0, 8 ];
    let n = a.length;

    // Key to find
    let key = 8;

    // Calling function
    findIndex(a, n, key);

//This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
Start index: 3
Last index: 10
```

**相关文章:**
[查找排序数组中某个元素的第一次和最后一次出现](https://www.geeksforgeeks.org/find-first-last-occurrences-element-sorted-array/)
本文由 [**Sahil Rajput**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。