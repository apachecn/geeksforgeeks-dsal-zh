# 将包含 N 个元素的数组拆分成 K 组不同的元素

> 原文:[https://www . geeksforgeeks . org/将包含 n 个元素的数组拆分为 k 个不同的元素集/](https://www.geeksforgeeks.org/split-an-array-containing-n-elements-into-k-sets-of-distinct-elements/)

给定两个整数 **N** 和 **K** 以及一个由重复元素组成的数组**arr【】**，任务是将 N 个元素拆分成 K 组不同的元素。
**举例:**

> **输入:** N = 5，K = 2，arr[] = {3，2，1，2，3}
> **输出:**
> ( 3 2 1 )
> ( 2 3 )
> **输入:** N = 5，K = 2，arr[] = {2，1，1，2，1}
> **输出:** -1
> **说明:**
> 不可能全部拆分

**方法:**为了解决这个问题，我们使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来[存储每个元素](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)的频率。如果任何元素的频率超过 **K** ，打印 **-1** 。维护另一个地图来存储每个频率的集合。如果没有任何元素的频率大于 **K** ，则打印所有相应频率的集合作为所需集合。
以下是上述方法的实施:

## C++

```
// C++ Program to split N elements
// into exactly K sets consisting
// of no distinct elements

#include <bits/stdc++.h>
using namespace std;

// Function to check if possible to
// split N elements into exactly K
// sets consisting of no distinct elements
void splitSets(int a[], int n, int k)
{
    // Store the frequency
    // of each element
    map<int, int> freq;

    // Store the required sets
    map<int, vector<int> > ans;

    for (int i = 0; i < n; i++) {
        // If frequency of a
        // particular element
        // exceeds K
        if (freq[a[i]] + 1 > k) {
            // Not possible
            cout << -1 << endl;
            return;
        }

        // Increase the frequency
        freq[a[i]] += 1;
        // Store the element for the
        // respective set
        ans[freq[a[i]]].push_back(a[i]);
    }

    // Display the sets
    for (auto it : ans) {
        cout << "( ";
        for (int i : it.second) {
            cout << i << " ";
        }
        cout << ")\n";
    }
}

// Driver code
int main()
{

    int arr[] = { 2, 1, 2, 3, 1,
                  4, 1, 3, 1, 4 };
    int n = sizeof(arr) / sizeof(int);

    int k = 4;

    splitSets(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split N elements
// into exactly K sets consisting
// of no distinct elements
import java.util.*;

class GFG{

// Function to check if possible to
// split N elements into exactly K
// sets consisting of no distinct elements
static void splitSets(int a[], int n, int k)
{

    // Store the frequency
    // of each element
    Map<Integer, Integer> freq = new HashMap<>();

    // Store the required sets
    Map<Integer,
        ArrayList<Integer>> ans = new HashMap<>();

    for(int i = 0; i < n; i++)
    {

        // If frequency of a
        // particular element
        // exceeds K
        if(freq.get(a[i]) != null)
        {
            if (freq.get(a[i]) + 1 > k)
            {

                // Not possible
                System.out.println(-1);
                return;
            }
        }

        // Increase the frequency
        freq.put(a[i], freq.getOrDefault(a[i], 0) + 1 );

        // Store the element for the
        // respective set
        if( ans.get(freq.get(a[i])) == null)
            ans.put(freq.get(a[i]),
                    new ArrayList<Integer>());

        ans.get(freq.get(a[i])).add(a[i]);
    }

    // Display the sets
    for(ArrayList<Integer> it : ans.values())
    {
        System.out.print("( ");
        for(int i = 0; i < it.size() - 1; i++)
        {
            System.out.print(it.get(i) + " ");
        }

        System.out.print(it.get(it.size() - 1));
        System.out.println(" )");
    }
}

// Driver code   
public static void main (String[] args)
{
    int arr[] = { 2, 1, 2, 3, 1,
                  4, 1, 3, 1, 4 };

    int n = arr.length;
    int k = 4;

    splitSets(arr, n, k);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 Program to split N elements
# into exactly K sets consisting
# of no distinct elements

# Function to check if possible to
# split N elements into exactly K
# sets consisting of no distinct elements
def splitSets(a, n, k) :

    # Store the frequency
    # of each element
    freq = {}

    # Store the required sets
    ans = {}

    for i in range(n) :

        # If frequency of a
        # particular element
        # exceeds K
        if a[i] in freq :
            if freq[a[i]] + 1 > k :

                # Not possible
                print(-1)
                return

        # Increase the frequency
        if a[i] in freq :
            freq[a[i]] += 1
        else :
            freq[a[i]] = 1

        # Store the element for the
        # respective set
        if freq[a[i]] in ans :
            ans[freq[a[i]]].append(a[i])
        else :
            ans[freq[a[i]]] = [a[i]]

    # Display the sets
    for it in ans :
        print("( ", end = "")
        for i in ans[it] :
            print(i , end = " ")

        print(")")

arr = [ 2, 1, 2, 3, 1, 4, 1, 3, 1, 4 ]
n = len(arr)

k = 4

splitSets(arr, n, k)

# This code is contributed by divyesh072019
```

## C#

```
// C# Program to split N elements
// into exactly K sets consisting
// of no distinct elements
using System;
using System.Collections.Generic;
class GFG
{

  // Function to check if possible to
  // split N elements into exactly K
  // sets consisting of no distinct elements
  static void splitSets(int[] a, int n, int k)
  {
    // Store the frequency
    // of each element
    Dictionary<int, int> freq = new Dictionary<int, int>();

    // Store the required sets
    Dictionary<int, List<int>> ans = new Dictionary<int, List<int>>();

    for (int i = 0; i < n; i++)
    {

      // If frequency of a
      // particular element
      // exceeds K
      if(freq.ContainsKey(a[i]))
      {
        if(freq[a[i]] + 1 > k)
        {

          // Not possible
          Console.WriteLine(-1);
          return;
        }
      }
      else if(1 > k)
      {

        // Not possible
        Console.WriteLine(-1);
        return;
      }

      // Increase the frequency
      if(freq.ContainsKey(a[i]))
      {
        freq[a[i]] += 1;
      }
      else
      {
        freq[a[i]] = 1;
      }

      // Store the element for the
      // respective set
      if(ans.ContainsKey(freq[a[i]]))
      {
        ans[freq[a[i]]].Add(a[i]);
      }
      else
      {
        ans[freq[a[i]]] = new List<int>();
        ans[freq[a[i]]].Add(a[i]);
      }

    }

    // Display the sets
    foreach(KeyValuePair<int, List<int>> it in ans)
    {
      Console.Write("( ");
      foreach(int i in it.Value)
      {
        Console.Write(i + " ");
      }
      Console.WriteLine(")");
    }
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 2, 1, 2, 3, 1,
                 4, 1, 3, 1, 4 };
    int n = arr.Length;
    int k = 4;
    splitSets(arr, n, k);
  }
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
( 2 1 3 4 )
( 2 1 3 4 )
( 1 )
( 1 )
```