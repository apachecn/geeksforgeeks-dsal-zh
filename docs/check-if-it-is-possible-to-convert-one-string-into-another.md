# 检查在给定约束条件下是否可以将一个字符串转换成另一个字符串

> 原文:[https://www . geesforgeks . org/check-如果有可能将一个字符串转换为另一个字符串/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-convert-one-string-into-another/)

给定的两个字符串包含三个字符，即“A”、“B”和“#”。检查是否可以通过先对字符串执行以下操作将第一个字符串转换为另一个字符串。
1-‘A’只能向左移动
2-‘B’只能向右移动
3-‘A’和‘B’都不能交叉
如果可能，则打印“是”否则打印“否”。
示例:

> 输入:str1=" #A#B#B# "，str2 = " # A # # B # B "
> 输出:是
> 解释:
> str1 中的‘A’在 str2 中是在‘A’的右边，所以 str1 的‘A’可以很容易地向左移动，因为它的左边位置没有‘B ’,对于 str 1 中的第一个‘B’在 str2 中是在‘B’的左边，所以 str 2 的‘B’可以很容易地向右移动，因为它的右边位置没有‘A ’,对于
> 输入:str1=" #A#B# "，str2=" #B#A# "
> 输出:否
> 说明:
> 这里 str1 中的第一个‘A’在 str2 中向左移动到‘A’上，根据条件‘A’不能向右移动。所以 str1 不能转换成 str2。

**方法:**
1-两个字符串的长度必须相同
2-两个字符串中 A 和 B 的数量必须相等
3-两个字符串中 A 和 B 的顺序应该相同(例如:如果字符串中的“A”在“B”之前，则字符串中的“B”必须在第一个字符串中遵循相同的顺序)

## C++

```
// C++ Program for above implementation
#include <bits/stdc++.h>
using namespace std;

// Function to check is it possible to convert
// first string into another string or not.
bool isItPossible(string str1, string str2, int m, int n)
{

    // To Check Length of Both String is Equal or Not
    if (m != n)
        return false;

    // To Check  Frequency of A's and  B's are
    // equal in both strings or not.
    if (count(str1.begin(), str1.end(), 'A') !=
           count(str2.begin(), str2.end(), 'A') ||
        count(str1.begin(), str1.end(), 'B') !=
            count(str2.begin(), str2.end(), 'B'))
        return false;

    // Start traversing
    for (int i = 0; i < m; i++) {
        if (str1[i] != '#') {
            for (int j = 0; j < n; j++) {

                // To Check no two elements cross each other.
                if ((str2[j] != str1[i]) && str2[j] != '#')
                    return false;

                if (str2[j] == str1[i]) {
                    str2[j] = '#';

                    // To Check Is it Possible to Move
                    // towards Left or not.
                    if (str1[i] == 'A' && i < j)
                        return false;

                    // To Check Is it Possible to Move
                    // towards Right or not.
                    if (str1[i] == 'B' && i > j)
                        return false;

                    break;
                }
            }
        }
    }

    return true;
}

// Drivers code
int main()
{
    string str1 = "A#B#";
    string str2 = "A##B";

    int m = str1.length();
    int n = str2.length();

    isItPossible(str1, str2, m, n) ? cout << "Yes\n"
                                   : cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above implementation
class GFG
{

// Function to check is it possible to convert
// first String into another String or not.
static boolean isItPossible(char[] str1, char[] str2,
                            int m, int n)
{

    // To Check Length of Both String is Equal or Not
    if (m != n)
        return false;

    // To Check Frequency of A's and B's are
    // equal in both Strings or not.
    if (count(str1, 'A') !=
        count(str2, 'A') ||
        count(str1, 'B') !=
            count(str2, 'B'))
        return false;

    // Start traversing
    for (int i = 0; i < m; i++) {
        if (str1[i] != '#') {
            for (int j = 0; j < n; j++) {

                // To Check no two elements cross each other.
                if ((str2[j] != str1[i]) && str2[j] != '#')
                    return false;

                if (str2[j] == str1[i]) {
                    str2[j] = '#';

                    // To Check Is it Possible to Move
                    // towards Left or not.
                    if (str1[i] == 'A' && i < j)
                        return false;

                    // To Check Is it Possible to Move
                    // towards Right or not.
                    if (str1[i] == 'B' && i > j)
                        return false;

                    break;
                }
            }
        }
    }

    return true;
}

private static int count(char[] str1, char c) {
    int count = 0;
    for(char temp : str1) {
        if(c == temp)
            count++;
    }
    return count;
}

// Drivers code
public static void main(String[] args)
{
    String str1 = "A#B#";
    String str2 = "A##B";

    int m = str1.length();
    int n = str2.length();

    System.out.print(isItPossible(str1.toCharArray(), str2.toCharArray(), m, n) ?
            "Yes\n":"No\n");

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python Program for above implementation

# Function to check is it possible to convert
# first string into another string or not.
def isItPossible(str1, str2, m, n):

    # To Check Length of Both String is Equal or Not
    if (m != n):
        return False

    # To Check Frequency of A's and B's are
    # equal in both strings or not.
    if str1.count('A') != str2.count('A') \
    or str1.count('B') != str2.count('B'):
        return False

    # Start traversing
    for i in range(m):
        if (str1[i] != '#'):
            for j in range(n):
                # To Check no two elements cross each other.
                if ((str2[j] != str1[i]) and str2[j] != '#'):
                    return False

                if (str2[j] == str1[i]):
                    str2[j] = '#'

                    # To Check Is it Possible to Move
                    # towards Left or not.
                    if (str1[i] == 'A' and i < j):
                        return False

                    # To Check Is it Possible to Move
                    # towards Right or not.
                    if (str1[i] == 'B' and i > j):
                        return False

                    break

    return True

# Drivers code

str1 = "A#B#"
str2 = "A##B"

m = len(str1)
n = len(str2)

str1 = list(str1)
str2 = list(str2)

if(isItPossible(str1, str2, m, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by ankush_953
```

## C#

```
// C# Program for above implementation
using System;

class GFG
{

// Function to check is it possible to convert
// first String into another String or not.
static bool isItPossible(char[] str1, char[] str2,
                            int m, int n)
{

    // To Check Length of Both String is Equal or Not
    if (m != n)
        return false;

    // To Check Frequency of A's and B's are
    // equal in both Strings or not.
    if (count(str1, 'A') !=
        count(str2, 'A') ||
        count(str1, 'B') !=
            count(str2, 'B'))
        return false;

    // Start traversing
    for (int i = 0; i < m; i++) {
        if (str1[i] != '#') {
            for (int j = 0; j < n; j++) {

                // To Check no two elements cross each other.
                if ((str2[j] != str1[i]) && str2[j] != '#')
                    return false;

                if (str2[j] == str1[i]) {
                    str2[j] = '#';

                    // To Check Is it Possible to Move
                    // towards Left or not.
                    if (str1[i] == 'A' && i < j)
                        return false;

                    // To Check Is it Possible to Move
                    // towards Right or not.
                    if (str1[i] == 'B' && i > j)
                        return false;

                    break;
                }
            }
        }
    }

    return true;
}

private static int count(char[] str1, char c) {
    int count = 0;
    foreach(char temp in str1) {
        if(c == temp)
            count++;
    }
    return count;
}

// Drivers code
public static void Main(String[] args)
{
    String str1 = "A#B#";
    String str2 = "A##B";

    int m = str1.Length;
    int n = str2.Length;

    Console.Write(isItPossible(str1.ToCharArray(), str2.ToCharArray(), m, n) ?
            "Yes\n":"No\n");

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// js Program for above implementation
function getFreq(string,chr) {
  let ans = 0;
    for (var i=0; i<string.length;i++) {
        if( chr == string.charAt(i))
          ans++; 
    }
    return ans;
};
// Function to check is it possible to convert
// first string into another string or not.
function isItPossible(str1, str2, m, n){
    // To Check Length of Both String is Equal or Not
    if (m != n)
        return false;
    // To Check  Frequency of A's and  B's are
    // equal in both strings or not.
    if (getFreq(str1, 'A') !=
           getFreq(str2, 'A') ||
        getFreq(str1, 'B') !=
            getFreq(str2, 'B'))
        return false;

    // Start traversing
    for (let i = 0; i < m; i++) {
        if (str1[i] != '#') {
            for (let j = 0; j < n; j++) {

                // To Check no two elements cross each other.
                if ((str2[j] != str1[i]) && str2[j] != '#')
                    return false;

                if (str2[j] == str1[i]) {
                    str2 = str2.substr(0,j)+'#'+str2.substr(j+1);

                    // To Check Is it Possible to Move
                    // towards Left or not.
                    if (str1[i] == 'A' && i < j)
                        return false;

                    // To Check Is it Possible to Move
                    // towards Right or not.
                    if (str1[i] == 'B' && i > j)
                        return false;

                    break;
                }
            }
        }
    }

    return true;
}

// Drivers code
let str1 = "A#B#";
let str2 = "A##B";

let m = str1.length;
let n = str2.length;
isItPossible(str1, str2, m, n) ?document.write( "Yes<br>")
                                   : document.write( "No<br>");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n^2)