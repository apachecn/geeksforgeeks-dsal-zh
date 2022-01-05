# 在去除频率不是 2 的幂的字符后，对每个字符串进行排序后，对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-字符串数组-排序后-移除字符后的每个字符串-其频率不是 2 的幂/](https://www.geeksforgeeks.org/sort-array-of-strings-after-sorting-each-string-after-removing-characters-whose-frequencies-are-not-a-powers-of-2/)

给定一个由 **N** 个字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是[在修改每个字符串后，通过移除所有不是](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)[2 的完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)的字符来按升序对数组进行排序，然后按降序对修改后的字符串进行排序。

**示例:**

> **输入:**arr[]= {“aacbb”、“极客”、“AAA”}
> **输出:** cbb skgee
> **解释:**
> 数组中修改后的字符串如下 arr[]:
> 
> 1.  **对于字符串“aacbb”:**a 的频率不是 2 的幂。因此，删除“a”会将字符串修改为“cbb”。现在，按频率递增顺序对字符串“cbb”进行排序会将字符串修改为“cbb”。
> 2.  **对于字符串“极客”:**每个字符的频率是 2 的幂。现在，按照频率递增的顺序对字符串“极客”进行排序会将字符串修改为“skgee”。
> 3.  **对于字符串“AAA”:**a 的频率不是 2 的幂。因此，移除“a”会将字符串修改为“”。
> 
> 因此，按递增顺序对上述字符串进行排序会给出{“cbb”、“skgee”}。
> 
> **输入:**S[]= {“c”、“a”、“b”}
> T3】输出: a b c

**方法:**给定的问题可以通过使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)到[存储每个字符串的所有字符的频率](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)然后执行给定的操作来解决。按照以下步骤解决问题:

*   [遍历给定的字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr[]**，并对每个字符串执行以下操作:
    *   在地图中存储每个字符的[频率。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
    *   创建一个空字符串，比如 **T** ，来存储修改后的字符串。
    *   现在[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并将频率在[T3](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)[2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)次方的字符追加到字符串 **T** 中。
    *   [按照递增顺序](https://www.geeksforgeeks.org/sort-string-characters/)对字符串 **T** 进行排序，并将其添加到字符串数组**RES【】**中。
*   [按照递增顺序](https://www.geeksforgeeks.org/c-program-sort-array-names-strings/)对数组 **res[]** 进行排序。
*   完成以上步骤后，[打印数组中的字符串](https://www.geeksforgeeks.org/print-array-strings-sorted-order-without-copying-one-string-another/) **res[]** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N is power of
// 2 or not
bool isPowerOfTwo(int n)
{
    // Base Case
    if (n == 0)
        return false;

    // Return true if N is power of 2
    return (ceil(log2(n))
            == floor(log2(n)));
}

// Function to print array of strings
// in ascending order
void printArray(vector<string> res)
{
    // Sort strings in ascending order
    sort(res.begin(), res.end());

    // Print the array
    for (int i = 0; i < res.size(); i++) {
        cout << res[i] << " ";
    }
}

// Function to sort the strings after
// modifying each string according to
// the given conditions
void sortedStrings(string S[], int N)
{
    // Store the frequency of each
    // characters of the string
    unordered_map<char, int> freq;

    // Stores the required
    // array of strings
    vector<string> res;

    // Traverse the array of strings
    for (int i = 0; i < N; i++) {

        // Temporary string
        string st = "";

        // Stores frequency of each
        // alphabet of the string
        for (int j = 0;
             j < S[i].size(); j++) {

            // Update frequency of S[i][j]
            freq[S[i][j]]++;
        }

        // Traverse the map freq
        for (auto i : freq) {

            // Check if the frequency
            // of i.first is a power of 2
            if (isPowerOfTwo(i.second)) {

                // Update string st
                for (int j = 0;
                     j < i.second; j++) {
                    st += i.first;
                }
            }
        }

        // Clear the map
        freq.clear();

        // Null string
        if (st.size() == 0)
            continue;

        // Sort the string in
        // descending order
        sort(st.begin(), st.end(),
             greater<char>());

        // Update res
        res.push_back(st);
    }

    // Print the array of strings
    printArray(res);
}

// Driver Code
int main()
{
    string arr[] = { "aaacbb", "geeks", "aaa" };
    int N = sizeof(arr) / sizeof(arr[0]);
    sortedStrings(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if N is power of
// 2 or not
static boolean isPowerOfTwo(int n)
{

    // Base Case
    if (n == 0)
        return false;

    // Return true if N is power of 2
    return (Math.ceil(Math.log(n) / Math.log(2)) ==
           Math.floor(Math.log(n) / Math.log(2)));
}

// Function to print array of strings
// in ascending order
static void printArray(ArrayList<String> res)
{

    // Sort strings in ascending order
    Collections.sort(res);

    // Print the array
    for(int i = 0; i < res.size(); i++)
    {
        System.out.print(res.get(i) + " ");
    }
}

// Function to sort the strings after
// modifying each string according to
// the given conditions
static void sortedStrings(String S[], int N)
{

    // Store the frequency of each
    // characters of the string
    HashMap<Character, Integer> freq = new HashMap<>();

    // Stores the required
    // array of strings
    ArrayList<String> res = new ArrayList<>();

    // Traverse the array of strings
    for(int i = 0; i < N; i++)
    {

        // Temporary string
        String st = "";

        // Stores frequency of each
        // alphabet of the string
        for(int j = 0; j < S[i].length(); j++)
        {

            // Update frequency of S[i][j]
            freq.put(S[i].charAt(j),
                freq.getOrDefault(S[i].charAt(j), 0) + 1);
        }

        // Traverse the map freq
        for(char ch : freq.keySet())
        {

            // Check if the frequency
            // of i.first is a power of 2
            if (isPowerOfTwo(freq.get(ch)))
            {

                // Update string st
                for(int j = 0; j < freq.get(ch); j++)
                {
                    st += ch;
                }
            }
        }

        // Clear the map
        freq.clear();

        // Null string
        if (st.length() == 0)
            continue;

        // Sort the string in
        // descending order
        char myCharArr[] = st.toCharArray();
        Arrays.sort(myCharArr);
        String ns = "";

        for(int j = myCharArr.length - 1; j >= 0; --j)
            ns += myCharArr[j];

        // Update res
        res.add(ns);
    }

    // Print the array of strings
    printArray(res);
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "aaacbb", "geeks", "aaa" };
    int N = arr.length;

    sortedStrings(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict
import math

# Function to check if N is power of
# 2 or not
def isPowerOfTwo(n):

    # Base Case
    if (n == 0):
        return False

    # Return true if N is power of 2
    return (math.ceil(math.log2(n)) ==
            math.floor(math.log2(n)))

# Function to print array of strings
# in ascending order
def printArray(res):

    # Sort strings in ascending order
    res.sort()

    # Print the array
    for i in range(len(res)):
        print(res[i], end = " ")

# Function to sort the strings after
# modifying each string according to
# the given conditions
def sortedStrings(S, N):

    # Store the frequency of each
    # characters of the string
    freq = defaultdict(int)

    # Stores the required
    # array of strings
    res = []

    # Traverse the array of strings
    for i in range(N):

        # Temporary string
        st = ""

        # Stores frequency of each
        # alphabet of the string
        for j in range(len(S[i])):

            # Update frequency of S[i][j]
            freq[S[i][j]] += 1

        # Traverse the map freq
        for i in freq:

            # Check if the frequency
            # of i.first is a power of 2
            if (isPowerOfTwo(freq[i])):

                # Update string st
                for j in range(freq[i]):
                    st += i

        # Clear the map
        freq.clear()

        # Null string
        if (len(st) == 0):
            continue

        # Sort the string in
        # descending order
        st = list(st)
        st.sort(reverse=True)
        st = ''.join(st)

        # Update res
        res.append(st)

    # Print the array of strings
    printArray(res)

# Driver Code
if __name__ == "__main__":

    arr = [ "aaacbb", "geeks", "aaa" ]
    N = len(arr)

    sortedStrings(arr, N)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to check if N is power of
  // 2 or not
  static bool isPowerOfTwo(int n)
  {

    // Base Case
    if (n == 0)
      return false;

    // Return true if N is power of 2
    return (Math.Ceiling(Math.Log(n) / Math.Log(2)) ==
            Math.Floor(Math.Log(n) / Math.Log(2)));
  }

  // Function to print array of strings
  // in ascending order
  static void printArray(List<string> res)
  {

    // Sort strings in ascending order
    (res).Sort();

    // Print the array
    for(int i = 0; i < res.Count; i++)
    {
      Console.Write(res[i] + " ");
    }
  }

  // Function to sort the strings after
  // modifying each string according to
  // the given conditions
  static void sortedStrings(string[] S, int N)
  {

    // Store the frequency of each
    // characters of the string
    Dictionary<char,int> freq = new Dictionary<char,int>();

    // Stores the required
    // array of strings
    List<string> res = new List<string>();

    // Traverse the array of strings
    for(int i = 0; i < N; i++)
    {

      // Temporary string
      string st = "";

      // Stores frequency of each
      // alphabet of the string
      for(int j = 0; j < S[i].Length; j++)
      {

        // Update frequency of S[i][j]
        if(!freq.ContainsKey(S[i][j]))
          freq.Add(S[i][j],0);
        freq[S[i][j]]++;
      }

      // Traverse the map freq
      foreach(KeyValuePair<char, int> ch in freq)
      {

        // Check if the frequency
        // of i.first is a power of 2
        if (isPowerOfTwo(freq[ch.Key]))
        {

          // Update string st
          for(int j = 0; j < freq[ch.Key]; j++)
          {
            st += ch.Key;
          }
        }
      }

      // Clear the map
      freq.Clear();

      // Null string
      if (st.Length == 0)
        continue;

      // Sort the string in
      // descending order
      char[] myCharArr = st.ToCharArray();
      Array.Sort(myCharArr);
      string ns = "";

      for(int j = myCharArr.Length - 1; j >= 0; --j)
        ns += myCharArr[j];

      // Update res
      res.Add(ns);
    }

    // Print the array of strings
    printArray(res);
  }

  // Driver Code

  static public void Main ()
  {

    string[] arr = { "aaacbb", "geeks", "aaa" };
    int N = arr.Length;

    sortedStrings(arr, N);

  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if N is power of
// 2 or not
function isPowerOfTwo(n)
{

    // Base Case
    if (n == 0)
        return false;

    // Return true if N is power of 2
    return (Math.ceil(Math.log(n) / Math.log(2)) ==
           Math.floor(Math.log(n) / Math.log(2)));
}

// Function to print array of strings
// in ascending order
function printArray(res)
{

    // Sort strings in ascending order
    res.sort((a, b) => a - b);

    // Print the array
    for(let i = 0; i < res.length; i++)
    {
        document.write(res[i] + " ");
    }
}

// Function to sort the strings after
// modifying each string according to
// the given conditions
function sortedStrings(s, N)
{

    // Store the frequency of each
    // characters of the string
    let freq = new Map();

    // Stores the required
    // array of strings
    let res = new Array();

    // Traverse the array of strings
    for(let i = 0; i < N; i++)
    {

        // Temporary string
        let st = "";

        // Stores frequency of each
        // alphabet of the string
        for(let j = 0; j < s[i].length; j++)
        {

            // Update frequency of S[i][j]
            if (freq.has(s[i][j]))
            {
                freq.set(s[i][j], freq.get(s[i][j]) + 1)
            }
            else
            {
                freq.set(s[i][j], 1)
            }
        }

        // Traverse the map freq
        for(let ch of freq.keys())
        {

            // Check if the frequency
            // of i.first is a power of 2
            if (isPowerOfTwo(freq.get(ch)))
            {

                // Update string st
                for(let j = 0; j < freq.get(ch); j++)
                {
                    st += ch;
                }
            }
        }

        // Clear the map
        freq.clear();

        // Null string
        if (st.length == 0)
            continue;

        // Sort the string in
        // descending order
        let myCharArr = st.split("");
        myCharArr.sort();
        let ns = "";

        for(let j = myCharArr.length - 1;
                j >= 0; --j)
            ns += myCharArr[j];

        // Update res
        res.push(ns);
    }

    // Print the array of strings
    printArray(res);
}

// Driver Code
let arr = [ "aaacbb", "geeks", "aaa" ];
let N = arr.length;

sortedStrings(arr, N);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
cbb skgee
```

***时间复杂度:** O(N * log N + M * log M)，其中 M 是一个字符串的最大* [*长度*](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/) *在**S【】***
***辅助空间:** O(N)*