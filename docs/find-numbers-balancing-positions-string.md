# 找出串中平衡位置的数量

> 原文:[https://www . geesforgeks . org/find-numbers-balancing-positions-string/](https://www.geeksforgeeks.org/find-numbers-balancing-positions-string/)

给定一个字符串，任务是从该字符串的左部分和右部分包含相同字符的位置找到字符串中这种平衡位置的数量。人物出现的频率不重要。

**示例:**

```
Input : str[] = abaaba
Output : Number of balancing positions : 3
Explanations : All 3 balancing positions are as :
ab|aaba, aba|aba, abaa|ba

Input : str[] = noon
Output : Number of balancing positions : 1
Explanations : Balancing position is :
no|on
```

**朴素方法:**如果我们试图用朴素方法解决这个问题，我们必须对字符串的所有 n 个位置进行处理，并且在每个位置，我们必须检查来自那个位置的字符串的左右部分是否具有相同的字符。
寻找位置是否平衡的过程(两个部分的频率不需要相同)可以在 O(n^2 时间为单个位置完成(在这里我们应该检查左边部分的每个元素是否出现在右边，反之亦然)。整个过程将产生一个时间复杂度为 O(n^3).的算法
**高效方法:**高效算法的想法来自于本文。主要区别是我们不应该关心等频率，而使用遍历字符串。
我们首先用所有字符的计数填充右侧[]。然后我们从左向右遍历字符串。对于每个字符，我们在左[]增加其计数，在右[]减少计数。对于任何被遍历的点，如果所有在左边有非零值的字符在右边也有非零值，反之亦然，那么我们增加结果。

## C++

```
// C++ program to find number of balancing
// points in string
#include<bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 256;

// function to return number of balancing points
int countBalance(char *str)
{
    int n = strlen(str); // string length

    // hash array for storing hash of string
    // initialized by 0 being global
    int leftVisited[MAX_CHAR] = {0};
    int rightVisited[MAX_CHAR] = {0};

    // process string initially for rightVisited
    for (int i=0; i<n; i++)
        rightVisited[str[i]]++;

    // check for balancing points
    int res = 0;
    for (int i=0; i<n; i++)
    {
        // for every position inc left hash
        // & dec rightVisited
        leftVisited[str[i]]++;
        rightVisited[str[i]]--;

        // check whether  both hash have same
        // character or not
        int j;
        for (j=0; j<MAX_CHAR; j++)
        {
            // Either both leftVisited[j] and
            // rightVisited[j] should have none
            // zero value or both should have
            // zero value
            if ( (leftVisited[j] == 0 &&
                   rightVisited[j] != 0) ||
                 (leftVisited[j] != 0 &&
                  rightVisited[j] == 0)
               )
                break;
        }

        // if both have same character increment
        // count
        if (j == MAX_CHAR)
            res++;
    }
    return res;
}

//driver program
int main()
{
    char str[] = "abaababa";
    cout << countBalance(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of balancing
// points in string

class GFG
{
    static final int MAX_CHAR = 256;

    // method to return number of balancing points
    static int countBalance(String s)
    {
        char[] str=s.toCharArray();
        int n = str.length; // string length

        // hash array for storing hash of string
        // initialized by 0 being global
        int[] rightVisited = new int[MAX_CHAR];
        int[] leftVisited = new int[MAX_CHAR];

        // process string initially for rightVisited
        for (int i=0; i<n; i++)
            rightVisited[str[i]]++;

        // check for balancing points
        int res = 0;
        for (int i=0; i<n; i++)
        {
            // for every position inc left hash
            // & dec rightVisited
            leftVisited[str[i]]++;
            rightVisited[str[i]]--;

            // check whether both hash have same
            // character or not
            int j;
            for (j=0; j<MAX_CHAR; j++)
            {
                // Either both leftVisited[j] and
                // rightVisited[j] should have none
                // zero value or both should have
                // zero value
                if ( (leftVisited[j] == 0 &&
                    rightVisited[j] != 0) ||
                    (leftVisited[j] != 0 &&
                    rightVisited[j] == 0)
                )
                    break;
            }

            // if both have same character increment
            // count
            if (j == MAX_CHAR)
                res++;
        }
        return res;
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "abaababa";
        System.out.println(countBalance(str));
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python3 program to find number of
# balancing points in string
MAX_CHAR = 256

# function to return number of
# balancing points
def countBalance(string):

    n = len(string) # string length

    # hash array for storing hash of
    # string initialized by 0 being global
    leftVisited = [0] * (MAX_CHAR)
    rightVisited = [0] * (MAX_CHAR)

    # process string initially for
    # rightVisited
    for i in range(0, n):
        rightVisited[ord(string[i])] += 1

    # check for balancing points
    res = 0
    for i in range(0, n):

        # for every position inc left
        # hash & dec rightVisited
        leftVisited[ord(string[i])] += 1
        rightVisited[ord(string[i])] -= 1

        # check whether both hash have
        # same character or not
        j = 0
        while j < MAX_CHAR:

            # Either both leftVisited[j] and
            # rightVisited[j] should have none
            # zero value or both should have
            # zero value
            if ((leftVisited[j] == 0 and
                 rightVisited[j] != 0) or
                (leftVisited[j] != 0 and
                 rightVisited[j] == 0)):
                break

            j += 1

        # if both have same character
        # increment count
        if j == MAX_CHAR:
            res += 1

    return res

# Driver Code
if __name__ == "__main__":

    string = "abaababa"
    print(countBalance(string))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find number of
// balancing points in string
using System;

class GFG
{
    static int MAX_CHAR = 256;

    // method to return number of
    // balancing points
    static int countBalance(string s)
    {
        //char[] str=s.toCharArray();
        int n = s.Length; // string length

        // hash array for storing hash of string
        // initialized by 0 being global
        int[] rightVisited = new int[MAX_CHAR];
        int[] leftVisited = new int[MAX_CHAR];

        // process string initially for rightVisited
        for (int i = 0; i < n; i++)
            rightVisited[s[i]]++;

        // check for balancing points
        int res = 0;
        for (int i = 0; i < n; i++)
        {
            // for every position inc left
            // hash & dec rightVisited
            leftVisited[s[i]]++;
            rightVisited[s[i]]--;

            // check whether both hash have
            // same character or not
            int j;
            for (j = 0; j < MAX_CHAR; j++)
            {
                // Either both leftVisited[j] and
                // rightVisited[j] should have none
                // zero value or both should have
                // zero value
                if ((leftVisited[j] == 0 &&
                    rightVisited[j] != 0) ||
                    (leftVisited[j] != 0 &&
                    rightVisited[j] == 0))

                    break;
            }

            // if both have same character
            // increment count
            if (j == MAX_CHAR)
                res++;
        }
        return res;
    }

    // Driver Code
    public static void Main(String []args)
    {
        string str = "abaababa";
        Console.WriteLine(countBalance(str));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of balancing
// points in string

$MAX_CHAR = 256;

// function to return number of balancing points
function countBalance($str)
{
    global $MAX_CHAR;
    $n = strlen($str); // string length

    // hash array for storing hash of string
    // initialized by 0 being global
    $leftVisited = array_fill(0, $MAX_CHAR, NULL);
    $rightVisited = array_fill(0, $MAX_CHAR, NULL);

    // process string initially for rightVisited
    for ($i = 0; $i < $n; $i++)
        $rightVisited[ord($str[$i])]++;

    // check for balancing points
    $res = 0;
    for ($i = 0; $i < $n; $i++)
    {
        // for every position inc left hash
        // & dec rightVisited
        $leftVisited[ord($str[$i])]++;
        $rightVisited[ord($str[$i])]--;

        // check whether both hash have same
        // character or not
        for ($j = 0; $j < $MAX_CHAR; $j++)
        {
            // Either both leftVisited[j] and
            // rightVisited[j] should have none
            // zero value or both should have
            // zero value
            if (($leftVisited[$j] == 0 &&
                 $rightVisited[$j] != 0) ||
                ($leftVisited[$j] != 0 &&
                 $rightVisited[$j] == 0)
            )
                break;
        }

        // if both have same character
        // increment count
        if ($j == $MAX_CHAR)
            $res++;
    }
    return $res;
}

// Driver Code
$str = "abaababa";
echo countBalance($str);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of balancing
// points in string
var MAX_CHAR = 256;

// function to return number of balancing points
function countBalance(str)
{
    var n = str.length; // string length

    // hash array for storing hash of string
    // initialized by 0 being global
    var leftVisited = Array(MAX_CHAR).fill(0);
    var rightVisited = Array(MAX_CHAR).fill(0);

    // process string initially for rightVisited
    for (var i=0; i<n; i++)
        rightVisited[str[i].charCodeAt(0)]++;

    // check for balancing points
    var res = 0;
    for (var i=0; i<n; i++)
    {
        // for every position inc left hash
        // & dec rightVisited
        leftVisited[str[i].charCodeAt(0)]++;
        rightVisited[str[i].charCodeAt(0)]--;

        // check whether  both hash have same
        // character or not
        var j;
        for (j=0; j<MAX_CHAR; j++)
        {
            // Either both leftVisited[j] and
            // rightVisited[j] should have none
            // zero value or both should have
            // zero value
            if ( (leftVisited[j] == 0 &&
                   rightVisited[j] != 0) ||
                 (leftVisited[j] != 0 &&
                  rightVisited[j] == 0)
               )
                break;
        }

        // if both have same character increment
        // count
        if (j == MAX_CHAR)
            res++;
    }
    return res;
}

//driver program
var str = "abaababa";
document.write( countBalance(str));

</script>
```

**输出:**

```
5
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。