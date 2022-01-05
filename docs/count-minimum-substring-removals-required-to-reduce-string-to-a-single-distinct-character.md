# 计算将字符串简化为单个不同字符所需的最小子字符串删除次数

> 原文:[https://www . geesforgeks . org/count-minimum-substring-removes-required-reduce-string-to-single-distinct-character/](https://www.geeksforgeeks.org/count-minimum-substring-removals-required-to-reduce-string-to-a-single-distinct-character/)

给定一个仅由**【X】****【Y】**和**【Z】**组成的[字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) S，任务是通过选择一个字符并移除不包含该字符的子字符串(最少次数)，将 **S** 转换为仅由单个不同字符组成的字符串。

***注意:**一旦选择了一个角色，就不能在进一步的操作中使用其他角色。*

**示例:**

> **输入:** S = "XXX"
> **输出:** 0
> **解释:**由于给定的字符串已经由单个不同的字符组成，即 X，因此不需要移除。因此，所需的计数为 0。
> 
> **输入:** S = "XYZXYZX"
> **输出:** 2
> **解释:**
> 在两个连续的操作中选择字符‘X’并移除子串“YZ”将字符串简化为“XXX”，该字符串仅由单个不同的字符组成。

**方法:**思路是[使用](https://www.geeksforgeeks.org/java-program-count-occurrences-character/)[无序 _ 贴图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)统计每个角色的出现次数，并统计每个角色需要移除的次数，打印最小值。按照以下步骤解决问题:

*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)并存储每个字符出现的索引。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 的所有字符，并更新字符**【X】【Y】**和**【Z】**在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中的出现次数。
*   [在地图上重复](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/)，对于每个字符，计算每个字符需要移除的次数。
*   计算每个字符后，打印任一字符的最小计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum removals
// required to convert given string
// to single distinct characters only
int minimumOperations(string s, int n)
{

    // Unordered map to store positions
    // of characters X, Y and Z
    unordered_map<char, vector<int> > mp;

    // Update indices of X, Y, Z;
    for (int i = 0; i < n; i++) {
        mp[s[i]].push_back(i);
    }

    // Stores the count of
    // minimum removals
    int ans = INT_MAX;

    // Traverse the Map
    for (auto x : mp) {
        int curr = 0;
        int prev = 0;
        bool first = true;

        // Count the number of removals
        // required for current character
        for (int index : (x.second)) {
            if (first) {
                if (index > 0) {
                    curr++;
                }
                prev = index;
                first = false;
            }
            else {
                if (index != prev + 1) {
                    curr++;
                }
                prev = index;
            }
        }
        if (prev != n - 1) {
            curr++;
        }

        // Update the answer
        ans = min(ans, curr);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given string
    string s = "YYXYZYXYZXY";

    // Size of string
    int N = s.length();

    // Function call
    minimumOperations(s, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to find minimum removals
  // required to convert given string
  // to single distinct characters only
  static void minimumOperations(String s, int n)
  {

    // Unordered map to store positions
    // of characters X, Y and Z
    HashMap<Character, List<Integer>> mp = new HashMap<>();

    // Update indices of X, Y, Z;
    for(int i = 0; i < n; i++)
    {
      if (mp.containsKey(s.charAt(i)))
      {
        mp.get(s.charAt(i)).add(i);
      }
      else
      {
        mp.put(s.charAt(i), new ArrayList<Integer>(Arrays.asList(i)));
      }
    }

    // Stores the count of
    // minimum removals
    int ans = Integer.MAX_VALUE;

    // Traverse the Map
    for (Map.Entry<Character, List<Integer>> x : mp.entrySet())
    {
      int curr = 0;
      int prev = 0;
      boolean first = true;

      // Count the number of removals
      // required for current character
      for(Integer index : (x.getValue()))
      {
        if (first)
        {
          if (index > 0)
          {
            curr++;
          }
          prev = index;
          first = false;
        }
        else
        {
          if (index != prev + 1)
          {
            curr++;
          }
          prev = index;
        }
      }
      if (prev != n - 1)
      {
        curr++;
      }

      // Update the answer
      ans = Math.min(ans, curr);
    }

    // Print the answer
    System.out.print(ans);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given string
    String s = "YYXYZYXYZXY";

    // Size of string
    int N = s.length();

    // Function call
    minimumOperations(s, N);
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys;
INT_MAX = sys.maxsize;

# Function to find minimum removals
# required to convert given string
# to single distinct characters only
def minimumOperations(s, n) :

    # Unordered map to store positions
    # of characters X, Y and Z
    mp = {};

    # Update indices of X, Y, Z;
    for i in range(n) :
        if s[i] in mp :
            mp[s[i]].append(i);
        else :
            mp[s[i]] = [i];

    # Stores the count of
    # minimum removals
    ans = INT_MAX;

    # Traverse the Map
    for x in mp :
        curr = 0;
        prev = 0;
        first = True;

        # Count the number of removals
        # required for current character
        for index in mp[x] :
            if (first) :
                if (index > 0) :
                    curr += 1;
                prev = index;
                first = False;

            else :
                if (index != prev + 1) :
                    curr += 1;
                prev = index;

        if (prev != n - 1) :
            curr += 1;

        # Update the answer
        ans = min(ans, curr);

    # Print the answer
    print(ans);

# Driver Code
if __name__ == "__main__" :

    # Given string
    s = "YYXYZYXYZXY";

    # Size of string
    N = len(s);

    # Function call
    minimumOperations(s, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function to find minimum removals
// required to convert given string
// to single distinct characters only
static void minimumOperations(string s, int n)
{

    // Unordered map to store positions
    // of characters X, Y and Z
    Dictionary<char,
          List<int>> mp = new Dictionary<char,
                                    List<int>>(); 

    // Update indices of X, Y, Z;
    for(int i = 0; i < n; i++)
    {
        if (mp.ContainsKey(s[i]))
        {
            mp[s[i]].Add(i);
        }
        else
        {
            mp[s[i]] = new List<int>();
            mp[s[i]].Add(i);
        }
    }

    // Stores the count of
    // minimum removals
    int ans = Int32.MaxValue;

    // Traverse the Map
    foreach(KeyValuePair<char, List<int>> x in mp)
    {
        int curr = 0;
        int prev = 0;
        bool first = true;

        // Count the number of removals
        // required for current character
        foreach(int index in (x.Value))
        {
            if (first)
            {
                if (index > 0)
                {
                    curr++;
                }
                prev = index;
                first = false;
            }
            else
            {
                if (index != prev + 1)
                {
                    curr++;
                }
                prev = index;
            }
        }
        if (prev != n - 1)
        {
            curr++;
        }

        // Update the answer
        ans = Math.Min(ans, curr);
    }

    // Print the answer
    Console.Write(ans);
}

// Driver Code
static void Main()
{

    // Given string
    string s = "YYXYZYXYZXY";

    // Size of string
    int N = s.Length;

    // Function call
    minimumOperations(s, N);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find minimum removals
      // required to convert given string
      // to single distinct characters only
      function minimumOperations(s, n)
      {

        // Unordered map to store positions
        // of characters X, Y and Z
        var mp = {};

        // Update indices of X, Y, Z;
        for (var i = 0; i < n; i++) {
          if (mp.hasOwnProperty(s[i])) {
            mp[s[i]].push(i);
          } else {
            mp[s[i]] = [];
            mp[s[i]].push(i);
          }
        }

        // Stores the count of
        // minimum removals
        var ans = 2147483647;

        // Traverse the Map
        for (const [key, value] of Object.entries(mp)) {
          var curr = 0;
          var prev = 0;
          var first = true;

          // Count the number of removals
          // required for current character
          for (const index of value) {
            if (first) {
              if (index > 0) {
                curr++;
              }
              prev = index;
              first = false;
            } else {
              if (index !== prev + 1) {
                curr++;
              }
              prev = index;
            }
          }
          if (prev !== n - 1) {
            curr++;
          }

          // Update the answer
          ans = Math.min(ans, curr);
        }

        // Print the answer
        document.write(ans);
      }

      // Driver Code
      // Given string
      var s = "YYXYZYXYZXY";

      // Size of string
      var N = s.length;

      // Function call
      minimumOperations(s, N);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)