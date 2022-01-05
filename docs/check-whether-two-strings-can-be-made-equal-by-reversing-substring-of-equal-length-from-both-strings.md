# 通过反转两个字符串中长度相等的子串来检查两个字符串是否可以相等

> 原文:[https://www . geesforgeks . org/check-是否可以通过反转两个字符串中长度相等的子字符串来使两个字符串相等/](https://www.geeksforgeeks.org/check-whether-two-strings-can-be-made-equal-by-reversing-substring-of-equal-length-from-both-strings/)

给两个字符串 **S1** 和 **S2** ，任务是检查字符串 **S1** 是否可以通过反转两个长度相等的字符串中的子字符串使其等于字符串 **S2** 。

**注意:**一个子串可以反转任意次。

**示例:**

> **输入:** S1 =【阿贝卡】，S2 =【阿卡布】
> **输出:**是
> **解释:**
> 可以通过以下方法使字符串 S1 和 S2 相等:
> 在范围[2，4](长度= 3)内反转 S1，在范围[1，3](长度= 3)内 S1 =【阿巴布】
> 反转 S2，在反转后 S2 =【阿巴布】
> S1 =【阿巴布】和 S2 =【阿巴布】。
> 因此，两者可以相等。
> 
> **输入:“**S1 =“ABCD”，S2 =“abdc”
> **输出:**否

**进场:**

1.  其思想是通过对两个字符串进行排序来使两个字符串相等。
2.  首先，检查两个字符串是否有相同的字符集。如果没有，那么回答是“没有”。
3.  将子字符串的长度固定为 2。这意味着交换相邻的字符。
4.  现在，通过反转大小为 2 的子串或换句话说，交换相邻字符来对字符串进行排序所需的移动次数是字符串的[反转计数](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)。
5.  如果两个字符串具有相同的反转计数，那么答案是“是”。
6.  如果它们具有不同的反转计数，只有在下列条件中至少有一个匹配时，才能使它们相等:
    *   首先，如果反转计数的奇偶性相同，即都是偶数或奇数，那么答案是“是”。我们将继续交换排序字符串中的任意一对元素，直到另一个被排序。因为，反转计数的差异将是均匀的，所以交换任何一对两次都不会产生任何变化。
    *   其次，如果奇偶校验不相同，那么在任何字符串中必须至少有一个频率大于 1 的字符。我们只是交换它们，直到另一个得到解决。因为交换相同的字符不会有任何改变。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// function to count inversion
// count of the string
int inversionCount(string& s)
{

    // for storing frequency
    int freq[26] = { 0 };
    int inv = 0;
    for (int i = 0; i < s.length(); i++) {
        int temp = 0;

        // Add all the characters which
        // are less than the ith character
        // before i.
        for (int j = 0; j < int(s[i] - 'a'); j++)
            // adding the count to inversion
            // count
            temp += freq[j];

        inv += (i - temp);
        // updating the character in
        // the frequency array

        freq[s[i] - 'a']++;
    }
    return inv;
}

// function to check whether any
// of the string have a repeated
// character
bool haveRepeated(string& S1,
                string& S2)
{

    int freq[26] = { 0 };
    for (char i : S1) {
        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    }

    for (int i = 0; i < 26; i++)
        freq[i] = 0;

    for (char i : S2) {
        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    }
    return false;
}

// function to check whether the
// string S1 and S2 can be made
// equal by reversing sub strings
// of same size in both strings
void checkToMakeEqual(string S1,
                    string S2)
{

    // frequency array to check
    // whether both string have
    // same character or not
    int freq[26] = { 0 };

    for (int i = 0; i < S1.length(); i++) {
        // adding the frequency;
        freq[S1[i] - 'a']++;
    }

    bool flag = 0;
    for (int i = 0; i < S2.length(); i++) {
        if (freq[S2[i] - 'a'] == 0) {
            // if the character is not in S1
            flag = true;
            break;
        }
        // decrementing the frequency
        freq[S2[i] - 'a']--;
    }

    if (flag == true) {
        // If both string doesnot
        // have same characters or not
        cout << "No\n";
        return;
    }

    // finding inversion count
    // of both strings
    int invCount1 = inversionCount(S1);
    int invCount2 = inversionCount(S2);

    if (invCount1 == invCount2
        || (invCount1 & 1) == (invCount2 & 1)
        || haveRepeated(S1, S2)) {
        // If inversion count is same,
        // or have same parity or if
        // any of the string have a
        // repeated character then
        // the answer is Yes else No
        cout << "Yes\n";
    }
    else
        cout << "No\n";
}

// driver code
int main()
{
    string S1 = "abbca", S2 = "acabb";
    checkToMakeEqual(S1, S2);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# function to count inversion
# count of the string
def inversionCount(s):

    # for storing frequency
    freq = [0 for _ in range(26)]
    inv = 0
    for i in range(len(s)):

        # we'll add all the characters
        # which are less than the ith
        # character before i.
        temp = 0
        for j in range(ord(s[i]) - ord('a')):

            # adding the count to
            # inversion count
            temp += freq[j]

        inv += (i - temp)

        # updating the character in
        # the frequency array
        freq[ord(s[i]) - ord('a')] += 1
    return inv

# function to check whether
# any of the string have a
# repeated character
def haveRepeated(S1, S2):
    freq = [0 for _ in range(26)]
    for i in range(len(S1)):
        if freq[ord(S1[i]) - ord('a')] > 0:
            return 1
        freq[ord(S1[i]) - ord('a')] += 1

    for i in range(26):
        freq[i] = 0

    for i in range(len(S2)):
        if freq[ord(S2[i]) - ord('a')] > 0:
            return 1
        freq[ord(S2[i]) - ord('a')] += 1

    return 0

# function to check whether
# the string S1 and S2 can
# be made equal by reversing
# sub strings ofsame size in
# both strings
def checkToMakeEqual(S1, S2):

    # frequency array to check
    # whether both string have
    # same character or not
    freq = [0 for _ in range(26)]

    for i in range(len(S1)):

        # adding the frequency;
        freq[ord(S1[i]) - ord('a')] += 1

    flag = 0
    for i in range(len(S2)):
        if freq[ord(S2[i]) - ord('a')] == 0:

            # if the character is not in S1
            flag = 1
            break

        # decrementing the frequency
        freq[ord(S2[i]) - ord('a')] -= 1

    if flag == 1:

        # If both string does not
        # have same characters or not
        print("No")
        return

    # finding inversion count of
    # both strings
    invCount1 = inversionCount(S1)
    invCount2 = inversionCount(S2)

    if ((invCount1 == invCount2) or
       ((invCount1 % 2) == (invCount2 % 2)) or
         haveRepeated(S1, S2) == 1):

        # If inversion count is same,
        # or have same parity
        # or if any of the string
        # have a repeated character
        # then the answer is Yes else No
        print("Yes")
    else:
        print("No")

# Driver Code
S1 = "abbca"
S2 = "acabb"

checkToMakeEqual(S1, S2)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count inversion
// count of the string
static int inversionCount(String s)
{

    // For storing frequency
    int[] freq = new int[26];
    int inv = 0;
    for(int i = 0; i < s.length(); i++)
    {
        int temp = 0;

        // Add all the characters which
        // are less than the ith character
        // before i.
        for(int j = 0;
                j < (int)(s.charAt(i) - 'a');
                j++)

        // Adding the count to inversion
        // count
        temp += freq[j];
        inv += (i - temp);

        // Updating the character in
        // the frequency array
        freq[s.charAt(i) - 'a']++;
    }
    return inv;
}

// Function to check whether any
// of the string have a repeated
// character
static boolean haveRepeated(String S1,
                            String S2)
{
    int[] freq = new int[26];
    for(char i : S1.toCharArray())
    {
        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    }

    for(int i = 0; i < 26; i++)
        freq[i] = 0;

    for(char i : S2.toCharArray())
    {
        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    }
    return false;
}

// Function to check whether the
// string S1 and S2 can be made
// equal by reversing sub strings
// of same size in both strings
static void checkToMakeEqual(String S1,
                             String S2)
{

    // Frequency array to check
    // whether both string have
    // same character or not
    int[] freq = new int[26];
    for(int i = 0; i < S1.length(); i++)
    {

        // Adding the frequency;
        freq[S1.charAt(i) - 'a']++;
    }

    boolean flag = false;
    for(int i = 0; i < S2.length(); i++)
    {
        if (freq[S2.charAt(i) - 'a'] == 0)
        {

            // If the character is not in S1
            flag = true;
            break;
        }

        // Decrementing the frequency
        freq[S2.charAt(i) - 'a']--;
    }

    if (flag == true)
    {

        // If both string doesnot
        // have same characters or not
        System.out.println("No");
        return;
    }

    // Finding inversion count
    // of both strings
    int invCount1 = inversionCount(S1);
    int invCount2 = inversionCount(S2);

    if (invCount1 == invCount2 ||
       (invCount1 & 1) == (invCount2 & 1) ||
        haveRepeated(S1, S2))
    {

        // If inversion count is same,
        // or have same parity or if
        // any of the string have a
        // repeated character then
        // the answer is Yes else No
        System.out.println("Yes");
    }
    else
    System.out.println("No");
}

// Driver Code
public static void main (String[] args)
{
    String S1 = "abbca", S2 = "acabb";

    checkToMakeEqual(S1, S2);
}
}

// This code is contributed by offbeat
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count inversion
// count of the string
static int inversionCount(String s)
{

    // For storing frequency
    int[] freq = new int[26];
    int inv = 0;
    for(int i = 0; i < s.Length; i++)
    {
        int temp = 0;

        // Add all the characters which
        // are less than the ith character
        // before i.
        for(int j = 0;
                j < (int)(s[i] - 'a');
                j++)

        // Adding the count to inversion
        // count
        temp += freq[j];
        inv += (i - temp);

        // Updating the character in
        // the frequency array
        freq[s[i] - 'a']++;
    }
    return inv;
}

// Function to check whether any
// of the string have a repeated
// character
static bool haveRepeated(String S1,
                            String S2)
{
    int[] freq = new int[26];
    foreach(char i in S1.ToCharArray())
    {
        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    }

    for(int i = 0; i < 26; i++)
        freq[i] = 0;

    foreach(char i in S2.ToCharArray())
    {
        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    }
    return false;
}

// Function to check whether the
// string S1 and S2 can be made
// equal by reversing sub strings
// of same size in both strings
static void checkToMakeEqual(String S1,
                             String S2)
{

    // Frequency array to check
    // whether both string have
    // same character or not
    int[] freq = new int[26];
    for(int i = 0; i < S1.Length; i++)
    {

        // Adding the frequency;
        freq[S1[i] - 'a']++;
    }

    bool flag = false;
    for(int i = 0; i < S2.Length; i++)
    {
        if (freq[S2[i] - 'a'] == 0)
        {

            // If the character is not in S1
            flag = true;
            break;
        }

        // Decrementing the frequency
        freq[S2[i] - 'a']--;
    }

    if (flag == true)
    {

        // If both string doesnot
        // have same characters or not
        Console.WriteLine("No");
        return;
    }

    // Finding inversion count
    // of both strings
    int invCount1 = inversionCount(S1);
    int invCount2 = inversionCount(S2);

    if (invCount1 == invCount2 ||
       (invCount1 & 1) == (invCount2 & 1) ||
        haveRepeated(S1, S2))
    {

        // If inversion count is same,
        // or have same parity or if
        // any of the string have a
        // repeated character then
        // the answer is Yes else No
        Console.WriteLine("Yes");
    }
    else
    Console.WriteLine("No");
}

// Driver Code
public static void Main(String[] args)
{
    String S1 = "abbca", S2 = "acabb";

    checkToMakeEqual(S1, S2);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// function to count inversion
// count of the string
function inversionCount(s)
{

    // For storing frequency
    var freq = Array(26).fill(0);
    var inv = 0;
    for(var i = 0; i < s.length; i++)
    {
        var temp = 0;

        // Add all the characters which
        // are less than the ith character
        // before i.
        for(var j = 0;
                j < String.fromCharCode(
                      s[i].charCodeAt(0) -
                       'a'.charCodeAt(0)); j++)

            // Adding the count to inversion
            // count
            temp += freq[j];

        inv += (i - temp);

        // Updating the character in
        // the frequency array
        freq[s[i] - 'a']++;
    }
    return inv;
}

// Function to check whether any
// of the string have a repeated
// character
function haveRepeated(S1, S2)
{
    var freq = Array(26).fill(0);

    S1.forEach(i => {

        if (freq[i - 'a'] > 0)
            return true;
        freq[i - 'a']++;
    });

    for(var i = 0; i < 26; i++)
        freq[i] = 0;

    S2.split('').forEach(i => {

        if (freq[i - 'a'] > 0)
            return true;

        freq[i - 'a']++;
    });
    return false;
}

// Function to check whether the
// string S1 and S2 can be made
// equal by reversing sub strings
// of same size in both strings
function checkToMakeEqual(S1, S2)
{

    // Frequency array to check
    // whether both string have
    // same character or not
    var freq = Array(26).fill(0);

    for(var i = 0; i < S1.length; i++)
    {

        // Adding the frequency;
        freq[S1[i] - 'a']++;
    }

    var flag = 0;
    for(var i = 0; i < S2.length; i++)
    {
        if (freq[S2[i] - 'a'] == 0)
        {

            // If the character is not in S1
            flag = true;
            break;
        }

        // Decrementing the frequency
        freq[S2[i] - 'a']--;
    }

    if (flag == true)
    {

        // If both string doesnot
        // have same characters or not
        document.write("No<br>");
        return;
    }

    // Finding inversion count
    // of both strings
    var invCount1 = inversionCount(S1);
    var invCount2 = inversionCount(S2);

    if (invCount1 == invCount2 ||
       (invCount1 & 1) == (invCount2 & 1) ||
       haveRepeated(S1, S2))
    {

        // If inversion count is same,
        // or have same parity or if
        // any of the string have a
        // repeated character then
        // the answer is Yes else No
        document.write("Yes<br>");
    }
    else
        document.write("No<br>");
}

// Driver code
var S1 = "abbca", S2 = "acabb";
checkToMakeEqual(S1, S2);

// This code is contributed by itsok

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**

![O(N)      ](img/56c93df2bf6a993c04aac37fd5fe19ee.png "Rendered by QuickLaTeX.com")
**空间复杂度:**
![O(1)      ](img/030ae5c263badcd7c9cff0982bb3749f.png "Rendered by QuickLaTeX.com")