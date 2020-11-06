# 包含所有元音的最小子串的长度

> 原文：[https://www.geeksforgeeks.org/length-of-the-smallest-substring-which-contains-all-vowels/](https://www.geeksforgeeks.org/length-of-the-smallest-substring-which-contains-all-vowels/)

给定仅由小写英文字母组成的字符串`str`，任务是找到包含所有元音的最小长度的子字符串。 如果找不到这样的子字符串，请打印 **-1**。

**示例**：

> **输入**：`str = "babeivoucu"`
>
> **输出**：7
>
> **说明**：包含每个元音至少一次的最小子串`"abeivou"`长度为 7
> 
> **输入**：`str = "abcdef"`
>
> **输出**：-1
>
> **说明**：找不到这样的子字符串。

[**两指针方法**](https://www.geeksforgeeks.org/two-pointers-technique/) ：

*   [存储每个元音的频率](https://www.geeksforgeeks.org/print-number-words-vowels-frequency-character/)和存在元音的索引。

*   如果没有所有元音，请直接打印-1。

*   在包含元音的第一个和最后一个索引处取两个指针`i`和`j`。

*   如果在第`i`个和第`j`个索引处的元音频率超过 1，则减少该元音的数量，并分别向左和向右移动`i`和`j`到包含元音的下一个索引。

*   如果在`i`或`j`索引处的元音频率等于 1，则设置`flag1`或`flag2`并继续。

*   一旦设置了`flag1`和`flag2`，就无法进一步最小化子字符串的长度。 两个指针指向的当前索引之间的距离表示结果。

以下代码是上述方法的实现：

## C++

```cpp

// C++ Program to find the
// length of the smallest
// substring of which
// contains all vowels

#include <bits/stdc++.h>
using namespace std;

int findMinLength(string s)
{
    int n = s.size();

    // Map to store the
    // frequency of vowels
    map<char, int> counts;

    // Store the indices
    // which contains
    // the vowels
    vector<int> indices;

    for (int i = 0; i < n; i++) {

        if (s[i] == 'a' || s[i] == 'e'
            || s[i] == 'o'
            || s[i] == 'i'
            || s[i] == 'u') {

            counts[s[i]]++;
            indices.push_back(i);
        }
    }

    // If all vowels are not
    // present in the string
    if (counts.size() < 5)
        return -1;

    int flag1 = 0, flag2 = 0;
    int i = 0;
    int j = indices.size() - 1;

    while ((j - i) >= 4) {

        // If the frequency of the
        // vowel at i-th index
        // exceeds 1
        if (!flag1
            && counts[s[indices[i]]] > 1) {

            // Decrease the frequency
            // of that vowel
            counts[s[indices[i]]]--;

            // Move to the left
            i++;
        }

        // Otherwise set flag1
        else
            flag1 = 1;

        // If the frequency of the
        // vowel at j-th index
        // exceeds 1
        if (!flag2
            && counts[s[indices[j]]] > 1) {

            // Decrease the frequency
            // of that vowel
            counts[s[indices[j]]]--;
            // Move to the right
            j--;
        }

        // Otherwise set flag2
        else
            flag2 = 1;

        // If both flag1 and flag2
        // are set, break out of the
        // loop as the substring
        // length cannot be minimized
        if (flag1 && flag2)
            break;
    }

    // Return the length of the substring
    return (indices[j] - indices[i] + 1);
}

int main()
{

    string s = "aaeebbeaccaaoiuooooooooiuu";
    cout << findMinLength(s);

    return 0;
}

```

## Java

```java

// Java program to find the length of 
// the smallest substring of which
// contains all vowels
import java.util.*; 
class GFG{

public static int findMinLength(String s)
{
    int n = s.length();

    // Map to store the
    // frequency of vowels
    HashMap<Character, 
            Integer> counts = new HashMap<>(); 

    // Store the indices
    // which contains
    // the vowels
    Vector<Integer> indices = new Vector<Integer>();

    for(int i = 0; i < n; i++)
    {
        if (s.charAt(i) == 'a' || 
            s.charAt(i) == 'e' ||
            s.charAt(i) == 'o' ||
            s.charAt(i) == 'i' || 
            s.charAt(i) == 'u')
        {
            if (counts.containsKey(s.charAt(i)))
            {
                counts.replace(s.charAt(i), 
                    counts.get(s.charAt(i)) + 1); 
            }
            else
            {
                counts.put(s.charAt(i), 1);
            }
            indices.add(i);
        }
    }

    // If all vowels are not
    // present in the string
    if (counts.size() < 5)
        return -1;

    int flag1 = 0, flag2 = 0;
    int i = 0;
    int j = indices.size() - 1;

    while ((j - i) >= 4) 
    {

        // If the frequency of the
        // vowel at i-th index
        // exceeds 1
        if (flag1 == 0 && 
            counts.get(s.charAt(
                indices.get(i))) > 1) 
        {

            // Decrease the frequency
            // of that vowel
            counts.replace(s.charAt(indices.get(i)),
                counts.get(s.charAt(indices.get(i))) - 1); 

            // Move to the left
            i++;
        }

        // Otherwise set flag1
        else
            flag1 = 1;

        // If the frequency of the
        // vowel at j-th index
        // exceeds 1
        if (flag2 == 0 && 
            counts.get(s.charAt(
                indices.get(j))) > 1)
        {

            // Decrease the frequency
            // of that vowel
            counts.replace(s.charAt(indices.get(j)), 
                counts.get(s.charAt(indices.get(j))) - 1);

            // Move to the right
            j--;
        }

        // Otherwise set flag2
        else
            flag2 = 1;

        // If both flag1 and flag2
        // are set, break out of the
        // loop as the substring
        // length cannot be minimized
        if (flag1 == 1 && flag2 == 1)
            break;
    }

    // Return the length of the substring
    return (indices.get(j) - indices.get(i) + 1);
}

// Driver Code 
public static void main(String[] args) 
{
    String s = "aaeebbeaccaaoiuooooooooiuu";

    System.out.print(findMinLength(s));
}
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```py

# Python3 program to find the 
# length of the smallest 
# substring of which 
# contains all vowels 
from collections import defaultdict

def findMinLength(s): 

    n = len(s) 

    # Map to store the 
    # frequency of vowels 
    counts = defaultdict(int)

    # Store the indices 
    # which contains 
    # the vowels 
    indices = [] 

    for i in range(n): 

        if (s[i] == 'a' or s[i] == 'e' or
            s[i] == 'o' or s[i] == 'i' or
            s[i] == 'u'): 

            counts[s[i]] += 1
            indices.append(i) 

    # If all vowels are not 
    # present in the string 
    if len(counts) < 5:
        return -1

    flag1 = 0
    flag2 = 0
    i = 0
    j = len(indices) - 1

    while (j - i) >= 4: 

        # If the frequency of the 
        # vowel at i-th index 
        # exceeds 1 
        if (~flag1 and
             counts[s[indices[i]]] > 1): 

            # Decrease the frequency 
            # of that vowel 
            counts[s[indices[i]]] -= 1

            # Move to the left 
            i += 1

        # Otherwise set flag1 
        else:
            flag1 = 1

        # If the frequency of the 
        # vowel at j-th index 
        # exceeds 1 
        if (~flag2 and
             counts[s[indices[j]]] > 1): 

            # Decrease the frequency 
            # of that vowel 
            counts[s[indices[j]]] -= 1

            # Move to the right 
            j -= 1

        # Otherwise set flag2 
        else:
            flag2 = 1

        # If both flag1 and flag2 
        # are set, break out of the 
        # loop as the substring 
        # length cannot be minimized 
        if (flag1 and flag2): 
            break

    # Return the length of the substring 
    return (indices[j] - indices[i] + 1) 

# Driver Code
s = "aaeebbeaccaaoiuooooooooiuu"
print(findMinLength(s)) 

# This code is contributed by
# divyamohan123

```

## C#

```cs

// C# program to find the length of 
// the smallest substring of which
// contains all vowels
using System;
using System.Collections.Generic;
class GFG{

public static int findMinLength(String s)
{
  int n = s.Length;
  int i = 0;

  // Map to store the
  // frequency of vowels
  Dictionary<char,
             int> counts = new Dictionary<char,
                                          int>(); 

  // Store the indices
  // which contains
  // the vowels
  List<int> indices = new List<int>();

  for(i = 0; i < n; i++)
  {
    if (s[i] == 'a' || 
        s[i] == 'e' ||
        s[i] == 'o' ||
        s[i] == 'i' || 
        s[i] == 'u')
    {
      if (counts.ContainsKey(s[i]))
      {
        counts[s[i]] = counts[s[i]] + 1; 
      }
      else
      {
        counts.Add(s[i], 1);
      }
      indices.Add(i);
    }
  }

  // If all vowels are not
  // present in the string
  if (counts.Count < 5)
    return -1;

  int flag1 = 0, flag2 = 0;
  i = 0;
  int j = indices.Count - 1;

  while ((j - i) >= 4) 
  {
    // If the frequency of the
    // vowel at i-th index
    // exceeds 1
    if (flag1 == 0 && 
        counts[s[indices[i]]] > 1) 
    {
      // Decrease the frequency
      // of that vowel
      counts[s[indices[i]]]= 
             counts[s[indices[i]]] - 1; 

      // Move to the left
      i++;
    }

    // Otherwise set flag1
    else
      flag1 = 1;

    // If the frequency of the
    // vowel at j-th index
    // exceeds 1
    if (flag2 == 0 && 
        counts[s[indices[j]]] > 1)
    {
      // Decrease the frequency
      // of that vowel
      counts[s[indices[j]]] = 
             counts[s[indices[j]]] - 1;

      // Move to the right
      j--;
    }

    // Otherwise set flag2
    else
      flag2 = 1;

    // If both flag1 and flag2
    // are set, break out of the
    // loop as the substring
    // length cannot be minimized
    if (flag1 == 1 && flag2 == 1)
      break;
  }

  // Return the length of the substring
  return (indices[j] - indices[i] + 1);
}

// Driver Code 
public static void Main(String[] args) 
{
  String s = "aaeebbeaccaaoiuooooooooiuu";
  Console.Write(findMinLength(s));
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
9

```

**时间复杂度**：*`O(n)`*；

**辅助空间**：*`O(n)`*

[**滑动窗口方法**](https://www.geeksforgeeks.org/window-sliding-technique/) ：

*   保持数组`count`，以存储每个元音的频率。

*   维护`start`变量以存储当前子字符串的起始索引。

*   遍历字符串并执行以下操作：

    *   如果是元音，请增加字符的频率。

    *   根据`start`处的字符不是元音或它是频率大于 1 的元音（这意味着它以前已经出现过）的条件，尽可能向右移动`start`。

    *   一旦将`start`尽可能地移开，请检查在`start`和当前索引之间的子字符串中是否存在所有元音。

    *   每当上述条件满足时，更新获得的此类子字符串的最小长度

*   打印获得的子字符串的最小长度；如果没有获得此子字符串，则打印 -1

以下代码实现了上述方法：

## C++

```cpp

// C++ Program to find the
// length of the smallest
// substring of which
// contains all vowels

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// index for respective
// vowels to increase their count
int get_index(char ch)
{
    if (ch == 'a')
        return 0;
    else if (ch == 'e')
        return 1;
    else if (ch == 'i')
        return 2;
    else if (ch == 'o')
        return 3;
    else if (ch == 'u')
        return 4;

    // Returns -1 for consonants
    else
        return -1;
}

// Function to find the minimum length
int findMinLength(string s)
{
    int n = s.size();
    int ans = n + 1;

    // Store the starting index
    // of the current substring
    int start = 0;

    // Store the frequencies of vowels
    int count[5] = { 0 };

    for (int x = 0; x < n; x++) {

        int idx = get_index(s[x]);

        // If the current character
        // is a vowel
        if (idx != -1) {

            // Increase its count
            count[idx]++;
        }

        // Move start as much
        // right as possible
        int idx_start
            = get_index(s[start]);

        while (idx_start == -1
               || count[idx_start] > 1) {

            if (idx_start != -1) {

                count[idx_start]--;
            }

            start++;
            if (start < n)
                idx_start
                    = get_index(s[start]);
        }

        // Condition for valid substring
        if (count[0] > 0 && count[1] > 0
            && count[2] > 0 && count[3] > 0
            && count[4] > 0) {
            ans = min(ans, x - start + 1);
        }
    }

    if (ans == n + 1)
        return -1;

    return ans;
}

// Driver code
int main()
{
    string s = "aaeebbeaccaaoiuooooooooiuu";
    cout << findMinLength(s);

    return 0;
}

```

## Java

```java

// Java program to find the length 
// of the smallest subString of 
// which contains all vowels
import java.util.*;

class GFG{

// Function to return the
// index for respective
// vowels to increase their count
static int get_index(char ch)
{
    if (ch == 'a')
        return 0;
    else if (ch == 'e')
        return 1;
    else if (ch == 'i')
        return 2;
    else if (ch == 'o')
        return 3;
    else if (ch == 'u')
        return 4;

    // Returns -1 for consonants
    else
        return -1;
}

// Function to find the minimum length
static int findMinLength(String s)
{
    int n = s.length();
    int ans = n + 1;

    // Store the starting index
    // of the current subString
    int start = 0;

    // Store the frequencies of vowels
    int count[] = new int[5];

    for(int x = 0; x < n; x++)
    {
       int idx = get_index(s.charAt(x));

       // If the current character
       // is a vowel
       if (idx != -1)
       {

           // Increase its count
           count[idx]++;
       }

       // Move start as much
       // right as possible
       int idx_start = get_index(s.charAt(start));

       while (idx_start == -1 || 
              count[idx_start] > 1) 
       {
           if (idx_start != -1)
           {
               count[idx_start]--;
           }
           start++;
           if (start < n)
               idx_start = get_index(s.charAt(start));
       }

       // Condition for valid subString
       if (count[0] > 0 && count[1] > 0 && 
           count[2] > 0 && count[3] > 0 && 
           count[4] > 0) 
       {
           ans = Math.min(ans, x - start + 1);
       }
    }
    if (ans == n + 1)
        return -1;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "aaeebbeaccaaoiuooooooooiuu";

    System.out.print(findMinLength(s));
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python3 Program to find the
# length of the smallest
# substring of which
# contains all vowels

# Function to return the
# index for respective
# vowels to increase their count
def get_index(ch):

    if (ch == 'a'):
        return 0
    elif (ch == 'e'):
        return 1
    elif (ch == 'i'):
        return 2
    elif (ch == 'o'):
        return 3
    elif (ch == 'u'):
        return 4

    # Returns -1 for consonants
    else:
        return -1

# Function to find the minimum length
def findMinLength(s):

    n = len(s)
    ans = n + 1

    # Store the starting index
    # of the current substring
    start = 0

    # Store the frequencies 
    # of vowels
    count = [0] * 5

    for x in range (n):

        idx = get_index(s[x])

        # If the current character
        # is a vowel
        if (idx != -1):

            # Increase its count
            count[idx] += 1

        # Move start as much
        # right as possible
        idx_start = get_index(s[start])

        while (idx_start == -1 or
               count[idx_start] > 1):

            if (idx_start != -1):

                count[idx_start] -= 1

            start += 1
            if (start < n):
                idx_start = get_index(s[start])

        # Condition for valid substring
        if (count[0] > 0 and count[1] > 0 and
            count[2] > 0 and count[3] > 0 and
            count[4] > 0):
            ans = min(ans, x - start + 1)

    if (ans == n + 1):
        return -1
    return ans

# Driver code
if __name__ == "__main__":

    s = "aaeebbeaccaaoiuooooooooiuu"
    print(findMinLength(s))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program to find the length 
// of the smallest subString of 
// which contains all vowels
using System;
class GFG{

// Function to return the
// index for respective
// vowels to increase their count
static int get_index(char ch)
{
    if (ch == 'a')
        return 0;
    else if (ch == 'e')
        return 1;
    else if (ch == 'i')
        return 2;
    else if (ch == 'o')
        return 3;
    else if (ch == 'u')
        return 4;

    // Returns -1 for consonants
    else
        return -1;
}

// Function to find the minimum length
static int findMinLength(String s)
{
    int n = s.Length;
    int ans = n + 1;

    // Store the starting index
    // of the current subString
    int start = 0;

    // Store the frequencies of vowels
    int []count = new int[5];

    for(int x = 0; x < n; x++)
    {
        int idx = get_index(s[x]);

        // If the current character
        // is a vowel
        if (idx != -1)
        {

            // Increase its count
            count[idx]++;
        }

        // Move start as much
        // right as possible
        int idx_start = get_index(s[start]);

        while (idx_start == -1 || 
               count[idx_start] > 1) 
        {
            if (idx_start != -1)
            {
                count[idx_start]--;
            }
            start++;
            if (start < n)
                idx_start = get_index(s[start]);
        }

        // Condition for valid subString
        if (count[0] > 0 && count[1] > 0 && 
            count[2] > 0 && count[3] > 0 && 
            count[4] > 0) 
        {
            ans = Math.Min(ans, x - start + 1);
        }
    }
    if (ans == n + 1)
        return -1;

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s = "aaeebbeaccaaoiuooooooooiuu";

    Console.Write(findMinLength(s));
}
}

// This code is contributed by sapnasingh4991

```

**Output:** 

```
9

```

**时间复杂度**：*`O(n)`*



* * *

* * *



