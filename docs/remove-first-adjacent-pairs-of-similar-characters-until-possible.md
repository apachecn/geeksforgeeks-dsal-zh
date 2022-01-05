# 尽可能删除第一对相邻的相似字符

> 原文:[https://www . geesforgeks . org/remove-first-相邻-对-相似-字符-直到-可能/](https://www.geeksforgeeks.org/remove-first-adjacent-pairs-of-similar-characters-until-possible/)

给定一个字符串 **Str** ，任务是移除第一对相邻的相似字符，直到我们可以。
**注意**:移除相邻字符以获得新字符串，然后再次从新字符串中移除相邻的重复字符，并继续重复此过程，直到移除所有相似的相邻字符对。
**例:**

> **输入:**str = " keexxlx "
> **输出:** kx
> 第 0 步:移除 ee 获得“kxxlx”
> 第 1 步:移除 xx 获得“kllx”
> 第 2 步:移除 ll 获得“kx”
> **输入:** str = "阿巴卡"
> **输出:** ca

**逼近** :
使用 C++中 string 的 [back()](https://www.geeksforgeeks.org/stdstringback-in-c-with-examples/) 和 [pop_back()](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) 方法 STL 解决上述问题。对字符串中的每个字符进行迭代，如果相邻字符相同，则使用 pop_back()函数移除相邻字符。最后，返回最后一个字符串。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove adjacent duplicates
string removeDuplicates(string S)
{
    string ans = "";

    // Iterate for every character
    // in the string
    for (auto it : S) {

        // If ans string is empty or its last
        // character does not match with the
        // current character then append this
        // character to the string
        if (ans.empty() or ans.back() != it)
            ans.push_back(it);

        // Matches with the previous one
        else if (ans.back() == it)
            ans.pop_back();
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    string str = "keexxllx";
    cout << removeDuplicates(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to remove adjacent duplicates
    static String removeDuplicates(String S)
    {
        String ans = "";

        // Iterate for every character
        // in the string
        for (int i = 0; i < S.length(); i++)
        {

            // If ans string is empty or its last
            // character does not match with the
            // current character then append this
            // character to the string
            if (ans.isEmpty() ||
                ans.charAt(ans.length() - 1) != S.charAt(i))
                ans += S.charAt(i);

            // Matches with the previous one
            else if (ans.charAt(ans.length() - 1) == S.charAt(i))
                ans = ans.substring(0, ans.length() - 1);
        }

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "keexxllx";
        System.out.println(removeDuplicates(str));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to remove adjacent duplicates
def removeDuplicates(S) :

    ans = "";

    # Iterate for every character
    # in the string
    for it in S :

        # If ans string is empty or its last
        # character does not match with the
        # current character then append this
        # character to the string
        if (ans == "" or ans[-1] != it) :
            ans += it ;

        # Matches with the previous one
        elif (ans[-1] == it) :
            ans = ans[:-1];

    # Return the answer
    return ans;

# Driver Code
if __name__ == "__main__" :

    string = "keexxllx";
    print(removeDuplicates(string));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to remove adjacent duplicates
    static String removeDuplicates(String S)
    {
        String ans = "";

        // Iterate for every character
        // in the string
        for (int i = 0; i < S.Length; i++)
        {

            // If ans string is empty or its last
            // character does not match with the
            // current character then append this
            // character to the string
            if (ans == "" ||
                ans[ans.Length - 1] != S[i])
                ans += S[i];

            // Matches with the previous one
            else if (ans[ans.Length - 1] == S[i])
                ans = ans.Substring(0, ans.Length - 1);
        }

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "keexxllx";
        Console.WriteLine(removeDuplicates(str));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to remove adjacent duplicates
     function removeDuplicates( S) {
        var ans = "";

        // Iterate for every character
        // in the string
        for (i = 0; i < S.length; i++) {

            // If ans string is empty or its last
            // character does not match with the
            // current character then append this
            // character to the string
            if (ans.length==0 ||
            ans.charAt(ans.length - 1) != S.charAt(i))
                ans += S.charAt(i);

            // Matches with the previous one
            else if (ans.charAt(ans.length - 1) == S.charAt(i))
                ans = ans.substring(0, ans.length - 1);
        }

        // Return the answer
        return ans;
    }

    // Driver Code

        var str = "keexxllx";
        document.write(removeDuplicates(str));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
kx
```