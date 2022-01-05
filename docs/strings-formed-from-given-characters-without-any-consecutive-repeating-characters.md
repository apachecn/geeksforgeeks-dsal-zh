# 由给定字符组成的字符串，没有任何连续的重复字符

> 原文:[https://www . geesforgeks . org/strings-由给定字符组成-不含任何连续重复字符/](https://www.geeksforgeeks.org/strings-formed-from-given-characters-without-any-consecutive-repeating-characters/)

给定一个字符串数组 **arr[]** 和一个字符串 **str** ，任务是打印数组 **arr** 中符合以下条件的所有字符串:

*   结果字符串不应包含任何连续的重复字符。
*   结果字符串应该只使用字符串**字符串**中的字符。

**示例:**

> **输入:** arr[] = { “AABCDA”、“abcdzadc”、“ABCD dbca”、“ABCD DCA”}、str = " ADC b "
> **输出:**ABCD DCA ABCD dbca
> 
> **输入:**arr[]= {“A”、“B”、“AB”、“ACB”}，str = "AB"
> **输出:** A B AB

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个字符串，检查它是否包含任何连续的重复字符以及字符串**字符串**中提到的字符之外的任何字符。如果上述任一条件通过，则继续检查下一个字符串。否则，打印字符串。
以下是上述方法的实现:

## C++

```
// CPP implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check whether the string contains
// any consecutive repetitive characters
// and any characters other than those in str
bool check(string s, string str)
{
    string chars = s;

    set<char> st;
    // Valid characters check
    for(int i = 0; i < str.length(); i++)
        st.insert(str[i]);
    for (char c : chars) {
        if(st.find(c) == st.end())
        return false;
    }

    // Nonrepetitive check
    for (int i = 0; i < chars.length() - 1; i++) {
        if (chars[i] == chars[i + 1]) {
            return false;
        }
    }
    return true;
}

// Function to print the strings which
// satisfy the mentioned conditions
void getStrings(string str, vector<string> arr)
{
    // Iterate through all the strings
    // in the array.
    for (int i = 0; i <arr.size(); i++) {

        // check function to check the
        // conditions for every string
        if (check(arr[i], str)) {
            cout<<arr[i]<<" ";
        }
    }
}

// Driver code
int main()
{
    string str = "ABCD";
    vector<string> arr({"AABCDA", "ABCDZADC","ABCDBCA", "ABCDABDCA"});
    getStrings(str, arr);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

public class GFG {

    // Function to print the strings which
    // satisfy the mentioned conditions
    public static void getStrings(
        String str, String[] arr)
    {
        // Iterate through all the strings
        // in the array.
        for (int i = 0; i < arr.length; i++) {

            // check function to check the
            // conditions for every string
            if (check(arr[i], str)) {
                System.out.print(arr[i] + " ");
            }
        }
    }

    // Function to check whether the string contains
    // any consecutive repetitive characters
    // and any characters other than those in str
    public static boolean check(String s, String str)
    {
        char[] chars = s.toCharArray();

        // Valid characters check
        for (char c : chars) {
            if (!str.contains(String.valueOf(c))) {
                return false;
            }
        }

        // Nonrepetitive check
        for (int i = 0; i < chars.length - 1; i++) {
            if (chars[i] == chars[i + 1]) {
                return false;
            }
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "ABCD";
        String[] arr
            = { "AABCDA", "ABCDZADC",
                "ABCDBCA", "ABCDABDCA" };
        getStrings(str, arr);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
# Function to print the strings which
# satisfy the mentioned conditions

def getStrings(strr, arr):

    # Iterate through all the strings
    # in the array.
    for i in range(len(arr)):

        # check function to check the
        # conditions for every string
        if (check(arr[i], strr)):
            print(arr[i],end=" ")

# Function to check whether the string contains
# any consecutive repetitive characters
# and any characters other than those in str
def check(s, strr):

    chars = s

    # Valid characters check
    for c in chars:

        if c not in strr:
            return False

    # Nonrepetitive check
    for i in range(len(chars)-1):
        if (chars[i] == chars[i + 1]):
            return False

    return True

# Driver code

strr = "ABCD"
arr = ["AABCDA", "ABCDZADC","ABCDBCA", "ABCDABDCA"]
getStrings(strr, arr)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Function to print the strings which
    // satisfy the mentioned conditions
    public static void getStrings(
        String str, String[] arr)
    {
        // Iterate through all the strings
        // in the array.
        for (int i = 0; i < arr.Length; i++) {

            // check function to check the
            // conditions for every string
            if (check(arr[i], str)) {
                Console.Write(arr[i] + " ");
            }
        }
    }

    // Function to check whether the string contains
    // any consecutive repetitive characters
    // and any characters other than those in str
    public static bool check(String s, String str)
    {
        char[] chars = s.ToCharArray();

        // Valid characters check
        foreach (char c in chars) {
            if (!str.Contains(String.Join("",c))) {
                return false;
            }
        }

        // Nonrepetitive check
        for (int i = 0; i < chars.Length - 1; i++) {
            if (chars[i] == chars[i + 1]) {
                return false;
            }
        }
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "ABCD";
        String[] arr
            = { "AABCDA", "ABCDZADC",
                "ABCDBCA", "ABCDABDCA" };
        getStrings(str, arr);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to check whether the string contains
// any consecutive repetitive characters
// and any characters other than those in str
function check(s, str)
{
    let chars = s;

    let st = new Set();
    // Valid characters check
    for(let i = 0; i < str.length; i++)
        st.add(str[i]);
    for (let c of chars) {
        if(!st.has(c))
        return false;
    }

    // Nonrepetitive check
    for (let i = 0; i < chars.length - 1; i++) {
        if (chars[i] == chars[i + 1]) {
            return false;
        }
    }
    return true;
}

// Function to print the strings which
// satisfy the mentioned conditions
function getStrings(str, arr)
{
    // Iterate through all the strings
    // in the array.
    for (let i = 0; i < arr.length; i++) {

        // check function to check the
        // conditions for every string
        if (check(arr[i], str)) {
            document.write(arr[i] + " ");
        }
    }
}

// Driver code

let str = "ABCD";
let arr = new Array("AABCDA", "ABCDZADC","ABCDBCA", "ABCDABDCA");
getStrings(str, arr);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
ABCDBCA ABCDABDCA
```