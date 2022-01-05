# 删除给定数字中的重复数字

> 原文:[https://www . geesforgeks . org/remove-给定数字中的重复数字/](https://www.geeksforgeeks.org/remove-recurring-digits-in-a-given-number/)

给定一个数字作为字符串，从给定的字符串中删除重复出现的数字。这些改变必须就地进行。预期时间复杂度 O(n)和辅助空间 O(1)。
示例:

```
Input:  num[] = "1299888833"
Output: num[] = "12983"

Input:  num[] = "1299888833222"
Output: num[] = "129832"
```

**强烈建议你尽量减少浏览器，先自己试试这个**
这个问题类似于[游程编码](https://www.geeksforgeeks.org/run-length-encoding/)。

```
Let num[] be input number represented as character array

1) Initialize index of modified string 'j' as 0\. 
2) Traverse input string and do following for every digit num[i].
   a) Copy current character 'num[i]' to 'num[j]' and increment i & j.
   b) Keep incrementing i while num[i] is same as previous digit.
3) Add string termination character at 'num[j]'
```

下面是上述算法的实现。

## C++

```
// C++ program to remove recurring digits from
// a given number
#include <bits/stdc++.h>
using namespace std;

/* Removes recurring digits in num[]  */
void removeRecurringDigits(char num[])
{
    int len = strlen(num);

    int j = 0; // Index in modified string

    /* Traverse digits of given number one by one */
    for (int i=0; i<len; i++)
    {
        /* Copy the first occurrence of new digit */
        num[j++] = num[i];

        /* Remove repeating occurrences of digit */
        while (i + 1 < len && num[i] == num[i+1])
            i++;
    }

    /* terminate the modified string */
   num[j] = '\0';
}

/* Driver program to test above function */
int main()
{
    char num[] = "1299888833";
    removeRecurringDigits(num);
    cout << "Modified number is " << num;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove recurring
// digits from a given number
class GFG
{

    /* Removes recurring digits in num[] */
    static String removeRecurringDigits(char num[])
    {
        int len = num.length;

        int j = 0; // Index in modified string
        String s = "";

        /* Traverse digits of given number one by one */
        for (int i = 0; i < len; i++)
        {

            /* Copy the first occurrence of new digit */
            s += String.valueOf(num[i]);

            /* Remove repeating occurrences of digit */
            while (i + 1 < len && num[i] == num[i + 1])
            {
                i++;
            }
        }
        return s;
    }

    /* Driver code */
    public static void main(String[] args)
    {
        char num[] = "1299888833".toCharArray();
        System.out.print("Modified number is " +
                        removeRecurringDigits(num));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to remove recurring
# digits from a given number

# Removes recurring digits in num[]
def removeRecurringDigits(num):

    l = len(num)

    # Index in modified string
    (i, j) = (0, 0)
    str = ''

    # Traverse digits of given
    # number one by one
    while i < l:

        # Copy the first occurrence
        # of new digit
        str += num[i]
        j += 1

        # Remove repeating occurrences of digit
        while (i + 1 < l and num[i] == num[i + 1]):
            i += 1
        i += 1

    return str

# Driver code
if __name__ == '__main__':

    num = '1299888833'
    print('Modified number is {}'.format(
           removeRecurringDigits(num)))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to remove recurring
// digits from a given number
using System;

class GFG
{

    /* Removes recurring digits in num[] */
    static String removeRecurringDigits(char []num)
    {
        int len = num.Length;

        int j = 0; // Index in modified string
        String s = "";

        /* Traverse digits of given number one by one */
        for (int i = 0; i < len; i++)
        {

            /* Copy the first occurrence of new digit */
            s += String.Join("",num[i]);

            /* Remove repeating occurrences of digit */
            while (i + 1 < len && num[i] == num[i + 1])
            {
                i++;
            }
        }
        return s;
    }

    /* Driver code */
    public static void Main()
    {
        char []num = "1299888833".ToCharArray();
        Console.Write("Modified number is " +
                        removeRecurringDigits(num));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to remove recurring
// digits from a given number

 /* Removes recurring digits in num[] */
function removeRecurringDigits(num)
{
    let len = num.length;

        let j = 0; // Index in modified string
        let s = "";

        /* Traverse digits of given number one by one */
        for (let i = 0; i < len; i++)
        {

            /* Copy the first occurrence of new digit */
            s += (num[i]);

            /* Remove repeating occurrences of digit */
            while (i + 1 < len && num[i] == num[i + 1])
            {
                i++;
            }
        }
        return s;
}

/* Driver code */
let num="1299888833".split("");
document.write("Modified number is " +
                        removeRecurringDigits(num));

// This code is contributed by rag2127
</script>
```

**输出:**

```
Modified number is 12983
```

本文由普里扬卡供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息