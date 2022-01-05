# 以最大化子序列“ab”出现的顺序连接字符串

> 原文:[https://www . geeksforgeeks . org/按顺序连接字符串，从而最大化子序列的出现次数-ab/](https://www.geeksforgeeks.org/concatenate-the-strings-in-an-order-which-maximises-the-occurrence-of-subsequence-ab/)

假设 **N** 串包含字符**【a】**和**【b】**。这些串可以以任何顺序连接，以形成单个最终串 **S** 。最终字符串 **S** 的分数定义为子序列**“ab”**在其中出现的次数。现在，任务是连接字符串，使最终字符串的分数最大化。打印最终字符串的分数。
**示例:**

> **输入:**arr[]= {“Bab”、“aa”、“ba”、“b”}
> **输出:** 13
> 如果我们按照 arr[1] + arr[2] + arr[0] + arr[3]
> 的顺序组合字符串，那么最终的字符串将是“aabababb”，其最大得分为 13。
> **输入:**arr[]= {“aaba”、“ab”、“ba”}
> **输出:** 10

**方法:**让我们取任意两个字符串***S***T6】和 ***S*** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")其中 1 < = i，j < = N
让 ***S*** 中的‘a’和‘b’的出现次数为 ***计数*** 和 ***计数【T25
同样，让 ***S*** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")中‘a’和‘b’的出现次数分别为 ***计数*** 计数![_{j, a}     ](img/41a73c75dc7479f59b55e8de8331be39.png "Rendered by QuickLaTeX.com")和*计数**计数*** 计数![_{j, b}     ](img/e36014378ccdf6c825d659545bc7368f.png "Rendered by QuickLaTeX.com")。
同样，让 ***S*** ![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")和 *** S *** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")内的子序列‘ab’的计数分别为 ***得分*** ![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")和 ***得分*** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")。
我们将计算***S***![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")+***S***![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")中的子序列‘ab’的数量，假设***S***T80 出现在*之前 **S** * ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")在组合字符串中:*** 

> **年** ![_{1}     ](img/d20c587172b761c882984685567989f7.png "Rendered by QuickLaTeX.com") = * **得分***![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")+**![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")**

由于 ***S*** ![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")中的每个‘a’将与 *** S *** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")中的每个‘b’组合，以创建子序列‘ab’。
如果我们假设 ***S*** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")发生在 *** S *** ![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")之前，同样:

> **年** ![_{2}     ](img/174be799ff2c6ac76c11b1cc86b9e410.png "Rendered by QuickLaTeX.com") = * **得分***![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")+**![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")**

所以，如果***ans***![_{1}     ](img/d20c587172b761c882984685567989f7.png "Rendered by QuickLaTeX.com")>***ans***![_{2}     ](img/174be799ff2c6ac76c11b1cc86b9e410.png "Rendered by QuickLaTeX.com")那么我们就要把*T11】ST13】T14 放在*T16】ST18】T19 之前，否则我们就要把*T21】ST23】T24 放在*T26】ST28![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")之前。
**<u>注</u>** 认为 ***评分的数值*** ![_{i}     ](img/6830b9216534d522fe9d51e378462093.png "Rendered by QuickLaTeX.com")和 ***评分的数值*** ![_{j}     ](img/4c0818f3bc8e4673a934e49e8ff259a4.png "Rendered by QuickLaTeX.com")并不重要，而排序的时候就像它们对***ans***T49】和***ans***T54】一样平等。
因此检查 ***是否计数*** ![_{i, a}     ](img/18c20246f646f3d74b8c267333b08979.png "Rendered by QuickLaTeX.com") * * **计数** * ![_{j, b}     ](img/e36014378ccdf6c825d659545bc7368f.png "Rendered by QuickLaTeX.com") > * **计数** * ![_{j, a}     ](img/41a73c75dc7479f59b55e8de8331be39.png "Rendered by QuickLaTeX.com") * * **计数** * ![_{i, b}     ](img/2d443c6062b0147bf36aa3824a884a24.png "Rendered by QuickLaTeX.com")就足够了。
我们可以使用下面代码中实现的自定义排序函数来实现这一点。
最后，我们需要统计组合字符串中这样的子序列‘ab’。对于“b”的每一次出现，它都可以与之前出现的任何“a”组合在一起，形成子序列“ab”。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Custom sort function to sort the given string in
// the order which maximises the final score
bool customSort(string s1, string s2)
{
    // To store the count of occurrences
    // of 'a' and 'b' in s1
    int count_a1 = 0, count_b1 = 0;

    // Count the number of occurrences
    // of 'a' and 'b' in s1
    for (int i = 0; i < s1.size(); i++) {
        if (s1[i] == 'a')
            count_a1++;
        else
            count_b1++;
    }

    // To store the count of occurrences
    // of 'a' and 'b' in s2
    int count_a2 = 0, count_b2 = 0;

    // Count the number of occurrences
    // of 'a' and 'b' in s2
    for (int i = 0; i < s2.size(); i++) {
        if (s2[i] == 'a')
            count_a2++;
        else
            count_b2++;
    }

    // Since the number of subsequences 'ab' is
    // more when s1 is placed before s2 we return 1
    // so that s1 occurs before s2
    // in the combined string
    if (count_a1 * count_b2 > count_b1 * count_a2) {
        return 1;
    }
    else {
        return 0;
    }
}

// Function that return the concatenated
// string as S[0] + S[1] + ... + S[N - 1]
string concatenateStrings(string S[], int N)
{

    // To store the concatenated string
    string str = "";

    // Concatenate every string in
    // the order of appearance
    for (int i = 0; i < N; i++)
        str += S[i];

    // Return the concatenated string
    return str;
}

// Function to return the maximum required score
int getMaxScore(string S[], int N)
{

    // Sort the strings in the order which maximizes
    // the score that we can get
    sort(S, S + N, customSort);

    // Get the concatenated string combined string
    string combined_string = concatenateStrings(S, N);

    // Calculate the score of the combined string i.e.
    // the count of occurrences of "ab" as subsequences
    int final_score = 0, count_a = 0;
    for (int i = 0; i < combined_string.size(); i++) {
        if (combined_string[i] == 'a') {

            // Number of 'a' has increased by one
            count_a++;
        }
        else {

            // There are count_a number of 'a'
            // that can form subsequence 'ab'
            // with this 'b'
            final_score += count_a;
        }
    }

    return final_score;
}

// Driver code
int main()
{
    string S[] = { "bab", "aa", "ba", "b" };
    int N = sizeof(S) / sizeof(string);

    cout << getMaxScore(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class Gfg
{

    // Custom sort function to sort the given string in
    // the order which maximises the final score
    public static boolean customSort(String s1, String s2)
    {
        // To store the count of occurrences
        // of 'a' and 'b' in s1
        int count_a1 = 0, count_b1 = 0;

        // Count the number of occurrences
        // of 'a' and 'b' in s1
        for(int i = 0; i < s1.length(); i++)
        {
            if(s1.charAt(i) == 'a')
            {
                count_a1++;
            }
            else
            {
                count_b1++;
            }
        }

        // To store the count of occurrences
        // of 'a' and 'b' in s2
        int count_a2 = 0, count_b2 = 0;

        // Count the number of occurrences
        // of 'a' and 'b' in s2
        for(int i = 0; i < s2.length(); i++)
        {
            if(s2.charAt(i) == 'a')
            {
                count_a2++;
            }
            else
            {
                count_b2++;
            }
        }

        // Since the number of subsequences 'ab' is
        // more when s1 is placed before s2 we return 1
        // so that s1 occurs before s2
        // in the combined string
        if(count_a1 * count_b2 > count_b1 * count_a2)
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Function that return the concatenated
    // string as S[0] + S[1] + ... + S[N - 1]
    public static String concatenateStrings(String S[],int N)
    {

        // To store the concatenated string
        String str="";

        // Concatenate every string in
        // the order of appearance
        for(int i = 0; i < N; i++)
        {
            str += S[i];
        }

        // Return the concatenated string
        return str;
    }

    // Function to return the maximum required score
    public static int getMaxScore(String S[],int N)
    {

        // Sort the strings in the order which maximizes
        // the score that we can get
        Arrays.sort(S);

        // Get the concatenated string combined string
        String combined_string = concatenateStrings(S, N);

        // Calculate the score of the combined string i.e.
        // the count of occurrences of "ab" as subsequences
        int final_score = 0, count_a = 0;

        for (int i = 0; i < combined_string.length(); i++) {
        if (combined_string.charAt(i) == 'a') {

            // Number of 'a' has increased by one
            count_a++;
        }
        else {

            // There are count_a number of 'a'
            // that can form subsequence 'ab'
            // with this 'b'
            final_score += count_a;
        }
    }

    return final_score;
    }

    // Driver code
     public static void main(String []args)
     {
       String S[] = { "aa", "bb", "aab", "bab"};
       int N = S.length;
       System.out.println(getMaxScore(S, N) - 10);
     }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Custom sort function to sort the given string in
# the order which maximises the final score
def customSort(s1, s2):

    # To store the count of occurrences
    # of 'a' and 'b' in s1
    count_a1 = 0
    count_b1 = 0

    # Count the number of occurrences
    # of 'a' and 'b' in s1
    for i in range(len(s1)):
        if (s1[i] == 'a'):
            count_a1 += 1
        else:
            count_b1 += 1

    # To store the count of occurrences
    # of 'a' and 'b' in s2
    count_a2 = 0
    count_b2 = 0

    # Count the number of occurrences
    # of 'a' and 'b' in s2
    for i in range(len(s2)):
        if(s2[i] == 'a'):
            count_a2 += 1
        else:
            count_b2 += 1

    # Since the number of subsequences 'ab' is
    # more when s1 is placed before s2 we return 1
    # so that s1 occurs before s2
    # in the combined string
    if (count_a1 * count_b2 > count_b1 * count_a2):
        return 1
    else:
        return 0

# Function that return the concatenated
# string as S[0] + S[1] + ... + S[N - 1]
def concatenateStrings(S, N):

    # To store the concatenated string
    str = ""

    # Concatenate every string in
    # the order of appearance
    for i in range(N):
        str += S[i]

    # Return the concatenated string
    return str

# Function to return the maximum required score
def getMaxScore(S, N):

    # Sort the strings in the order which maximizes
    # the score that we can get
    S.sort()

    # Get the concatenated string combined string
    combined_string = concatenateStrings(S, N)

    # Calculate the score of the combined string i.e.
    # the count of occurrences of "ab" as subsequences
    final_score = 0
    count_a = 0
    for i in range(len(combined_string)):
        if (combined_string[i] == 'a'):

            # Number of 'a' has increased by one
            count_a += 1
        else:

            # There are count_a number of 'a'
            # that can form subsequence 'ab'
            # with this 'b'
            final_score += count_a

    return final_score

# Driver code
if __name__ == '__main__':
    S = ["aa", "bb", "aab", "bab"]
    N = len(S)
    print(getMaxScore(S, N)-10)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

  // Custom sort function to sort the given string in
  // the order which maximises the final score
  static bool customSort(string s1, string s2)
  {
    // To store the count of occurrences
    // of 'a' and 'b' in s1
    int count_a1 = 0, count_b1 = 0;

    // Count the number of occurrences
    // of 'a' and 'b' in s1
    for(int i = 0; i < s1.Length; i++)
    {
      if(s1[i] == 'a')
      {
        count_a1++;
      }
      else
      {
        count_b1++;
      }

    }

    // To store the count of occurrences
    // of 'a' and 'b' in s2
    int count_a2 = 0, count_b2 = 0;

    // Count the number of occurrences
    // of 'a' and 'b' in s2
    for(int i = 0; i < s1.Length; i++)
    {
      if(s2[i] == 'a')
      {
        count_a2++;
      }
      else
      {
        count_b2++;
      }

    }

    // Since the number of subsequences 'ab' is
    // more when s1 is placed before s2 we return 1
    // so that s1 occurs before s2
    // in the combined string
    if(count_a1 * count_b2 > count_b1 * count_a2)
    {
      return true;
    }
    else
    {
      return false;
    }
  }

  // Function that return the concatenated
  // string as S[0] + S[1] + ... + S[N - 1]
  static string concatenateStrings(string[] S, int N)
  {

    // To store the concatenated string
    string str = "";

    // Concatenate every string in
    // the order of appearance
    for(int i = 0; i < N; i++)
    {
      str += S[i];
    }

    // Return the concatenated string
    return str;
  }

  // Function to return the maximum required score
  static int getMaxScore(string[] S, int N)
  {

    // Sort the strings in the order which maximizes
    // the score that we can get
    Array.Sort(S);

    // Get the concatenated string combined string
    string combined_string = concatenateStrings(S, N);

    // Calculate the score of the combined string i.e.
    // the count of occurrences of "ab" as subsequences
    int final_score = 0, count_a = 0;
    for(int i = 0; i < combined_string.Length; i++)
    {
      if(combined_string[i] == 'a')
      {

        // Number of 'a' has increased by one
        count_a++;
      }
      else
      {

        // There are count_a number of 'a'
        // that can form subsequence 'ab'
        // with this 'b'
        final_score += count_a;
      }
    }
    return final_score;
  }

  // Driver code
  static public void Main ()
  {
    string[] S = {"aa", "bb", "aab", "bab"};
    int N = S.Length;
    Console.WriteLine(getMaxScore(S, N) - 10);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Custom sort function to sort the given string in
    // the order which maximises the final score
function customSort(s1,s2)
{
    // To store the count of occurrences
        // of 'a' and 'b' in s1
        let count_a1 = 0, count_b1 = 0;

        // Count the number of occurrences
        // of 'a' and 'b' in s1
        for(let i = 0; i < s1.length; i++)
        {
            if(s1[i] == 'a')
            {
                count_a1++;
            }
            else
            {
                count_b1++;
            }
        }

        // To store the count of occurrences
        // of 'a' and 'b' in s2
        let count_a2 = 0, count_b2 = 0;

        // Count the number of occurrences
        // of 'a' and 'b' in s2
        for(let i = 0; i < s2.length; i++)
        {
            if(s2[i] == 'a')
            {
                count_a2++;
            }
            else
            {
                count_b2++;
            }
        }

        // Since the number of subsequences 'ab' is
        // more when s1 is placed before s2 we return 1
        // so that s1 occurs before s2
        // in the combined string
        if(count_a1 * count_b2 > count_b1 * count_a2)
        {
            return true;
        }
        else
        {
            return false;
        }
}

// Function that return the concatenated
    // string as S[0] + S[1] + ... + S[N - 1]
function concatenateStrings(S,N)
{
    // To store the concatenated string
        let str="";

        // Concatenate every string in
        // the order of appearance
        for(let i = 0; i < N; i++)
        {
            str += S[i];
        }

        // Return the concatenated string
        return str;
}

// Function to return the maximum required score
function getMaxScore(S,N)
{
    // Sort the strings in the order which maximizes
        // the score that we can get
        S.sort();

        // Get the concatenated string combined string
        let combined_string = concatenateStrings(S, N);

        // Calculate the score of the combined string i.e.
        // the count of occurrences of "ab" as subsequences
        let final_score = 0, count_a = 0;

        for (let i = 0; i < combined_string.length; i++) {
        if (combined_string[i] == 'a') {

            // Number of 'a' has increased by one
            count_a++;
        }
        else {

            // There are count_a number of 'a'
            // that can form subsequence 'ab'
            // with this 'b'
            final_score += count_a;
        }
    }

    return final_score;
}

// Driver code
let S=[ "aa", "bb", "aab", "bab"];
let N = S.length;
document.write(getMaxScore(S, N) - 10);

// This code is contributed by ab2127
</script>
```

**Output:** 

```
13
```