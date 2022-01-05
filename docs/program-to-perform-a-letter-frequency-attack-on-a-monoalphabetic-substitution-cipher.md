# 对单字母替代密码进行字母频率攻击的程序

> 原文:[https://www . geesforgeks . org/program-to-performance-a-字母-频率-攻击-a-单字母-替换-密码/](https://www.geeksforgeeks.org/program-to-perform-a-letter-frequency-attack-on-a-monoalphabetic-substitution-cipher/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，代表一个[单字母密码](https://www.geeksforgeeks.org/difference-between-monoalphabetic-cipher-and-polyalphabetic-cipher/)，任务是使用[字母频率攻击](https://en.wikipedia.org/wiki/Frequency_analysis)打印可以从给定的[单字母密码](https://www.geeksforgeeks.org/difference-between-monoalphabetic-cipher-and-polyalphabetic-cipher/)解密的前五个可能的纯文本。

**示例:**

> **输入:**s = " et oinshrdlcumfgbkqz "
> **输出:**a simple message
> 【b tjnqmf nftbhf】
> a simple message
> 【c ukrng ogucig】
> c ukrng ogucig
> 
> **输入:**s = " abcdefgh "
> T3】输出:w oeilha iaoowca
> 【j brvyun vnbbjpn】
> 【c ukrng ogucig】
> r jzdgcv dvjrxv
> 和 qggnjc kcqk

**方法:**根据以下观察结果可以解决问题:

1.  **频率分析**是已知的密文攻击之一。它基于对密文中字母或字母组出现频率的研究。在所有语言中，不同的字母使用频率不同。
2.  频率阵列攻击是基于这样的观察:在英文文本中，并非所有字母都以相同的**频率**出现。
3.  在给定的问题中，字符串**T =“etaoinshrdlcumfgypvkjxqz”**用于解密。
4.  因此，想法是找出给定字符串中**I<sup>th</sup>T3【最大出现字母】和字符串 **T** 之间的差异，然后用该差异移动给定字符串的所有字母。获得的字符串将是可能的解密字符串之一。** 

按照以下步骤解决问题:

*   初始化一个字符串，说 **T** 为**“etaoinshrdlcumfgypvkjxqz”。**
*   [找到字符串](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/) **S** 每个字符的频率，并将其存储在一个变量中，比如 **freq[]。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，5】**，并执行以下步骤:
    *   找到字符串 **S** 中出现次数最多的元素 **i <sup>th</sup>** ，并将其存储在一个变量中，比如 **ch** 。
    *   找出字符串 **T** 的 **ch** 和**I<sup>th</sup>T5】字符之间的区别，并将其存储在一个变量中，比如说 **x** 。**
    *   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S、**的字符，将所有字符移动 **x** ，然后将得到的字符串推入一个数组**明文[]。**
*   最后，经过以上步骤，打印数组**中获得的字符串明文[]。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to decrypt a monoalphabetic
// substitution cipher using the letter
// frequency attack
void printString(string S, int N)
{

    // Stores final 5 possible deciphered
    // plaintext
    string plaintext[5];

    // Store the frequency of each letter in
    // cipher text
    int freq[26] = { 0 };

    // Stores the frequency of each letter
    // in cipher text in descending order
    int freqSorted[26];

    // Store which alphabet is used already
    int Used[26] = { 0 };

    // Traverse the string S
    for (int i = 0; i < N; i++) {
        if (S[i] != ' ') {
            freq[S[i] - 'A']++;
        }
    }

    // Copy the frequency array
    for (int i = 0; i < 26; i++) {
        freqSorted[i] = freq[i];
    }

    // Stores the string formed from concatenating
    // the english letters in the decreasing frequency
    // in the english language
    string T = "ETAOINSHRDLCUMWFGYPBVKJXQZ";

    // Sort the array in descending order
    sort(freqSorted, freqSorted + 26, greater<int>());

    // Iterate over the range [0, 5]
    for (int i = 0; i < 5; i++) {

        int ch = -1;

        // Iterate over the range [0, 26]
        for (int j = 0; j < 26; j++) {

            if (freqSorted[i] == freq[j] && Used[j] == 0) {
                Used[j] = 1;
                ch = j;
                break;
            }
        }
        if (ch == -1)
            break;

        // Store the numerical equivalent of letter at
        // ith index of array letter_frequency
        int x = T[i] - 'A';

        // Calculate the probable shift used
        // in monoalphabetic cipher
        x = x - ch;

        // Temporary string to generate one
        // plaintext at a time
        string curr = "";

        // Generate the probable ith plaintext
        // string using the shift calculated above
        for (int k = 0; k < N; k++) {

            // Insert whitespaces as it is
            if (S[k] == ' ') {
                curr += ' ';
                continue;
            }

            // Shift the kth letter of the
            // cipher by x
            int y = S[k] - 'A';
            y += x;

            if (y < 0)
                y += 26;
            if (y > 25)
                y -= 26;

            // Add the kth calculated/shifted
            // letter to temporary string
            curr += 'A' + y;
        }

        plaintext[i] = curr;
    }

    // Print the generated 5 possible plaintexts
    for (int i = 0; i < 5; i++) {
        cout << plaintext[i] << endl;
    }
}

// Driver Code
int main()
{
    // Given string
    string S = "B TJNQMF NFTTBHF";
    int N = S.length();

    // Function Call
    printString(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to decrypt a monoalphabetic
// substitution cipher using the letter
// frequency attack
static void printString(String S, int N)
{

    // Stores final 5 possible deciphered
    // plaintext
    String []plaintext = new String[5];

    // Store the frequency of each letter in
    // cipher text
    int freq[] = new int[26];

    // Stores the frequency of each letter
    // in cipher text in descending order
    int freqSorted[] = new int[26];

    // Store which alphabet is used already
    int Used[] = new int[26];

    // Traverse the String S
    for (int i = 0; i < N; i++) {
        if (S.charAt(i) != ' ') {
            freq[S.charAt(i) - 'A']++;
        }
    }

    // Copy the frequency array
    for (int i = 0; i < 26; i++) {
        freqSorted[i] = freq[i];
    }

    // Stores the String formed from concatenating
    // the english letters in the decreasing frequency
    // in the english language
    String T = "ETAOINSHRDLCUMWFGYPBVKJXQZ";

    // Sort the array in descending order
    Arrays.sort(freqSorted);
    freqSorted= reverse(freqSorted);
    // Iterate over the range [0, 5]
    for (int i = 0; i < 5; i++) {

        int ch = -1;

        // Iterate over the range [0, 26]
        for (int j = 0; j < 26; j++) {

            if (freqSorted[i] == freq[j] && Used[j] == 0) {
                Used[j] = 1;
                ch = j;
                break;
            }
        }
        if (ch == -1)
            break;

        // Store the numerical equivalent of letter at
        // ith index of array letter_frequency
        int x = T.charAt(i) - 'A';

        // Calculate the probable shift used
        // in monoalphabetic cipher
        x = x - ch;

        // Temporary String to generate one
        // plaintext at a time
        String curr = "";

        // Generate the probable ith plaintext
        // String using the shift calculated above
        for (int k = 0; k < N; k++) {

            // Insert whitespaces as it is
            if (S.charAt(k) == ' ') {
                curr += (char)' ';
                continue;
            }

            // Shift the kth letter of the
            // cipher by x
            int y = S.charAt(k) - 'A';
            y += x;

            if (y < 0)
                y += 26;
            if (y > 25)
                y -= 26;

            // Add the kth calculated/shifted
            // letter to temporary String
            curr += (char)('A' + y);
        }

        plaintext[i] = curr;
    }

    // Print the generated 5 possible plaintexts
    for (int i = 0; i < 5; i++) {
        System.out.print(plaintext[i] +"\n");
    }
}
static int[] reverse(int a[]) {
    int i, n = a.length, t;
    for (i = 0; i < n / 2; i++) {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}
// Driver Code
public static void main(String[] args)
{
    // Given String
    String S = "B TJNQMF NFTTBHF";
    int N = S.length();

    // Function Call
    printString(S, N);

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to decrypt a monoalphabetic
# substitution cipher using the letter
# frequency attack
def printString(S, N):

    # Stores final 5 possible deciphered
    # plaintext
    plaintext = [None] * 5

    # Store the frequency of each letter in
    # cipher text
    freq = [0] * 26

    # Stores the frequency of each letter
    # in cipher text in descending order
    freqSorted = [None] * 26

    # Store which alphabet is used already
    used = [0] * 26

    # Traverse the string S
    for i in range(N):
        if S[i] != ' ':
            freq[ord(S[i]) - 65] += 1

    # Copy the frequency array        
    for i in range(26):
        freqSorted[i] = freq[i]

    # Stores the string formed from
    # concatenating the english letters
    # in the decreasing frequency in the
    # english language    
    T = "ETAOINSHRDLCUMWFGYPBVKJXQZ"

    # Sort the array in descending order
    freqSorted.sort(reverse = True)

    # Iterate over the range [0, 5]
    for i in range(5):
        ch = -1

        # Iterate over the range [0, 26]
        for j in range(26):
            if freqSorted[i] == freq[j] and used[j] == 0:
                used[j] = 1
                ch = j
                break

        if ch == -1:
            break

        # Store the numerical equivalent of letter
        # at ith index of array letter_frequency
        x = ord(T[i]) - 65

        # Calculate the probable shift used
        # in monoalphabetic cipher
        x = x - ch

        # Temporary string to generate one
        # plaintext at a time
        curr = ""

        # Generate the probable ith plaintext
        # string using the shift calculated above
        for k in range(N):

            # Insert whitespaces as it is
            if S[k] == ' ':
                curr += " "
                continue

            # Shift the kth letter of the
            # cipher by x
            y = ord(S[k]) - 65
            y += x

            if y < 0:
                y += 26
            if y > 25:
                y -= 26

            # Add the kth calculated/shifted
            # letter to temporary string    
            curr += chr(y + 65)

        plaintext[i] = curr

    # Print the generated 5 possible plaintexts    
    for i in range(5):
        print(plaintext[i])

# Driver code

# Given string
S = "B TJNQMF NFTTBHF"
N = len(S)

# Function Call
printString(S, N)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to decrypt a monoalphabetic
// substitution cipher using the letter
// frequency attack
static void printString(String S, int N)
{

    // Stores readonly 5 possible deciphered
    // plaintext
    String []plaintext = new String[5];

    // Store the frequency of each letter in
    // cipher text
    int []freq = new int[26];

    // Stores the frequency of each letter
    // in cipher text in descending order
    int []freqSorted = new int[26];

    // Store which alphabet is used already
    int []Used = new int[26];

    // Traverse the String S
    for (int i = 0; i < N; i++) {
        if (S[i] != ' ') {
            freq[S[i] - 'A']++;
        }
    }

    // Copy the frequency array
    for (int i = 0; i < 26; i++) {
        freqSorted[i] = freq[i];
    }

    // Stores the String formed from concatenating
    // the english letters in the decreasing frequency
    // in the english language
    String T = "ETAOINSHRDLCUMWFGYPBVKJXQZ";

    // Sort the array in descending order
    Array.Sort(freqSorted);
    freqSorted= reverse(freqSorted);
    // Iterate over the range [0, 5]
    for (int i = 0; i < 5; i++) {

        int ch = -1;

        // Iterate over the range [0, 26]
        for (int j = 0; j < 26; j++) {

            if (freqSorted[i] == freq[j] && Used[j] == 0) {
                Used[j] = 1;
                ch = j;
                break;
            }
        }
        if (ch == -1)
            break;

        // Store the numerical equivalent of letter at
        // ith index of array letter_frequency
        int x = T[i] - 'A';

        // Calculate the probable shift used
        // in monoalphabetic cipher
        x = x - ch;

        // Temporary String to generate one
        // plaintext at a time
        String curr = "";

        // Generate the probable ith plaintext
        // String using the shift calculated above
        for (int k = 0; k < N; k++) {

            // Insert whitespaces as it is
            if (S[k] == ' ') {
                curr += (char)' ';
                continue;
            }

            // Shift the kth letter of the
            // cipher by x
            int y = S[k] - 'A';
            y += x;

            if (y < 0)
                y += 26;
            if (y > 25)
                y -= 26;

            // Add the kth calculated/shifted
            // letter to temporary String
            curr += (char)('A' + y);
        }

        plaintext[i] = curr;
    }

    // Print the generated 5 possible plaintexts
    for (int i = 0; i < 5; i++) {
        Console.Write(plaintext[i] +"\n");
    }
}
static int[] reverse(int []a) {
    int i, n = a.Length, t;
    for (i = 0; i < n / 2; i++) {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void Main(String[] args)
{
    // Given String
    String S = "B TJNQMF NFTTBHF";
    int N = S.Length;

    // Function Call
    printString(S, N);

}
}

// This code is contributed by shikhasingrajput
```

**Output**

```
A SIMPLE MESSAGE
B TJNQMF NFTTBHF
A SIMPLE MESSAGE
C UKORNG OGUUCIG
C UKORNG OGUUCIG
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)