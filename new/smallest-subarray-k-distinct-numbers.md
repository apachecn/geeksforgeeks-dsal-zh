# 具有 k 个不同数字的最小子数组

> 原文：[https://www.geeksforgeeks.org/smallest-subarray-k-distinct-numbers/](https://www.geeksforgeeks.org/smallest-subarray-k-distinct-numbers/)

给定一个由 n 个整数和一个整数 k 组成的数组。 我们需要在数组[l，r]中找到最小范围（l 和 r 都包括在内），以便恰好有 k 个不同的数字。

**示例**：

```
Input : arr[] = { 1, 1, 2, 2, 3, 3, 4, 5} 
            k = 3
Output : 5 7

Input : arr[] = { 1, 2, 2, 3} 
            k = 2
Output : 0 1

```

**简单解决方案**是使用两个嵌套循环。 外循环用于选择起点，内循环用于选择终点。 对于每对起点到起点，我们都会计算其中的不同元素，如果当前窗口较小，则会更新结果。 我们使用散列来计算范围内的不同元素。

## C++

```cpp

// C++ program to find minimum range that
// contains exactly k distinct numbers.
#include <bits/stdc++.h>
using namespace std;

// Prints the minimum range that contains exactly
// k distinct numbers.
void minRange(int arr[], int n, int k)
{
    int l = 0, r = n;

    // Consider every element as starting
    // point.
    for (int i = 0; i < n; i++) {

        // Find the smallest window starting
        // with arr[i] and containing exactly
        // k distinct elements.
        unordered_set<int> s;
        int j;
        for (j = i; j < n; j++) {
            s.insert(arr[j]);
            if (s.size() == k) {
                if ((j - i) < (r - l)) {
                    r = j;
                    l = i;
                }
                break;
            }
        }

        // There are less than k distinct elements
        // now, so no need to continue.
        if (j == n)
            break;
    }

    // If there was no window with k distinct
    // elements (k is greater than total distinct
    // elements)
    if (l == 0 && r == n)
        cout << "Invalid k";
    else
        cout << l << " " << r;
}

// Driver code for above function.
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    minRange(arr, n, k);
    return 0;
}

```

## Java

```java

// Java program to find minimum 
// range that contains exactly 
// k distinct numbers.
import java.util.*;

class GFG 
{

// Prints the minimum range 
// that contains exactly k 
// distinct numbers.
static void minRange(int arr[], 
                     int n, int k)
{
    int l = 0, r = n;

    // Consider every element 
    // as starting point.
    for (int i = 0; i < n; i++)
    {

        // Find the smallest window 
        // starting with arr[i] and 
        // containing exactly k 
        // distinct elements.
        Set<Integer> s = new HashSet<Integer>();
        int j;
        for (j = i; j < n; j++) 
        {
            s.add(arr[j]);
            if (s.size() == k) 
            {
                if ((j - i) < (r - l))
                {
                    r = j;
                    l = i;
                }
                break;
            }
        }

        // There are less than k 
        // distinct elements now, 
        // so no need to continue.
        if (j == n)
            break;
    }

    // If there was no window 
    // with k distinct elements 
    // (k is greater than total 
    // distinct elements)
    if (l == 0 && r == n)
        System.out.println("Invalid k");
    else
        System.out.println(l + " " + r);
}

// Driver code 
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;
    int k = 3;
    minRange(arr, n, k);
}
}

// This code is contributed 
// by Kirti_Mangal

```

## Python 3

```

# Python 3 program to find minimum range 
# that contains exactly k distinct numbers.

# Prints the minimum range that contains 
# exactly k distinct numbers.
def minRange(arr, n, k):

    l = 0
    r = n

    # Consider every element as 
    # starting point.
    for i in range(n):

        # Find the smallest window starting
        # with arr[i] and containing exactly
        # k distinct elements.
        s = []
        for j in range(i, n) :
            s.append(arr[j])
            if (len(s) == k):
                if ((j - i) < (r - l)) :
                    r = j
                    l = i

                break

        # There are less than k distinct 
        # elements now, so no need to continue.
        if (j == n):
            break

    # If there was no window with k distinct
    # elements (k is greater than total 
    # distinct elements)
    if (l == 0 and r == n):
        print("Invalid k")
    else:
        print(l, r)

# Driver code 
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5 ]
    n = len(arr)
    k = 3
    minRange(arr, n, k)

# This code is contributed 
# by ChitraNayal

```

## C#

```cs

// C#  program to find minimum  
// range that contains exactly  
// k distinct numbers. 
using System;
using System.Collections.Generic;

public class GFG
{

// Prints the minimum range  
// that contains exactly k  
// distinct numbers. 
public static void minRange(int[] arr, int n, int k)
{
    int l = 0, r = n;

    // Consider every element  
    // as starting point. 
    for (int i = 0; i < n; i++)
    {

        // Find the smallest window  
        // starting with arr[i] and  
        // containing exactly k  
        // distinct elements. 
        ISet<int> s = new HashSet<int>();
        int j;
        for (j = i; j < n; j++)
        {
            s.Add(arr[j]);
            if (s.Count == k)
            {
                if ((j - i) < (r - l))
                {
                    r = j;
                    l = i;
                }
                break;
            }
        }

        // There are less than k  
        // distinct elements now,  
        // so no need to continue. 
        if (j == n)
        {
            break;
        }
    }

    // If there was no window  
    // with k distinct elements  
    // (k is greater than total  
    // distinct elements) 
    if (l == 0 && r == n)
    {
        Console.WriteLine("Invalid k");
    }
    else
    {
        Console.WriteLine(l + " " + r);
    }
}

// Driver code  
public static void Main(string[] args)
{
    int[] arr = new int[] {1, 2, 3, 4, 5};
    int n = arr.Length;
    int k = 3;
    minRange(arr, n, k);
}
}

// This code is contributed by Shrikant13

```

**输出**：

```
0 2

```

**时间复杂度**：`O(N ^ 2)`

**通过上述简单解决方案的优化**。 我们的想法是在找到 k 个不同的元素后删除左侧的重复项。

## C++

```cpp

// C++ program to find minimum range that
// contains exactly k distinct numbers.
#include <bits/stdc++.h>
using namespace std;

// prints the minimum range that contains exactly
// k distinct numbers.
void minRange(int arr[], int n, int k)
{
    // Initially left and right side is -1 and -1,
    // number of distinct elements are zero and
    // range is n.
    int l = 0, r = n;

    int j = -1; // Initialize right side
    map<int, int> hm;
    for (int i=0; i<n; i++)
    {
        while (j < n)
        {
            // increment right side.
            j++;

            // if number of distinct elements less
            // than k.
            if (hm.size() < k)
                hm[arr[j]]++;

            // if distinct elements are equal to k
            // and length is less than previous length.
            if (hm.size() == k && ((r - l) >= (j - i)))
            {
                l = i;
                r = j;
                break;
            }
        }

        // if number of distinct elements less
        // than k, then break.
        if (hm.size() < k)
            break;

        // if distinct elements equals to k then
        // try to increment left side.
        while (hm.size() == k)
        {

            if (hm[arr[i]] == 1)
                hm.erase(arr[i]);
            else
                hm[arr[i]]--;

            // increment left side.
            i++;

            // it is same as explained in above loop.
            if (hm.size() == k && (r - l) >= (j - i))
            {
                l = i;
                r = j;
            }
        }
        if (hm[arr[i]] == 1)
            hm.erase(arr[i]);
        else
            hm[arr[i]]--;
    }

    if (l == 0 && r == n)
        cout << "Invalid k" << endl;
    else
        cout << l << " " << r << endl;
}

// Driver code for above function.
int main()
{
    int arr[] = { 1, 1, 2, 2, 3, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    minRange(arr, n, k);
    return 0;
}

```

## Java

```java

// Java program to find minimum range that
// contains exactly k distinct numbers.
import java.util.*;

class GFG{

// Prints the minimum range that contains exactly
// k distinct numbers.
static void minRange(int arr[], int n, int k)
{

    // Initially left and right side is -1 and -1,
    // number of distinct elements are zero and
    // range is n.
    int l = 0, r = n;

    // Initialize right side
    int j = -1; 

    HashMap<Integer, Integer> hm = new HashMap<>();

    for(int i = 0; i < n; i++)
    {
        while (j < n)
        {

            // Increment right side.
            j++;

            // If number of distinct elements less
            // than k.
            if (j < n && hm.size() < k)
                hm.put(arr[j],
                       hm.getOrDefault(arr[j], 0) + 1);

            // If distinct elements are equal to k
            // and length is less than previous length.
            if (hm.size() == k && 
                 ((r - l) >= (j - i)))
            {
                l = i;
                r = j;
                break;
            }
        }

        // If number of distinct elements less
        // than k, then break.
        if (hm.size() < k)
            break;

        // If distinct elements equals to k then
        // try to increment left side.
        while (hm.size() == k)
        {
            if (hm.getOrDefault(arr[i], 0) == 1)
                hm.remove(arr[i]);
            else
                hm.put(arr[i],
                       hm.getOrDefault(arr[i], 0) - 1);

            // Increment left side.
            i++;

            // It is same as explained in above loop.
            if (hm.size() == k &&
                  (r - l) >= (j - i)) 
            {
                l = i;
                r = j;
            }
        }
        if (hm.getOrDefault(arr[i], 0) == 1)
            hm.remove(arr[i]);
        else
            hm.put(arr[i],
                hm.getOrDefault(arr[i], 0) - 1);
    }

    if (l == 0 && r == n)
        System.out.println("Invalid k");
    else
        System.out.println(l + " " + r);
}

// Driver code 
public static void main(String[] args)
{
    int arr[] = { 1, 1, 2, 2, 3, 3, 4, 5 };
    int n = arr.length;
    int k = 3;

    minRange(arr, n, k);
}
}

// This code is contributed by jrishabh99

```

## Python3

```py

# Python3 program to find the minimum range 
# that contains exactly k distinct numbers. 
from collections import defaultdict

# Prints the minimum range that contains 
# exactly k distinct numbers. 
def minRange(arr, n, k): 

    # Initially left and right side is -1 
    # and -1, number of distinct elements 
    # are zero and range is n. 
    l, r = 0, n 
    i = 0
    j = -1 # Initialize right side 

    hm = defaultdict(lambda:0) 
    while i < n: 

        while j < n: 

            # increment right side. 
            j += 1

            # if number of distinct elements less than k. 
            if len(hm) < k and j < n:
                hm[arr[j]] += 1

            # if distinct elements are equal to k 
            # and length is less than previous length. 
            if len(hm) == k and ((r - l) >= (j - i)): 

                l, r = i, j 
                break

        # if number of distinct elements less 
        # than k, then break. 
        if len(hm) < k:
            break

        # if distinct elements equals to k then 
        # try to increment left side. 
        while len(hm) == k: 

            if hm[arr[i]] == 1: 
                del(hm[arr[i]]) 
            else:
                hm[arr[i]] -= 1

            # increment left side. 
            i += 1

            # it is same as explained in above loop. 
            if len(hm) == k and (r - l) >= (j - i): 

                l, r = i, j 

        if hm[arr[i]] == 1: 
            del(hm[arr[i]]) 
        else:
            hm[arr[i]] -= 1

        i += 1

    if l == 0 and r == n:
        print("Invalid k") 
    else:
        print(l, r) 

# Driver code for above function. 
if __name__ == "__main__": 

    arr = [1, 1, 2, 2, 3, 3, 4, 5]  
    n = len(arr) 
    k = 3
    minRange(arr, n, k) 

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to find minimum 
// range that contains exactly 
// k distinct numbers.
using System;
using System.Collections.Generic;
class GFG{

// Prints the minimum 
// range that contains exactly
// k distinct numbers.
static void minRange(int []arr, 
                     int n, int k)
{
  // Initially left and 
  // right side is -1 and -1,
  // number of distinct 
  // elements are zero and
  // range is n.
  int l = 0, r = n;

  // Initialize right side
  int j = -1; 

  Dictionary<int, 
             int> hm = new Dictionary<int, 
                                      int>();

  for(int i = 0; i < n; i++)
  {
    while (j < n)
    {
      // Increment right side.
      j++;

      // If number of distinct elements less
      // than k.
      if (j < n && hm.Count < k)
        if(hm.ContainsKey(arr[j]))
          hm[arr[j]] = hm[arr[j]] + 1;
      else
        hm.Add(arr[j], 1);

      // If distinct elements are equal to k
      // and length is less than previous length.
      if (hm.Count == k && 
         ((r - l) >= (j - i)))
      {
        l = i;
        r = j;
        break;
      }
    }

    // If number of distinct elements less
    // than k, then break.
    if (hm.Count < k)
      break;

    // If distinct elements equals to k then
    // try to increment left side.
    while (hm.Count == k)
    {
      if (hm.ContainsKey(arr[i]) &&  
          hm[arr[i]] == 1)
        hm.Remove(arr[i]);
      else
      {
        if(hm.ContainsKey(arr[i]))
          hm[arr[i]] = hm[arr[i]] - 1;
      }

      // Increment left side.
      i++;

      // It is same as explained in above loop.
      if (hm.Count == k &&
         (r - l) >= (j - i)) 
      {
        l = i;
        r = j;
      }
    }
    if (hm.ContainsKey(arr[i]) &&  
        hm[arr[i]] == 1)
      hm.Remove(arr[i]);
    else
      if(hm.ContainsKey(arr[i]))
        hm[arr[i]] = hm[arr[i]] - 1;
  }

  if (l == 0 && r == n)
    Console.WriteLine("Invalid k");
  else
    Console.WriteLine(l + " " + r);
}

// Driver code 
public static void Main(String[] args)
{
  int []arr = {1, 1, 2, 2, 
               3, 3, 4, 5};
  int n = arr.Length;
  int k = 3;
  minRange(arr, n, k);
}
}

// This code is contributed by shikhasingrajput

```

**输出**：

```
5 7

```

该解决方案的时间复杂度为`O(n)`。 在每个嵌套迭代中，我们要么添加一个元素，要么删除一个元素。 每个元素最多只能插入和删除一次。

本文由 [**Pawan Asipu**](https://www.facebook.com/pawan.asipu.5) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

