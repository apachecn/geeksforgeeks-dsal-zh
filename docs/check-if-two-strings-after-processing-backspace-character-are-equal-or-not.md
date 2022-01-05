# 处理退格字符后检查两个字符串是否相等

> 原文:[https://www . geesforgeks . org/check-if-two-string-after-processing-back space-character-equal-or-not/](https://www.geeksforgeeks.org/check-if-two-strings-after-processing-backspace-character-are-equal-or-not/)

给定两个**字符串 s1 和 s2** ，让我们假设在输入字符串时遇到了一些退格，用#表示。任务是确定处理退格字符后的结果字符串是否相等。

**示例:**

```
Input: s1= geee#e#ks, s2 = gee##eeks 
Output: True 
Explanation: Both the strings after processing the backspace character
becomes "geeeeks". Hence, true.

Input: s1 = equ#ual, s2 = ee#quaal#
Output:  False
Explanation: String 1 after processing the backspace character
becomes "equal" whereas string 2 is "eequaal". Hence, false.

```

**方法:**
要解决上述问题，我们必须观察到，如果第一个字符是“#”，也就是说，最初肯定没有键入字符，因此我们不执行任何操作。当我们遇到除“#”以外的任何字符时，我们就在当前索引之后添加该字符。当我们遇到“#”时，我们向后移动一个索引，所以我们不删除字符，而是忽略它。然后最后通过从头到尾比较每个字符来比较这两个字符串。

下面是上述方法的实现:

## C++

```
/* C++ implementation to Check if
two strings after processing
backspace character are equal or not*/

#include <bits/stdc++.h>
using namespace std;

// function to compare the two strings
bool compare(string s, string t)
{
    int ps, pt, i;

    /* the index of character in string which
       would be removed when
       backspace is encountered*/
    ps = -1;

    for (i = 0; i < s.size(); i++) {

        /* checks if a backspace is encountered or not.
            In case the first character is #,
            no change in string takes place*/
        if (s[i] == '#' && ps != -1)

            ps -= 1;

        /* the character after the # is added
         after the character at position rem_ind1 */
        else if (s[i] != '#') {

            s = s[i];
            ps += 1;
        }
    }

    pt = -1;

    for (i = 0; i < t.size(); i++) {
        /* checks if a backspace is encountered or not */
        if (t[i] == '#' && pt != -1)
            pt -= 1;

        else if (t[i] != '#') {

            t[pt + 1] = t[i];

            pt += 1;
        }
    }

    /* check if the value of
        rem_ind1 and rem_ind2
        is same, if not then
        it means they have different
        length */
    if (pt != ps)

        return false;

    /* check if resultant strings are empty */
    else if (ps == -1 && pt == -1)

        return true;

    /* check if each character in the resultant
       string is same */
    else {

        for (i = 0; i <= pt; i++) {

            if (s[i] != t[i])

                return false;
        }
        return true;
    }
}

// Driver code
int main()
{
    // initialise two strings
    string s = "geee#e#ks";
    string t = "gee##eeks";

    if (compare(s, t))

        cout << "True";
    else

        cout << "False";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Check if 
// two strings after processing 
// backspace character are equal or not
import java.util.*;
import java.lang.*;

class GFG{

// Function to compare the two strings
static boolean compare(StringBuilder s,
                       StringBuilder t)
{
    int ps, pt, i;

    // The index of character in string
    // which would be removed when
    // backspace is encountered
    ps = -1;

    for(i = 0; i < s.length(); i++)
    {

        // Checks if a backspace is encountered
        // or not. In case the first character
        // is #, no change in string takes place
        if (s.charAt(i) == '#' && ps != -1)
            ps -= 1;

        // The character after the # is added
        // after the character at position rem_ind1
        else if (s.charAt(i) != '#')
        {
            s.setCharAt(ps + 1, s.charAt(i));
            ps += 1;
        }
    }

    pt = -1;

    for(i = 0; i < t.length(); i++)
    {

        // Checks if a backspace is
        // encountered or not
        if (t.charAt(i) == '#' && pt != -1)
            pt -= 1;

        else if (t.charAt(i) != '#')
        {
            t.setCharAt(pt + 1, t.charAt(i));

            pt += 1;
        }
    }

    // Check if the value of rem_ind1 and
    // rem_ind2 is same, if not then it
    // means they have different length
    if (pt != ps)
        return false;

    // Check if resultant strings are empty
    else if (ps == -1 && pt == -1)
        return true;

    // Check if each character in the
    // resultant string is same
    else
    {
        for(i = 0; i <= pt; i++)
        {
            if (s.charAt(i) != t.charAt(i))
                return false;
        }
        return true;
    }
}

// Driver code
public static void main(String[] args)
{

    // Initialise two strings
    StringBuilder s = new StringBuilder("geee#e#ks");
    StringBuilder t = new StringBuilder("gee##eeks");

    if (compare(s, t))
        System.out.print("True");
    else
        System.out.print("False");
}
}

// This code is contributed by offbeat
```

**Output:** 

```
True

```

**时间复杂度:**O(N)
T3】辅助空间: O(1)