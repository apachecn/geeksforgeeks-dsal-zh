# 重新排列一个数字的数字，删除另一个给定数字的任何子序列

> 原文:[https://www . geeksforgeeks . org/重排一个数字的数字以移除另一个给定数字的任何子序列/](https://www.geeksforgeeks.org/rearrange-digits-of-a-number-to-remove-any-subsequence-of-another-given-number/)

给定两个数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **N** 和 **K** (K ≤ N)，其中 **K** 的数字按非递减顺序排列，任务是重新排列 **N** 的数字，使得 **K** 不会作为[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)出现在 **N** 中。如果无法获得这样的排列，打印**-1”**。否则打印任何有效的 **N** 排列。

**示例:**

> **输入:** N = 93039373637，K = 339
> T3】输出: 97093736333
> 
> **输入:** N=965，K = 55
> T3】输出: 965

**天真方法:**最简单的方法是[生成**N**T5】的每个排列，并检查每个排列，](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)[是否 **K** 作为子序列出现在其中](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)。如果发现任何排列为假，打印该排列。
***时间复杂度:** O(N*N！)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于 **K** 的位数为非递减顺序的观察进行优化。因此，通过[排序](https://www.geeksforgeeks.org/sorting-algorithms/)将 **N** 的数字按降序重新排列。按照以下步骤解决问题:

*   [将 **N** 和 **K** 的数字](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)的频率分别存储在[hashmap](https://www.geeksforgeeks.org/hashing-data-structure/)T8】M1 和 **M2** 中。
*   使用一个变量迭代范围**【0，9】**，比如说 **i** ，检查 **K** 是否有出现次数多于 **N** 的数字。如果**M2【I】>M1【I】**，则打印 **N** 返回。
*   再次，使用变量 **i** 迭代范围**【0，9】**，检查 **K** 是否只包含 1 个不同的数字。如果**M2【I】**与**长度(K)** 相同，则打印**-1”**返回。
*   对于所有其他情况，[按照递减顺序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)排序 **N** ，然后打印 **N** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a permutation of
// number N such that the number K does
// not appear as a subsequence in N
void findArrangement(string n, string k)
{

    // Stores frequency of digits of N
    unordered_map<char, int> um1;
    for (int i = 0; i < n.size(); i++) {
        um1[n[i]]++;
    }

    // Stores frequency of digits of K
    unordered_map<char, int> um2;
    for (int i = 0; i < k.size(); i++) {
        um2[k[i]]++;
    }

    // Check if any digit in K has
    // more occurrences than in N
    for (int i = 0; i <= 9; i++) {
        char ch = '0' + i;

        // If true, print N and return
        if (um2[ch] > um1[ch]) {
            cout << n;
            return;
        }
    }

    // Check if K contains only a
    // single distinct digit
    for (int i = 0; i <= 9; i++) {
        char ch = '0' + i;

        // If true, print -1 and return
        if (um2[ch] == k.size()) {
            cout << -1;
            return;
        }
    }

    // For all other cases, sort N
    // in decreasing order
    sort(n.begin(), n.end(),
         greater<char>());

    // Print the value of N
    cout << n;
}

// Driver Code
int main()
{
    string N = "93039373637", K = "339";

    // Function Call
    findArrangement(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find a permutation of
// number N such that the number K does
// not appear as a subsequence in N
static void findArrangement(String n, String k)
{

    // Stores frequency of digits of N
    HashMap<Character,Integer> um1 = new HashMap<Character,Integer>();
    for (int i = 0; i < n.length(); i++)
    {
         if(um1.containsKey(n.charAt(i)))
         {
                um1.put(n.charAt(i), um1.get(n.charAt(i))+1);
            }
            else
            {
                um1.put(n.charAt(i), 1);
            }
    }

    // Stores frequency of digits of K
    HashMap<Character,Integer> um2 = new HashMap<Character,Integer>();
    for (int i = 0; i < k.length(); i++) {
         if(um2.containsKey(k.charAt(i))){
                um2.put(k.charAt(i), um2.get(k.charAt(i))+1);
            }
            else{
                um2.put(k.charAt(i), 1);
            }
    }

    // Check if any digit in K has
    // more occurrences than in N
    for (int i = 0; i <= 9; i++)
    {
        char ch = (char) ('0' + i);

        // If true, print N and return
        if (um2.containsKey(ch) && um1.containsKey(ch)
                && um2.get(ch) > um1.get(ch))
        {
            System.out.print(n);
            return;
        }
    }

    // Check if K contains only a
    // single distinct digit
    for (int i = 0; i <= 9; i++)
    {
        char ch = (char) ('0' + i);

        // If true, print -1 and return
        if (um2.containsKey(ch) && um2.get(ch) == k.length())
        {
            System.out.print(-1);
            return;
        }
    }

    // For all other cases, sort N
    // in decreasing order
    n = sortString(n);

    // Print the value of N
    System.out.print(n);
}
static String sortString(String inputString)
{

    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(new StringBuffer(new String(tempArray)).reverse());
}

// Driver Code
public static void main(String[] args)
{
    String N = "93039373637", K = "339";

    // Function Call
    findArrangement(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a permutation of
# number N such that the number K does
# not appear as a subsequence in N
def findArrangement(n, k) :

    # Stores frequency of digits of N
    um1 = dict.fromkeys(n, 0);

    for i in range(len(n)):
        um1[n[i]] += 1;

    # Stores frequency of digits of K
    um2 = dict.fromkeys(k, 0);

    for i in range(len(k)) :
        um2[k[i]] += 1;

    # Check if any digit in K has
    # more occurrences than in N
    for i in range(10) :
        ch = chr(ord('0') + i);

        if ch in um2 :

            # If true, print N and return
            if (um2[ch] > um1[ch]) :
                print(n, end = "");
                return;

    # Check if K contains only a
    # single distinct digit
    for i in range(10) :
        ch = chr(ord('0') + i);

        if ch in um2 :

            # If true, print -1 and return
            if (um2[ch] == len(k)) :
                print(-1, end = "");
                return;

    # For all other cases, sort N
    # in decreasing order
    n = list(n)
    n.sort(reverse = True)

    # Print the value of N
    print("".join(n));

# Driver Code
if __name__ == "__main__" :

    N = "93039373637"; K = "339";

    # Function Call
    findArrangement(N, K);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find a permutation of
  // number N such that the number K does
  // not appear as a subsequence in N
  static void findArrangement(string n, string k)
  {

    // Stores frequency of digits of N
    Dictionary<char, int> um1 = new Dictionary<char, int>();
    for (int i = 0; i < n.Length; i++)
    {
      if(um1.ContainsKey(n[i]))
      {
        um1[n[i]]++;
      }
      else
      {
        um1[n[i]] = 1;
      }
    }

    // Stores frequency of digits of K
    Dictionary<char, int> um2 = new Dictionary<char, int>();
    for (int i = 0; i < k.Length; i++)
    {
      if(um2.ContainsKey(k[i]))
      {
        um2[k[i]]++;
      }
      else
      {
        um2[k[i]] = 1;
      }
    }

    // Check if any digit in K has
    // more occurrences than in N
    for (int i = 0; i <= 9; i++)
    {
      char ch = (char) ('0' + i);

      // If true, print N and return
      if (um2.ContainsKey(ch) && um1.ContainsKey(ch)
          && um2[ch] > um1[ch])
      {
        Console.Write(n);
        return;
      }
    }

    // Check if K contains only a
    // single distinct digit
    for (int i = 0; i <= 9; i++)
    {
      char ch = (char) ('0' + i);

      // If true, print -1 and return
      if (um2.ContainsKey(ch) && um2[ch] == k.Length)
      {
        Console.Write(-1);
        return;
      }
    }

    // For all other cases, sort N
    // in decreasing order
    n = sortString(n);

    // Print the value of N
    Console.Write(n);
  }

  static string sortString(string inputString)
  {

    // convert input string to char array
    char[] tempArray = inputString.ToCharArray();

    // sort tempArray
    Array.Sort(tempArray);
    Array.Reverse(tempArray);

    // return new sorted string
    return new string(tempArray);
  }

  // Driver codew
  static void Main()
  {
    string N = "93039373637", K = "339";

    // Function Call
    findArrangement(N, K);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach
// Function to find a permutation of
// number N such that the number K does
// not appear as a subsequence in N
function findArrangement(n, k)
{

  // Stores frequency of digits of N
  var um1 = new Map();
  for (var i = 0; i < n.length; i++)
  {
    if(um1.has(n[i]))
    {
      um1.set(n[i], um1.get(n[i])+1);
    }
    else
    {
        um1.set(n[i], 1);
    }
  }

  // Stores frequency of digits of K
  var um2 = new Map();
  for (var i = 0; i < k.length; i++)
  {
    if(um2.has(k[i]))
    {
        um2.set(k[i], um2.get(k[i])+1);
    }
    else
    {
        um2.set(k[i], 1);
    }
  }

  // Check if any digit in K has
  // more occurrences than in N
  for (var i = 0; i <= 9; i++)
  {
    var ch = String.fromCharCode('0'.charCodeAt(0) + i);

    // If true, print N and return
    if (um2.has(ch) && um1.has(ch)
        && um2.get(ch) > um1.get(ch))
    {
      Console.Write(n);
      return;
    }
  }

  // Check if K contains only a
  // single distinct digit
  for (var i = 0; i <= 9; i++)
  {
    var ch =  String.fromCharCode('0'.charCodeAt(0) + i);

    // If true, print -1 and return
    if (um2.has(ch) && um2.get(ch) == k.length)
    {
      document.write(-1);
      return;
    }
  }

  // For all other cases, sort N
  // in decreasing order
  n = sortString(n);

  // Print the value of N
  document.write(n);
}
function sortString(inputString)
{
  // convert input string to char array
  var tempArray = inputString.split('');

  // sort tempArray
  tempArray.sort();
  tempArray.reverse();

  // return new sorted string
  return tempArray.join('');
}

// Driver codew
var N = "93039373637", K = "339";

// Function Call
findArrangement(N, K);

// This code is contributed by itsok.

</script>
```

**Output:** 

```
99776333330
```

***时间复杂度:** O(L*log (L))，其中 L 是字符串 N 的大小*
***辅助空间:** O(L)*