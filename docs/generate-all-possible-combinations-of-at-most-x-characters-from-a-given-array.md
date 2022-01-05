# 从给定数组中生成最多 X 个字符的所有可能组合

> 原文:[https://www . geeksforgeeks . org/从给定数组中生成最多 x 个字符的所有可能组合/](https://www.geeksforgeeks.org/generate-all-possible-combinations-of-at-most-x-characters-from-a-given-array/)

给定一个由 **N** 个字符组成的数组**arr【】**，任务是生成最多 **X** 个元素(1 ≤ X ≤ N)的所有可能组合。

**示例:**

> **输入:** N = 3，X = 2，arr[] = {'a '，' b '，' a'}
> **输出:** a b c bc ca ab cb ac ba
> **解释:**使用 1 个字符的所有可能组合为 3 {'a '，' b '，' c'}。使用 2 个字符的所有可能组合为{“BC”“ca”“ab”“CB”“AC”“ba”}。
> 
> **输入:** N = 3，X = 3，arr[]= {‘d’，‘a’，‘b’}
> **输出:**d a b da ab BD da ba db DBA Abd ADB BDA bad

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法来解决。按照以下步骤解决问题:

1.  生成可以用 1 个字符创建的所有可能的排列，这是给定的数组 **arr[]** 。
2.  存储所有排列。
3.  一旦存储，生成 2 个字符的所有可能的排列并存储它们。
4.  一旦最后一步完成，丢弃单个字符的所有排列。
5.  以同样的方式迭代计算排列，直到达到 **X** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate permutations of
// at most X elements from array arr[]
void differentFlagPermutations(int X,
                               vector<string> arr)
{
    vector<string> ml;
    ml = arr;

    for(int i = 0; i < ml.size(); i++)
    {
        cout << ml[i] << " ";
    }

    int count = ml.size();

    // Traverse all possible lengths
    for(int z = 0; z < X - 1; z++)
    {

        // Stores all combinations
        // of length z
        vector<string> tmp;

        // Traverse the array
        for(int i = 0; i < arr.size(); i++)
        {
            for(int k = 0; k < ml.size(); k++)
            {
                if (arr[i] != ml[k])
                {

                    // Generate all
                    // combinations of length z
                    tmp.push_back(ml[k] + arr[i]);
                    count += 1;
                }
            }
        }    

        // Print all combinations of length z
        for(int i = 0; i < tmp.size(); i++)
        {
            cout << tmp[i] << " ";
        }

        // Replace all combinations of length z - 1
        // with all combinations of length z
        ml = tmp;
    }
}

// Driver Code
int main()
{

    // Given array
    vector<string> arr{ "c", "a", "b" };

    // Given X
    int X = 2;

    differentFlagPermutations(X, arr);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to generate permutations of
// at most X elements from array arr[]
static void differentFlagPermutations(int X,
                               String[] arr)
{
    String[] ml = arr;

    for(int i = 0; i < ml.length; i++)
    {
        System.out.print(ml[i] + " ");
    }

    int count = ml.length;

    // Traverse all possible lengths
    for(int z = 0; z < X - 1; z++)
    {

        // Stores all combinations
        // of length z
        Vector<String> tmp = new Vector<String>();

        // Traverse the array
        for(int i = 0; i < arr.length; i++)
        {
            for(int k = 0; k < ml.length; k++)
            {
                if (arr[i] != ml[k])
                {

                    // Generate all
                    // combinations of length z
                    tmp.add(ml[k] + arr[i]);
                    count += 1;
                }
            }
        }    

        // Print all combinations of length z
        for(int i = 0; i < tmp.size(); i++)
        {
            System.out.print(tmp.get(i) + " ");
        }

        // Replace all combinations of length z - 1
        // with all combinations of length z
        ml = tmp.toArray(new String[tmp.size()]);;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    String []arr = { "c", "a", "b" };

    // Given X
    int X = 2;     
    differentFlagPermutations(X, arr);  
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to generate permutations of
# at most X elements from array arr[]
def differentFlagPermutations(X, arr):

    ml = arr.copy()

    print(" ".join(ml), end =" ")
    count = len(ml)

    # Traverse all possible lengths
    for z in range(X-1):

        # Stores all combinations
        # of length z
        tmp = []

        # Traverse the array
        for i in arr:
            for k in ml:
                if i not in k:

                    # Generate all
                    # combinations of length z
                    tmp.append(k + i)
                    count += 1

        # Print all combinations of length z
        print(" ".join(tmp), end =" ")

        # Replace all combinations of length z - 1
        # with all combinations of length z
        ml = tmp

# Given array
arr = ['c', 'a', 'b']

# Given X
X = 2

differentFlagPermutations(X, arr)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to generate permutations of
  // at most X elements from array arr[]
  static void differentFlagPermutations(int X, List<string> arr)
  {
    List<string> ml = new List<string>();
    ml = arr;
    for(int i = 0; i < ml.Count; i++)
    {
      Console.Write(ml[i] + " ");
    }

    int count = ml.Count;

    // Traverse all possible lengths
    for(int z = 0; z < X - 1; z++)
    {

      // Stores all combinations
      // of length z
      List<string> tmp = new List<string>();

      // Traverse the array
      for(int i = 0; i < arr.Count; i++)
      {
        for(int k = 0; k < ml.Count; k++)
        {
          if (arr[i] != ml[k])
          {

            // Generate all
            // combinations of length z
            tmp.Add(ml[k] + arr[i]);
            count += 1;
          }
        }
      }    

      // Print all combinations of length z
      for(int i = 0; i < tmp.Count; i++)
      {
        Console.Write(tmp[i] + " ");
      }

      // Replace all combinations of length z - 1
      // with all combinations of length z
      ml = tmp;
    }
  }

  // Driver code
  static void Main()
  {

    // Given array
    List<string> arr = new List<string>(new string[] { "c", "a", "b" });

    // Given X
    int X = 2;

    differentFlagPermutations(X, arr);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to generate permutations of
    // at most X elements from array arr[]
    function differentFlagPermutations(X, arr)
    {
      let ml = [];
      ml = arr;
      for(let i = 0; i < ml.length; i++)
      {
        document.write(ml[i] + " ");
      }

      let count = ml.length;

      // Traverse all possible lengths
      for(let z = 0; z < X - 1; z++)
      {

        // Stores all combinations
        // of length z
        let tmp = [];

        // Traverse the array
        for(let i = 0; i < arr.length; i++)
        {
          for(let k = 0; k < ml.length; k++)
          {
            if (arr[i] != ml[k])
            {

              // Generate all
              // combinations of length z
              tmp.push(ml[k] + arr[i]);
              count += 1;
            }
          }
        }   

        // Print all combinations of length z
        for(let i = 0; i < tmp.length; i++)
        {
          document.write(tmp[i] + " ");
        }

        // Replace all combinations of length z - 1
        // with all combinations of length z
        ml = tmp;
      }
    }

    // Given array
    let arr = [ "c", "a", "b" ];

    // Given X
    let X = 2;

    differentFlagPermutations(X, arr);

</script>
```

**Output:** 

```
c a b ac bc ca ba cb ab
```

***时间复杂度:**O(X * N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*