# 给定字符串数组中第 k 个字典上最小的独特字符串

> 原文:[https://www . geeksforgeeks . org/kth-按字典顺序排列-最小-不同-字符串-来自给定的字符串数组/](https://www.geeksforgeeks.org/kth-lexicographically-smallest-distinct-string-from-given-array-of-strings/)

给定一个具有 **N** 字符串和一个整数 **K** 的数组 **arr** ，任务是找到字典上最小的**kt**不同字符串。如果不存在空字符串，则打印该字符串。

**示例:**

> **输入:**arr[]= {“aa”、“aa”、“bb”、“cc”、“dd”、“cc”}，K = 2
> **输出:** dd
> **解释:**不同的字符串是:“bb”、“dd”。其中第二小的字符串是“dd”
> 
> **输入:**arr[]= {“aa”、“aa”、“bb”、“cc”、“dd”、“cc”}，K = 1
> **输出:** bb

**方法:**给定的问题可以通过首先对给定的字符串数组进行排序，然后打印频率为 1 的第 k 个字符串来解决。请按照以下步骤解决此问题:

1.  对给定的字符串数组排序
2.  创建一个映射来存储每个字符串的频率。
3.  现在，遍历地图，每次找到一个频率为 1 的字符串时，减少 K 的值。
4.  当 **K** 变为零时，打印下一个频率为 1 的字符串。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print lexicographically
// smallest Kth string
string KthDistinctString(vector<string>& arr, int K)
{

    // Sorting the array of strings
    sort(arr.begin(), arr.end());

    // Map to store the strings
    map<string, int> mp;
    for (auto x : arr) {
        mp[x]++;
    }

    for (auto x : mp) {

        // Reducing K
        if (x.second == 1) {
            K--;
        }

        if (K == 0 and x.second == 1) {
            return x.first;
        }
    }

    return "";
}

// Driver Code
int main()
{
    vector<string> a
        = { "aa", "aa", "bb", "cc", "dd", "cc" };
    int K = 2;
    cout << KthDistinctString(a, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;

class GFG {

    // Function to print lexicographically
    // smallest Kth string
    static String KthDistinctString(ArrayList<String> arr, int K) {

        // Sorting the array of strings
        Collections.sort(arr);

        // Map to store the strings
        HashMap<String, Integer> mp = new HashMap<String, Integer>();

        for (String x : arr) {
            int count = 0;

            if (mp.containsKey(x)) {
                count = mp.get(x);
            }
            mp.put(x, count + 1);
        }

        for (String x : mp.keySet()) {
            // Reducing K
            if (mp.get(x) == 1) {
                K--;
            }

            if (K == 0 && mp.get(x) == 1) {
                return x;
            }
        }

        return "";
    }

    // Driver Code
    public static void main(String args[]) {
        ArrayList<String> a = new ArrayList<String>();

        a.add("aa");
        a.add("aa");
        a.add("bb");
        a.add("cc");
        a.add("dd");
        a.add("cc");

        int K = 2;
        System.out.println(KthDistinctString(a, K));
    }
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to print lexicographically
# smallest Kth string
def KthDistinctString(arr, K):

    # Sorting the array of strings
    arr.sort()

    # Map to store the strings
    mp = {}
    for x in arr:
        if x in mp:
            mp[x] += 1
        else:
            mp[x] = 1

    for x in mp:

        # Reducing K
        if (mp[x] == 1):
            K -= 1

        if (K == 0 and mp[x] == 1):
            return x

    return ""

# Driver Code
if __name__ == "__main__":

    a = [ "aa", "aa", "bb", "cc", "dd", "cc" ]
    K = 2

    print(KthDistinctString(a, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to print lexicographically
// smallest Kth string
static string KthDistinctString(ArrayList arr, int K)
{

    // Sorting the array of strings
    arr.Sort();

    // Map to store the strings
    Dictionary<string, int> mp =
          new Dictionary<string, int>();

    foreach (string x in arr) {
        int count = 0;

        if (mp.ContainsKey(x)) {
                count = mp[x];
        }
        mp[x] = count + 1;
    }

    foreach (KeyValuePair<string, int> x in mp) {
        // Reducing K
        if (x.Value == 1) {
            K--;
        }

        if (K == 0 && x.Value == 1) {
            return x.Key;
        }
    }

    return "";
}

// Driver Code
public static void Main()
{
    ArrayList a = new ArrayList();

    a.Add("aa");
    a.Add("aa");
    a.Add("bb");
    a.Add("cc");
    a.Add("dd");
    a.Add("cc");

    int K = 2;
    Console.Write(KthDistinctString(a, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to print lexicographically
       // smallest Kth string
       function KthDistinctString(arr, K) {

           // Sorting the array of strings
           arr.sort();

           // Map to store the strings
           let mp = new Map();
           for (let x of arr) {
               if (mp.has(x))
                   mp.set(x, mp.get(x) + 1);
               else
                   mp.set(x, 1);

           }

           for (let [key, value] of mp)
           {

               // Reducing K
               if (value == 1) {
                   K--;
               }

               if (K == 0 && value == 1) {
                   return key;
               }
           }

           return "";
       }

       // Driver Code
       let a
           = ["aa", "aa", "bb", "cc", "dd", "cc"];
       let K = 2;
       document.write(KthDistinctString(a, K));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
dd
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(N)