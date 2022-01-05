# 打印一个字符串的所有回文分区

> 原文:[https://www . geesforgeks . org/print-回文-partitions-string/](https://www.geeksforgeeks.org/print-palindromic-partitions-string/)

给定一个字符串 s，分区 s，使得分区的每个字符串都是回文。返回 s 的所有可能的回文分区。

**示例:**

```
Input  : s = "bcc"
Output : [["b", "c", "c"], ["b", "cc"]]

Input  : s = "geeks"
Output : [["g", "e", "e", "k", "s"], 
          ["g", "ee", "k", "s"]]

```

我们必须列出所有可能的分区，这样我们就会朝着递归的方向思考。当我们在索引 I 上时，我们递增地检查从 I 开始的所有子串是否是回文。如果找到，我们递归地解决剩余字符串的问题，并将其添加到我们的解决方案中。

以下是解决方案-

1.  我们将维护一个用于存储所有可能分区的二维向量和一个用于存储当前分区的临时向量，字符串的新起始索引用于检查分区，因为我们已经在此索引之前检查过分区。
2.  现在继续在字符串上迭代，检查它是否是回文。
3.  如果它是回文，那么在当前分区向量中添加这个字符串。如果不是字符串的结尾，则在这个新字符串上递归。再次返回后，将当前分区向量更改为旧的分区向量，因为它在递归步骤中可能已经更改。
4.  如果我们在迭代的时候到达了字符串的末尾，那么我们的临时向量中就有了分区，所以我们将把它添加到结果中。

要检查它是否是回文，通过取两个指针来迭代字符串。初始化第一个字符串开始，另一个字符串结束。如果两个字符相同，增加第一个，减少最后一个指针，并继续迭代，直到第一个小于最后一个。

## C++

```
// C++ program to print all palindromic partitions
// of a given string.
#include <bits/stdc++.h>
using namespace std;

// Returns true if str is palindrome, else false
bool checkPalindrome(string str)
{
    int len = str.length();
    len--;
    for (int i=0; i<len; i++)
    {
        if (str[i] != str[len])
            return false;
        len--;
    }
    return true;
}

void printSolution(vector<vector<string> > partitions)
{
    for (int i = 0; i < partitions.size(); ++i)
    {
        for(int j = 0; j < partitions[i].size(); ++j)
            cout << partitions[i][j] << " ";
        cout << endl;
    }
    return;
}

// Goes through all indexes and recursively add remaining
// partitions if current string is palindrome.
void addStrings(vector<vector<string> > &v, string &s,
                vector<string> &temp, int index)
{
    int len = s.length();
    string str;
    vector<string> current = temp;
    if (index == 0)
        temp.clear();
    for (int i = index; i < len; ++i)
    {
        str = str + s[i];
        if (checkPalindrome(str))
        {
            temp.push_back(str);
            if (i+1 < len)
                addStrings(v,s,temp,i+1);
            else
                v.push_back(temp);
            temp = current;
        }
    }
    return;
}

// Generates all palindromic partitions of 's' and
// stores the result in 'v'.
void partition(string s, vector<vector<string> >&v)
{
    vector<string> temp;
    addStrings(v, s, temp, 0);
    printSolution(v);
    return;
}

// Driver code
int main()
{
    string s = "geeks";
    vector<vector<string> > partitions;
    partition(s, partitions);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all palindromic partitions
// of a given string.
import java.util.ArrayList;
public class GFG 
{     
    // Returns true if str is palindrome, else false
    static boolean checkPalindrome(String str)
    {
        int len = str.length();
        len--;
        for (int i=0; i<len; i++)
        {
            if (str.charAt(i) != str.charAt(len))
                return false;
            len--;
        }
        return true;
    }

    // Prints the partition list
    static void printSolution(ArrayList<ArrayList<String>> 
                                          partitions)
    {
        for(ArrayList<String> i: partitions)
        {
            for(String j: i)
            {
                System.out.print(j+" ");
            }
            System.out.println();
        }
    }

    // Goes through all indexes and recursively add remaining
    // partitions if current string is palindrome.
    static ArrayList<ArrayList<String>> addStrings(ArrayList<
       ArrayList<String>> v, String s, ArrayList<String> temp, 
                                             int index)
    {
        int len = s.length();
        String str = "";
        ArrayList<String> current = new ArrayList<>(temp);

        if (index == 0)
            temp.clear();

        // Iterate over the string
        for (int i = index; i < len; ++i)
        {
            str = str + s.charAt(i);

            // check whether the substring is 
            // palindromic or not
            if (checkPalindrome(str))
            {
                // if palindrome add it to temp list
                temp.add(str);

                if (i + 1 < len)
                {    
                    // recurr to get all the palindromic
                    // partitions for the substrings
                    v = addStrings(v,s,temp,i+1);
                }
                else
                {
                    // if end of the string is reached 
                    // add temp to v
                    v.add(temp);
                }

                // temp is reinitialize with the 
                // current i.
                temp = new ArrayList<>(current);
            }
        }
        return v;
    }

    // Generates all palindromic partitions of 's' and
    // stores the result in 'v'.
    static void partition(String s, ArrayList<ArrayList<
                                          String>> v)
    {
        // temporary ArrayList to store each
        // palindromic string
        ArrayList<String> temp = new ArrayList<>();

        // calling addString method it adds all  
        // the palindromic partitions to v
        v = addStrings(v, s, temp, 0);

        // printing the solution
        printSolution(v);
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "geeks";
        ArrayList<ArrayList<String>> partitions = new
                                           ArrayList<>();
        partition(s, partitions);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to print all palindromic 
# partitions of a given string.
def checkPalindrome(string):

    # Returns true if str is palindrome, 
    # else false
    length = len(string)
    length -= 1
    for i in range(length):
        if string[i] != string[length]:
            return False
        length -= 1
    return True

def printSolution(partitions):
    for i in range(len(partitions)):
        for j in range(len(partitions[i])):
            print(partitions[i][j], end = " ")
        print()

def addStrings(v, s, temp, index):

    # Goes through all indexes and 
    # recursively add remaining partitions 
    # if current string is palindrome.
    length = len(s)
    string = ""

    current = temp[:]

    if index == 0:
        temp = []
    for i in range(index, length):
        string += s[i]
        if checkPalindrome(string):
            temp.append(string)
            if i + 1 < length:
                addStrings(v, s, temp[:], i + 1)
            else:
                v.append(temp)
            temp = current

def partition(s, v):

    # Generates all palindromic partitions 
    # of 's' and stores the result in 'v'.
    temp = []
    addStrings(v, s, temp[:], 0)
    printSolution(v)

# Driver Code
if __name__ == "__main__":
    s = "geeks"
    partitions = []
    partition(s, partitions)

# This code is contributed by
# vibhu4agarwal
```

## C#

```
// C# program to print all palindromic partitions
// of a given string.
using System;
using System.Collections.Generic;

class GFG 
{     
    // Returns true if str is palindrome, else false
    static bool checkPalindrome(String str)
    {
        int len = str.Length;
        len--;
        for (int i = 0; i < len; i++)
        {
            if (str[i] != str[len])
                return false;
            len--;
        }
        return true;
    }

    // Prints the partition list
    static void printSolution(List<List<String>> 
                                        partitions)
    {
        foreach(List<String> i in partitions)
        {
            foreach(String j in i)
            {
                Console.Write(j+" ");
            }
            Console.WriteLine();
        }
    }

    // Goes through all indexes and recursively add remaining
    // partitions if current string is palindrome.
    static List<List<String>> addStrings(List<
    List<String>> v, String s, List<String> temp, 
                                            int index)
    {
        int len = s.Length;
        String str = "";
        List<String> current = new List<String>(temp);

        if (index == 0)
            temp.Clear();

        // Iterate over the string
        for (int i = index; i < len; ++i)
        {
            str = str + s[i];

            // check whether the substring is 
            // palindromic or not
            if (checkPalindrome(str))
            {
                // if palindrome add it to temp list
                temp.Add(str);

                if (i + 1 < len)
                { 
                    // recurr to get all the palindromic
                    // partitions for the substrings
                    v = addStrings(v,s,temp,i+1);
                }
                else
                {
                    // if end of the string is reached 
                    // add temp to v
                    v.Add(temp);
                }

                // temp is reinitialize with the 
                // current i.
                temp = new List<String>(current);
            }
        }
        return v;
    }

    // Generates all palindromic partitions of 's' and
    // stores the result in 'v'.
    static void partition(String s, List<List<
                                        String>> v)
    {
        // temporary List to store each
        // palindromic string
        List<String> temp = new List<String>();

        // calling addString method it adds all 
        // the palindromic partitions to v
        v = addStrings(v, s, temp, 0);

        // printing the solution
        printSolution(v);
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "geeks";
        List<List<String>> partitions = new
                                        List<List<String>>();
        partition(s, partitions);
    }
}

// This code is contributed by PrinciRaj1992
```

**Output :**

```
g e e k s 
g ee k s
```

**相关文章:**
[动态规划|第 17 集(回文分区)](https://www.geeksforgeeks.org/dynamic-programming-set-17-palindrome-partitioning/)

本文由**安舒·戈亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论