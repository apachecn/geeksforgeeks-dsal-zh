# 查询子串回文格式

> 原文:[https://www . geesforgeks . org/query-substring-回文-formation/](https://www.geeksforgeeks.org/queries-substring-palindrome-formation/)

给定一个字符串 **S** ，以及两种类型的查询。

```
Type 1: 1 L x, Indicates update Lth index 
               of string S by x character.
Type 2: 2 L R, Find if characters between position L and R 
               of string, S can form a palindrome string. 
               If palindrome can be formed print "Yes", 
               else print "No".
1 <= L, R <= |S| 
```

**例:**

```
Input : S = "geeksforgeeks"
Query 1: 1 4 g
Query 2: 2 1 4
Query 3: 2 2 3
Query 4: 1 10 t
Query 5: 2 10 11
Output :
Yes
Yes
No

Query 1: update index 3 (position 4) of string S by 
character 'g'. So new string S = "geegsforgeeks".

Query 2: find if rearrangement between index 0 and 3
can form a palindrome. "geegs" is palindrome, print "Yes".

Query 3: find if rearrangement between index 1 and 2 
can form a palindrome. "ee" is palindrome, print "Yes".

Query 4: update index 9 (position 10) of string S by 
character 't'. So new string S = "geegsforgteks".

Query 3: find if rearrangement between index 9 and 10 
can form a palindrome. "te" is not palindrome, print "No".
```

子串 S[L…R]只有在 S[L…R]中所有字符的频率都是偶数时才构成回文，允许有一个除外。

```
For query of type 1, simply update string 
S[L] by character x.

For each query of type 2, calculate the 
frequency of character and check if 
frequencies of all characters is even (with)
one exception allowed.
```

下面是两种不同的方法来查找 S[L…R]中每个字符的频率:
**方法 1:使用频率数组来查找 S[L…R]中每个元素的频率。**
以下是本办法的实施:

## C++

```
// C++ program to Queries on substring palindrome
// formation.
#include <bits/stdc++.h>
using namespace std;

// Query type 1: update string position i with
// character x.
void qType1(int l, int x, char str[])
{
    str[l - 1] = x;
}

// Print "Yes" if range [L..R] can form palindrome,
// else print "No".
void qType2(int l, int r, char str[])
{
    int freq[27] = { 0 };

    // Find the frequency of each character in
    // S[L...R].
    for (int i = l - 1; i <= r - 1; i++)
        freq[str[i] - 'a']++;

    // Checking if more than one character have
    // frequency greater than 1.
    int count = 0;
    for (int j = 0; j < 26; j++)
        if (freq[j] % 2)
            count++;

    (count <= 1) ? (cout << "Yes" << endl) : (cout << "No" << endl);
}

// Driven Program
int main()
{
    char str[] = "geeksforgeeks";
    int n = strlen(str);

    qType1(4, 'g', str);
    qType2(1, 4, str);
    qType2(2, 3, str);
    qType1(10, 't', str);
    qType2(10, 11, str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Queries on substring
// palindrome formation.

class GFG {

    // Query type 1: update string
    // position i with character x.
    static void qType1(int l, int x, char str[])
    {
        str[l - 1] = (char)x;
    }

    // Print "Yes" if range [L..R] can form
    // palindrome, else print "No".
    static void qType2(int l, int r, char str[])
    {
        int freq[] = new int[27];

        // Find the frequency of each
        // character in S[L...R].
        for (int i = l - 1; i <= r - 1; i++) {
            freq[str[i] - 'a']++;
        }

        // Checking if more than one character
        // have frequency greater than 1.
        int count = 0;
        for (int j = 0; j < 26; j++) {
            if (freq[j] % 2 != 0) {
                count++;
            }
        }
        if (count <= 1) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }

    // Driven code
    public static void main(String[] args)
    {
        char str[] = "geeksforgeeks".toCharArray();
        int n = str.length;

        qType1(4, 'g', str);
        qType2(1, 4, str);
        qType2(2, 3, str);
        qType1(10, 't', str);
        qType2(10, 11, str);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to Queries on substring
# palindrome formation.

# Query type 1: update str1ing position
# i with character x.
def qType1(l, x, str1):
    str1[l - 1] = x

# Pr"Yes" if range [L..R] can form palindrome,
# else pr"No".
def qType2(l, r, str1):

    freq = [0 for i in range(27)]

    # Find the frequency of
    # each character in S[L...R].
    for i in range(l - 1, r):
        freq[ord(str1[i]) - ord('a')] += 1

    # Checking if more than one character
    # have frequency greater than 1.
    count = 0
    for j in range(26):
        if (freq[j] % 2):
            count += 1
    if count <= 1:
        print("Yes")
    else:
        print("No")

# Driver Code
str1 = "geeksforgeeks"
str2 = [i for i in str1]
n = len(str2)

qType1(4, 'g', str2)
qType2(1, 4, str2)
qType2(2, 3, str2)
qType1(10, 't', str2)
qType2(10, 11, str2)

# This code is contributed by mohit kumar
```

## C#

```
// C# program to Queries on substring
// palindrome formation.
using System;

class GFG {

    // Query type 1: update string
    // position i with character x.
    static void qType1(int l, int x, char[] str)
    {
        str[l - 1] = (char)x;
    }

    // Print "Yes" if range [L..R] can form
    // palindrome, else print "No".
    static void qType2(int l, int r, char[] str)
    {
        int[] freq = new int[27];

        // Find the frequency of each
        // character in S[L...R].
        for (int i = l - 1; i <= r - 1; i++) {
            freq[str[i] - 'a']++;
        }

        // Checking if more than one character
        // have frequency greater than 1.
        int count = 0;
        for (int j = 0; j < 26; j++) {
            if (freq[j] % 2 != 0) {
                count++;
            }
        }
        if (count <= 1) {
            Console.WriteLine("Yes");
        }
        else {
            Console.WriteLine("No");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        char[] str = "geeksforgeeks".ToCharArray();
        int n = str.Length;

        qType1(4, 'g', str);
        qType2(1, 4, str);
        qType2(2, 3, str);
        qType1(10, 't', str);
        qType2(10, 11, str);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Queries on substring palindrome
// formation.

// Query type 1: update string position i with
// character x.
function qType1($l, $x, &$str)
{
    $str[$l - 1] = $x;
}

// Print "Yes" if range [L..R] can form palindrome,
// else print "No".
function qType2($l, $r, $str)
{
    $freq=array_fill(0, 27, 0);

    // Find the frequency of each character in
    // S[L...R].
    for ($i = $l - 1; $i <= $r - 1; $i++)
        $freq[ord($str[$i]) - ord('a')]++;

    // Checking if more than one character have
    // frequency greater than 1.
    $count = 0;
    for ($j = 0; $j < 26; $j++)
        if ($freq[$j] % 2)
            $count++;

    ($count <= 1) ? (print("Yes\n")) : (print("No\n"));
}

// Driver code
    $str = "geeksforgeeks";
    $n = strlen($str);

    qType1(4, 'g', $str);
    qType2(1, 4, $str);
    qType2(2, 3, $str);
    qType1(10, 't', $str);
    qType2(10, 11, $str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to Queries on substring
// palindrome formation.

     // Query type 1: update string
    // position i with character x.
    function qType1(l,x,str1)
    {
        str1[l - 1] = x;
    }

    // Print "Yes" if range [L..R] can form
    // palindrome, else print "No".
    function qType2(l,r,str1)
    {
        let freq = new Array(27);
        for(let i=0;i<27;i++)
        {
            freq[i]=0;
        }

        // Find the frequency of each
        // character in S[L...R].
        for (let i = l - 1; i <= r - 1; i++) {

            freq[str1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // Checking if more than one character
        // have frequency greater than 1.
        let count = 0;
        for (let j = 0; j < 26; j++) {
            if (freq[j] % 2 != 0) {
                count++;
            }
        }
        if (count <= 1) {
            document.write("Yes<br>");
        }
        else {
            document.write("No<br>");
        }
    }

    // Driven code
    let str="geeksforgeeks".split("");
    let n = str.length;
    qType1(4, 'g', str);
    qType2(1, 4, str);
    qType2(2, 3, str);
    qType1(10, 't', str);
    qType2(10, 11, str);

// This code is contributed by patel2127
</script>
```

**输出:**

```
Yes
Yes
No
```

**方法 2:使用二进制索引树**
有效的方法可以是为每个字母表维护 26 个[二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)。
定义一个函数 getFrequency(i，u)，返回 i <sup>第</sup>个前缀中‘u’的频率。范围 L…R 中字符' u '的频率可以通过 getFrequency(R，u)–getFrequency(L-1，u)找到。
每当更新(查询 1)将字符“u”更改为“v”时。位[u]在索引 I 处用-1 更新，位[v]在索引 I 处用+1 更新。
下面是该方法的实现:

## C++

```
// C++ program to Queries on substring palindrome
// formation.
#include <bits/stdc++.h>
#define max 1000
using namespace std;

// Return the frequency of the character in the
// i-th prefix.
int getFrequency(int tree[max][27], int idx, int i)
{
    int sum = 0;

    while (idx > 0) {
        sum += tree[idx][i];
        idx -= (idx & -idx);
    }

    return sum;
}

// Updating the BIT
void update(int tree[max][27], int idx, int val, int i)
{
    while (idx <= max) {
        tree[idx][i] += val;
        idx += (idx & -idx);
    }
}

// Query to update the character in the string.
void qType1(int tree[max][27], int l, int x, char str[])
{
    // Adding -1 at L position
    update(tree, l, -1, str[l - 1] - 97 + 1);

    // Updating the character
    str[l - 1] = x;

    // Adding +1 at R position
    update(tree, l, 1, str[l - 1] - 97 + 1);
}

// Query to find if rearrangement of character in range
// L...R can form palindrome
void qType2(int tree[max][27], int l, int r, char str[])
{
    int count = 0;

    for (int i = 1; i <= 26; i++) {
        // Checking on the first character of the string S.
        if (l == 1) {
            if (getFrequency(tree, r, i) % 2 == 1)
                count++;
        }
        else {
            // Checking if frequency of character is even or odd.
            if ((getFrequency(tree, r, i) - getFrequency(tree, l - 1, i)) % 2 == 1)
                count++;
        }
    }

    (count <= 1) ? (cout << "Yes" << endl) : (cout << "No" << endl);
}

// Creating the Binary Index Tree of all alphabet
void buildBIT(int tree[max][27], char str[], int n)
{
    memset(tree, 0, sizeof(tree));

    for (int i = 0; i < n; i++)
        update(tree, i + 1, 1, str[i] - 97 + 1);
}

// Driven Program
int main()
{
    char str[] = "geeksforgeeks";
    int n = strlen(str);

    int tree[max][27];
    buildBIT(tree, str, n);

    qType1(tree, 4, 'g', str);
    qType2(tree, 1, 4, str);
    qType2(tree, 2, 3, str);
    qType1(tree, 10, 't', str);
    qType2(tree, 10, 11, str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Queries on substring palindrome
// formation.

import java.util.*;

class GFG {

    static int max = 1000;

    // Return the frequency of the character in the
    // i-th prefix.
    static int getFrequency(int tree[][], int idx, int i)
    {
        int sum = 0;

        while (idx > 0) {
            sum += tree[idx][i];
            idx -= (idx & -idx);
        }

        return sum;
    }

    // Updating the BIT
    static void update(int tree[][], int idx,
                       int val, int i)
    {
        while (idx <= max) {
            tree[idx][i] += val;
            idx += (idx & -idx);
        }
    }

    // Query to update the character in the string.
    static void qType1(int tree[][], int l, int x, char str[])
    {
        // Adding -1 at L position
        update(tree, l, -1, str[l - 1] - 97 + 1);

        // Updating the character
        str[l - 1] = (char)x;

        // Adding +1 at R position
        update(tree, l, 1, str[l - 1] - 97 + 1);
    }

    // Query to find if rearrangement of character in range
    // L...R can form palindrome
    static void qType2(int tree[][], int l, int r, char str[])
    {
        int count = 0;

        for (int i = 1; i <= 26; i++) {
            // Checking on the first character of the string S.
            if (l == 1) {
                if (getFrequency(tree, r, i) % 2 == 1)
                    count++;
            }
            else {
                // Checking if frequency of character is even or odd.
                if ((getFrequency(tree, r, i) - getFrequency(tree, l - 1, i)) % 2 == 1)
                    count++;
            }
        }

        if (count <= 1)
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Creating the Binary Index Tree of all aphabet
    static void buildBIT(int tree[][], char str[], int n)
    {

        for (int i = 0; i < n; i++)
            update(tree, i + 1, 1, str[i] - 97 + 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        char str[] = "geeksforgeeks".toCharArray();
        int n = str.length;

        int tree[][] = new int[max][27];
        buildBIT(tree, str, n);

        qType1(tree, 4, 'g', str);
        qType2(tree, 1, 4, str);
        qType2(tree, 2, 3, str);
        qType1(tree, 10, 't', str);
        qType2(tree, 10, 11, str);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to Queries on substr1ing palindrome
# formation.

max = 1000;

# Return the frequency of the character in the
# i-th prefix.
def getFrequency(tree, idx, i):
    sum = 0;

    while (idx > 0):
        sum += tree[idx][i];
        idx -= (idx & -idx);

    return sum;

# Updating the BIT
def update(tree, idx, val, i):
    while (idx <= max):
        tree[idx][i] += val;
        idx += (idx & -idx);

# Query to update the character in the str1ing.
def qType1(tree, l, x, str1):

    # Adding -1 at L position
    update(tree, l, -1, ord(str1[l - 1]) - 97 + 1);

    # Updating the character
    list1 = list(str1)
    list1[l - 1] = x;
    str1 = ''.join(list1);

    # Adding +1 at R position
    update(tree, l, 1, ord(str1[l - 1]) - 97 + 1);

# Query to find if rearrangement of character in range
# L...R can form palindrome
def qType2(tree, l, r, str1):
    count = 0;

    for i in range(1, 27):

        # Checking on the first character of the str1ing S.
        if (l == 1):
            if (getFrequency(tree, r, i) % 2 == 1):
                count+=1;
        else:
            # Checking if frequency of character is even or odd.
            if ((getFrequency(tree, r, i) -
                getFrequency(tree, l - 1, i)) % 2 == 1):
                count += 1;

    print("Yes") if(count <= 1) else print("No");

# Creating the Binary Index Tree of all aphabet
def buildBIT(tree,str1, n):

    for i in range(n):
        update(tree, i + 1, 1, ord(str1[i]) - 97 + 1);

# Driver code

str1 = "geeksforgeeks";
n = len(str1);

tree = [[0 for x in range(27)] for y in range(max)];
buildBIT(tree, str1, n);

qType1(tree, 4, 'g', str1);
qType2(tree, 1, 4, str1);
qType2(tree, 2, 3, str1);
qType1(tree, 10, 't', str1);
qType2(tree, 10, 11, str1);

# This code is contributed by mits
```

## C#

```
// C# program to Queries on substring palindrome
// formation.
using System;

class GFG
{

    static int max = 1000;

    // Return the frequency of the character in the
    // i-th prefix.
    static int getFrequency(int [,]tree, int idx, int i)
    {
        int sum = 0;

        while (idx > 0)
        {
            sum += tree[idx,i];
            idx -= (idx & -idx);
        }

        return sum;
    }

    // Updating the BIT
    static void update(int [,]tree, int idx,
                    int val, int i)
    {
        while (idx <= max)
        {
            tree[idx,i] += val;
            idx += (idx & -idx);
        }
    }

    // Query to update the character in the string.
    static void qType1(int [,]tree, int l, int x, char []str)
    {
        // Adding -1 at L position
        update(tree, l, -1, str[l - 1] - 97 + 1);

        // Updating the character
        str[l - 1] = (char)x;

        // Adding +1 at R position
        update(tree, l, 1, str[l - 1] - 97 + 1);
    }

    // Query to find if rearrangement of character in range
    // L...R can form palindrome
    static void qType2(int [,]tree, int l, int r, char []str)
    {
        int count = 0;

        for (int i = 1; i <= 26; i++)
        {
            // Checking on the first character of the string S.
            if (l == 1)
            {
                if (getFrequency(tree, r, i) % 2 == 1)
                    count++;
            }
            else
            {
                // Checking if frequency of character is even or odd.
                if ((getFrequency(tree, r, i) - getFrequency(tree, l - 1, i)) % 2 == 1)
                    count++;
            }
        }

        if (count <= 1)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

    // Creating the Binary Index Tree of all aphabet
    static void buildBIT(int [,]tree, char []str, int n)
    {

        for (int i = 0; i < n; i++)
            update(tree, i + 1, 1, str[i] - 97 + 1);
    }

    // Driver code
    static void Main()
    {
        char []str = "geeksforgeeks".ToCharArray();
        int n = str.Length;

        int[,] tree = new int[max,27];
        buildBIT(tree, str, n);

        qType1(tree, 4, 'g', str);
        qType2(tree, 1, 4, str);
        qType2(tree, 2, 3, str);
        qType1(tree, 10, 't', str);
        qType2(tree, 10, 11, str);
    }
}

// This code contributed by mits
```

## java 描述语言

```
<script>

// Javascript program to Queries
// on substring palindrome
// formation.

    let max = 1000;
    // Return the frequency of the character in the
    // i-th prefix.
    function getFrequency(tree,idx,i)
    {
        let sum = 0;

        while (idx > 0) {
            sum += tree[idx][i];
            idx -= (idx & -idx);
        }

        return sum;
    }

    // Updating the BIT
    function update(tree,idx,val,i)
    {
        while (idx <= max) {
            tree[idx][i] += val;
            idx += (idx & -idx);
        }
    }

    // Query to update the character in the string.
    function qType1(tree,l,x,str)
    {
        // Adding -1 at L position
        update(tree, l, -1,
        str[l - 1].charCodeAt(0) - 97 + 1);

        // Updating the character
        str[l - 1] = x;

        // Adding +1 at R position
        update(tree, l, 1,
        str[l - 1].charCodeAt(0) - 97 + 1);
    }

    // Query to find if rearrangement
    // of character in range
    // L...R can form palindrome
    function qType2(tree,l,r,str)
    {
        let count = 0;

        for (let i = 1; i <= 26; i++) {
            // Checking on the first character
            // of the string S.
            if (l == 1) {
                if (getFrequency(tree, r, i) % 2 == 1)
                    count++;
            }
            else {
                // Checking if frequency of
                // character is even or odd.
                if ((getFrequency(tree, r, i) -
                getFrequency(tree, l - 1, i)) % 2 == 1)
                    count++;
            }
        }

        if (count <= 1)
            document.write("Yes<br>");
        else
            document.write("No<br>");
    }

    // Creating the Binary Index Tree of all aphabet
    function buildBIT(tree,str,n)
    {
        for (let i = 0; i < n; i++)
            update(tree, i + 1, 1,
            str[i].charCodeAt(0) - 97 + 1);
    }

    // Driver code
    let str="geeksforgeeks".split("");
    let n = str.length;
    let tree=new Array(max);
    for(let i=0;i<tree.length;i++)
    {
        tree[i]=new Array(27);
        for(let j=0;j<tree[i].length;j++)
        {
            tree[i][j]=0;
        }
    }

    buildBIT(tree, str, n);

    qType1(tree, 4, 'g', str);
    qType2(tree, 1, 4, str);
    qType2(tree, 2, 3, str);
    qType1(tree, 10, 't', str);
    qType2(tree, 10, 11, str);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
Yes
Yes
No
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。