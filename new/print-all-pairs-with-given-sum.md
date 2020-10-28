# 打印具有给定总和的所有对

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)

给定一个整数数组和一个数字“和”，请打印该数组中所有总和等于“和”的对。

```
Examples :
Input  :  arr[] = {1, 5, 7, -1, 5}, 
          sum = 6
Output : (1, 5) (7, -1) (1, 5)

Input  :  arr[] = {2, 5, 17, -1}, 
          sum = 7
Output :  (2, 5)

```

一种简单的**解决方案**是遍历每个元素，并检查数组中是否存在可以添加到其上的另一个数字以求和。

## C++

```cpp

// C++ implementation of simple method to
// find print pairs with given sum.
#include <bits/stdc++.h>
using namespace std;

// Returns number of pairs in arr[0..n-1]
// with sum equal to 'sum'
int printPairs(int arr[], int n, int sum)
{
    int count = 0; // Initialize result

    // Consider all possible pairs and check
    // their sums
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (arr[i] + arr[j] == sum)
                cout << "(" << arr[i] << ", "
                     << arr[j] << ")" << endl;
}

// Driver function to test the above function
int main()
{
    int arr[] = { 1, 5, 7, -1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 6;
    printPairs(arr, n, sum);
    return 0;
}

```

## Java

```java

// Java implementation of
// simple method to find
// print pairs with given sum.

class GFG {

    // Returns number of pairs
    // in arr[0..n-1] with sum
    // equal to 'sum'
    static void printPairs(int arr[],
                           int n, int sum)
    {
        // int count = 0;

        // Consider all possible pairs
        // and check their sums
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (arr[i] + arr[j] == sum)
                    System.out.println("(" + arr[i] + ", " + arr[j] + ")");
    }

    // Driver Code
    public static void main(String[] arg)
    {
        int arr[] = { 1, 5, 7, -1, 5 };
        int n = arr.length;
        int sum = 6;
        printPairs(arr, n, sum);
    }
}

// This code is contributed
// by Smitha

```

## Python3

```py

# Python 3 implementation 

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
# of simple method to find

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
# print pairs with given sum.

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)

# Returns number of pairs 

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
# in arr[0..n-1] with sum

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
# equal to 'sum'

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
def printPairs(arr, n, sum):

    # count = 0 

    # Consider all possible 
    # pairs and check their sums
    for i in range(0, n ):
        for j in range(i + 1, n ):
            if (arr[i] + arr[j] == sum):
                print("(", arr[i], 
                      ", ", arr[j], 
                      ")", sep = "")

# Driver Code

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
arr = [1, 5, 7, -1, 5]
n = len(arr)
sum = 6
printPairs(arr, n, sum)

# This code is contributed 

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
# by Smitha

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)

```

## C#

```cs

// C# implementation of simple
// method to find print pairs
// with given sum.
using System;

class GFG {
    // Returns number of pairs
    // in arr[0..n-1] with sum
    // equal to 'sum'
    static void printPairs(int[] arr,
                           int n, int sum)
    {
        // int count = 0;

        // Consider all possible pairs
        // and check their sums
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (arr[i] + arr[j] == sum)
                    Console.Write("(" + arr[i] + ", " + arr[j] + ")"
                                  + "\n");
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 5, 7, -1, 5 };
        int n = arr.Length;
        int sum = 6;
        printPairs(arr, n, sum);
    }
}

// This code is contributed
// by Smitha

```

## PHP

```php

<?php
// PHP implementation of simple 
// method to find print pairs 
// with given sum.

// Returns number of pairs in 
// arr[0..n-1] with sum equal
// to 'sum'
function printPairs($arr, $n, $sum)
{
    // Initialize result
    $count = 0; 

    // Consider all possible 
    // pairs and check their sums
    for ($i = 0; $i < $n; $i++)
        for ( $j = $i + 1; $j < $n; $j++)
            if ($arr[$i] + $arr[$j] == $sum)
                echo "(", $arr[$i], ", ",
                           $arr[$j], ")", "\n";
}

// Driver Code
$arr = array (1, 5, 7, -1, 5);
$n = sizeof($arr);
$sum = 6;
printPairs($arr, $n, $sum);

// This code is contributed by m_kit
?>

```

**Output :** 

```
(1, 5)
(1, 5)
(7, -1)

```

**方法 2（使用哈希）**。

我们创建一个空的哈希表。 现在，我们遍历数组并检查哈希表中的对。 如果找到匹配的元素，我们将打印出等于该匹配元素出现次数的对数。

请注意，此解决方案最复杂的时间复杂度是 **O（c + n）**，其中 c 是具有给定总和的对的计数。

## C++

```cpp

// C++ implementation of simple method to
// find count of pairs with given sum.
#include <bits/stdc++.h>
using namespace std;

// Returns number of pairs in arr[0..n-1]
// with sum equal to 'sum'
void printPairs(int arr[], int n, int sum)
{
    // Store counts of all elements in map m
    unordered_map<int, int> m;

    // Traverse through all elements
    for (int i = 0; i < n; i++) {

        // Search if a pair can be formed with
        // arr[i].
        int rem = sum - arr[i];
        if (m.find(rem) != m.end()) {
            int count = m[rem];
            for (int j = 0; j < count; j++)
                cout << "(" << rem << ", "
                     << arr[i] << ")" << endl;
        }
        m[arr[i]]++;
    }
}

// Driver function to test the above function
int main()
{
    int arr[] = { 1, 5, 7, -1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 6;
    printPairs(arr, n, sum);
    return 0;
}

```

## Java

```java

// Java implementation of simple method to
// find count of pairs with given sum.
import java.util.*;

class GFG{

// Returns number of pairs in arr[0..n-1]
// with sum equal to 'sum'
static void printPairs(int arr[], int n,
                       int sum)
{

    // Store counts of all elements in map m
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Traverse through all elements
    for(int i = 0; i < n; i++) 
    {

        // Search if a pair can be formed with
        // arr[i].
        int rem = sum - arr[i];
        if (mp.containsKey(rem)) 
        {
            int count = mp.get(rem);

            for(int j = 0; j < count; j++)
                System.out.print("(" + rem + 
                                ", " + arr[i] +
                                 ")" + "\n");
        }
        if (mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 7, -1, 5 };
    int n = arr.length;
    int sum = 6;

    printPairs(arr, n, sum);
}
}

// This code is contributed by Princi Singh

```

## C#

```cs

// C# implementation of simple method to
// find count of pairs with given sum.
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Returns number of pairs in arr[0..n-1]
// with sum equal to 'sum'
static void printPairs(int []arr, int n, int sum)
{

    // Store counts of all elements in map m
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // Traverse through all elements
    for(int i = 0; i < n; i++)
    {

        // Search if a pair can be formed with
        // arr[i].
        int rem = sum - arr[i];

        if (m.ContainsKey(rem)) 
        {
            int count = m[rem];

            for(int j = 0; j < count; j++)
            {
                Console.Write("(" + rem + ", " + 
                           arr[i] + ")" + "\n");
            }
        }

        if (m.ContainsKey(arr[i]))
        {
            m[arr[i]]++;
        }
        else
        {
            m[arr[i]] = 1;
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 1, 5, 7, -1, 5 };
    int n = arr.Length;
    int sum = 6;

    printPairs(arr, n, sum);
}
}

// This code is contributed by rutvik_56

```

**Output :** 

```
(1, 5)
(7, -1)
(1, 5)

```

**方法 3** 。

另一种打印具有给定总和的对的方法如下：

## C++

```cpp

// C++ code to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

void pairedElements(int arr[], 
                    int sum, int n)
{
  int low = 0;
  int high = n - 1;

  while (low < high) 
  {
    if (arr[low] + arr[high] == sum) 
    {
      cout << "The pair is : (" << 
               arr[low] << ", " << 
               arr[high] << ")" << endl;
    }
    if (arr[low] + arr[high] > sum) 
    {
      high--;
    }
    else
    {
      low++;
    }
  }
}

// Driver code
int  main()
{
  int arr[] = {2, 3, 4, -2, 
               6, 8, 9, 11};
  int n = sizeof(arr) / sizeof(arr[0]);
  sort(arr, arr + n);
  pairedElements(arr, 6, n);
}

// This code is contributed by Rajput-Ji

```

## Java

```java

import java.util.Arrays;

/**
 * Created by sampat.
 */
public class SumOfPairs {

    public void pairedElements(int arr[], int sum)
    {
        int low = 0;
        int high = arr.length - 1;

        while (low < high) {
            if (arr[low] + arr[high] == sum) {
                System.out.println("The pair is : ("
                                   + arr[low] + ", " + arr[high] + ")");
            }
            if (arr[low] + arr[high] > sum) {
                high--;
            }
            else {
                low++;
            }
        }
    }

    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, -2, 6, 8, 9, 11 };
        Arrays.sort(arr);

        SumOfPairs sp = new SumOfPairs();
        sp.pairedElements(arr, 6);
    }
}

```

## Python3

```py

# Python3 program for the 

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
# above approach

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
def pairedElements(arr, sum):

    low = 0;
    high = len(arr) - 1;

    while (low < high):
        if (arr[low] +
            arr[high] == sum):
            print("The pair is : (", arr[low], 
                  ", ", arr[high], ")");
        if (arr[low] + arr[high] > sum):
            high -= 1;
        else:
            low += 1;

# Driver code

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)
if __name__ == '__main__':

    arr = [2, 3, 4, -2, 
           6, 8, 9, 11];
    arr.sort();
    pairedElements(arr, 6);

# This code contributed by shikhasingrajput

> 原文：[https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/](https://www.geeksforgeeks.org/print-all-pairs-with-given-sum/)

```

## C#

```cs

// C# program to find triplets in a given
// array whose sum is equal to given sum.
using System;

public class SumOfPairs 
{

    public void pairedElements(int []arr, int sum)
    {
        int low = 0;
        int high = arr.Length - 1;

        while (low < high) 
        {
            if (arr[low] + arr[high] == sum)
            {
                Console.WriteLine("The pair is : ("
                                + arr[low] + ", " + arr[high] + ")");
            }
            if (arr[low] + arr[high] > sum)
            {
                high--;
            }
            else
            {
                low++;
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 3, 4, -2, 6, 8, 9, 11 };
        Array.Sort(arr);

        SumOfPairs sp = new SumOfPairs();
        sp.pairedElements(arr, 6);
    }
}

// This code is contributed by Princi Singh

```

**Output :** 

```
The pair is : (-2, 8)
The pair is : (2, 4)

```



* * *

* * *



