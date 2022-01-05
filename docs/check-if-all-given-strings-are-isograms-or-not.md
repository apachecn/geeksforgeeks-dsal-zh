# 检查所有给定的字符串是否都是等值线

> 原文:[https://www . geeksforgeeks . org/check-如果所有给定的字符串都是-isogram-or-not/](https://www.geeksforgeeks.org/check-if-all-given-strings-are-isograms-or-not/)

给定一个包含 **N** 字符串的数组 **arr** ，任务是检查所有字符串是否都是[等值线图](https://www.geeksforgeeks.org/check-string-isogram-not/)。如果是，打印**是**，否则打印**否**。

> 一个**等值线**是一个字母出现不超过一次的单词。

**示例:**

> **输入:**arr[]= {“ABCD”、“derg”、“erty”}
> T3】输出:是
> 
> **输入:**arr[]= {“agka”、“lkmn”}
> T3】输出:否

**方法:**如果字符串中没有字母出现超过一次，则该字符串为等值线图。现在为了解决这个问题，

*   遍历数组 **arr** ，对于每个字符串
*   创建字符的频率图。
*   任何字符频率大于 1 的地方，打印**否**并返回。
*   否则，遍历整个数组后，打印**是**。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is an isogram or not
bool isIsogram(string s)
{
    vector<int> freq(26, 0);
    for (char c : s) {
        freq++;
        if (freq > 1) {
            return false;
        }
    }

    return true;
}

// Function to check if array arr contains
// all isograms or not
bool allIsograms(vector<string>& arr)
{
    for (string x : arr) {
        if (!isIsogram(x)) {
            return false;
        }
    }

    return true;
}

// Driver Code
int main()
{
    vector<string> arr = { "abcd", "derg", "erty" };
    if (allIsograms(arr)) {
        cout << "Yes";
        return 0;
    }
    cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to check if a string
    // is an isogram or not
    static boolean isIsogram(String s)
    {
        int freq[] = new int[26];
        char S[] = s.toCharArray();
        for (char c : S) {
            freq++;
            if (freq > 1) {
                return false;
            }
        }

        return true;
    }

    // Function to check if array arr contains
    // all isograms or not
    static boolean allIsograms(String arr[])
    {
        for (String x : arr) {
            if (isIsogram(x) == false) {
                return false;
            }
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String arr[] = { "abcd", "derg", "erty" };
        if (allIsograms(arr) == true) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}

 // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to check if a string
# is an isogram or not
def isIsogram (s):
    freq = [0] * 26
    for c in s:
        freq[ord(c) - ord('a')] += 1
        if (freq[ord(c) - ord('a')] > 1):
            return False
    return True

# Function to check if array arr contains
# all isograms or not
def allIsograms (arr):
    for x in arr:
        if (not isIsogram(x)):
            return False
    return True

# Driver Code
arr = ["abcd", "derg", "erty"]
if (allIsograms(arr)):
    print("Yes")
else:
    print("No")

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to check if a string
    // is an isogram or not
    static bool isIsogram(String s)
    {
        int []freq = new int[26];
        char []S = s.ToCharArray();
        foreach (char c in S) {
            freq++;
            if (freq > 1) {
                return false;
            }
        }

        return true;
    }

    // Function to check if array arr contains
    // all isograms or not
    static bool allIsograms(String []arr)
    {
        foreach (String x in arr) {
            if (isIsogram(x) == false) {
                return false;
            }
        }

        return true;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String []arr = { "abcd", "derg", "erty" };
        if (allIsograms(arr) == true) {
            Console.WriteLine("Yes");
        }
        else {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to check if a string
    // is an isogram or not
    const isIsogram = (s) => {
        let freq = new Array(26).fill(0);
        for (let c in s) {
            freq[s.charCodeAt(c) - 'a'.charCodeAt(0)]++;
            if (freq[s.charCodeAt(c) - 'a'.charCodeAt(0)] > 1) {
                return false;
            }
        }

        return true;
    }

    // Function to check if array arr contains
    // all isograms or not
    const allIsograms = (arr) => {
        for (let x in arr) {
            if (!isIsogram(arr[x])) {
                return false;
            }
        }

        return true;
    }

    // Driver Code
    let arr = ["abcd", "derg", "erty"];
    if (allIsograms(arr))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(N*M)，其中 N 是数组的大小，M 是最长字符串的大小
T3】辅助空间: O(1)