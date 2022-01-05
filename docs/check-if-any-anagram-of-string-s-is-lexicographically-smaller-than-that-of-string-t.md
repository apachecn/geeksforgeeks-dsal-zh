# 检查字符串 S 的任何字谜在字典上是否小于字符串 T 的字谜

> 原文:[https://www . geesforgeks . org/check-if-any-anagram-of-string-s-is-is-按字典顺序小于-string-t/](https://www.geeksforgeeks.org/check-if-any-anagram-of-string-s-is-lexicographically-smaller-than-that-of-string-t/)

给定两个字符串 **S** 和 **T** ，任务是检查字符串 **S** 的任何变位是否在字典上小于字符串 **T** 的任何变位。

**示例:**

> **输入:** S = "xy "，T = "axy"
> **输出:**是
> **说明:**把 yx 重新排列成 xy，axy 重新排列成 yxa。然后，xy < yxa。
> 
> **输入:** S = "cd "，T = " ABC "
> T3】输出:否

**处理方法:**处理方法是检查字符串 S 的字典最小变位是否小于字符串 t 的字典最大变位，如果是，那么答案是**是**。否则，**不**。现在，按照以下步骤解决这个问题:

1.  排序字符串 **S** 以获得其字典上最小的字谜。
2.  反向排序字符串 **T** 以获得其字典上最大的字谜。
3.  检查新弦 **T** 是否大于新弦 **S** 。如果是，打印**是**。否则，打印**否**。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if any anagram
// of string S is lexicographically
// smaller than any anagram of string T
void CompareAnagrams(string S, string T)
{
    // Sort string S
    sort(S.begin(), S.end());

    // Reverse sort string T
    sort(T.begin(), T.end(), greater<char>());

    // Comparing both the strings
    if (S.compare(T) < 0) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}

// Driver code
int main()
{
    string S = "cd";
    string T = "abc";

    CompareAnagrams(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

    // function to Reverse String
    static String ReverseString(String myStr)
    {
        String nstr = "";
        char ch;

        for (int i = 0; i < myStr.length(); i++) {
            ch = myStr.charAt(i); // extracts each character
            nstr
                = ch + nstr; // adds each character in
                             // front of the existing string
        }

        return nstr;
    }

    // function to print string in sorted order
    static String sortString(String str)
    {
        char[] arr = str.toCharArray();
        Arrays.sort(arr);
        return new String(arr);
    }

    // Function to check if any anagram
    // of string S is lexicographically
    // smaller than any anagram of string T
    static void CompareAnagrams(String S, String T)
    {

        // Sort string S
        sortString(S);

        // Reverse sort string T
        T = sortString(T);
        T = ReverseString(T);

        // Comparing both the strings
        if (S.compareTo(T) < 0) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "cd";
        String T = "abc";

        CompareAnagrams(S, T);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if any anagram
# of string S is lexicographically
# smaller than any anagram of string T

def CompareAnagrams(S,  T):

    # Sort string S
    S = list(S)
    S.sort()
    S = ''.join(S)

    # Reverse sort string T
    T = list(T)
    T.sort(reverse=True)
    T = ''.join(T)

    # Comparing both the strings
    if (S < T):
        print("Yes")

    else:
        print("No")

# Driver code
if __name__ == "__main__":

    S = "cd"
    T = "abc"

    CompareAnagrams(S, T)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// function to Reverse String
static string ReverseString(string myStr)
    {
        char[] myArr = myStr.ToCharArray();
        Array.Reverse(myArr);
        return new string(myArr);
    }

// function to print string in sorted order
    static void sortString(String str) {
        char []arr = str.ToCharArray();
        Array.Sort(arr);
        String.Join("",arr);
    }

// Function to check if any anagram
// of string S is lexicographically
// smaller than any anagram of string T
static void CompareAnagrams(string S, string T)
{

    // Sort string S
    sortString(S);

    // Reverse sort string T
    sortString(T);
    ReverseString(T);

    // Comparing both the strings
    if (string.Compare(S, T) < 0) {
        Console.WriteLine("Yes");
    }
    else {
        Console.WriteLine("No");
    }
}

// Driver Code
public static void Main(String []args) {

    string S = "cd";
    string T = "abc";

    CompareAnagrams(S, T);
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

    // JavaScript Program to implement
    // the above approach

    // function to Reverse String
    function ReverseString(myStr)
    {
        let nstr = "";
        let ch;

        for (let i = 0; i < myStr.length; i++) {
            ch = myStr[i]; // extracts each character
            nstr
                = ch + nstr; // adds each character in
                             // front of the existing string
        }

        return nstr;
    }

    // function to print string in sorted order
    function sortString(str)
    {
        let arr = str.split();
        arr.sort();
        return arr.join();
    }

    // Function to check if any anagram
    // of string S is lexicographically
    // smaller than any anagram of string T
    function CompareAnagrams(S, T)
    {

        // Sort string S
        sortString(S);

        // Reverse sort string T
        T = sortString(T);
        T = ReverseString(T);

        // Comparing both the strings
        if (S.localeCompare(T) < 0) {
            document.write("Yes");
        }
        else {
            document.write("No");
        }
    }

    // Driver code

    let S = "cd";
    let T = "abc";

    CompareAnagrams(S, T);

// This code is contributed by sanjoy_62.
</script>
```

**Output**

```
No
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(1)