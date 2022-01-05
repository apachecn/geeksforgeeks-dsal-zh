# 找出从 1 开始的数字，不包括给定的数字

> 原文:[https://www . geesforgeks . org/find-numbers-从 1 开始最多 k 个不包括给定数字的总和/](https://www.geeksforgeeks.org/find-numbers-starting-from-1-with-sum-at-most-k-excluding-given-numbers/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找出从 1 开始的数字，并且不包括给定数组
**的元素，最多 K 个**【示例】:

> **输入** : arr[] = {4，6，8，12}，K = 14
> **输出** : {1，2，3，5}
> **解释**:最大可能和为 11，元素为 1，2，3，5
> 
> **输入** : arr[] = {1，3，4}，K = 7
> **输出** : {2，5}
> **解释**:最大可能和为 7，元素为 2 和 5

**方法:**这个任务可以通过创建一个[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)来存储给定数组的元素来解决。从 **1** 开始**迭代**，通过检查哈希表来跟踪**当前总和**和排除的元素。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required elements
void solve(vector<int>& arr, int K)
{

    // Store the elements of arr[]
    unordered_map<int, int> occ;

    for (int i = 0; i < (int)arr.size(); i++)
        occ[arr[i]]++;

    // Store the current sum
    int curSum = 0;

    // Start from 1
    int cur = 1;

    // Store the answer
    vector<int> ans;

    while (curSum + cur <= K) {

        // Exclude the current element
        if (occ.find(cur) != occ.end()) {
            cur++;
        }
        else {
            curSum += cur;

            // Valid element
            ans.push_back(cur);
            cur++;
        }
    }

    for (int i = 0; i < (int)ans.size(); i++)
        cout << ans[i] << " ";
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 6, 8, 12 };
    int K = 14;

    solve(arr, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.HashMap;

class GFG {

    // Function to find the required elements
    public static void solve(ArrayList<Integer> arr, int K) {

        // Store the elements of arr[]
        HashMap<Integer, Integer> occ = new HashMap<Integer, Integer>();

        for (int i = 0; i < arr.size(); i++) {
            if (occ.containsKey(arr.get(i))) {
                occ.put(arr.get(i), occ.get(arr.get(i)) + 1);
            } else {
                occ.put(arr.get(i), 1);
            }
        }

        // Store the current sum
        int curSum = 0;

        // Start from 1
        int cur = 1;

        // Store the answer
        ArrayList<Integer> ans = new ArrayList<Integer>();

        while (curSum + cur <= K) {

            // Exclude the current element
            if (occ.containsKey(cur)) {
                cur++;
            } else {
                curSum += cur;

                // Valid element
                ans.add(cur);
                cur++;
            }
        }

        for (int i = 0; i < (int) ans.size(); i++)
            System.out.print(ans.get(i) + " ");
    }

    // Driver Code
    public static void main(String args[]) {
        ArrayList<Integer> arr = new ArrayList<Integer>();
        arr.add(4);
        arr.add(6);
        arr.add(8);
        arr.add(12);
        int K = 14;

        solve(arr, K);
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the required elements
def solve(arr, K):

    # Store the elements of arr[]
    occ = {}

    for i in range(len(arr)):
        if (arr[i] in occ):
            occ[arr[i]] += 1
        else:
            occ[arr[i]] = 1

    # Store the current sum
    curSum = 0

    # Start from 1
    cur = 1

    # Store the answer
    ans = []

    while (curSum + cur <= K) :

        # Exclude the current element
        if (cur in occ):
            cur += 1
        else:
            curSum += cur

            # Valid element
            ans.append(cur)
            cur += 1

    for i in range(len(ans)):
        print(ans[i], end=" ")

# Driver Code
arr = [4, 6, 8, 12]
K = 14

solve(arr, K)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG {

    // Function to find the required elements
    public static void solve(List<int> arr, int K) {

        // Store the elements of []arr
        Dictionary<int, int> occ = new Dictionary<int, int>();

        for (int i = 0; i < arr.Count; i++) {
            if (occ.ContainsKey(arr[i])) {
                occ.Add(arr[i], occ[arr[i]] + 1);
            } else {
                occ.Add(arr[i], 1);
            }
        }

        // Store the current sum
        int curSum = 0;

        // Start from 1
        int cur = 1;

        // Store the answer
        List<int> ans = new List<int>();

        while (curSum + cur <= K) {

            // Exclude the current element
            if (occ.ContainsKey(cur)) {
                cur++;
            } else {
                curSum += cur;

                // Valid element
                ans.Add(cur);
                cur++;
            }
        }

        for (int i = 0; i < (int) ans.Count; i++)
            Console.Write(ans[i] + " ");
    }

    // Driver Code
    public static void Main(String []args) {
        List<int> arr = new List<int>();
        arr.Add(4);
        arr.Add(6);
        arr.Add(8);
        arr.Add(12);
        int K = 14;

        solve(arr, K);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach

      // Function to find the required elements
      function solve(arr, K) {

          // Store the elements of arr[]
          let occ = new Map();

          for (let i = 0; i < arr.length; i++) {
              if (occ.has(arr[i])) {
                  occ.set(arr[i], occ.get(arr[i]) + 1)
              }
              else {
                  occ.set(arr[i], 1);
              }
          }

          // Store the current sum
          let curSum = 0;

          // Start from 1
          let cur = 1;

          // Store the answer
          let ans = [];

          while (curSum + cur <= K) {

              // Exclude the current element
              if (occ.has(cur)) {
                  cur++;
              }
              else {
                  curSum += cur;

                  // Valid element
                  ans.push(cur);
                  cur++;
              }
          }

          for (let i = 0; i < ans.length; i++)
              document.write(ans[i] + " ");
      }

      // Driver Code
      let arr = [4, 6, 8, 12];
      let K = 14;

      solve(arr, K);

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
1 2 3 5 
```

***时间复杂度*** : O(N)
***辅助空间*** : O(N)