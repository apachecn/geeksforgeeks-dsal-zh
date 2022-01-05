# 最大一组数字的长度，直到出现 I 或 I/2

> 原文:[https://www . geeksforgeeks . org/最大数字集长度-up-n-这样-要么-i-要么-I-2-存在/](https://www.geeksforgeeks.org/length-of-largest-set-of-numbers-upto-n-such-that-either-i-or-i-2-is-present/)

给定一个正整数 **N** ，任务是找到可以生成的最大集合的长度，使得如果 **i** 存在，那么 **i/2** 将不存在并且 **1 < =i < =N** 。

> **注:**多解，满足条件的任意打印。

**示例:**

> **输入:** N = 2
> **输出:** 1
> **说明:**有两个可能值 1 和 2。如果 2 存在，则 1 不能存在，因为 2/2=1。所以只有可能性是 1 或 2。1 和 2 分别可以是答案。
> 
> **输入:** N = 10
> **输出:** 1 3 4 5 7 9
> **说明:**在输出中，不存在 i/2 存在的 I。

**方法:** [创建一个地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以便于存储和搜索，创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储最终的集合。运行一个从 **1** 到 **N** 的循环(说 **i** )如果 **i** 是奇数，那么将 **i** 添加到答案向量中，并作为地图中的一个键。否则如果 **i** 为偶数，则在地图中搜索 **i/2** 作为关键字。如果地图中没有 **i/2** ，则将 **i** 添加到答案向量中，并作为地图中的一个关键点。按照以下步骤解决问题:

*   [初始化地图< int，bool >](https://www.geeksforgeeks.org/default-values-in-a-map-in-c-stl/) **mp[]。**
*   [初始化向量<int>](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)**ans【】**来存储结果。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   如果 **i** 为奇数，则将 **i** 推入矢量**ans【】**[并将 **{i，1}** 插入地图](https://www.geeksforgeeks.org/map-insert-in-c-stl/) **mp【】。**
    *   否则如果 **i/2** 存在于地图**MP【】**中，那么[将 **i** 推入矢量](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)T8】ans【】并将 **{i，1}** 插入地图 **mp【】。**
*   执行上述步骤后，打印向量**和**的值作为答案。

下面是上述方法的实现。

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the largest set
vector<int> reqsubarray(int& n)
{

    // Initialize the map
    map<int, bool> mp;

    // Vector to store the answer
    vector<int> ans;
    int i;

    // Traverse the range
    for (i = 1; i <= n; i++) {
        if (i & 1) {
            ans.push_back(i);
            mp.insert({ i, 1 });
        }
        else if (mp.find(i / 2) == mp.end()) {
            ans.push_back(i);
            mp.insert({ i, 1 });
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int n = 10, i;

    vector<int> ans;

    ans = reqsubarray(n);

    for (i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.HashMap;

class GFG
{

  // Function to get the largest set
  static ArrayList<Integer> reqsubarray(int n)
  {

    // Initialize the map
    HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

    // Vector to store the answer
    ArrayList<Integer> ans = new ArrayList<Integer>();
    int i;

    // Traverse the range
    for (i = 1; i <= n; i++) {
      if ((i & 1) == 1) {
        ans.add(i);
        mp.put(i, 1);
      }
      else if (!mp.containsKey(i / 2)) {
        ans.add(i);
        mp.put(i, 1);
      }
    }

    // Return the answer
    return ans;
  }

  // Driver Code
  public static void main(String args[])
  {
    int n = 10, i;

    ArrayList<Integer> ans = reqsubarray(n);

    for (i = 0; i < ans.size(); i++)
      System.out.print(ans.get(i) + " ");

  }
}

// This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

  // Function to get the largest set
  static ArrayList reqsubarray(int n)
  {

    // Initialize the map
    Dictionary<int, int> mp =
      new Dictionary<int, int>();

    // Vector to store the answer
    ArrayList ans = new ArrayList();
    int i;

    // Traverse the range
    for (i = 1; i <= n; i++) {
      if ((i & 1) == 1) {
        ans.Add(i);
        mp.Add(i, 1);
      }
      else if (!mp.ContainsKey(i / 2)) {
        ans.Add(i);
        mp.Add(i, 1);
      }
    }

    // Return the answer
    return ans;
  }

  // Driver Code
  public static void Main()
  {
    int n = 10, i;

    ArrayList ans = reqsubarray(n);

    for (i = 0; i < ans.Count; i++)
      Console.Write(ans[i] + " ");

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to get the largest set
       function reqsubarray(n) {

           // Initialize the map
           let mp = new Map();

           // Vector to store the answer
           let ans = [];
           let i;

           // Traverse the range
           for (i = 1; i <= n; i++) {
               if (i & 1) {
                   ans.push(i);
                   mp.set(i, 1);
               }
               else if (!mp.has(Math.floor(i / 2))) {
                   ans.push(i);
                   mp.set(i, 1);
               }
           }

           // Return the answer
           return ans;
       }

       // Driver Code
       let n = 10;
       let ans;
       ans = reqsubarray(n);
       for (let i = 0; i < ans.length; i++)
           document.write(ans[i] + " ");

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
1 3 4 5 7 9 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)