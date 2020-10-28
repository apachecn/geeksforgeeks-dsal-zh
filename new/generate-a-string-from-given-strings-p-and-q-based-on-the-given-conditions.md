# 根据给定的条件从给定的字符串 P 和 Q 生成一个字符串

给定两个字符串 **P** 和 **Q，**，任务是生成满足以下条件的字符串 **S** ：

*   找到 **S** ，以便重新排列 **P** ，并且 **Q** 是其中的子串。

*   **S** 中 **Q** 之前的所有字符均应小于或等于 **Q** 中的第一个字符，并按词典顺序排列。

*   其余字符应按字典顺序出现在 **Q** 之后

**注意**：Q 的所有字符始终存在于 P 中，并且 Q 的长度始终小于或等于 P 的长度。

**示例**：

> **输入**：P =“ geeksforgeeksfor” Q =“用于”
> **输出**：eeeefforggkkorss
> **说明**：
> 字符'e'和 “ f”是这里唯一小于或等于“ f”（Q 的第一个字符）的字符。
> 因此，在“ for”之前，字符串在字典上等于 eeeef。
> P 中的其余字符大于“ f”，因​​此按字典顺序放在“ for”之后。
> 因此，在“ for”之后，字符串是 ggkkorss。
> 因此，输出为 eeeefforggkkorss。
> 
> **输入**：P =“字典式” Q =“间隙”
> **输出**：accegaphiillorx
> **说明**：
> 字符串 accegaphiillorx 满足上述要求 字符串 P 和 Q 的条件。

**方法**：的想法是找到 P 和 Q 中所有字符的[**频率**](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) 以解决问题。

*   维持 P 和 Q 中所有字母的频率数组。

*   找到频率后，根据 Q 中的第一个字符分隔 P 中的字符，并将它们添加到结果字符串中。

*   最后返回结果字符串。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate a string S from string P
// and Q according to the given conditions
void manipulateStrings(string P, string Q)
{

    // Stores the frequencies
    int freq[26];
    memset(freq, 0, sizeof(freq));

    // Counts occurrences of each characters
    for(int i = 0; i < P.size(); i++)
    {
        freq[P[i] - 'a']++;
    }

    // Reduce the count of the character
    // which is also present in Q
    for(int i = 0; i < Q.size(); i++)
    {
        freq[Q[i] - 'a']--;
    }

    // Stores the resultant string
    string sb = "";

    // Index in freq[] to segregate the string
    int pos = Q[0] - 'a';

    for(int i = 0; i <= pos; i++)
    {
        while (freq[i] > 0)
        {
            char c = (char)('a' + i);
            sb += c;
            freq[i]--;
        }
    }

    // Add Q to the resulting string
    sb += Q;

    for(int i = pos + 1; i < 26; i++)
    {
        while (freq[i] > 0)
        {
            char c = (char)('a' + i);
            sb += c;
            freq[i]--;
        }
    }

    cout << sb << endl;
}

// Driver Code
int main()
{
    string P = "geeksforgeeksfor";
    string Q = "for";

    // Function call
    manipulateStrings(P, Q);
}

// This code is contributed by Amit Katiyar

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // Function to generate a string S from string P
    // and Q according to the given conditions
    public static void manipulateStrings(String P,
                                         String Q)
    {

        // Stores the frequencies
        int[] freq = new int[26];

        // Counts occurrences of each characters
        for (int i = 0; i < P.length(); i++) {
            freq[P.charAt(i) - 'a']++;
        }

        // Reduce the count of the character
        // which is also present in Q
        for (int i = 0; i < Q.length(); i++) {
            freq[Q.charAt(i) - 'a']--;
        }

        // Stores the resultant string
        StringBuilder sb
            = new StringBuilder();

        // Index in freq[] to segregate the string
        int pos = Q.charAt(0) - 'a';

        for (int i = 0; i <= pos; i++) {
            while (freq[i] > 0) {
                char c = (char)('a' + i);
                sb.append(c);
                freq[i]--;
            }
        }

        // Add Q to the resulting string
        sb.append(Q);

        for (int i = pos + 1; i < 26; i++) {
            while (freq[i] > 0) {
                char c = (char)('a' + i);
                sb.append(c);
                freq[i]--;
            }
        }

        System.out.println(sb);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String P = "geeksforgeeksfor";
        String Q = "for";
        // Function call
        manipulateStrings(P, Q);
    }
}

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to generate a string S 
# from string P and Q according to 
# the given conditions
def manipulateStrings(P, Q):

    # Stores the frequencies
    freq = [0 for i in range(26)];

    # Counts occurrences of each characters
    for i in range(len(P)):
        freq[ord(P[i]) - ord('a')] += 1

    # Reduce the count of the character
    # which is also present in Q
    for i in range(len(Q)):
        freq[ord(Q[i]) - ord('a')] -= 1

    # Stores the resultant string
    sb = ""

    # Index in freq[] to segregate the string
    pos = ord(Q[0]) - ord('a')

    for i in range(pos + 1):
        while freq[i] > 0:
            sb += chr(ord('a') + i)
            freq[i] -= 1

    # Add Q to the resulting string
    sb += Q

    for i in range(pos + 1, 26):
        while freq[i] > 0:
            sb += chr(ord('a') + i)
            freq[i] -= 1

    print(sb)

# Driver Code 
if __name__=="__main__":

    P = "geeksforgeeksfor";
    Q = "for";

    # Function call
    manipulateStrings(P, Q);

# This code is contributed by rutvik_56

```

## C#

```cs

// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to generate a string S from string P
  // and Q according to the given conditions
  public static void manipulateStrings(String P,
                                       String Q)
  {

    // Stores the frequencies
    int[] freq = new int[26];

    // Counts occurrences of each characters
    for (int i = 0; i < P.Length; i++) 
    {
      freq[P[i] - 'a']++;
    }

    // Reduce the count of the character
    // which is also present in Q
    for (int i = 0; i < Q.Length; i++)
    {
      freq[Q[i] - 'a']--;
    }

    // Stores the resultant string
    String sb = "";

    // Index in []freq to segregate the string
    int pos = Q[0] - 'a';

    for (int i = 0; i <= pos; i++) 
    {
      while (freq[i] > 0)
      {
        char c = (char)('a' + i);
        sb += c;
        freq[i]--;
      }
    }

    // Add Q to the resulting string
    sb += Q;

    for (int i = pos + 1; i < 26; i++)
    {
      while (freq[i] > 0) 
      {
        char c = (char)('a' + i);
        sb += c;
        freq[i]--;
      }
    }
    Console.WriteLine(sb);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String P = "geeksforgeeksfor";
    String Q = "for";

    // Function call
    manipulateStrings(P, Q);
  }
}

// This code is contributed by Rohit_ranjan

```

**Output:** 

```
eeeefforggkkorss

```

***时间复杂度**：O（N + M），其中 N 和 M 分别是 P 和 Q 的长度。*

***辅助空间**：O （1）*



* * *

* * *



