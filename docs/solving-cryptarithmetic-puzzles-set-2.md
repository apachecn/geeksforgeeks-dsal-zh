# 解开密码谜题|第二集

> 原文:[https://www . geeksforgeeks . org/solving-cryptarithmetic-拼图-set-2/](https://www.geeksforgeeks.org/solving-cryptarithmetic-puzzles-set-2/)

给定一个大小为 **N** 的[字符串数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)、**arr【】**和一个[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，任务是找出是否有可能将范围**【0，9】**中的整数值映射到字符串中出现的每个字母表，使得对数组中所有字符串编码形成的数字求和后得到的总和等于字符串 **S** 形成的数字。

**示例:**

> **输入:**arr[][]= {“SEND”、“MORE”}，S =“MONEY”
> **输出:** Yes
> **解释:**
> 可能的方式之一是:
> 
> 1.  将字符映射如下， *'* S'→ 9，' E'→5，' N'→6，' D'→7，' M'→1，' O'→0，' R'→8，' Y'→2。
> 2.  现在，对字符串“SEND”、“MORE”和“MONEY”编码后，分别修改为 9567、1085 和 10652。
> 3.  因此，“SEND”和“MORE”的值之和等于(9567+1085 = 10652)，等于字符串“MONEY”的值。
> 
> 因此，打印“是”。
> 
> **输入:**arr[][]= {“SIX”、“SEVEN”、“SEVEN”}，S = "二十"
> **输出:**是
> **解释:**
> 可能的方式之一是:
> 
> 1.  将字符映射如下，“S”→6、“I”→5、“X”→0、“E”→8、“V”→7、“N”→2、“T”→1、“W”→“3”、“Y”→4。
> 2.  现在，在对字符串“六”、“七”和“二十”编码后，分别修改为 650、68782 和 138214。
> 3.  因此，“六”、“七”和“七”的值之和等于(650+ 68782+ 68782 = 138214)，这等于字符串“二十”的值。
> 
> 因此，打印“是”。

**本文第 1 集**已经讨论过[这里](https://www.geeksforgeeks.org/c-code-article-backtracking-set-8-solving-cryptarithmetic-puzzles/)中的弦阵大小为 **2** 。

**方法:**给定的问题可以使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。按照以下步骤解决问题:

*   初始化三个、[数组](https://www.geeksforgeeks.org/arrays-in-java/)比如**MP【26】、Hash【26】**和**charattfront【26】**来存储字母表的映射值，每个字符串中字母表的位置值之和，以及一个字符是否在任何字符串的起始索引处。
*   初始化一个数组**，该数组用于存储一个数字是否映射到任何字母表。**
*   初始化一个[字符串缓冲区](https://www.geeksforgeeks.org/stringbuffer-class-in-java/)表示**唯一的**来存储每个字母出现一次的字符串。
*   将 **-1** 分配给 **mp** 的每个数组元素。
*   [使用变量 **i** 迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** ，并执行以下操作:
    *   将字符串的长度**arr【I】**存储在变量 **M** 中。
    *   [使用变量 **j** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)、**arr【I】**，并执行以下操作:
        *   如果**MP[arr[I][j]–‘A’]**是 **-1** ，则在 **uniq** 中追加 **arr[i][j]** ，并将 **0** 分配给**MP[arr[I][j]-[A]**。
        *   现在用 **10 <sup>(M-j-1)</sup>** 来增加**散列[arr[I][j]-[A]]**的值。
        *   如果 **arr[i]。长度()> 1** 和 **j** 为 **0** 然后在**arr【I】【j】–**中的【A】标记为真。
*   [迭代字符串，](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** ，执行与每个数组字符串相同的任务。
*   将 **-1** 填充到 **mp 的每个数组元素中。**
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)说出**求解(字符串字，int i，int S，int[] mp，int[]已使用)**进行回溯:
    *   如果 **i** 等于 **word.length()** 则返回 **true** 如果 **S** 为 **0** 。否则，返回**假**。
    *   如果 **mp[word[i]-'A']** 不等于 **-1** 则递归调用函数**求解(word，i+1，S+mp[word[I]-' A ']* Hash[word[I]-' A]，MP，used)** 然后返回其返回的值。
    *   否则，将变量 **X** 初始化为**假**，并使用变量 **j** 迭代范围**【0，9】**，并执行以下操作:
        *   如果满足以下任一条件，继续循环中的下一次迭代:
            *   如果**用【j】**是**真**。
            *   如果**CharAtfront【word[I]—【A】】**为**1****j**为 **0** 。
        *   现在将**使用的【j】**标记为**真**，并将 **j** 分配给 **mp【单词【I】-【A】】。**
        *   以上步骤完成后，调用函数**求解(word，i+1，S + j * Hash[word[i]-'A']，mp，used)** ，然后用其返回的值执行 **X** 的[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-java/) 。
        *   现在将**使用的【j】**标记为**假**，并将 **-1** 分配给**MP【word[I]–‘A’】**进行回溯。
    *   返回 **X** 的值。
*   最后，完成以上步骤后，如果 **solve(uniq，0，0，mp，used)** 返回的值为真，则打印“**是**”。否则，打印“ **No** ”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Auxiliary Recursive function
// to perform backtracking
bool solve(string words, int i,
    int S, int mp[], int used[],
    int Hash[],
    int CharAtfront[])
{
    // If i is word.length
    if (i == words.length())

        // Return true if S is 0
        return (S == 0);

    // Stores the character at
    // index i
    char ch = words[i];

    // Stores the mapped value
    // of ch
    int val = mp[words[i] - 'A'];

    // If val is -1
    if (val != -1) {

        // Recursion
        return solve(words, i + 1,
                     S + val * Hash[ch - 'A'],
                     mp, used,
                     Hash, CharAtfront);
    }

    // Stores if there is any
    // possible solution
    bool x = false;

    // Iterate over the range
    for (int l = 0; l < 10; l++) {

        // If CharAtfront[ch-'A']
        // is true and l is 0
        if (CharAtfront[ch - 'A'] == 1
            && l == 0)
            continue;

        // If used[l] is true
        if (used[l] == 1)
            continue;

        // Assign l to ch
        mp[ch - 'A'] = l;

        // Marked l as used
        used[l] = 1;

        // Recursive function call
        x |= solve(words, i + 1,
                   S + l * Hash[ch - 'A'],
                   mp, used, Hash, CharAtfront);

        // Backtrack
        mp[ch - 'A'] = -1;

        // Unset used[l]
        used[l] = 0;
    }

    // Return the value of x;
    return x;
}

// Function to check if the
// assignment of digits to
// characters is possible
bool isSolvable(string words[], string result, int N)
{

    // Stores the value
    // assigned to alphabets
    int mp[26];

    // Stores if a number
    // is assigned to any
    // character or not
    int used[10];

    // Stores the sum of position
    // value of a character
    // in every string
    int Hash[26];

    // Stores if a character
    // is at index 0 of any
    // string
    int CharAtfront[26];

    memset(mp, -1, sizeof(mp));
    memset(used, -1, sizeof(used));
    memset(Hash, -1, sizeof(Hash));
    memset(CharAtfront, -1, sizeof(CharAtfront));

    // Stores the string formed
    // by concatenating every
    // occured character only
    // once
    string uniq = "";

    // Iterator over the array,
    // words
    for(int word = 0; word < N; word++) {

        // Iterate over the string,
        // word
        for (int i = 0; i < words[word].length(); i++) {

            // Stores the character
            // at ith position
            char ch = words[word][i];

            // Update Hash[ch-'A]
            Hash[ch - 'A'] += (int)pow(10, words[word].length() - i - 1);

            // If mp[ch-'A'] is -1
            if (mp[ch - 'A'] == -1) {

                mp[ch - 'A'] = 0;
                uniq += (char)ch;
            }

            // If i is 0 and word
            // length is greater
            // than 1
            if (i == 0 && words[word].length() > 1) {

                CharAtfront[ch - 'A'] = 1;
            }
        }
    }

    // Iterate over the string result
    for (int i = 0; i < result.length(); i++) {

        char ch = result[i];

        Hash[ch - 'A'] -= (int)pow(10, result.length() - i - 1);

        // If mp[ch-'A] is -1
        if (mp[ch - 'A'] == -1) {
            mp[ch - 'A'] = 0;
            uniq += (char)ch;
        }

        // If i is 0 and length of
        // result is greater than 1
        if (i == 0 && result.length() > 1) {
            CharAtfront[ch - 'A'] = 1;
        }
    }

    memset(mp, -1, sizeof(mp));

    // Recursive call of the function
    return solve(uniq, 0, 0, mp, used, Hash, CharAtfront);
}

int main()
{
    // Input
    string arr[] = { "SIX", "SEVEN", "SEVEN" };
    string S = "TWENTY";

    int N = sizeof(arr)/sizeof(arr[0]);

    // Function Call
    if (isSolvable(arr, S, N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}

// This code is contributed by suresh07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to check if the
    // assignment of digits to
    // characters is possible
    public static boolean isSolvable(String[] words,
                                     String result)
    {
        // Stores the value
        // assigned to alphabets
        int mp[] = new int[26];

        // Stores if a number
        // is assigned to any
        // character or not
        int used[] = new int[10];

        // Stores the sum of position
        // value of a character
        // in every string
        int Hash[] = new int[26];

        // Stores if a character
        // is at index 0 of any
        // string
        int CharAtfront[] = new int[26];

        Arrays.fill(mp, -1);
        Arrays.fill(used, 0);
        Arrays.fill(Hash, 0);
        Arrays.fill(CharAtfront, 0);

        // Stores the string formed
        // by concatenating every
        // occured character only
        // once
        StringBuilder uniq = new StringBuilder();

        // Iterator over the array,
        // words
        for (String word : words) {

            // Iterate over the string,
            // word
            for (int i = 0; i < word.length(); i++) {

                // Stores the character
                // at ith position
                char ch = word.charAt(i);

                // Update Hash[ch-'A]
                Hash[ch - 'A'] += (int)Math.pow(
                    10, word.length() - i - 1);

                // If mp[ch-'A'] is -1
                if (mp[ch - 'A'] == -1) {

                    mp[ch - 'A'] = 0;
                    uniq.append((char)ch);
                }

                // If i is 0 and word
                // length is greater
                // than 1
                if (i == 0 && word.length() > 1) {

                    CharAtfront[ch - 'A'] = 1;
                }
            }
        }

        // Iterate over the string result
        for (int i = 0; i < result.length(); i++) {

            char ch = result.charAt(i);

            Hash[ch - 'A'] -= (int)Math.pow(
                10, result.length() - i - 1);

            // If mp[ch-'A] is -1
            if (mp[ch - 'A'] == -1) {
                mp[ch - 'A'] = 0;
                uniq.append((char)ch);
            }

            // If i is 0 and length of
            // result is greater than 1
            if (i == 0 && result.length() > 1) {
                CharAtfront[ch - 'A'] = 1;
            }
        }

        Arrays.fill(mp, -1);

        // Recursive call of the function
        return solve(uniq, 0, 0, mp, used, Hash,
                     CharAtfront);
    }

    // Auxiliary Recursive function
    // to perform backtracking
    public static boolean solve(
        StringBuilder words, int i,
        int S, int[] mp, int[] used,
        int[] Hash,
        int[] CharAtfront)
    {
        // If i is word.length
        if (i == words.length())

            // Return true if S is 0
            return (S == 0);

        // Stores the character at
        // index i
        char ch = words.charAt(i);

        // Stores the mapped value
        // of ch
        int val = mp[words.charAt(i) - 'A'];

        // If val is -1
        if (val != -1) {

            // Recursion
            return solve(words, i + 1,
                         S + val * Hash[ch - 'A'],
                         mp, used,
                         Hash, CharAtfront);
        }

        // Stores if there is any
        // possible solution
        boolean x = false;

        // Iterate over the range
        for (int l = 0; l < 10; l++) {

            // If CharAtfront[ch-'A']
            // is true and l is 0
            if (CharAtfront[ch - 'A'] == 1
                && l == 0)
                continue;

            // If used[l] is true
            if (used[l] == 1)
                continue;

            // Assign l to ch
            mp[ch - 'A'] = l;

            // Marked l as used
            used[l] = 1;

            // Recursive function call
            x |= solve(words, i + 1,
                       S + l * Hash[ch - 'A'],
                       mp, used, Hash, CharAtfront);

            // Backtrack
            mp[ch - 'A'] = -1;

            // Unset used[l]
            used[l] = 0;
        }

        // Return the value of x;
        return x;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        String[] arr
            = { "SIX", "SEVEN", "SEVEN" };
        String S = "TWENTY";

        // Function Call
        if (isSolvable(arr, S))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the
# assignment of digits to
# characters is possible
def isSolvable(words, result):
    # Stores the value
    # assigned to alphabets
    mp = [-1]*(26)

    # Stores if a number
    # is assigned to any
    # character or not
    used = [0]*(10)

    # Stores the sum of position
    # value of a character
    # in every string
    Hash = [0]*(26)

    # Stores if a character
    # is at index 0 of any
    # string
    CharAtfront = [0]*(26)

    # Stores the string formed
    # by concatenating every
    # occured character only
    # once
    uniq = ""

    # Iterator over the array,
    # words
    for word in range(len(words)):
        # Iterate over the string,
        # word
        for i in range(len(words[word])):
            # Stores the character
            # at ith position
            ch = words[word][i]

            # Update Hash[ch-'A]
            Hash[ord(ch) - ord('A')] += pow(10, len(words[word]) - i - 1)

            # If mp[ch-'A'] is -1
            if mp[ord(ch) - ord('A')] == -1:
                mp[ord(ch) - ord('A')] = 0
                uniq += str(ch)

            # If i is 0 and word
            # length is greater
            # than 1
            if i == 0 and len(words[word]) > 1:
                CharAtfront[ord(ch) - ord('A')] = 1

    # Iterate over the string result
    for i in range(len(result)):
        ch = result[i]

        Hash[ord(ch) - ord('A')] -= pow(10, len(result) - i - 1)

        # If mp[ch-'A] is -1
        if mp[ord(ch) - ord('A')] == -1:
            mp[ord(ch) - ord('A')] = 0
            uniq += str(ch)

        # If i is 0 and length of
        # result is greater than 1
        if i == 0 and len(result) > 1:
            CharAtfront[ord(ch) - ord('A')] = 1

    mp = [-1]*(26)

    # Recursive call of the function
    return True

# Auxiliary Recursive function
# to perform backtracking
def solve(words, i, S, mp, used, Hash, CharAtfront):
    # If i is word.length
    if i == len(words):
        # Return true if S is 0
        return S == 0

    # Stores the character at
    # index i
    ch = words[i]

    # Stores the mapped value
    # of ch
    val = mp[ord(words[i]) - ord('A')]

    # If val is -1
    if val != -1:
        # Recursion
        return solve(words, i + 1, S + val * Hash[ord(ch) - ord('A')], mp, used, Hash, CharAtfront)

    # Stores if there is any
    # possible solution
    x = False

    # Iterate over the range
    for l in range(10):
        # If CharAtfront[ch-'A']
        # is true and l is 0
        if CharAtfront[ord(ch) - ord('A')] == 1 and l == 0:
            continue

        # If used[l] is true
        if used[l] == 1:
            continue

        # Assign l to ch
        mp[ord(ch) - ord('A')] = l

        # Marked l as used
        used[l] = 1

        # Recursive function call
        x |= solve(words, i + 1, S + l * Hash[ord(ch) - ord('A')], mp, used, Hash, CharAtfront)

        # Backtrack
        mp[ord(ch) - ord('A')] = -1

        # Unset used[l]
        used[l] = 0

    # Return the value of x;
    return x

arr = [ "SIX", "SEVEN", "SEVEN" ]
S = "TWENTY"

# Function Call
if isSolvable(arr, S):
    print("Yes")
else:
    print("No")

    # This code is contributed by mukesh07.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to check if the
    // assignment of digits to
    // characters is possible
    static bool isSolvable(string[] words, string result)
    {
        // Stores the value
        // assigned to alphabets
        int[] mp = new int[26];

        // Stores if a number
        // is assigned to any
        // character or not
        int[] used = new int[10];

        // Stores the sum of position
        // value of a character
        // in every string
        int[] Hash = new int[26];

        // Stores if a character
        // is at index 0 of any
        // string
        int[] CharAtfront = new int[26];

        Array.Fill(mp, -1);
        Array.Fill(used, 0);
        Array.Fill(Hash, 0);
        Array.Fill(CharAtfront, 0);

        // Stores the string formed
        // by concatenating every
        // occured character only
        // once
        string uniq = "";

        // Iterator over the array,
        // words
        foreach(string word in words) {

            // Iterate over the string,
            // word
            for (int i = 0; i < word.Length; i++) {

                // Stores the character
                // at ith position
                char ch = word[i];

                // Update Hash[ch-'A]
                Hash[ch - 'A'] += (int)Math.Pow(10, word.Length - i - 1);

                // If mp[ch-'A'] is -1
                if (mp[ch - 'A'] == -1) {

                    mp[ch - 'A'] = 0;
                    uniq += (char)ch;
                }

                // If i is 0 and word
                // length is greater
                // than 1
                if (i == 0 && word.Length > 1) {

                    CharAtfront[ch - 'A'] = 1;
                }
            }
        }

        // Iterate over the string result
        for (int i = 0; i < result.Length; i++) {

            char ch = result[i];

            Hash[ch - 'A'] -= (int)Math.Pow(10, result.Length - i - 1);

            // If mp[ch-'A] is -1
            if (mp[ch - 'A'] == -1) {
                mp[ch - 'A'] = 0;
                uniq += (char)ch;
            }

            // If i is 0 and length of
            // result is greater than 1
            if (i == 0 && result.Length > 1) {
                CharAtfront[ch - 'A'] = 1;
            }
        }

        Array.Fill(mp, -1);

        // Recursive call of the function
        return solve(uniq, 0, 0, mp, used, Hash, CharAtfront);
    }

    // Auxiliary Recursive function
    // to perform backtracking
    public static bool solve(string words, int i,
        int S, int[] mp, int[] used,
        int[] Hash,
        int[] CharAtfront)
    {
        // If i is word.length
        if (i == words.Length)

            // Return true if S is 0
            return (S == 0);

        // Stores the character at
        // index i
        char ch = words[i];

        // Stores the mapped value
        // of ch
        int val = mp[words[i] - 'A'];

        // If val is -1
        if (val != -1) {

            // Recursion
            return solve(words, i + 1,
                         S + val * Hash[ch - 'A'],
                         mp, used,
                         Hash, CharAtfront);
        }

        // Stores if there is any
        // possible solution
        bool x = false;

        // Iterate over the range
        for (int l = 0; l < 10; l++) {

            // If CharAtfront[ch-'A']
            // is true and l is 0
            if (CharAtfront[ch - 'A'] == 1
                && l == 0)
                continue;

            // If used[l] is true
            if (used[l] == 1)
                continue;

            // Assign l to ch
            mp[ch - 'A'] = l;

            // Marked l as used
            used[l] = 1;

            // Recursive function call
            x |= solve(words, i + 1,
                       S + l * Hash[ch - 'A'],
                       mp, used, Hash, CharAtfront);

            // Backtrack
            mp[ch - 'A'] = -1;

            // Unset used[l]
            used[l] = 0;
        }

        // Return the value of x;
        return x;
    }

  static void Main()
  {

    // Input
    string[] arr = { "SIX", "SEVEN", "SEVEN" };
    string S = "TWENTY";

    // Function Call
    if (isSolvable(arr, S))
        Console.Write("Yes");
    else
        Console.Write("No");
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if the
    // assignment of digits to
    // characters is possible
    function isSolvable(words, result)
    {
        // Stores the value
        // assigned to alphabets
        let mp = new Array(26);

        // Stores if a number
        // is assigned to any
        // character or not
        let used = new Array(10);

        // Stores the sum of position
        // value of a character
        // in every string
        let Hash = new Array(26);

        // Stores if a character
        // is at index 0 of any
        // string
        let CharAtfront = new Array(26);

        mp.fill(-1);
        used.fill(0);
        Hash.fill(0);
        CharAtfront.fill(0);

        // Stores the string formed
        // by concatenating every
        // occured character only
        // once
        let uniq = "";

        // Iterator over the array,
        // words
        for(let word = 0; word < words.length; word++) {

            // Iterate over the string,
            // word
            for (let i = 0; i < words[word].length; i++) {

                // Stores the character
                // at ith position
                let ch = words[word][i];

                // Update Hash[ch-'A]
                Hash[ch.charCodeAt() - 'A'.charCodeAt()] += Math.pow(10, words[word].length - i - 1);

                // If mp[ch-'A'] is -1
                if (mp[ch.charCodeAt() - 'A'.charCodeAt()] == -1) {

                    mp[ch.charCodeAt() - 'A'.charCodeAt()] = 0;
                    uniq += String.fromCharCode(ch);
                }

                // If i is 0 and word
                // length is greater
                // than 1
                if (i == 0 && words[word].length > 1) {

                    CharAtfront[ch.charCodeAt() - 'A'.charCodeAt()] = 1;
                }
            }
        }

        // Iterate over the string result
        for (let i = 0; i < result.length; i++) {

            let ch = result[i];

            Hash[ch.charCodeAt() - 'A'.charCodeAt()] -= Math.pow(10, result.length - i - 1);

            // If mp[ch-'A] is -1
            if (mp[ch.charCodeAt() - 'A'.charCodeAt()] == -1) {
                mp[ch.charCodeAt() - 'A'.charCodeAt()] = 0;
                uniq += String.fromCharCode(ch);
            }

            // If i is 0 and length of
            // result is greater than 1
            if (i == 0 && result.length > 1) {
                CharAtfront[ch.charCodeAt() - 'A'.charCodeAt()] = 1;
            }
        }

        mp.fill(-1);

        // Recursive call of the function
        return solve(uniq, 0, 0, mp, used, Hash, CharAtfront);
    }

    // Auxiliary Recursive function
    // to perform backtracking
    function solve(words, i, S, mp, used, Hash, CharAtfront)
    {
        // If i is word.length
        if (i == words.length)

            // Return true if S is 0
            return (S == 0);

        // Stores the character at
        // index i
        let ch = words[i];

        // Stores the mapped value
        // of ch
        let val = mp[words[i].charCodeAt() - 'A'.charCodeAt()];

        // If val is -1
        if (val != -1) {

            // Recursion
            return solve(words, i + 1, S + val * Hash[ch.charCodeAt() - 'A'.charCodeAt()], mp, used, Hash, CharAtfront);
        }

        // Stores if there is any
        // possible solution
        let x = false;

        // Iterate over the range
        for (let l = 0; l < 10; l++) {

            // If CharAtfront[ch-'A']
            // is true and l is 0
            if (CharAtfront[ch.charCodeAt() - 'A'.charCodeAt()] == 1
                && l == 0)
                continue;

            // If used[l] is true
            if (used[l] == 1)
                continue;

            // Assign l to ch
            mp[ch.charCodeAt() - 'A'.charCodeAt()] = l;

            // Marked l as used
            used[l] = 1;

            // Recursive function call
            x |= solve(words, i + 1,
                       S + l * Hash[ch.charCodeAt() - 'A'.charCodeAt()],
                       mp, used, Hash, CharAtfront);

            // Backtrack
            mp[ch.charCodeAt() - 'A'.charCodeAt()] = -1;

            // Unset used[l]
            used[l] = 0;
        }

        // Return the value of x;
        return x;
    }

    // Input
    let arr = [ "SIX", "SEVEN", "SEVEN" ];
    let S = "TWENTY";

    // Function Call
    if (!isSolvable(arr, S))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by decode2207.
</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N*M+10！)，其中 M 是最大字符串的长度。*
***辅助空间:** O(26)*