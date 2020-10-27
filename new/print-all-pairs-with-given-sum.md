# 打印具有给定总和的所有对

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

## C ++

```

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

## 爪哇

```

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

```

# Python 3 implementation 
# of simple method to find
# print pairs with given sum.

# Returns number of pairs 
# in arr[0..n-1] with sum
# equal to 'sum'
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
arr = [1, 5, 7, -1, 5]
n = len(arr)
sum = 6
printPairs(arr, n, sum)

# This code is contributed 
# by Smitha

```

## C＃

```

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

## 的 PHP

```

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

## C ++

```

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

## 爪哇

```

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

## C＃

```

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

## C ++

```

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

## 爪哇

```

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

```

# Python3 program for the 
# above approach
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
if __name__ == '__main__':

    arr = [2, 3, 4, -2, 
           6, 8, 9, 11];
    arr.sort();
    pairedElements(arr, 6);

# This code contributed by shikhasingrajput

```

## C＃

```

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

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。