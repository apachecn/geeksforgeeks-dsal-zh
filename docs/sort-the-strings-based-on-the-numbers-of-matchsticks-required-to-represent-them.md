# 根据代表字符串所需的火柴杆数量对字符串进行排序

> 原文:[https://www . geeksforgeeks . org/基于火柴杆数量的字符串排序-需要代表它们/](https://www.geeksforgeeks.org/sort-the-strings-based-on-the-numbers-of-matchsticks-required-to-represent-them/)

给定一个由 **N** 个字符串组成的数组 **arr[]** ，任务是根据表示这些字符串所需的木棒数量对它们进行排序。

**示例:**

> **输入:**arr[]= {“123”、“ABC”、“88”}
> **输出:** 123 88 ABC
> **说明:**
> 每串所需木棒如下:
> 123 - > 12 木棒
> 88 - > 14 木棒
> ABC - > 17 木棒
> 
> **输入:**arr[]= {“GEEKS”“FOR”“GEEKS forgeeks”}
> **输出:**FOR GEEKS GEEKS forgeeks
> **说明:**
> 每根弦需要的木棒如下:
> FOR = > 16 根木棒
> GEEKS = > 25 根木棒
> GEEKSFORGEEKS = > 66 根木棒

**方法:**思路是借助每个字符所需的棒数，计算出每个字符串所需的棒数。然后，将木棒和细绳的数量存储成一对数组。最后，[根据需要的木棒数量对](https://www.geeksforgeeks.org/merge-sort/)进行排序。
下图显示了代表每个角色所需的木棒数量:

![](img/b70af5019d891a46d3a2d2e6f85fe961.png)

下面是上述方法的实现:

## C++

```
// C++ implementation to sort the
// strings with the number of
// sticks required to represent them

#include <bits/stdc++.h>

using namespace std;

// Stick[] stores the count
// of sticks required to
// represent the alphabets
int sticks[] = { 6, 7, 4, 6, 5, 4, 6,
                 5, 2, 4, 4, 3, 6, 6,
                 6, 5, 7, 6, 5, 3, 5,
                 4, 6, 4, 3, 4 };

// Number[] stores the count
// of sticks required to
// represent the numerals
int number[] = { 6, 2, 5, 5, 4, 5, 6,
                 3, 7, 6 };

// Function that return the count of
// sticks required to represent
// the given string str
int countSticks(string str)
{
    int cnt = 0;

    // Loop to iterate over every
    // character of the string
    for (int i = 0; str[i]; i++) {

        char ch = str[i];

        // Add the count of sticks
        // required to represent the
        // current character
        if (ch >= 'A' && ch <= 'Z') {
            cnt += sticks[ch - 'A'];
        }
        else {
            cnt += number[ch - '0'];
        }
    }
    return cnt;
}
// Function to sort the array
// according to the number of
// sticks required to represent it
void sortArr(string arr[], int n)
{
    // Vector to store the number
    // of sticks required with
    // respective strings
    vector<pair<int, string> > vp;

    // Inserting number of sticks
    // with respective strings
    for (int i = 0; i < n; i++) {
        vp.push_back(
            make_pair(countSticks(arr[i]),
                      arr[i]));
    }

    // Sort the vector,
    sort(vp.begin(), vp.end());

    // Print the sorted vector
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " ";
}

// Driver Code
int main()
{
    string arr[] = { "GEEKS", "FOR",
                     "GEEKSFORGEEKS" };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the
// strings with the number of
// sticks required to represent them

import java.io.*;
import java.util.*;

class GFG{
    // Stick[] stores the count
    // of sticks required to
    // represent the alphabets
    static int sticks[] = { 6, 7, 4, 6, 5, 4, 6,
                    5, 2, 4, 4, 3, 6, 6,
                    6, 5, 7, 6, 5, 3, 5,
                    4, 6, 4, 3, 4 };

    // Number[] stores the count
    // of sticks required to
    // represent the numerals
    static int number[] = { 6, 2, 5, 5, 4, 5, 6,
                    3, 7, 6 };

    // Function that return the count of
    // sticks required to represent
    // the given string str

    static class Pair implements Comparable<Pair>{
        int num_sticks;
        String str;

        Pair(int n, String s)
        {
            num_sticks = n;
            str=s;
        }

        public int compareTo(Pair p)
        {
            return this.num_sticks-p.num_sticks;
        }
    }
    static int countSticks(String str)
    {
        int cnt = 0;
        int n=str.length();

        // Loop to iterate over every
        // character of the string
        for (int i = 0; i < n; i++) {

            char ch = str.charAt(i);

            // Add the count of sticks
            // required to represent the
            // current character
            if (ch >= 'A' && ch <= 'Z') {
                cnt += sticks[ch - 'A'];
            }
            else {
                cnt += number[ch - '0'];
            }
        }
        return cnt;
    }

    // Function to sort the array
    // according to the number of
    // sticks required to represent it
    static void sortArr(String arr[], int n) 
    {
        // ArrayList to store the number
        // of sticks required with
        // respective strings
        ArrayList<Pair> list = new ArrayList<>();

        // Inserting number of sticks
        // with respective strings
        for (int i = 0; i < n; i++) {
            list.add(
                new Pair(countSticks(arr[i]),
                        arr[i]));
        }

        // Sort the list,
        Collections.sort(list);

        // Print the sorted vector
        for (int i = 0; i < list.size(); i++)
            System.out.print(list.get(i).str + " ");
    }

    // Driver Code
    public static void main(String []args)
    {
        String arr[] = { "GEEKS", "FOR",
                        "GEEKSFORGEEKS" };
        int n = arr.length;

        sortArr(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to sort the
# strings with the number of
# sticks required to represent them

# Stick[] stores the count
# of sticks required to
# represent the alphabets
sticks = [6, 7, 4, 6, 5, 4, 6,
          5, 2, 4, 4, 3, 6, 6,
          6, 5, 7, 6, 5, 3, 5,
          4, 6, 4, 3, 4]

# Number[] stores the count
# of sticks required to
# represent the numerals
number = [6, 2, 5, 5, 4,
          5, 6, 3, 7, 6]

# Function that return the count of
# sticks required to represent
# the given string str
def countSticks(st):

    cnt = 0

    # Loop to iterate over every
    # character of the string
    for i in range(len(st)):

        ch = st[i]

        # Add the count of sticks
        # required to represent the
        # current character
        if (ch >= 'A' and ch <= 'Z'):
            cnt += sticks[ord(ch) -
                          ord('A')]       
        else :
            cnt += number[ord(ch ) -
                          ord('0')]

    return cnt

# Function to sort the array
# according to the number of
# sticks required to represent it
def sortArr(arr, n):

    # Vector to store the number
    # of sticks required with
    # respective strings
    vp = []

    # Inserting number of sticks
    # with respective strings
    for i in range(n):
        vp.append([countSticks(arr[i]),
                               arr[i]])

    # Sort the vector
    vp.sort()

    # Print the sorted vector
    for i in range(len(vp)):
        print (vp[i][1], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = ["GEEKS", "FOR",
           "GEEKSFORGEEKS"]
    n = len(arr)
    sortArr(arr, n)

 # This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript program

// Stick[] stores the count
// of sticks required to
// represent the alphabets
var sticks = [ 6, 7, 4, 6, 5, 4, 6,
                 5, 2, 4, 4, 3, 6, 6,
                 6, 5, 7, 6, 5, 3, 5,
                 4, 6, 4, 3, 4 ];

// Number[] stores the count
// of sticks required to
// represent the numerals
var number = [ 6, 2, 5, 5, 4, 5, 6,
                 3, 7, 6 ];

// Function that return the count of
// sticks required to represent
// the given string str
function countSticks(str)
{
    var cnt = 0;
    var n=str.length;

    // Loop to iterate over every
    // character of the string
    for (var i = 0; i < n; i++) {

        var ch = str[i];

        // Add the count of sticks
        // required to represent the
        // current character
        if (ch >= 'A' && ch <= 'Z') {
            cnt += sticks[ch.charCodeAt(0) - 'A'.charCodeAt(0)];
        }
        else {
            cnt += number[ch.charCodeAt(0) - '0'.charCodeAt(0)];
        }
    }
    return cnt;
}
// Function to sort the array
// according to the number of
// sticks required to represent it
function sortArr(arr, int)
{
    // Vector to store the number
    // of sticks required with
    // respective strings
    var vp = new Array(n);

    // Inserting number of sticks
    // with respective strings
    for (var i = 0; i < n; i++) {
        vp[i] = [countSticks(arr[i]), arr[i]];
    }

    // Sort the vector,
    vp.sort();

    // Print the sorted vector
    for (var i = 0; i < n; i++)
        document.write(vp[i][1] + " ");
}
var arr = [  "GEEKS", "FOR", "GEEKSFORGEEKS"];
var n = arr.length;

sortArr(arr, n);
</script>
```

**Output:** 

```
FOR GEEKS GEEKSFORGEEKS
```

***时间复杂度:** O(N * log N)*

***辅助空间:** O(N)*