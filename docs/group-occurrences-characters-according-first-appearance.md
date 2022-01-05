# 根据第一次出现将所有出现的字符分组

> 原文:[https://www . geesforgeks . org/group-occurs-characters-resident-first-appearance/](https://www.geeksforgeeks.org/group-occurrences-characters-according-first-appearance/)

给定一个小写字符的字符串，任务是以这样一种方式打印该字符串:字符串中的第一个字符显示在第一位，其所有出现在字符串中。

**示例:**

```
Input : str = "geeksforgeeks"
Output:  ggeeeekkssfor
Explanation: In the given string 'g' comes first 
and occurs 2 times so it is printed first
Then 'e' comes in this string and 4 times so 
it gets printed. Similarly remaining string is
printed.

Input :  str = "occurrence"
output : occcurreen 

Input  : str = "cdab"
Output : cdab

```

这个问题是以下整数数组问题的字符串版本。

[按照第一次出现的顺序对数组元素的多次出现进行分组](https://www.geeksforgeeks.org/group-multiple-occurrence-of-array-elements-ordered-by-first-occurrence/)

因为给定的字符串只有 26 个可能的字符，所以更容易实现字符串。

**实现:**
1-使用大小为 26 的数组计算给定字符串中所有字符的出现次数。
2-然后开始遍历字符串。打印每个字符的计数次数。

## C++

```
// C++ program to print all occurrences of every character
// together.
# include<bits/stdc++.h>
using namespace std;

// Since only lower case characters are there
const int MAX_CHAR = 26;

// Function to print the string
void printGrouped(string str)
{
    int n = str.length();

    // Initialize counts of all characters as 0
    int  count[MAX_CHAR] = {0};

    // Count occurrences of all characters in string
    for (int i = 0 ; i < n ; i++)
        count[str[i]-'a']++;

    // Starts traversing the string
    for (int i = 0; i < n ; i++)
    {
        // Print the character till its count in
        // hash array
        while (count[str[i]-'a']--)
            cout << str[i];

        // Make this character's count value as 0.
        count[str[i]-'a'] = 0;
    }
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    printGrouped(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all occurrences of every character
// together.

class Test
{
    // Since only lower case characters are there
    static final int MAX_CHAR = 26;

    // Method to print the string
    static void printGrouped(String str)
    {
        int n = str.length();

        // Initialize counts of all characters as 0
        int  count[] = new int[MAX_CHAR];

        // Count occurrences of all characters in string
        for (int i = 0 ; i < n ; i++)
            count[str.charAt(i)-'a']++;

        // Starts traversing the string
        for (int i = 0; i < n ; i++)
        {
            // Print the character till its count in
            // hash array
            while (count[str.charAt(i)-'a']!=0){
                System.out.print(str.charAt(i));
                count[str.charAt(i)-'a']--;
            }

            // Make this character's count value as 0.
            count[str.charAt(i)-'a'] = 0;
        }
    }

    // Driver method
    public static void main(String args[])
    {
        String str = new String("geeksforgeeks");

        printGrouped(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print all occurrences
# of every character together.

# Since only lower case characters are there
MAX_CHAR = 26

# Function to print the string
def printGrouped(string):
    n = len(string)

    # Initialize counts of all characters as 0
    count = [0] * MAX_CHAR

    # Count occurrences of all characters in string
    for i in range(n):
        count[ord(string[i]) - ord("a")] += 1

    # Starts traversing the string
    for i in range(n):

        # Print the character till its count in
        # hash array
        while count[ord(string[i]) - ord("a")]:
            print(string[i], end = "")
            count[ord(string[i]) - ord("a")] -= 1

        # Make this character's count value as 0.
        count[ord(string[i]) - ord("a")] = 0

# Driver code
if __name__ == "__main__":
    string = "geeksforgeeks"
    printGrouped(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print all 
// occurrences of every 
// character together.
using System;

class GFG
{
    // Since only lower case 
    // characters are there
    static int MAX_CHAR = 26;

    // Method to print 
    // the string
    static void printGrouped(String str)
    {
        int n = str.Length;

        // Initialize counts of
        // all characters as 0
        int []count = new int[MAX_CHAR];

        // Count occurrences of 
        // all characters in string
        for (int i = 0 ; i < n ; i++)
            count[str[i] - 'a']++;

        // Starts traversing
        // the string
        for (int i = 0; i < n ; i++)
        {
            // Print the character 
            // till its count in
            // hash array
            while (count[str[i] - 'a'] != 0)
            {
                Console.Write(str[i]);
                count[str[i] - 'a']--;
            }

            // Make this character's 
            // count value as 0.
            count[str[i] - 'a'] = 0;
        }
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        printGrouped(str);
    }
}

// This code is contributed by Sam007
```

**Output:**

```
ggeeeekkssfor

```

本文由 **[萨哈布拉](https://www.facebook.com/sahil.chhabra.965)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。