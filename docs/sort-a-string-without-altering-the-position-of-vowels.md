# 在不改变元音位置的情况下对字符串进行排序

> 原文:[https://www . geesforgeks . org/sort-a-string-不改变元音的位置/](https://www.geeksforgeeks.org/sort-a-string-without-altering-the-position-of-vowels/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是在不改变元音位置的情况下[对字符串](https://www.geeksforgeeks.org/sort-string-characters/)进行排序。

**示例:**

> **输入:**S = " geeksforgeks "
> T3】输出:feeggkokres
> **解释:**
> 字符串中出现的辅音是 **gksfrgks** 。对辅音进行排序会将其顺序修改为 **fggkkrss** 。
> 现在，通过将排序后的辅音放在这些位置来更新字符串。
> 
> **输入:** S =【苹果】
> T3】输出:阿尔佩

**方法:**按照以下步骤解决问题:

*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，比如**温度**。
*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)T2
*   如果当前字符是辅音，将字符插入 **temp** 。
*   [按照字典顺序对字符串](https://www.geeksforgeeks.org/sort-a-string-in-java-2-different-ways/) **temp** 进行排序。
*   初始化一个指针，比如 **ptr = 0** ，指向字符串 **temp** 中的当前字符。
*   现在，[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** ，用**temp【ptr】**替换字符串 **S** 的每个辅音。递增 **ptr** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the string
// leaving the vowels unchanged
void sortStr(string S)
{
    // Length of string S
    int N = S.size();

    string temp = "";

    // Traverse the string S
    for (int i = 0; i < N; i++) {
        if (S[i] != 'a' && S[i] != 'e' && S[i] != 'i'
            && S[i] != 'o' && S[i] != 'u')
            temp += S[i];
    }

    // Sort the string temp
    if (temp.size())
        sort(temp.begin(), temp.end());

    // Pointer to traverse the
    // sorted string of consonants
    int ptr = 0;

    // Traverse the string S
    for (int i = 0; i < N; i++) {
        if (S[i] != 'a' && S[i] != 'e' && S[i] != 'i'
            && S[i] != 'o' && S[i] != 'u')
            S[i] = temp[ptr++];
    }

    cout << S;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    sortStr(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to sort the string
// leaving the vowels unchanged
static void sortStr(String str)
{
    char S[] = str.toCharArray();

    // Length of string S
    int N = S.length;

    ArrayList<Character> temp = new ArrayList<>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {
        if (S[i] != 'a' && S[i] != 'e' &&
            S[i] != 'i' && S[i] != 'o' &&
            S[i] != 'u')
            temp.add(S[i]);
    }

    // Sort the string temp
    if (temp.size() != 0)
        Collections.sort(temp);

    // Pointer to traverse the
    // sorted string of consonants
    int ptr = 0;

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {
        if (S[i] != 'a' && S[i] != 'e' &&
            S[i] != 'i' && S[i] != 'o' &&
            S[i] != 'u')
            S[i] = temp.get(ptr++);
    }
    System.out.println(new String(S));
}

// Driver Code
public static void main(String[] args)
{
    String S = "geeksforgeeks";

    sortStr(S);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to sort the string
# leaving the vowels unchanged
def sortStr(S):

    # Length of string S
    N = len(S)
    temp = ""

    # Traverse the string S
    for i in range(N):
        if (S[i] != 'a' and S[i] != 'e' and S[i] != 'i'
                and S[i] != 'o'and S[i] != 'u'):
            temp += S[i]

    # Sort the string temp
    if (len(temp)):
        p = list(temp)
        p.sort()
        temp=''.join(p)

    # Pointer to traverse the
    # sorted string of consonants
    ptr = 0

    # Traverse the string S
    for i in range(N):
      S = list(S)
      if (S[i] != 'a' and S[i] != 'e' and S[i] != 'i'
                and S[i] != 'o' and S[i] != 'u'):
            S[i] = temp[ptr]
            ptr += 1

    print(''.join(S))

# Driver Code
if __name__ == "__main__":

    S = "geeksforgeeks"
    sortStr(S)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG{

// Function to sort the string
// leaving the vowels unchanged
static void sortStr(String str)
{
    char []S = str.ToCharArray();

    // Length of string S
    int N = S.Length;

    List<char> temp = new List<char>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {
        if (S[i] != 'a' && S[i] != 'e' &&
            S[i] != 'i' && S[i] != 'o' &&
            S[i] != 'u')
            temp.Add(S[i]);
    }

    // Sort the string temp
    if (temp.Count != 0)
        temp.Sort();

    // Pointer to traverse the
    // sorted string of consonants
    int ptr = 0;

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {
        if (S[i] != 'a' && S[i] != 'e' &&
            S[i] != 'i' && S[i] != 'o' &&
            S[i] != 'u')
            S[i] = temp[ptr++];
    }
    Console.WriteLine(new String(S));
}

// Driver Code
public static void Main(String[] args)
{
    String S = "geeksforgeeks";

    sortStr(S);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to sort the string
// leaving the vowels unchanged
function sortStr(str)
{
    var S = str.split('');

    // Length of string S
    var N = S.length;

    var temp = [];

    // Traverse the string S
    for(var i = 0; i < N; i++)
    {
        if (S[i] != 'a' && S[i] != 'e' &&
            S[i] != 'i' && S[i] != 'o' &&
            S[i] != 'u')
            temp.push(S[i]);
    }

    // Sort the string temp
    if (temp.length != 0)
        temp.sort();

    // Pointer to traverse the
    // sorted string of consonants
    var ptr = 0;

    // Traverse the string S
    for(var i = 0; i < N; i++)
    {
        if (S[i] != 'a' && S[i] != 'e' &&
            S[i] != 'i' && S[i] != 'o' &&
            S[i] != 'u')
            S[i] = temp[ptr++];
    }
    var str = "";
    for(var i =0;i<S.length;i++)
    str+=S[i];

    document.write(str);
}

// Driver Code

    var S = "geeksforgeeks";

    sortStr(S);

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
feeggkokreess
```

***时间复杂度:** O(N logN)*
***辅助空间:** O(N)*