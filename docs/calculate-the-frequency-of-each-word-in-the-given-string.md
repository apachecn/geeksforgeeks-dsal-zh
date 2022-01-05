# 计算给定字符串中每个单词的出现频率

> 原文:[https://www . geesforgeks . org/计算给定字符串中每个单词的出现频率/](https://www.geeksforgeeks.org/calculate-the-frequency-of-each-word-in-the-given-string/)

给定一个字符串 **str** ，任务是找出一个字符串中每个单词的出现频率。

**示例:**

> **输入:** str = "Geeks For Geeks"
> **输出:**
> For 1
> Geeks 2
> **解释:**
> For 在给定的字符串 str 中出现 1 次，Geeks 出现 2 次。
> 
> **输入:** str = "学习编码就是学习创造和创新"
> **输出:**
> 和 1
> 编码 1
> 创造 1
> 创新 1
> 是 1
> 学习 2
> 到 2
> **解释:**
> 这个词和，编码，创造，创新，是发生 1 次；和学习，在给定的字符串中出现两次。

**方法:**要解决上述问题，我们必须遵循以下步骤:

*   使用[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)数据结构来存储字符串中每个单词的出现。
*   遍历整个字符串，检查当前单词是否出现在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。如果存在，则更新当前单词的频率，否则插入频率为 1 的单词。
*   在地图中遍历并打印每个单词的频率。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the frequency
// of each word in the given string

#include <bits/stdc++.h>
using namespace std;

// Function to print frequency of each word
void printFrequency(string str)
{
    map<string, int> M;

    // String for storing the words
    string word = "";

    for (int i = 0; i < str.size(); i++) {

        // Check if current character
        // is blank space then it
        // means we have got one word
        if (str[i] == ' ') {

            // If the current word
            // is not found then insert
            // current word with frequency 1
            if (M.find(word) == M.end()) {
                M.insert(make_pair(word, 1));
                word = "";
            }

            // update the frequency
            else {
                M[word]++;
                word = "";
            }
        }

        else
            word += str[i];
    }

    // Storing the last word of the string
    if (M.find(word) == M.end())
        M.insert(make_pair(word, 1));

    // Update the frequency
    else
        M[word]++;

    // Traverse the map
    // to print the  frequency
    for (auto& it : M) {
        cout << it.first << " - "
             << it.second
             << endl;
    }
}

// Driver Code
int main()
{
    string str = "Geeks For Geeks";

    printFrequency(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above
// approach

import java.util.Map;
import java.util.TreeMap;
public class Frequency_Of_String_Words {

    // Function to count frequency of
    // words in the given string
    static void count_freq(String str)
    {
        Map<String,Integer> mp=new TreeMap<>();

        // Splitting to find the word
        String arr[]=str.split(" ");

        // Loop to iterate over the words
        for(int i=0;i<arr.length;i++)
        {
            // Condition to check if the
            // array element is present
            // the hash-map
            if(mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i])+1);
            }
            else
            {
                mp.put(arr[i],1);
            }
        }

        // Loop to iterate over the
        // elements of the map
        for(Map.Entry<String,Integer> entry:
                    mp.entrySet())
        {
            System.out.println(entry.getKey()+
                    " - "+entry.getValue());
        }
    }

    // Driver Code
    public static void main(String[] args) {
        String str = "Geeks For Geeks";

        // Function Call
        count_freq(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate the frequency
# of each word in the given string

# Function to print frequency of each word
def printFrequency(strr):
    M = {}

    # string for storing the words
    word = ""

    for i in range(len(strr)):

        # Check if current character
        # is blank space then it
        # means we have got one word
        if (strr[i] == ' '):

            # If the current word    
            # is not found then insert
            # current word with frequency 1
            if (word not in M):
                M[word] = 1
                word = ""

            # update the frequency
            else:
                M[word] += 1
                word = ""

        else:
            word += strr[i]

    # Storing the last word of the string
    if (word not in M):
        M[word] = 1

    # Update the frequency
    else:
        M[word] += 1

    # Traverse the map
    # to print the frequency
    for it in M:
        print(it, "-", M[it])

# Driver Code
strr = "Geeks For Geeks"
printFrequency(strr)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the above
// approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count frequency of
// words in the given string
static void count_freq(String str)
{
    SortedDictionary<String,
                     int> mp = new SortedDictionary<String,
                                                    int>();

    // Splitting to find the word
    String []arr = str.Split(' ');

    // Loop to iterate over the words
    for(int i = 0; i < arr.Length; i++)
    {

        // Condition to check if the
        // array element is present
        // the hash-map
        if (mp.ContainsKey(arr[i]))
        {
            mp[arr[i]] = mp[arr[i]] + 1;
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Loop to iterate over the
    // elements of the map
    foreach(KeyValuePair<String, int> entry in mp)
    {
        Console.WriteLine(entry.Key + " - " +
                          entry.Value);
    }
}

// Driver Code
public static void Main(String[] args)
{
    String str = "Geeks For Geeks";

    // Function call
    count_freq(str);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
For - 1
Geeks - 2
```