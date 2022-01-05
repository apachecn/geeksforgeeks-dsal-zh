# 可移除的最长子串长度

> 原文:[https://www . geesforgeks . org/length-最长-子字符串-can-make-removed/](https://www.geeksforgeeks.org/length-longest-sub-string-can-make-removed/)

给定一个二进制字符串(仅由 0 和 1 组成)。如果字符串中有“100”作为子字符串，那么我们可以删除这个子字符串。任务是找到最长的子串的长度，它可以被删除？
示例:

```
Input  : str = "1011100000100"
Output : 6
// Sub-strings present in str that can be make removed 
// 101{110000}0{100}. First sub-string 110000-->100-->null,
// length is = 6\. Second sub-string 100-->null, length is = 3

Input  : str = "111011"
Output : 0
// There is no sub-string which can be make null
```

我们可以使用一个容器来解决这个问题，比如 c++中的[vector](https://www.geeksforgeeks.org/vector-in-cpp-stl/)或者 Java 中的[ArrayList](https://www.geeksforgeeks.org/arraylist-in-java/)。下面是解决这个问题的算法:

*   取一对类型的向量 arr。arr 中的每个元素存储两个值字符和它在字符串中各自的索引。
*   存储对(“@”，-1)作为 arr 中的基数。取存储最终结果的变量 maxlen = 0。
*   现在对字符串中的所有字符逐一迭代，生成一对字符及其各自的索引，并将其存储在 arr 中。同时，如果在插入第一个字符后，arr 的最后三个元素构成子字符串“100”，也要检查条件。
*   如果子字符串存在，则将其从“arr”中删除。多次重复此循环，直到 arr 中出现子字符串“100”，并通过连续删除使其为空。
*   删除后 arr 中当前存在的第 I 个字符的索引和最后一个元素的索引之间的差异给出了子串的长度，通过连续删除子串“100”可以使该长度为空，更新 maxlen。

## C++

```
// C++ implementation of program to find the maximum length
// that can be removed
#include<bits/stdc++.h>
using namespace std;

// Function to find the length of longest sub-string that
// can me make removed
// arr  --> pair type of array whose first field store
//          character in string and second field stores
//          corresponding index of that character
int longestNull(string str)
{
    vector<pair<char,int> > arr;

    // store {'@',-1} in arr , here this value will
    // work as base index
    arr.push_back({'@', -1});

    int maxlen = 0;   // Initialize result

    // one by one iterate characters of string
    for (int i = 0; i < str.length(); ++i)
    {
        // make pair of char and index , then store
        // them into arr
        arr.push_back({str[i], i});

        // now if last three elements of arr[]  are making
        // sub-string "100" or not
        while (arr.size()>=3 &&
               arr[arr.size()-3].first=='1' &&
               arr[arr.size()-2].first=='0' &&
               arr[arr.size()-1].first=='0')
        {
            // if above condition is true then delete
            // sub-string "100" from arr[]
            arr.pop_back();
            arr.pop_back();
            arr.pop_back();
        }

        // index of current last element in arr[]
        int tmp = arr.back().second;

        // This is important, here 'i' is the index of
        // current character inserted into arr[]
        // and 'tmp' is the index of last element in arr[]
        // after continuous deletion of sub-string
        // "100" from arr[] till we make it null, difference
        // of these to 'i-tmp' gives the length of current
        // sub-string that can be make null by continuous
        // deletion of sub-string "100"
        maxlen = max(maxlen, i - tmp);
    }

    return maxlen;
}

// Driver program to run the case
int main()
{
    cout << longestNull("1011100000100");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of program to find
// the maximum length that can be removed
import java.util.ArrayList;

public class GFG
{   
    // User defined class Pair
    static class Pair{
        char first;
        int second;
        Pair(char first, int second){
            this.first = first;
            this.second = second;
        }
    }

    /* Function to find the length of longest
    sub-string that can me make removed
     arr  --> pair type of array whose first
              field store character in string
              and second field stores
              corresponding index of that character*/
    static int longestNull(String str)
    {
        ArrayList<Pair> arr = new ArrayList<>();

        // store {'@',-1} in arr , here this value
        // will work as base index
        arr.add(new Pair('@', -1));

        int maxlen = 0;   // Initialize result

        // one by one iterate characters of string
        for (int i = 0; i < str.length(); ++i)
        {
            // make pair of char and index , then
            // store them into arr
            arr.add(new Pair(str.charAt(i), i));

            // now if last three elements of arr[]
            // are making sub-string "100" or not
            while (arr.size() >= 3 &&
                   arr.get(arr.size()-3).first=='1' &&
                   arr.get(arr.size()-2).first=='0' &&
                   arr.get(arr.size()-1).first=='0')
            {
                // if above condition is true then
                // delete sub-string "100" from arr[]
                arr.remove(arr.size() - 3);
                arr.remove(arr.size() - 2);
                arr.remove(arr.size() - 1);
            }

            // index of current last element in arr[]
            int tmp = arr.get(arr.size() - 1).second;

            // This is important, here 'i' is the index
            // of current character inserted into arr[]
            // and 'tmp' is the index of last element
            // in arr[] after continuous deletion of
            // sub-string "100" from arr[] till we make
            // it null, difference of these to 'i-tmp'
            // gives the length of current sub-string
            // that can be make null by continuous
            // deletion of sub-string "100"
            maxlen = Math.max(maxlen, i - tmp);
        }

        return maxlen;
    }

    // Driver program to run the case
    public static void main(String args[])
    {
        System.out.println(longestNull("1011100000100"));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 implementation of program to find the maximum length
# that can be removed

# Function to find the length of longest sub-that
# can me make removed
# arr --> pair type of array whose first field store
#         character in and second field stores
#         corresponding index of that character
def longestNull(S):

    arr=[]

    # store {'@',-1} in arr , here this value will
    # work as base index
    arr.append(['@', -1])

    maxlen = 0 # Initialize result

    # one by one iterate characters of Sing
    for i in range(len(S)):
        # make pair of char and index , then store
        # them into arr
        arr.append([S[i], i])

        # now if last three elements of arr[] are making
        # sub-"100" or not
        while (len(arr)>=3 and
            arr[len(arr)-3][0]=='1' and
            arr[len(arr)-2][0]=='0' and
            arr[len(arr)-1][0]=='0'):

            # if above condition is true then delete
            # sub-"100" from arr[]
            arr.pop()
            arr.pop()
            arr.pop()

        # index of current last element in arr[]
        tmp = arr[-1]
        # This is important, here 'i' is the index of
        # current character inserted into arr[]
        # and 'tmp' is the index of last element in arr[]
        # after continuous deletion of sub-Sing
        # "100" from arr[] till we make it null, difference
        # of these to 'i-tmp' gives the length of current
        # sub-that can be make null by continuous
        # deletion of sub-"100"
        maxlen = max(maxlen, i - tmp[1])

    return maxlen

# Driver code

print(longestNull("1011100000100"))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of program to find
// the maximum length that can be removed
using System;
using System.Collections.Generic;

class GFG
{
    // User defined class Pair
    class Pair
    {
        public char first;
        public int second;
        public Pair(char first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    /* Function to find the length of longest
    sub-string that can me make removed
    arr --> pair type of array whose first
            field store character in string
            and second field stores
            corresponding index of that character*/
    static int longestNull(String str)
    {
        List<Pair> arr = new List<Pair>();

        // store {'@',-1} in arr , here this value
        // will work as base index
        arr.Add(new Pair('@', -1));

        int maxlen = 0; // Initialize result

        // one by one iterate characters of string
        for (int i = 0; i < str.Length; ++i)
        {
            // make pair of char and index , then
            // store them into arr
            arr.Add(new Pair(str[i], i));

            // now if last three elements of []arr
            // are making sub-string "100" or not
            while (arr.Count >= 3 &&
                arr[arr.Count-3].first=='1' &&
                arr[arr.Count-2].first=='0' &&
                arr[arr.Count-1].first=='0')
            {
                // if above condition is true then
                // delete sub-string "100" from []arr
                arr.RemoveAt(arr.Count - 3);
                arr.RemoveAt(arr.Count - 2);
                arr.RemoveAt(arr.Count - 1);
            }

            // index of current last element in []arr
            int tmp = arr[arr.Count - 1].second;

            // This is important, here 'i' is the index
            // of current character inserted into []arr
            // and 'tmp' is the index of last element
            // in []arr after continuous deletion of
            // sub-string "100" from []arr till we make
            // it null, difference of these to 'i-tmp'
            // gives the length of current sub-string
            // that can be make null by continuous
            // deletion of sub-string "100"
            maxlen = Math.Max(maxlen, i - tmp);
        }

        return maxlen;
    }

    // Driver code
    public static void Main(String []args)
    {
        Console.WriteLine(longestNull("1011100000100"));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of program to find
// the maximum length that can be removed

    /* Function to find the length of longest
    sub-string that can me make removed
     arr  --> pair type of array whose first
              field store character in string
              and second field stores
              corresponding index of that character*/
    function longestNull(str)
    {
        let arr = [];

        // store {'@',-1} in arr , here this value
        // will work as base index
        arr.push(['@', -1]);

        let maxlen = 0;   // Initialize result

        // one by one iterate characters of string
        for (let i = 0; i < str.length; ++i)
        {
            // make pair of char and index , then
            // store them into arr
            arr.push([str[i],i]);

            // now if last three elements of arr[]
            // are making sub-string "100" or not
            while (arr.length >= 3 &&
                   arr[arr.length-3][0]=='1' &&
                   arr[arr.length-2][0]=='0' &&
                   arr[arr.length-1][0]=='0')
            {
                // if above condition is true then
                // delete sub-string "100" from arr[]
                arr.pop();
                arr.pop();
                arr.pop();
            }

            // index of current last element in arr[]
            let tmp = arr[arr.length-1][1];

            // This is important, here 'i' is the index
            // of current character inserted into arr[]
            // and 'tmp' is the index of last element
            // in arr[] after continuous deletion of
            // sub-string "100" from arr[] till we make
            // it null, difference of these to 'i-tmp'
            // gives the length of current sub-string
            // that can be make null by continuous
            // deletion of sub-string "100"
            maxlen = Math.max(maxlen, i - tmp);
        }

        return maxlen;
    }

    // Driver program to run the case
    document.write(longestNull("1011100000100"));

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
6
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由 [**沙莎克·米什拉(古鲁)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。