# 每次字符替换后检查回文查询

> 原文:[https://www . geesforgeks . org/check-for-回文-每字符替换后-query/](https://www.geeksforgeeks.org/check-for-palindrome-after-every-character-replacement-query/)

给定一个字符串**字符串**和 **Q** 查询。每个查询包含一对整数(i1，i2)和一个字符“ch”。我们需要用新字符“ch”替换索引 i1 和 i2 处的字符，然后判断字符串是否是回文。(0 < = i1，i2 <弦长)
**例:**

```
Input : str = "geeks"  Q = 2
        query 1: i1 = 3 ,i2 = 0, ch = 'e'
        query 2: i1 = 0 ,i2 = 2, ch = 's'
Output : query 1: "NO"
         query 2: "NO"
Explanation :
        In query 1 : i1 = 3 , i2 = 0 ch = 'e'
                    After replacing char at index i1, i2
                    str[3] = 'e', str[0] = 'e'
                    string become "eeees" which is not
                    palindrome so output "NO"
        In query 2 : i1 = 0 i2 = 2  ch = 's'
                    After replacing char at index i1 , i2
                     str[0] = 's', str[2] = 's'
                    string become "sesks" which is
                    palindrome so output "NO"

Input : str = "jasonamat"  Q = 3
        query 1: i1 = 3, i2 = 8 ch = 'j'
        query 2: i1 = 2, i2 = 6 ch = 'n'
        query 3: i1 = 3, i2 = 7 ch = 'a'
Output :
       query 1: "NO"
       query 2: "NO"
       query 3: "YES"
```

一个**简单的解决方案**是，对于每个查询，我们用一个新的字符“ch”替换索引处的字符(i1 & i2)，然后检查字符串是否是回文。
以下是上述想法的实现

## C++

```
// C++ program to find if string becomes palindrome
// after every query.
#include<bits/stdc++.h>
using namespace std;

// Function to check if string is Palindrome or Not
bool IsPalindrome(string &str)
{
    int n = strlen(str);
    for (int i = 0; i < n/2 ; i++)
        if (str[i] != str[n-1-i])
            return false;
    return true;
}

// Takes two inputs for Q queries. For every query, it
// prints Yes if string becomes palindrome and No if not.
void Query(string &str, int Q)
{
    int i1, i2;
    char ch;

    // Process all queries one by one
    for (int q = 1 ; q <= Q ; q++ )
    {
        cin >> i1 >> i2 >> ch;

        // query 1: i1 = 3 ,i2 = 0, ch = 'e'
        // query 2: i1 = 0 ,i2 = 2 , ch = 's'
        // replace character at index i1 & i2 with new 'ch'
        str[i1] = str[i2] = ch;

        // check string is palindrome or not
        (isPalindrome(str)== true) ? cout << "YES" << endl :
                                     cout << "NO" << endl;
    }
}

// Driver program
int main()
{
    char str[] = "geeks";
    int Q = 2;
    Query(str, Q);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find if
# string becomes palindrome
# after every query.

# Function to check if string
# is Palindrome or Not
def isPalindrome(string: list) -> bool:
    n = len(string)
    for i in range(n // 2):
        if string[i] != string[n - 1 - i]:
            return False
    return True

# Takes two inputs for Q queries.
# For every query, it prints Yes
# if string becomes palindrome
# and No if not.
def Query(string: list, Q: int) -> None:

    # Process all queries one by one
    for i in range(Q):

        # To get space separated
        # input from user
        inp = list(input().split())

        # parsing user inputs as integers
        # and strings/char
        i1 = int(inp[0])
        i2 = int(inp[1])
        ch = inp[2]

        # query 1: i1 = 3 ,i2 = 0, ch = 'e'
        # query 2: i1 = 0 ,i2 = 2 , ch = 's'
        # replace character at index
        # i1 & i2 with new 'ch'
        string[i1] = string[i2] = ch

        # check string is palindrome or not
        if isPalindrome(string):
            print("Yes")
        else:
            print("No")

# Driver Code
if __name__ == "__main__":
    string = list("geeks")
    Q = 2
    Query(string, Q)

# This code is contributed by
# sanjeev2552
```

**输入:**

```
3 0 e
0 2 s
```

**输出:**

```
"NO"
"YES"
```

时间复杂度 O(Q*n) (n 是字符串长度)
一个有效的解决方案是使用哈希。我们创建一个空的散列集来存储回文中不相等的索引(**注意**:“我们必须只存储不相等的字符串的前半部分的索引”)。

```
Given string "str" and length 'n'.
Create an empty set S and store unequal indexes in first half.
Do following for each query :
   1\. First replace character at indexes i1 & i2 with 
      new char "ch"

   2\. If i1 and/or i2 are/is greater than n/2 then convert 
      into first half index(es)

   3\. In this step we make sure that S contains maintains 
      unequal indexes of first half.
      a) If str[i1] == str [n - 1 - i1] means i1 becomes 
         equal after replacement, remove it from S (if present)
         Else add i1 to S 
      b) Repeat step a) for i2 (replace i1 with i2)  

   4\. If S is empty then string is palindrome else NOT
```

下面是以上思路的 C++实现

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++/c program check if given string is palindrome
// or not after every query
#include<bits/stdc++.h>
using namespace std;

// This function makes sure that set S contains
// unequal characters from first half. This is called
// for every character.
void addRemoveUnequal(string &str, int index, int n,
                              unordered_set<int> &S)
{
    // If character becomes equal after query
    if (str[index] == str[n-1-index])
    {
        // Remove the current index from set if it
        // is present
        auto it = S.find(index);
        if (it != S.end())
            S.erase(it) ;
    }

    // If not equal after query, insert it into set
    else
        S.insert(index);
}

// Takes two inputs for Q queries. For every query, it
// prints Yes if string becomes palindrome and No if not.
void Query(string &str, int Q)
{
    int n = str.length();

    // create an empty set that store indexes of
    // unequal location in palindrome
    unordered_set<int> S;

    // we store indexes that are unequal in palindrome
    // traverse only first half of string
    for (int i=0; i<n/2; i++)
        if (str[i] != str[n-1-i])
            S.insert(i);

    // traversal the query
    for (int q=1; q<=Q; q++)
    {
        // query 1: i1 = 3, i2 = 0, ch = 'e'
        // query 2: i1 = 0, i2 = 2, ch = 's'
        int i1, i2;
        char ch;
        cin >> i1 >> i2 >> ch;

        // Replace characters at indexes i1 & i2 with
        // new char 'ch'
        str[i1] = str [i2] = ch;

        // If i1 and/or i2 greater than n/2
        // then convert into first half index
        if (i1 > n/2)
            i1 = n- 1 -i1;
        if (i2 > n/2)
            i2 = n -1 - i2;

        // call addRemoveUnequal function to insert and remove
        // unequal indexes
        addRemoveUnequal(str, i1 , n, S );
        addRemoveUnequal(str, i2 , n, S );

        // if set is not empty then string is not palindrome
        S.empty()? cout << "YES\n" : cout << "NO\n";
    }
}

// Driver program
int main()
{
    string str = "geeks";
    int Q = 2 ;
    Query(str, Q);
    return 0;
}
```

输入:

```
3 0 e
0 2 s
```

输出:

```
"NO"
"YES"
```

时间复杂度:在集合插入、删除和查找操作花费 O(1)时间的假设下，为 O(Q + n)。
本文由 [**尼尚特 _ 辛格(平图)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。