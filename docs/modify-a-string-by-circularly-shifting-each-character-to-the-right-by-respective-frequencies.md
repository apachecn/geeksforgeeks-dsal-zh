# 通过将每个字符向右循环移动各自的频率来修改字符串

> 原文:[https://www . geeksforgeeks . org/按各个频率将每个字符向右循环移动修改字符串/](https://www.geeksforgeeks.org/modify-a-string-by-circularly-shifting-each-character-to-the-right-by-respective-frequencies/)

给定一个由小写英文字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是将给定字符串 **S** 的每个字符按其频率循环右移。

> 字符的循环移动是指将字符“z”移动到“a”，作为其下一个字符。

**示例:**

> **输入:** S = "geeksforgeeks"
> **输出:** iiimugpsiiimu
> **说明:**
> 对字符串 S 进行以下更改:
> 
> 1.  g 的频率是 2。因此，将字符“g”移动 2 就变成了“I”。
> 2.  “e”的频率是 4。因此，将字符“e”移动 4 就变成了“I”。
> 3.  “k”的频率是 2。因此，将字符“k”移动 2 就变成了“m”。
> 4.  的频率是 2。因此，将字符的移动 2 就变成了 u。
> 5.  “f”的频率为 1。因此，将字符“f”移动 1 就变成了“g”。
> 6.  “o”的频率为 1。因此，将字符“o”移动 1 就变成了“p”。
> 7.  “r”的频率为 1。因此，将字符“r”移动 1 就变成了“s”。
> 
> 在上述字符移动之后，字符串修改为“iiimugpsiiimu”。
> 
> **输入:**S = " aabcadb "
> T3】输出:dddd

**方法:**解决这个问题的思路是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)找到字符串中每个字符的[出现频率，然后按其频率递增每个字符。按照以下步骤解决问题:](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如**频率[]** ，存储字符串 **S** 中每个字符的出现次数。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   求当前字符 **S[i]** 的频率。
    *   增加当前字符的频率，并将 **S[i]** 的值更新为其更新的字符。
*   完成上述步骤后，打印字符串 **S** 作为结果修改字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to replace the characters
// by its frequency of character in it
void addFrequencyToCharacter(string S)
{
    // Stores frequencies of characters
    // in the string S
    int frequency[26] = { 0 };

    int N = S.length();

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Increment the frequency of
        // each character by 1
        frequency[S[i] - 'a'] += 1;
    }

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Find the frequency of
        // the current character
        int add = frequency[S[i] - 'a'] % 26;

        // Update the character
        if (int(S[i]) + add
            <= int('z'))
            S[i] = char(int(S[i])
                        + add);

        else {
            add = (int(S[i]) + add)
                  - (int('z'));
            S[i] = char(int('a')
                        + add - 1);
        }
    }

    // Print the resultant string
    cout << S;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    addFrequencyToCharacter(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to replace the characters
    // by its frequency of character in it
    static void addFrequencyToCharacter(String Str)
    {
        // Stores frequencies of characters
        // in the string S
        int frequency[] = new int[26];

        int N = Str.length();
        char S[] = Str.toCharArray();

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // Increment the frequency of
            // each character by 1
            frequency[S[i] - 'a'] += 1;
        }

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // Find the frequency of
            // the current character
            int add = frequency[S[i] - 'a'] % 26;

            // Update the character
            if ((int)(S[i]) + add <= (int)('z'))
                S[i] = (char)((int)(S[i]) + add);

            else {
                add = ((int)(S[i]) + add) - ((int)('z'));
                S[i] = (char)((int)('a') + add - 1);
            }
        }

        // Print the resultant string
        System.out.println(new String(S));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "geeksforgeeks";
        addFrequencyToCharacter(S);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to replace the characters
# by its frequency of character in it
def addFrequencyToCharacter(S):

    # Stores frequencies of characters
    # in the string S
    frequency = [0 for i in range(26)]

    N = len(S)

    S = list(S)
    # Traverse the string S
    for i in range(N):

        # Increment the frequency of
        # each character by 1
        frequency[ord(S[i]) - ord('a')] += 1

    # Traverse the string S
    for i in range(N):

        # Find the frequency of
        # the current character
        add = frequency[ord(S[i]) - ord('a')] % 26

        # Update the character
        if ord(S[i]) + add <= ord('z'):
            S[i] = chr(ord(S[i]) + add)

        else:
            add = ord(S[i]) + add - ord('z')
            S[i] = chr(ord('a') + add - 1)

    # Print the resultant string
    s = ""
    print(s.join(S))

# Driver Code
if __name__ == '__main__':

    S = "geeksforgeeks"

    addFrequencyToCharacter(S)

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to replace the characters
// by its frequency of character in it
static void addFrequencyToCharacter(string Str)
{

    // Stores frequencies of characters
    // in the string S
    int[] frequency = new int[26];

    int N = Str.Length;
    char[] S = Str.ToCharArray();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Increment the frequency of
        // each character by 1
        frequency[S[i] - 'a'] += 1;
    }

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Find the frequency of
        // the current character
        int add = frequency[S[i] - 'a'] % 26;

        // Update the character
        if ((int)(S[i]) + add <= (int)('z'))
            S[i] = (char)((int)(S[i]) + add);

        else
        {
            add = ((int)(S[i]) + add) - ((int)('z'));
            S[i] = (char)((int)('a') + add - 1);
        }
    }

    // Print the resultant string
    Console.Write(new string(S));
}

// Driver Code
public static void Main(string[] args)
{
    string S = "geeksforgeeks";
    addFrequencyToCharacter(S);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to replace the characters
// by its frequency of character in it
function addFrequencyToCharacter(Str)
{
    // Stores frequencies of characters
    // in the string S
    var frequency = Array.from({length: 26}, (_, i) => 0);

    var N = Str.length;
    var S = Str.split('');

    // Traverse the string S
    for (var i = 0; i < N; i++) {

        // Increment the frequency of
        // each character by 1
        frequency[S[i].charCodeAt(0) -
        'a'.charCodeAt(0)] += 1;
    }

    // Traverse the string S
    for (var i = 0; i < N; i++) {

        // Find the frequency of
        // the current character
        var add = frequency[S[i].charCodeAt(0) -
        'a'.charCodeAt(0)] % 26;

        // Update the character
        if ((S[i].charCodeAt(0)) +
                               add <= ('z').charCodeAt(0))
            S[i] = String.fromCharCode((S[i].charCodeAt(0))
            + add);

        else {
            add = ((S[i].charCodeAt(0)) + add) -
            (('z').charCodeAt(0));
            S[i] = String.fromCharCode(('a'.charCodeAt(0)) +
            add - 1);
        }
    }

    // Print the resultant string
    document.write(S.join(''));
}

// Driver Code
var S = "geeksforgeeks";
addFrequencyToCharacter(S);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
iiimugpsiiimu
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(26)