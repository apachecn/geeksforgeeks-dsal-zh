# 将字符串中的每个元音替换为词典中的下一个元音

> 原文:[https://www . geesforgeks . org/将每一个元音都替换为按字典顺序排列的字符串中的下一个元音/](https://www.geeksforgeeks.org/replace-every-vowels-with-lexicographically-next-vowel-in-a-string/)

给定字符串**大小为 **N** 的字符串**，其中包含小写英文字母。任务是用词典学上的下一个直接元音替换每个元音，即，

> “a”将由“e”代替,
> “e”将由“I”代替，
> “I”将由“o”代替，
> “o”将由“u”代替，
> “u”将由“a”代替。

**示例**:

> **输入:** str = "geeksforgeeks"
> **输出:**giiksfurgiks
> **解释:**
> e 被 I 替换
> o 被 u 替换
> 所以最终的字符串将是“giiksfurgiks”。
> 
> **输入:**str = " gfg "
> T3】输出: gfg

**方法:**我们将创建一个大小为 5 的 Hashing 来存储所有元音，这样就可以很容易地对每个元音进行替换。

*   创建一个地图并存储所有元音。
*   从左到右迭代字符串元素。
*   如果字符串元素是一个元音，则将其更改为下一个元音。
*   最后，打印最后一个字符串。

下面是上述方法的实现:

## C++14

```
// C++ program to convert all the vowels in
// in the string to the next vowel

#include <bits/stdc++.h>
using namespace std;

// Function to replace every vowel
// with next vowel lexicographically
string print_next_vovel_string(string str)
{

    // Storing the vowels in the map with
    // custom numbers showing  their index
    map<char, int> m;
    m['a'] = 0;
    m['e'] = 1;
    m['i'] = 2;
    m['o'] = 3;
    m['u'] = 4;
    char arr[5] = { 'a', 'e', 'i', 'o', 'u' };

    int N = str.length();

    // Iterate over the string
    for (int i = 0; i < N; i++) {

        char c = str[i];

        // If the current character is a vowel
        // Find the index in Hash and
        // Replace it with next vowel from Hash
        if (c == 'a' || c == 'e' || c == 'i'
            || c == 'o' || c == 'u') {

            int index = m + 1;
            int newindex = index % 5;
            str[i] = arr[newindex];
        }
    }

    return str;
}

// Driver function
int main()
{
    string str = "geeksforgeeks";

    cout << print_next_vovel_string(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert all the vowels in
// in the String to the next vowel
import java.util.*;

class GFG{

// Function to replace every vowel
// with next vowel lexicographically
static String print_next_vovel_String(char []str)
{

    // storing the vowels in the map with
    // custom numbers showing their index
    HashMap<Character,
            Integer> m = new HashMap<Character,
                                     Integer>();
    m.put('a', 0);
    m.put('e', 1);
    m.put('i', 2);
    m.put('o', 3);
    m.put('u', 4);

    char arr[] = { 'a', 'e', 'i', 'o', 'u' };

    int N = str.length;

    // Iterate over the String
    for(int i = 0; i < N; i++)
    {
        char c = str[i];

        // If the current character is a vowel
        // Find the index in Hash and
        // Replace it with next vowel from Hash
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u')
        {
            int index = m.get(c) + 1;
            int newindex = index % 5;

            str[i] = arr[newindex];
        }
    }
    return String.valueOf(str);
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";

    System.out.print(print_next_vovel_String(
        str.toCharArray()));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to convert
# all the vowels in the string
# to the next vowel

# Function to replace every vowel
# with next vowel lexicographically
def print_next_vovel_string(st):

    # Storing the vowels in
    # the map with custom
    # numbers showing  their index
    m = {}
    m['a'] = 0
    m['e'] = 1
    m['i'] = 2
    m['o'] = 3
    m['u'] = 4
    arr = ['a', 'e', 'i', 'o', 'u']

    N = len(st)

    # Iterate over the string
    for i in range (N):

        c = st[i]

        # If the current character
        # is a vowel
        # Find the index in Hash
        # and Replace it with next
        # vowel from Hash
        if (c == 'a' or c == 'e' or
            c == 'i'or c == 'o' or
            c == 'u'):           
            index = m[st[i]] + 1
            newindex = index % 5
            st = st.replace(st[i], arr[newindex], 1)

    return st

# Driver function
if __name__ == "__main__":
    st = "geeksforgeeks"
    print (print_next_vovel_string(st))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to convert all the vowels in
// in the String to the next vowel
using System;
using System.Collections.Generic;

class GFG{

// Function to replace every vowel
// with next vowel lexicographically
static String print_next_vovel_String(char []str)
{

    // Storing the vowels in the map with
    // custom numbers showing their index
    Dictionary<char,
               int> m = new Dictionary<char,
                                       int>();
    m.Add('a', 0);
    m.Add('e', 1);
    m.Add('i', 2);
    m.Add('o', 3);
    m.Add('u', 4);

    char []arr = { 'a', 'e', 'i', 'o', 'u' };

    int N = str.Length;

    // Iterate over the String
    for(int i = 0; i < N; i++)
    {
        char c = str[i];

        // If the current character is a vowel
        // Find the index in Hash and
        // Replace it with next vowel from Hash
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u')
        {
            int index = m + 1;
            int newindex = index % 5;

            str[i] = arr[newindex];
        }
    }
    return String.Join("", str);
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";

    Console.Write(print_next_vovel_String(
        str.ToCharArray()));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript program to convert
      // all the vowels in the string
      // to the next vowel
      // Function to replace every vowel
      // with next vowel lexicographically
      function print_next_vovel_string(st) {
        // Storing the vowels in
        // the map with custom
        // numbers showing their index
        var m = {};
        m["a"] = 0;
        m["e"] = 1;
        m["i"] = 2;
        m["o"] = 3;
        m["u"] = 4;
        var arr = ["a", "e", "i", "o", "u"];

        var N = st.length;

        // Iterate over the string
        for (let i = 0; i < N; i++) {
          var c = st[i];

          // If the current character
          // is a vowel
          // Find the index in Hash
          // and Replace it with next
          // vowel from Hash
          if (c === "a" || c === "e" || c === "i" || c === "o" || c === "u") {
            index = m[st[i]] + 1;
            newindex = index % 5;
            st = st.replace(st[i], arr[newindex]);
          }
        }
        return st;
      }

      // Driver function
      var st = "geeksforgeeks";
      document.write(print_next_vovel_string(st));
    </script>
```

**Output:** 

```
giiksfurgiiks
```

***时间复杂度:**O(N)*
T5**辅助空间:** O (1)