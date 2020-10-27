# 字符串在其所有子字符串中的词典等级

给定字符串 **str** ，任务是在字典编排的所有[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)中找到给定字符串的等级。

**示例**：

> **输入**：S =“ enren”
> **输出**：7
> **说明**：
> 排序后所有可能的子字符串均为{“ e”，“ e”，“ en”，“ en”，“ enr”，“ enre”，“ enren”，“ n”，“ n”，“ nr”，“ nre”，“ nren”，“ r” ，“ re”，“ ren”}。
> 因此，给定字符串“ enren”的等级为 7。
> 
> **输入**：S =“怪胎”
> **输出**：12
> **说明**：
> 排序后所有可能的子串均为{“ e ”，“ e”，“ ee”，“ eek”，“ eeks”，“ ek”，“ eks”，“ g”，“ ge”，“ gee”，“ geek”，“ geeks”，“ k”， “ ks”，“ s”}。
> 因此，给定字符串“ geeks”的等级为 12。

**方法**：请按照以下步骤解决问题：

1.  初始化长度为 **26** 的向量的数组 **arr []** ，以将字符串中存在的字符的索引和**等级**的存储为 0。
2.  存储每个字符的索引。 **a** 的索引将存储在 **arr [0]** 中，对于 **b** ， **arr [1]** 将存储其所有索引，因此 上。
3.  遍历[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 中存储的每个索引，直到小于字符串 **S** 的第一个字符的字符。
4.  对于每个索引 **i** ，从该索引开始的总子串为 **N – i** 。 将 **N – i** 添加到**等级**，因为具有这些索引的所有字符都较小。
5.  现在，遍历之后，存储从 **S** 的第一个字符开始的所有子字符串，并按字典顺序对这些子字符串进行排序。
6.  遍历排序的子字符串，并将每个子字符串与字符串 **S** 比较，并增加**等级**，直到找到等于 **S** 的子字符串。
7.  打印 **rank + 1** 的值以获得给定字符串的排名。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find lexiographic rank
// of string among all its substring
int lexiographicRank(string s)
{
    // Length of string
    int n = s.length();

    vector<int> alphaIndex[26];

    // Traverse the given string
    // and store the indices of
    // each character
    for (int i = 0; i < s.length(); i++) {

        // Extract the index
        int x = s[i] - 'a';

        // Store it in the vector
        alphaIndex[x].push_back(i);
    }

    // Traverse the aphaIndex array
    // lesser than the index of first
    // character of given string
    int rank = 0;

    for (int i = 0; i < 26
                    && 'a' + i < s[0];
         i++) {

        // If alphaIndex[i] size exceeds 0
        if (alphaIndex[i].size() > 0) {

            // Traverse over the indices
            for (int j = 0;
                 j < alphaIndex[i].size(); j++) {

                // Add count of substring
                // equal to n - alphaIndex[i][j]
                rank = rank
                       + (n
                          - alphaIndex[i][j]);
            }
        }
    }

    vector<string> str;

    for (int i = 0;
         i < alphaIndex[s[0] - 'a'].size();
         i++) {

        // Store all substrings in a vector
        // str starting with the first
        // character of the given string
        string substring;

        int j = alphaIndex[s[0] - 'a'][i];

        for (; j < n; j++) {

            // Insert the current
            // character to substring
            substring.push_back(s[j]);

            // Store the substring formed
            str.push_back(substring);
        }
    }

    // Sort the substring in the
    // lexicographical order
    sort(str.begin(), str.end());

    // Find the rank of given string
    for (int i = 0; i < str.size(); i++) {

        if (str[i] != s) {

            // increase the rank until
            // the given string is same
            rank++;
        }

        // If substring is same as
        // the given string
        else {
            break;
        }
    }

    // Add 1 to rank of
    // the given string
    return rank + 1;
}

// Driver Code
int main()
{
    // Given string
    string str = "enren";

    // Function Call
    cout << lexiographicRank(str);

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG{

// Function to find lexiographic rank
// of String among all its subString
static int lexiographicRank(char []s)
{
  // Length of String
  int n = s.length;

  Vector<Integer> []alphaIndex = new Vector[26];
  for (int i = 0; i < alphaIndex.length; i++)
    alphaIndex[i] = new Vector<Integer>();

  // Traverse the given String
  // and store the indices of
  // each character
  for (int i = 0; i < s.length; i++) 
  {
    // Extract the index
    int x = s[i] - 'a';

    // Store it in the vector
    alphaIndex[x].add(i);
  }

  // Traverse the aphaIndex array
  // lesser than the index of first
  // character of given String
  int rank = 0;

  for (int i = 0; i < 26 && 
           'a' + i < s[0]; i++) 
  {
    // If alphaIndex[i] size exceeds 0
    if (alphaIndex[i].size() > 0) 
    {
      // Traverse over the indices
      for (int j = 0;
               j < alphaIndex[i].size(); 
               j++) 
      {
        // Add count of subString
        // equal to n - alphaIndex[i][j]
        rank = rank + (n - alphaIndex[i].get(j));
      }
    }
  }

  Vector<String> str = new Vector<String>();

  for (int i = 0;
           i < alphaIndex[s[0] - 'a'].size();
           i++) 
  {
    // Store all subStrings in a vector
    // str starting with the first
    // character of the given String
    String subString = "";

    int j = alphaIndex[s[0] - 'a'].get(i);

    for (; j < n; j++) 
    {
      // Insert the current
      // character to subString
      subString += (s[j]);

      // Store the subString formed
      str.add(subString);
    }
  }

  // Sort the subString in the
  // lexicographical order
  Collections.sort(str);

  // Find the rank of given String
  for (int i = 0; i < str.size(); i++) 
  {
    if (!str.get(i).equals(String.valueOf(s))) 
    {
      // increase the rank until
      // the given String is same
      rank++;
    }

    // If subString is same as
    // the given String
    else
    {
      break;
    }
  }

  // Add 1 to rank of
  // the given String
  return rank + 1;
}

// Driver Code
public static void main(String[] args)
{
  // Given String
  String str = "enren";

  // Function Call
  System.out.print(lexiographicRank(str.toCharArray()));
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program for the above approach

# Function to find lexiographic rank
# of among all its substrring
def lexiographicRank(s):

    # Length of strring
    n = len(s)

    alphaIndex = [[] for i in range(26)]

    # Traverse the given strring
    # and store the indices of
    # each character
    for i in range(len(s)):

        # Extract the index
        x = ord(s[i]) - ord('a')

        # Store it in the vector
        alphaIndex[x].append(i)

    # Traverse the aphaIndex array
    # lesser than the index of first
    # character of given strring
    rank = -1

    for i in range(26):
        if ord('a') + i >= ord(s[0]):
            break

        # If alphaIndex[i] size exceeds 0
        if len(alphaIndex[i]) > 0:

            # T raverse over the indices
            for j in range(len(alphaIndex[i])):

                # Add count of substrring
                # equal to n - alphaIndex[i][j]
                rank = rank + (n - alphaIndex[i][j])

    # print(rank)
    strr = []

    for i in range(len(alphaIndex[ord(s[0]) - ord('a')])):

        # Store all substrrings in a vector
        # strr starting with the first
        # character of the given strring
        substrring = []

        jj = alphaIndex[ord(s[0]) - ord('a')][i]

        for j in range(jj, n):

            # Insert the current
            # character to substrring
            substrring.append(s[j])

            # Store the subformed
            strr.append(substrring)

    # Sort the subin the
    # lexicographical order
    strr = sorted(strr)

    # Find the rank of given strring
    for i in range(len(strr)):
        if (strr[i] != s):

            # Increase the rank until
            # the given is same
            rank += 1

        # If subis same as
        # the given strring
        else:
            break

    # Add 1 to rank of
    # the given strring
    return rank + 1

# Driver Code
if __name__ == '__main__':

    # Given strring
    strr = "enren"

    # Function call
    print(lexiographicRank(strr))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find lexiographic rank
// of String among all its subString
static int lexiographicRank(char []s)
{
  // Length of String
  int n = s.Length;

  List<int> []alphaIndex = new List<int>[26];
  for (int i = 0; i < alphaIndex.Length; i++)
    alphaIndex[i] = new List<int>();

  // Traverse the given String
  // and store the indices of
  // each character
  for (int i = 0; i < s.Length; i++) 
  {
    // Extract the index
    int x = s[i] - 'a';

    // Store it in the vector
    alphaIndex[x].Add(i);
  }

  // Traverse the aphaIndex array
  // lesser than the index of first
  // character of given String
  int rank = 0;

  for (int i = 0; i < 26 && 
           'a' + i < s[0]; i++) 
  {
    // If alphaIndex[i] size exceeds 0
    if (alphaIndex[i].Count > 0) 
    {
      // Traverse over the indices
      for (int j = 0;
               j < alphaIndex[i].Count; j++) 
      {
        // Add count of subString
        // equal to n - alphaIndex[i,j]
        rank = rank + (n - alphaIndex[i][j]);
      }
    }
  }

  List<String> str = new List<String>();

  for (int i = 0;
           i < alphaIndex[s[0] - 'a'].Count; i++) 
  {
    // Store all subStrings in a vector
    // str starting with the first
    // character of the given String
    String subString = "";

    int j = alphaIndex[s[0] - 'a'][i];

    for (; j < n; j++) 
    {
      // Insert the current
      // character to subString
      subString += (s[j]);

      // Store the subString formed
      str.Add(subString);
    }
  }

  // Sort the subString in the
  // lexicographical order
  str.Sort();

  // Find the rank of given String
  for (int i = 0; i < str.Count; i++) 
  {
    if (!str[i].Equals(String.Join("", s))) 
    {
      // increase the rank until
      // the given String is same
      rank++;
    }

    // If subString is same as
    // the given String
    else
    {
      break;
    }
  }

  // Add 1 to rank of
  // the given String
  return rank + 1;
}

// Driver Code
public static void Main(String[] args)
{
  // Given String
  String str = "enren";

  // Function Call
  Console.Write(lexiographicRank(str.ToCharArray()));
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
7

```

***时间复杂度**：O（N <sup>3</sup> ）*
***辅助空间**：O（N）*



* * *

* * *



