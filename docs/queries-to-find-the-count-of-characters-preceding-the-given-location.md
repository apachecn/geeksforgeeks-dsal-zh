# 查询给定位置前的字符数

> 原文:[https://www . geesforgeks . org/query-to-find-给定位置前的字符数/](https://www.geeksforgeeks.org/queries-to-find-the-count-of-characters-preceding-the-given-location/)

给定长度为 **N** 的字符串 **S** ，其中只包含小写字母。另外，给定 **Q** 查询，其中每个查询由整数 **P** 组成，使得 **1≤ P ≤ N** 。任务是找出给定位置 **P** 前相同字母出现的次数。
**示例:**

```
Input: S = "abacsddaa", Q[] = {9, 3}
Output:
3
1
For first query, P = 9, character at 9th location is 'a'.
The number of occurrences of 'a' before P i.e. 9 is three.

Similarly, for P = 3, 3rd character is 'a'.
The number of occurrences of 'a' before P. i.e. 3 is one.
```

**天真方法**对于给出位置‘p’的每个查询 Q <sub>i</sub> ，运行从 1 到‘p-1’的循环，并检查该索引处存在的元素是否等于索引‘p’处的元素，如果是，则将计数器变量的值增加 1。循环完成后，在新行中打印计数器变量的值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

int Count(string s, int pos )
{
    // returns character at index pos - 1
    int c = s[pos - 1] ;
    int counter = 0 ;
    for (int i = 0; i < pos-1; i++ )
    {
        if(s[i] == c)
            counter = counter + 1;
    }
    return counter;
}

// Driver Code
int main()
{
    string s = "abacsddaa";
    int pos;
    int n = s.length();
    int query[] = {9, 3, 2};
    int Q = sizeof(query) / sizeof(query[0]);
    for(int i = 0; i < Q; i++ )
    {
        pos = query[i] ;
        cout << Count( s, pos ) << endl;
    }
    return 0;
}

// This code is contributed by
// divyamohan123
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static int Count(String s, int pos )
    {
        // returns character at index pos - 1
        int c = s.charAt(pos - 1);
        int counter = 0;
        for (int i = 0; i < pos - 1; i++ )
        {
            if(s.charAt(i) == c)
                counter = counter + 1;
        }
        return counter;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String s = "abacsddaa";
        int pos;
        int n = s.length();

        int query[] = {9, 3, 2};
        int Q = query.length;

        for(int i = 0; i < Q; i++)
        {
            pos = query[i];
            System.out.println(Count(s, pos));
        }
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
def Count( s, pos ):
    # returns character at index pos - 1
    c = s[pos - 1]
    counter = 0
    for i in range( pos - 1 ):
        if s[i] == c:
              counter = counter + 1 
    return counter

# Driver Code   
if __name__ == "__main__" :
    s = "abacsddaa"
    n = len(s)
    query = [9, 3, 2]
    Q = len(query)
    for i in range( Q ):
        pos = query[i]
        print(Count( s, pos ))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int Count(String s, int pos )
    {
        // returns character at index pos - 1
        int c = s[pos - 1];
        int counter = 0;
        for (int i = 0; i < pos - 1; i++ )
        {
            if(s[i] == c)
                counter = counter + 1;
        }
        return counter;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        String s = "abacsddaa";
        int pos;
        int n = s.Length;

        int []query = {9, 3, 2};
        int Q = query.Length;

        for(int i = 0; i < Q; i++)
        {
            pos = query[i];
            Console.WriteLine(Count(s, pos));
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    function Count(s, pos )
    {
        // returns character at index pos - 1
        let c = s[pos - 1];
        let counter = 0;
        for (let i = 0; i < pos - 1; i++ )
        {
            if(s[i] == c)
                counter = counter + 1;
        }
        return counter;
    }

    // Driver code

        let s = "abacsddaa";
        let pos;
        let n = s.length;

        let query = [9, 3, 2];
        let Q = query.length;

        for(let i = 0; i < Q; i++)
        {
            pos = query[i];
            document.write(Count(s, pos) + "<br/>");
        }

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
3
1
0
```