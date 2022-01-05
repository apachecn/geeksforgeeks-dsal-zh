# 按升序排列罗马数字的数组

> 原文:[https://www . geeksforgeeks . org/sort-按升序排列罗马数字数组/](https://www.geeksforgeeks.org/sort-an-array-of-roman-numerals-in-ascending-order/)

给定一个由罗马数字组成的数组**arr[]****N**[，任务是按升序排列这些罗马数字。](https://www.geeksforgeeks.org/converting-roman-numerals-decimal-lying-1-3999/)

**示例:**

> **输入:**arr[]= {“MCMIV”、“MIV”、“MCM”、“MMIV”}
> **输出:** MIV MCM MCMIV MMIV
> **解释:**
> 它们对应的十进制中的罗马数字是:
> MIV:1004
> MCM:1900
> MCMIV:1904
> MMIV:2004
> 
> **输入:**arr = {“MV”、“MIV”、“MCM”、“MM”}
> **输出:** MIV MV MCM MM
> **说明:**
> 它们对应的十进制中的罗马数字是:
> MIV 1004
> MV 1005
> MCM 1900
> MM 2000

**方法:**解决这个问题的思路是将每个元素及其[罗马到整数](https://www.geeksforgeeks.org/converting-roman-numerals-decimal-lying-1-3999/)值存储在一个[向量对中，然后根据存储的罗马到整数值对向量的所有元素进行排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。

*   迭代给定的罗马数字。
*   [将罗马数字转换为十进制](https://www.geeksforgeeks.org/converting-roman-numerals-decimal-lying-1-3999/)并将它们作为一对存储在向量中。
*   根据存储在向量中的十进制数对向量进行排序。
*   最后，按排序顺序打印罗马数字。

下面是上述方法的实现:

## C++

```
// C++ program to sort an array of
// Roman Numerals in ascending order

#include <bits/stdc++.h>
using namespace std;

// Function to return the value
// of a Roman symbol
int value(char r)
{
    // I in roman is equal to
    // 1 in decimal
    if (r == 'I')
        return 1;

    // V in roman is equal to
    // 5 in decimal
    if (r == 'V')
        return 5;

    // X in roman is equal to
    // 10 in decimal
    if (r == 'X')
        return 10;

    // L in roman is equal to
    // 50 in decimal
    if (r == 'L')
        return 50;

    // C in roman is equal to
    // 100 in decimal
    if (r == 'C')
        return 100;

    // D in roman is equal to
    // 500 in decimal
    if (r == 'D')
        return 500;

    // M in roman is equal to
    // 1000 in decimal
    if (r == 'M')
        return 1000;

    return -1;
}

// Function to return the decimal value
// of a roman numaral
int romanToDecimal(string& str)
{
    // Initialize result
    int res = 0;

    // Traverse given input
    for (int i = 0; i < str.length(); i++) {

        // Getting value of symbol s[i]
        int s1 = value(str[i]);

        if (i + 1 < str.length()) {

            // Getting value of symbol s[i+1]
            int s2 = value(str[i + 1]);

            // Comparing both values
            if (s1 >= s2) {

                // Value of current symbol
                // is >= the next symbol
                res = res + s1;
            }
            else {

                // Value of current symbol
                // is < the next symbol
                res = res + s2 - s1;
                i++;
            }
        }
        else {
            res = res + s1;
        }
    }
    return res;
}

// Function to sort the array according to
// the increasing order
void sortArr(string arr[], int n)
{
    // Vector to store the roman to integer
    // with respective elements
    vector<pair<int, string> > vp;

    // Inserting roman to integer
    // with respective elements in vector pair
    for (int i = 0; i < n; i++) {
        vp.push_back(make_pair(
            romanToDecimal(
                arr[i]),
            arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the increasing order.
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " "
             << vp[i].first << "\n";
}

// Driver code
int main()
{
    string arr[] = { "MCMIV", "MIV",
                     "MCM", "MMIV" };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array of
// Roman Numerals in ascending order
import java.io.*;
import java.util.*;

// User defined Pair class
class Pair
{
    int x;
    String y;

    public Pair(int a, String b)
    {
        this.x = a;
        this.y = b;
    }
}

// Class to define user defined conparator
class Compare
{
    static void compare(ArrayList<Pair> vp)
    {

        // Comparator to sort the pair according
        // to first element
        Collections.sort(vp, new Comparator<Pair>()
        {
            @Override public int compare(Pair p1, Pair p2)
            {
                return p1.x - p2.x;
            }
        });
    }
}

class GFG{

// Function to return the value
// of a Roman symbol
static int value(char r)
{

    // I in roman is equal to
    // 1 in decimal
    if (r == 'I')
        return 1;

    // V in roman is equal to
    // 5 in decimal
    if (r == 'V')
        return 5;

    // X in roman is equal to
    // 10 in decimal
    if (r == 'X')
        return 10;

    // L in roman is equal to
    // 50 in decimal
    if (r == 'L')
        return 50;

    // C in roman is equal to
    // 100 in decimal
    if (r == 'C')
        return 100;

    // D in roman is equal to
    // 500 in decimal
    if (r == 'D')
        return 500;

    // M in roman is equal to
    // 1000 in decimal
    if (r == 'M')
        return 1000;

    return -1;
}

// Function to return the decimal value
// of a roman numaral
static int romanToDecimal(String str)
{

    // Initialize result
    int res = 0;

    // Traverse given input
    for(int i = 0; i < str.length(); i++)
    {

        // Getting value of symbol s[i]
        int s1 = value(str.charAt(i));

        if (i + 1 < str.length())
        {

            // Getting value of symbol s[i+1]
            int s2 = value(str.charAt(i + 1));

            // Comparing both values
            if (s1 >= s2)
            {

                // Value of current symbol
                // is >= the next symbol
                res = res + s1;
            }
            else
            {

                // Value of current symbol
                // is < the next symbol
                res = res + s2 - s1;
                i++;
            }
        }
        else
        {
            res = res + s1;
        }
    }
    return res;
}

// Function to sort the array according to
// the increasing order
static void sortArr(String[] arr, int n)
{

    // Vector to store the roman to integer
    // with respective elements
    ArrayList<Pair> vp = new ArrayList<Pair>();

    // Inserting roman to integer
    // with respective elements in vector pair
    for(int i = 0; i < n; i++)
    {
        vp.add(new Pair(romanToDecimal(arr[i]),
                                       arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the increasing order.
    Compare obj = new Compare();
    obj.compare(vp);

    // Print the sorted vector content
    for(int i = 0; i < vp.size(); i++)
        System.out.println(vp.get(i).y + " " +
                           vp.get(i).x + "\n");
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "MCMIV", "MIV", "MCM", "MMIV" };
    int n = arr.length;

    sortArr(arr, n);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to sort an array of
# Roman Numerals in ascending order

# Function to return the value
# of a Roman symbol
def value(r):

    # I in roman is equal to
    # 1 in decimal
    if (r == 'I'):
        return 1

    # V in roman is equal to
    # 5 in decimal
    if (r == 'V'):
        return 5

    # X in roman is equal to
    # 10 in decimal
    if (r == 'X'):
        return 10

    # L in roman is equal to
    # 50 in decimal
    if (r == 'L'):
        return 50

    # C in roman is equal to
    # 100 in decimal
    if (r == 'C'):
        return 100

    # D in roman is equal to
    # 500 in decimal
    if (r == 'D'):
        return 500

    # M in roman is equal to
    # 1000 in decimal
    if (r == 'M'):
        return 1000

    return -1

# Function to return the decimal value
# of a roman numaral
def romanToDecimal(st):

    # Initialize result
    res = 0

    # Traverse given input
    i = 0
    while i < len(st):

        # Getting value of symbol s[i]
        s1 = value(st[i])

        if (i + 1 < len(st)):

            # Getting value of symbol s[i+1]
            s2 = value(st[i + 1])

            # Comparing both values
            if (s1 >= s2):

                # Value of current symbol
                # is >= the next symbol
                res = res + s1

            else :

                # Value of current symbol
                # is < the next symbol
                res = res + s2 - s1
                i += 1

        else :
            res = res + s1

        i += 1

    return res

# Function to sort the array according to
# the increasing order
def sortArr(arr, n):

    # Vector to store the roman to integer
    # with respective elements
    vp = {}

    # Inserting roman to integer
    # with respective elements in vector pair
    for i in range(n):
        p = romanToDecimal(arr[i])
        vp[p] = arr[i]

    # Sort the vector, this will sort the pair
    # according to the increasing order.
    for i in sorted(vp):
        print(vp[i], i)

# Driver code
if __name__ == "__main__":

    arr = [ "MCMIV", "MIV",
            "MCM", "MMIV" ]
    n = len(arr)

    sortArr(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program to sort an array of
// Roman Numerals in ascending order
using System;
using System.Collections;
using System.Collections.Generic;

class ABC : IComparer<Pair>
{
    public int Compare(Pair p1, Pair p2)
    {
        if (p1.x == 0 || p2.x == 0)
        {
            return 0;
        }

        // CompareTo() method
        return p1.x.CompareTo(p2.x);
    }
}

// User defined Pair class
public class Pair
{
    public int x;
    public string y;

    public Pair(int a, string b)
    {
        this.x = a;
        this.y = b;
    }
}

class GFG{

// Function to return the value
// of a Roman symbol
static int value(char r)
{

    // I in roman is equal to
    // 1 in decimal
    if (r == 'I')
        return 1;

    // V in roman is equal to
    // 5 in decimal
    if (r == 'V')
        return 5;

    // X in roman is equal to
    // 10 in decimal
    if (r == 'X')
        return 10;

    // L in roman is equal to
    // 50 in decimal
    if (r == 'L')
        return 50;

    // C in roman is equal to
    // 100 in decimal
    if (r == 'C')
        return 100;

    // D in roman is equal to
    // 500 in decimal
    if (r == 'D')
        return 500;

    // M in roman is equal to
    // 1000 in decimal
    if (r == 'M')
        return 1000;

    return -1;
}

// Function to return the decimal value
// of a roman numaral
static int romanToDecimal(string str)
{

    // Initialize result
    int res = 0;

    // Traverse given input
    for(int i = 0; i < str.Length; i++)
    {

        // Getting value of symbol s[i]
        int s1 = value(str[i]);

        if (i + 1 < str.Length)
        {

            // Getting value of symbol s[i+1]
            int s2 = value(str[i + 1]);

            // Comparing both values
            if (s1 >= s2)
            {

                // Value of current symbol
                // is >= the next symbol
                res = res + s1;
            }
            else
            {

                // Value of current symbol
                // is < the next symbol
                res = res + s2 - s1;
                i++;
            }
        }
        else
        {
            res = res + s1;
        }
    }
    return res;
}

// Function to sort the array according to
// the increasing order
static void sortArr(String[] arr, int n)
{

    // Vector to store the roman to integer
    // with respective elements
    List<Pair> vp = new List<Pair>();

    // Inserting roman to integer
    // with respective elements in vector pair
    for(int i = 0; i < n; i++)
    {
        vp.Add(new Pair(romanToDecimal(arr[i]),
                                       arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the increasing order.
    ABC gg = new ABC();
    vp.Sort(gg);

    // Print the sorted vector content
    for(int i = 0; i < vp.Count; i++)
        Console.WriteLine(vp[i].y + " " +
                          vp[i].x + "\n");
}

// Driver Code
static public void Main ()
{
     string[] arr = { "MCMIV", "MIV", "MCM", "MMIV" };
    int n = arr.Length;

    sortArr(arr, n);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

// Function to return the value
// of a Roman symbol
function value(r)
{
    // I in roman is equal to
    // 1 in decimal
    if (r == 'I')
        return 1;

    // V in roman is equal to
    // 5 in decimal
    if (r == 'V')
        return 5;

    // X in roman is equal to
    // 10 in decimal
    if (r == 'X')
        return 10;

    // L in roman is equal to
    // 50 in decimal
    if (r == 'L')
        return 50;

    // C in roman is equal to
    // 100 in decimal
    if (r == 'C')
        return 100;

    // D in roman is equal to
    // 500 in decimal
    if (r == 'D')
        return 500;

    // M in roman is equal to
    // 1000 in decimal
    if (r == 'M')
        return 1000;

    return -1;
}

// Function to return the decimal value
// of a roman numaral
function romanToDecimal(str)
{
    // Initialize result
    var res = 0;

    // Traverse given input
    for (var i = 0; i < str.length; i++) {

        // Getting value of symbol s[i]
        var s1 = value(str[i]);

        if (i + 1 < str.length) {

            // Getting value of symbol s[i+1]
            var s2 = value(str[i + 1]);

            // Comparing both values
            if (s1 >= s2) {

                // Value of current symbol
                // is >= the next symbol
                res = res + s1;
            }
            else {

                // Value of current symbol
                // is < the next symbol
                res = res + s2 - s1;
                i++;
            }
        }
        else {
            res = res + s1;
        }
    }
    return res;
}

// Function to sort the array according to
// the increasing order
function sortArr(arr, n)
{
    // Vector to store the roman to integer
    // with respective elements
    var vp = new Array(n);
    // Inserting roman to integer
    // with respective elements in vector pair
    for (var i = 0; i < n; i++) {
        vp[i] = [romanToDecimal(arr[i]),arr[i]];
    }

    // Sort the vector, this will sort the pair
    // according to the increasing order.
    vp.sort();

    // Print the sorted vector content
    for (var i = 0; i < n; i++)
        document.write(vp[i][1]+" "+vp[i][0]+"<br>");
}

// Driver Code
var arr = ["MCMIV", "MIV",
           "MCM", "MMIV"];
var n = arr.length;
sortArr(arr, n);

</script>
```

**Output:** 

```
MIV 1004
MCM 1900
MCMIV 1904
MMIV 2004
```

**时间复杂度:** *O(N * log(N))* ，其中 N 为数组中的元素个数。

**辅助空间:**T2【O(N)T4】