# 按字母顺序打印每个字符的频率

> 原文:[https://www . geesforgeks . org/print-按字母顺序打印每个字符的频率/](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)

给定一个字符串 **str** ，任务是按字母顺序打印 **str** 的每个字符的频率。
**例:**

> **输入:** str = "aabccccddd"
> **输出:** a2b1c4d3
> 由于已经按字母顺序排列，所以返回每个字符的字符频率
> 。
> **输入:**str = " geeksforgeeks "
> **输出:** e4f1g2k2o1r1s2

**进场:**

1.  创建一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储给定字符串中每个字符的频率。
2.  遍历字符串并检查字符是否出现在地图中。
3.  如果字符不存在，将它以 1 作为初始值插入到地图中，否则将其频率增加 1。
4.  最后，按字母顺序打印每个字符的频率。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to print the frequency
// of each of the characters of
// s in alphabetical order
void compressString(string s, int n)
{
    // To store the frequency
    // of the characters
    int freq[MAX] = { 0 };

    // Update the frequency array
    for (int i = 0; i < n; i++) {
        freq[s[i] - 'a']++;
    }

    // Print the frequency in alphatecial order
    for (int i = 0; i < MAX; i++) {

        // If the current alphabet doesn't
        // appear in the string
        if (freq[i] == 0)
            continue;

        cout << (char)(i + 'a') << freq[i];
    }
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    int n = s.length();

    compressString(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int MAX = 26;

    // Function to print the frequency
    // of each of the characters of
    // s in alphabetical order
    static void compressString(String s, int n)
    {
        // To store the frequency
        // of the characters
        int freq[] = new int[MAX] ;

        // Update the frequency array
        for (int i = 0; i < n; i++)
        {
            freq[s.charAt(i) - 'a']++;
        }

        // Print the frequency in alphatecial order
        for (int i = 0; i < MAX; i++)
        {

            // If the current alphabet doesn't
            // appear in the string
            if (freq[i] == 0)
                continue;

            System.out.print((char)(i + 'a') +""+ freq[i]);
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "geeksforgeeks";
        int n = s.length();

        compressString(s, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26;

# Function to print the frequency
# of each of the characters of
# s in alphabetical order
def compressString(s, n) :

    # To store the frequency
    # of the characters
    freq = [ 0 ] * MAX;

    # Update the frequency array
    for i in range(n) :
        freq[ord(s[i]) - ord('a')] += 1;

    # Print the frequency in alphatecial order
    for i in range(MAX) :

        # If the current alphabet doesn't
        # appear in the string
        if (freq[i] == 0) :
            continue;

        print((chr)(i + ord('a')),freq[i],end = " ");

# Driver code
if __name__ == "__main__" :

    s = "geeksforgeeks";
    n = len(s);

    compressString(s, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAX = 26;

    // Function to print the frequency
    // of each of the characters of
    // s in alphabetical order
    static void compressString(string s, int n)
    {
        // To store the frequency
        // of the characters
        int []freq = new int[MAX] ;

        // Update the frequency array
        for (int i = 0; i < n; i++)
        {
            freq[s[i] - 'a']++;
        }

        // Print the frequency in alphatecial order
        for (int i = 0; i < MAX; i++)
        {

            // If the current alphabet doesn't
            // appear in the string
            if (freq[i] == 0)
                continue;

            Console.Write((char)(i + 'a') +""+ freq[i]);
        }
    }

    // Driver code
    public static void Main()
    {
        string s = "geeksforgeeks";
        int n = s.Length;

        compressString(s, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    let MAX = 26;

    // Function to print the frequency
    // of each of the characters of
    // s in alphabetical order
    function compressString(s, n)
    {
        // To store the frequency
        // of the characters
        let freq = new Array(MAX);
        freq.fill(0);

        // Update the frequency array
        for (let i = 0; i < n; i++)
        {
            freq[s[i].charCodeAt() - 'a'.charCodeAt()]++;
        }

        // Print the frequency in alphatecial order
        for (let i = 0; i < MAX; i++)
        {

            // If the current alphabet doesn't
            // appear in the string
            if (freq[i] == 0)
                continue;

            document.write(String.fromCharCode(i +
            'a'.charCodeAt()) +""+ freq[i]);
        }
    }

    let s = "geeksforgeeks";
    let n = s.length;

    compressString(s, n);

</script>
```

**Output:** 

```
e4f1g2k2o1r1s2
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)