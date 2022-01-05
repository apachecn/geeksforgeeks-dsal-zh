# 在给定的数字中使用一次交换操作可能得到的最大偶数

> 原文:[https://www . geesforgeks . org/最大偶数-可能使用一个交换操作-给定号码/](https://www.geeksforgeeks.org/largest-even-number-possible-using-one-swap-operation-given-number/)

给定一个字符串形式的奇数，任务是从给定的数字中产生最大的偶数，并且只允许您执行一次交换操作。
**例:**

```
Input : 1235785
Output :1535782
Swap 2 and 5.

Input :  536425
Output :  536524
Swap 4 and 5 to make the largest even number.
```

1.  在最后一个索引处找到小于或等于奇数的第一个偶数。
2.  如果找到，交换两个值。否则与字符串中的最后一个偶数交换。
3.  如果无法做到平衡，打印给定的字符串。

## C++

```
// C++ program for above implementation
#include <bits/stdc++.h>
using namespace std;

// Make the largest even number
string makeEven(string str)
{
    int n = str.length();
    int even = INT_MAX, index;

    // Start traversing the string
    for (int i = 0; i < n - 1; i++) {

        // Find the even number
        if ((str[i] - '0') % 2 == 0) {
            even = (str[i] - '0');
            index = i;
        }

        // Check if current even is equal to
        // or less than the odd number
        if (even <= (str[n - 1] - '0'))
            break;
    }

    // Return original string if there is no
    // even value
    if (even == INT_MAX)
        return str;

    // Swap even and odd value
    swap(str[index], str[n - 1]);

    return str;
}

// Driver code
int main()
{
    string str = "1356425";
    cout << makeEven(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation

class GFG {

// Make the largest even number
    static char[] makeEven(String string) {
        char []str = string.toCharArray();
        int n = str.length;
        int even = Integer.MAX_VALUE, index = 0;

        // Start traversing the String
        for (int i = 0; i < n - 1; i++) {

            // Find the even number
            if ((str[i] - '0') % 2 == 0) {
                even = (str[i] - '0');
                index = i;
            }

            // Check if current even is equal to
            // or less than the odd number
            if (even <= (str[n-1] - '0')) {
                break;
            }
        }

        // Return original String if there is no
        // even value
        if (even == Integer.MAX_VALUE) {
            return str;
        }

        // Swap even and odd value
        swap(str,index, n - 1);

        return str;
    }
static void swap(char[] str,int index1,int index2){
    char temp = str[index1];
    str[index1] = str[index2];
    str[index2] =temp;
}
// Driver code
    public static void main(String[] args) {
        String str = "1356425";
        System.out.print(makeEven(str));
    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 code for the above implementation
import sys

# Make the largest even number
def makeEven(arr, n):

    # index to first even no,if any
    first_e_i = -1

    # index to last even no, if any
    last_e_i = -1

    # index to last no
    last_n_i = n - 1

    # Start traversing the String
    for i in range(n):

        # if it finds any first even no less
        # than last digit then break the loop
        if (int(arr[i]) % 2 == 0 and
            int(arr[i]) < int(arr[last_n_i])):
            first_e_i = i
            break

        # it finds last even no
        if int(arr[i]) % 2 == 0:
            last_e_i = i
    if first_e_i != -1:

        # swap even and odd value
        (arr[first_e_i],
         arr[last_n_i]) = (arr[last_n_i],
                           arr[first_e_i])
        return arr
    if first_e_i == -1 and last_e_i != -1:

        # swap even and odd value
        (arr[last_e_i],
         arr[last_n_i]) = (arr[last_n_i],
                           arr[last_e_i])
        return arr

    # Return original String if there is
    # no even number
    return arr    

# Driver Code
if __name__=='__main__':
    string="1356425"
    result = "".join(makeEven(list(string),
                          len(list(string))))
    print(result)

# This code is contributed
# by Vikash Kumar 37
```

## C#

```
// C# implementation of above approach
using System;

public class GFG {

// Make the largest even number
    static char[] makeEven(String str1) {
        char []str = str1.ToCharArray();
        int n = str.Length;
        int even = int.MaxValue, index = 0;

        // Start traversing the String
        for (int i = 0; i < n - 1; i++) {

            // Find the even number
            if ((str[i] - '0') % 2 == 0) {
                even = (str[i] - '0');
                index = i;
            }

            // Check if current even is equal to
            // or less than the odd number
            if (even <= (str[n-1] - '0')) {
                break;
            }
        }

        // Return original String if there is no
        // even value
        if (even == int.MaxValue) {
            return str;
        }

        // Swap even and odd value
        swap(str,index, n - 1);

        return str;
    }
static void swap(char[] str,int index1,int index2){
    char temp = str[index1];
    str[index1] = str[index2];
    str[index2] =temp;
}
// Driver code
    public static void Main() {
        String str = "1356425";
        Console.WriteLine(makeEven(str));
    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above implementation

// Make the largest even number
function makeEven($str)
{
    $n = strlen($str);
    $even = PHP_INT_MAX; $index;

    // Start traversing the string
    for ($i = 0; $i < $n - 1; $i++)
    {

        // Find the even number
        if (($str[$i] - '0') % 2 == 0)
        {
            $even = ($str[$i] - '0');
            $index = $i;
        }

        // Check if current even is
        // equal to or less than
        // the odd number
        if ($even <= ($str[$n - 1] - '0'))
            break;
    }

    // Return original string if
    // there is no even value
    if ($even == PHP_INT_MAX)
        return $str;

    //swap the number
    list($str[$index],
         $str[$n - 1]) = array($str[$n - 1],
                               $str[$index]);
    return $str;
}

// Driver code
$str = "1356425";
echo makeEven($str);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program for above implementation

    // Make the largest even number
    function makeEven(string) {
        let str = string.split('');
        let n = str.length;
        let even = Number.MAX_VALUE, index = 0;

        // Start traversing the String
        for (let i = 0; i < n - 1; i++) {

            // Find the even number
            if ((str[i].charCodeAt() - '0'.charCodeAt()) % 2 == 0) {
                even = (str[i] - '0');
                index = i;
            }

            // Check if current even is equal to
            // or less than the odd number
            if (even <= (str[n-1].charCodeAt() - '0'.charCodeAt())) {
                break;
            }
        }

        // Return original String if there is no
        // even value
        if (even == Number.MAX_VALUE) {
            return str;
        }

        // Swap even and odd value
        swap(str,index, n - 1);

        return str.join("");
    }

    function swap(str, index1, index2)
    {
      let temp = str[index1];
      str[index1] = str[index2];
      str[index2] =temp;
    }

    let str = "1356425";
      document.write(makeEven(str));

</script>
```

**输出:**

```
1356524
```

**时间复杂度:** O(N)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。