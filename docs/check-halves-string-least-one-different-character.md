# 检查字符串的两半是否至少有一个不同的字符

> 原文:[https://www . geesforgeks . org/check-halves-string-至少一个不同字符/](https://www.geeksforgeeks.org/check-halves-string-least-one-different-character/)

前面我们已经讨论了[如何检查字符串的两部分是否具有相同的字符集](https://www.geeksforgeeks.org/check-half-string-character-frequency-character/)。现在，我们进一步扩展我们的问题，检查字符串的两部分是否至少有一个不同的字符。

**示例:**

```
Input : baaaab
Output: No, both halves do not differ at all
The two halves contain the same characters
and their frequencies match so not different
the character exists

Input : abccpb
Output : Yes, both halves differ by at least one character
```

**方法 1:(两个计数器阵列)**

*   把绳子分成两半
*   分别遍历两个不同的部分，并将每个字符的出现计数到两个不同的计数器数组中
*   现在，遍历这些数组，如果这些数组在某一点上不同，我们得到的答案是“是”

## C++

```
// C++ implementation to check if
// both halves of the string have
// at least one different character
#include <cstring>
#include <iostream>
#include <string>
using namespace std;
# define MAX 26

// Function which break string into two halves
// Counts frequency of characters in each half
// Compares the two counter array and returns
// true if these counter arrays differ
bool function(string str)
{
    int l = str.length();

    // Declaration and initialization
    // of counter array
    int counter1[MAX];
    int counter2[MAX];
    memset(counter1, 0, sizeof(counter1));
    memset(counter2, 0, sizeof(counter2));

    for (int i = 0; i < l / 2; i++)
        counter1[str[i] - 'a']++;
    for (int i = l / 2; i < l; i++)
        counter2[str[i] - 'a']++;
    for (int i = 0; i < MAX; i++)
        if (counter2[i] != counter1[i])
            return true;

    return false;
}

// Driver function
int main()
{
    string str = "abcasdsabcae";
    if (function(str))
        cout << "Yes, both halves differ"
             <<" by at least one character";
    else
        cout << "No, both halves do "
             <<"not differ at all";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the problem
import java.util.*;
import java.lang.*;

class GeeksforGeeks {
    final static int MAX = 26;

    // Function which break string into two halves
    // Counts frequency of characters in each half
    // Compares the two counter array and returns
    // true if these counter arrays differ
    static boolean function(String str)
    {
        int l = str.length();

        // Declaration and initialization
        // of counter array
        int counter1[] = new int[MAX];
        int counter2[] = new int[MAX];
        for (int i = 0; i < MAX; i++) {
            counter1[i] = 0;
            counter2[i] = 0;
        }

        for (int i = 0; i < l / 2; i++)
            counter1[str.charAt(i) - 'a']++;
        for (int i = l / 2; i < l; i++)
            counter2[str.charAt(i) - 'a']++;
        for (int i = 0; i < MAX; i++) {
            if (counter2[i] != counter1[i])
                return true;
        }
        return false;
    }

    // Driver function
    public static void main(String args[])
    {
        String str = "abcasdsabcae";
        if (function(str))
            System.out.print("Yes, both halves "+
            "differ by at least one character");
        else
            System.out.print("No, both halves "+
            "do not differ at all");
    }
}
```

## 蟒蛇 3

```
# Python implementation to check if
# both halves of the string have
# at least one different character

MAX = 26

# Function which break string into two halves
# Counts frequency of characters in each half
# Compares the two counter array and returns
# true if these counter arrays differ
def function(st):
    global MAX
    l = len(st)

    # Declaration and initialization
    # of counter array
    counter1, counter2 = [0] * MAX, [0] * MAX

    for i in range(l//2):
        counter1[ord(st[i]) - ord('a')] += 1

    for i in range(l//2, l):
        counter2[ord(st[i]) - ord('a')] += 1

    for i in range(MAX):
        if (counter2[i] != counter1[i]):
            return True
    return False

# Driver function
st = "abcasdsabcae"
if function(st): print("Yes, both halves differ ",
                       "by at least one character")
else: print("No, both halves do not differ at all")

# This code is contributed by Ansu Kumari
```

## C#

```
// C# implementation to check if
// both halves of the string have
// at least one different character

using System;

class GeeksforGeeks {
    static int MAX = 26;

    // Function which break string into two halves
    // Counts frequency of characters in each half
    // Compares the two counter array and returns
    // true if these counter arrays differ
    static bool function(String str)
    {
        int l = str.Length;

        // Declaration and initialization
        // of counter array
        int []counter1 = new int[MAX];
        int []counter2 = new int[MAX];
        for (int i = 0; i < MAX; i++)
        {
            counter1[i] = 0;
            counter2[i] = 0;
        }

        for (int i = 0; i < l / 2; i++)
            counter1[str[i] - 'a']++;
        for (int i = l / 2; i < l; i++)
            counter2[str[i] - 'a']++;
        for (int i = 0; i < MAX; i++) {
            if (counter2[i] != counter1[i])
                return true;
        }
        return false;
    }

    // Driver function
    public static void Main()
    {
        String str = "abcasdsabcae";
        if (function(str))
            Console.WriteLine("Yes, both halves "+
            "differ by at least one character");
        else
            Console.WriteLine("No, both halves "+
            "do not differ at all");
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check if
// both halves of the string have
// at least one different character

$MAX = 26;

// Function which break string into two halves
// Counts frequency of characters in each half
// Compares the two counter array and returns
// true if these counter arrays differ
function function_1($str)
{
    global $MAX;
    $l = strlen($str);

    // Declaration and initialization
    // of counter array
    $counter1 = array_fill(0,$MAX,NULL);
    $counter2 = array_fill(0,$MAX,NULL);

    for ($i = 0; $i < $l / 2; $i++)
        $counter1[ord($str[$i]) - ord('a')]++;
    for ($i = $l / 2; $i < $l; $i++)
        $counter2[ord($str[$i]) - ord('a')]++;
    for ($i = 0; $i < $MAX; $i++)
        if ($counter2[$i] != $counter1[$i])
            return true;

    return false;
}

// Driver function

$str = "abcasdsabcae";
if (function_1($str))
    echo "Yes, both halves differ"
         ." by at least one character";
else
    echo "No, both halves do "
         ."not differ at all";
return 0;
?>
```

## java 描述语言

```
<script>

// JavaScript program implementation of the problem

let MAX = 26;

    // Function which break string into two halves
    // Counts frequency of characters in each half
    // Compares the two counter array and returns
    // true if these counter arrays differ
    function functions(str)
    {
        let l = str.length;

        // Declaration and initialization
        // of counter array
        let counter1 = [];
        let counter2 = [];
        for (let i = 0; i < MAX; i++)
        {
            counter1[i] = 0;
            counter2[i] = 0;
        }

        for (let i = 0; i < l / 2; i++)
            counter1[str[i] - 'a']++;
        for (let i = l / 2; i < l; i++)
            counter2[str[i] - 'a']++;
        for (let i = 0; i < MAX; i++) {
            if (counter2[i] != counter1[i])
                return true;
        }
        return false;
    }

// Driver code

        let str = "abcasdsabcae";
        if (functions(str) != 1)
            document.write("Yes, both halves "+
            "differ by at least one character");
        else
            document.write("No, both halves "+
            "do not differ at all");

</script>
```

**输出:**

```
Yes, both halves differ by at least one character
```

**方法二:(一个计数器阵列)**

*   此方法仅使用长度为 26 的单个数组。
*   对于前半部分，我们增加长度为 26 的计数器数组中的字符。
*   对于第二个数组，我们递减该计数器数组中的字符。
*   现在，如果对应于一个字符的索引有非零值，那就是存在的不同字符
*   正面的是前半部分的人物，反面的是后半部分的人物

## C++

```
// C++ implementation to check if
// both halves of the string have
// at least one different character
#include <cstring>
#include <iostream>
#include <string>
using namespace std;
# define MAX 26

// Function which break string into two halves
// Increments frequency of characters for first half
// Decrements frequency of characters for second half
// true if any index has non-zero value
bool function(string str)
{
    int l = str.length();

    // Declaration and initialization
    // of counter array
    int counter[MAX];
    memset(counter, 0, sizeof(counter));
    for (int i = 0; i < l / 2; i++)
        counter[str[i] - 'a']++;
    for (int i = l / 2; i < l; i++)
        counter[str[i] - 'a']--;
    for (int i = 0; i < MAX; i++)
        if (counter[i] != 0)
            return true;

    return false;
}

// Driver function
int main()
{
    string str = "abcasdsabcae";
    if (function(str))
        cout << "Yes, both halves differ"
             <<" by at least one character";
    else
        cout << "No, both halves do"
             <<" not differ at all";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the problem
import java.util.*;
import java.lang.*;

class GeeksforGeeks {

    final static int MAX = 26;

    // Function which break string into two halves
    // Increments frequency of characters for first half
    // Decrements frequency of characters for second half
    // true if any index has non-zero value
    static boolean function(String str)
    {
        int l = str.length();

        // Declaration and initialization
        // of counter array
        int counter[] = new int[MAX];
        for (int i = 0; i < MAX; i++)
            counter[i] = 0;
        for (int i = 0; i < l / 2; i++)
            counter[str.charAt(i) - 'a']++;
        for (int i = l / 2; i < l; i++)
            counter[str.charAt(i) - 'a']--;
        for (int i = 0; i < MAX; i++)
            if (counter[i] != 0)
                return true;

        return false;
    }

    // Driver function
    public static void main(String args[])
    {
        String str = "abcasdsabcae";
        if (function(str))
            System.out.print("Yes, both halves"
            +" differ by at least one character");
        else
            System.out.print("No, both halves"
            +" do not differ at all");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to check if
# both halves of the string have
# at least one different character
MAX = 26

# Function which break string into two
# halves Increments frequency of characters
# for first half Decrements frequency of
# characters for second half true if any
# index has non-zero value
def function(st):
    global MAX
    l = len(st)

    # Declaration and initialization
    # of counter array
    counter = [0] * MAX

    for i in range(l // 2):
        counter[ord(st[i]) - ord('a')] += 1

    for i in range(l // 2, l):
        counter[ord(st[i]) - ord('a')] -= 1

    for i in range(MAX):
        if (counter[i] != 0):
            return True

    return False

# Driver function
st = "abcasdsabcae"
if function(st):
    print("Yes, both halves differ by at ",
          "least one character")
else:
    print("No, both halves do not differ at all")

# This code is contributed by Ansu Kumari
```

## C#

```
// C# implementation of the problem
using System;

class GFG {

    static int MAX = 26;

    // Function which break string into
    // two halves Increments frequency
    // of characters for first half
    // Decrements frequency of characters
    // for second half true if any index
    // has non-zero value
    static bool function(String str)
    {
        int l = str.Length;

        // Declaration and initialization
        // of counter array
        int []counter = new int[MAX];
        for (int i = 0; i < MAX; i++)
            counter[i] = 0;
        for (int i = 0; i < l / 2; i++)
            counter[str[i] - 'a']++;
        for (int i = l / 2; i < l; i++)
            counter[str[i] - 'a']--;
        for (int i = 0; i < MAX; i++)
            if (counter[i] != 0)
                return true;

        return false;
    }

    // Driver function
    public static void Main()
    {
        string str = "abcasdsabcae";
        if (function(str))
        Console.Write("Yes, both halves"
            + " differ by at least one "
                         + "character");
        else
            Console.Write("No, both halves"
              + " do not differ at all");
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>
// Javascript implementation of the problem

    let MAX = 26;

    // Function which break string into two halves
    // Increments frequency of characters for first half
    // Decrements frequency of characters for second half
    // true if any index has non-zero value
    function Function(str)
    {
        let l = str.length;

        // Declaration and initialization
        // of counter array
        let counter = new Array(MAX);
        for (let i = 0; i < MAX; i++)
            counter[i] = 0;
        for (let i = 0; i < l / 2; i++)
            counter[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        for (let i = Math.floor(l / 2); i < l; i++)
            counter[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]--;
        for (let i = 0; i < MAX; i++)
            if (counter[i] != 0)
                return true;

        return false;
    }

    // Driver function
    let str = "abcasdsabcae";
    if (Function(str))
        document.write("Yes, both halves"
            +" differ by at least one character");
    else
        document.write("No, both halves"
            +" do not differ at all");

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Yes, both halves differ by at least one character
```

两种方法的时间复杂度都是线性的，即 **O(len)**

**方法三:(无多余空间)**

*   以字符数组的形式输入字符串
*   将两个字符串分别排序
*   一起遍历两半，如果它们在任何一点上不同，返回真
    到调用函数

遵循下面的代码。

## C++

```
// C++ implementation to check if
// both halves of the string have
// at least one different character
#include <algorithm>
#include <cstring>
#include <iostream>
#include <string>
using namespace std;

// Function which break string into two halves
// Sorts the two halves separately
// Compares the two halves
// return true if any index has non-zero value
bool function(char str[])
{
    int l = strlen(str);

    // Declaration and initialization
    // of counter array
    sort(str, str + (l / 2));
    sort(str + (l / 2), str + l);
    for (int i = 0; i < l / 2; i++)
        if (str[i] != str[l / 2 + i])
            return true;
    return false;
}

// Driver function
int main()
{
    char str[] = "abcasdsabcae";
    if (function(str))
        cout << "Yes, both halves differ by"
             <<" at least one character";
    else
        cout << "No, both halves do"
             <<" not differ at all";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// both halves of the string have
// at least one different character

import java.io.*;
import java.util.*;

class GFG {

// Function which break string into two halves
// Sorts the two halves separately
// Compares the two halves
// return true if any index has non-zero value
static Boolean function(char str[])
{
    int l = str.length;

    // Declaration and initialization
    // of counter array
    Arrays.sort(str, 0, (l / 2));
    Arrays.sort(str,(l / 2), l);
    for (int i = 0; i < l / 2; i++)
        if (str[i] != str[l / 2 + i])
            return true;
    return false;
}

    public static void main (String[] args) {
    char str[] = ("abcasdsabcae").toCharArray();
    if (function(str))
        System.out.println("Yes, both halves differ"
        + " by at least one character");
    else
        System.out.println("No, both halves do"
        + " not differ at all");
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python implementation to check if
# both halves of the string have
# at least one different character

# Function which break string into two halves
# Sorts the two halves separately
# Compares the two halves
# return true if any index has non-zero value
def function(st):
    st = list(st)
    l = len(st)

    # Declaration and initialization
    # of counter array
    st[:l//2] = sorted(st[:l//2])
    st[l//2:] = sorted(st[l//2:])
    for i in range(l//2):
        if (st[i] != st[l//2 + i]):
            return True
    return False

# Driver function
st = "abcasdsabcae"
if function(st): print("Yes, both halves differ ",
                       "by at least one character")
else: print("No, both halves do not differ at all")

# This code is contributed by Ansu Kumari
```

## C#

```
// C# implementation to check if
// both halves of the string have
// at least one different character
using System;

class GFG
{

// Function which break string into two halves
// Sorts the two halves separately
// Compares the two halves
// return true if any index has non-zero value
static Boolean function(char []str)
{
    int l = str.Length;

    // Declaration and initialization
    // of counter array
    Array.Sort(str, 0, (l / 2));
    Array.Sort(str,(l / 2), l-(l/2));
    for (int i = 0; i < l / 2; i++)
        if (str[i] != str[l / 2 + i])
            return true;
    return false;
}

// Driver code
public static void Main (String[] args)
{
    char []str = ("abcasdsabcae").ToCharArray();
    if (function(str))
        Console.WriteLine("Yes, both halves differ"
        + " by at least one character");
    else
        Console.WriteLine("No, both halves do"
        + " not differ at all");
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation to check if
// both halves of the string have
// at least one different character

    // Function which break string into two halves
    // Sorts the two halves separately
    // Compares the two halves
    // return true if any index has non-zero value
    function Function(str)
    {
        let l = str.length;

    // Declaration and initialization
    // of counter array
    str=(str.slice(0,Math.floor(l/2)).sort()).concat(str.slice(Math.floor(l/2),l).sort());
    for (let i = 0; i < Math.floor(l / 2); i++)
        if (str[i] != str[Math.floor(l / 2) + i])
            return true;
    return false;
    }

    let str="abcasdsabcae".split("");
    if (Function(str))
        document.write("Yes, both halves differ"
        + " by at least one character");
    else
        document.write("No, both halves do"
        + " not differ at all");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Yes, both halves differ by at least one character
```

上述方法的复杂性是 **O(len log (len))**