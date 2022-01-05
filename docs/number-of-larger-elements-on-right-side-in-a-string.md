# 字符串右侧较大元素的数量

> 原文:[https://www . geesforgeks . org/字符串右侧较大元素的数量/](https://www.geeksforgeeks.org/number-of-larger-elements-on-right-side-in-a-string/)

给定一个字符串，计算字符串中每个字符的大字母数。
**例:**

```
Input  : str = "abcd"
Output : 3 2 1 0
There are 3 greater characters on right of 'a',
2 greater characters on right of 'b', 1 greater
character on right of 'c' and 0 greater characters
on right of 'd'.

Input :  geeks
Output : 2 2 2 1 0
```

一种天真的方法是使用两个循环。第一个循环将跟踪字符串中的每个字母，第二个循环将用于根据 ASCII 值查找更大的字母。

## C++

```
// CPP program to find counts of right greater
// characters for every character.
#include <bits/stdc++.h>
using namespace std;

void printGreaterCount(string str)
{
    int len = str.length(), right[len] = { 0 };
    for (int i = 0; i < len; i++)
        for (int j = i + 1; j < len; j++)
            if (str[i] < str[j])
                right[i]++;

    for (int i = 0; i < len; i++)
        cout << right[i] << " ";
}

// Driver code
int main()
{
    string str = "abcd";
    printGreaterCount(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find counts of right greater
// characters for every character.
class GFG {

    static void printGreaterCount(String str)
    {
        int len = str.length(), right[] = new int[len];
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                if (str.charAt(i) < str.charAt(j)) {
                    right[i]++;
                }
            }
        }

        for (int i = 0; i < len; i++) {
            System.out.print(right[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abcd";
        printGreaterCount(str);
    }
}
// This code is contributed Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find counts of right
# greater characters for every character.

def printGreaterCount(str):
    len__ = len(str)
    right = [0 for i in range(len__)]
    for i in range(len__):
        for j in range(i + 1, len__, 1):
            if (str[i] < str[j]):
                right[i] += 1

    for i in range(len__):
        print(right[i], end = " ")

# Driver code
if __name__ == '__main__':
    str = "abcd"
    printGreaterCount(str)

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to find counts of right greater
// characters for every character.
using System;
public class GFG {

    static void printGreaterCount(String str)
    {
        int len = str.Length;
        int[] right = new int[len];
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                if (str[i] < str[j]) {
                    right[i]++;
                }
            }
        }

        for (int i = 0; i < len; i++) {
            Console.Write(right[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        String str = "abcd";
        printGreaterCount(str);
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find counts
// of right greater characters
// for every character.

function printGreaterCount($str)
{
    $len = strlen($str);
    $right = array_fill(0, $len, 0);
    for ($i = 0; $i < $len; $i++)
    {
        for ($j = $i + 1; $j < $len; $j++)
            if ($str[$i] < $str[$j])
                $right[$i]++;
    }

    for ($i = 0; $i < $len; $i++)
        echo $right[$i] . " ";
}

// Driver code
$str = 'abcd';
printGreaterCount($str);

// This code is contributed
// by Abhinav96
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // counts of right greater
    // characters for every character.

    function printGreaterCount(str)
    {
        let len = str.length;
        let right = new Array(len);
        right.fill(0);
        for (let i = 0; i < len; i++) {
            for (let j = i + 1; j < len; j++) {
                if (str[i].charCodeAt() < str[j].charCodeAt())
                {
                    right[i]++;
                }
            }
        }

        for (let i = 0; i < len; i++) {
            document.write(right[i] + " ");
        }
    }

    let str = "abcd";
      printGreaterCount(str);

</script>
```

**Output:** 

```
3 2 1 0
```