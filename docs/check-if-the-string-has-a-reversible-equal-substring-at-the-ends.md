# 检查字符串是否在末尾有可逆的相等子字符串

> 原文:[https://www . geesforgeks . org/check-如果字符串在末尾有一个可逆的相等子字符串/](https://www.geeksforgeeks.org/check-if-the-string-has-a-reversible-equal-substring-at-the-ends/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查这个字符串从开始到结束是否有一个可逆的相等子字符串。如果是，打印**真**，然后按照给定的条件出现最长的子串，否则打印**假。**

**示例:**

> **输入:** S = "abca"
> **输出:**
> 真
> a
> **说明:**
> 子串“a”只是满足给定条件的最长子串。因此，打印一份。
> 
> **输入:** S = "acdfbcdca"
> **输出:**
> 真
> acd
> **说明:**
> 子串“acd”只是满足给定条件的最长子串。因此，打印 acd。
> 
> **输入:**S = " abcdcb "
> T3】输出:假

**方法:**给定的问题可以通过使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决给定的问题:

*   初始化一个字符串，比如说**和**为 **""** ，存储满足给定标准的结果字符串。
*   初始化两个变量，分别把 **i** 和 **j** 设为 **0** 和**(N–1)**。
*   [循环迭代直到 **j** 为非负](https://www.geeksforgeeks.org/range-based-loop-c/)且 f 字符 **S[i]** 和 **S[j]** 相同，然后只需在变量 **ans** 中加上字符 **S[i]** ，将 **i** 的值增加 **1** 并将 **j** 的值减少 **1** 否则，[打破循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果字符串**和**为空，则打印**假**。否则，打印**真**，然后打印[字符串](https://www.geeksforgeeks.org/strings-in-c-2/) **和**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print longest substring
// that appears at beginning of string
// and also at end in reverse order
void commonSubstring(string s)
{
    int n = s.size();
    int i = 0;
    int j = n - 1;

    // Stores the resultant string
    string ans = "";
    while (j >= 0) {

        // If the characters are same
        if (s[i] == s[j]) {
            ans += s[i];
            i++;
            j--;
        }

        // Otherwise, break
        else {
            break;
        }
    }

    // If the string can't be formed
    if (ans.size() == 0)
        cout << "False";

    // Otherwise print resultant string
    else {
        cout << "True \n"
             << ans;
    }
}

// Driver Code
int main()
{
    string S = "abca";
    commonSubstring(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG
{

    // Function to print longest substring
    // that appears at beginning of string
    // and also at end in reverse order
    static void commonSubstring(String s)
    {
        int n = s.length();
        int i = 0;
        int j = n - 1;

        // Stores the resultant string
        String ans = "";
        while (j >= 0) {

            // If the characters are same
            if (s.charAt(i) == s.charAt(j)) {
                ans += s.charAt(i);
                i++;
                j--;
            }

            // Otherwise, break
            else {
                break;
            }
        }

        // If the string can't be formed
        if (ans.length() == 0)
            System.out.println("False");

        // Otherwise print resultant string
        else {
            System.out.println("True ");
            System.out.println(ans);
        }
    }

    // Driver Code
    public static void main(String []args)
    {
        String S = "abca";
        commonSubstring(S);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Function to print longest substring
# that appears at beginning of string
# and also at end in reverse order
def commonSubstring(s):

    n = len(s)
    i = 0
    j = n - 1

    # Stores the resultant string
    ans = ""
    while (j >= 0):

        # // If the characters are same
        if (s[i] == s[j]):
            ans += s[i]
            i = i + 1
            j = j - 1

        # Otherwise, break
        else:
            break

    # If the string can't be formed
    if (len(ans) == 0):
        print("False")

    # Otherwise print resultant string
    else:
        print("True")
        print(ans)

# Driver Code
if __name__ == "__main__":

    S = "abca"
    commonSubstring(S)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to print longest substring
    // that appears at beginning of string
    // and also at end in reverse order
    static void commonSubstring(string s)
    {
        int n = s.Length;
        int i = 0;
        int j = n - 1;

        // Stores the resultant string
        string ans = "";
        while (j >= 0) {

            // If the characters are same
            if (s[i] == s[j]) {
                ans += s[i];
                i++;
                j--;
            }

            // Otherwise, break
            else {
                break;
            }
        }

        // If the string can't be formed
        if (ans.Length == 0)
            Console.WriteLine("False");

        // Otherwise print resultant string
        else {
            Console.WriteLine("True ");
            Console.WriteLine(ans);
        }
    }

    // Driver Code
    public static void Main()
    {
        string S = "abca";
        commonSubstring(S);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to print longest substring
        // that appears at beginning of string
        // and also at end in reverse order
        function commonSubstring(s) {
            let n = s.length;
            let i = 0;
            let j = n - 1;

            // Stores the resultant string
            let ans = "";
            while (j >= 0) {

                // If the characters are same
                if (s[i] == s[j]) {
                    ans += s[i];
                    i++;
                    j--;
                }

                // Otherwise, break
                else {
                    break;
                }
            }

            // If the string can't be formed
            if (ans.length == 0)
                document.write("False");

            // Otherwise print resultant string
            else {
                document.write("True" + "<br>"
                    + ans);
            }
        }

        // Driver Code
        let S = "abca";
        commonSubstring(S);

     // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
a
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)