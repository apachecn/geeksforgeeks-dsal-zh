# 根据不同字符的数量对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/基于不同字符计数的字符串数组排序/](https://www.geeksforgeeks.org/sort-an-array-of-strings-based-on-count-of-distinct-characters/)

给定一个**字符串数组 arr[]** 作为输入，任务是打印单词，按照单词中出现的**不同**字符的数量排序，后跟单词的**长度**。

***注:***

*   *如果两个单词有相同数量的不同字符，则总字符数较多的单词优先。*
*   *如果两个单词有相同数量的不同字符和相同的长度，则必须首先打印句子中较早出现的单词。*

**示例:**

> ***输入:** arr[] =* {“香蕉”“做”“不做”“长”“在”“密西西比州”}
> ***输出:**做在不密西西比州香蕉长出来*
> ***解释:***
> *按唯一字符的数量和长度排序后输出将为，做在不密西西比州香蕉长出来。*
> 
> ***输入:*** arr[] = {“谢谢”、“你”、“极客”、“世界”}
> ***输出:*** 各位极客感谢世界
> ***解释:***
> *按独特字符的数量和长度排序后输出的将是，*各位极客感谢世界。

**进场:**思路是用[**排序**](https://www.geeksforgeeks.org/sorting-algorithms/) **。**

*   初始化一个**映射**数据结构，从给定数组的每个字符串中计算所有可能的不同字符。
*   然后通过传递比较器函数对数组进行排序，排序是通过单词中唯一字符的**号和单词的**长度**来完成的。**
*   排序完成后，打印数组的字符串。

> 例如 s = *“香蕉不生长在密西西比”*
> 
> ***唯一字符的字数**字数*
> 
> *做 2 2*
> 
> *在 2 中 2*
> 
> *不是 3 3*
> 
> *香蕉 4 7*
> 
> *成长 4 4*
> 
> *密西西比 4 11*

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return no of
// unique character in a word
int countDistinct(string s)
{
    // Initialize map
    unordered_map<char, int> m;

    for (int i = 0; i < s.length(); i++) {
        // Count distinct characters
        m[s[i]]++;
    }

    return m.size();
}

// Function to perform sorting
bool compare(string& s1, string& s2)
{
    if (countDistinct(s1) == countDistinct(s2)) {
        // Check if size of string 1
        // is same as string 2 then
        // return false because s1 should
        // not be placed before s2
        if (s1.size() == s2.size()) {
            return false;
        }
        return s1.size() > s2.size();
    }
    return countDistinct(s1) < countDistinct(s2);
}

// Function to print the sorted array of string
void printArraystring(string str[], int n)
{
    for (int i = 0; i < n; i++)
        cout << str[i] << " ";
}

// Driver Code
int main()
{
    string arr[] = { "Bananas", "do",
                     "not", "grow", "in",
                     "Mississippi" };
    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    sort(arr, arr + n, compare);

    // Print result
    printArraystring(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return no of
// unique character in a word
static int countDistinct(String s)
{

    // Initialize map
    Map<Character, Integer> m = new HashMap<>();

    for(int i = 0; i < s.length(); i++)
    {

        // Count distinct characters
        if (m.containsKey(s.charAt(i)))
        {
            m.put(s.charAt(i),
            m.get(s.charAt(i)) + 1);
        }
        else
        {
            m.put(s.charAt(i), 1);
        }
    }
    return m.size();
}

// Function to print the sorted
// array of string
static void printArraystring(String[] str,
                             int n)
{
    for(int i = 0; i < n; i++)
    {
        System.out.print(str[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    String[] arr = { "Bananas", "do",
                     "not", "grow",
                     "in", "Mississippi" };
    int n = arr.length;

    // Function call
    Arrays.sort(arr, new Comparator<String>()
    {
        public int compare(String a, String b)
        {
            if (countDistinct(a) ==
                countDistinct(b))
            {

                // Check if size of string 1
                // is same as string 2 then
                // return false because s1 should
                // not be placed before s2
                return (b.length() - a.length());
            }
            else
            {
                return (countDistinct(a) -
                        countDistinct(b));
            }
        }
    });

    // Print result
    printArraystring(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the above approach
import functools

# Function to return no of
# unique character in a word
def countDistinct(s):

    # Initialize dictionary
    m = {}

    for i in range(len(s)):

        # Count distinct characters
        if s[i] not in m:
            m[s[i]] = 1
        else:
            m[s[i]] += 1

    return len(m)

# Function to perform sorting
def compare(a, b):

    if (countDistinct(a) == countDistinct(b)):

        # Check if size of string 1
        # is same as string 2 then
        # return false because s1 should
        # not be placed before s2
        return (len(b) - len(a))
    else:
        return (countDistinct(a) - countDistinct(b))

# Driver Code
arr = [ "Bananas", "do", "not",
        "grow", "in","Mississippi" ]

n = len(arr)

# Print result
print(*sorted(
    arr, key = functools.cmp_to_key(compare)), sep = ' ')

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program of the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to return no of
// unique character in a word
static int countDistinct(string s)
{

    // Initialize map
    Dictionary<char,
               int> m = new Dictionary<char,
                                       int>();

    for(int i = 0; i < s.Length; i++)
    {

        // Count distinct characters
        if (m.ContainsKey(s[i]))
        {
            m[s[i]]++;
        }
        else
        {
            m[s[i]] = 1;
        }
    }
    return m.Count;
}

static int compare(string s1, string s2)
{
    if (countDistinct(s1) == countDistinct(s2))
    {

        // Check if size of string 1
        // is same as string 2 then
        // return false because s1 should
        // not be placed before s2
        return s2.Length - s1.Length;
    }
    else
    {
        return (countDistinct(s1) -
                countDistinct(s2));
    }
}

// Function to print the sorted array of string
static void printArraystring(string []str, int n)
{
    for(int i = 0; i < n; i++)
    {
        Console.Write(str[i] + " ");
    }
}

// Driver Code
public static void Main(string[] args)
{
    string []arr = { "Bananas", "do",
                     "not", "grow",
                     "in", "Mississippi" };
    int n = arr.Length;

    // Function call
    Array.Sort(arr, compare);

    // Print result
    printArraystring(arr, n);
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
do in not Mississippi Bananas grow
```

***时间复杂度:** O(n * log n)*

***辅助空间:** O(n)*