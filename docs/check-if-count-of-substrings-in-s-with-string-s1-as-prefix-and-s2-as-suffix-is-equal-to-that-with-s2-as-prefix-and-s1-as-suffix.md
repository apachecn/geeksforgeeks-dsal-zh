# 检查以字符串 S1 为前缀、S2 为后缀的 S 中的子字符串个数是否等于以 S2 为前缀、S1 为后缀的子字符串个数

> 原文:[https://www . geesforgeks . org/check-if-count-in-s-string-S1-as-prefix-and-S2-as-后缀-等于-as-S2-as-prefix-and-S1-as-后缀/](https://www.geeksforgeeks.org/check-if-count-of-substrings-in-s-with-string-s1-as-prefix-and-s2-as-suffix-is-equal-to-that-with-s2-as-prefix-and-s1-as-suffix/)

给定三个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)**S****S1**和 **S2** ，任务是检查以 **S1** 和 **S2** 开始和结束的子字符串数量是否等于以 **S2** 和 **S1** 开始和结束的子字符串数量。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S =“hello world”hello world，S1 =“hello”，S2 =“world”
> **输出:** No
> **解释:**
> 以 S1(=“hello”)开头，以 S2(=“world”)结尾的子字符串是{“hello world”“hello world”“hello world”“hello world”“hello world”“hello world”}。
> 因此，总计数为 4。
> 以 S2(=“world”)开头，以 S1(=“hello”)结尾的子字符串是{“world hello”、“world hello”}。
> 因此，总计数为 2。
> 所以，以上两个计数不一样。
> 
> **输入:**S =“open closepenclosepen”，S1 =“open”，S2 =“close”
> T3】输出:是

**方法:**按照以下步骤解决问题:

*   将[长度的字符串](https://www.geeksforgeeks.org/find-length-of-a-string-in-python-4-ways/)**S****S1**和 **S2** 存储在变量中，分别表示**N****N1**和 **N2** 。
*   初始化一个变量，比如**计数**，将[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **S1** 的出现次数存储在字符串 **S** 中。
*   初始化一个变量，比如说**和**，来存储分别以 **S1** 和 **S2** 开始和结束的子串。
*   [遍历给定的字符串**S**T3】并执行以下步骤:](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
    *   将字符串 **S** 的[子字符串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)存储在字符串**前缀**中，从大小为**的索引 **i** 开始。**
    *   将字符串 **S** 的[子字符串](https://www.geeksforgeeks.org/substring-in-java/)存储在字符串**后缀**中，从大小为**的索引 **i** 开始。**
    *   如果前缀与字符串 **S1** 相同，那么将**计数**的值增加 **1** 。
    *   如果后缀与字符串 **S2** 相同，则通过**计数**增加 **ans** 的值。
*   使用以上步骤，分别找到以 **S2** 和 **S1** 开始和结束的子串数量。将获得的计数存储在变量 say **ans2** 中。
*   如果 **ans** 和 **ans2** 的值相等，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of
// substrings that starts with
// string S1 and ends with string S2
int countSubstrings(string S, string S1,
                    string S2)
{
    // Stores the length of each string
    int N = S.length();
    int N1 = S1.length();
    int N2 = S2.length();

    // Stores the count of prefixes
    // as S1 and suffixes as S2
    int count = 0, totalcount = 0;

    // Traverse string S
    for (int i = 0; i < N; i++) {

        // Find the prefix at index i
        string prefix = S.substr(i, N1);

        // Find the suffix at index i
        string suffix = S.substr(i, N2);

        // If the prefix is S1
        if (S1 == prefix)
            count++;

        // If the suffix is S2
        if (S2 == suffix)
            totalcount += count;
    }

    // Return the count of substrings
    return totalcount;
}

// Function to check if the number of
// substrings starts with S1 and ends
// with S2 and vice-versa is same or not
void checkSubstrings(string S, string S1,
                     string S2)
{

    // Count the number of substrings
    int x = countSubstrings(S, S1, S2);
    int y = countSubstrings(S, S2, S1);

    // Print the result
    if (x == y)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    string S = "opencloseopencloseopen";
    string S1 = "open";
    string S2 = "close";
    checkSubstrings(S, S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count number of
// substrings that starts with
// string S1 and ends with string S2
static int countSubstrings(String S, String S1,
                           String S2)
{

    // Stores the length of each string
    int N = S.length();
    int N1 = S1.length();
    int N2 = S2.length();

    // Stores the count of prefixes
    // as S1 and suffixes as S2
    int count = 0, totalcount = 0;

    // Traverse string S
    for(int i = 0; i < N; i++)
    {

        // Find the prefix at index i
        String prefix = S.substring(
            i, (i + N1 < N) ? (i + N1) : N);

        // Find the suffix at index i
        String suffix = S.substring(
            i, (i + N2 < N) ? (i + N2) : N);

        // If the prefix is S1
        if (S1.equals(prefix))
            count++;

        // If the suffix is S2
        if (S2.equals(suffix))
            totalcount += count;
    }

    // Return the count of substrings
    return totalcount;
}

// Function to check if the number of
// substrings starts with S1 and ends
// with S2 and vice-versa is same or not
static void checkSubstrings(String S, String S1,
                            String S2)
{

    // Count the number of substrings
    int x = countSubstrings(S, S1, S2);

    int y = countSubstrings(S, S2, S1);

    // Print the result
    if (x == y)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String[] args)
{
    String S = "opencloseopencloseopen";
    String S1 = "open";
    String S2 = "close";

    checkSubstrings(S, S1, S2);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count number of
# substrings that starts with
# string S1 and ends with string S2
def countSubstrings(S, S1, S2):

    # Stores the length of each string
    N = len(S)
    N1 = len(S1)
    N2 = len(S2)

    # Stores the count of prefixes
    # as S1 and suffixes as S2
    count = 0
    totalcount = 0

    # Traverse string S
    for i in range(N):

        # Find the prefix at index i
        prefix = S[i: (i + N1) if (i + N1 < N) else N]

        # Find the suffix at index i
        suffix = S[i: (i + N2) if (i + N2 < N) else N]

        # If the prefix is S1
        if S1 == prefix:
            count += 1

        # If the suffix is S2
        if S2 == suffix:
            totalcount += count

    # Return the count of substrings
    return totalcount

# Function to check if the number of
# substrings starts with S1 and ends
# with S2 and vice-versa is same or not
def checkSubstrings(S, S1, S2):

    x = countSubstrings(S, S1, S2)
    y = countSubstrings(S, S2, S1)

    if x == y:
        print("Yes")
    else:
        print("No")

# Driver code
S = "opencloseopencloseopen"
S1 = "open"
S2 = "close"

checkSubstrings(S, S1, S2)

# This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count number of
// substrings that starts with
// string S1 and ends with string S2
static int countSubstrings(string S, string S1,
                           string S2)
{

    // Stores the length of each string
    int N = S.Length;
    int N1 = S1.Length;
    int N2 = S2.Length;

    // Stores the count of prefixes
    // as S1 and suffixes as S2
    int count = 0, totalcount = 0;

    // Traverse string S
    for(int i = 0; i < N; i++)
    {

        // Find the prefix at index i
        String prefix = S.Substring(
            i, (i + N1 < N) ? N1 : (N - i));

        // Find the suffix at index i
        String suffix = S.Substring(
            i, (i + N2 < N) ? N2 : (N - i));

        // If the prefix is S1
        if (S1.Equals(prefix))
            count++;

        // If the suffix is S2
        if (S2.Equals(suffix))
            totalcount += count;
    }

    // Return the count of substrings
    return totalcount;
}

// Function to check if the number of
// substrings starts with S1 and ends
// with S2 and vice-versa is same or not
static void checkSubstrings(string S, string S1,
                            string S2)
{

    // Count the number of substrings
    int x = countSubstrings(S, S1, S2);

    int y = countSubstrings(S, S2, S1);

    // Print the result
    if (x == y)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
static void Main()
{
    string S = "opencloseopencloseopen";
    string S1 = "open";
    string S2 = "close";

    checkSubstrings(S, S1, S2);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count number of
// substrings that starts with
// string S1 and ends with string S2
function countSubstrings(S, S1, S2)
{

    // Stores the length of each string
    let N = S.length;
    let N1 = S1.length;
    let N2 = S2.length;

    // Stores the count of prefixes
    // as S1 and suffixes as S2
    let count = 0, totalcount = 0;

    // Traverse string S
    for (let i = 0; i < N; i++) {

        // Find the prefix at index i
        let prefix = S.substr(i, N1);

        // Find the suffix at index i
        let suffix = S.substr(i, N2);

        // If the prefix is S1
        if (S1 == prefix)
            count++;

        // If the suffix is S2
        if (S2 == suffix)
            totalcount += count;
    }

    // Return the count of substrings
    return totalcount;
}

// Function to check if the number of
// substrings starts with S1 and ends
// with S2 and vice-versa is same or not
function checkSubstrings(S, S1, S2)
{

    // Count the number of substrings
    let x = countSubstrings(S, S1, S2);
    let y = countSubstrings(S, S2, S1);

    // Print the result
    if (x == y)
        document.write("Yes");
    else
        document.write("No");
}

// Driver Code
    let S = "opencloseopencloseopen";
    let S1 = "open";
    let S2 = "close";
    checkSubstrings(S, S1, S2);

// This code is contributed by gfgking
</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N * (N1 + N2))，其中 N、N1 和 N2 分别是字符串 S、S1 和 S2 的长度。*
***辅助空间:** O(1)*