# 检查一个字符串中最多两次交换后，两个非重复字符串是否可以相等

> 原文:[https://www . geesforgeks . org/check-if-two-非重复字符串-最多两个字符串交换后可以相等/](https://www.geeksforgeeks.org/check-if-two-non-duplicate-strings-can-be-made-equal-after-at-most-two-swaps-in-one-string/)

给定由唯一小写字母组成的两个字符串 **A** 和 **B** ，任务是通过最多使用两次互换来检查这两个字符串是否可以相等。打印**是的**如果可以的话。否则，打印**否**。

**示例:**

> **输入:**A =“ABCD”，B =“badc”
> **输出:**是
> 先交换 A 和 B，再交换 c 和 d，在字符串 A 中.
> **输入:**A =“ABCD”，B =“cbda”
> **输出:**否

**方法:**在这个问题中，字符串 **A** 只能转换为字符串 **B** 如果:

> **情况 1:** 如果 **A** 已经等于 **B** 。
> **情况 2:** 如果两个字符串的差异数小于或等于 3，并且两个字符串包含相同的字符。那么总是有可能从 **A** 创建 **B** 。
> **情况 3:** 如果差异数为 4，且串 **A** 中的所有对换对在串 **B** 中相同且相反。

现在要解决这个问题，请按照以下步骤操作:

1.  首先，检查两个字符串是否已经相等。如果是，则打印**是**。
2.  另外，检查两个字符串的大小是否相等。如果不是，则打印**否**。
3.  创建一个向量，说 **b** 并将字符的索引存储在字符串 **B** 中。
4.  创建两个地图，停留 **mp1** 和 **mp2** 分别存储字符串 **A** 和 **B** 中的字符频率。
5.  现在，检查差异数是否小于或等于 **3** ，并且两个地图， **mp1** 和 **mp2** 具有相同的条目。如果是，那么两个字符串可以相等。所以，打印是。
6.  此外，如果两个字符串有 **4** 的差异，但如果是一对两个镜像错误，则可以使它们相等。因此，如果差异成对反映，打印**是**。
7.  否则最后打印**否**。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if two strings can be made
// equal using at most two swaps
bool canBecomeEqual(string A, string B)
{

    if (A.size() != B.size()) {
        return 0;
    }

    // Case 1:
    if (A == B) {
        return 1;
    }

    // Vector to store the index of characters
    // in B
    vector<int> b(26, -1);

    for (int i = 0; i < A.size(); i++) {
        b[B[i] - 'a'] = i;
    }

    // Map to store the characters
    // with their frequencies
    unordered_map<char, int> mp1, mp2;

    // Variable to store
    // the total number of differences
    int diff = 0;

    // Set to store the the pair of indexes
    // having changes in A wrt to B
    set<pair<int, int> > positions;

    for (int i = 0; i < A.size(); ++i) {
        if (A[i] != B[i]) {
            positions.insert({ i, b[A[i] - 'a'] });
            diff++;
        }
        mp1[A[i]]++;
        mp2[B[i]]++;
    }

    // Case 2:
    if (diff <= 3 and mp1 == mp2) {
        return 1;
    }

    // Case 3:
    if (diff == 4 and mp1 == mp2) {
        for (auto x : positions) {
            pair<int, int> search
                = { x.second, x.first };

            if (positions.find(search)
                == positions.end()) {
                return 0;
            }
        }
        return 1;
    }

    return 0;
}

// Driver Code
int main()
{
    string A = "abcd";
    string B = "cdba";

    if (canBecomeEqual(A, B)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }
        @Override
        public int hashCode() {
            final int prime = 31;
            int result = 1;
            result = prime * result + first;
            result = prime * result + second;
            return result;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj)
                return true;
            if (obj == null)
                return false;
            if (getClass() != obj.getClass())
                return false;
            pair other = (pair) obj;
            if (first != other.first)
                return false;
            if (second != other.second)
                return false;
            return true;
        }   

    }

// Function to check if two Strings can be made
// equal using at most two swaps
static boolean canBecomeEqual(String A, String B)
{

    if (A.length() != B.length()) {
        return false;
    }

    // Case 1:
    if (A == B) {
        return true;
    }

    // Vector to store the index of characters
    // in B
    int []b = new int[26];

    for (int i = 0; i < A.length(); i++) {
        b[B.charAt(i) - 'a'] = i;
    }

    // Map to store the characters
    // with their frequencies
    HashMap<Character,Integer> mp1, mp2;
    mp1 = new HashMap<Character,Integer>();
    mp2 = new HashMap<Character,Integer>();

    // Variable to store
    // the total number of differences
    int diff = 0;

    // Set to store the the pair of indexes
    // having changes in A wrt to B
    HashSet<pair> positions = new HashSet<pair>();

    for (int i = 0; i < A.length(); ++i) {
        if (A.charAt(i) != B.charAt(i)) {
            positions.add(new pair(i, b[A.charAt(i) - 'a'] ));
            diff++;
        }
        if(mp1.containsKey(A.charAt(i))){
            mp1.put(A.charAt(i), mp1.get(A.charAt(i))+1);
        }
        else{
            mp1.put(A.charAt(i), 1);
        }
        if(mp2.containsKey(B.charAt(i))){
            mp2.put(B.charAt(i), mp2.get(B.charAt(i))+1);
        }
        else{
            mp2.put(B.charAt(i), 1);
        }
    }

    // Case 2:
    if (diff <= 3 && mp1 == mp2) {
        return true;
    }

    // Case 3:
    if (diff == 4 && mp1 == mp2) {
        for (pair x : positions) {
            pair search
                = new pair( x.second, x.first );

            if (!positions.contains(search)) {
                return false;
            }
        }
        return true;
    }

    return false;
}

// Driver Code
public static void main(String[] args)
{
    String A = "abcd";
    String B = "cdba";

    if (canBecomeEqual(A, B)) {
        System.out.print("Yes" +"\n");
    }
    else {
        System.out.print("No" +"\n");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python3 code for the above approach

# Function to check if two strings can be made
# equal using at most two swaps
def canBecomeEqual(A, B):

    if (len(A) != len(B)):
        return 0

        # Case 1:
    if (A == B):
        return 1

        # Vector to store the index of characters
        # in B
    b = [-1 for _ in range(26)]

    for i in range(0, len(A)):
        b[ord(B[i]) - ord('a')] = i

        # Map to store the characters
        # with their frequencies
    mp1 = {}
    mp2 = {}

    # Variable to store
    # the total number of differences
    diff = 0

    # Set to store the the pair of indexes
    # having changes in A wrt to B
    positions = set()

    for i in range(0, len(A)):
        if (A[i] != B[i]):
            positions.add((i, b[ord(A[i]) - ord('a')]))
            diff += 1
        if A[i] in mp1:
            mp1[A[i]] += 1
        else:
            mp1[A[i]] = 1

        if B[i] in mp2:
            mp2[B[i]] += 1
        else:
            mp2[B[i]] = 1

        # Case 2:
    if (diff <= 3 and mp1 == mp2):
        return 1

        # Case 3:
    if (diff == 4 and mp1 == mp2):
        for x in positions:
            search = (x[1], x[0])
            if (not (search in positions)):
                return 0

        return 1

    return 0

# Driver Code
if __name__ == "__main__":

    A = "abcd"
    B = "cdba"

    if (canBecomeEqual(A, B)):
        print("Yes")

    else:
        print("No")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

public class GFG{
  class pair : IComparable<pair>
  {
    public int first, second;
    public pair(int first, int second)
    {
      this.first = first;
      this.second = second;
    }
    public int CompareTo(pair p)
    {
      return this.second-p.first;
    }
  }

  // Function to check if two Strings can be made
  // equal using at most two swaps
  static bool canBecomeEqual(String A, String B)
  {

    if (A.Length != B.Length) {
      return false;
    }

    // Case 1:
    if (A == B) {
      return true;
    }

    // List to store the index of characters
    // in B
    int []b = new int[26];

    for (int i = 0; i < A.Length; i++) {
      b[B[i] - 'a'] = i;
    }

    // Map to store the characters
    // with their frequencies
    Dictionary<char,int> mp1, mp2;
    mp1 = new Dictionary<char,int>();
    mp2 = new Dictionary<char,int>();

    // Variable to store
    // the total number of differences
    int diff = 0;

    // Set to store the the pair of indexes
    // having changes in A wrt to B
    HashSet<pair> positions = new HashSet<pair>();

    for (int i = 0; i < A.Length; ++i) {
      if (A[i] != B[i]) {
        positions.Add(new pair(i, b[A[i] - 'a'] ));
        diff++;
      }
      if(mp1.ContainsKey(A[i])){
        mp1[A[i]] = mp1[A[i]]+1;
      }
      else{
        mp1.Add(A[i], 1);
      }
      if(mp2.ContainsKey(B[i])){
        mp2[B[i]] = mp2[B[i]]+1;
      }
      else{
        mp2.Add(B[i], 1);
      }
    }

    // Case 2:
    if (diff <= 3 && mp1 == mp2) {
      return true;
    }

    // Case 3:
    if (diff == 4 && mp1 == mp2) {
      foreach (pair x in positions) {
        pair search
          = new pair( x.second, x.first );

        if (!positions.Contains(search)) {
          return false;
        }
      }
      return true;
    }

    return false;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String A = "abcd";
    String B = "cdba";

    if (canBecomeEqual(A, B)) {
      Console.Write("Yes" +"\n");
    }
    else {
      Console.Write("No" +"\n");
    }
  }
}

// This code is contributed by shikhasingrajput
```

**Output**

```
No
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)