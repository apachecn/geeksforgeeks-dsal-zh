# 检查角色的出现频率是否在重铸系列

> 原文:[https://www . geesforgeks . org/check-if-frequency-of-characters-in-recaman-series/](https://www.geeksforgeeks.org/check-if-frequency-of-characters-are-in-recaman-series/)

给定一串小写字母。任务是检查在以任何可能的方式排列后，这个字符串中字母的频率是否形成了重铸人序列(不包括第一个术语)。
按顺序打印“是”，否则输出“否”。
[雷卡曼序列](https://www.geeksforgeeks.org/recamans-sequence/)的几个起始术语是:

> 0, 1, 3, 6, 2, 7, 13, 20, 12, 21, 11, 22, 10, 23, 9, 24, 8 ….

**注:**因为是零，所以不考虑重铸人序列的第一项。
**例:**

```
Input  : str = "dddeweecceee"
Output : YES
Frequency of 'd' => 3
Frequency of 'e' => 6
Frequency of 'w' => 1
Frequency of 'c' => 2
These frequencies form the first 4 terms of 
Recaman's sequence => {1, 3, 6, 2}

Input : str = "geeksforgeeks"
Output : NO
```

**进场:**

*   遍历字符串并在地图中存储字符的频率。存储频率后，让地图的大小为 N。
*   现在，制作一个数组，并在其中插入重铸人序列的前 N 个元素。
*   现在，遍历数组并检查数组的元素是否作为键出现在地图**中(不包括对零的检查)**。
*   如果数组的每个元素都出现在地图中，则输出“是”，否则输出“否”。

以下是上述方法的实现:

## C++

```
// C++ program to check whether frequency of
// characters in a string makes
// Recaman Sequence

#include <bits/stdc++.h>
using namespace std;

// Function to fill the array with first N numbers
// from Recaman's Sequence
int recaman(int arr[], int n)
{
    // First term of the sequence is always 0
    arr[0] = 0;

    // Fill remaining terms using recursive
    // formula
    for (int i = 1; i <= n; i++) {
        int temp = arr[i - 1] - i;
        int j;

        for (j = 0; j < i; j++) {

            // If arr[i-1] - i is negative or
            // already exists.
            if ((arr[j] == temp) || temp < 0) {
                temp = arr[i - 1] + i;
                break;
            }
        }

        arr[i] = temp;
    }
}

// Function to check if the frequencies
// are in Recaman series
string isRecaman(string s)
{
    // Store frequencies of characters
    unordered_map<char, int> m;
    for (int i = 0; i < s.length(); i++)
        m[s[i]]++;   

    // Get the size of the map
    int n = m.size();

    int arr[n + 1];
    recaman(arr, n);

    int flag = 1;

    // Compare vector elements with values in Map
    for (auto itr = m.begin(); itr != m.end(); itr++) {

        int found = 0;

        for (int j = 1; j <= n; j++) {
            if (itr->second == arr[j]) {
                found = 1;
                break;
            }
        }

        if (found == 0) {
            flag = 0;
            break;
        }
    }

    if (flag == 1)
        return "YES";
    else
        return "NO";
}

// Driver code
int main()
{
    string s = "geeekkkkkkss";
    cout << isRecaman(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether frequency of
// characters in a string makes Recaman Sequence
import java.util.HashMap;
import java.util.Map;

class GfG
{

    // Function to fill the array with first
    // N numbers from Recaman's Sequence
    static void recaman(int arr[], int n)
    {
        // First term of the sequence is always 0
        arr[0] = 0;

        // Fill remaining terms using
        // recursive formula
        for (int i = 1; i <= n; i++)
        {
            int temp = arr[i - 1] - i;

            for (int j = 0; j < i; j++)
            {

                // If arr[i-1] - i is negative or
                // already exists.
                if ((arr[j] == temp) || temp < 0)
                {
                    temp = arr[i - 1] + i;
                    break;
                }
            }

            arr[i] = temp;
        }
    }

    // Function to check if the frequencies
    // are in Recaman series
    static String isRecaman(String s)
    {
        // Store frequencies of characters
        HashMap <Character, Integer> m = new HashMap<>();
        for (int i = 0; i < s.length(); i++)

            if (m.containsKey(s.charAt(i)))
                m.put(s.charAt(i), m.get(s.charAt(i))+1);
            else
                m.put(s.charAt(i), 1);

        // Get the size of the map
        int n = m.size();

        int arr[] = new int[n + 1];
        recaman(arr, n);

        int flag = 1;

        // Compare vector elements with values in Map
        for (Map.Entry mapEle : m.entrySet())
        {

            int found = 0;

            for (int j = 1; j <= n; j++)
            {
                if ((int)mapEle.getValue() == arr[j])
                {
                    found = 1;
                    break;
                }
            }

            if (found == 0)
            {
                flag = 0;
                break;
            }
        }

        if (flag == 1)
            return "YES";
        else
            return "NO";
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "geeekkkkkkss";
        System.out.println(isRecaman(s));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program to check whether
# frequency of characters in a string
# makes Recaman Sequence

# Function to fill the array with first
# N numbers from Recaman's Sequence
def recaman(arr, n) :

    # First term of the sequence
    # is always 0
    arr[0] = 0;

    # Fill remaining terms using
    # recursive formula
    for i in range(1, n + 1) :
        temp = arr[i - 1] - i;

        for j in range(i) :

            # If arr[i-1] - i is negative
            # or already exists.
            if ((arr[j] == temp) or temp < 0) :
                temp = arr[i - 1] + i;
                break;

        arr[i] = temp;

# Function to check if the frequencies
# are in Recaman series
def isRecaman(s) :

    # Store frequencies of characters
    m = dict.fromkeys(list(s), 0);

    for i in range(len(s)) :
        m[s[i]] += 1;

    # Get the size of the map
    n = len(m);

    arr = [0] * (n + 1);
    recaman(arr, n);

    flag = 1;

    # Compare vector elements with
    # values in Map
    for keys in m.keys() :

        found = 0;

        for j in range(1, n + 1) :
            if (m[keys] == arr[j]) :
                found = 1;
                break;

        if (found == 0) :
            flag = 0;
            break;

    if (flag == 1) :
        return "YES";
    else :
        return "NO";

# Driver code
if __name__ == "__main__" :

    s = "geeekkkkkkss";

    print(isRecaman(s));

# This code is contributed by Ryuga
```

## C#

```
// C# program to check whether frequency of
// characters in a string makes Recaman Sequence
using System;
using System.Collections.Generic;

class GFG
{
    // Function to fill the array with first
    // N numbers from Recaman's Sequence
    public static void recaman(int[] arr, int n)
    {
        // First term of the sequence is always 0
        arr[0] = 0;

        // Fill remaining terms using
        // recursive formula
        for (int i = 1; i <= n; i++)
        {
            int temp = arr[i - 1] - i;
            for (int j = 0; j < i; j++)
            {
                // If arr[i-1] - i is negative or
                // already exists.
                if ((arr[j] == temp) || temp < 0)
                {
                    temp = arr[i - 1] + i;
                    break;
                }
            }

            arr[i] = temp;
        }
    }

    // Function to check if the frequencies
    // are in Recaman series
    public static String isRecaman(String s)
    {
        // Store frequencies of characters
        Dictionary<char,
                   int> m = new Dictionary<char,
                                           int>();
        for (int i = 0; i < s.Length; i++)
        {
            if (m.ContainsKey(s[i]))
                m[s[i]]++;
            else
                m.Add(s[i], 1);
        }

        // Get the size of the map
        int n = m.Count;
        int[] arr = new int[n + 1];
        recaman(arr, n);
        int flag = 1;

        // Compare vector elements with values in Map
        foreach (KeyValuePair<char,
                              int> mapEle in m)
        {
            int found = 0;
            for (int j = 1; j <= n; j++)
            {
                if (mapEle.Value == arr[j])
                {
                    found = 1;
                    break;
                }
            }

            if (found == 0)
            {
                flag = 0;
                break;
            }
        }

        if (flag == 1)
            return "YES";
        else
            return "NO";
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeekkkkkkss";
        Console.WriteLine(isRecaman(s));
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

// Javascript program to check whether frequency of
// characters in a string makes
// Recaman Sequence

// Function to fill the array with first N numbers
// from Recaman's Sequence
function recaman(arr, n)
{
    // First term of the sequence is always 0
    arr[0] = 0;

    // Fill remaining terms using recursive
    // formula
    for (var i = 1; i <= n; i++) {
        var temp = arr[i - 1] - i;
        var j;

        for (j = 0; j < i; j++) {

            // If arr[i-1] - i is negative or
            // already exists.
            if ((arr[j] == temp) || temp < 0) {
                temp = arr[i - 1] + i;
                break;
            }
        }

        arr[i] = temp;
    }
}

// Function to check if the frequencies
// are in Recaman series
function isRecaman(s)
{
    // Store frequencies of characters
    var m = new Map();
    for (var i = 0; i < s.length; i++)
    {
        if(m.has(s[i]))
        {
            m.set(s[i], m.get(s[i])+1);
        }
        else
        {
            m.set(s[i], 1);
        }
    }

    // Get the size of the map
    var n = m.size;

    var arr = Array(n+1).fill(0);
    recaman(arr, n);

    var flag = 1;

    // Compare vector elements with values in Map
    m.forEach((value, key) => {
          var found = 0;

        for (var j = 1; j <= n; j++) {
            if (value == arr[j]) {
                found = 1;
                break;
            }
        }

        if (found == 0) {
            flag = 0;
        }
    });

    if (flag == 1)
        return "YES";
    else
        return "NO";
}

// Driver code
var s = "geeekkkkkkss";
document.write( isRecaman(s));

</script>
```

**Output:** 

```
YES
```