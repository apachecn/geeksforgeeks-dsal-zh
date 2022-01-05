# 用大于最大值的重复元素替换

> 原文:[https://www . geeksforgeeks . org/用最大值替换重复元素/](https://www.geeksforgeeks.org/replace-repeating-elements-with-greater-that-greatest-values/)

给定一个整数数组，如果一个整数是重复的，那么用一个大于该整数的数字替换它，这个数字还没有被插入到数组中。
**例:**

```
Input : arr = {1, 3, 4, 5, 3}
Output : 1 3 4 5 6
Here 3 is repeating so it is replaced with 6

Input : arr = {1, 3, 4, 4, 5, 3}
Output : 1 3 4 6 5 7
```

我们需要用一个不出现在数组中并且比数组中最大的数字大一的数字来替换重复的数字。
**来源** : [Paytm 面试体验(后端开发者)](https://www.geeksforgeeks.org/paytm-interview-experience-backend-developer/)。
计算数组中的最大元素，用 maxx+1 替换重复的元素，并根据访问更新 maxx 元素。在实现中，使用了哈希的基本概念。

## C++

```
// CPP program to replace repeating elements
// with greater than the greatest.
#include <bits/stdc++.h>
using namespace std;

void replaceElements(int arr[], int n)
{
    // Maximum element in an array
    int maxx = *max_element(arr, arr+n);

    unordered_set<int> s;

    for (int i = 0; i < n; i++) {

        // check whether the element is
        // repeated or not
        if (s.find(arr[i]) == s.end())
            s.insert(arr[i]);

        else {

            // update the repeated element with the
            // maxx element
            arr[i] = maxx + 1;

            maxx++; // update the max

            // mark the maximum element as visited
            s.insert(maxx);
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 4, 5, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);
    replaceElements(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to replace repeating elements
// with greater than the greatest.
import java.util.*;
class Solution
{
    //returns the maximum element
    static int max_element(int arr[])
    {
        int max=arr[0];
        for(int i=1;i<arr.length;i++)
        {
            if(max<arr[i])
            max=arr[i];
        }
        return max;
    }

static void replaceElements(int arr[], int n)
{
    // Maximum element in an array
    int maxx = max_element(arr);

    Vector<Integer> s=new Vector<Integer>();

    for (int i = 0; i < n; i++) {

        // check whether the element is
        // repeated or not
        if (!s.contains(arr[i]))
            s.add(arr[i]);

        else {

            // update the repeated element with the
            // maxx element
            arr[i] = maxx + 1;

            maxx++; // update the max

            // mark the maximum element as visited
            s.add(maxx);
        }
    }
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 3, 4, 5, 3 };
    int n = arr.length;
    replaceElements(arr, n);
    for (int i = 0; i < n; i++)
        System.out.print( arr[i] + " ");

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to replace repeating
# elements with greater than the greatest.

def replaceElements( arr, n):

    # Maximum element in an array
    maxx = max(arr)

    s = []

    for i in range (n) :

        # check whether the element is
        # repeated or not
        if arr[i] not in s:
            s.append(arr[i])

        else:

            # update the repeated element
            # with the maxx element
            arr[i] = maxx + 1

            maxx += 1 # update the max

            # mark the maximum element
            # as visited
            s.append(maxx)

# Driver code
if __name__ =="__main__":

    arr = [ 1, 3, 4, 5, 3 ]
    n = len(arr)
    replaceElements(arr, n)
    for i in range( n):
        print (arr[i], end = " ")

# This code is contributed by ita_c
```

## C#

```
// C# program to replace repeating elements
// with greater than the greatest.
using System;
using System.Collections.Generic;

class GFG
{
    //returns the maximum element
    static int max_element(int []arr)
    {
        int max = arr[0];
        for(int i = 1; i < arr.Length; i++)
        {
            if(max < arr[i])
            max = arr[i];
        }
        return max;
    }

static void replaceElements(int []arr, int n)
{
    // Maximum element in an array
    int maxx = max_element(arr);

    List<int> s = new List<int>();

    for (int i = 0; i < n; i++)
    {

        // check whether the element is
        // repeated or not
        if (!s.Contains(arr[i]))
            s.Add(arr[i]);

        else
        {

            // update the repeated element with the
            // maxx element
            arr[i] = maxx + 1;

            maxx++; // update the max

            // mark the maximum element as visited
            s.Add(maxx);
        }
    }
}

// Driver code
public static void Main()
{
    int []arr = { 1, 3, 4, 5, 3 };
    int n = arr.Length;
    replaceElements(arr, n);
    for (int i = 0; i < n; i++)
        Console.Write( arr[i] + " ");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript  program to replace repeating elements
// with greater than the greatest.

    //returns the maximum element
    function max_element(arr)
    {
        let max=arr[0];
        for(let i=1;i<arr.length;i++)
        {
            if(max<arr[i])
                max=arr[i];
        }
        return max;
    }

    function replaceElements(arr,n)
    {
        // Maximum element in an array
    let maxx = max_element(arr);

    let s=[];

    for (let i = 0; i < n; i++) {

        // check whether the element is
        // repeated or not
        if (!s.includes(arr[i]))
            s.push(arr[i]);

        else {

            // update the repeated element with the
            // maxx element
            arr[i] = maxx + 1;

            maxx++; // update the max

            // mark the maximum element as visited
            s.push(maxx);
        }
    }
    }

    // Driver code
    let arr=[1, 3, 4, 5, 3];
    let n = arr.length;
    replaceElements(arr, n);
    for (let i = 0; i < n; i++)
        document.write( arr[i] + " ");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
1 3 4 5 6
```