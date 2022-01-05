# 通过将数组拆分为两个子集，最大可能和的最小子集

> 原文:[https://www . geesforgeks . org/通过将数组拆分为两个子集获得最大可能和的最小子集/](https://www.geeksforgeeks.org/smallest-subset-of-maximum-sum-possible-by-splitting-array-into-two-subsets/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印通过将该数组拆分为两个子集而获得的两个子集中较小的一个，使得较小子集的总和最大化。

**示例:**

> **输入:** arr[] = {5，3，2，4，1，2}
> **输出:** 4 5
> **解释:**
> 将数组拆分为{4，5}和{1，2，2，3}两个子集。
> 子集{4，5}的长度最小，即 2，最大和= 4 + 5 = 9。
> 
> **输入:** arr[] = {20，15，20，50，20 }
> T3】输出: 15 50

**方法:**给定的问题可以通过[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)来解决。
按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如说 **M** ，来[存储数组](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)**arr【】**每个字符的频率。
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**并增加 HashMap **M** 中每个字符的计数。
*   初始化两个变量，比如 **S** 和**标志**，分别存储第一个子集的和和以及是否存在答案。
*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化一个[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)，比如**和**，来存储结果子集的元素。
*   [按照](https://www.geeksforgeeks.org/iterating-arrays-java/)[的相反顺序](https://www.geeksforgeeks.org/collections-reverseorder-java-examples/)遍历阵列 **arr[]** ，并执行以下步骤:
    *   将当前字符的频率存储在一个变量中，比如 **F** 。
    *   如果 **(F + ans.size())** 小于(**N –( F+ans . size()))**，则在数组列表 **ans** 中追加元素**arr【I】**的次数。
    *   将 **i** 的值减 **F** 。
    *   如果 **S** 的值大于[数组元素之和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)，则将**标志**标记为**真**，然后[破](https://www.geeksforgeeks.org/break-statement-in-java/)。
*   完成上述步骤后，如果**标志**的值为**真**，则打印数组列表**和**作为结果子集。否则，打印 **-1** 。这

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split array elements
// into two subsets having sum of
// the smaller subset maximized
static void findSubset(vector<int> arr)
{

    // Stores the size of the array
    int N = arr.size();

    // Stores the frequency
    // of array elements
    map<int,int> mp;

    // Stores the total
    // sum of the array
    int totSum = 0;

    // Stores the sum of
    // the resultant set
    int s = 0;

    // Stores if it is possible
    // to split the array that
    // satisfies the conditions
    int flag = 0;

    // Stores the elements
    // of the first subseta
    vector<int> ans;

    // Traverse the array arr[]
    for (int i = 0;
         i < arr.size(); i++) {

        // Increment total sum
        totSum += arr[i];

        // Increment count of arr[i]
        mp[arr[i]]=mp[arr[i]]+1;
      } 

    // Sort the array arr[]
    sort(arr.begin(),arr.end());

    // Stores the index of the
    // last element of the array
    int i = N - 1;

    // Traverse the array arr[]
    while (i >= 0) {

        // Stores the frequency
        // of arr[i]
        int frq = mp[arr[i]];

        // If frq + ans.size() is
        // at most remaining size
        if ((frq + ans.size())
            < (N - (frq + ans.size())))
        {

            for (int k = 0; k < frq; k++)
            {

                // Append arr[i] to ans
                ans.push_back(arr[i]);

                // Decrement totSum by arr[i]
                totSum -= arr[i];

                // Increment s by arr[i]
                s += arr[i];

                i--;
            }
        }

        // Otherwise, decrement i
        // by frq
        else {
            i -= frq;
        }

        // If s is greater
        // than totSum
        if (s > totSum) {

            // Mark flag 1
            flag = 1;
            break;
        }
    }

    // If flag is equal to 1
    if (flag == 1) {

        // Print the arrList ans
        for (i = ans.size() - 1;
             i >= 0; i--) {

            cout<<ans[i]<<" ";
        }
    }

    // Otherwise, print "-1"
    else {
        cout<<-1;
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 5, 3, 2, 4, 1, 2 };
    findSubset(arr);
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to split array elements
    // into two subsets having sum of
    // the smaller subset maximized
    static void findSubset(int[] arr)
    {
        // Stores the size of the array
        int N = arr.length;

        // Stores the frequency
        // of array elements
        Map<Integer, Integer> map
            = new HashMap<>();

        // Stores the total
        // sum of the array
        int totSum = 0;

        // Stores the sum of
        // the resultant set
        int s = 0;

        // Stores if it is possible
        // to split the array that
        // satisfies the conditions
        int flag = 0;

        // Stores the elements
        // of the first subset
        ArrayList<Integer> ans
            = new ArrayList<>();

        // Traverse the array arr[]
        for (int i = 0;
             i < arr.length; i++) {

            // Increment total sum
            totSum += arr[i];

            // Increment count of arr[i]
            map.put(arr[i],
                    map.getOrDefault(
                        arr[i], 0)
                        + 1);
        }

        // Sort the array arr[]
        Arrays.sort(arr);

        // Stores the index of the
        // last element of the array
        int i = N - 1;

        // Traverse the array arr[]
        while (i >= 0) {

            // Stores the frequency
            // of arr[i]
            int frq = map.get(arr[i]);

            // If frq + ans.size() is
            // at most remaining size
            if ((frq + ans.size())
                < (N - (frq + ans.size()))) {

                for (int k = 0; k < frq; k++) {

                    // Append arr[i] to ans
                    ans.add(arr[i]);

                    // Decrement totSum by arr[i]
                    totSum -= arr[i];

                    // Increment s by arr[i]
                    s += arr[i];

                    i--;
                }
            }

            // Otherwise, decrement i
            // by frq
            else {
                i -= frq;
            }

            // If s is greater
            // than totSum
            if (s > totSum) {

                // Mark flag 1
                flag = 1;
                break;
            }
        }

        // If flag is equal to 1
        if (flag == 1) {

            // Print the arrList ans
            for (i = ans.size() - 1;
                 i >= 0; i--) {

                System.out.print(
                    ans.get(i) + " ");
            }
        }

        // Otherwise, print "-1"
        else {
            System.out.print(-1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 5, 3, 2, 4, 1, 2 };
        findSubset(arr);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict

# Function to split array elements
# into two subsets having sum of
# the smaller subset maximized
def findSubset(arr):

    # Stores the size of the array
    N = len(arr)

    # Stores the frequency
    # of array elements
    mp = defaultdict(int)

    # Stores the total
    # sum of the array
    totSum = 0

    # Stores the sum of
    # the resultant set
    s = 0

    # Stores if it is possible
    # to split the array that
    # satisfies the conditions
    flag = 0

    # Stores the elements
    # of the first subseta
    ans = []

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Increment total sum
        totSum += arr[i]

        # Increment count of arr[i]
        mp[arr[i]] = mp[arr[i]]+1

    # Sort the array arr[]
    arr.sort()

    # Stores the index of the
    # last element of the array
    i = N - 1

    # Traverse the array arr[]
    while (i >= 0):

        # Stores the frequency
        # of arr[i]
        frq = mp[arr[i]]

        # If frq + ans.size() is
        # at most remaining size
        if ((frq + len(ans))
                < (N - (frq + len(ans)))):

            for k in range(frq):

                # Append arr[i] to ans
                ans.append(arr[i])

                # Decrement totSum by arr[i]
                totSum -= arr[i]

                # Increment s by arr[i]
                s += arr[i]
                i -= 1

        # Otherwise, decrement i
        # by frq
        else:
            i -= frq

        # If s is greater
        # than totSum
        if (s > totSum):

            # Mark flag 1
            flag = 1
            break

    # If flag is equal to 1
    if (flag == 1):

        # Print the arrList ans
        for i in range(len(ans) - 1, -1, -1):

            print(ans[i], end = " ")

    # Otherwise, print "-1"
    else:
        print(-1)

# Driver Code
if __name__ == "__main__":

    arr = [5, 3, 2, 4, 1, 2]
    findSubset(arr)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to split array elements
// into two subsets having sum of
// the smaller subset maximized
static void findSubset(List<int> arr)
{

    // Stores the size of the array
    int N = arr.Count;
    int i;

    // Stores the frequency
    // of array elements
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Stores the total
    // sum of the array
    int totSum = 0;

    // Stores the sum of
    // the resultant set
    int s = 0;

    // Stores if it is possible
    // to split the array that
    // satisfies the conditions
    int flag = 0;

    // Stores the elements
    // of the first subseta
    List<int> ans = new List<int>();

    // Traverse the array arr[]
    for (i = 0;
         i < arr.Count; i++) {

        // Increment total sum
        totSum += arr[i];

        // Increment count of arr[i]
        if(mp.ContainsKey(arr[i]))
         mp[arr[i]]=mp[arr[i]]+1;
        else
          mp.Add(arr[i],1);
      } 

    // Sort the array arr[]
    arr.Sort();

    // Stores the index of the
    // last element of the array
    i = N - 1;

    // Traverse the array arr[]
    while (i >= 0) {

        // Stores the frequency
        // of arr[i]
        int frq = mp[arr[i]];

        // If frq + ans.size() is
        // at most remaining size
        if ((frq + ans.Count)
            < (N - (frq + ans.Count)))
        {

            for (int k = 0; k < frq; k++)
            {

                // Append arr[i] to ans
                ans.Add(arr[i]);

                // Decrement totSum by arr[i]
                totSum -= arr[i];

                // Increment s by arr[i]
                s += arr[i];

                i--;
            }
        }

        // Otherwise, decrement i
        // by frq
        else {
            i -= frq;
        }

        // If s is greater
        // than totSum
        if (s > totSum) {

            // Mark flag 1
            flag = 1;
            break;
        }
    }

    // If flag is equal to 1
    if (flag == 1) {

        // Print the arrList ans
        for (i = ans.Count - 1;
             i >= 0; i--) {

            Console.Write(ans[i]+" ");
        }
    }

    // Otherwise, print "-1"
    else {
        Console.Write(-1);
    }
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 5, 3, 2, 4, 1, 2 };
    findSubset(arr);
}

}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to split array elements
// into two subsets having sum of
// the smaller subset maximized
function findSubset(arr)
{

    // Stores the size of the array
    var N = arr.length;

    // Stores the frequency
    // of array elements
    var mp = new Map();

    // Stores the total
    // sum of the array
    var totSum = 0;

    // Stores the sum of
    // the resultant set
    var s = 0;

    // Stores if it is possible
    // to split the array that
    // satisfies the conditions
    var flag = 0;

    // Stores the elements
    // of the first subseta
    var ans = [];

    // Traverse the array arr[]
    for (var i = 0;
         i < arr.length; i++) {

        // Increment total sum
        totSum += arr[i];

        // Increment count of arr[i]
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1);
      } 

    // Sort the array arr[]
    arr.sort((a,b)=> a-b)

    // Stores the index of the
    // last element of the array
    var i = N - 1;

    // Traverse the array arr[]
    while (i >= 0) {

        // Stores the frequency
        // of arr[i]
        var frq = mp.get(arr[i]);

        // If frq + ans.size() is
        // at most remaining size
        if ((frq + ans.length)
            < (N - (frq + ans.length)))
        {

            for (var k = 0; k < frq; k++)
            {

                // Append arr[i] to ans
                ans.push(arr[i]);

                // Decrement totSum by arr[i]
                totSum -= arr[i];

                // Increment s by arr[i]
                s += arr[i];

                i--;
            }
        }

        // Otherwise, decrement i
        // by frq
        else {
            i -= frq;
        }

        // If s is greater
        // than totSum
        if (s > totSum) {

            // Mark flag 1
            flag = 1;
            break;
        }
    }

    // If flag is equal to 1
    if (flag == 1) {

        // Print the arrList ans
        for (i = ans.length - 1;
             i >= 0; i--) {

            document.write( ans[i] + " ");
        }
    }

    // Otherwise, print "-1"
    else {
        document.write(-1);
    }
}

// Driver Code
var arr = [5, 3, 2, 4, 1, 2 ];
findSubset(arr);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
4 5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*