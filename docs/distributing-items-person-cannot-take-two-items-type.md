# 当一个人不能携带两个以上相同类型的物品时分配物品

> 原文：[https://www.geeksforgeeks.org/distributing-items-person-cannot-take-two-items-type/](https://www.geeksforgeeks.org/distributing-items-person-cannot-take-two-items-type/)

假设有`N`种糖果可以有许多不同的类型，并且有`k`个客户，那么一个客户购买的同一类型的糖果不会超过 2 件，任务是确定是否可以分发所有糖果，然后打印`Yes`，否则打印`No`。

给定数组`arr[]`表示糖果数组，`arr[i]`是糖果的类型。

**示例**：

```
Input : arr[] = {1, 1, 2, 3, 1}, 
            k = 2;
Output : Yes
There are three pieces of sweet type 1,
one piece of type 2 and one piece of 
type 3\. Two customers can distribute 
sweets under given constraints.

Input : arr[] = {2, 3, 3, 5, 3, 3}, 
            k = 2;
Output : Yes

Input : arr[] = {2, 3, 3, 5, 3, 3, 3}, 
            k = 2;
Output : No

```

**方法 1**：

1.  遍历数组的每个元素。

2.  数组中每个元素的出现次数。

3.  检查每个元素的结果出现必须小于或等于`2 * k`。

## C++

```cpp

// C++ program for above implementation
#include <bits/stdc++.h>
using namespace std;

// Function to check occurrence of each element
bool checkCount(int arr[], int n, int k)
{
    int count;

    // Start traversing the elements
    for (int i = 0; i < n; i++) {

        // Count occurrences of current element
        count = 0;
        for (int j = 0; j < n; j++) {
            if (arr[j] == arr[i])
                count++;

            // If count of any element is greater
            // than 2*k then return false
            if (count > 2 * k)
                return false;
        }
    }

    return true;
}

// Drivers code
int main()
{
    int arr[] = { 1, 1, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    checkCount(arr, n, k) ? cout << "Yes"
                           : cout << "No";

    return 0;
}

```

## Java

```java

// java program for above implementation
import java.io.*;

public class GFG {

    // Function to check occurrence of
    // each element
    static boolean checkCount(int []arr,
                            int n, int k)
    {
        int count;

        // Start traversing the elements
        for (int i = 0; i < n; i++)
        {

            // Count occurrences of
            // current element
            count = 0;
            for (int j = 0; j < n; j++)
            {
                if (arr[j] == arr[i])
                    count++;

                // If count of any element
                // is greater than 2*k then
                // return false
                if (count > 2 * k)
                    return false;
            }
        }

        return true;
    }

    // Drivers code
    static public void main (String[] args)
    {
        int []arr = { 1, 1, 2, 3, 1 };
        int n = arr.length;
        int k = 2;

        if(checkCount(arr, n, k)) 
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by vt_m.

```

## Python3

```py

# Python 3 program for above implementation 

# Function to check occurrence 
# of each element 
def checkCount(arr, n, k):

    # Start traversing the elements 
    for i in range(n):

        # Count occurrences of 
        # current element 
        count = 0
        for j in range(n):
            if arr[j] == arr[i]:
                count += 1

            # If count of any element is greater 
            # than 2*k then return false 
            if count > 2 * k:
                return False
    return True

# Driver code
arr = [1, 1, 2, 3, 1]
n = len(arr)
k = 2
if checkCount(arr, n, k) == True:
    print("Yes")
else:
    print("No")

# This code is contributed by Shrikant13

```

## C#

```cs

// C# program for above implementation
using System;

public class GFG {

    // Function to check occurrence
    // of each element
    static bool checkCount(int []arr,
                          int n, int k)
    {
        int count;

        // Start traversing the elements
        for (int i = 0; i < n; i++)
        {

            // Count occurrences of
            // current element
            count = 0;
            for (int j = 0; j < n; j++)
            {
                if (arr[j] == arr[i])
                    count++;

                // If count of any element 
                // is greater than 2*k then
                // return false
                if (count > 2 * k)
                    return false;
            }
        }

        return true;
    }

    // Drivers code
    static public void Main ()
    {
        int []arr = { 1, 1, 2, 3, 1 };
        int n = arr.Length;
        int k = 2;

        if(checkCount(arr, n, k)) 
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.

```

## PHP

```php

<?php
// PHP program for above implementation

// Function to check occurrence
// of each element
function checkCount($arr, $n, $k)
{
    $count;

    // Start traversing the elements
    for($i = 0; $i < $n; $i++) 
    {

        // Count occurrences of 
        // current element
        $count = 0;
        for($j = 0; $j < $n; $j++)
        {
            if ($arr[$j] == $arr[$i])
                $count++;

            // If count of any element 
            // is greater than 2*k then
            // return false
            if ($count > 2 * $k)
                return false;
        }
    }

    return true;
}

    // Driver Code
    $arr = array(1, 1, 2, 3, 1);
    $n =count($arr);
    $k = 2;
    if(checkCount($arr, $n, $k))
        echo "Yes";
    else
        echo "No";

// This code is contributed by anuj_67.
?>

```

输出：

```
Yes

```

时间复杂度：`O(N ^ 2)`。

**方法 2**：

1.  维护 32 种不同类型的糖果的哈希。

2.  遍历数组并检查每个`arr[i]`。

```
hash[arr[i]] <= 2*k. 

```

## C++

```cpp

// C++ program for above implementation
#include <bits/stdc++.h>
using namespace std;

// Function to check hash array
// corresponding to the given array
bool checkCount(int arr[], int n, int k)
{
    unordered_map<int, int> hash;

    // Maintain a hash
    for (int i = 0; i < n; i++)
        hash[arr[i]]++;

    // Check for each value in hash
    for (auto x : hash)
        if (x.second > 2 * k)
            return false;

    return true;
}

// Drivers code
int main()
{
    int arr[] = { 1, 1, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    checkCount(arr, n, k) ? cout << "Yes"
                           : cout << "No";
    return 0;
}

```

## Java

```java

// Java program for above implementation
import java.util.HashMap;
import java.util.Map;

class GfG
{

    // Function to check hash array 
    // corresponding to the given array 
    static boolean checkCount(int arr[], int n, int k) 
    { 
        HashMap <Integer, Integer> hash = new HashMap<>(); 

        // Maintain a hash 
        for (int i = 0; i < n; i++)
        {
            if (!hash.containsKey(arr[i]))
                hash.put(arr[i], 0);
            hash.put(arr[i], hash.get(arr[i]) + 1);
        }

        // Check for each value in hash 
        for (Map.Entry x : hash.entrySet())
            if ((int)x.getValue() > 2 * k) 
                return false; 

        return true; 
    } 

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 1, 1, 2, 3, 1 }; 
        int n = arr.length; 
        int k = 2; 
        if (checkCount(arr, n, k)) 
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Rituraj Jain

```

## Python3

```py

# Python3 program for above implementation 
from collections import defaultdict

# Function to check hash array 
# corresponding to the given array 
def checkCount(arr, n, k):

    mp = defaultdict(lambda:0)

    # Insert all array elements in
    # hash table Maintain a hash
    for i in range(n):
        mp[arr[i]] += 1

    # Check for each value in hash
    for key, values in mp.items():
        if values > 2 * k:
            return False
    return True

# Driver code
arr = [ 1, 1, 2, 3, 1 ]
n = len(arr)
k = 2
if checkCount(arr, n, k) == True:
    print("Yes")
else:
    print("No")

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# program for above implementation
using System; 
using System.Collections.Generic;

class GfG
{

    // Function to check hash array 
    // corresponding to the given array 
    static Boolean checkCount(int []arr, int n, int k) 
    { 
        Dictionary<int,int> hash = new Dictionary<int,int>(); 

        // Maintain a hash 
        for (int i = 0; i < n; i++)
        {
            if(hash.ContainsKey(arr[i]))
            {
                var val = hash[arr[i]];
                hash.Remove(arr[i]);
                hash.Add(arr[i], val + 1); 
            }
            else
            {
                hash.Add(arr[i], 0);
            }
        }

        // Check for each value in hash 
        foreach(KeyValuePair<int, int> x in hash)
            if ((int)x.Value > 2 * k) 
                return false; 

        return true; 
    } 

    // Driver code
    public static void Main(String []args)
    {

        int []arr = { 1, 1, 2, 3, 1 }; 
        int n = arr.Length; 
        int k = 2; 
        if (checkCount(arr, n, k)) 
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

/* This code is contributed by PrinciRaj1992 */

```

**输出**：

```
Yes

```

**时间复杂度**：`O(n)`。



* * *

* * *



