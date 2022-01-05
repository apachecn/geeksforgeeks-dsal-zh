# 使用数组列表

打印字符串的所有子序列

> 原文:[https://www . geesforgeks . org/print-all-subseries-of-a-string-use-ArrayList/](https://www.geeksforgeeks.org/print-all-subsequences-of-a-string-using-arraylist/)

给定一个字符串 **str** ，任务是打印 **str** 的所有子序列。
A [子序列](https://en.wikipedia.org/wiki/Subsequence)是一个序列，可以通过删除一些元素或不删除元素而不改变剩余元素的顺序，从另一个序列中派生出来。
**示例:**

> **输入:**【str = " ABC】
> **输出:**a b ab AC BC ABC
> **输入:**【str = " geek】**输出:**g e ge ee gee GK ek geke

**方法:**编写一个递归函数，在每个子序列的开头追加字符串的第一个字符**str【0】**之后，打印从第二个字符**str【1，n–1】**开始的子字符串的每个子序列。终止条件将是当传递的字符串为空时，在这种情况下，函数将返回一个空的[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the contents
// of the List
void printList(vector<string> arrL)
{
    arrL.erase(find(arrL.begin(), arrL.end(), ""));
    for (int i = 0; i < arrL.size(); i++)
        cout << arrL[i] << " ";
}

// Function to returns the arraylist which contains
// all the sub-sequences of str
vector<string> getSequence(string str)
{

    // If string is empty
    if (str.length() == 0)
    {
        // Return an empty arraylist
        vector<string> empty;
        empty.push_back("");
        return empty;
    }

    // Take first character of str
    char ch = str[0];

    // Take sub-string starting from the
    // second character
    string subStr = str.substr(1);

    // Recurvise call for all the sub-sequences
    // starting from the second character
    vector<string> subSequences = getSequence(subStr);

    // Add first character from str in the beginning
    // of every character from the sub-sequences
    // and then store it into the resultant arraylist
    vector<string> res;
    for(string val : subSequences)
    {
        res.push_back(val);
        res.push_back(ch + val);
    }

    // Return the resultant arraylist
    return res;
}

int main()
{
    string str = "geek";
    printList(getSequence(str));

    return 0;
}

// This code is contributed by rameshtravel07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;

public class GFG {

    // Utility function to print the contents
    // of the ArrayList
    static void printArrayList(ArrayList<String> arrL)
    {
        arrL.remove("");
        for (int i = 0; i < arrL.size(); i++)
            System.out.print(arrL.get(i) + " ");
    }

    // Function to returns the arraylist which contains
    // all the sub-sequences of str
    public static ArrayList<String> getSequence(String str)
    {

        // If string is empty
        if (str.length() == 0) {

            // Return an empty arraylist
            ArrayList<String> empty = new ArrayList<>();
            empty.add("");
            return empty;
        }

        // Take first character of str
        char ch = str.charAt(0);

        // Take sub-string starting from the
        // second character
        String subStr = str.substring(1);

        // Recurvise call for all the sub-sequences
        // starting from the second character
        ArrayList<String> subSequences =
                              getSequence(subStr);

        // Add first character from str in the beginning
        // of every character from the sub-sequences
        // and then store it into the resultant arraylist
        ArrayList<String> res = new ArrayList<>();
        for (String val : subSequences) {
            res.add(val);
            res.add(ch + val);
        }

        // Return the resultant arraylist
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geek";
        printArrayList(getSequence(str));
        // System.out.print(getSequence(str));
    }
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Utility function to print the contents
# of the ArrayList
def printArrayList(arrL):
    arrL.remove("")
    print(*arrL, sep = " ")

# Function to returns the arraylist which contains
# all the sub-sequences of str
def getSequence(Str):

    # If string is empty
    if(len(Str) == 0):

        # Return an empty arraylist
        empty = []
        empty.append("")
        return empty

    # Take first character of str
    ch = Str[0]

    # Take sub-string starting from the
    # second character
    subStr = Str[1:]

    # Recurvise call for all the sub-sequences
    # starting from the second character
    subSequences = getSequence(subStr)

    # Add first character from str in the beginning
    # of every character from the sub-sequences
    # and then store it into the resultant arraylist
    res = []

    for val in subSequences:
        res.append(val)
        res.append(ch + val)

    # Return the resultant arraylist
    return res

# Driver code
Str = "geek"
printArrayList(getSequence(Str))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

    // Utility function to print the contents
    // of the List
    static void printList(List<String> arrL)
    {
        arrL.Remove("");
        for (int i = 0; i < arrL.Count; i++)
            Console.Write(arrL[i] + " ");
    }

    // Function to returns the arraylist which contains
    // all the sub-sequences of str
    public static List<String> getSequence(String str)
    {

        // If string is empty
        if (str.Length == 0)
        {

            // Return an empty arraylist
            List<String> empty = new List<String>();
            empty.Add("");
            return empty;
        }

        // Take first character of str
        char ch = str[0];

        // Take sub-string starting from the
        // second character
        String subStr = str.Substring(1);

        // Recurvise call for all the sub-sequences
        // starting from the second character
        List<String> subSequences = getSequence(subStr);

        // Add first character from str in the beginning
        // of every character from the sub-sequences
        // and then store it into the resultant arraylist
        List<String> res = new List<String>();
        foreach (String val in subSequences)
        {
            res.Add(val);
            res.Add(ch + val);
        }

        // Return the resultant arraylist
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "geek";
        printList(getSequence(str));
        // Console.Write(getSequence(str));
    }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Utility function to print the contents
    // of the ArrayList
    function printArrayList(arrL)
    {
        arrL.splice(arrL.indexOf(""), 1);
        for (let i = 0; i < arrL.length; i++)
            document.write(arrL[i] + " ");
    }

    // Function to returns the arraylist which contains
    // all the sub-sequences of str
    function getSequence(str)
    {

        // If string is empty
        if (str.length == 0) {

            // Return an empty arraylist
            let empty = [];
            empty.push("");
            return empty;
        }

        // Take first character of str
        let ch = str[0];

        // Take sub-string starting from the
        // second character
        let subStr = str.substring(1);

        // Recurvise call for all the sub-sequences
        // starting from the second character
        let subSequences = getSequence(subStr);

        // Add first character from str in the beginning
        // of every character from the sub-sequences
        // and then store it into the resultant arraylist
        let res = [];
        for (let val = 0; val < subSequences.length; val++) {
            res.push(subSequences[val]);
            res.push(ch + subSequences[val]);
        }

        // Return the resultant arraylist
        return res;
    }

    let str = "geek";
      printArrayList(getSequence(str));

</script>
```

**Output:** 

```
g e ge e ge ee gee k gk ek gek ek gek eek geek
```

**备选方案:**逐个固定字符，并从它们开始递归生成所有子集。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the sub-sequences
// of a string
void printSubSeq(string sub, string ans)
{

    if (sub.length() == 0) {
        cout << "" << ans << " ";
        return;
    }

    // First character of sub
    char ch = sub[0];

    // Sub-string starting from second
    // character of sub
    string ros = sub.substr(1);

    // Excluding first character
    printSubSeq(ros, ans);

    // Including first character
    printSubSeq(ros, ans + ch);
}

// Driver code
int main()
{
    string str = "abc";
    printSubSeq(str, "");

    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class sub_sequence {

    // Function to print all the sub-sequences
    // of a string
    public static void printSubSeq(String sub,
                                  String ans)
    {

        if (sub.length() == 0) {
            System.out.print("" + ans + " ");
            return;
        }

        // First character of sub
        char ch = sub.charAt(0);

        // Sub-string starting from second
        // character of sub
        String ros = sub.substring(1);

        // Excluding first character
        printSubSeq(ros, ans);

        // Including first character
        printSubSeq(ros, ans + ch);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abc";
        printSubSeq(str, "");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print all the sub-sequences
# of a string
def printSubSeq(sub, ans) :

    if (len(sub) == 0) :
        print(ans , end = " ")
        return

    # First character of sub
    ch = sub[0]

    # Sub-string starting from second
    # character of sub
    ros = sub[1 : ]

    # Excluding first character
    printSubSeq(ros, ans)

    # Including first character
    printSubSeq(ros, ans + ch)

Str = "abc"
printSubSeq(Str, "")

# This code iscontributed by divyeshrabadiya07
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print all the 
// sub-sequences of a string
public static void printSubSeq(string sub,
                               string ans)
{
    if (sub.Length == 0)
    {
        Console.Write("" + ans + " ");
        return;
    }

    // First character of sub
    char ch = sub[0];

    // Sub-string starting from second
    // character of sub
    string ros = sub.Substring(1);

    // Excluding first character
    printSubSeq(ros, ans);

    // Including first character
    printSubSeq(ros, ans + ch);
}

// Driver code
public static void Main()
{
    string str = "abc";
    printSubSeq(str, "") ;
}
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to print all the
    // sub-sequences of a string
    function printSubSeq(sub, ans)
    {
        if (sub.length == 0)
        {
            document.write("" + ans + " ");
            return;
        }

        // First character of sub
        let ch = sub[0];

        // Sub-string starting from second
        // character of sub
        let ros = sub.substring(1);

        // Excluding first character
        printSubSeq(ros, ans);

        // Including first character
        printSubSeq(ros, ans + ch);
    }

    let str = "abc";
    printSubSeq(str, "") ;

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
c b bc a ac ab abc
```