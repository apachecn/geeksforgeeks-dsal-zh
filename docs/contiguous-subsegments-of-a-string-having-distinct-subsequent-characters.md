# 具有不同后续字符的字符串的连续子段

> 原文:[https://www . geeksforgeeks . org/具有不同后续字符的字符串的连续子段/](https://www.geeksforgeeks.org/contiguous-subsegments-of-a-string-having-distinct-subsequent-characters/)

给定长度为 **L** 的字符串**和一个整数 **N** ，任务是形成包含不同后续字符的字符串的总共 **(L / N)** 个连续子段。
**注意:**整数 **N** 将是字符串长度的一个因子，即 **L** 。**

**示例:**

> **输入:**str = " geesforgeeksgfg "，N = 4
> **输出:**
> gek
> for
> gek
> sgf
> “geesforgeeksgfg”的长度为 16，因此会有 4 个子段。
> 第一个子段将包含字符 g、e、e 和 k，但是字母‘e’是重复的，
> 所以我们丢弃一个‘e’。因此，最终的子片段将是“gek”。
> 同样，其他三个子段将为“稳定”、“gek”和“sgf”。
> 每个亚片段应具有随后的不同特征。
> 
> **输入:**str = " aabdefgf "，N = 3
> **输出:**
> ab
> dek
> fg

**方法:**每次在新的子段上开始迭代时，都会创建一个数组。这些元素按顺序存储在该数组中。如果数组中已经存在任何元素，则不会将其推入数组。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function that prints the segments
void sub_segments(string str, int n)
{
    int l = str.length();
    for (int x = 0; x < l; x += n)
    {
        string newlist = str.substr(x, n);

        // New array for every iteration
        list<char> arr;

        // Iterator for new array
        list<char>::iterator it;

        for(auto y:newlist)
        {
            it = find(arr.begin(), arr.end(), y);

            // Check if iterator points to end or not
            if(it == arr.end())
                arr.push_back(y);
        }

        for(auto y:arr)
            cout << y;
        cout << endl;
    }
}

// Driver code
int main()
{
    string str = "geeksforgeeksgfg";
    int n = 4;
    sub_segments(str, n);
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that prints the segments
static void sub_segments(String str, int n)
{
    int l = str.length();
    for (int x = 0; x < l; x += n)
    {
        String newlist = str.substring(x, x + n);

        // New array for every iteration
        List<Character> arr = new ArrayList<Character>();
        for (char y : newlist.toCharArray())
        {

            // Check if the character is in the array
            if (!arr.contains(y))
                arr.add(y);
        }
        for (char y : arr)
            System.out.print(y);
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeksgfg";
    int n = 4;
    sub_segments(str, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that prints the segments
def sub_segments (string, n):
    l = len (string)
    for x in range (0, l, n):
        newlist = string[x : x + n]

        # New array for every iteration
        arr = []
        for y in newlist:

           # Check if the character is in the array
            if y not in arr:
                arr.append (y)

        print (''.join (arr))

# Driver code
string = "geeksforgeeksgfg"
n = 4
sub_segments (string, n)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that prints the segments
static void sub_segments(String str, int n)
{
    int l = str.Length;
    for (int x = 0; x < l; x += n)
    {
        String newlist = str.Substring(x, n);

        // New array for every iteration
        List<char> arr = new List<char>();
        foreach (char y in newlist.ToCharArray())
        {

            // Check if the character is in the array
            if (!arr.Contains(y))
                arr.Add(y);
        }
        foreach (char y in arr)
            Console.Write(y);
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeksgfg";
    int n = 4;
    sub_segments(str, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that prints the segments
function sub_segments(str, n) {
    let l = str.length;
    for (let x = 0; x < l; x += n) {
        let newlist = str.substr(x, n);

        // New array for every iteration
        let arr = [];

        for (let y of newlist) {

            // Check if the character is in the array
            if (!arr.includes(y))
                arr.push(y);
        }
        for (let y of arr)
            document.write(y);
        document.write("<br>");
    }
}

// Driver code

let str = "geeksforgeeksgfg";
let n = 4;
sub_segments(str, n);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
gek
sfor
gek
sgf
```