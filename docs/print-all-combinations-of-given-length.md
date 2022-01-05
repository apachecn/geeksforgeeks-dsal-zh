# 打印所有可能的长度为 k 的字符串，这些字符串可以由一组 n 个字符组成

> 原文:[https://www . geesforgeks . org/print-所有给定长度的组合/](https://www.geeksforgeeks.org/print-all-combinations-of-given-length/)

给定一组字符和一个正整数 k，打印所有可能的长度为 k 的字符串，这些字符串可以由给定的字符集组成。

**示例:**

```
Input: 
set[] = {'a', 'b'}, k = 3

Output:
aaa
aab
aba
abb
baa
bab
bba
bbb

Input: 
set[] = {'a', 'b', 'c', 'd'}, k = 1
Output:
a
b
c
d
```

对于给定的一组大小为 n 的字符串，将会有长度为 k 的 n^k 可能的字符串，其思想是从一个空的输出字符串开始(我们在下面的代码中称之为*前缀*)。逐个将所有字符添加到*前缀*中。对于添加的每个字符，通过递归调用等于 k-1 的 k 来打印当前前缀的所有可能的字符串。

以下是上述想法的实现:

## C++

```
// C++ program to print all
// possible strings of length k
#include <bits/stdc++.h>
using namespace std;

// The main recursive method
// to print all possible
// strings of length k
void printAllKLengthRec(char set[], string prefix,
                                    int n, int k)
{

    // Base case: k is 0,
    // print prefix
    if (k == 0)
    {
        cout << (prefix) << endl;
        return;
    }

    // One by one add all characters
    // from set and recursively
    // call for k equals to k-1
    for (int i = 0; i < n; i++)
    {
        string newPrefix;

        // Next character of input added
        newPrefix = prefix + set[i];

        // k is decreased, because
        // we have added a new character
        printAllKLengthRec(set, newPrefix, n, k - 1);
    }

}

void printAllKLength(char set[], int k,int n)
{
    printAllKLengthRec(set, "", n, k);
}

// Driver Code
int main()
{

    cout << "First Test" << endl;
    char set1[] = {'a', 'b'};
    int k = 3;
    printAllKLength(set1, k, 2);

    cout << "Second Test\n";
    char set2[] = {'a', 'b', 'c', 'd'};
    k = 1;
    printAllKLength(set2, k, 4);
}

// This code is contributed
// by Mohit kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// possible strings of length k

class GFG {

// The method that prints all
// possible strings of length k.
// It is mainly a wrapper over
// recursive function printAllKLengthRec()
static void printAllKLength(char[] set, int k)
{
    int n = set.length;
    printAllKLengthRec(set, "", n, k);
}

// The main recursive method
// to print all possible
// strings of length k
static void printAllKLengthRec(char[] set,
                               String prefix,
                               int n, int k)
{

    // Base case: k is 0,
    // print prefix
    if (k == 0)
    {
        System.out.println(prefix);
        return;
    }

    // One by one add all characters
    // from set and recursively
    // call for k equals to k-1
    for (int i = 0; i < n; ++i)
    {

        // Next character of input added
        String newPrefix = prefix + set[i];

        // k is decreased, because
        // we have added a new character
        printAllKLengthRec(set, newPrefix,
                                n, k - 1);
    }
}

// Driver Code
public static void main(String[] args)
{
    System.out.println("First Test");
    char[] set1 = {'a', 'b'};
    int k = 3;
    printAllKLength(set1, k);

    System.out.println("\nSecond Test");
    char[] set2 = {'a', 'b', 'c', 'd'};
    k = 1;
    printAllKLength(set2, k);
}
}
```

## 蟒蛇 3

```
# Python 3 program to print all
# possible strings of length k

# The method that prints all
# possible strings of length k.
# It is mainly a wrapper over
# recursive function printAllKLengthRec()
def printAllKLength(set, k):

    n = len(set)
    printAllKLengthRec(set, "", n, k)

# The main recursive method
# to print all possible
# strings of length k
def printAllKLengthRec(set, prefix, n, k):

    # Base case: k is 0,
    # print prefix
    if (k == 0) :
        print(prefix)
        return

    # One by one add all characters
    # from set and recursively
    # call for k equals to k-1
    for i in range(n):

        # Next character of input added
        newPrefix = prefix + set[i]

        # k is decreased, because
        # we have added a new character
        printAllKLengthRec(set, newPrefix, n, k - 1)

# Driver Code
if __name__ == "__main__":

    print("First Test")
    set1 = ['a', 'b']
    k = 3
    printAllKLength(set1, k)

    print("\nSecond Test")
    set2 = ['a', 'b', 'c', 'd']
    k = 1
    printAllKLength(set2, k)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print all
// possible strings of length k
using System;

class GFG {

// The method that prints all
// possible strings of length k.
// It is mainly a wrapper over
// recursive function printAllKLengthRec()
static void printAllKLength(char[] set, int k)
{
    int n = set.Length;
    printAllKLengthRec(set, "", n, k);
}

// The main recursive method
// to print all possible
// strings of length k
static void printAllKLengthRec(char[] set,
                               String prefix,
                               int n, int k)
{

    // Base case: k is 0,
    // print prefix
    if (k == 0)
    {
        Console.WriteLine(prefix);
        return;
    }

    // One by one add all characters
    // from set and recursively
    // call for k equals to k-1
    for (int i = 0; i < n; ++i)
    {

        // Next character of input added
        String newPrefix = prefix + set[i];

        // k is decreased, because
        // we have added a new character
        printAllKLengthRec(set, newPrefix,
                                n, k - 1);
    }
}

// Driver Code
static public void Main ()
{
    Console.WriteLine("First Test");
    char[] set1 = {'a', 'b'};
    int k = 3;
    printAllKLength(set1, k);

    Console.WriteLine("\nSecond Test");
    char[] set2 = {'a', 'b', 'c', 'd'};
    k = 1;
    printAllKLength(set2, k);
}
}

// This code is contributed by Ajit.
```

## java 描述语言

```
<script>
// Javascript program to print all
// possible strings of length k  

    // The method that prints all
    // possible strings of length k.
    // It is mainly a wrapper over
    // recursive function printAllKLengthRec()
    function printAllKLength(set,k)
    {
        let n = set.length;
        printAllKLengthRec(set, "", n, k);
    }

    // The main recursive method
    // to print all possible
    // strings of length k
    function printAllKLengthRec(set,prefix,n,k)
    {
        // Base case: k is 0,
        // print prefix
        if (k == 0)
        {
            document.write(prefix+"<br>");
            return;
        }

        // One by one add all characters
        // from set and recursively
        // call for k equals to k-1
        for (let i = 0; i < n; ++i)
        {

            // Next character of input added
            let newPrefix = prefix + set[i];

            // k is decreased, because
            // we have added a new character
            printAllKLengthRec(set, newPrefix,
                                    n, k - 1);
        }
    }

    // Driver Code
    document.write("First Test<br>");
    let set1=['a', 'b'];
    let k = 3;
    printAllKLength(set1, k);

    document.write("<br>Second Test<br>");
    let set2 = ['a', 'b', 'c', 'd'];
    k = 1;
    printAllKLength(set2, k);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
First Test
aaa
aab
aba
abb
baa
bab
bba
bbb

Second Test
a
b
c
d
```

以上解决方案主要是[这个帖子](https://www.geeksforgeeks.org/print-all-permutations-with-repetition-of-characters/)的概括。

本文由 [**阿比纳夫·拉玛那**](https://plus.google.com/104230157879525004164/posts) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息