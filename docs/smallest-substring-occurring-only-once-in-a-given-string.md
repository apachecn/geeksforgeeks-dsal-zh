# 在给定字符串中只出现一次的最小子串

> 原文:[https://www . geesforgeks . org/minist-substring-only-in-给定字符串出现一次/](https://www.geeksforgeeks.org/smallest-substring-occurring-only-once-in-a-given-string/)

给定一个由 **N** 个小写字母组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是在 **S** 中找到最小的[子字符串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)的长度，其出现时间正好是**1**。

**示例:**

> **输入:**S = " abaababa "
> T3】输出: 2
> **解释:**
> 字符串 S 中出现次数正好为 1 的最小子串为“aa”。这个子串的长度是 2。
> 因此，打印 2。
> 
> **输入:**S = " zyzyzyz "
> T3】输出: 5

**方法:**解决问题的思路是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **S** 的所有可能的子串，并将每个子串的[频率存储在](https://www.geeksforgeeks.org/frequency-substring-string/) [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中。现在，[遍历 HashMap](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) ，打印最小长度的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)，其频率为 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// substring occurring only once
int smallestSubstring(string a)
{

    // Stores all occurences
    vector<string> a1;

    // Generate all the substrings
    for (int i = 0; i < a.size(); i++)
    {
        for (int j = i + 1; j < a.size(); j++)
        {

            // Avoid multiple occurences
            if (i != j)

                // Append all substrings
                a1.push_back(a.substr(i,j+1));
            }
      }

    // Take into account
    // all the substrings
    map<string,int> a2;
    for(string i:a1) a2[i]++;
    vector<string> freshlist;

    // Iterate over all
    // unique substrings
    for (auto i:a2)
    {

          // If frequency is 1
        if (i.second == 1)

            // Append into fresh list
            freshlist.push_back(i.first);
    }

    // Initialize a dictionary
    map<string,int> dictionary;

    for (auto i:freshlist)
    {
        // Append the keys
        dictionary[i] = i.size();
    }

    vector<int> newlist;

    // Traverse the dictionary
    for (auto i:dictionary)
        newlist.push_back(i.second);
    int ans = INT_MAX;

    for(int i:newlist) ans = min(ans, i);

    // Print the minimum of dictionary
    return ans;
}

// Driver Code
int main()
{
  string S = "ababaabba";
  cout<<smallestSubstring(S);
  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the smallest
// substring occurring only once
static int smallestSubstring(String a)
{

    // Stores all occurences
    ArrayList<String> a1 = new ArrayList<>();

    // Generate all the substrings
    for(int i = 0; i < a.length(); i++)
    {
        for(int j = i + 1; j <= a.length(); j++)
        {

            // Avoid multiple occurences
            if (i != j)

                // Append all substrings
                a1.add(a.substring(i, j));
        }
    }

    // Take into account
    // all the substrings
    TreeMap<String, Integer> a2 = new TreeMap<>();
    for(String s : a1)
        a2.put(s, a2.getOrDefault(s, 0) + 1);

    ArrayList<String> freshlist = new ArrayList<>();

    // Iterate over all
    // unique substrings
    for(String s : a2.keySet())
    {

        // If frequency is 1
        if (a2.get(s) == 1)

            // Append into fresh list
            freshlist.add(s);
    }

    // Initialize a dictionary
    TreeMap<String, Integer> dictionary = new TreeMap<>();

    for(String s : freshlist)
    {

        // Append the keys
        dictionary.put(s, s.length());
    }

    ArrayList<Integer> newlist = new ArrayList<>();

    // Traverse the dictionary
    for(String s : dictionary.keySet())
        newlist.add(dictionary.get(s));

    int ans = Integer.MAX_VALUE;

    for(int i : newlist)
        ans = Math.min(ans, i);

    // Return the minimum of dictionary
    return ans == Integer.MAX_VALUE ? 0 : ans;
}

// Driver Code
public static void main(String[] args)
{
    String S = "ababaabba";

    System.out.println(smallestSubstring(S));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program of the above approach
from collections import Counter

# Function to find the smallest
# substring occurring only once
def smallestSubstring(a):

    # Stores all occurences
    a1 = [] 

    # Generate all the substrings
    for i in range(len(a)):
        for j in range(i+1, len(a)):

            # Avoid multiple occurences
            if i != j: 

                # Append all substrings
                a1.append(a[i:j+1]) 

    # Take into account
    # all the substrings
    a2 = Counter(a1) 
    freshlist = []

    # Iterate over all
    # unique substrings
    for i in a2: 

          # If frequency is 1
        if a2[i] == 1:

            # Append into fresh list
            freshlist.append(i)

    # Initialize a dictionary
    dictionary = dict() 

    for i in range(len(freshlist)):

        # Append the keys
        dictionary[freshlist[i]] = len(freshlist[i]) 

    newlist = []

    # Traverse the dictionary
    for i in dictionary: 
        newlist.append(dictionary[i])

    # Print the minimum of dictionary
    return(min(newlist))

# Driver Code
S = "ababaabba"
print(smallestSubstring(S))
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the smallest
// substring occurring only once
function smallestSubstring(a)
{
    // Stores all occurences
    let a1 = [];

    // Generate all the substrings
    for(let i = 0; i < a.length; i++)
    {
        for(let j = i + 1; j <= a.length; j++)
        {

            // Avoid multiple occurences
            if (i != j)

                // Append all substrings
                a1.push(a.substring(i, j));
        }
    }

    // Take into account
    // all the substrings
    let a2 = new Map();
    for(let s=0;s<a1.length;s++)
    {
        if(a2.has(a1[s]))
            a2.set(a1[s],a2.get(a1[s])+1);
        else
            a2.set(a1[s],1);
    }

    let freshlist = [];

    // Iterate over all
    // unique substrings
    for(let s of a2.keys())
    {

        // If frequency is 1
        if (a2.get(s) == 1)

            // Append into fresh list
            freshlist.push(s);
    }

    // Initialize a dictionary
    let dictionary = new Map();

    for(let s=0;s<freshlist.length;s++)
    {
        // Append the keys
        dictionary.set(freshlist[s],
        freshlist[s].length);
    }

    let newlist = [];

    // Traverse the dictionary
    for(let s of dictionary.keys())
        newlist.push(dictionary.get(s));

    let ans = Number.MAX_VALUE;

    for(let i=0;i<newlist.length;i++)
        ans = Math.min(ans, newlist[i]);

    // Return the minimum of dictionary
    return ans == Number.MAX_VALUE ? 0 : ans;
}

// Driver Code
let S = "ababaabba";
document.write(smallestSubstring(S));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*