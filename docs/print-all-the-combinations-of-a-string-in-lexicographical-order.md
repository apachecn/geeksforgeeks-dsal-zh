# 按照字典顺序打印一个字符串的所有组合

> 原文:[https://www . geesforgeks . org/print-所有按字典顺序排列的字符串组合/](https://www.geeksforgeeks.org/print-all-the-combinations-of-a-string-in-lexicographical-order/)

给定一个字符串，按字典顺序打印一个字符串的所有组合。
**例:**

```
Input: str = "ABC"
Output:
A
AB
ABC
AC
ACB
B
BA
BAC
BC
BCA
C
CA
CAB
CB
CBA

Input: ED
Output:
D
DE
E
ED
```

**方法:**用地图计算字符串中所有字符的出现次数，然后用递归打印所有可能的组合。将元素及其计数存储在两个不同的数组中。使用三个数组，输入[]有字符的数组，计数[]有字符的数组，结果[]是一个临时数组，用于[递归](http://www.geeksforgeeks.org/recursion/)来生成所有的组合。使用[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)可以打印所有组合。
以下是上述办法的实施情况。

## C++

```
// C++ program to find all combinations
// of a string in lexicographical order
#include <bits/stdc++.h>
using namespace std;

// function to print string
void printResult(char* result, int len)
{
    for (int i = 0; i <= len; i++)
        cout << result[i];
    cout << endl;
}

// Method to found all combination
// of string it is based in tree
void stringCombination(char result[], char str[], int count[],
                       int level, int size, int length)
{
    // return if level is equal size of string
    if (level == size)
        return;

    for (int i = 0; i < length; i++) {

        // if occurrence of char is 0 then
        // skip the iteration of loop
        if (count[i] == 0)
            continue;

        // decrease the char occurrence by 1
        count[i]--;

        // store the char in result
        result[level] = str[i];

        // print the string till level
        printResult(result, level);

        // call the function from level +1
        stringCombination(result, str, count,
                          level + 1, size, length);

        // backtracking
        count[i]++;
    }
}

void combination(string str)
{

    // declare the map for store
    // each char with occurrence
    map<char, int> mp;

    for (int i = 0; i < str.size(); i++) {

        if (mp.find(str[i]) != mp.end())
            mp[str[i]] = mp[str[i]] + 1;
        else
            mp[str[i]] = 1;
    }

    // initialize the input array
    // with all unique char
    char* input = new char[mp.size()];

    // initialize the count array with
    // occurrence the unique char
    int* count = new int[mp.size()];

    // temporary char array for store the result
    char* result = new char[str.size()];

    map<char, int>::iterator it = mp.begin();
    int i = 0;

    for (it; it != mp.end(); it++) {
        // store the element of input array
        input[i] = it->first;

        // store the element of count array
        count[i] = it->second;
        i++;
    }

    // size of map(no of unique char)
    int length = mp.size();

    // size of original string
    int size = str.size();

    // call function for print string combination
    stringCombination(result, input, count,
                      0, size, length);
}

// Driver code
int main()
{
    string str = "ABC";

    combination(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all combinations
// of a string in lexicographical order
import java.util.HashMap;

class GFG
{

    // function to print string
    static void printResult(char[] result,
                            int len)
    {
        for (int i = 0; i <= len; i++)
            System.out.print(result[i]);
        System.out.println();
    }

    // Method to found all combination
    // of string it is based in tree
    static void stringCombination(char[] result, char[] str,
                                  int[] count, int level,
                                  int size, int length)
    {

        // return if level is equal size of string
        if (level == size)
            return;

        for (int i = 0; i < length; i++)
        {

            // if occurrence of char is 0 then
            // skip the iteration of loop
            if (count[i] == 0)
                continue;

            // decrease the char occurrence by 1
            count[i]--;

            // store the char in result
            result[level] = str[i];

            // print the string till level
            printResult(result, level);

            // call the function from level +1
            stringCombination(result, str, count,
                              level + 1, size, length);

            // backtracking
            count[i]++;
        }
    }

    static void combination(String str)
    {

        // declare the map for store
        // each char with occurrence
        HashMap<Character,
                Integer> mp = new HashMap<>();

        for (int i = 0; i < str.length(); i++)
            mp.put(str.charAt(i), mp.get(str.charAt(i)) == null ? 1 :
                                  mp.get(str.charAt(i)) + 1);

        // initialize the input array
        // with all unique char
        char[] input = new char[mp.size()];

        // initialize the count array with
        // occurrence the unique char
        int[] count = new int[mp.size()];

        // temporary char array for store the result
        char[] result = new char[str.length()];

        int i = 0;
        for (HashMap.Entry<Character,
                           Integer> entry : mp.entrySet())
        {

            // store the element of input array
            input[i] = entry.getKey();

            // store the element of count array
            count[i] = entry.getValue();
            i++;
        }

        // size of map(no of unique char)
        int length = mp.size();

        // size of original string
        int size = str.length();

        // call function for print string combination
        stringCombination(result, input, count, 0,
                                    size, length);
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "ABC";
        combination(str);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 program to find all combinations
# of a string in lexicographical order
from collections import defaultdict

# function to print string

def printResult(result, length):

    for i in range(length+1):
        print(result[i], end="")
    print()

# Method to found all combination
# of string it is based in tree

def stringCombination(result, st, count,
                      level, size, length):

    # return if level is equal size of string
    if (level == size):
        return

    for i in range(length):

        # if occurrence of char is 0 then
        # skip the iteration of loop
        if (count[i] == 0):
            continue

        # decrease the char occurrence by 1
        count[i] -= 1

        # store the char in result
        result[level] = st[i]

        # print the string till level
        printResult(result, level)

        # call the function from level +1
        stringCombination(result, st, count,
                          level + 1, size, length)

        # backtracking
        count[i] += 1

def combination(st):

    # declare the map for store
    # each char with occurrence
    mp = defaultdict(int)

    for i in range(len(st)):

        if (st[i] in mp.keys()):
            mp[st[i]] = mp[st[i]] + 1

        else:
            mp[st[i]] = 1

    # initialize the input array
    # with all unique char
    input = ['']*len(mp)

    # initialize the count array with
    # occurrence the unique char
    count = [0] * len(mp)

    # temporary char array for store the result
    result = ['']*len(st)

    i = 0

    for key, value in mp.items():
        # store the element of input array
        input[i] = key

        # store the element of count array
        count[i] = value
        i += 1

    # size of map(no of unique char)
    length = len(mp)

    # size of original string
    size = len(st)

    # call function for print string combination
    stringCombination(result, input, count,
                      0, size, length)

# Driver code
if __name__ == "__main__":

    st = "ABC"
    combination(st)

    # This code is contributed by ukasp.
```

## C#

```
// C# program to find all combinations
// of a string in lexicographical order
using System;
using System.Collections.Generic;

class GFG
{

    // function to print string
    static void printResult(char[] result,
                            int len)
    {
        for (int i = 0; i <= len; i++)
            Console.Write(result[i]);
        Console.WriteLine();
    }

    // Method to found all combination
    // of string it is based in tree
    static void stringCombination(char[] result, char[] str,
                                int[] count, int level,
                                int size, int length)
    {

        // return if level is equal size of string
        if (level == size)
            return;

        for (int i = 0; i < length; i++)
        {

            // if occurrence of char is 0 then
            // skip the iteration of loop
            if (count[i] == 0)
                continue;

            // decrease the char occurrence by 1
            count[i]--;

            // store the char in result
            result[level] = str[i];

            // print the string till level
            printResult(result, level);

            // call the function from level +1
            stringCombination(result, str, count,
                            level + 1, size, length);

            // backtracking
            count[i]++;
        }
    }

    static void combination(String str)
    {
        int i;

        // declare the map for store
        // each char with occurrence
        Dictionary<char,int> mp = new Dictionary<char,int>();

        for (i= 0; i < str.Length; i++)
            if(mp.ContainsKey(str[i]))
                mp[str[i]] = mp[str[i]] + 1;
            else
                mp.Add(str[i], 1);

        // initialize the input array
        // with all unique char
        char[] input = new char[mp.Count];

        // initialize the count array with
        // occurrence the unique char
        int[] count = new int[mp.Count];

        // temporary char array for store the result
        char[] result = new char[str.Length];

        i = 0;
        foreach(KeyValuePair<char, int> entry in mp)
        {

            // store the element of input array
            input[i] = entry.Key;

            // store the element of count array
            count[i] = entry.Value;
            i++;
        }

        // size of map(no of unique char)
        int length = mp.Count;

        // size of original string
        int size = str.Length;

        // call function for print string combination
        stringCombination(result, input, count, 0,
                                    size, length);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "ABC";
        combination(str);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program to find all combinations
      // of a string in lexicographical order
      // function to print string
      function printResult(result, len) {
        for (var i = 0; i <= len; i++) document.write(result[i]);
        document.write("<br>");
      }

      // Method to found all combination
      // of string it is based in tree
      function stringCombination(result, str, count, level, size, len) {
        // return if level is equal size of string
        if (level === size) return;

        for (var i = 0; i < len; i++) {
          // if occurrence of char is 0 then
          // skip the iteration of loop
          if (count[i] === 0) continue;

          // decrease the char occurrence by 1
          count[i]--;

          // store the char in result
          result[level] = str[i];

          // print the string till level
          printResult(result, level);

          // call the function from level +1
          stringCombination(result, str, count, level + 1, size, len);

          // backtracking
          count[i]++;
        }
      }

      function combination(str) {
        var i;

        // declare the map for store
        // each char with occurrence
        var mp = {};

        for (i = 0; i < str.length; i++)
          if (mp.hasOwnProperty(str[i])) mp[str[i]] = mp[str[i]] + 1;
          else mp[str[i]] = 1;

        // initialize the input array
        // with all unique char
        var input = new Array(Object.keys(mp).length).fill(0);

        // initialize the count array with
        // occurrence the unique char
        var count = new Array(Object.keys(mp).length).fill(0);

        // temporary char array for store the result
        var result = new Array(str.length).fill(0);

        i = 0;
        for (const [key, value] of Object.entries(mp)) {
          // store the element of input array
          input[i] = key;

          // store the element of count array
          count[i] = value;
          i++;
        }

        // size of map(no of unique char)
        var len = Object.keys(mp).length;

        // size of original string
        var size = str.length;

        // call function for print string combination
        stringCombination(result, input, count, 0, size, len);
      }

      // Driver code
      var str = "ABC";
      combination(str);
    </script>
```

**Output:** 

```
A
AB
ABC
AC
ACB
B
BA
BAC
BC
BCA
C
CA
CAB
CB
CBA
```

**时间复杂度:** O( ![2 ^ N   ](img/c068f3f9c980e19a3a0b5d21071fb51c.png "Rendered by QuickLaTeX.com"))其中 N 是字符串的大小。
**辅助空间:** O(N)