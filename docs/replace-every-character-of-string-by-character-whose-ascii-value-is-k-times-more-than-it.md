# 用 ASCII 值比字符串多 K 倍的字符替换字符串的每个字符

> 原文:[https://www . geesforgeks . org/逐字符替换字符串中的每个字符，其 ascii 值比它多 k 倍/](https://www.geeksforgeeks.org/replace-every-character-of-string-by-character-whose-ascii-value-is-k-times-more-than-it/)

给定字符串*字符串*仅由小写字母和整数 *k* 组成，任务是用 ASCII 值比它大 k 倍的字符替换给定字符串的每个字符。如果 ASCII 值超过“z”，则以循环方式从“a”开始检查。

**示例:**

> **输入:** str = "abc "，k = 2
> **输出:** cde
> a 移动 2 次导致字符 c
> b 移动 2 次导致字符 d
> c 移动 2 次导致字符 e
> **输入:** str = "abc "，k = 28
> **输出** : cde
> a 移动 25 次，到达 z。那么第 26 个字符将是 a，第 27 个 b 和第 28 个 c。
> b 移动 24 次，到达 z。28-th 为 d.
> b 移动 23 次，到达 z。28 号是 e。

**逼近**:对字符串中的每个字符进行迭代，并对每个字符执行以下步骤:

*   将 k 添加到字符串[i]的 ASCII 值中。
*   如果超过 122，则用 26 执行 k 的模数运算，以减少步数，因为 26 是一次旋转中可以执行的最大移位数。
*   要查找字符，请将 k 加到 96。因此，ASCII 值为 k+96 的字符将是一个新字符。

对给定字符串的每个字符重复上述步骤。

下面是上述方法的实现:

## C++

```
// CPP program to move every character
// K times ahead in a given string
#include <bits/stdc++.h>
using namespace std;

// Function to move string character
void encode(string s,int k){

    // changed string
    string newS;

    // iterate for every characters
    for(int i=0; i<s.length(); ++i)
    {
        // ASCII value
        int val = int(s[i]);

        // store the duplicate
        int dup = k;

        // if k-th ahead character exceed 'z'
        if(val + k > 122){
            k -= (122-val);
            k = k % 26;
            newS += char(96 + k);
        }
        else
            newS += char(val + k);

        k = dup;
    }

    // print the new string
    cout<<newS;
}

// driver code
int main(){
    string str = "abc";
    int k = 28;

    // function call
    encode(str, k);

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to move every character
// K times ahead in a given string

class GFG {

// Function to move string character
    static void encode(String s, int k) {

        // changed string
        String newS = "";

        // iterate for every characters
        for (int i = 0; i < s.length(); ++i) {
            // ASCII value
            int val = s.charAt(i);
            // store the duplicate
            int dup = k;

            // if k-th ahead character exceed 'z'
            if (val + k > 122) {
                k -= (122 - val);
                k = k % 26;

                newS += (char)(96 + k);
            } else {
                newS += (char)(val + k);
            }

            k = dup;
        }

        // print the new string
        System.out.println(newS);
    }

// Driver Code
    public static void main(String[] args) {
        String str = "abc";
        int k = 28;

        // function call
        encode(str, k);
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python program to move every character
# K times ahead in a given string

# Function to move string character
def encode(s, k):

    # changed string
    newS = ""

    # iterate for every characters
    for i in range(len(s)):

        # ASCII value
        val = ord(s[i])

        # store the duplicate
        dup = k

        # if k-th ahead character exceed 'z'
        if val + k>122:
            k -= (122-val)
            k = k % 26
            newS += chr(96 + k)

        else:
            newS += chr(val + k)

        k = dup

    # print the new string
    print (newS)

# driver code    
str = "abc"
k = 28

encode(str, k)
```

## C#

```
// C# program to move every character
// K times ahead in a given string
using System;
public class GFG {

// Function to move string character
    static void encode(String s, int k) {

        // changed string
        String newS = "";

        // iterate for every characters
        for (int i = 0; i < s.Length; ++i) {
            // ASCII value
            int val = s[i];
            // store the duplicate
            int dup = k;

            // if k-th ahead character exceed 'z'
            if (val + k > 122) {
                k -= (122 - val);
                k = k % 26;

                newS += (char)(96 + k);
            } else {
                newS += (char)(96 + k);
            }

            k = dup;
        }

        // print the new string
        Console.Write(newS);
    }

// Driver Code
    public static void Main() {
        String str = "abc";
        int k = 28;

        // function call
        encode(str, k);
    }
}

// This code is contributed by Rajput-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to move every character
// K times ahead in a given string

// Function to move string character
function encode($s, $k)
{

    // changed string
    $newS = "";

    // iterate for every characters
    for($i = 0; $i < strlen($s); ++$i)
    {
        // ASCII value
        $val = ord($s[$i]);

        // store the duplicate
        $dup = $k;

        // if k-th ahead character exceed 'z'
        if($val + $k > 122)
        {
            $k -= (122 - $val);
            $k = $k % 26;
            $newS = $newS.chr(96 + $k);
        }
        else
            $newS = $newS.chr($val + $k);

        $k = $dup;
    }

    // print the new string
    echo $newS;
}

// Driver code

$str = "abc";
$k = 28;

// function call
encode($str, $k);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to move every character
// K times ahead in a given string

// Function to move string character

    function encode(s,k)
    {
        // changed string
        let newS = "";

        // iterate for every characters
        for (let i = 0; i < s.length; ++i) {
            // ASCII value
            let val = s[i].charCodeAt(0);
            // store the duplicate
            let dup = k;

            // if k-th ahead character exceed 'z'
            if (val + k > 122) {
                k -= (122 - val);
                k = k % 26;

                newS += String.fromCharCode(96 + k);
            } else {
                newS += String.fromCharCode(val + k);
            }

            k = dup;
        }

        // print the new string
        document.write(newS);
    }

    // Driver Code
    let str = "abc";
    let k = 28;

    // function call
    encode(str, k);

// This code is contributed by rag2127
</script>
```

**输出:**

```
cde
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。