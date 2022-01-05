# 从给定字符串形成最小数量的回文字符串

> 原文:[https://www . geesforgeks . org/form-给定字符串的最小回文字符串数/](https://www.geeksforgeeks.org/form-minimum-number-of-palindromic-strings-from-a-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是将 **S** 的字符进行划分，形成**最小**个数的[回文字符串](https://www.geeksforgeeks.org/string-palindrome/)。

**注意:**可以有多个正确答案。

**示例:**

> **输入:**S = " geeksforgeeks "
> T3】输出: {eegksrskgee，o，f}
> 
> **说明:**
> 至少要有 3 个字符串“eegksrskgee”、“o”、“f”。3 个形成的字符串都是回文。
> 
> **输入** : S =“阿巴”
> **输出:** {“亚贝巴”}
> 
> **解释:**
> 给定的字符串 S =“亚贝巴”已经是回文字符串了所以，只会形成 1 个字符串。
> 
> **输入:S =**【ABC】
> **输出:**{“a”、“b”、“c”}
> 
> **说明:**
> 至少要有 3 个字符串“a”、“b”、“c”。3 个形成的字符串都是回文。

**进场:**

主要观察到一个[回文串](https://www.geeksforgeeks.org/string-palindrome/)如果反转的话保持不变。形成的字符串的长度并不重要，所以尽量让字符串变得更大。如果某个字符不能成为回文字符串的一部分，则将该字符推入新字符串。

*   一般的方法是存储每个字符的[频率，如果某个字符的频率是奇数，那么我们必须创建一个新的字符串，并将我们的答案增加 1。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)
*   请注意，如果没有奇数频率的字符，至少还需要一个字符串，所以最终答案将是 max(1，奇数频率的字符)。
*   要打印字符串，请将奇数字符频率字符存储在一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，将偶数字符存储在另一个向量中。
*   用包含奇数字符的字符串组成一个回文字符串，并附加一个包含偶数字符的字符串，所有其他字符串都只有一个字符。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return
// minimum palindromic strings formed
int minimumPalindromicStrings(string S)
{
    // Store the length of string
    int N = S.length();

    // Iterate over the string
    // and store the frequency of
    // all characters A vector
    // to store the frequency
    vector<int> freq(26);
    for (int i = 0; i < N; i++) {
        freq[S[i] - 'a']++;
    }

    // Store the odd frequency characters
    vector<int> oddFreqCharacters;

    // Store the even frequency of characters
    // in the same vector by dividing
    // current frequency by 2 as one element
    // will be used on left as well as right side

    // Iterate through all possible characters
    // and check the parity of frequency
    for (int i = 0; i < 26; i++) {

        if (freq[i] & 1) {

            oddFreqCharacters.push_back(i);
            freq[i]--;
        }

        freq[i] /= 2;
    }

    // store answer in a vector
    vector<string> ans;

    // if there are no odd Frequency characters
    // then print the string with even characters
    if (oddFreqCharacters.empty()) {

        // store the left part
        // of the palindromic string
        string left = "";

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < freq[i]; j++) {

                left += char(i + 'a');
            }
        }

        string right = left;

        // reverse the right part of the string
        reverse(right.begin(), right.end());

        // store the string in ans vector
        ans.push_back(left + right);
    }

    else {

        // take any character
        // from off frequency element
        string middle = "";
        int c = oddFreqCharacters.back();
        oddFreqCharacters.pop_back();
        middle += char(c + 'a');

        // repeat the above step to form
        // left and right strings
        string left = "";

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < freq[i]; j++) {

                left += char(i + 'a');
            }
        }

        string right = left;

        // reverse the right part of the string
        reverse(right.begin(), right.end());

        // store the string in ans vector
        ans.push_back(left + middle + right);

        // store all other odd frequency strings
        while (!oddFreqCharacters.empty()) {

            int c = oddFreqCharacters.back();
            oddFreqCharacters.pop_back();
            string middle = "";
            middle += char(c + 'a');
            ans.push_back(middle);
        }
    }

    // Print the answer
    cout << "[";
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i];
        if (i != ans.size() - 1) {
            cout << ", ";
        }
    }
    cout << "]";
    return 0;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    minimumPalindromicStrings(S);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

class GFG{

// Function to return
// minimum palindromic Strings formed
static int minimumPalindromicStrings(String S)
{

    // Store the length of String
    int N = S.length();

    // Iterate over the String
    // and store the frequency of
    // all characters A vector
    // to store the frequency
   int[] freq = new int[26];
    for (int i = 0; i < N; i++) {
        freq[S.charAt(i) - 'a']++;
    }

    // Store the odd frequency characters
    Vector<Integer> oddFreqCharacters = new Vector<Integer>();

    // Store the even frequency of characters
    // in the same vector by dividing
    // current frequency by 2 as one element
    // will be used on left as well as right side

    // Iterate through all possible characters
    // and check the parity of frequency
    for (int i = 0; i < 26; i++) {

        if (freq[i] % 2 == 1) {

            oddFreqCharacters.add(i);
            freq[i]--;
        }

        freq[i] /= 2;
    }

    // store answer in a vector
    Vector<String> ans = new Vector<String>();

    // if there are no odd Frequency characters
    // then print the String with even characters
    if (oddFreqCharacters.isEmpty()) {

        // store the left part
        // of the palindromic String
        String left = "";

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < freq[i]; j++) {

                left += (char)(i + 'a');
            }
        }

        String right = left;

        // reverse the right part of the String
        right = reverse(right);

        // store the String in ans vector
        ans.add(left + right);
    }

    else {

        // take any character
        // from off frequency element
        String middle = "";
        int c = oddFreqCharacters.lastElement();
        oddFreqCharacters.remove(oddFreqCharacters.size()-1);
        middle += (char)(c + 'a');

        // repeat the above step to form
        // left and right Strings
        String left = "";

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < freq[i]; j++) {

                left += (char)(i + 'a');
            }
        }

        String right = left;

        // reverse the right part of the String
        right = reverse(right);

        // store the String in ans vector
        ans.add(left + middle + right);

        // store all other odd frequency Strings
        while (!oddFreqCharacters.isEmpty()) {

            c = oddFreqCharacters.lastElement();
            oddFreqCharacters.remove(oddFreqCharacters.size()-1);
            middle = "";
            middle += (char)(c + 'a');
            ans.add(middle);
        }
    }

    // Print the answer
    System.out.print("[");
    for (int i = 0; i < ans.size(); i++) {
        System.out.print(ans.get(i));
        if (i != ans.size() - 1) {
            System.out.print(", ");
        }
    }
    System.out.print("]");
    return 0;
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{
    String S = "geeksforgeeks";
    minimumPalindromicStrings(S);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to return
// minimum palindromic Strings formed
static int minimumPalindromicStrings(String S)
{

    // Store the length of String
    int N = S.Length;

    // Iterate over the String
    // and store the frequency of
    // all characters A vector
    // to store the frequency
   int[] freq = new int[26];
    for (int i = 0; i < N; i++) {
        freq[S[i] - 'a']++;
    }

    // Store the odd frequency characters
    List<int> oddFreqchars = new List<int>();

    // Store the even frequency of characters
    // in the same vector by dividing
    // current frequency by 2 as one element
    // will be used on left as well as right side

    // Iterate through all possible characters
    // and check the parity of frequency
    for (int i = 0; i < 26; i++) {

        if (freq[i] % 2 == 1) {

            oddFreqchars.Add(i);
            freq[i]--;
        }

        freq[i] /= 2;
    }

    // store answer in a vector
    List<String> ans = new List<String>();

    // if there are no odd Frequency characters
    // then print the String with even characters
    if (oddFreqchars.Count==0) {

        // store the left part
        // of the palindromic String
        String left = "";

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < freq[i]; j++) {

                left += (char)(i + 'a');
            }
        }

        String right = left;

        // reverse the right part of the String
        right = reverse(right);

        // store the String in ans vector
        ans.Add(left + right);
    }

    else {

        // take any character
        // from off frequency element
        String middle = "";
        int c = oddFreqchars[oddFreqchars.Count-1];
        oddFreqchars.RemoveAt(oddFreqchars.Count-1);
        middle += (char)(c + 'a');

        // repeat the above step to form
        // left and right Strings
        String left = "";

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < freq[i]; j++) {

                left += (char)(i + 'a');
            }
        }

        String right = left;

        // reverse the right part of the String
        right = reverse(right);

        // store the String in ans vector
        ans.Add(left + middle + right);

        // store all other odd frequency Strings
        while (oddFreqchars.Count!=0) {

            c = oddFreqchars[oddFreqchars.Count-1];
            oddFreqchars.RemoveAt(oddFreqchars.Count-1);
            middle = "";
            middle += (char)(c + 'a');
            ans.Add(middle);
        }
    }

    // Print the answer
    Console.Write("[");
    for (int i = 0; i < ans.Count; i++) {
        Console.Write(ans[i]);
        if (i != ans.Count - 1) {
            Console.Write(", ");
        }
    }
    Console.Write("]");
    return 0;
}
static String reverse(String input) {
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "geeksforgeeks";
    minimumPalindromicStrings(S);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
[eegksrskgee, o, f]
```

**时间复杂度:** O(N*26)

**空间复杂度:** O(N)