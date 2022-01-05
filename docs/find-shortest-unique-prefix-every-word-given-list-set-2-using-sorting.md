# 为给定列表中的每个单词找到最短的唯一前缀|集合 2(使用排序)

> 原文:[https://www . geesforgeks . org/find-最短-唯一-前缀-每个单词-给定-列表-集合-2-使用-排序/](https://www.geeksforgeeks.org/find-shortest-unique-prefix-every-word-given-list-set-2-using-sorting/)

给定一个单词数组，找到所有最短的唯一前缀来表示给定数组中的每个单词。假设没有一个单词是另一个单词的前缀。按排序顺序输出最短的唯一前缀。

```
Input  : {"zebra", "dog", "duck", "dove"}
Output : z, dog, dov, du
Explanation: dog => dog
             dove = dov 
             duck = du
             z   => zebra 

Input: {"geeksgeeks", "geeksquiz", "geeksforgeeks"}
Output: geeksf, geeksg, geeksq
```

我们已经在下面的帖子中讨论了基于 Trie 的方法。
[为给定列表中的每个单词找到最短的唯一前缀| Set 1(使用 Trie)](https://www.geeksforgeeks.org/find-all-shortest-unique-prefixes-to-represent-each-word-in-a-given-list/)
在这篇文章中，讨论了一种基于排序的方法。通过将该字符串与数组中其他两个最相似的字符串进行比较，我们可以找到其最短的唯一前缀。例如，如果我们对数组{“斑马”、“狗”、“鸭子”、“鸽子”}进行排序，我们会得到{“狗”、“鸽子”、“鸭子”、“斑马”}。字符串“dove”的最短唯一前缀可以找到:
比较“dove”和“dog”——>dove 的唯一前缀是“dov”
比较“dove”和“duck”——>dove 的唯一前缀是“do”
现在，“dove”的最短唯一前缀是“dov”和“do”之间长度较大的那个。所以，它是“dov”。
第一个和最后一个字符串的最短唯一前缀可以通过分别与左右最相似的 1 个邻居进行比较来找到。

我们可以对字符串数组进行排序，并对数组中的每个字符串继续这样做。

## C++

```
// C++ program to print shortest unique prefixes
// for every word.
#include <bits/stdc++.h>
using namespace std;

vector<string> uniquePrefix(vector<string> &a)
{
    int size = a.size();

    /* create an array to store the results */
    vector<string> res(size);

    /* sort the array of strings */
    sort(a.begin(), a.end());

    /* compare the first string with its only right
    neighbor */
    int j = 0;
    while (j < min(a[0].length() - 1, a[1].length() - 1))
    {
        if (a[0][j] == a[1][j])
            j++;
        else
            break;
    }
    int ind = 0;
    res[ind++] = a[0].substr(0, j + 1);

    /* Store the unique prefix of a[1] from its left neighbor */
    string temp_prefix = a[1].substr(0, j + 1);
    for (int i = 1; i < size - 1; i++)
    {
        /* compute common prefix of a[i] unique from
        its right neighbor */
        j = 0;
        while (j < min(a[i].length() - 1, a[i + 1].length() - 1))
        {
            if (a[i][j] == a[i + 1][j])
                j++;
            else
                break;
        }

        string new_prefix = a[i].substr(0, j + 1);

        /* compare the new prefix with previous prefix */
        if (temp_prefix.length() > new_prefix.length())
            res[ind++] = temp_prefix;
        else
            res[ind++] = new_prefix;

        /* store the prefix of a[i+1] unique from its
        left neighbour */
        temp_prefix = a[i + 1].substr(0, j + 1);
    }

    /* compute the unique prefix for the last string
    in sorted array */
    j = 0;
    string sec_last = a[size - 2];

    string last = a[size - 1];

    while (j < min(sec_last.length() - 1, last.length() - 1))
    {
        if (sec_last[j] == last[j])
            j++;
        else
            break;
    }

    res[ind] = last.substr(0, j + 1);
    return res;
}

// Driver Code
int main()
{
    vector<string> input = {"zebra", "dog", "duck", "dove"};
    vector<string> output = uniquePrefix(input);
    cout << "The shortest unique prefixes in sorted order are : \n";

    for (auto i : output)
        cout << i << ' ';

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print shortest unique prefixes
// for every word.
import java.io.*;
import java.util.*;

class GFG
{
    public String[] uniquePrefix(String[] a)
    {
        int size = a.length;

        /* create an array to store the results */
        String[] res = new String[size];

        /* sort the array of strings */
        Arrays.sort(a);

        /* compare the first string with its only right
           neighbor */
        int j = 0;
        while (j < Math.min(a[0].length()-1, a[1].length()-1))
        {
            if (a[0].charAt(j)==a[1].charAt(j))
                j++;
            else
                break;
        }

        int ind = 0;
        res[ind++] = a[0].substring(0, j+1);

        /* Store the unique prefix of a[1] from its left neighbor */
        String temp_prefix = a[1].substring(0, j+1);
        for (int i = 1; i < size-1; i++)
        {
            /* compute common prefix of a[i] unique from
               its right neighbor */
            j = 0;
            while (j < Math.min( a[i].length()-1, a[i+1].length()-1 ))
            {
                if (a[i].charAt(j) == a[i+1].charAt(j))
                    j++;
                else
                    break;
            }

            String new_prefix = a[i].substring(0, j+1);

            /* compare the new prefix with previous prefix */
            if (temp_prefix.length() > new_prefix.length() )
                res[ind++] = temp_prefix;
            else
                res[ind++] = new_prefix;

            /* store the prefix of a[i+1] unique from its
               left neighbour */
            temp_prefix = a[i+1].substring(0, j+1);
        }

        /* compute the unique prefix for the last string
           in sorted array */
        j = 0;
        String sec_last = a[size-2] ;

        String last = a[size-1];

        while (j < Math.min( sec_last.length()-1, last.length()-1))
        {
            if (sec_last.charAt(j) == last.charAt(j))
                j++;
            else
                break;
        }

        res[ind] = last.substring(0, j+1);
        return res;
    }

    /* Driver Function to test other function */
    public static void main(String[] args)
    {
        GFG gfg = new GFG();

        String[] input = {"zebra", "dog", "duck", "dove"};

        String[] output = gfg.uniquePrefix(input);
        System.out.println( "The shortest unique prefixes" +
                               " in sorted order are :");

        for (int i=0; i < output.length; i++)
            System.out.print( output[i] + " ");
    }
}
```

## 蟒蛇 3

```
# Python3 program to prshortest unique prefixes
# for every word.
def uniquePrefix(a):

    size = len(a)

    # Create an array to store the results
    res = [0] * (size)

    # Sort the array of strings */
    a = sorted(a)

    # Compare the first with its only right
    # neighbor
    j = 0
    while (j < min(len(a[0]) - 1, len(a[1]) - 1)):
        if (a[0][j] == a[1][j]):
            j += 1
        else:
            break

    ind = 0
    res[ind] = a[0][0:j + 1]
    ind += 1

    # Store the unique prefix of a[1]
    # from its left neighbor
    temp_prefix = a[1][0:j + 1]
    for i in range(1, size - 1):

        # Compute common prefix of a[i] unique from
        # its right neighbor
        j = 0

        while (j < min(len(a[i]) - 1, len(a[i + 1]) - 1)):
            if (a[i][j] == a[i + 1][j]):
                j += 1
            else:
                break

        new_prefix = a[i][0:j + 1]

        # Compare the new prefix with previous prefix
        if (len(temp_prefix) > len(new_prefix)):
            res[ind] = temp_prefix
            ind += 1
        else:
            res[ind] = new_prefix
            ind += 1

        # Store the prefix of a[i+1] unique from its
        # left neighbour
        temp_prefix = a[i + 1][0:j + 1]

    # Compute the unique prefix for the last
    # in sorted array
    j = 0
    sec_last = a[size - 2]

    last = a[size - 1]

    while (j < min(len(sec_last) - 1, len(last) - 1)):
        if (sec_last[j] == last[j]):
            j += 1
        else:
            break

    res[ind] = last[0:j + 1]
    return res

# Driver Code
if __name__ == '__main__':

    input = [ "zebra", "dog", "duck", "dove" ]
    output = uniquePrefix(input)

    print("The shortest unique prefixes " +
          "in sorted order are : ")

    for i in output:
        print(i, end = " ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print shortest unique prefixes
// for every word.
using System;

class GFG
{
    public String[] uniquePrefix(String[] a)
    {
        int size = a.Length;

        /* create an array to store the results */
        String[] res = new String[size];

        /* sort the array of strings */
        Array.Sort(a);

        /* compare the first string with its only right
        neighbor */
        int j = 0;
        while (j < Math.Min(a[0].Length - 1, a[1].Length - 1))
        {
            if (a[0][j] == a[1][j])
                j++;
            else
                break;
        }

        int ind = 0;
        res[ind++] = a[0].Substring(0, j + 1);

        /* Store the unique prefix of a[1] from its left neighbor */
        String temp_prefix = a[1].Substring(0, j + 1);
        for (int i = 1; i < size - 1; i++)
        {
            /* compute common prefix of a[i] unique from
            its right neighbor */
            j = 0;
            while (j < Math.Min( a[i].Length - 1, a[i + 1].Length - 1 ))
            {
                if (a[i][j] == a[i + 1][j])
                    j++;
                else
                    break;
            }

            String new_prefix = a[i].Substring(0, j+1);

            /* compare the new prefix with previous prefix */
            if (temp_prefix.Length > new_prefix.Length )
                res[ind++] = temp_prefix;
            else
                res[ind++] = new_prefix;

            /* store the prefix of a[i+1] unique from its
            left neighbour */
            temp_prefix = a[i+1].Substring(0, j+1);
        }

        /* compute the unique prefix for the last string
        in sorted array */
        j = 0;
        String sec_last = a[size-2] ;

        String last = a[size-1];

        while (j < Math.Min( sec_last.Length-1, last.Length-1))
        {
            if (sec_last[j] == last[j])
                j++;
            else
                break;
        }

        res[ind] = last.Substring(0, j+1);
        return res;
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        GFG gfg = new GFG();

        String[] input = {"zebra", "dog", "duck", "dove"};

        String[] output = gfg.uniquePrefix(input);
        Console.WriteLine( "The shortest unique prefixes" +
                            " in sorted order are :");

        for (int i = 0; i < output.Length; i++)
            Console.Write( output[i] + " ");
    }
}

// This code is contributed by Princi Singh
```

**输出:**

```
The shortest unique prefixes in sorted order are :
dog dov du z 
```

**另一种 Python 方法:**
如果我们想要输出前缀作为输入数组中字符串的顺序，我们可以将字符串及其对应的索引存储在 hashmap 中。在将前缀添加到结果数组时，我们可以从 hashmap 中获取相应字符串的索引，并将前缀添加到该索引中。

## 蟒蛇 3

```
#Python program to print shortest unique prefix for every word in a list

a=['dogs','dove','duck','zebra']
r=[]
j=0
while(j<min(len(a[0]),len(a[1]))):
    if(a[0][j]==a[1][j]):
        j+=1
    else:
        break

i=0
r.append(a[0][0:j+1])
x=a[1][0:j+1]

for i in range(1,len(a)-1):
    j=0
    while(j<min(len(a[i]),len(a[i+1]))):
        if a[i][j]==a[i+1][j]:
            j+=1
        else:
            break

    y=a[i][0:j+1]
    if(len(x)>len(y)):
        r.append(x)
    else:
        r.append(y)
    x=a[i+1][0:j+1]

j=0
l=a[len(a)-2]
k=a[len(a)-1]

while(j<min(len(l),len(k))):
    if ( l[j]==k[j]):
        j+=1
    else:
        break

r.append(k[0:j+1])
print("The shortest unique prefixes are :")
for i in range(0,len(r)):
  print(r[i],end=' ')

 #This code is contributed by Saahith Reddy
```

**输出:**

```
The shortest unique prefixes are :
dog dov du z
```

为了获得更有效的解决方案，我们可以使用本文[帖子](https://www.geeksforgeeks.org/find-all-shortest-unique-prefixes-to-represent-each-word-in-a-given-list/)中讨论的 Trie。
本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。