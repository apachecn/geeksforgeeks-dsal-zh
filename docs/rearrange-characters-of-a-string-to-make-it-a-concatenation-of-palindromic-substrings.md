# 重新排列字符串的字符，使其成为回文子串的串联

> 原文:[https://www . geesforgeks . org/重排字符串字符使其成为回文子字符串的串联/](https://www.geeksforgeeks.org/rearrange-characters-of-a-string-to-make-it-a-concatenation-of-palindromic-substrings/)

给定一个由小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查给定的字符串是否可以重新排列，以便该字符串可以被拆分为长度至少为 2 的不重叠的[回文子字符串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)。如果发现**为真**，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S =“aaaaabcdd”
> T3】输出:是
> **解释:**将给定的字符串 S 重新排列为“acaaabbdd”，可以拆分为不重叠的回文子串“aca”、“aa”、“bb”、“dd”。
> 
> **输入:**S =
> 输出:否

**方法:**给定的问题可以通过将字符串的字符重新排列成由单个不同字符组成的**长度为 2** 的子字符串来解决。如果存在奇数频率的字符，则将它们放在**长度 2** 的回文子串中间。
按照以下步骤解决问题:

*   初始化一个辅助[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说大小为 **26** 的**频率[]** ，来存储字符串 **S** 中出现的每个字符的频率。
*   [遍历给定的字符串**S**T3】并更新数组**频率【】**中每个字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)[的频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   初始化两个变量，说**奇数**和**偶数**都为 **0** ，存储奇数元素的[频率和形成的**长度 2** 的](https://www.geeksforgeeks.org/find-the-number-occurring-odd-number-of-times/)[回文子串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)个数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **频率[]** ，如果**频率【I】**的值大于 **0** ，则将值**(频率【I】&1)**和**(频率【I】/2)**分别加到变量**奇数**和**偶数**上。
*   完成上述步骤后，如果**奇数**的值最多为**偶数**，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string can be
// modified such that it can be split into
// palindromic substrings of length >= 2
void canSplit(string& S)
{
    // Stores frequencies of characters
    vector<int> frequency(26, 0);

    int cnt_singles = 0;

    int k = 0;

    // Traverse the string
    for (int i = 0; i < S.length(); i++)

        // Update frequency
        // of each character
        frequency[S[i] - 'a']++;

    int odd = 0, eve = 0;

    // Traverse the frequency array
    for (int i = 0; i < 26; i++) {

        // Update values of odd and eve
        if (frequency[i]) {
            odd += (frequency[i] & 1);
            eve += frequency[i] / 2;
        }
    }

    // Print the result
    if (eve >= odd)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    string S = "aaabbbccc";
    canSplit(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to check if a string can be
    // modified such that it can be split into
    // palindromic substrings of length >= 2
    static void canSplit(String S)
    {
        // Stores frequencies of characters
        int frequency[] = new int[26];

        int cnt_singles = 0;

        int k = 0;

        // Traverse the string
        for (int i = 0; i < S.length(); i++)

            // Update frequency
            // of each character
            frequency[S.charAt(i) - 'a']++;

        int odd = 0, eve = 0;

        // Traverse the frequency array
        for (int i = 0; i < 26; i++) {

            // Update values of odd and eve
            if (frequency[i] != 0) {
                odd += (frequency[i] & 1);
                eve += frequency[i] / 2;
            }
        }

        // Print the result
        if (eve >= odd)
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "aaabbbccc";
        canSplit(S);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a string can be
# modified such that it can be split into
# palindromic substrings of length >= 2
def canSplit(S):

    # Stores frequencies of characters
    frequency = [0] * 26

    cnt_singles = 0

    k = 0

    # Traverse the string
    for i in range(len(S)):

        # Update frequency
        # of each character
        frequency[ord(S[i]) - ord('a')] += 1

    odd = 0
    eve = 0

    # Traverse the frequency array
    for i in range(26):

        # Update values of odd and eve
        if (frequency[i]):
            odd += (frequency[i] & 1)
            eve += frequency[i] // 2

    # Print the result
    if (eve >= odd):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == "__main__" :

    S = "aaabbbccc"

    canSplit(S)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to check if a string can be
  // modified such that it can be split into
  // palindromic substrings of length >= 2
  static void canSplit(string S)
  {

    // Stores frequencies of characters
    int []frequency = new int[26];
    int cnt_singles = 0;
    int k = 0;

    // Traverse the string
    for (int i = 0; i < S.Length; i++)

      // Update frequency
      // of each character
      frequency[S[i] - 'a']++;

    int odd = 0, eve = 0;

    // Traverse the frequency array
    for (int i = 0; i < 26; i++)
    {

      // Update values of odd and eve
      if (frequency[i] != 0)
      {
        odd += (frequency[i] & 1);
        eve += frequency[i] / 2;
      }
    }

    // Print the result
    if (eve >= odd)
      Console.WriteLine("Yes");
    else
      Console.WriteLine("No");
  }

  // Driver Code
  public static void Main(string[] args)
  {

    string S = "aaabbbccc";
    canSplit(S);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

// Function to check if a string can be
// modified such that it can be split into
// palindromic substrings of length >= 2
function canSplit(S){

    // Stores frequencies of characters
    let frequency = new Array(26).fill(0)

    let cnt_singles = 0

    let k = 0

    // Traverse the string
    for(let i = 0; i < S.length; i++){

        // Update frequency
        // of each character
        frequency[S.charCodeAt(i) - 'a'.charCodeAt(0)] += 1
    }
    let odd = 0
    let eve = 0

    // Traverse the frequency array
    for(let i = 0;  i < 26; i++){

        // Update values of odd and eve
        if (frequency[i]){
            odd += (frequency[i] & 1)
            eve += frequency[i] // 2
        }
    }
    // document.write the result
    if (eve >= odd){
        document.write("Yes")
    }
    else{
        document.write("No")
    }
}

// Driver Code

    let S = "aaabbbccc"

    canSplit(S)

// This code is contributed by gfgking

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)