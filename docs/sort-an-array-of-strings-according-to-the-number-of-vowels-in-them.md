# 根据字符串中元音的数量对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-一个字符串数组-根据其中元音的数量/](https://www.geeksforgeeks.org/sort-an-array-of-strings-according-to-the-number-of-vowels-in-them/)

给定一个由 **N** 个字符串组成的数组 **arr[]** ，任务是根据这些字符串中元音的数量对它们进行排序。

**示例:**

> **输入:** arr[] = {“极客”，“for”，“coding”}
> **输出:** for，coding，极客
> for - > o = 1 元音
> coding - > o，i = 2 元音
> 极客- > e，e = 2 元音
> 
> **输入:**arr[]= {“lmno”、“pqrst”、“aeiou”、“xyz”}
> **输出:** pqrst、XYZ、lmno、aeiou

**方法:**思想是将每个带有元音数的元素存储在一个**向量对**中，然后根据存储的元音数对向量的所有元素进行排序。最后，按顺序打印字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to check the Vowel
bool isVowel(char ch)
{
    ch = toupper(ch);
    return (ch == 'A' || ch == 'E'
            || ch == 'I' || ch == 'O'
            || ch == 'U');
}

// Returns count of vowels in str
int countVowels(string str)
{
    int count = 0;
    for (int i = 0; i < str.length(); i++)
        if (isVowel(str[i])) // Check for vowel
            ++count;
    return count;
}

// Function to sort the array according to
// the number of the vowels
void sortArr(string arr[], int n)
{
    // Vector to store the number of vowels
    // with respective elements
    vector<pair<int, string> > vp;

    // Inserting number of vowels
    // with respective strings
    // in the vector pair
    for (int i = 0; i < n; i++) {

        vp.push_back(
            make_pair(
                countVowels(
                    arr[i]),
                arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the number of vowels
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " ";
}

// Driver code
int main()
{
    string arr[] = { "lmno", "pqrst",
                     "aeiou", "xyz" };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static class pair
{
    int first;
    String second;

    pair(int first,String second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to check the Vowel
static boolean isVowel(char ch)
{
    ch = Character.toUpperCase(ch);
    return (ch == 'A' || ch == 'E' ||
            ch == 'I' || ch == 'O' ||
            ch == 'U');
}

// Returns count of vowels in str
static int countVowels(String str)
{
    int count = 0;
    for(int i = 0; i < str.length(); i++)

        // Check for vowel
        if (isVowel(str.charAt(i)))
            ++count;

    return count;
}

// Function to sort the array according to
// the number of the vowels
static void sortArr(String arr[], int n)
{

    // Vector to store the number of vowels
    // with respective elements
    ArrayList<pair> vp = new ArrayList<>();

    // Inserting number of vowels
    // with respective strings
    // in the vector pair
    for(int i = 0; i < n; i++)
    {
        vp.add(new pair(countVowels(arr[i]),
                                    arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the number of vowels
    Collections.sort(vp, (a, b) -> a.first - b.first);

    // Print the sorted vector content
    for(int i = 0; i < vp.size(); i++)
        System.out.print(vp.get(i).second + " ");
}

// Driver code
public static void main(String[] args)
{
    String arr[] = { "lmno", "pqrst",
                     "aeiou", "xyz" };
    int n = arr.length;

    sortArr(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check the Vowel
def isVowel(ch) :

    ch = ch.upper();
    return (ch == 'A' or ch == 'E'or ch == 'I' or
            ch == 'O'or ch == 'U');

# Returns count of vowels in str
def countVowels(string) :

    count = 0;
    for i in range(len(string)) :

        # Check for vowel
        if (isVowel(string[i])) :
            count += 1;

    return count;

# Function to sort the array according to
# the number of the vowels
def sortArr(arr, n) :

    # Vector to store the number of vowels
    # with respective elements
    vp = [];

    # Inserting number of vowels
    # with respective strings
    # in the vector pair
    for i in range(n) :

        vp.append((countVowels(arr[i]),arr[i]));

    # Sort the vector, this will sort the pair
    # according to the number of vowels
    vp.sort()

    # Print the sorted vector content
    for i in range(len(vp)) :
        print(vp[i][1], end= " ");

# Driver code
if __name__ == "__main__" :
    arr = [ "lmno", "pqrst","aeiou", "xyz" ];
    n = len(arr);

    sortArr(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to check the Vowel
    static bool isVowel(char ch)
    {
        ch = char.ToUpper(ch);
        return (ch == 'A' || ch == 'E'
                || ch == 'I' || ch == 'O'
                || ch == 'U');
    }

    // Returns count of vowels in str
    static int countVowels(string str)
    {
        int count = 0;
        for (int i = 0; i < str.Length; i++)
            if (isVowel(str[i])) // Check for vowel
                ++count;
        return count;
    }

    // Function to sort the array according to
    // the number of the vowels
    static void sortArr(string[] arr, int n)
    {

        // Vector to store the number of vowels
        // with respective elements
        List<Tuple<int, string>> vp = new List<Tuple<int, string>>();

        // Inserting number of vowels
        // with respective strings
        // in the vector pair
        for (int i = 0; i < n; i++)
        { 
            vp.Add(new Tuple<int, string>(countVowels(arr[i]), arr[i]));
        }

        // Sort the vector, this will sort the pair
        // according to the number of vowels
        vp.Sort();

        // Print the sorted vector content
        for (int i = 0; i < vp.Count; i++)
            Console.Write(vp[i].Item2 + " ");
    }

  // Driver code
  static void Main()
  {
    string[] arr = { "lmno", "pqrst",
                     "aeiou", "xyz" };
    int n = arr.Length;
    sortArr(arr, n);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to check the Vowel
    function isVowel(ch)
    {
        ch = ch.toUpperCase();
        return (ch == 'A' || ch == 'E'
                || ch == 'I' || ch == 'O'
                || ch == 'U');
    }

    // Returns count of vowels in str
    function countVowels(str)
    {
        let count = 0;
        for (let i = 0; i < str.length; i++)
            if (isVowel(str[i])) // Check for vowel
                ++count;
        return count;
    }

    // Function to sort the array according to
    // the number of the vowels
    function sortArr(arr, n)
    {

        // Vector to store the number of vowels
        // with respective elements
        let vp = [];

        // Inserting number of vowels
        // with respective strings
        // in the vector pair
        for (let i = 0; i < n; i++)
        {
            vp.push([countVowels(arr[i]), arr[i]]);
        }

        // Sort the vector, this will sort the pair
        // according to the number of vowels
        vp.sort();

        // Print the sorted vector content
        for (let i = 0; i < vp.length; i++)
            document.write(vp[i][1] + " ");
    }

    let arr = [ "lmno", "pqrst", "aeiou", "xyz" ];
    let n = arr.length;
    sortArr(arr, n);

</script>
```

**Output:** 

```
pqrst xyz lmno aeiou
```

**时间复杂度:**T2【O(N * log N)T4】