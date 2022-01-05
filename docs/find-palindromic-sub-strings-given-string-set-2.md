# 查找给定字符串的所有回文子串|集合 2

> 原文:[https://www . geesforgeks . org/find-回文-子字符串-给定-字符串-set-2/](https://www.geeksforgeeks.org/find-palindromic-sub-strings-given-string-set-2/)

给定一个字符串，任务是从给定的字符串中找到所有的回文子字符串。
在[集合–1](https://www.geeksforgeeks.org/find-number-distinct-palindromic-sub-strings-given-string/)中，已经讨论了另一种方法，该方法只考虑不同的子串，但是在这种情况下，相等的子串，即 ll 和 ll 被认为是两个子串，而不是一个。

**示例:**

> 输入:hellolle
> 输出:13
> 【h，e，l，ll，l，o，lol，lloll，ellille，l，ll，l，e】
> 解释:
> 1) ellolle
> 2) ll，ll–注意，这是两个不同的子串，只是碰巧相等
> 3) lol 和 lloll
> 4)当然，每个字母都可以被认为是回文–全部 8 个。
> 
> 输入:geesforgeks
> 输出:15
> 【g，e，ee，e，k，s，f，o，r，g，e，ee，e，k，s】

**方法:**
1-我们可以有两种类型的回文串需要处理-偶数长度-奇数长度
2-想法是考虑一个中点，通过每次增加一个距离或回文串，比较左边的元素和右边的元素，一直检查回文串，直到不匹配。
3-该算法一次处理偶数和奇数长度回文。
4-枢轴从 0 开始，以 0.5 的步长移动到终点。
……。a)当透视是非分数值时，则回文值是从 0 开始的整数。
……。b)当轴是一个小数值时，回文值类似于 0.5，1.5，2.5，3.5..
5-所以，每次我们得到一个回文匹配，我们把它放在一个列表中(这样重复的值被保留，因为每个重复的子串是由不同的字母位置组合获得的)

## C++

```
// c++ program to Count number of ways we
// can get palindrome string from a given
// string
#include<bits/stdc++.h>
using namespace std;

// function to find the substring of the
// string
string substring(string s,int a,int b)
{
    string s1="";

    // extract the specified position of
    // the string
    for(int i = a; i < b; i++)
        s1 = s1 + s[i];

    return s1;
}

// can get palindrome string from a
// given string
vector<string> allPalindromeSubstring(string s)
{
    vector<string> v ;

    // moving the pivot from starting till
    // end of the string
    for (float pivot = 0; pivot < s.length();
                                 pivot += .5)
    {

        // set radius to the first nearest
        // element on left and right
        float palindromeRadius = pivot -
                                  (int)pivot;

        // if the position needs to be
        // compared has an element and the
        // characters at left and right
        // matches
        while ((pivot + palindromeRadius)
         < s.length() && (pivot - palindromeRadius)
         >= 0 && s[((int)(pivot - palindromeRadius))]
             == s[((int)(pivot + palindromeRadius))])
        {

            v.push_back(substring(s,(int)(pivot -
                     palindromeRadius), (int)(pivot
                           + palindromeRadius + 1)));

            // increasing the radius by 1 to point
            // to the next elements in left and right
            palindromeRadius++;
        }
    }

    return v;
}

// Driver code
int main()
{
    vector <string> v =
                  allPalindromeSubstring("hellolle");

    cout << v.size() << endl;
    for(int i = 0; i < v.size(); i++)
        cout << v[i] << ",";
    cout << endl;
    v = allPalindromeSubstring("geeksforgeeks");
    cout << v.size() << endl;

    for(int i = 0; i < v.size(); i++)
        cout << v[i] << ",";
}

// This code is contributed by Arnab Kundu.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count number of ways we
// can get palindrome string from a given string
import java.util.ArrayList;
import java.util.List;

public class AllPalindromeSubstringsPossible {
    public static List<String> allPalindromeSubstring(String s)
    {
        List<String> list = new ArrayList<String>();

        // moving the pivot from starting till end of the string
        for (float pivot = 0; pivot < s.length(); pivot += .5) {

            // set radius to the first nearest element
            // on left and right
            float palindromeRadius = pivot - (int)pivot;

            // if the position needs to be compared has an element
            // and the characters at left and right matches
            while ((pivot + palindromeRadius) < s.length()
                   && (pivot - palindromeRadius) >= 0
                   && s.charAt((int)(pivot - palindromeRadius))
                          == s.charAt((int)(pivot + palindromeRadius))) {

                list.add(s.substring((int)(pivot - palindromeRadius),
                                     (int)(pivot + palindromeRadius + 1)));

                // increasing the radius by 1 to point to the
                // next elements in left and right
                palindromeRadius++;
            }
        }

        return list;
    }

    // Drivers code
    public static void main(String[] args)
    {
        List<String> list = allPalindromeSubstring("hellolle");
        System.out.println(list.size());
        System.out.println(list);
        list = allPalindromeSubstring("geeksforgeeks");
        System.out.println(list.size());
        System.out.println(list);
    }
}
```

## 蟒蛇 3

```
# Python3 program to Count number of ways we
# can get palindrome string from a given
# string

# function to find the substring of the
# string
def substring(s, a, b):
    s1 = ""

    # extract the specified position of
    # the string
    for i in range(a, b, 1):
        s1 += s[i]

    return s1

# can get palindrome string from a
# given string
def allPalindromeSubstring(s):
    v = []

    # moving the pivot from starting till
    # end of the string
    pivot = 0.0
    while pivot < len(s):

        # set radius to the first nearest
        # element on left and right
        palindromeRadius = pivot - int(pivot)

        # if the position needs to be
        # compared has an element and the
        # characters at left and right
        # matches
        while ((pivot + palindromeRadius) < len(s) and
                   (pivot - palindromeRadius) >= 0 and
                  (s[int(pivot - palindromeRadius)] ==
                   s[int(pivot + palindromeRadius)])):
             v.append(s[int(pivot - palindromeRadius):
                        int(pivot + palindromeRadius + 1)])

             # increasing the radius by 1 to point
             # to the next elements in left and right
             palindromeRadius += 1

        pivot += 0.5
    return v

# Driver Code
if __name__ == "__main__":
    v = allPalindromeSubstring("hellolle")
    print(len(v))
    print(v)

    v = allPalindromeSubstring("geeksforgeeks")
    print(len(v))
    print(v)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to Count number of ways we
// can get palindrome string from a given string
using System;
using System.Collections.Generic;

public class AllPalindromeSubstringsPossible
{
    public static List<String> allPalindromeSubstring(String s)
    {
        List<String> list = new List<String>();

        // moving the pivot from starting till end of the string
        for (float pivot = 0; pivot < s.Length; pivot+= (float).5)
        {

            // set radius to the first nearest element
            // on left and right
            float palindromeRadius = pivot - (int)pivot;

            // if the position needs to be compared has an element
            // and the characters at left and right matches
            while ((pivot + palindromeRadius) < s.Length
                && (pivot - palindromeRadius) >= 0
                && s[(int)(pivot - palindromeRadius)]
                        == s[(int)(pivot + palindromeRadius)])
            {

                list.Add(s.Substring((int)(pivot - palindromeRadius),
                            (int)(pivot + palindromeRadius + 1)-
                            (int)(pivot - palindromeRadius)));

                // increasing the radius by 1 to point to the
                // next elements in left and right
                palindromeRadius++;
            }
        }

        return list;
    }

    // Drivers code
    public static void Main(String[] args)
    {
        List<String> list = allPalindromeSubstring("hellolle");
        Console.WriteLine(list.Count);
        for(int i = 0; i < list.Count; i++)
            Console.Write(list[i]+",");
        list = allPalindromeSubstring("geeksforgeeks");
        Console.WriteLine("\n"+list.Count);
        for(int i = 0; i < list.Count; i++)
            Console.Write(list[i]+",");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to Count number of ways we
// can get palindrome string from a given string

function allPalindromeSubstring(s)
{
    let list = [];

        // moving the pivot from starting till end of the string
        for (let pivot = 0; pivot < s.length; pivot += .5) {

            // set radius to the first nearest element
            // on left and right
            let palindromeRadius = pivot - Math.floor(pivot);

            // if the position needs to be compared has an element
            // and the characters at left and right matches
            while ((pivot + palindromeRadius) < s.length
                   && (pivot - palindromeRadius) >= 0
                   && s[(Math.floor(pivot - palindromeRadius))]
                          == s[Math.floor(pivot + palindromeRadius)])
                          {

                list.push(s.substring(Math.floor(pivot -
                palindromeRadius),
                Math.floor(pivot + palindromeRadius + 1)));

                // increasing the radius by 1 to point to the
                // next elements in left and right
                palindromeRadius++;
            }
        }

        return list;
}

// Drivers code
let list = allPalindromeSubstring("hellolle");
document.write(list.length+"<br>");
document.write("["+list.join(", ")+"]<br>");
list = allPalindromeSubstring("geeksforgeeks");
document.write(list.length+"<br>");
document.write("["+list.join(", ")+"]<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
13
[h, e, l, ll, l, o, lol, lloll, ellolle, l, ll, l, e]
15
[g, e, ee, e, k, s, f, o, r, g, e, ee, e, k, s]
```

**注意:**要打印不同的子字符串，请使用 Set，因为它只接受不同的元素。