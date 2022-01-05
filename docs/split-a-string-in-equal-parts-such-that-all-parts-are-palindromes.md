# 将一个字符串等分，使所有部分都是回文

> 原文:[https://www . geesforgeks . org/split-a-string-in-equal-part-so-all-part-is-回文/](https://www.geeksforgeeks.org/split-a-string-in-equal-parts-such-that-all-parts-are-palindromes/)

给定一个字符串 **str** ，任务是将该字符串分割成**最小**部分，这样每个部分的长度都相同，并且每个部分都是一个回文。打印所需数量的零件。
**例:**

> **输入:**str = " civic ob "
> **输出:**8
> “b”“b”“c”“c”“I”“I”“v”“o”为所需分区。“思域”和“bob”也是回文，但它们的长度不相等
> **输入:** str = "noonpeep"
> **输出:** 1

**进场:**

*   统计出现的奇数字符数，并存储在**计数奇数**中。
*   将所有偶出现字符的频率相加并存储在**sumever**中。
*   因为，不超过一个奇数频率字符可以是同一个回文的一部分。所以，如果 **(sumEven / 2) % countOdd = 0** 那么答案就是 **countOdd** 作为 **sumEven** 可以分为 **countOdd** 部分。
*   否则，我们仍然可以将出现的奇数字符分成回文对。例如，如果字符 **a** 出现 **3** 次，即 **aaa** ，那么 **aa** 可以是某个回文的一部分，而留下 **a** 为奇数(不影响原频率)。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the frequency array
// for the given string
int* getFrequencies(string str)
{
    static int freq[26] = { 0 };

    for (int i = 0; i < str.length(); i++) {
        freq[str[i] - 'a']++;
    }

    return freq;
}

// Function to return the required count
int countMinParts(string str)
{

    int n = str.length();
    int *freq = getFrequencies(str);

    vector<int> oddFreq, evenFreq;

    int i, sumEven = 0;

    for (i = 0; i < 26; i++) {
        if (freq[i] == 0)
            continue;

        // Add frequencies of the even appearing
        // characters
        if (freq[i] % 2 == 0)
            evenFreq.push_back(freq[i]);

        // Count of the characters that appeared
        // odd number of times
        else
            oddFreq.push_back(freq[i]);
    }

    for (i = 0; i < evenFreq.size(); i++) {
        sumEven += evenFreq[i];
    }

    // If there are no characters with odd frequency
    if (oddFreq.size() == 0)
        return 1;

    // If there are no characters with even frequency
    if (sumEven == 0) {

        // Only a single character with odd frequency
        if (oddFreq.size() == 1)
            return 1;

        // More than 1 character with odd frequency
        // string isn't a palindrome
        return 0;
    }

    i = 0;

    // All odd appearing characters can also contribute to
    // the even length palindrome if one character
    // is removed from the frequency leaving it as even
    while (i < oddFreq.size()) {

        // If k palindromes are possible where k
        // is the number of characters with odd frequency
        if ((sumEven / 2) % oddFreq.size() == 0)
            return oddFreq.size();

        // Current character can no longer be an element
        // in a string other than the mid character
        if (oddFreq[i] == 1) {
            i++;
            continue;
        }

        // If current character has odd frequency > 1
        // take two characters which can be used in
        // any of the parts
        sumEven += 2;

        // Update the frequency
        oddFreq[i] = oddFreq[i] - 2;
    }

    // If not possible, then every character of the
    // string will act as a separate palindrome
    return n;
}

// Driver code
int main()
{

    string s = "noonpeep";

    cout<<countMinParts(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class GFG {

    // Function to return the frequency array
    // for the given string
    static int[] getFrequencies(String str)
    {
        int freq[] = new int[26];
        for (int i = 0; i < str.length(); i++) {
            freq[str.charAt(i) - 'a']++;
        }
        return freq;
    }

    // Function to return the required count
    static int countMinParts(String str)
    {

        int n = str.length();
        int freq[] = getFrequencies(str);
        List<Integer> oddFreq = new ArrayList<>();
        List<Integer> evenFreq = new ArrayList<>();

        int i, sumEven = 0;

        for (i = 0; i < 26; i++) {
            if (freq[i] == 0)
                continue;

            // Add frequencies of the even appearing
            // characters
            if (freq[i] % 2 == 0)
                evenFreq.add(freq[i]);

            // Count of the characters that appeared
            // odd number of times
            else
                oddFreq.add(freq[i]);
        }

        for (i = 0; i < evenFreq.size(); i++) {
            sumEven += evenFreq.get(i);
        }

        // If there are no characters with odd frequency
        if (oddFreq.size() == 0)
            return 1;

        // If there are no characters with even frequency
        if (sumEven == 0) {

            // Only a single character with odd frequency
            if (oddFreq.size() == 1)
                return 1;

            // More than 1 character with odd frequency
            // string isn't a palindrome
            return 0;
        }

        i = 0;

        // All odd appearing characters can also contribute to
        // the even length palindrome if one character
        // is removed from the frequency leaving it as even
        while (i < oddFreq.size()) {

            // If k palindromes are possible where k
            // is the number of characters with odd frequency
            if ((sumEven / 2) % oddFreq.size() == 0)
                return oddFreq.size();

            // Current character can no longer be an element
            // in a string other than the mid character
            if (oddFreq.get(i) == 1) {
                i++;
                continue;
            }

            // If current character has odd frequency > 1
            // take two characters which can be used in
            // any of the parts
            sumEven += 2;

            // Update the frequency
            oddFreq.set(i, oddFreq.get(i) - 2);
        }

        // If not possible, then every character of the
        // string will act as a separate palindrome
        return n;
    }

    // Driver code
    public static void main(String[] args)
    {

        String s = "noonpeep";

        System.out.println(countMinParts(s));
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the frequency array
# for the given string
def getFrequencies(string) :
        freq = [0] * 26

        for i in range(len(string)) :
                freq[ord(string[i]) -
                     ord('a')] += 1

        return freq

# Function to return the required count
def countMinParts(string) :
        n = len(string)
        freq = getFrequencies(string)
        oddFreq = []
        evenFreq = []

        sumEven = 0

        for i in range(26) :

                if freq[i] == 0 :
                    continue

                # Add frequencies of the even
                # appearing characters
                if freq[i] % 2 == 0 :
                        evenFreq.append(freq[i])

                # Count of the characters that
                # appeared odd number of times
                else :
                        oddFreq.append(freq[i])

        for i in range(len(evenFreq)) :
                sumEven += evenFreq[i]

        # If there are no characters with
        # odd frequency
        if len(oddFreq) == 0 :
                return 1

        # If there are no characters with
        # even frequency
        if sumEven == 0 :

                # Only a single character with
                # odd frequency
                if len(oddFreq) == 1:
                        return 1

                # More than 1 character with odd
                # frequency string isn't a palindrome
                return 0

        i = 0

        # All odd appearing characters can also
        # contribute to the even length palindrome
        # if one character is removed from the
        # frequency leaving it as even
        while(i < len(oddFreq)) :

                # If k palindromes are possible where
                # k is the number of characters with
                # odd frequency
                if ((sumEven / 2) % len(oddFreq) == 0) :
                        return len(oddFreq)

                # Current character can no longer be
                # an element in a string other than
                # the mid character
                if (oddFreq[i] == 1) :
                        i += 1
                        continue

                # If current character has odd frequency > 1
                # take two characters which can be used in
                # any of the parts
                sumEven += 2

                # Update the frequency
                oddFreq[i] = oddFreq[i] - 2

        # If not possible, then every character of the
        # string will act as a separate palindrome
        return n

# Driver code
if __name__ == "__main__" :

    s = "noonpeep"

    print(countMinParts(s))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the frequency array
    // for the given string
    static int[] getFrequencies(String str)
    {
        int []freq = new int[26];
        for (int i = 0; i < str.Length; i++)
        {
            freq[str[i] - 'a']++;
        }
        return freq;
    }

    // Function to return the required count
    static int countMinParts(String str)
    {

        int n = str.Length;
        int []freq = getFrequencies(str);
        List<int> oddFreq = new List<int>();
        List<int> evenFreq = new List<int>();

        int i, sumEven = 0;

        for (i = 0; i < 26; i++)
        {
            if (freq[i] == 0)
                continue;

            // Add frequencies of the even appearing
            // characters
            if (freq[i] % 2 == 0)
                evenFreq.Add(freq[i]);

            // Count of the characters that appeared
            // odd number of times
            else
                oddFreq.Add(freq[i]);
        }

        for (i = 0; i < evenFreq.Count; i++)
        {
            sumEven += evenFreq[i];
        }

        // If there are no characters with odd frequency
        if (oddFreq.Count == 0)
            return 1;

        // If there are no characters with even frequency
        if (sumEven == 0)
        {

            // Only a single character with odd frequency
            if (oddFreq.Count == 1)
                return 1;

            // More than 1 character with odd frequency
            // string isn't a palindrome
            return 0;
        }

        i = 0;

        // All odd appearing characters can also contribute to
        // the even length palindrome if one character
        // is removed from the frequency leaving it as even
        while (i < oddFreq.Count)
        {

            // If k palindromes are possible where k
            // is the number of characters with odd frequency
            if ((sumEven / 2) % oddFreq.Count == 0)
                return oddFreq.Count;

            // Current character can no longer be an element
            // in a string other than the mid character
            if (oddFreq[i] == 1)
            {
                i++;
                continue;
            }

            // If current character has odd frequency > 1
            // take two characters which can be used in
            // any of the parts
            sumEven += 2;

            // Update the frequency
            oddFreq.Insert(i, oddFreq[i] - 2);
        }

        // If not possible, then every character of the
        // string will act as a separate palindrome
        return n;
    }

    // Driver code
    public static void Main(String[] args)
    {

        String s = "noonpeep";

        Console.WriteLine(countMinParts(s));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the frequency array
    // for the given string
function getFrequencies(str)
{
    let freq = new Array(26);
    for(let i=0;i<26;i++)
        freq[i]=0;
        for (let i = 0; i < str.length; i++) {
            freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }
        return freq;
}

// Function to return the required count
function countMinParts(str)
{
        let n = str.length;
        let freq = getFrequencies(str);
        let oddFreq = [];
        let evenFreq = [];

        let i, sumEven = 0;

        for (i = 0; i < 26; i++) {
            if (freq[i] == 0)
                continue;

            // Add frequencies of the even appearing
            // characters
            if (freq[i] % 2 == 0)
                evenFreq.push(freq[i]);

            // Count of the characters that appeared
            // odd number of times
            else
                oddFreq.push(freq[i]);
        }

        for (i = 0; i < evenFreq.length; i++) {
            sumEven += evenFreq[i];
        }

        // If there are no characters with odd frequency
        if (oddFreq.length == 0)
            return 1;

        // If there are no characters with even frequency
        if (sumEven == 0) {

            // Only a single character with odd frequency
            if (oddFreq.length == 1)
                return 1;

            // More than 1 character with odd frequency
            // string isn't a palindrome
            return 0;
        }

        i = 0;

        // All odd appearing characters can also contribute to
        // the even length palindrome if one character
        // is removed from the frequency leaving it as even
        while (i < oddFreq.length) {

            // If k palindromes are possible where k
            // is the number of characters with odd frequency
            if ((sumEven / 2) % oddFreq.length == 0)
                return oddFreq.length;

            // Current character can no longer be an element
            // in a string other than the mid character
            if (oddFreq[i] == 1) {
                i++;
                continue;
            }

            // If current character has odd frequency > 1
            // take two characters which can be used in
            // any of the parts
            sumEven += 2;

            // Update the frequency
            oddFreq[i]= oddFreq[i] - 2;
        }

        // If not possible, then every character of the
        // string will act as a separate palindrome
        return n;
}

 // Driver code
let s = "noonpeep";

document.write(countMinParts(s));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
1
```