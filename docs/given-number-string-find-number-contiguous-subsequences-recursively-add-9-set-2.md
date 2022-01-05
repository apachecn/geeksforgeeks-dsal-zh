# 给定一个数字作为字符串，求递归加起来等于 9 的连续子序列的数目|集合 2

> 原文:[https://www . geesforgeks . org/给定-数字-字符串-查找-数字-连续-子序列-递归-添加-9-集合-2/](https://www.geeksforgeeks.org/given-number-string-find-number-contiguous-subsequences-recursively-add-9-set-2/)

给定一个数字作为字符串，编写一个函数来查找给定字符串的子字符串(或连续子序列)的数量，这些子字符串递归加起来等于 9。
例如 729 的数字递归加到 9，
7 + 2 + 9 = 18
递归 18
1+8 = 9
T5】示例:

```
Input: 4189
Output: 3
There are three substrings which recursively 
add to 9\. The substrings are 18, 9 and 189.

Input: 909
Output: 5
There are 5 substrings which recursively add 
to nine, 9, 90, 909, 09, 9
```

本文是关于下述问题的一个优化解决方案:
[给定一个数字作为字符串，求递归加起来等于 9 的连续子序列的个数|集合 1](https://www.geeksforgeeks.org/given-number-find-number-contiguous-subsequences-recursively-add-9/) 。
一个数的所有数字递归加起来等于 9，如果这个数是 9 的倍数。我们基本上需要检查所有子字符串的 s%9。下面程序中使用的一个技巧是进行模块化运算，以避免大字符串溢出。

算法:

```
Initialize an array d of size 10 with 0
d[0]<-1
Initialize mod_sum = 0, continuous_zero = 0
for every character
    if character == '0';
        continuous_zero++
    else
        continuous_zero=0
    compute mod_sum
    update result += d[mod_sum]
    update d[mod_sum]++
    subtract those cases from result which have only 0s
```

说明:
如果从索引 I 到 j 的数字总和加起来是 9，那么总和(0 到 i-1) =总和(0 到 j) (mod 9)。
我们只需要删除只包含零的案例。我们可以通过记住到这个字符的连续零的数量(以这个索引结束的这些情况的数量)并从结果中减去它们来做到这一点。
以下是基于这种方法的简单实现。
该实现假设输入的数字中有可以前导的 0。

## C++

```
// C++ program to count substrings with recursive sum equal to 9
#include <iostream>
#include <cstring>
using namespace std;

int count9s(char number[])
{
    int n = strlen(number);

    // to store no. of previous encountered modular sums
    int d[9];
    memset(d, 0, sizeof(d));

    // no. of modular sum(==0) encountered till now = 1
    d[0] = 1;
    int result = 0;

    int mod_sum = 0, continuous_zero = 0;
    for (int i = 0; i < n; i++) {
        if (!int(number[i] - '0')) // if number is 0 increase
            continuous_zero++;     // no. of continuous_zero by 1
        else                       // else continuous_zero is 0
            continuous_zero=0;
        mod_sum += int(number[i] - '0');
        mod_sum %= 9;
        result+=d[mod_sum];
        d[mod_sum]++;      // increase d value of this mod_sum
                          // subtract no. of cases where there
                          // are only zeroes in substring
        result -= continuous_zero;
    }
    return result;
}

// driver program to test above function
int main()
{
    cout << count9s("01809") << endl;
    cout << count9s("1809") << endl;
    cout << count9s("4189");
    return 0;
}
// This code is contributed by Gulab Arora
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count substrings with recursive sum equal to 9

class GFG {

    static int count9s(char number[]) {
        int n = number.length;

        // to store no. of previous encountered modular sums
        int d[] = new int[9];

        // no. of modular sum(==0) encountered till now = 1
        d[0] = 1;
        int result = 0;

        int mod_sum = 0, continuous_zero = 0;
        for (int i = 0; i < n; i++) {
            if ((number[i] - '0') == 0) // if number is 0 increase
            {
                continuous_zero++;     // no. of continuous_zero by 1
            } else // else continuous_zero is 0
            {
                continuous_zero = 0;
            }
            mod_sum += (number[i] - '0');
            mod_sum %= 9;
            result += d[mod_sum];
            d[mod_sum]++;  // increase d value of this mod_sum
                          // subtract no. of cases where there
                          // are only zeroes in substring
            result -= continuous_zero;
        }
        return result;
    }

// driver program to test above function
    public static void main(String[] args) {
        System.out.println(count9s("01809".toCharArray()));
        System.out.println(count9s("1809".toCharArray()));
        System.out.println(count9s("4189".toCharArray()));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count substrings with
# recursive sum equal to 9

def count9s(number):
    n = len(number)

    # to store no. of previous encountered
    # modular sums
    d = [0 for i in range(9)]

    # no. of modular sum(==0) encountered
    # till now = 1
    d[0] = 1
    result = 0

    mod_sum = 0
    continuous_zero = 0
    for i in range(n):

        # if number is 0 increase
        if (ord(number[i]) - ord('0') == 0):
            continuous_zero += 1 # no. of continuous_zero by 1
        else:
            continuous_zero = 0 # else continuous_zero is 0

        mod_sum += ord(number[i]) - ord('0')
        mod_sum %= 9
        result += d[mod_sum]
        d[mod_sum] += 1     # increase d value of this mod_sum
                         # subtract no. of cases where there
                         # are only zeroes in substring
        result -= continuous_zero

    return result

# Driver Code
if __name__ == '__main__':
    print(count9s("01809"))
    print(count9s("1809"))
    print(count9s("4189"))

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to count substrings with recursive sum equal to 9

using System;

class GFG {

    static int count9s(string number) {
        int n = number.Length;

        // to store no. of previous encountered modular sums
        int[] d = new int[9];

        // no. of modular sum(==0) encountered till now = 1
        d[0] = 1;
        int result = 0;

        int mod_sum = 0, continuous_zero = 0;
        for (int i = 0; i < n; i++) {
            if ((number[i] - '0') == 0) // if number is 0 increase
            {
                continuous_zero++;     // no. of continuous_zero by 1
            } else // else continuous_zero is 0
            {
                continuous_zero = 0;
            }
            mod_sum += (number[i] - '0');
            mod_sum %= 9;
            result += d[mod_sum];
            d[mod_sum]++;  // increase d value of this mod_sum
                          // subtract no. of cases where there
                          // are only zeroes in substring
            result -= continuous_zero;
        }
        return result;
    }

// driver program to test above function
    public static void Main() {
        Console.WriteLine(count9s("01809"));
        Console.WriteLine(count9s("1809"));
        Console.WriteLine(count9s("4189"));
    }
}
```

## java 描述语言

```
<script>
// Javascript program to count substrings with recursive sum equal to 9

    function count9s(number)
    {
        let n = number.length;

        // to store no. of previous encountered modular sums
        let d = new Array(9);
        for(let i=0;i<d.length;i++)
        {
            d[i]=0;
        }

        // no. of modular sum(==0) encountered till now = 1
        d[0] = 1;
        let result = 0;

        let mod_sum = 0, continuous_zero = 0;
        for (let i = 0; i < n; i++) {
            if ((number[i] - '0') == 0) // if number is 0 increase
            {
                continuous_zero++;     // no. of continuous_zero by 1
            } else // else continuous_zero is 0
            {
                continuous_zero = 0;
            }
            mod_sum += (number[i] - '0');
            mod_sum %= 9;
            result += d[mod_sum];
            d[mod_sum]++;  // increase d value of this mod_sum
                          // subtract no. of cases where there
                          // are only zeroes in substring
            result -= continuous_zero;
        }
        return result;
    }

    // driver program to test above function
    document.write(count9s("01809")+"<br>");
    document.write(count9s("1809")+"<br>");
    document.write(count9s("4189")+"<br>");

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
8
5
3
```

上述程序的时间复杂度为 0(n)。程序也支持前导零。
本文由**古拉·阿罗拉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。