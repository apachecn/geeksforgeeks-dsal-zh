# 根据字符的 ASCII 值对字符串进行排序

> 原文:[https://www . geesforgeks . org/按字符 ascii 值对字符串进行排序/](https://www.geeksforgeeks.org/sort-the-string-as-per-ascii-values-of-the-characters/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)T2 S，任务是根据它们的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)对字符串进行排序。

**示例:**

> **输入:** S = "Geeks7"
> **输出:** 7Geeks
> **说明:**根据 ASCII 值，首先是整数，然后是大写字母和小字母。
> 
> **输入:**S = " geekesforgeeks "
> T3】输出:fggeeekkors

**方法:**解决这个问题的思路是维护一个数组来存储每个字符的频率，然后在结果字符串中相应地添加它们。因为最多有 **256** 个字符，这使得空间复杂度恒定。按照以下步骤解决此问题:

*   [用值 **0** 初始化大小为 **256** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **freq[]** ，以存储字符串中每个字符的频率。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并将数组**中**s【I】**的计数增加 **1** 。**
*   将字符串 **S** 设为空字符串。
*   [使用变量 **i** 和](https://www.geeksforgeeks.org/range-based-loop-c/)[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**使用变量 **j** 迭代范围**【0，freq【I】)**，并在字符串 **s[]中添加与 **i-th** ASCII 值对应的字符。**
*   执行上述步骤后，打印字符串 **S** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the string based
// on their ASCII values
void sortString(string s)
{
    int N = s.length();

    // Stores the frequency of each
    // character of the string
    vector<int> freq(256, 0);

    // Count and store the frequency
    for (int i = 0; i < N; i++) {
        freq[s[i]]++;
    }

    s = "";

    // Store the result
    for (int i = 0; i < 256; i++) {
        for (int j = 0; j < freq[i]; j++)
            s = s + (char)i;
    }

    // Print the result
    cout << s << "\n";

    return;
}

// Driver Code
int main()
{
    string S = "GeeksForGeeks";
    sortString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.util.*;

class Main
{

// Function to sort the string based
// on their ASCII values
static void sortString(String s)
{
    int N = s.length();

    // Stores the frequency of each
    // character of the string
    int [] freq = new int [256];
    for(int i = 0; i < 256; i++){
        freq[i] = 0;
    }

    // Count and store the frequency
    for (int i = 0; i < N; i++) {
         char character = s.charAt(i);
         int val = (int) character;
        freq[val]++;
    }

    // Store the result
    for (int i = 0; i < 256; i++) {
        for (int j = 0; j < freq[i]; j++)
          //    s = s + (char)i;
            System.out.print((char)i);
    }
}

// Driver Code
public static void main(String [] args)
{
    String S = "GeeksForGeeks";
    sortString(S);
}
}

// This code is contributed by amreshkumar3.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to sort the string based
# on their ASCII values
def sortString(s):
    N = len(s)

    # Stores the frequency of each
    # character of the string
    freq = [0] * 256

    # Count and store the frequency
    for i in range(0, N) :
        freq[ord(s[i])] += 1

    s = ""

    # Store the result
    for i in range(256):
        for j in range(freq[i]):
            s = s + chr(i)

    # Print the result
    print(s)

    return

# Driver Code
S = "GeeksForGeeks"
sortString(S)

# This code is contributed by gfgking.
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

// Function to sort the string based
// on their ASCII values
static void sortString(string s)
{
    int N = s.Length;

    // Stores the frequency of each
    // character of the string
    int [] freq = new int[256];
    for(int i = 0; i < 256; i++){
        freq[i] = 0;
    }

    // Count and store the frequency
    for (int i = 0; i < N; i++) {
         char character = s[i];
         int val = (int) character;
        freq[val]++;
    }

    // Store the result
    for (int i = 0; i < 256; i++) {
        for (int j = 0; j < freq[i]; j++)
          //    s = s + (char)i;
           Console.Write((char)i);
    }
}

    // Driver Code
    public static void Main()
    {
        string S = "GeeksForGeeks";
        sortString(S);
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to sort the string based
       // on their ASCII values
       function sortString(s)
       {
           let N = s.length;

           // Stores the frequency of each
           // character of the string
           let freq = new Array(256).fill(0)

           // Count and store the frequency
           for (let i = 0; i < N; i++) {
               freq[s[i].charCodeAt(0)]++;
           }

           s = "";

           // Store the result
           for (let i = 0; i < 256; i++) {
               for (let j = 0; j < freq[i]; j++)
                   s = s + String.fromCharCode(i);
           }

           // Print the result
           document.write(s);

           return;
       }

       // Driver Code
       let S = "GeeksForGeeks";
       sortString(S);

       // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
FGGeeeekkorss
```

***时间复杂度:**O(256 * N)*
T5**辅助空间:** O(256)

**替代方法:**给定的问题也可以通过使用带有内置的[排序()函数](https://www.geeksforgeeks.org/sort-c-stl/)的[比较器函数](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)根据给定字符串的 ASCII 值对其进行排序来解决。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Comparator Function to sort the given
// string in increasing order of their
// ASCII value
bool cmp(char ch, char chh) { return int(ch) <= int(chh); }

// Function to sort the string based
// on their ASCII values
string sortString(string S)
{
    // Sort the string S
    sort(S.begin(), S.end(), cmp);

    return S;
}

// Driver Code
int main()
{
    string S = "GeeksForGeeks";
    cout << sortString(S);

    return 0;
}
```

**Output:** 

```
FGGeeeekkorss
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*