# 数组中所有元素是否相同？

> 原文:[https://www . geesforgeks . org/数组中的所有元素是相同还是不同/](https://www.geeksforgeeks.org/all-elements-in-an-array-are-same-or-not/)

给定一个数组，检查数组中的所有元素是否相同。

**例:**

```
Input : "Geeks", "for", "Geeks"
Output : Not all Elements are Same

Input : 1, 1, 1, 1, 1
Output : All Elements are Same
```

**方法 1 (Hashing)** 我们创建一个空的 HashSet，把所有的元素都插入其中，然后我们最后看看 HashSet 的大小是否为 1。

## c++

```
//c++ program to check if all array are same or not
#include<bits/stdc++.h>

using namespace std;

bool areSame(int a[],int n)
{
    unordered_map<int,int> m;//hash map to store the frequency od every
                             //element

    for(int i=0;i<n;i++)
       m[a[i]]++;

    if(m.size()==1)
       return true;
    else
       return false;
}
//Driver code
int main()
{
    int arr[]={1,2,3,2};

    int n=sizeof(arr)/sizeof(arr[0]);

    if(areSame(arr,n))
      cout<<"All Elements are Same";
    else
      cout<<"Not all Elements are Same";
}
```

## Java

```
// Java program to check if all array elements are
// same or not.
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

public class SameElements {
public static boolean areSame(Integer arr[])
    {
        // Put all array elements in a HashSet
        Set<Integer> s = new HashSet<>(Arrays.asList(arr));

        // If all elements are same, size of
        // HashSet should be 1\. As HashSet contains only distinct values.
        return (s.size() == 1);
    }

    // Driver code
public static void main(String[] args)
    {
        Integer[] arr = { 1, 2, 3, 2 };
        if (areSame(arr))
            System.out.println("All Elements are Same");
        else
            System.out.println("Not all Elements are Same");
    }
}
```

## python 3

```
# Python 3 program to check if all
# array are same or not
def areSame(a, n):
    m = {i:0 for i in range(len(a))}

    # hash map to store the frequency
    # of every element

    for i in range(n):
        m[a[i]] += 1

    if(len(m) == 1):
        return True
    else:
        return False

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 2]

    n = len(arr)

    if(areSame(arr, n)):
        print("All Elements are Same")
    else:
        print("Not all Elements are Same")

# This code is contributed by
# Shashank_Sharma
```

## c#

```
// C# program to check if all array elements
// are same or not.
using System;
using System.Collections.Generic;

class GFG{

public static bool areSame(int []arr)
{

    // Put all array elements in a HashSet
    HashSet<int> s = new HashSet<int>();
    for(int i = 0; i < arr.Length; i++)
        s.Add(arr[i]);

    // If all elements are same, size of
    // HashSet should be 1\. As HashSet
    // contains only distinct values.
    return (s.Count == 1);
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 1, 2, 3, 2 };

    if (areSame(arr))
        Console.WriteLine("All Elements are Same");
    else
        Console.WriteLine("Not all Elements are Same");
}
}

// This code is contributed by Amit Katiyar
```

## Javascript

```
<script>
// Javascript program to check if all array elements are
// same or not.

    function areSame(arr)
    {
        // Put all array elements in a HashSet
        let s = new Set(arr);

        // If all elements are same, size of
        // HashSet should be 1\. As HashSet contains only distinct values.
        return (s.size == 1);
    }

    // Driver code
    let arr=[1, 2, 3, 2];
    if (areSame(arr))
            document.write("All Elements are Same");
        else
            document.write("Not all Elements are Same");

// This code is contributed by patel2127
</script>
```

**输出**

```
Not all Elements are Same
```