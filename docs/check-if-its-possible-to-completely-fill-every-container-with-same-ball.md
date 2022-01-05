# 检查是否有可能用相同的球完全填满每个容器

> 原文:[https://www . geeksforgeeks . org/check-如果可能的话-用同一个球完全填满每个容器/](https://www.geeksforgeeks.org/check-if-its-possible-to-completely-fill-every-container-with-same-ball/)

给定两个[阵列](https://www.geeksforgeeks.org/arrays-in-java/)、**arr【】C**的容器和**arr【】B**的球**、**的任务是找出是否有可能用给定的球完全填满每个容器，如果每个容器只能储存相同类型的球的话。在**阵列 C** 中，**C【I】**存储第 I 个容器可以存储的最大球数。在**数组 B 中，B[i]** 存储第 I 个球的类型。

***例:***

> **输入:** C = [1，2，3]，B = [1，2，2，3，3，4，4]
> **输出:** YES
> **解释:**用 1 号球填充第一个容器，用 2 号球填充第二个容器，用 2 号球填充第三个容器
> 
> **输入:**C =【2】，B =【1，2，3】
> **输出:**否
> **解释:**没有可能的组合来填充容器

***方法:*** 想法是使用 [**回溯**](https://www.geeksforgeeks.org/backtracking-algorithms/) 检查是否有可能填满每个容器。可以观察到，每种球的**频率**只需要一个，所以我们把每种球的**频率**存储在一个**图**中。让我们看看实施我们的方法所涉及的步骤:

*   将同类型球的频率存储在**图中。**
*   调用函数**获取**检查是否可以填充容器。
*   试着用**频率大于等于容器容量**的球填充容器。如果可能的话返回**真**否则**回溯**并检查其他球。
*   如果不存在组合，返回**假**。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// A boolean function that returns true if it's possible to
// completely fill the container else return false
bool getans(int i, vector<int> v, vector<int> q)
{
    // Base Case
    if (i == q.size())
        return true;

    // Backtracking
    for (int j = 0; j < v.size(); j++) {
        if (v[j] >= q[i]) {
            v[j] -= q[i];
            if (getans(i + 1, v, q)) {
                return true;
            }
            v[j] += q[i];
        }
    }
    return false;
}

// Function to check the conditions
void Check(vector<int> c, vector<int> b)
{

    // Storing frequencies
    map<int, int> m;
    for (int i = 0; i < b.size(); i++) {
        m[b[i]]++;
    }
    vector<int> v;
    for (auto i : m) {
        v.push_back(i.second);
    }

    // Function Call for backtracking
    bool check = getans(0, v, c);
    if (check)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

// Driver Code
int main()
{
    // Given Input
    vector<int> c = { 1, 3, 3 };
    vector<int> b = { 2, 2, 2, 2, 4, 4, 4 };

    // Function Call
    Check(c, b);
    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for above approach

# A boolean function that returns true if it's possible to
# completely fill the container else return false
def getans(i, v, q):

    # Base Case
    if (i == len(q)):
        return True

    # Backtracking
    for j in range(len(v)):
        if(v[j] >= q[i]):
            v[j] -= q[i]
            if (getans(i + 1, v, q)):
                return True
            v[j] += q[i]
    return False

# Function to check the conditions
def Check(c, b):

    # Storing frequencies
    m = {}
    for i in range(len(b)):
        if b[i] in m:
            m[b[i]] += 1
        else:
            m[b[i]] = 1
    v = []
    for key,value in m.items():
        v.append(value)

    # Function Call for backtracking
    check = getans(0, v, c)
    if (check):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':

    # Given Input
    c = [1, 3, 3]
    b = [2, 2, 2, 2, 4, 4, 4]

    # Function Call
    Check(c, b)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;
class GFG
{

    // A boolean function that returns true if it's possible
    // to completely fill the container else return false
    static bool getans(int i, List<int> v, int[] q)
    {
        // Base Case
        if (i == q.Length)
            return true;

        // Backtracking
        for (int j = 0; j < v.Count; j++) {
            if (v[j] >= q[i]) {
                v[j] -= q[i];
                if (getans(i + 1, v, q)) {
                    return true;
                }
                v[j] += q[i];
            }
        }
        return false;
    }

    // Function to check the conditions
    static void Check(int[] c, int[] b)
    {

        // Storing frequencies
        Dictionary<int, int> m = new Dictionary<int, int>();
        for (int i = 0; i < b.Length; i++)
            m[b[i]] = 0;
        for (int i = 0; i < b.Length; i++) {
            m[b[i]]++;
        }
        List<int> v = new List<int>();
        foreach(KeyValuePair<int, int> i in m)
        {
            v.Add(i.Value);
        }

        // Function Call for backtracking
        bool check = getans(0, v, c);
        if (check)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }

    // Driver Code
    public static void Main()
    {

        // Given Input
        int[] c = { 1, 3, 3 };
        int[] b = { 2, 2, 2, 2, 4, 4, 4 };

        // Function Call
        Check(c, b);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for above approach

// A boolean function that returns true if it's possible to
// completely fill the container else return false
function getans(i, v, q) {
  // Base Case
  if (i == q.length) return true;

  // Backtracking
  for (let j = 0; j < v.length; j++) {
    if (v[j] >= q[i]) {
      v[j] -= q[i];
      if (getans(i + 1, v, q)) {
        return true;
      }
      v[j] += q[i];
    }
  }
  return false;
}

// Function to check the conditions
function Check(c, b) {
  // Storing frequencies
  let m = new Map();
  for (let i = 0; i < b.length; i++) {
    if (m.has(b[i])) {
      m.set(b[i], m.get(b[i]) + 1);
    } else {
      m.set(b[i], 1);
    }
  }

  let v = [];
  for (i of m) {
    v.push(i[1]);
  }

  // Function Call for backtracking
  let check = getans(0, v, c);
  if (check) document.write("YES");
  else document.write("NO");
}

// Driver Code

// Given Input
let c = [1, 3, 3];
let b = [2, 2, 2, 2, 4, 4, 4];

// Function Call
Check(c, b);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:*** O(m^n)，其中 n 是 arr[ ] C 的大小，m 是 arr[ ] B 的大小.

***辅助空间:*** O(m)