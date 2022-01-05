# 线性搜索给定数组中元素的递归程序

> 原文:[https://www . geesforgeks . org/recursive-c-program-linear-search-element-给定-array/](https://www.geeksforgeeks.org/recursive-c-program-linearly-search-element-given-array/)

给定一个未排序的数组和一个元素 x，在给定数组中搜索 x。为此编写递归 C 代码。如果元素不存在，返回-1。

**方法:**想法是将 x 与 arr[]中的最后一个元素进行比较。如果在最后一个位置找到一个元素，返回它。否则对剩余数组和元素 x 重复 elntsrch()

## C++

```
/*
 * Approach : The idea is to compare x with the last element in arr[].
 * If an element is found at the last position, return it.
 * Else recur elmntSrch() for remaining array and element x.
 */

#include<iostream>
using namespace std;

bool checkNum(int arr[], int size, int x) {

    if(size==0)
        return false;
    else{
    if(arr[size]==x)
        return true;
    else{
        checkNum(arr,size-1,x);
    }
    }

}
int main(){
    int n;
    cin >> n;

    int a[n];

    for(int i = 0; i < n; i++) {
        cin >> a[i];
    }

    int x;

    cin >> x;

    if(checkNum(a, n, x)) {
        cout << "true" << endl;
    }
    else {
        cout << "false" << endl;
    }
}
```

## C

```
/*
 * Approach : The idea is to compare x with the last element in arr[].
 * If an element is found at the last position, return it.
 * Else recur elmntSrch() for remaining array and element x.
 */

#include <stdio.h>

// Recursive function to search x in arr[]
int elmntSrch(int arr[], int size, int x) {
    int rec;

    size--;

    if (size >= 0) {
        if (arr[size] == x)
            return size;
        else
            rec = elmntSrch(arr, size, x);
    }
    else
        return -1;

    return rec;
}

int main(void) {
    int arr[] = {12, 34, 54, 2, 3};
    int size = sizeof(arr) / sizeof(arr[0]);
    int x = 3;
    int indx;

    indx = elmntSrch(arr, size, x);

    if (indx != -1)
        printf("Element %d is present at index %d", x, indx);
    else
        printf("Element %d is not present", x);

    return 0;
}

// This code is contributed by Manish Kumar (mkumar2789)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to search x in array
class Test
{
     static int arr[] = {12, 34, 54, 2, 3};

     /* Recursive Method to search x in arr[l..r] */
     static int recSearch(int arr[], int l, int r, int x)
     {
          if (r < l)
             return -1;
          if (arr[l] == x)
             return l;
          if (arr[r] == x)
             return r;
          return recSearch(arr, l+1, r-1, x);
     }

     // Driver method
     public static void main(String[] args)
     {
        int x = 3;

        //Method call to find x
        int index = recSearch(arr, 0, arr.length-1, x);
        if (index != -1)
           System.out.println("Element " + x + " is present at index " +
                                                    index);
        else
            System.out.println("Element " + x + " is not present");
        }
 }
```

## 计算机编程语言

```
# Recursive function to search x in arr[l..r]
def recSearch( arr, l, r, x):
    if r < l:
        return -1
    if arr[l] == x:
        return l
    if arr[r] == x:
        return r
    return recSearch(arr, l+1, r-1, x)

# Driver Code
arr = [12, 34, 54, 2, 3]
n = len(arr)
x = 3
index = recSearch(arr, 0, n-1, x)
if index != -1:
    print "Element", x,"is present at index %d" %(index)
else:
    print "Element %d is not present" %(x)

# Contributed By Harshit Agrawal
```

## C#

```
// Recursive C# program to
// search x in array
using System;

static class Test
{
    static int []arr = {12, 34, 54, 2, 3};

    /* Recursive Method to search x in arr[l..r] */
    static int recSearch(int []arr, int l, int r, int x)
    {
        if (r < l)
            return -1;
        if (arr[l] == x)
            return l;
        if (arr[r] == x)
            return r;
        return recSearch(arr, l+1, r-1, x);
    }

    // Driver method
    public static void Main(String[] args)
    {
        int x = 3;

        // Method call to find x
        int index = recSearch(arr, 0, arr.Length-1, x);

        if (index != -1)
        Console.Write("Element " + x +
                      " is present at index " + index);
        else
            Console.Write("Element " + x +
                          " is not present");
        }
}

// This code is contributed by Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to
// search x in array

// Recursive function to
// search x in arr[l..r]
function recSearch($arr, int $l,
                   int $r, int $x)
{
    if ($r < $l)
        return -1;
    if ($arr[$l] == $x)
        return $l;
    if ($arr[$r] == $x)
        return $r;
     return recSearch($arr, $l+1, $r-1, $x);
}

    // Driver Code
    $arr = array(12, 34, 54, 2, 3); $i;
    $n = count($arr);
    $x = 3;
    $index = recSearch($arr, 0, $n - 1, $x);
    if ($index != -1)
    echo "Element"," ", $x," ",
         "is present at index ", $index;
    else
        echo "Element is not present", $x;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Recursive Javascript program to 
// search x in array

// Recursive function to 
// search x in arr[l..r] 
function recSearch(arr, l, r, x)
{
    if (r < l)
        return -1;
    if (arr[l] == x)
        return l;
    if (arr[r] == x)
        return r;
     return recSearch(arr, l+1, r-1, x);
}

    // Driver Code
    let arr = [12, 34, 54, 2, 3];
    let i;
    let n = arr.length;
    let x = 23;
    let index = recSearch(arr, 0, n - 1, x);

    if (index != -1){
      document.write(`Element ${x} is present at index ${index}`);
    }
    else{
        document.write("Element is not present " + x);
    }

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
false

```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息