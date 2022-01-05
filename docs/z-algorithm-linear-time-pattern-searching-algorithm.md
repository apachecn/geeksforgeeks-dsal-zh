# Z 算法(线性时间模式搜索算法)

> 原文:[https://www . geesforgeks . org/z-算法-线性-时间-模式-搜索-算法/](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)

该算法在线性时间内查找文本中模式的所有出现。假设文本长度为 n，模式长度为 m，那么所用的总时间为 O(m + n)，空间复杂度为线性。现在我们可以看到时间和空间复杂度都和 KMP 算法一样，但是这个算法更容易理解。
在这个算法中，我们构造了一个 Z 数组。

**什么是 Z 阵？**
为字符串[0..n-1]，Z 数组与字符串长度相同。Z 数组的元素 Z[i]存储从字符串[i]开始的最长子串的长度，字符串[i]也是字符串[0]的前缀..n-1]。Z 数组的第一个条目意义不大，因为完整的字符串总是它自己的前缀。

```
Example:
Index            0   1   2   3   4   5   6   7   8   9  10  11 
Text             a   a   b   c   a   a   b   x   a   a   a   z
Z values         X   1   0   0   3   1   0   0   2   2   1   0 
```

```
More Examples:
str  = "aaaaaa"
Z[]  = {x, 5, 4, 3, 2, 1}

str = "aabaacd"
Z[] = {x, 1, 0, 2, 1, 0, 0}

str = "abababab"
Z[] = {x, 0, 6, 0, 4, 0, 2, 0}

```

**Z 数组如何在线性时间内帮助搜索模式？**
思路是将模式和文本串联起来，创建一个字符串“P$T”，其中 P 是模式，$是模式和文本中不应该出现的特殊字符，T 是文本。为串联字符串构建 Z 数组。在 Z 数组中，如果任意一点的 Z 值等于模式长度，则该点存在模式。

```
Example:
Pattern P = "aab",  Text T = "baabaa"

The concatenated string is = "aab$baabaa"

Z array for above concatenated string is {x, 1, 0, 0, 0, 
                                          3, 1, 0, 2, 1}.
Since length of pattern is 3, the value 3 in Z array 
indicates presence of pattern. 
```

**如何构造 Z 数组？**
一个简单的解决方案是运行两个嵌套循环，外部循环到达每个索引，内部循环找到与从当前索引开始的子串匹配的最长前缀的长度。这个解的时间复杂度为 O(n <sup>2</sup> )。
我们可以在线性时间内构建 Z 阵列。

```
The idea is to maintain an interval [L, R] which is the interval with max R
such that [L,R] is prefix substring (substring which is also prefix). 

Steps for maintaining this interval are as follows – 

1) If i > R then there is no prefix substring that starts before i and 
   ends after i, so we reset L and R and compute new [L,R] by comparing 
   str[0..] to str[i..] and get Z[i] (= R-L+1).

2) If i <= R then let K = i-L,  now Z[i] >= min(Z[K], R-i+1)  because 
   str[i..] matches with str[K..] for atleast R-i+1 characters (they are in
   [L,R] interval which we know is a prefix substring).     
   Now two sub cases arise – 
      a) If Z[K] < R-i+1  then there is no prefix substring starting at 
         str[i] (otherwise Z[K] would be larger)  so  Z[i] = Z[K]  and 
         interval [L,R] remains same.
      b) If Z[K] >= R-i+1 then it is possible to extend the [L,R] interval
         thus we will set L as i and start matching from str[R]  onwards  and
         get new R then we will update interval [L,R] and calculate Z[i] (=R-L+1).
```

为了更好地理解上述一步一步的过程，请查看此动画–[http://www.utdallas.edu/~besp/demo/John2010/z-algorithm.htm](http://www.utdallas.edu/~besp/demo/John2010/z-algorithm.htm)
该算法以线性时间运行，因为我们从不比较小于 R 的字符，并且通过匹配，我们将 R 增加 1，因此最多有 T 个比较。在不匹配情况下，每个 I 只发生一次不匹配(因为哪个 R 停止)，这是另一个最多 T 的比较，使整体线性复杂度。

下面是用于模式搜索的 Z 算法的实现。

## C++

```
// A C++ program that implements Z algorithm for pattern searching
#include<iostream>
using namespace std;

void getZarr(string str, int Z[]);

// prints all occurrences of pattern in text using Z algo
void search(string text, string pattern)
{
    // Create concatenated string "P$T"
    string concat = pattern + "{content}quot; + text;
    int l = concat.length();

    // Construct Z array
    int Z[l];
    getZarr(concat, Z);

    // now looping through Z array for matching condition
    for (int i = 0; i < l; ++i)
    {
        // if Z[i] (matched region) is equal to pattern
        // length we got the pattern
        if (Z[i] == pattern.length())
            cout << "Pattern found at index "
                << i - pattern.length() -1 << endl;
    }
}

// Fills Z array for given string str[]
void getZarr(string str, int Z[])
{
    int n = str.length();
    int L, R, k;

    // [L,R] make a window which matches with prefix of s
    L = R = 0;
    for (int i = 1; i < n; ++i)
    {
        // if i>R nothing matches so we will calculate.
        // Z[i] using naive way.
        if (i > R)
        {
            L = R = i;

            // R-L = 0 in starting, so it will start
            // checking from 0'th index. For example,
            // for "ababab" and i = 1, the value of R
            // remains 0 and Z[i] becomes 0\. For string
            // "aaaaaa" and i = 1, Z[i] and R become 5
            while (R<n && str[R-L] == str[R])
                R++;
            Z[i] = R-L;
            R--;
        }
        else
        {
            // k = i-L so k corresponds to number which
            // matches in [L,R] interval.
            k = i-L;

            // if Z[k] is less than remaining interval
            // then Z[i] will be equal to Z[k].
            // For example, str = "ababab", i = 3, R = 5
            // and L = 2
            if (Z[k] < R-i+1)
                Z[i] = Z[k];

            // For example str = "aaaaaa" and i = 2, R is 5,
            // L is 0
            else
            {
                // else start from R and check manually
                L = i;
                while (R<n && str[R-L] == str[R])
                    R++;
                Z[i] = R-L;
                R--;
            }
        }
    }
}

// Driver program
int main()
{
    string text = "GEEKS FOR GEEKS";
    string pattern = "GEEK";
    search(text, pattern);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program that implements Z algorithm for pattern
// searching
class GFG {

    //  prints all occurrences of pattern in text using
    // Z algo
    public static void search(String text, String pattern)
    {

        // Create concatenated string "P$T"
        String concat = pattern + "{content}quot; + text;

        int l = concat.length();

        int Z[] = new int[l];

        // Construct Z array
        getZarr(concat, Z);

        // now looping through Z array for matching condition
        for(int i = 0; i < l; ++i){

            // if Z[i] (matched region) is equal to pattern
            // length we got the pattern

            if(Z[i] == pattern.length()){
                System.out.println("Pattern found at index "
                              + (i - pattern.length() - 1));
            }
        }
    }

    // Fills Z array for given string str[]
    private static void getZarr(String str, int[] Z) {

        int n = str.length();

        // [L,R] make a window which matches with
        // prefix of s
        int L = 0, R = 0;

        for(int i = 1; i < n; ++i) {

            // if i>R nothing matches so we will calculate.
            // Z[i] using naive way.
            if(i > R){

                L = R = i;

                // R-L = 0 in starting, so it will start
                // checking from 0'th index. For example,
                // for "ababab" and i = 1, the value of R
                // remains 0 and Z[i] becomes 0\. For string
                // "aaaaaa" and i = 1, Z[i] and R become 5

                while(R < n && str.charAt(R - L) == str.charAt(R))
                    R++;

                Z[i] = R - L;
                R--;

            }
            else{

                // k = i-L so k corresponds to number which
                // matches in [L,R] interval.
                int k = i - L;

                // if Z[k] is less than remaining interval
                // then Z[i] will be equal to Z[k].
                // For example, str = "ababab", i = 3, R = 5
                // and L = 2
                if(Z[k] < R - i + 1)
                    Z[i] = Z[k];

                // For example str = "aaaaaa" and i = 2, R is 5,
                // L is 0
                else{

                // else start from R and check manually
                    L = i;
                    while(R < n && str.charAt(R - L) == str.charAt(R))
                        R++;

                    Z[i] = R - L;
                    R--;
                }
            }
        }
    }

    // Driver program
    public static void main(String[] args)
    {
        String text = "GEEKS FOR GEEKS";
        String pattern = "GEEK";

        search(text, pattern);
    }
}

// This code is contributed by PavanKoli.
```

## 蟒蛇 3

```
# Python3 program that implements Z algorithm
# for pattern searching

# Fills Z array for given string str[]
def getZarr(string, z):
    n = len(string)

    # [L,R] make a window which matches
    # with prefix of s
    l, r, k = 0, 0, 0
    for i in range(1, n):

        # if i>R nothing matches so we will calculate.
        # Z[i] using naive way.
        if i > r:
            l, r = i, i

            # R-L = 0 in starting, so it will start
            # checking from 0'th index. For example,
            # for "ababab" and i = 1, the value of R
            # remains 0 and Z[i] becomes 0\. For string
            # "aaaaaa" and i = 1, Z[i] and R become 5
            while r < n and string[r - l] == string[r]:
                r += 1
            z[i] = r - l
            r -= 1
        else:

            # k = i-L so k corresponds to number which
            # matches in [L,R] interval.
            k = i - l

            # if Z[k] is less than remaining interval
            # then Z[i] will be equal to Z[k].
            # For example, str = "ababab", i = 3, R = 5
            # and L = 2
            if z[k] < r - i + 1:
                z[i] = z[k]

            # For example str = "aaaaaa" and i = 2,
            # R is 5, L is 0
            else:

                # else start from R and check manually
                l = i
                while r < n and string[r - l] == string[r]:
                    r += 1
                z[i] = r - l
                r -= 1

# prints all occurrences of pattern
# in text using Z algo
def search(text, pattern):

    # Create concatenated string "P$T"
    concat = pattern + "{content}quot; + text
    l = len(concat)

    # Construct Z array
    z = [0] * l
    getZarr(concat, z)

    # now looping through Z array for matching condition
    for i in range(l):

        # if Z[i] (matched region) is equal to pattern
        # length we got the pattern
        if z[i] == len(pattern):
            print("Pattern found at index",
                      i - len(pattern) - 1)

# Driver Code
if __name__ == "__main__":
    text = "GEEKS FOR GEEKS"
    pattern = "GEEK"
    search(text, pattern)

# This code is contributed by
# sanjeev2552
```

## C#

```
// A C# program that implements Z
// algorithm for pattern searching
using System;

class GFG
{

// prints all occurrences of
// pattern in text using Z algo
public static void search(string text,
                          string pattern)
{

    // Create concatenated string "P$T"
    string concat = pattern + "{content}quot; + text;

    int l = concat.Length;

    int[] Z = new int[l];

    // Construct Z array
    getZarr(concat, Z);

    // now looping through Z array
    // for matching condition
    for (int i = 0; i < l; ++i)
    {

        // if Z[i] (matched region) is equal
        // to pattern length we got the pattern

        if (Z[i] == pattern.Length)
        {
            Console.WriteLine("Pattern found at index " +
                             (i - pattern.Length - 1));
        }
    }
}

// Fills Z array for given string str[]
private static void getZarr(string str,
                            int[] Z)
{

    int n = str.Length;

    // [L,R] make a window which
    // matches with prefix of s
    int L = 0, R = 0;

    for (int i = 1; i < n; ++i)
    {

        // if i>R nothing matches so we will
        // calculate. Z[i] using naive way.
        if (i > R)
        {
            L = R = i;

            // R-L = 0 in starting, so it will start
            // checking from 0'th index. For example,
            // for "ababab" and i = 1, the value of R
            // remains 0 and Z[i] becomes 0\. For string
            // "aaaaaa" and i = 1, Z[i] and R become 5
            while (R < n && str[R - L] == str[R])
            {
                R++;
            }

            Z[i] = R - L;
            R--;

        }
        else
        {

            // k = i-L so k corresponds to number
            // which matches in [L,R] interval.
            int k = i - L;

            // if Z[k] is less than remaining interval
            // then Z[i] will be equal to Z[k].
            // For example, str = "ababab", i = 3,
            // R = 5 and L = 2
            if (Z[k] < R - i + 1)
            {
                Z[i] = Z[k];
            }

            // For example str = "aaaaaa" and
            // i = 2, R is 5, L is 0
            else
            {

                // else start from R and
                // check manually
                L = i;
                while (R < n && str[R - L] == str[R])
                {
                    R++;
                }

                Z[i] = R - L;
                R--;
            }
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    string text = "GEEKS FOR GEEKS";
    string pattern = "GEEK";

    search(text, pattern);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// A JavaScript program that implements Z algorithm for pattern
// searching

//  prints all occurrences of pattern in text using
    // Z algo
function search(text,pattern)
{
    // Create concatenated string "P$T"
        let concat = pattern + "{content}quot; + text;

        let l = concat.length;

        let Z = new Array(l);

        // Construct Z array
        getZarr(concat, Z);

        // now looping through Z array for matching condition
        for(let i = 0; i < l; ++i){

            // if Z[i] (matched region) is equal to pattern
            // length we got the pattern

            if(Z[i] == pattern.length){
                document.write("Pattern found at index "
                              + (i - pattern.length - 1)+"<br>");
            }
        }
}

 // Fills Z array for given string str[]
function getZarr(str,Z)
{
    let n = str.length;

        // [L,R] make a window which matches with
        // prefix of s
        let L = 0, R = 0;

        for(let i = 1; i < n; ++i) {

            // if i>R nothing matches so we will calculate.
            // Z[i] using naive way.
            if(i > R){

                L = R = i;

                // R-L = 0 in starting, so it will start
                // checking from 0'th index. For example,
                // for "ababab" and i = 1, the value of R
                // remains 0 and Z[i] becomes 0\. For string
                // "aaaaaa" and i = 1, Z[i] and R become 5

                while(R < n && str[R - L] == str[R])
                    R++;

                Z[i] = R - L;
                R--;

            }
            else{

                // k = i-L so k corresponds to number which
                // matches in [L,R] interval.
                let k = i - L;

                // if Z[k] is less than remaining interval
                // then Z[i] will be equal to Z[k].
                // For example, str = "ababab", i = 3, R = 5
                // and L = 2
                if(Z[k] < R - i + 1)
                    Z[i] = Z[k];

                // For example str = "aaaaaa" and i = 2, R is 5,
                // L is 0
                else{

                // else start from R and check manually
                    L = i;
                    while(R < n && str[R - L] == str[R])
                        R++;

                    Z[i] = R - L;
                    R--;
                }
            }
        }
}

// Driver program
let text = "GEEKS FOR GEEKS";
let pattern = "GEEK";

search(text, pattern);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Pattern found at index 0
Pattern found at index 10
```

本文由 [**乌卡什·特里维迪**](https://www.linkedin.com/pub/utkarsh-trivedi/a7/69/253) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息