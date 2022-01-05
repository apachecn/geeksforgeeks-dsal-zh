# 通过用字母替换字符来修改字符串，字母与字符的距离等于其频率

> 原文:[https://www . geeksforgeeks . org/通过字母替换字符来修改字符串，字母与字符的距离等于其频率/](https://www.geeksforgeeks.org/modify-string-by-replacing-characters-by-alphabets-whose-distance-from-that-character-is-equal-to-its-frequency/)

给定一个由 **N** 个小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过用字母替换每个字符来修改字符串 **S** ，该字母与字符的圆形距离等于字符在 **S** 中的出现频率。

**示例:**

> **输入:** S =【极客】
> T3】输出:hgglt
> T6】说明:T8】对字符串 S 做了如下修改:
> 
> *   字符串中“g”的频率是 1。因此，“g”被“h”代替。
> *   字符串中“e”的频率是 2。因此，“e”被“g”所取代。
> *   字符串中“e”的频率是 2。因此，“e”被“g”所取代。
> *   字符串中“k”的频率是 1。因此，“k”被转换为“k”+1 =“l”。
> *   字符串中“s”的频率为 1。因此，“s”被转换为“s”+1 =“t”。
> 
> 因此，修改后的字符串 S 为“hgglt”。
> 
> **输入:** S =【爵士】
> **输出:**【kbbb】

**方法:**给定的问题可以通过维护[频率数组来解决，该数组存储字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)中每个字符的出现次数。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，**freq【26】**，最初所有元素为 **0** ，存储字符串每个字符的[频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   [遍历给定的字符串](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **S** ，将数组**freq【】**中每个字符**S【I】**的频率增加 **1** 。
*   [遍历字符串](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **S** 使用变量 **i** 并执行以下步骤:
    *   将要添加到 **S[i]** 的值存储在变量中，**将**添加为 **(freq[i] % 26)** 。
    *   如果将**的值加到 **S[i]** 后， **S[i]** 没有超过字符 **z** ，则更新 **S[i]** 为 **S[i] +加**。**
    *   否则，将**的值更新为**(S[I]+add–z)**，然后将 **S[i]** 设置为**(a+add–1)**。**
*   完成上述步骤后，[打印修改后的字符串](https://www.geeksforgeeks.org/print-string-specified-character-occurred-given-no-times/) **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify string by replacing
// characters by the alphabet present at
// distance equal to frequency of the string
void addFrequencyToCharacter(string s)
{
    // Stores frequency of characters
    int frequency[26] = { 0 };

    // Stores length of the string
    int n = s.size();

    // Traverse the given string S
    for (int i = 0; i < n; i++) {

        // Increment frequency of
        // current character by 1
        frequency[s[i] - 'a'] += 1;
    }

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // Store the value to be added
        // to the current character
        int add = frequency[s[i] - 'a'] % 26;

        // Check if after adding the
        // frequency, the character is
        // less than 'z' or not
        if (int(s[i]) + add <= int('z'))
            s[i] = char(int(s[i]) + add);

        // Otherwise, update the value of
        // add so that s[i] doesn't exceed 'z'
        else {
            add = (int(s[i]) + add) - (int('z'));
            s[i] = char(int('a') + add - 1);
        }
    }

    // Print the modified string
    cout << s;
}

// Driver Code
int main()
{
    string str = "geeks";
    addFrequencyToCharacter(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to modify string by replacing
// characters by the alphabet present at
// distance equal to frequency of the string
static void addFrequencyToCharacter(char[] s)
{

    // Stores frequency of characters
    int frequency[] = new int[26];

    // Stores length of the string
    int n = s.length;

    // Traverse the given string S
    for(int i = 0; i < n; i++)
    {

        // Increment frequency of
        // current character by 1
        frequency[s[i] - 'a'] += 1;
    }

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // Store the value to be added
        // to the current character
        int add = frequency[s[i] - 'a'] % 26;

        // Check if after adding the
        // frequency, the character is
        // less than 'z' or not
        if ((int)(s[i]) + add <= (int)('z'))
            s[i] = (char)((int)(s[i]) + add);

        // Otherwise, update the value of
        // add so that s[i] doesn't exceed 'z'
        else
        {
            add = ((int)(s[i]) + add) - ((int)('z'));
            s[i] = (char)((int)('a') + add - 1);
        }
    }

    // Print the modified string
    System.out.println(s);
}

// Driver Code
public static void main(String[] args)
{
    String str = "geeks";

    addFrequencyToCharacter(str.toCharArray());
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to modify string by replacing
# characters by the alphabet present at
# distance equal to frequency of the string
def addFrequencyToCharacter(s):

    # Stores frequency of characters
    frequency = [0] * 26

    # Stores length of the string
    n = len(s)

    # Traverse the given string S
    for i in range(n):

        # Increment frequency of
        # current character by 1
        frequency[ord(s[i]) - ord('a')] += 1

    # Traverse the string
    for i in range(n):

        # Store the value to be added
        # to the current character
        add = frequency[ord(s[i]) - ord('a')] % 26

        # Check if after adding the
        # frequency, the character is
        # less than 'z' or not
        if (ord(s[i]) + add <= ord('z')):
            s[i] = chr(ord(s[i]) + add)

        # Otherwise, update the value of
        # add so that s[i] doesn't exceed 'z'
        else:
            add = (ord(s[i]) + add) - (ord('z'))
            s[i] = chr(ord('a') + add - 1)

    # Print the modified string
    print("".join(s))

# Driver Code
if __name__ == '__main__':

    str = "geeks"

    addFrequencyToCharacter([i for i in str])

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to modify string by replacing
// characters by the alphabet present at
// distance equal to frequency of the string
static void addFrequencyToCharacter(char[] s)
{

    // Stores frequency of characters
    int[] frequency = new int[26];

    // Stores length of the string
    int n = s.Length;

    // Traverse the given string S
    for(int i = 0; i < n; i++)
    {

        // Increment frequency of
        // current character by 1
        frequency[s[i] - 'a'] += 1;
    }

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // Store the value to be added
        // to the current character
        int add = frequency[s[i] - 'a'] % 26;

        // Check if after adding the
        // frequency, the character is
        // less than 'z' or not
        if ((int)(s[i]) + add <= (int)('z'))
            s[i] = (char)((int)(s[i]) + add);

        // Otherwise, update the value of
        // add so that s[i] doesn't exceed 'z'
        else
        {
            add = ((int)(s[i]) + add) - ((int)('z'));
            s[i] = (char)((int)('a') + add - 1);
        }
    }

    // Print the modified string
    Console.WriteLine(s);
}

// Driver Code
public static void Main(string[] args)
{
    string str = "geeks";

    addFrequencyToCharacter(str.ToCharArray());
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to modify string by replacing
      // characters by the alphabet present at
      // distance equal to frequency of the string
      function addFrequencyToCharacter(s) {
        // Stores frequency of characters
        var frequency = new Array(26).fill(0);

        // Stores length of the string
        var n = s.length;

        // Traverse the given string S
        for (var i = 0; i < n; i++) {
          // Increment frequency of
          // current character by 1
          frequency[s[i].charCodeAt(0) - "a".charCodeAt(0)] += 1;
        }

        // Traverse the string
        for (var i = 0; i < n; i++) {
          // Store the value to be added
          // to the current character
          var add = frequency[s[i].charCodeAt(0) - "a".charCodeAt(0)] % 26;

          // Check if after adding the
          // frequency, the character is
          // less than 'z' or not
          if (s[i].charCodeAt(0) + add <= "z".charCodeAt(0))
            s[i] = String.fromCharCode(s[i].charCodeAt(0) + add);
          // Otherwise, update the value of
          // add so that s[i] doesn't exceed 'z'
          else {
            add = s[i].charCodeAt(0) + add - "z".charCodeAt(0);
            s[i] = String.fromCharCode("a".charCodeAt(0) + add - 1);
          }
        }

        // Print the modified string
        document.write(s.join("") + "<br>");
      }

      // Driver Code
      var str = "geeks";
      addFrequencyToCharacter(str.split(""));
</script>
```

**Output:** 

```
hgglt
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)