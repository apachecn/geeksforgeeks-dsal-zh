# 将字符串分成两部分，使两部分至少有 k 个不同的字符

> 原文:[https://www . geesforgeks . org/partition-the-string-in-two-part-so-这两个部分都至少有-k 个不同的字符/](https://www.geeksforgeeks.org/partition-the-string-in-two-parts-such-that-both-parts-have-at-least-k-different-characters/)

给定一串小写英文字母和一个整数 0 < K <= 26\. The task is to divide the string into two parts (also print them) such that both parts have at least k different characters. If there are more than one answers possible, print one having the smallest left part. If there is no such answers, print “Not Possible”.
**示例:**

> **输入:** str = "geeksforgeeks "，k = 4
> **输出:** geeks，forgeeks
> 字符串可以分为“geeks”和“forgeeks”两部分。由于“极客”有四个不同的字符‘g’、‘e’、‘k’和‘s’，并且这是最小的左边部分，“伪造者”也至少有四个不同的字符。
> **输入:**str = " aaababb "，k = 2
> **输出:**不可能

**进场:**

*   想法是使用 Hashmap 计算不同字符的数量。
*   如果 distinct 变量的计数等于 **k** ，则找到字符串的左边部分，因此存储该索引，中断循环并取消标记所有字符。
*   现在运行一个从左字符串结束到给定字符串结束的循环，重复与查找左字符串相同的过程。
*   如果计数大于或等于 **k** ，则可以找到正确的字符串，否则打印“不可能”。
*   如果可能，则打印左字符串和右字符串。

以下是上述方法的实施

## C++

```
// C++ implementation of the above approach
#include <iostream>
#include <map>
using namespace std;

// Function to find the partition of the
// string such that both parts have at
// least k different characters
void division_of_string(string str, int k)
{
    // Length of the string
    int n = str.size();

    // To check if the current
    // character is already found
    map<char, bool> has;

    int ans, cnt = 0, i = 0;

    // Count number of different
    // characters in the left part
    while (i < n) {

        // If current character is not
        // already found, increase cnt by 1
        if (!has[str[i]]) {
            cnt++;
            has[str[i]] = true;
        }

        // If count becomes equal to k, we've
        // got the first part, therefore,
        // store current index and break the loop
        if (cnt == k) {
            ans = i;
            break;
        }

        i++;
    }
    //Increment i by 1
    i++;

    // Clear the map
    has.clear();

    // Assign cnt as 0
    cnt = 0;

    while (i < n) {

        // If the current character is not
        // already found, increase cnt by 1
        if (!has[str[i]]) {
            cnt++;
            has[str[i]] = true;
        }

        // If cnt becomes equal to k, the
        // second part also have k different
        // characters so break it
        if (cnt == k) {
            break;
        }

        i++;
    }

    // If the second part has less than
    // k different characters, then
    // print "Not Possible"
    if (cnt < k) {
        cout << "Not possible" << endl;
    }

    // Otherwise print both parts
    else {
        i = 0;
        while (i <= ans) {
            cout << str[i];
            i++;
        }
        cout << endl;

        while (i < n) {
            cout << str[i];
            i++;
        }
        cout << endl;
    }

    cout << endl;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int k = 4;

    // Function call
    division_of_string(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the partition of the
// string such that both parts have at
// least k different characters
static void division_of_string(char[] str, int k)
{
    // Length of the string
    int n = str.length;

    // To check if the current
    // character is already found
    Map<Character, Boolean> has = new HashMap<>();

    int ans = 0, cnt = 0, i = 0;

    // Count number of different
    // characters in the left part
    while (i < n)
    {

        // If current character is not
        // already found, increase cnt by 1
        if (!has.containsKey(str[i]))
        {
            cnt++;
            has.put(str[i], true);
        }

        // If count becomes equal to k, we've
        // got the first part, therefore,
        // store current index and break the loop
        if (cnt == k)
        {
            ans = i;
            break;
        }

        i++;
    }
    //Increment i by 1
    i++;

    // Clear the map
    has.clear();

    // Assign cnt as 0
    cnt = 0;

    while (i < n)
    {

        // If the current character is not
        // already found, increase cnt by 1
        if (!has.containsKey(str[i]))
        {
            cnt++;
            has.put(str[i], true);
        }

        // If cnt becomes equal to k, the
        // second part also have k different
        // characters so break it
        if (cnt == k)
        {
            break;
        }

        i++;
    }

    // If the second part has less than
    // k different characters, then
    // print "Not Possible"
    if (cnt < k)
    {
        System.out.println("Not possible");
    }

    // Otherwise print both parts
    else
    {
        i = 0;
        while (i <= ans)
        {
            System.out.print(str[i]);
            i++;
        }
        System.out.println("");

        while (i < n)
        {
            System.out.print(str[i]);
            i++;
        }
        System.out.println("");
    }

    System.out.println("");
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int k = 4;

    // Function call
    division_of_string(str.toCharArray(), k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the partition of the
# string such that both parts have at
# least k different characters
def division_of_string(string, k) :

    # Length of the string
    n = len(string);

    # To check if the current
    # character is already found
    has = {};

    cnt = 0; i = 0;

    # Count number of different
    # characters in the left part
    while (i < n) :

        # If current character is not
        # already found, increase cnt by 1
        if string[i] not in has :
            cnt += 1;
            has[string[i]] = True;

        # If count becomes equal to k, we've
        # got the first part, therefore,
        # store current index and break the loop
        if (cnt == k) :
            ans = i;
            break;

        i += 1;

    # Increment i by 1
    i += 1;

    # Clear the map
    has.clear();

    # Assign cnt as 0
    cnt = 0;

    while (i < n) :

        # If the current character is not
        # already found, increase cnt by 1
        if (string[i] not in has) :
            cnt += 1;
            has[string[i]] = True;

        # If cnt becomes equal to k, the
        # second part also have k different
        # characters so break it
        if (cnt == k) :
            break;

        i += 1;

    # If the second part has less than
    # k different characters, then
    # print "Not Possible"
    if (cnt < k) :
        print("Not possible",end = "");

    # Otherwise print both parts
    else :
        i = 0;
        while (i <= ans) :
            print(string[i],end= "");
            i += 1;

        print();

        while (i < n) :
            print(string[i],end="");
            i += 1;

        print()

# Driver code
if __name__ == "__main__":

    string = "geeksforgeeks";
    k = 4;

    # Function call
    division_of_string(string, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the partition of the
// string such that both parts have at
// least k different characters
static void division_of_string(char[] str, int k)
{
    // Length of the string
    int n = str.Length;

    // To check if the current
    // character is already found
    Dictionary<char,bool> has = new Dictionary<char,bool> ();

    int ans = 0, cnt = 0, i = 0;

    // Count number of different
    // characters in the left part
    while (i < n)
    {

        // If current character is not
        // already found, increase cnt by 1
        if (!has.ContainsKey(str[i]))
        {
            cnt++;
            has.Add(str[i], true);
        }

        // If count becomes equal to k, we've
        // got the first part, therefore,
        // store current index and break the loop
        if (cnt == k)
        {
            ans = i;
            break;
        }

        i++;
    }
    // Increment i by 1
    i++;

    // Clear the map
    has.Clear();

    // Assign cnt as 0
    cnt = 0;

    while (i < n)
    {

        // If the current character is not
        // already found, increase cnt by 1
        if (!has.ContainsKey(str[i]))
        {
            cnt++;
            has.Add(str[i], true);
        }

        // If cnt becomes equal to k, the
        // second part also have k different
        // characters so break it
        if (cnt == k)
        {
            break;
        }

        i++;
    }

    // If the second part has less than
    // k different characters, then
    // print "Not Possible"
    if (cnt < k)
    {
        Console.WriteLine("Not possible");
    }

    // Otherwise print both parts
    else
    {
        i = 0;
        while (i <= ans)
        {
            Console.Write(str[i]);
            i++;
        }
        Console.WriteLine("");

        while (i < n)
        {
            Console.Write(str[i]);
            i++;
        }
        Console.WriteLine("");
    }

    Console.WriteLine("");
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int k = 4;

    // Function call
    division_of_string(str.ToCharArray(), k);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

// Function to find the partition of the
// string such that both parts have at
// least k different characters
function division_of_string(str, k)
{
    // Length of the string
    let n = str.length;

    // To check if the current
    // character is already found
    let has = new Map();

    let ans = 0, cnt = 0, i = 0;

    // Count number of different
    // characters in the left part
    while (i < n)
    {

        // If current character is not
        // already found, increase cnt by 1
        if (!has.has(str[i]))
        {
            cnt++;
            has.set(str[i], true);
        }

        // If count becomes equal to k, we've
        // got the first part, therefore,
        // store current index and break the loop
        if (cnt == k)
        {
            ans = i;
            break;
        }

        i++;
    }

    //Increment i by 1
    i++;

    // Clear the map
    has.clear();

    // Assign cnt as 0
    cnt = 0;

    while (i < n)
    {

        // If the current character is not
        // already found, increase cnt by 1
        if (!has.has(str[i]))
        {
            cnt++;
            has.set(str[i], true);
        }

        // If cnt becomes equal to k, the
        // second part also have k different
        // characters so break it
        if (cnt == k)
        {
            break;
        }

        i++;
    }

    // If the second part has less than
    // k different characters, then
    // print "Not Possible"
    if (cnt < k)
    {
        document.write("Not possible"  + "<br/>");
    }

    // Otherwise print both parts
    else
    {
        i = 0;
        while (i <= ans)
        {
            document.write(str[i]);
            i++;
        }
        document.write("" + "<br/>");

        while (i < n)
        {
            document.write(str[i]);
            i++;
        }
        document.write("" + "<br/>");
    }

    document.write("" + "<br/>");
}

    // Driver code

    let str = "geeksforgeeks";
    let k = 4;

    // Function call
    division_of_string(str.split(''), k);

  // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
geeks
forgeeks
```

**时间复杂度:** O(N)，其中 N 是给定字符串的长度。