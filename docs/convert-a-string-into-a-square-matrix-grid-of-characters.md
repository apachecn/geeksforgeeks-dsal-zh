# 将字符串转换为字符的方形矩阵网格

> 原文:[https://www . geesforgeks . org/convert-a-string-to-a-square-matrix-grid-of-characters/](https://www.geeksforgeeks.org/convert-a-string-into-a-square-matrix-grid-of-characters/)

给定长度为 l 的字符串，任务是将字符串转换为网格。
**例:**

```
Input : str = "haveaniceday"
Output :  have
          anic
          eday    

Explanation: k is the separator. If k is 4 then the output will be "have
          anic
          eday"

Input :str = "geeksforgeeks"
Output : geek
         sfor
         geek
         s
```

**注:** & l =弦长

**进场:**

1.  不使用内置函数
2.  制作(行*列)大小的 2d 字符数组。
3.  分配值 K，它是一个列值。
4.  打印 2d 字符数组。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to string into grid form
void gridStr(string str)
{
    int l = str.length();
    int k = 0, row, column;
    row = floor(sqrt(l));
    column = ceil(sqrt(l));

    if (row * column < l)
        row = column;

    char s[row][column];
    // convert the string into grid
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < column; j++) {
            s[i][j] = str[k];
            k++;
        }
    }

    // Printing the grid
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < column; j++) {
            if (s[i][j] == '\0')
                break;
            cout << s[i][j];
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    string str = "GEEKSFORGEEKS";
    gridStr(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG
{

    // Function to string into grid form
    static void gridStr(String str)
    {
        int l = str.length();
        int k = 0, row, column;
        row = (int) Math.floor(Math.sqrt(l));
        column = (int) Math.ceil(Math.sqrt(l));

        if (row * column < l)
        {
            row = column;
        }

        char s[][] = new char[row][column];

        // convert the string into grid
        for (int i = 0; i < row; i++)
        {
            for (int j = 0; j < column; j++)
            {
                if(k < str.length())
                    s[i][j] = str.charAt(k);
                k++;
            }
        }

        // Printing the grid
        for (int i = 0; i < row; i++)
        {
            for (int j = 0; j < column; j++)
            {
                if (s[i][j] == 0)
                {
                    break;
                }
                System.out.print(s[i][j]);
            }
            System.out.println("");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "GEEKSFORGEEKS";
        gridStr(str);
    }
}

//This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to string into grid form
def function(str, k):

    for i in range(len(str)):
        if i %k == 0:
            sub = str[i:i+k]
            lst = []
            for j in sub:
                lst.append(j)
            print(' '.join(lst))

function("GEEKSFORGEEKS", 5)

/* This code contributed by nsew1999gokulcvan */
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

    // Function to string into grid form
    static void gridStr(String str)
    {
        int l = str.Length;
        int k = 0, row, column;
        row = (int) Math.Floor(Math.Sqrt(l));
        column = (int) Math.Ceiling(Math.Sqrt(l));

        if (row * column < l)
        {
            row = column;
        }

        char [,]s = new char[row,column];

        // convert the string into grid
        for (int i = 0; i < row; i++)
        {
            for (int j = 0; j < column; j++)
            {
                if(k < str.Length)
                    s[i,j] = str[k];
                k++;
            }
        }

        // Printing the grid
        for (int i = 0; i < row; i++)
        {
            for (int j = 0; j < column; j++)
            {
                if (s[i, j] == 0)
                {
                    break;
                }
                Console.Write(s[i, j]);
            }
            Console.WriteLine("");
        }
    }

    // Driver code
    public static void Main()
    {
        String str = "GEEKSFORGEEKS";
        gridStr(str);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to string into grid form
function gridStr($str)
{
    $l = strlen($str);
    $k = 0;
    $row = floor(sqrt($l));
    $column = ceil(sqrt($l));

    if ($row * $column < $l)
        $row = $column;

    $s = array_fill(0, $row,
         array_fill(0, $column, ""));
    // convert the string into grid
    for ($i = 0; $i < $row; $i++)
    {
        for ($j = 0; $j < $column; $j++)
        {
            if(!empty($str[$k]))
            $s[$i][$j] = $str[$k];
            $k++;
        }
    }

    // Printing the grid
    for ($i = 0; $i < $row; $i++)
    {
        for ($j = 0; $j < $column; $j++)
        {
            if ($s[$i][$j] == '\0')
                break;
            echo $s[$i][$j];
        }
        echo "\n";
    }
}

// Driver code
$str = "GEEKSFORGEEKS";
gridStr($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to string into grid form
    function gridStr(str)
    {
        let l = str.length;
        let k = 0, row, column;
        row = Math.floor(Math.sqrt(l));
        column = Math.ceil(Math.sqrt(l));

        if (row * column < l)
        {
            row = column;
        }

        let s = new Array(row);
        for (let i = 0; i < row; i++)
        {
            s[i] = new Array(column);
            for (let j = 0; j < column; j++)
            {
                s[i][j] = 0;
            }
        }

        // convert the string into grid
        for (let i = 0; i < row; i++)
        {
            for (let j = 0; j < column; j++)
            {
                if(k < str.length)
                    s[i][j] = str[k];
                k++;
            }
        }

        // Printing the grid
        for (let i = 0; i < row; i++)
        {
            for (let j = 0; j < column; j++)
            {
                if (s[i][j] == 0)
                {
                    break;
                }
                document.write(s[i][j]);
            }
            document.write("</br>");
        }
    }

    let str = "GEEKSFORGEEKS";
      gridStr(str);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
GEEK
SFOR
GEEK
S
```