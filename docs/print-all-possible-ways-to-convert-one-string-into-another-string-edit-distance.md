# 打印将一个字符串转换成另一个字符串的所有可能方式|编辑-距离

> 原文:[https://www . geesforgeks . org/print-所有可能的方法-将一个字符串转换为另一个字符串-编辑-距离/](https://www.geeksforgeeks.org/print-all-possible-ways-to-convert-one-string-into-another-string-edit-distance/)

**先决条件:** [动态编程|集合 5(编辑距离)](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)
给定两个字符串 str1 和 str2，任务是打印将‘str 1’转换为‘str 2’的所有可能方式。
以下是可在“str1”上执行的操作:

1.  插入
2.  去除
3.  替换

上述所有操作的成本相同。任务是使用所需的最少编辑(操作)次数打印将“str1”转换为“str2”的所有不同方式，其中“方式”包括所需的一系列此类操作。
**例:**

> **输入:**str 1 =“abcdef”，str 2 =“axcdfdh”
> T3】输出:
> **方法 1:**
> 加 h
> 变 f 为 d
> 变 e 为 f
> 变 b 为 x
> **方法 2:**
> 变 f 为 h
> 加 d
> 变 e 为 f
> 变 b 为 x
> **方法 3**

**一种可能的打印方式:**

在这篇[帖子](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)中已经讨论了找到最小编辑次数的方法。要打印一种可能的方式，从使用[最小编辑距离](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)方法形成的动态规划矩阵的右下角开始迭代。检查两个字符串中与该元素相关的字符是否相等。如果是，说明不需要编辑，DP[i][j]是从 DP[i-1][j-1]复制过来的。

```
If str1[i-1] == str2[j-1], proceed diagonally. 
```

**注意**由于 DP 矩阵在 0 索引处包含一个额外的行和列，字符串索引将减少 1。即 DP[i][j]对应于 str1 的 i-1 指标和 str2 的 j-1 指标。
现在，如果字符不相等，这意味着这个矩阵元素 DP[i][j]是从 DP[i-1][j-1]、DP[i][j-1]和 DP[i-1][j]加上 1 的最小值获得的。因此，检查这个元素来自哪里。

```
1\. If DP[i][j] == DP[i-1][j-1] + 1 
        It means the character was replaced from str1[i] to str2[j]. Proceed diagonally.
2\. If DP[i][j] == DP[i][j-1] + 1
        It means the character was Added from str2[j]. Proceed left.
3\. If DP[i][j] == DP[i-1][j] + 1
        It means the character str1[i] was deleted. Proceed up.
```

一旦到达任一字符串的末尾，即(i==0 或 j==0)，就完成了一个字符串到另一个字符串的转换。我们将打印出所有需要的操作。
以下是上述方法的实现:

## C++

```
// C++ program to print one possible
// way of converting a string to another
#include <bits/stdc++.h>
using namespace std;

int DP[100][100];

// Function to print the steps
void printChanges(string s1, string s2,
                         int dp[][100])
{
    int i = s1.length();
    int j = s2.length();

    // check till the end
    while (i and j)
    {
        // if characters are same
        if (s1[i - 1] == s2[j - 1])
        {
            i--;
            j--;
        }

        // Replace
        else if (dp[i][j] == dp[i - 1][j - 1] + 1)
        {
            cout << "change " << s1[i - 1]
                 << " to " << s2[j - 1] << endl;
            i--;
            j--;
        }

        // Delete the character
        else if (dp[i][j] == dp[i - 1][j] + 1)
        {
            cout << "Delete " << s1[i - 1] << endl;
            i--;
        }

        // Add the character
        else if (dp[i][j] == dp[i][j - 1] + 1)
        {
            cout << "Add " << s2[j - 1] << endl;
            j--;
        }
    }
}

// Function to compute the DP matrix
void editDP(string s1, string s2)
{
    int l1 = s1.length();
    int l2 = s2.length();
    DP[l1 + 1][l2 + 1];

    // initialize by the maximum edits possible
    for (int i = 0; i <= l1; i++)
        DP[i][0] = i;
    for (int j = 0; j <= l2; j++)
        DP[0][j] = j;

    // Compute the DP matrix
    for (int i = 1; i <= l1; i++)
    {
        for (int j = 1; j <= l2; j++)
        {
            // if the characters are same
            // no changes required
            if (s1[i - 1] == s2[j - 1])
                DP[i][j] = DP[i - 1][j - 1];
            else
                // minimum of three operations possible
                DP[i][j] = min(min(DP[i - 1][j - 1],
                                   DP[i - 1][j]),
                                   DP[i][j - 1]) + 1;
        }
    }

    // print the steps
    printChanges(s1, s2, DP);
}
// Driver Code
int main()
{
    string s1 = "abcdef";
    string s2 = "axcdfdh";

    // calculate the DP matrix
    editDP(s1, s2);

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print one possible
// way of converting a string to another
import java.util.*;

public class Edit_Distance {
    static int dp[][];

    // Function to print the steps
    static void printChanges(String s1, String s2)
    {
        int i = s1.length();
        int j = s2.length();

        // check till the end
        while (i != 0 && j != 0) {

            // if characters are same
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                i--;
                j--;
            }

            // Replace
            else if (dp[i][j] == dp[i - 1][j - 1] + 1) {
                System.out.println("change " + s1.charAt(i - 1) + " to " + s2.charAt(j - 1));
                i--;
                j--;
            }

            // Delete the character
            else if (dp[i][j] == dp[i - 1][j] + 1) {
                System.out.println("Delete " + s1.charAt(i - 1));
                i--;
            }

            // Add the character
            else if (dp[i][j] == dp[i][j - 1] + 1) {
                System.out.println("Add " + s2.charAt(j - 1));
                j--;
            }
        }
    }

    // Function to compute the DP matrix
    static void editDP(String s1, String s2)
    {
        int l1 = s1.length();
        int l2 = s2.length();
        int[][] DP = new int[l1 + 1][l2 + 1];

        // initialize by the maximum edits possible
        for (int i = 0; i <= l1; i++)
            DP[i][0] = i;
        for (int j = 0; j <= l2; j++)
            DP[0][j] = j;

        // Compute the DP matrix
        for (int i = 1; i <= l1; i++) {
            for (int j = 1; j <= l2; j++) {

                // if the characters are same
                // no changes required
                if (s1.charAt(i - 1) == s2.charAt(j - 1))
                    DP[i][j] = DP[i - 1][j - 1];
                else {

                    // minimum of three operations possible
                    DP[i][j] = min(DP[i - 1][j - 1],
                                   DP[i - 1][j], DP[i][j - 1])
                               + 1;
                }
            }
        }

        // initialize to global array
        dp = DP;
    }

    // Function to find the minimum of three
    static int min(int a, int b, int c)
    {
        int z = Math.min(a, b);
        return Math.min(z, c);
    }

    // Driver Code
    public static void main(String[] args) throws Exception
    {
        String s1 = "abcdef";
        String s2 = "axcdfdh";

        // calculate the DP matrix
        editDP(s1, s2);

        // print the steps
        printChanges(s1, s2);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print one possible
# way of converting a string to another

# Function to print the steps
def printChanges(s1, s2, dp):

    i = len(s1)
    j = len(s2)

   # Check till the end
    while(i > 0 and j > 0):

        # If characters are same
        if s1[i - 1] == s2[j - 1]:
            i -= 1
            j -= 1

        # Replace
        elif dp[i][j] == dp[i - 1][j - 1] + 1:
            print("change", s1[i - 1],
                      "to", s2[j - 1])
            j -= 1
            i -= 1

        # Delete
        elif dp[i][j] == dp[i - 1][j] + 1:
            print("Delete", s1[i - 1])
            i -= 1

        # Add
        elif dp[i][j] == dp[i][j - 1] + 1:
            print("Add", s2[j - 1])
            j -= 1

# Function to compute the DP matrix
def editDP(s1, s2):

    len1 = len(s1)
    len2 = len(s2)
    dp = [[0 for i in range(len2 + 1)]
             for j in range(len1 + 1)]

    # Initialize by the maximum edits possible
    for i in range(len1 + 1):
        dp[i][0] = i
    for j in range(len2 + 1):
        dp[0][j] = j

    # Compute the DP Matrix
    for i in range(1, len1 + 1):
        for j in range(1, len2 + 1):

            # If the characters are same
            # no changes required
            if s2[j - 1] == s1[i - 1]:
                dp[i][j] = dp[i - 1][j - 1]

            # Minimum of three operations possible
            else:
                dp[i][j] = 1 + min(dp[i][j - 1],
                                   dp[i - 1][j - 1],
                                   dp[i - 1][j])

    # Print the steps
    printChanges(s1, s2, dp)

# Driver Code
s1 = "abcdef"
s2 = "axcdfdh"

# Compute the DP Matrix
editDP(s1, s2)

# This code is contributed by Pranav S
```

## C#

```
// C# program to print one possible
// way of converting a string to another
using System;

public class Edit_Distance
{
    static int [,]dp;

    // Function to print the steps
    static void printChanges(String s1, String s2)
    {
        int i = s1.Length;
        int j = s2.Length;

        // check till the end
        while (i != 0 && j != 0)
        {

            // if characters are same
            if (s1[i - 1] == s2[j - 1])
            {
                i--;
                j--;
            }

            // Replace
            else if (dp[i, j] == dp[i - 1, j - 1] + 1)
            {
                Console.WriteLine("change " + s1[i - 1] + " to " + s2[j - 1]);
                i--;
                j--;
            }

            // Delete the character
            else if (dp[i, j] == dp[i - 1, j] + 1)
            {
                Console.WriteLine("Delete " + s1[i - 1]);
                i--;
            }

            // Add the character
            else if (dp[i, j] == dp[i, j - 1] + 1)
            {
                Console.WriteLine("Add " + s2[j - 1]);
                j--;
            }
        }
    }

    // Function to compute the DP matrix
    static void editDP(String s1, String s2)
    {
        int l1 = s1.Length;
        int l2 = s2.Length;
        int[,] DP = new int[l1 + 1, l2 + 1];

        // initialize by the maximum edits possible
        for (int i = 0; i <= l1; i++)
            DP[i, 0] = i;
        for (int j = 0; j <= l2; j++)
            DP[0, j] = j;

        // Compute the DP matrix
        for (int i = 1; i <= l1; i++)
        {
            for (int j = 1; j <= l2; j++)
            {

                // if the characters are same
                // no changes required
                if (s1[i - 1] == s2[j - 1])
                    DP[i, j] = DP[i - 1, j - 1];
                else
                {

                    // minimu of three operations possible
                    DP[i, j] = min(DP[i - 1, j - 1],
                                DP[i - 1, j], DP[i, j - 1])
                            + 1;
                }
            }
        }

        // initialize to global array
        dp = DP;
    }

    // Function to find the minimum of three
    static int min(int a, int b, int c)
    {
        int z = Math.Min(a, b);
        return Math.Min(z, c);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s1 = "abcdef";
        String s2 = "axcdfdh";

        // calculate the DP matrix
        editDP(s1, s2);

        // print the steps
        printChanges(s1, s2);
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
change f to h
change e to d
Add f
change b to x
```

**接近打印的所有可能方式:**

创建将存储所需操作的字符串集合。这个集合可以是 C++中的字符串向量，也可以是 Java 中的字符串列表。将操作添加到此集合中，就像之前打印它们一样。然后创建这些集合的集合，这些集合将存储多个方法(字符串操作集)。
Else-if 之前用于检查我们从哪里得到 DP[i][j]。现在，检查所有的 If，看看是否有超过 1 种方法可以获得元素。如果有的话，我们从之前创建一个新的集合，删除最后一个操作，添加这个新操作，并使用这个新列表启动这个函数的另一个实例。以这种方式，每当有新的方法将 str1 更改为 str2 时，就添加新的列表，每次都会得到一个新的方法。
到达任一字符串的末尾时，将该列表添加到列表集合中，从而完成所有可能操作的集合，并添加它们。
以下是上述办法的实施情况:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the possible
// steps to change a string to another
import java.util.ArrayList;

public class Edit_Distance {
    static int dp[][];

    // create List of lists that will store all sets of operations
    static ArrayList<ArrayList<String> > arrs =
                              new ArrayList<ArrayList<String> >();

    // Function to print all ways
    static void printAllChanges(String s1,
                                String s2, ArrayList<String> changes)
    {

        int i = s1.length();
        int j = s2.length();

        // Iterate till end
        while (true) {

            if (i == 0 || j == 0) {

                // Add this list to our List of lists.
                arrs.add(changes);
                break;
            }

            // If same
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                i--;
                j--;
            }

            else {
                boolean if1 = false, if2 = false;

                // Replace
                if (dp[i][j] == dp[i - 1][j - 1] + 1) {

                    // Add this step
                    changes.add("Change " + s1.charAt(i - 1)
                                + " to " + s2.charAt(j - 1));
                    i--;
                    j--;

                    // note whether this 'if' was true.
                    if1 = true;
                }

                // Delete
                if (dp[i][j] == dp[i - 1][j] + 1) {
                    if (if1 == false) {
                        changes.add("Delete " + s1.charAt(i - 1));
                        i--;
                    }
                    else {
                        // If the previous method was true,
                        // create a new list as a copy of previous.
                        ArrayList<String> changes2 = new ArrayList<String>();
                        changes2.addAll(changes);

                        // Remove last operation
                        changes2.remove(changes.size() - 1);

                        // Add this new operation
                        changes2.add("Delete " + s1.charAt(i));

                        // initiate new new instance of this
                        // function with remaining substrings
                        printAllChanges(s1.substring(0, i),
                                        s2.substring(0, j + 1), changes2);
                    }

                    if2 = true;
                }

                // Add character step
                if (dp[i][j] == dp[i][j - 1] + 1) {
                    if (if1 == false && if2 == false) {
                        changes.add("Add " + s2.charAt(j - 1));
                        j--;
                    }
                    else {

                        // Add steps
                        ArrayList<String> changes2 = new ArrayList<String>();
                        changes2.addAll(changes);
                        changes2.remove(changes.size() - 1);
                        changes2.add("Add " + s2.charAt(j));

                        // Recursively call for the next steps
                        printAllChanges(s1.substring(0, i + 1),
                                        s2.substring(0, j), changes2);
                    }
                }
            }
        }
    }

    // Function to compute the DP matrix
    static void editDP(String s1, String s2)
    {
        int l1 = s1.length();
        int l2 = s2.length();
        int[][] DP = new int[l1 + 1][l2 + 1];

        // initialize by the maximum edits possible
        for (int i = 0; i <= l1; i++)
            DP[i][0] = i;
        for (int j = 0; j <= l2; j++)
            DP[0][j] = j;

        // Compute the DP matrix
        for (int i = 1; i <= l1; i++) {
            for (int j = 1; j <= l2; j++) {

                // if the characters are same
                // no changes required
                if (s1.charAt(i - 1) == s2.charAt(j - 1))
                    DP[i][j] = DP[i - 1][j - 1];
                else {

                    // minimum of three operations possible
                    DP[i][j] = min(DP[i - 1][j - 1],
                                   DP[i - 1][j], DP[i][j - 1])
                               + 1;
                }
            }
        }

        // initialize to global array
        dp = DP;
    }

    // Function to find the minimum of three
    static int min(int a, int b, int c)
    {
        int z = Math.min(a, b);
        return Math.min(z, c);
    }
    static void printWays(String s1, String s2,
                          ArrayList<String> changes)
    {

        // Function to print all the ways
        printAllChanges(s1, s2, new ArrayList<String>());

        int i = 1;

        // print all the possible ways
        for (ArrayList<String> ar : arrs) {
            System.out.println("\nMethod " + i++ + " : \n");
            for (String s : ar) {
                System.out.println(s);
            }
        }
    }

    // Driver Code
    public static void main(String[] args) throws Exception
    {
        String s1 = "abcdef";
        String s2 = "axcdfdh";

        // calculate the DP matrix
        editDP(s1, s2);

        // Function to print all ways
        printWays(s1, s2, new ArrayList<String>());
    }
}
```

**Output:** 

```
Method 1 : 

Add h
Change f to d
Change e to f
Change b to x

Method 2 : 

Change f to h
Add d
Change e to f
Change b to x

Method 3 : 

Change f to h
Change e to d
Add f
Change b to x
```