# 将两个子串(一串的)替换为另一个

> 原文:[https://www . geesforgeks . org/replace-two-substring-of-a-string-to-other/](https://www.geeksforgeeks.org/replace-two-substrings-of-a-string-with-each-other/)

给定 3 根弦**S****A**和 **B** 。任务是用 **B** 替换 **S** 等于 **A** 的每个子串，用 **A** 替换 **S** 等于 **B** 的每个子串。匹配 **A** 或 **B** 的两个或多个子串有可能重叠。为了避免这种情况的混淆，您应该找到与 **A** 或 **B** 匹配的最左边的子字符串，将其替换，然后继续字符串的其余部分。
例如将 **A = "aa"** 与 **S = "aaa"** 匹配时，**A【0，1】**将优先于**A【1，2】**。

**注意**的 **A** 和 **B** 会和 **A 一样长！= B** 。

**示例:**

> **输入:**S =“aab”，A =“aa”，B =“bb”
> T3】输出: bbb
> 我们将前两个字符与 A 匹配，用 B 替换，得到 bbb。
> 然后我们继续从索引 3 开始的算法，我们没有找到更多的匹配。
> 
> **输入:**S =“aabbaabb”，A =“aa”，B =“bb”
> **输出:** bbaabbaa
> 我们用“bb”替换所有出现的“aa”，用“aa”替换“bb”，这样得到的字符串就是“bbaabbaa”。

**方法:**从长度为**的 **S** 开始，遍历所有可能的子串(A)** 。如果有子字符串匹配 **A** 或 **B** ，则根据需要更新字符串，并最终打印更新后的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the resultant string
string updateString(string S,
                    string A, string B)
{

    int l = A.length();

    // Iterate through all positions i
    for (int i = 0; i + l <= S.length(); i++)
    {

        // Current sub-string of
        // length = len(A) = len(B)
        string curr = S.substr(i, i + l);

        // If current sub-string gets
        // equal to A or B
        if (curr == A)
        {

            // Update S after replacing A
            string new_string = "";
            new_string += S.substr(0, i) + B +
                          S.substr(i + l, S.length());
            S = new_string;
            i += l - 1;
        }
        else if(curr == B)
        {

            // Update S after replacing B
            string new_string = "";
            new_string += S.substr(0, i) + A +
                          S.substr(i + l, S.length());
            S = new_string;
            i += l - 1;
        }
        else
        {
          //do nothing
        }
    }

    // Return the updated string
    return S;
}

// Driver code
int main()
{
    string S = "aaxb";
    string A = "aa";
    string B = "bb";

    cout << (updateString(S, A, B)) << endl;
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the resultant string
    static String updateString(String S, String A, String B)
    {

        int l = A.length();

        // Iterate through all positions i
        for (int i = 0; i + l <= S.length(); i++) {

            // Current sub-string of length = len(A) = len(B)
            String curr = S.substring(i, i + l);

            // If current sub-string gets equal to A or B
            if (curr.equals(A)) {

                // Update S after replacing A
                String new_string
                    = S.substring(0, i)
                      + B + S.substring(i + l, S.length());
                S = new_string;
                i += l - 1;
            }
            else {

                // Update S after replacing B
                String new_string
                    = S.substring(0, i)
                      + A + S.substring(i + l, S.length());
                S = new_string;
                i += l - 1;
            }
        }

        // Return the updated string
        return S;
    }

    // Driver code
    public static void main(String[] args)
    {
        String S = "aab";
        String A = "aa";
        String B = "bb";

        System.out.println(updateString(S, A, B));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the resultant string
def updateString(S, A, B):

    l = len(A)

    # Iterate through all positions i
    i = 0
    while i + l <= len(S):

        # Current sub-string of
        # length = len(A) = len(B)
        curr = S[i:i+l]

        # If current sub-string gets
        # equal to A or B
        if curr == A:

            # Update S after replacing A
            new_string = S[0:i] + B + S[i + l:len(S)]
            S = new_string
            i += l - 1

        else:

            # Update S after replacing B
            new_string = S[0:i] + A + S[i + l:len(S)]
            S = new_string
            i += l - 1

        i += 1

    # Return the updated string
    return S

# Driver code
if __name__ == "__main__":

    S = "aab"
    A = "aa"
    B = "bb"

    print(updateString(S, A, B))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the resultant string
    static string updateString(string S, string A, string B)
    {
        int l = A.Length;

        // Iterate through all positions i
        for (int i = 0; i + l <= S.Length; i++)
        {

            // Current sub-string of length = len(A) = len(B)
            string curr = S.Substring(i, l);

            // If current sub-string gets equal to A or B
            if (curr.Equals(A))
            {

                // Update S after replacing A
                string new_string = S.Substring(0, i) +
                                 B + S.Substring(i + l);
                S = new_string;
                i += l - 1;
            }
            else
            {

                // Update S after replacing B
                string new_string = S.Substring(0, i) +
                                A + S.Substring(i + l);
                S = new_string;
                i += l - 1;
            }
        }

        // Return the updated string
        return S;
    }

    // Driver code
    public static void Main()
    {
        string S = "aab";
        string A = "aa";
        string B = "bb";
        Console.WriteLine(updateString(S, A, B));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to return the resultant string
function updateString($S, $A, $B)
{

    $l = strlen($A);

    // Iterate through all positions i
    for ($i = 0; $i + $l <= strlen($S); $i++)
    {

        // Current sub-string of length = len(A) = len(B)
        $curr = substr($S, $i, $i + $l);

        // If current sub-string gets equal to A or B
        if (strcmp($curr, $A) == 0)
        {

            // Update S after replacing A
            $new_string = substr($S, 0, $i) . $B .
                        substr($S, $i + $l, strlen($S));
            $S = $new_string;
            $i += $l - 1;
        }
        else
        {

            // Update S after replacing B
            $new_string = substr($S, 0, $i) . $A .
                        substr($S, $i + $l, strlen($S));
            $S = $new_string;
            $i += $l - 1;
        }
    }

    // Return the updated string
    return $S;
}

// Driver code
$S = "aab";
$A = "aa";
$B = "bb";

echo(updateString($S, $A, $B));

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the resultant string
function updateString(S, A, B)
{
    let l = A.length;

    // Iterate through all positions i
    for(let i = 0; i + l <= S.length; i++)
    {

        // Current sub-string of length = len(A) = len(B)
        let curr = S.substring(i, i + l);

        // If current sub-string gets equal to A or B
        if (curr == A)
        {

            // Update S after replacing A
            let new_string = S.substring(0, i) +
                         B + S.substring(i + l);
            S = new_string;
            i += l - 1;
        }
        else
        {

            // Update S after replacing B
            let new_string = S.substring(0, i) +
                         A + S.substring(i + l);
            S = new_string;
            i += l - 1;
        }
    }

    // Return the updated string
    return S;
}

// Driver code
let S = "aab";
let A = "aa";
let B = "bb";

document.write(updateString(S, A, B));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
bbb
```