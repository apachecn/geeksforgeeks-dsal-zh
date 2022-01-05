# 检查一个字符串是否可以转换成另一个

> 原文:[https://www . geesforgeks . org/check-如果一个字符串可以转换为另一个字符串/](https://www.geeksforgeeks.org/check-if-one-string-can-be-converted-to-another/)

给定两个字符串 **str** 和 **str1** ，任务是使用以下操作检查一个字符串是否可以转换为其他字符串:

*   将一个字符的所有显示转换为另一个字符。

例如，如果 str = "abacd "和操作是将字符' a '更改为' k '，则结果 str = "kbkcd"
**示例:**

> **输入:**str = " abb CAA "；str1 = "bccdbb"
> **输出:**是
> **说明:**字符的映射为:
> c–>d
> b–>c
> a–>b
> **输入:**str = " abbc "；str1 = "bcca"
> **输出:**否
> **说明:**字符的映射为:
> a–>b
> b–>c
> c–>a
> 这里由于存在一个循环，所以找不到具体的顺序。

**进场:**

*   根据给定的操作，每个唯一字符应该映射到一个可能相同或不同的唯一字符。
*   这可以通过[哈希表](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)轻松检查。
*   但是，在映射中存在循环并且无法确定特定顺序的情况下，这种方法会失败。
*   这种情况的一个例子是上面的*例子 2* 。
*   因此，对于映射，第一个和最后一个字符作为边存储在散列表中。
*   为了寻找具有边的循环，这些边被一个接一个地映射到父边，并使用[联合和寻找算法](https://www.geeksforgeeks.org/union-find/)检查循环。

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;
int parent[26];
// Function for find
// from Disjoint set algorithm
int find(int x)
{
    if (x != parent[x])
        return parent[x] = find(parent[x]);
    return x;
}

// Function for the union
// from Disjoint set algorithm
void join(int x, int y)
{
    int px = find(x);
    int pz = find(y);
    if (px != pz) {
        parent[pz] = px;
    }
}
// Function to check if one string
// can be converted to another.
bool convertible(string s1, string s2)
{
    // All the characters are checked whether
    // it's either not replaced or replaced
    // by a similar character using a map.
    map<int, int> mp;

    for (int i = 0; i < s1.size(); i++) {
        if (mp.find(s1[i] - 'a') == mp.end()) {
            mp[s1[i] - 'a'] = s2[i] - 'a';
        }
        else {
            if (mp[s1[i] - 'a'] != s2[i] - 'a')
                return false;
        }
    }
    // To check if there are cycles.
    // If yes, then they are not convertible.
    // Else, they are convertible.
    for (auto it : mp) {
        if (it.first == it.second)
            continue;
        else {
            if (find(it.first) == find(it.second))
                return false;
            else
                join(it.first, it.second);
        }
    }
    return true;
}

// Function to initialize parent array
// for union and find algorithm.
void initialize()
{
    for (int i = 0; i < 26; i++) {
        parent[i] = i;
    }
}
// Driver code
int main()
{
    // Your C++ Code
    string s1, s2;
    s1 = "abbcaa";
    s2 = "bccdbb";
    initialize();
    if (convertible(s1, s2))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
import java.util.*;

class GFG
{

static int []parent = new int[26];

// Function for find
// from Disjoint set algorithm
static int find(int x)
{
    if (x != parent[x])
        return parent[x] = find(parent[x]);
    return x;
}

// Function for the union
// from Disjoint set algorithm
static void join(int x, int y)
{
    int px = find(x);
    int pz = find(y);
    if (px != pz)
    {
        parent[pz] = px;
    }
}
// Function to check if one String
// can be converted to another.
static boolean convertible(String s1, String s2)
{
    // All the characters are checked whether
    // it's either not replaced or replaced
    // by a similar character using a map.
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    for (int i = 0; i < s1.length(); i++)
    {
        if (!mp.containsKey(s1.charAt(i) - 'a'))
        {
            mp.put(s1.charAt(i) - 'a', s2.charAt(i) - 'a');
        }
        else
        {
            if (mp.get(s1.charAt(i) - 'a') != s2.charAt(i) - 'a')
                return false;
        }
    }

    // To check if there are cycles.
    // If yes, then they are not convertible.
    // Else, they are convertible.
    for (Map.Entry<Integer, Integer> it : mp.entrySet())
    {
        if (it.getKey() == it.getValue())
            continue;
        else
        {
            if (find(it.getKey()) == find(it.getValue()))
                return false;
            else
                join(it.getKey(), it.getValue());
        }
    }
    return true;
}

// Function to initialize parent array
// for union and find algorithm.
static void initialize()
{
    for (int i = 0; i < 26; i++)
    {
        parent[i] = i;
    }
}

// Driver code
public static void main(String[] args)
{

    String s1, s2;
    s1 = "abbcaa";
    s2 = "bccdbb";
    initialize();
    if (convertible(s1, s2))
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.
parent = [0] * 256

# Function for find
# from Disjoset algorithm
def find(x):
    if (x != parent[x]):
        parent[x] = find(parent[x])
        return parent[x]
    return x

# Function for the union
# from Disjoset algorithm
def join(x, y):
    px = find(x)
    pz = find(y)
    if (px != pz):
        parent[pz] = px

# Function to check if one string
# can be converted to another.
def convertible(s1, s2):

    # All the characters are checked whether
    # it's either not replaced or replaced
    # by a similar character using a map.
    mp = dict()

    for i in range(len(s1)):
        if (s1[i] in mp):
            mp[s1[i]] = s2[i]
        else:
            if s1[i] in mp and mp[s1[i]] != s2[i]:
                return False

    # To check if there are cycles.
    # If yes, then they are not convertible.
    # Else, they are convertible.
    for it in mp:
        if (it == mp[it]):
            continue
        else :
            if (find(ord(it)) == find(ord(it))):
                return False
            else:
                join(ord(it), ord(it))

    return True

# Function to initialize parent array
# for union and find algorithm.
def initialize():
    for i in range(256):
        parent[i] = i

# Driver code
s1 = "abbcaa"
s2 = "bccdbb"
initialize()
if (convertible(s1, s2)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach.
using System;
using System.Collections.Generic;

class GFG
{

static int []parent = new int[26];

// Function for find
// from Disjoint set algorithm
static int find(int x)
{
    if (x != parent[x])
        return parent[x] = find(parent[x]);
    return x;
}

// Function for the union
// from Disjoint set algorithm
static void join(int x, int y)
{
    int px = find(x);
    int pz = find(y);
    if (px != pz)
    {
        parent[pz] = px;
    }
}

// Function to check if one String
// can be converted to another.
static bool convertible(String s1, String s2)
{
    // All the characters are checked whether
    // it's either not replaced or replaced
    // by a similar character using a map.
    Dictionary<int,int> mp = new Dictionary<int,int>();

    for (int i = 0; i < s1.Length; i++)
    {
        if (!mp.ContainsKey(s1[i] - 'a'))
        {
            mp.Add(s1[i] - 'a', s2[i] - 'a');
        }
        else
        {
            if (mp[s1[i] - 'a'] != s2[i] - 'a')
                return false;
        }
    }

    // To check if there are cycles.
    // If yes, then they are not convertible.
    // Else, they are convertible.
    foreach(KeyValuePair<int, int> it in mp)
    {
        if (it.Key == it.Value)
            continue;
        else
        {
            if (find(it.Key) == find(it.Value))
                return false;
            else
                join(it.Key, it.Value);
        }
    }
    return true;
}

// Function to initialize parent array
// for union and find algorithm.
static void initialize()
{
    for (int i = 0; i < 26; i++)
    {
        parent[i] = i;
    }
}

// Driver code
public static void Main(String[] args)
{

    String s1, s2;
    s1 = "abbcaa";
    s2 = "bccdbb";
    initialize();
    if (convertible(s1, s2))
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

      // JavaScript implementation of the above approach.
      var parent = new Array(26).fill(0);

      // Function for find
      // from Disjoint set algorithm
      function find(x) {
        if (x !== parent[x]) return (parent[x] = find(parent[x]));
        return x;
      }

      // Function for the union
      // from Disjoint set algorithm
      function join(x, y) {
        var px = find(x);
        var pz = find(y);
        if (px !== pz) {
          parent[pz] = px;
        }
      }

      // Function to check if one String
      // can be converted to another.
      function convertible(s1, s2) {
        // All the characters are checked whether
        // it's either not replaced or replaced
        // by a similar character using a map.
        var mp = {};

        for (var i = 0; i < s1.length; i++) {
          if (!mp.hasOwnProperty(s1[i].charCodeAt(0) -
          "a".charCodeAt(0)))
          {
            mp[s1[i].charCodeAt(0) - "a".charCodeAt(0)] =
              s2[i].charCodeAt(0) - "a".charCodeAt(0);
          } else {
            if (
              mp[s1[i].charCodeAt(0) - "a".charCodeAt(0)] !==
              s2[i].charCodeAt(0) - "a".charCodeAt(0)
            )
              return false;
          }
        }

        // To check if there are cycles.
        // If yes, then they are not convertible.
        // Else, they are convertible.
        for (const [key, value] of Object.entries(mp)) {
          if (key === value) continue;
          else {
            if (find(key) == find(value)) return false;
            else join(key, value);
          }
        }
        return true;
      }

      // Function to initialize parent array
      // for union and find algorithm.
      function initialize() {
        for (var i = 0; i < 26; i++) {
          parent[i] = i;
        }
      }

      // Driver code
      var s1, s2;
      s1 = "abbcaa";
      s2 = "bccdbb";
      initialize();
      if (convertible(s1, s2)) document.write("Yes" + "<br>");
      else document.write("No" + "<br>");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N * logN)，其中 N 为字符串 s1 的长度。
**辅助空间:** O(N)