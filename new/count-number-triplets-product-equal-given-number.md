# 产品数量等于给定数量的三元组数量

> 原文：[https://www.geeksforgeeks.org/count-number-triplets-product-equal-given-number/](https://www.geeksforgeeks.org/count-number-triplets-product-equal-given-number/)

给定一组不同的整数（仅包含正数）和数字`m`，请找出乘积等于`m`的三元组数。

**示例**：

```
Input : arr[] = { 1, 4, 6, 2, 3, 8}  
            m = 24
Output : 3
{1, 4, 6} {1, 3, 8} {4, 2, 3}

Input : arr[] = { 0, 4, 6, 2, 3, 8}  
            m = 18
Output : 0

```

被询问：[微软](https://www.geeksforgeeks.org/microsoft-interview-experience-set-116-on-campus/)

**朴素的方法**是将每个三元组一一考虑，并计算它们的乘积是否等于`m`。

## C++

```cpp

// C++ program to count triplets with given
// product m
#include <iostream>
using namespace std;

// Function to count such triplets
int countTriplets(int arr[], int n, int m)
{
    int count = 0;

    // Consider all triplets and count if
    // their product is equal to m
    for (int i = 0; i < n - 2; i++)
        for (int j = i + 1; j < n - 1; j++)
            for (int k = j + 1; k < n; k++)
                if (arr[i] * arr[j] * arr[k] == m)
                    count++;

    return count;
}

// Drivers code
int main()
{
    int arr[] = { 1, 4, 6, 2, 3, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 24;

    cout << countTriplets(arr, n, m);

    return 0;
}

```

## Java

```java

// Java program to count triplets with given
// product m

class GFG {
    // Method to count such triplets
    static int countTriplets(int arr[], int n, int m)
    {
        int count = 0;

        // Consider all triplets and count if
        // their product is equal to m
        for (int i = 0; i < n - 2; i++)
            for (int j = i + 1; j < n - 1; j++)
                for (int k = j + 1; k < n; k++)
                    if (arr[i] * arr[j] * arr[k] == m)
                        count++;

        return count;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = { 1, 4, 6, 2, 3, 8 };
        int m = 24;

        System.out.println(countTriplets(arr, arr.length, m));
    }
}

```

## Python3

```py

# Python3 program to count 
# triplets with given product m

# Method to count such triplets
def countTriplets(arr, n, m):

    count = 0

    # Consider all triplets and count if
    # their product is equal to m
    for i in range (n - 2):
        for j in range (i + 1, n - 1):
            for k in range (j + 1, n):
                if (arr[i] * arr[j] * arr[k] == m):
                    count += 1
    return count

# Driver code
if __name__ == "__main__":

    arr = [1, 4, 6, 2, 3, 8]
    m = 24
    print(countTriplets(arr, 
                        len(arr), m))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program to count triplets 
// with given product m
using System;

public class GFG {

    // Method to count such triplets
    static int countTriplets(int[] arr, int n, int m)
    {
        int count = 0;

        // Consider all triplets and count if
        // their product is equal to m
        for (int i = 0; i < n - 2; i++)
            for (int j = i + 1; j < n - 1; j++)
                for (int k = j + 1; k < n; k++)
                    if (arr[i] * arr[j] * arr[k] == m)
                        count++;

        return count;
    }

    // Driver method
    public static void Main()
    {
        int[] arr = { 1, 4, 6, 2, 3, 8 };
        int m = 24;

        Console.WriteLine(countTriplets(arr, arr.Length, m));
    }
}

// This code is contributed by Sam007

```

## PHP

```php

<?php
// PHP program to count triplets
// with given product m

// Function to count such triplets
function countTriplets($arr, $n, $m)
{
    $count = 0;

    // Consider all triplets and count if
    // their product is equal to m
    for ( $i = 0; $i < $n - 2; $i++)
        for ( $j = $i + 1; $j < $n - 1; $j++)
            for ($k = $j + 1; $k < $n; $k++)
                if ($arr[$i] * $arr[$j] * $arr[$k] == $m)
                    $count++;

    return $count;
}

    // Driver code
    $arr = array(1, 4, 6, 2, 3, 8);
    $n = sizeof($arr);
    $m = 24;
    echo countTriplets($arr, $n, $m);

// This code is contributed by jit_t.
?>

```

**输出**：

```
3

```

时间复杂度：`O(n ^ 3)`。

一种有效的**方法**使用散列。

1.  将所有元素及其索引存储在哈希映射中。

2.  考虑所有对`(i, j)`并检查以下各项：

    *   如果`arr[i] * arr[j] != 0 && m % (arr[i] * arr[j]) == 0`，则搜索`m / (arr[i] * arr[j]`。

    *   还要检查`m / (arr[i] * arr[j])`不等于`arr[i]`和`arr[j]`。

    *   另外，通过使用映射中存储的索引，检查当前三元组是否未在前面进行计数。

    *   如果满足以上所有条件，则增加计数。

3.  返回计数。

## C++

```cpp

// C++ program to count triplets with given
// product m
#include <bits/stdc++.h>
using namespace std;

// Function to count such triplets
int countTriplets(int arr[], int n, int m)
{
    // Store all the elements in a set
    unordered_map<int, int> occ;
    for (int i = 0; i < n; i++)
        occ[arr[i]] = i;

    int count = 0;

    // Consider all pairs and check for a
    // third number so their product is equal to m
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            // Check if current pair divides m or not
            // If yes, then search for (m / arr[i]*arr[j])
            if ((arr[i] * arr[j] <= m) && (arr[i] * arr[j] != 0) && (m % (arr[i] * arr[j]) == 0)) {
                int check = m / (arr[i] * arr[j]);
                auto it = occ.find(check);

                // Check if the third number is present
                // in the map and it is not equal to any
                // other two elements and also check if
                // this triplet is not counted already
                // using their indexes
                if (check != arr[i] && check != arr[j]
                    && it != occ.end() && it->second > i
                    && it->second > j)
                    count++;
            }
        }
    }

    // Return number of triplets
    return count;
}

// Drivers code
int main()
{
    int arr[] = { 1, 4, 6, 2, 3, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 24;

    cout << countTriplets(arr, n, m);

    return 0;
}

```

## Java

```java

// Java program to count triplets with given
// product m

import java.util.HashMap;

class GFG {
    // Method to count such triplets
    static int countTriplets(int arr[], int n, int m)
    {
        // Store all the elements in a set
        HashMap<Integer, Integer> occ = new HashMap<Integer, Integer>(n);
        for (int i = 0; i < n; i++)
            occ.put(arr[i], i);

        int count = 0;

        // Consider all pairs and check for a
        // third number so their product is equal to m
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                // Check if current pair divides m or not
                // If yes, then search for (m / arr[i]*arr[j])
                if ((arr[i] * arr[j] <= m) && (arr[i] * arr[j] != 0) && (m % (arr[i] * arr[j]) == 0)) {
                    int check = m / (arr[i] * arr[j]);

                    occ.containsKey(check);

                    // Check if the third number is present
                    // in the map and it is not equal to any
                    // other two elements and also check if
                    // this triplet is not counted already
                    // using their indexes
                    if (check != arr[i] && check != arr[j]
                        && occ.containsKey(check) && occ.get(check) > i
                        && occ.get(check) > j)
                        count++;
                }
            }
        }

        // Return number of triplets
        return count;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = { 1, 4, 6, 2, 3, 8 };
        int m = 24;

        System.out.println(countTriplets(arr, arr.length, m));
    }
}

```

## Python3

```py

# Python3 program for the above approach

# Function to find the triplet
def countTriplets(li,product):
    flag = 0
    count = 0

    # Consider all pairs and check 
    # for a third number so their 
    # product is equal to product
    for i in range(len(li)):

        # Check if current pair 
        # divides product or not
        # If yes, then search for
        # (product / li[i]*li[j])
        if li[i]!= 0 and product % li[i] == 0:

            for j in range(i+1, len(li)):

                # Check if the third number is present
                # in the map and it is not equal to any
                # other two elements and also check if
                # this triplet is not counted already
                # using their indexes
                if li[j]!= 0 and product % (li[j]*li[i]) == 0:
                    if product // (li[j]*li[i]) in li:

                        n = li.index(product//(li[j]*li[i]))

                        if n > i and n > j:
                            flag = 1
                            count+=1
    print(count)

# Driver code 
li = [  1, 4, 6, 2, 3, 8 ]
product = 24

# Function call
countTriplets(li,product)

```

## C#

```cs

// C# implementation of the above 
// approach 
using System;
using System.Collections.Generic; 
class GFG{

// Method to count such triplets
static int countTriplets(int[] arr, 
                         int n, int m)
{
  // Store all the elements 
  // in a set
  Dictionary<int, 
             int> occ = new Dictionary<int, 
                                       int>(n);  

  for (int i = 0; i < n; i++)
    occ.Add(arr[i], i);

  int count = 0;

  // Consider all pairs and 
  // check for a third number 
  // so their product is equal to m
  for (int i = 0; i < n - 1; i++) 
  {
    for (int j = i + 1; j < n; j++) 
    {
      // Check if current pair divides 
      // m or not If yes, then search 
      // for (m / arr[i]*arr[j])
      if ((arr[i] * arr[j] <= m) && 
          (arr[i] * arr[j] != 0) && 
          (m % (arr[i] * arr[j]) == 0)) 
      {
        int check = m / (arr[i] * arr[j]);

        //occ.containsKey(check);
        // Check if the third number 
        // is present in the map and 
        // it is not equal to any
        // other two elements and also 
        // check if this triplet is not 
        // counted already using their indexes
        if (check != arr[i] && 
            check != arr[j] && 
            occ.ContainsKey(check) && 
            occ[check] > i && 
            occ[check] > j)
          count++;
      }
    }
  }

  // Return number of triplets
  return count;
}

// Driver code
static void Main() 
{
  int[] arr = {1, 4, 6, 
               2, 3, 8};
  int m = 24;
  Console.WriteLine(countTriplets(arr, 
                                  arr.Length, m));
}
}

// This code is contributed by divyeshrabadiya07

```

**输出**：

```
3

```

时间复杂度：`O(N ^ 2)`。

辅助空间：`O(n)`。

本文由 [**Sahil Chhabra**](https://www.facebook.com/sahil.chhabra.965) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，您还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想共享有关上述主题的更多信息，请发表评论。

