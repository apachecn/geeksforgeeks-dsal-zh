# 通过更新从字符串中查找范围[L，R]中第 k 个最大字符的查询

> 原文:[https://www . geeksforgeeks . org/query-to-find-kth-range-l-r-from-string-with-updates/](https://www.geeksforgeeks.org/queries-to-find-kth-greatest-character-in-a-range-l-r-from-a-string-with-updates/)

给定长度为 **N、**和 **Q 的字符串**字符串**，查询以下两种类型:**

1.  **(1 L R K):** 从索引范围**【L，R】***(基于 1 的索引)*中找到 **K <sup>第</sup>** 最伟大的角色(*非独特的*
2.  **(2 J C):** 用字符 **C.** 替换字符串中的 **J <sup>th</sup>** 字符

**示例:**

> **输入:**str = " abcdef "，Q = 3，Query[][]= { {1，2，5，3}，{2，4，g}，{ 1，1，4，3}}
> **输出:**
> c
> b
> **说明:**
> 查询 1:索引(2，5)之间的字符串为“bcdd”。第三大字符是“c”。因此，c 是所需的输出。
> 查询 2:将 S[4]替换为“g”。因此，S 修饰为“abcgdef”。
> 查询 3:索引(1，4)之间的字符串为“abcg”。第三大字符是“b”。因此，b 是所需的输出。
> 
> **输入:** str=" afcdehgk "，Q = 4，查询[][] = {{1，2，5，4}，{2，5，m}，{1，3，7，2}，{1，1，6，4}}
> **输出:**
> c
> h
> d

**天真方法:**解决问题最简单的方法如下:

*   对于每一个类型为( **1 L R K** 的查询，从索引**【L，R】**的范围中找到 S 的[子串](https://www.geeksforgeeks.org/length-of-the-longest-valid-substring/)，并[按照**非递增顺序**对该子串](https://www.geeksforgeeks.org/substring-sort/)进行排序。打印子字符串中第 K<sup>索引处的字符。</sup>
*   对于类型为 **( 2 J C )** 的每个查询，将 **S** 中的**J<sup>th</sup>T5】字符替换为 **C** 。**

***时间复杂度:** O ( Q * ( N log(N))，其中 N logN 是排序每个*子串*的计算复杂度。*
***辅助空间:** O(N)*

下面的代码是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to find the kth greatest
// character from the strijng
char find_kth_largest(string str, int k)
{

    // Sorting the string in
    // non-increasing Order
    sort(str.begin(), str.end(),
         greater<char>());
    return str[k - 1];
}

// Function to print the K-th character
// from the substring S[l] .. S[r]
char printCharacter(string str, int l,
                    int r, int k)
{
    // 0-based indexing
    l = l - 1;
    r = r - 1;

    // Substring of str from the
    // indices l to r.
    string temp
        = str.substr(l, r - l + 1);

    // Extract kth Largest character
    char ans
        = find_kth_largest(temp, k);

    return ans;
}

// Function to replace character at
// pos of str by the character s
void updateString(string str, int pos,
                  char s)
{
    // Index of S to be updated.
    int index = pos - 1;
    char c = s;

    // Character to be replaced
    // at index in S
    str[index] = c;
}

// Driver Code
int main()
{
    // Given string
    string str = "abcddef";

    // Count of queries
    int Q = 3;

    // Queries
    cout << printCharacter(str, 1, 2, 2)
         << endl;
    updateString(str, 4, 'g');
    cout << printCharacter(str, 1, 5, 4)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
//include "bits/stdJava.h"
import java.util.*;
class GFG{

// Function to find the kth greatest
// character from the strijng
static char find_kth_largest(char []str,
                             int k)
{
  // Sorting the String in
  // non-increasing Order
  Arrays.sort(str);
  reverse(str);
  return str[k - 1];
}
  static char[] reverse(char a[])
  {
    int i, n = a.length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
      t = a[i];
      a[i] = a[n - i - 1];
      a[n - i - 1] = t;
    }
    return a;
}

// Function to print the K-th character
// from the subString S[l] .. S[r]
static char printCharacter(String str, int l,
                           int r, int k)
{
  // 0-based indexing
  l = l - 1;
  r = r - 1;

  // SubString of str from the
  // indices l to r.
  String temp = str.substring(l, r - l + 1);

  // Extract kth Largest character
  char ans =
    find_kth_largest(temp.toCharArray(), k);

  return ans;
}

// Function to replace character at
// pos of str by the character s
static void updateString(char []str,
                         int pos, char s)
{
  // Index of S to be updated.
  int index = pos - 1;
  char c = s;

  // Character to be replaced
  // at index in S
  str[index] = c;
}

// Driver Code
public static void main(String[] args)
{
  // Given String
  String str = "abcddef";

  // Count of queries
  int Q = 3;

  // Queries
  System.out.print(printCharacter(str, 1,
                                  2, 2) + "\n");
  updateString(str.toCharArray(), 4, 'g');
  System.out.print(printCharacter(str, 1,
                                  5, 4) + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
# Function to find the kth greatest
# character from the string
def find_kth_largest(strr, k):

    # Sorting the in
    # non-increasing Order
    strr = sorted(strr)
    strr = strr[:: -1]
    return strr[k - 1]

# Function to print the K-th character
# from the subS[l] .. S[r]
def printCharacter(strr, l, r, k):

    #0-based indexing
    l = l - 1
    r = r - 1

    # Subof strr from the
    # indices l to r.
    temp= strr[l: r - l + 1]

    #Extract kth Largest character
    ans = find_kth_largest(temp, k)

    return ans

# Function to replace character at
# pos of strr by the character s
def updateString(strr, pos, s):
    # Index of S to be updated.
    index = pos - 1
    c = s

    # Character to be replaced
    # at index in S
    strr[index] = c

# Driver Code
if __name__ == '__main__':

    # Given string
    strr = "abcddef"
    strr=[i for i in strr]

    # Count of queries
    Q = 3

    # Queries
    print(printCharacter(strr, 1, 2, 2))
    updateString(strr, 4, 'g')
    print(printCharacter(strr, 1, 5, 4))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the kth greatest
// character from the string
static char find_kth_largest(char []str,
                             int k)
{

    // Sorting the String in
    // non-increasing Order
    Array.Sort(str);
    reverse(str);

    return str[k - 1];
}

static char[] reverse(char []a)
{
    int i, n = a.Length;
    char t;

    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to print the K-th character
// from the subString S[l] .. S[r]
static char printchar(String str, int l,
                           int r, int k)
{

    // 0-based indexing
    l = l - 1;
    r = r - 1;

    // SubString of str from the
    // indices l to r.
    String temp = str.Substring(l, r - l + 1);

    // Extract kth Largest character
    char ans = find_kth_largest(
               temp.ToCharArray(), k);

    return ans;
}

// Function to replace character at
// pos of str by the character s
static void updateString(char []str,
                         int pos, char s)
{

    // Index of S to be updated.
    int index = pos - 1;
    char c = s;

    // char to be replaced
    // at index in S
    str[index] = c;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String str = "abcddef";

    // Count of queries
    //int Q = 3;

    // Queries
    Console.Write(printchar(str, 1, 2, 2) + "\n");
    updateString(str.ToCharArray(), 4, 'g');

    Console.Write(printchar(str, 1, 5, 4) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach
//include "bits/stdJava.h"

// Function to find the kth greatest
// character from the strijng
function find_kth_largest(str,k)
{
  // Sorting the String in
  // non-increasing Order
  str.sort();
  reverse(str);
  return str[k - 1];
}

function reverse(a)
{
    let i, n = a.length;
    let t;
    for (i = 0; i < Math.floor(n / 2); i++)
    {
      t = a[i];
      a[i] = a[n - i - 1];
      a[n - i - 1] = t;
    }
    return a;
}

// Function to print the K-th character
// from the subString S[l] .. S[r]
function printCharacter(str,l,r,k)
{
  // 0-based indexing
  l = l - 1;
  r = r - 1;

  // SubString of str from the
  // indices l to r.
  let temp = str.substring(l, r - l + 1);

  // Extract kth Largest character
  let ans =
    find_kth_largest(temp.split(""), k);

  return ans;
}

// Function to replace character at
// pos of str by the character s
function updateString(str,pos,s)
{
  // Index of S to be updated.
  let index = pos - 1;
  let c = s;

  // Character to be replaced
  // at index in S
  str[index] = c;
}

// Driver Code
// Given String
let str = "abcddef";
// Count of queries
let Q = 3;

// Queries
document.write(printCharacter(str, 1,
                                2, 2) + "<br>");
updateString(str.split(""), 4, 'g');
document.write(printCharacter(str, 1,
                                5, 4) + "<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
a
b
```

**高效方法:**通过使用[芬威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)高效地预计算大于或等于字符 **C** ( 'a' ≤ C ≤ 'z ')的所有字符的计数，可以优化上述方法。
按照以下步骤解决问题:

*   创建一个**分威克树**来存储从“ **a”到“z** 的所有字符的频率
*   对于**类型 1** 的每个查询，检查从**‘z’到‘a’的每个字符，**是否是 **K <sup>th</sup>** 最伟大的字符。
*   为了执行此操作，从**“z”到**遍历，对于每个字符，检查遍历的所有字符的计数是否为≥ **K** 。打印计数变为≥ **K** 的字符。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include "bits/stdc++.h"
using namespace std;

// Maximum Size of a String
const int maxn = 100005;

// Fenwick Tree to store the
// frequencies of 26 alphabets
int BITree[26][maxn];

// Size of the String.
int N;

// Function to update Fenwick Tree for
// Character c at index val
void update_BITree(int index, char C,
                   int val)
{
    while (index <= N) {

        // Add val to current node
        // Fenwick Tree
        BITree[C - 'a'][index]
            += val;

        // Move index to parent node
        // in update View
        index += (index & -index);
    }
}

// Function to get sum of frequencies
// of character c till index
int sum_BITree(int index, char C)
{

    // Stores the sum
    int s = 0;
    while (index) {

        // Add current element of
        // Fenwick tree to sum
        s += BITree[C - 'a'][index];

        // Move index to parent node
        // in getSum View
        index -= (index & -index);
    }
    return s;
}

// Function to create the Fenwick tree
void buildTree(string str)
{
    for (int i = 1; i <= N; i++) {

        update_BITree(i, str[i], 1);
    }
    cout << endl;
}

// Function to print the kth largest
// character in the range of l to r
char printCharacter(string str, int l,
                    int r, int k)
{

    // Stores the count of
    // characters
    int count = 0;

    // Stores the required
    // character
    char ans;

    for (char C = 'z'; C >= 'a'; C--) {

        // Calculate frequency of
        // C in the given range
        int times = sum_BITree(r, C)
                    - sum_BITree(l - 1, C);

        // Increase count
        count += times;

        // If count exceeds K
        if (count >= k) {

            // Required character
            // found
            ans = C;
            break;
        }
    }

    return ans;
}

// Function to update character
// at pos by character s
void updateTree(string str, int pos,
                char s)
{

    // 0 based index system
    int index = pos;
    update_BITree(index, str[index], -1);

    str[index] = s;
    update_BITree(index, s, 1);
}

// Driver Code
int main()
{
    string str = "abcddef";
    N = str.size();

    // Makes the string 1-based indexed
    str = '#' + str;

    // Number of queries
    int Q = 3;

    // Construct the Fenwick Tree
    buildTree(str);

    cout << printCharacter(str, 1, 2, 2)
         << endl;
    updateTree(str, 4, 'g');
    cout << printCharacter(str, 1, 5, 4)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

//include "bits/stdJava.h"
import java.util.*;
class GFG{

// Maximum Size of a String
static int maxn = 100005;

// Fenwick Tree to store the
// frequencies of 26 alphabets
static int [][]BITree = new int[26][maxn];

// Size of the String.
static int N;

// Function to update Fenwick Tree for
// Character c at index val
static void update_BITree(int index,
                          char C, int val)
{
  while (index <= N)
  {
    // Add val to current node
    // Fenwick Tree
    BITree[C - 'a'][index] += val;

    // Move index to parent node
    // in update View
    index += (index & -index);
  }
}

// Function to get sum of frequencies
// of character c till index
static int sum_BITree(int index, char C)
{

  // Stores the sum
  int s = 0;
  while (index > 0)
  {
    // Add current element of
    // Fenwick tree to sum
    s += BITree[C - 'a'][index];

    // Move index to parent node
    // in getSum View
    index -= (index & -index);
  }
  return s;
}

// Function to create the Fenwick tree
static void buildTree(String str)
{
  for (int i = 1; i <= N; i++)
  {
    update_BITree(i, str.charAt(i), 1);
  }
  System.out.println();
}

// Function to print the kth largest
// character in the range of l to r
static char printCharacter(String str, int l,
                           int r, int k)
{
  // Stores the count of
  // characters
  int count = 0;

  // Stores the required
  // character
  char ans = 0;

  for (char C = 'z'; C >= 'a'; C--)
  {
    // Calculate frequency of
    // C in the given range
    int times = sum_BITree(r, C) -
      sum_BITree(l - 1, C);

    // Increase count
    count += times;

    // If count exceeds K
    if (count >= k)
    {
      // Required character
      // found
      ans = C;
      break;
    }
  }
  return ans;
}

// Function to update character
// at pos by character s
static void updateTree(String str,
                       int pos, char s)
{
    // 0 based index system
    int index = pos;
    update_BITree(index,
                  str.charAt(index), -1);
    str = str.substring(0, index) + s +
          str.substring(index + 1);
    update_BITree(index, s, 1);
}

// Driver Code
public static void main(String[] args)
{
  String str = "abcddef";
  N = str.length();

  // Makes the String 1-based indexed
  str = '/' + str;

  // Number of queries
  int Q = 3;

  // Construct the Fenwick Tree
  buildTree(str);

  System.out.print(printCharacter(str, 1,
                                  2, 2) + "\n");
  updateTree(str, 4, 'g');
  System.out.print(printCharacter(str, 1,
                                  5, 4) + "\n");

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Maximum Size of a String
maxn = 100005

# Fenwick Tree to store the
# frequencies of 26 alphabets
BITree = [[0 for x in range(maxn)]
             for y in range(26)]

# Size of the String.
N = 0

# Function to update Fenwick Tree for
# Character c at index val
def update_BITree(index, C, val):

    while (index <= N):

        # Add val to current node
        # Fenwick Tree
        BITree[ord(C) -
               ord('a')][index]+= val

        # Move index to parent node
        # in update View
        index += (index & -index)

# Function to get sum of
# frequencies of character
# c till index
def sum_BITree(index, C):

    # Stores the sum
    s = 0
    while (index):

        # Add current element of
        # Fenwick tree to sum
        s += BITree[ord(C) -
                    ord('a')][index]

        # Move index to parent node
        # in getSum View
        index -= (index & -index)
    return s

# Function to create
# the Fenwick tree
def buildTree(st):

    for i in range(1,
                   N + 1):
        update_BITree(i,
                      st[i], 1)

    print()

# Function to print the
# kth largest character
# in the range of l to r
def printCharacter(st, l,
                   r, k):

    # Stores the count of
    # characters
    count = 0

    for C in range(ord('z'),
                   ord('a') -
                   1, -1):

        # Calculate frequency of
        # C in the given range
        times = (sum_BITree(r, chr(C)) -
                 sum_BITree(l - 1, chr(C)))

        # Increase count
        count += times

        # If count exceeds K
        if (count >= k):

            # Required character
            # found
            ans = chr( C)
            break

    return ans

# Function to update character
# at pos by character s
def updateTree(st, pos, s):

    # 0 based index system
    index = pos;
    update_BITree(index,
                  st[index], -1)

    st.replace(st[index], s, 1)
    update_BITree(index, s, 1)

# Driver Code
if __name__ == "__main__":

    st = "abcddef"
    N = len(st)

    # Makes the string
    # 1-based indexed
    st = '#' + st

    # Number of queries
    Q = 3

    # Construct the Fenwick Tree
    buildTree(st)

    print (printCharacter(st, 1,
                          2, 2))
    updateTree(st, 4, 'g')
    print (printCharacter(st, 1,
                          5, 4))

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Maximum Size of a String
static int maxn = 100005;

// Fenwick Tree to store the
// frequencies of 26 alphabets
static int [,]BITree = new int[26, maxn];

// Size of the String.
static int N;

// Function to update Fenwick Tree for
// char c at index val
static void update_BITree(int index,
                          char C, int val)
{
  while (index <= N)
  {
    // Add val to current node
    // Fenwick Tree
    BITree[C - 'a', index] += val;

    // Move index to parent node
    // in update View
    index += (index & -index);
  }
}

// Function to get sum of frequencies
// of character c till index
static int sum_BITree(int index, char C)
{
  // Stores the sum
  int s = 0;
  while (index > 0)
  {
    // Add current element of
    // Fenwick tree to sum
    s += BITree[C - 'a', index];

    // Move index to parent node
    // in getSum View
    index -= (index & -index);
  }
  return s;
}

// Function to create the Fenwick tree
static void buildTree(String str)
{
  for (int i = 1; i <= N; i++)
  {
    update_BITree(i, str[i], 1);
  }
  Console.WriteLine();
}

// Function to print the kth largest
// character in the range of l to r
static char printchar(String str, int l,
                      int r, int k)
{
  // Stores the count of
  // characters
  int count = 0;

  // Stores the required
  // character
  char ans = (char)0;

  for (char C = 'z'; C >= 'a'; C--)
  {
    // Calculate frequency of
    // C in the given range
    int times = sum_BITree(r, C) -
                sum_BITree(l - 1, C);

    // Increase count
    count += times;

    // If count exceeds K
    if (count >= k)
    {
      // Required character
      // found
      ans = C;
      break;
    }
  }
  return ans;
}

// Function to update character
// at pos by character s
static void updateTree(String str,
                       int pos, char s)
{
  // 0 based index system
  int index = pos;
  update_BITree(index,
                str[index], -1);
  str = str.Substring(0, index) + s +
    str.Substring(index + 1);
  update_BITree(index, s, 1);
}

// Driver Code
public static void Main(String[] args)
{
  String str = "abcddef";
  N = str.Length;

  // Makes the String 1-based indexed
  str = '/' + str;

  // Number of queries
  int Q = 3;

  // Construct the Fenwick Tree
  buildTree(str);

  Console.Write(printchar(str, 1, 2, 2) + "\n");
  updateTree(str, 4, 'g');
  Console.Write(printchar(str, 1, 5, 4) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Maximum Size of a String
let maxn = 100005;

// Fenwick Tree to store the
// frequencies of 26 alphabets
let BITree = new Array(26);
for(let i=0;i<26;i++)
{
    BITree[i]=new Array(maxn);
    for(let j=0;j<maxn;j++)
    {
        BITree[i][j]=0;
    }

}

// Size of the String.
let N;

// Function to update Fenwick Tree for
// Character c at index val
function update_BITree(index,C,val)
{
    while (index <= N)
  {
    // Add val to current node
    // Fenwick Tree
    BITree[C.charCodeAt(0) - 'a'.charCodeAt(0)][index] += val;

    // Move index to parent node
    // in update View
    index += (index & -index);
  }
}

// Function to get sum of frequencies
// of character c till index
function sum_BITree(index,C)
{
    // Stores the sum
  let s = 0;
  while (index > 0)
  {
    // Add current element of
    // Fenwick tree to sum
    s += BITree[C.charCodeAt(0) - 'a'.charCodeAt(0)][index];

    // Move index to parent node
    // in getSum View
    index -= (index & -index);
  }
  return s;
}

// Function to create the Fenwick tree
function buildTree(str)
{
    for (let i = 1; i <= N; i++)
  {
    update_BITree(i, str[i], 1);
  }
  document.write("<br>");
}

// Function to print the kth largest
// character in the range of l to r
function printCharacter(str,l,r,k)
{
    // Stores the count of
  // characters
  let count = 0;

  // Stores the required
  // character
  let ans = 0;

  for (let C = 'z'.charCodeAt(0); C >= 'a'.charCodeAt(0); C--)
  {
    // Calculate frequency of
    // C in the given range
    let times = sum_BITree(r, String.fromCharCode(C)) -
      sum_BITree(l - 1, String.fromCharCode(C));

    // Increase count
    count += times;

    // If count exceeds K
    if (count >= k)
    {
      // Required character
      // found
      ans = String.fromCharCode(C);
      break;
    }
  }
  return ans;
}

// Function to update character
// at pos by character s
function updateTree(str,pos,s)
{
    // 0 based index system
    let index = pos;
    update_BITree(index,
                  str[index], -1);
    str = str.substring(0, index) + s +
          str.substring(index + 1);
    update_BITree(index, s, 1);
}

// Driver Code
let str = "abcddef";
N = str.length;

// Makes the String 1-based indexed
str = '/' + str;

// Number of queries
let Q = 3;

// Construct the Fenwick Tree
buildTree(str);

document.write(printCharacter(str, 1,
                                2, 2) + "<br>");
updateTree(str, 4, 'g');
document.write(printCharacter(str, 1,
                                5, 4) + "<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
a
b
```

***时间复杂度:**O(QlogN+NlogN)*
***辅助空间:** O(26 * maxn)，其中 maxn 表示字符串的最大可能长度。*