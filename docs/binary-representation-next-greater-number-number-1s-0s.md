# 具有相同 1 和 0 个数的下一个更大数字的二进制表示

> 原文:[https://www . geesforgeks . org/binary-presentation-next-greater-number-1s-0s/](https://www.geeksforgeeks.org/binary-representation-next-greater-number-number-1s-0s/)

给定一个代表正数 n 的二进制表示的二进制输入，找到大于 n 的最小数的二进制表示，其 1 和 0 的个数与 n 的二进制表示相同。如果不能形成这样的数，则打印“不大于”。
二进制输入可能适合也可能不适合无符号长整型。

示例:

```
Input : 10010
Output : 10100
Here n = (18)10 = (10010)2
next greater = (20)10 = (10100)2
Binary representation of 20 contains same number of
1's and 0's as in 18.

Input : 111000011100111110
Output :  111000011101001111

```

这个问题简单地归结为寻找给定字符串的下一个排列。我们可以找到输入二进制数的[next _ arrangement()](https://www.geeksforgeeks.org/find-the-next-lexicographically-greater-word-than-a-given-word/)。

下面是一个在二进制字符串中寻找下一个置换的算法。

1.  从右侧遍历二进制字符串 **bstr** 。
2.  遍历时，找到第一个索引 **i** ，使 bstr[I]= 0，bstr[I+1]= 1。
3.  at 索引“I”和“i+1”的交换字符。
4.  因为我们需要最小的下一个值，所以考虑从索引 **i+2** 到结束的子串，并最终移动子串中所有 **1 的**。

下面是以上步骤的实现。

## C++

```
// C++ program to find next permutation in a
// binary string.
#include <bits/stdc++.h>
using namespace std;

// Function to find the next greater number
// with same number of 1's and 0's
string nextGreaterWithSameDigits(string bnum)
{
    int l = bnum.size();
    int i;
    for (int i=l-2; i>=1; i--)
    {
        // locate first 'i' from end such that
        // bnum[i]=='0' and bnum[i+1]=='1'
        // swap these value and break;
        if (bnum.at(i) == '0' &&
           bnum.at(i+1) == '1')
        {
            char ch = bnum.at(i);
            bnum.at(i) = bnum.at(i+1);
            bnum.at(i+1) = ch;
            break;
        }
    }

    // if no swapping performed
    if (i == 0)
        "no greater number";

    // Since we want the smallest next value,
    // shift all 1's at the end in the binary
    // substring starting from index 'i+2'
    int j = i+2, k = l-1;
    while (j < k)
    {
        if (bnum.at(j) == '1' && bnum.at(k) == '0')
        {
            char ch = bnum.at(j);
            bnum.at(j) = bnum.at(k);
            bnum.at(k) = ch;
            j++;
            k--;
        }

        // special case while swapping if '0'
        // occurs then break
        else if (bnum.at(i) == '0')
            break;

        else
            j++;

    }

    // required next greater number
    return bnum;
}

// Driver program to test above
int main()
{
    string bnum = "10010";
    cout << "Binary representation of next greater number = "
         << nextGreaterWithSameDigits(bnum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next permutation in a
// binary string.
class GFG
{

// Function to find the next greater number
// with same number of 1's and 0's
static String nextGreaterWithSameDigits(char[] bnum)
{
    int l = bnum.length;
    int i;
    for (i = l - 2; i >= 1; i--)
    {
        // locate first 'i' from end such that
        // bnum[i]=='0' and bnum[i+1]=='1'
        // swap these value and break;
        if (bnum[i] == '0' &&
        bnum[i+1] == '1')
        {
            char ch = bnum[i];
            bnum[i] = bnum[i+1];
            bnum[i+1] = ch;
            break;
        }
    }

    // if no swapping performed
    if (i == 0)
        System.out.println("no greater number");

    // Since we want the smallest next value,
    // shift all 1's at the end in the binary
    // substring starting from index 'i+2'
    int j = i + 2, k = l - 1;
    while (j < k)
    {
        if (bnum[j] == '1' && bnum[k] == '0')
        {
            char ch = bnum[j];
            bnum[j] = bnum[k];
            bnum[k] = ch;
            j++;
            k--;
        }

        // special case while swapping if '0'
        // occurs then break
        else if (bnum[i] == '0')
            break;

        else
            j++;

    }

    // required next greater number
    return String.valueOf(bnum);
}

// Driver program to test above
public static void main(String[] args)
{
    char[] bnum = "10010".toCharArray();
    System.out.println("Binary representation of next greater number = "
        + nextGreaterWithSameDigits(bnum));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find next permutation in a
# binary string.

# Function to find the next greater number
# with same number of 1's and 0's
def nextGreaterWithSameDigits(bnum):
    l = len(bnum)
    bnum = list(bnum)
    for i in range(l - 2, 0, -1):

        # locate first 'i' from end such that
        # bnum[i]=='0' and bnum[i+1]=='1'
        # swap these value and break
        if (bnum[i] == '0' and bnum[i + 1] == '1'):
            ch = bnum[i]
            bnum[i] = bnum[i + 1]
            bnum[i + 1] = ch        
            break

    # if no swapping performed
    if (i == 0):
        return "no greater number"

    # Since we want the smallest next value,
    # shift all 1's at the end in the binary
    # substring starting from index 'i+2'
    j = i + 2
    k = l - 1
    while (j < k):
        if (bnum[j] == '1' and bnum[k] == '0'):
            ch = bnum[j]
            bnum[j] = bnum[k]
            bnum[k] = ch
            j += 1
            k -= 1

        # special case while swapping if '0'
        # occurs then break
        elif (bnum[i] == '0'):
            break
        else:
            j += 1

    # required next greater number
    return bnum

# Driver code
bnum = "10010"
print("Binary representation of next greater number = ",*nextGreaterWithSameDigits(bnum),sep="")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find next permutation in a
// binary string.
using System;

class GFG
{

// Function to find the next greater number
// with same number of 1's and 0's
static String nextGreaterWithSameDigits(char[] bnum)
{
    int l = bnum.Length;
    int i;
    for (i = l - 2; i >= 1; i--)
    {
        // locate first 'i' from end such that
        // bnum[i]=='0' and bnum[i+1]=='1'
        // swap these value and break;
        if (bnum[i] == '0' &&
        bnum[i+1] == '1')
        {
            char ch = bnum[i];
            bnum[i] = bnum[i+1];
            bnum[i+1] = ch;
            break;
        }
    }

    // if no swapping performed
    if (i == 0)
        Console.WriteLine("no greater number");

    // Since we want the smallest next value,
    // shift all 1's at the end in the binary
    // substring starting from index 'i+2'
    int j = i + 2, k = l - 1;
    while (j < k)
    {
        if (bnum[j] == '1' && bnum[k] == '0')
        {
            char ch = bnum[j];
            bnum[j] = bnum[k];
            bnum[k] = ch;
            j++;
            k--;
        }

        // special case while swapping if '0'
        // occurs then break
        else if (bnum[i] == '0')
            break;

        else
            j++;

    }

    // required next greater number
    return String.Join("",bnum);
}

// Driver code
public static void Main(String[] args)
{
    char[] bnum = "10010".ToCharArray();
    Console.WriteLine("Binary representation of next greater number = "
        + nextGreaterWithSameDigits(bnum));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find next permutation
// in a binary string.

// Function to find the next greater number
// with same number of 1's and 0's
function nextGreaterWithSameDigits(bnum)
{
    let l = bnum.length;
    let i;

    for(i = l - 2; i >= 1; i--)
    {

        // Locate first 'i' from end such that
        // bnum[i]=='0' and bnum[i+1]=='1'
        // swap these value and break;
        if (bnum[i] == '0' &&
            bnum[i + 1] == '1')
        {
            let ch = bnum[i];
            bnum[i] = bnum[i+1];
            bnum[i+1] = ch;
            break;
        }
    }

    // If no swapping performed
    if (i == 0)
        document.write("no greater number<br>");

    // Since we want the smallest next value,
    // shift all 1's at the end in the binary
    // substring starting from index 'i+2'
    let j = i + 2, k = l - 1;
    while (j < k)
    {
        if (bnum[j] == '1' && bnum[k] == '0')
        {
            let ch = bnum[j];
            bnum[j] = bnum[k];
            bnum[k] = ch;
            j++;
            k--;
        }

        // Special case while swapping if '0'
        // occurs then break
        else if (bnum[i] == '0')
            break;
        else
            j++;
    }

    // Required next greater number
    return (bnum).join("");
}

// Driver code
let bnum = "10010".split("");
document.write("Binary representation of next " +
               "greater number = " +
               nextGreaterWithSameDigits(bnum));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Binary representation of next greater number = 10100
```

**时间复杂度:** O(n)，其中 n 为输入的位数。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。