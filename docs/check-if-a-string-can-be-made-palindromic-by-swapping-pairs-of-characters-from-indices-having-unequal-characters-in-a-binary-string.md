# 通过交换二进制字符串中具有不相等字符的索引中的字符对，检查字符串是否可以成为回文字符串

> 原文:[https://www . geeksforgeeks . org/check-if-a-string-can-通过交换索引中具有不相等二进制字符串字符对来制作回文/](https://www.geeksforgeeks.org/check-if-a-string-can-be-made-palindromic-by-swapping-pairs-of-characters-from-indices-having-unequal-characters-in-a-binary-string/)

给定一个长度均为 **N** 的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** 和一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **B** ，任务是检查给定的[字符串 **S** 是否可以通过在由字符串 **B** 中的不相等字符组成的任意一对索引处重复交换字符](https://www.geeksforgeeks.org/check-if-given-strings-can-be-made-same-by-swapping-two-characters-of-same-or-different-strings/)而成为回文。

**示例:**

> ***输入:***S =“BAA”，B =“100”
> ***输出:**是*
> ***解释:***
> 交换 S[0]和 S[1]将 S 修改为“ABA”，将 B 修改为“010”。
> 
> ***输入:**S*=“ACABB”，B =“00000”
> T5**输出:** 否

**方法:**按照以下步骤解决这个问题:

*   [检查字符串 **S** 是否可以重新排列形成回文字符串](https://www.geeksforgeeks.org/check-characters-given-string-can-rearranged-form-palindrome/)。如果发现是**假**，则打印**“否”**。
*   否则，如果[串 **S** 是回文](https://www.geeksforgeeks.org/recursive-function-check-string-palindrome/)，则打印**“是”**。
*   如果**0s****1s**的计数至少为**1**，那么总有一种方法可以互换字符，使给定的字符串 **S** 回文。因此，打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Utility function to check if string
// S can be made palindromic or not
bool canBecomePalindromeUtil(string S, string B)
{

    // Stores the number of distinct
    // characters present in string S
    unordered_set<char> set;

    // Traverse the characters of string S
    for(int i = 0; i < S.size(); i++)
    {

        // Insert current character in S
        set.insert(S[i]);
    }

    // Count frequency of each
    // character of string S
    map<char, int> map;

    // Traverse the characters of string S
    for(int i = 0; i < S.length(); i++)
    {
        map[S[i]] += 1;
    }

    bool flag = false;

    // Check for the odd length string
    if (S.size() % 2 == 1)
    {

        // Stores the count of
        // even and odd frequent
        // characters in the string S
        int count1 = 0, count2 = 0;

        for(auto e : map)
        {
            if (e.second % 2 == 1)
            {

                // Update the count of
                // odd frequent characters
                count2++;
            }
            else
            {

                // Update the count of
                // even frequent characters
                count1++;
            }
        }

        // If the conditions satisfies
        if (count1 == set.size() - 1 && count2 == 1)
        {
            flag = true;
        }
    }

    // Check for even length string
    else
    {

        // Stores the frequency of
        // even and odd characters
        // in the string S
        int count1 = 0, count2 = 0;

        for(auto e : map)
        {
            if (e.second % 2 == 1)
            {

                // Update the count of
                // odd frequent characters
                count2++;
            }
            else
            {

                // Update the count of
                // even frequent characters
                count1++;
            }
        }

        // If the condition satisfies
        if (count1 == set.size() && count2 == 0)
        {
            flag = true;
        }
    }

    // If a palindromic string
    // cannot be formed
    if (!flag)
    {
        return false;
    }

    else
    {

        // Check if there is
        // atleast one '1' and '0'
        int count1 = 0, count0 = 0;
        for(int i = 0; i < B.size(); i++)
        {

            // If current character is '1'
            if (B[i] == '1')
            {
                count1++;
            }
            else
            {
                count0++;
            }
        }

        // If atleast one '1' and '0' is present
        if (count1 >= 1 && count0 >= 1)
        {
            return true;
        }

        else
        {
            return false;
        }
    }
}

// Function to determine whether
// string S can be converted to
// a palindromic string or not
void canBecomePalindrome(string S, string B)
{
    if (canBecomePalindromeUtil(S, B))
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    string S = "ACABB";
    string B = "00010";
    canBecomePalindrome(S, B);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;

class GFG {

    // Utility function to check if string
    // S can be made palindromic or not
    public static boolean
    canBecomePalindromeUtil(String S,
                            String B)
    {
        // Stores the number of distinct
        // characters present in string S
        HashSet<Character> set = new HashSet<>();

        // Traverse the characters of string S
        for (int i = 0; i < S.length(); i++) {

            // Insert current character in S
            set.add(S.charAt(i));
        }

        // Count frequency of each
        // character of string S
        HashMap<Character, Integer> map
            = new HashMap<>();

        // Traverse the characters of string S
        for (int i = 0; i < S.length(); i++) {
            Integer k = map.get(S.charAt(i));
            map.put(S.charAt(i),
                    (k == null) ? 1 : k + 1);
        }

        boolean flag = false;

        // Check for the odd length string
        if (S.length() % 2 == 1) {

            // Stores the count of
            // even and odd frequenct
            // characters in the string S
            int count1 = 0, count2 = 0;

            for (Map.Entry<Character, Integer> e :
                 map.entrySet()) {

                if (e.getValue() % 2 == 1) {

                    // Update the count of
                    // odd frequent characters
                    count2++;
                }
                else {

                    // Update the count of
                    // even frequent characters
                    count1++;
                }
            }

            // If the conditions satisfies
            if (count1 == set.size() - 1
                && count2 == 1) {
                flag = true;
            }
        }

        // Check for even length string
        else {

            // Stores the frequency of
            // even and odd characters
            // in the string S
            int count1 = 0, count2 = 0;

            for (Map.Entry<Character, Integer> e :
                 map.entrySet()) {

                if (e.getValue() % 2 == 1) {

                    // Update the count of
                    // odd frequent characters
                    count2++;
                }
                else {

                    // Update the count of
                    // even frequent characters
                    count1++;
                }
            }

            // If the condition satisfies
            if (count1 == set.size()
                && count2 == 0) {
                flag = true;
            }
        }

        // If a palindromic string
        // cannot be formed
        if (!flag) {
            return false;
        }

        else {

            // Check if there is
            // atleast one '1' and '0'
            int count1 = 0, count0 = 0;
            for (int i = 0;
                 i < B.length(); i++) {

                // If current character is '1'
                if (B.charAt(i) == '1') {
                    count1++;
                }
                else {
                    count0++;
                }
            }

            // If atleast one '1' and '0' is present
            if (count1 >= 1 && count0 >= 1) {
                return true;
            }

            else {
                return false;
            }
        }
    }

    // Function to determine whether
    // string S can be converted to
    // a palindromic string or not
    public static void
    canBecomePalindrome(String S,
                        String B)
    {
        if (canBecomePalindromeUtil(S, B))
            System.out.print("Yes");
        else
            System.out.print("No");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "ACABB";
        String B = "00010";
        canBecomePalindrome(S, B);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Utility function to check if string
# S can be made palindromic or not
def canBecomePalindromeUtil(S, B):

    # Stores the number of distinct
    # characters present in string S
    s = set(S)

    # Count frequency of each
    # character of string S
    map = {}

    # Traverse the characters of string S
    for i in range(len(S)):
        if S[i] in map:
            map[S[i]] += 1
        else:
            map[S[i]] = 1

    flag = False

    # Check for the odd length string
    if (len(S) % 2 == 1):

        # Stores the count of
        # even and odd frequenct
        # characters in the string S
        count1 = 0
        count2 = 0

        for e in map:
            if (map[e] % 2 == 1):

                # Update the count of
                # odd frequent characters
                count2 += 1

            else:

                # Update the count of
                # even frequent characters
                count1 += 1

        # If the conditions satisfies
        if (count1 == len(s) - 1 and
            count2 == 1):
            flag = True

    # Check for even length string
    else:

        # Stores the frequency of
        # even and odd characters
        # in the string S
        count1 = 0
        count2 = 0

        for e in map:
            if (map[e] % 2 == 1):

                # Update the count of
                # odd frequent characters
                count2 += 1

            else:

                # Update the count of
                # even frequent characters
                count1 += 1

        # If the condition satisfies
        if (count1 == len(s) and count2 == 0):
            flag = True

    # If a palindromic string
    # cannot be formed
    if (not flag):
        return False

    else:

        # Check if there is
        # atleast one '1' and '0'
        count1 = 0
        count0 = 0
        for i in range(len(B)):

            # If current character is '1'
            if (B[i] == '1'):
                count1 += 1
            else:
                count0 += 1

        # If atleast one '1' and '0' is present
        if (count1 >= 1 and count0 >= 1):
            return True
        else:
            return False

# Function to determine whether
# string S can be converted to
# a palindromic string or not
def canBecomePalindrome(S, B):

    if (canBecomePalindromeUtil(S, B)):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == "__main__":

    S = "ACABB"
    B = "00010"

    canBecomePalindrome(S, B)

# This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Utility function to check if string
// S can be made palindromic or not
function canBecomePalindromeUtil(S, B)
{

    // Stores the number of distinct
    // characters present in string S
    var st = new Set()
    var i;

    // Traverse the characters of string S
    for(i = 0; i < S.length; i++)
    {

        // Insert current character in S
        st.add(S[i]);
    }

    // Count frequency of each
    // character of string S
    var mp = new Map();

    // Traverse the characters of string S
    for(i = 0; i < S.length; i++)
    {
        if (mp.has(S[i]))
            mp.set(S[i], mp.get(S[i]))
        else
            mp.set(S[i], 1);
    }

    var flag = false;

    // Check for the odd length string
    if (S.length % 2 == 1)
    {

        // Stores the count of
        // even and odd frequenct
        // characters in the string S
        var count1 = 0, count2 = 0;
        for(const [key, value] of Object.entries(mp))
        {
            if (value % 2 == 1)
            {

                // Update the count of
                // odd frequent characters
                count2++;
            }
            else
            {

                // Update the count of
                // even frequent characters
                count1++;
            }
         }

        // If the conditions satisfies
        if (count1 == st.size - 1 && count2 == 1)
        {
            flag = true;
        }
    }

    // Check for even length string
    else
    {

        // Stores the frequency of
        // even and odd characters
        // in the string S
        var count1 = 0, count2 = 0;

        for (const [key, value] of Object.entries(mp))
        {
            if (value % 2 == 1)
            {

                // Update the count of
                // odd frequent characters
                count2++;
            }
            else
            {

                // Update the count of
                // even frequent characters
                count1++;
            }
        }

        // If the condition satisfies
        if (count1 == st.size && count2 == 0)
        {
            flag = true;
        }
    }

    // If a palindromic string
    // cannot be formed
    if (!flag)
    {
        return false;
    }

    else
    {

        // Check if there is
        // atleast one '1' and '0'
        var count1 = 0, count0 = 0;
        for(i = 0; i < B.length; i++)
        {

            // If current character is '1'
            if (B[i] == '1')
            {
                count1++;
            }
            else
            {
                count0++;
            }
        }

        // If atleast one '1' and '0' is present
        if (count1 >= 1 && count0 >= 1)
        {
            return true;
        }

        else
        {
            return false;
        }
    }
}

// Function to determine whether
// string S can be converted to
// a palindromic string or not
function canBecomePalindrome(S, B)
{
    if (canBecomePalindromeUtil(S, B))
        document.write("No");
    else
        document.write("Yes");
}

// Driver code
var S = "ACABB";
var B = "00010";

canBecomePalindrome(S, B);

// This code is contributed by SURENDRA_GANGWAR

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)