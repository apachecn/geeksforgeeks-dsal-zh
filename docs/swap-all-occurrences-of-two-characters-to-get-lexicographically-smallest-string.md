# 交换两个字符的所有出现，得到字典上最小的字符串

> 原文:[https://www . geeksforgeeks . org/swap-两个字符的所有出现次数-获取字典最小字符串/](https://www.geeksforgeeks.org/swap-all-occurrences-of-two-characters-to-get-lexicographically-smallest-string/)

给定一个由小写英文字母组成的字符串。可以选择字符串中的任意两个字符，用第二个字符替换第一个字符的所有出现，用第一个字符替换第二个字符的所有出现。找到字典上最小的字符串，最多可以通过执行一次此操作获得。

**示例:**

> **输入:** str = "ccad"
> **输出:** aacd
> 将所有出现的‘c’换成‘a’，将所有出现的‘a’换成‘c’，得到“aacd”，这是我们能得到的
> 字典上最小的字符串。
> 
> **输入:** str = "abba"
> **输出:** abba
> 唯一可能的操作是将给定的字符串
> 转换为“baab”，该字符串在字典上不是最小的。

**进场:**

*   首先，我们将字符串中每个字符的第一次出现存储在散列数组 **chk[]** 中。
*   为了找到字典上较小的字符串，最左边的字符必须替换为比它小的字符。只有当较小的字符出现在数组中它的后面时，才会发生这种情况。
*   因此，从左侧开始遍历字符串，对于每个字符，找到在交换所有出现的字符后出现的最小字符(甚至小于当前字符)，以获得所需的字符串。
*   If no such character pair is found in the previous string then print the given string as it is the smallest string possible.

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation of the approach
    #include <iostream>
    using namespace std;

    #define MAX 26

    // Function to return the lexicographically
    // smallest string after swapping all the
    // occurrences of any two characters
    string smallestStr(string str, int n)
    {
        int i, j;
        // To store the first index of
        // every character of str
        int chk[MAX];
        for (i = 0; i < MAX; i++)
            chk[i] = -1;

        // Store the first occurring
        // index every character
        for (i = 0; i < n; i++) {

            // If current character is appearing
            // for the first time in str
            if (chk[str[i] - 'a'] == -1)
                chk[str[i] - 'a'] = i;
        }

        // Starting from the leftmost character
        for (i = 0; i < n; i++) {

            bool flag = false;

            // For every character smaller than str[i]
            for (j = 0; j < str[i] - 'a'; j++) {

                // If there is a character in str which is
                // smaller than str[i] and appears after it
                if (chk[j] > chk[str[i] - 'a']) {
                    flag = true;
                    break;
                }
            }

            // If the required character pair is found
            if (flag)
                break;
        }

        // If swapping is possible
        if (i < n) {

            // Characters to be swapped
            char ch1 = str[i];
            char ch2 = char(j + 'a');

            // For every character
            for (i = 0; i < n; i++) {

                // Replace every ch1 with ch2
                // and every ch2 with ch1
                if (str[i] == ch1)
                    str[i] = ch2;

                else if (str[i] == ch2)
                    str[i] = ch1;
            }
        }

        return str;
    }

    // Driver code
    int main()
    {
        string str = "ccad";
        int n = str.length();

        cout << smallestStr(str, n);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of the approach 
    import java.util.*;

    class GFG
    {
    static int MAX = 26;

    // Function to return the lexicographically
    // smallest string after swapping all the
    // occurrences of any two characters
    static String smallestStr(char []str, int n)
    {
        int i, j = 0;

        // To store the first index of
        // every character of str
        int []chk = new int[MAX];
        for (i = 0; i < MAX; i++)
            chk[i] = -1;

        // Store the first occurring
        // index every character
        for (i = 0; i < n; i++) 
        {

            // If current character is appearing
            // for the first time in str
            if (chk[str[i] - 'a'] == -1)
                chk[str[i] - 'a'] = i;
        }

        // Starting from the leftmost character
        for (i = 0; i < n; i++)
        {
            boolean flag = false;

            // For every character smaller than str[i]
            for (j = 0; j < str[i] - 'a'; j++) 
            {

                // If there is a character in str which is
                // smaller than str[i] and appears after it
                if (chk[j] > chk[str[i] - 'a']) 
                {
                    flag = true;
                    break;
                }
            }

            // If the required character pair is found
            if (flag)
                break;
        }

        // If swapping is possible
        if (i < n) 
        {

            // Characters to be swapped
            char ch1 = str[i];
            char ch2 = (char) (j + 'a');

            // For every character
            for (i = 0; i < n; i++)
            {

                // Replace every ch1 with ch2
                // and every ch2 with ch1
                if (str[i] == ch1)
                    str[i] = ch2;

                else if (str[i] == ch2)
                    str[i] = ch1;
            }
        }

        return String.valueOf(str);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "ccad";
        int n = str.length();

        System.out.println(smallestStr(
                           str.toCharArray(), n));
    }
    }

    // This code is contributed by Princi Singh
    ```

    ## 蟒蛇 3

    ```
    # python3 implementation of the approach
    MAX=256

    # Function to return the lexicographically
    # smallest after swapping all the
    # occurrences of any two characters
    def smallestStr(str, n):
        i, j=0,0
        # To store the first index of
        # every character of str
        chk=[0 for i in range(MAX)]
        for i in range(MAX):
            chk[i] = -1

        # Store the first occurring
        # index every character
        for i in range(n):

            # If current character is appearing
            # for the first time in str
            if (chk[ord(str[i])] == -1):
                chk[ord(str[i])] = i

        # Starting from the leftmost character
        for  i in range(n):
            flag = False

            # For every character smaller than ord(str[i])
            for j in range(ord(str[i])):

                # If there is a character in str which is
                # smaller than ord(str[i]) and appears after it
                if (chk[j] > chk[ord(str[i])]):
                    flag = True
                    break

            # If the required character pair is found
            if (flag):
                break

        # If swapping is possible
        if (i < n):

            # Characters to be swapped
            ch1 = (str[i])
            ch2 = chr(j)

            # For every character
            for i in range(n):

                # Replace every ch1 with ch2
                # and every ch2 with ch1
                if (str[i] == ch1):
                    str[i] = ch2

                elif (str[i] == ch2):
                    str[i] = ch1

        return "".join(str)

    # Driver code

    st = "ccad"
    str=[i for i in st]
    n = len(str)

    print(smallestStr(str, n))
    ```

    ## C#

    ```
    // C# implementation of the approach
    using System;

    class GFG
    {
    static int MAX = 26;

    // Function to return the lexicographically
    // smallest string after swapping all the
    // occurrences of any two characters
    static String smallestStr(char []str, int n)
    {
        int i, j = 0;

        // To store the first index of
        // every character of str
        int []chk = new int[MAX];
        for (i = 0; i < MAX; i++)
            chk[i] = -1;

        // Store the first occurring
        // index every character
        for (i = 0; i < n; i++) 
        {

            // If current character is appearing
            // for the first time in str
            if (chk[str[i] - 'a'] == -1)
                chk[str[i] - 'a'] = i;
        }

        // Starting from the leftmost character
        for (i = 0; i < n; i++)
        {
            Boolean flag = false;

            // For every character smaller than str[i]
            for (j = 0; j < str[i] - 'a'; j++) 
            {

                // If there is a character in str which is
                // smaller than str[i] and appears after it
                if (chk[j] > chk[str[i] - 'a']) 
                {
                    flag = true;
                    break;
                }
            }

            // If the required character pair is found
            if (flag)
                break;
        }

        // If swapping is possible
        if (i < n) 
        {

            // Characters to be swapped
            char ch1 = str[i];
            char ch2 = (char) (j + 'a');

            // For every character
            for (i = 0; i < n; i++)
            {

                // Replace every ch1 with ch2
                // and every ch2 with ch1
                if (str[i] == ch1)
                    str[i] = ch2;

                else if (str[i] == ch2)
                    str[i] = ch1;
            }
        }

        return String.Join("", str);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "ccad";
        int n = str.Length;

        Console.WriteLine(smallestStr(
                          str.ToCharArray(), n));
    }
    }

    // This code is contributed by Princi Singh
    ```

    **Output:**

    ```
    aacd

    ```