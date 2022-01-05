# 检查字符串的两半是否有相同的字符集

> 原文:[https://www . geesforgeks . org/check-半字符串-字符-频率-字符/](https://www.geeksforgeeks.org/check-half-string-character-frequency-character/)

给定一个只有小写字符的字符串，任务是检查是否有可能从中间分割一个字符串，这将给出具有相同字符和每个字符相同频率的两半。如果给定字符串的长度为奇数，则忽略中间元素并检查其余部分。

**示例:**

```
Input: abbaab
Output: NO
The two halves contain the same characters
but their frequencies do not match so they
are NOT CORRECT

Input : abccab
Output : YES
```

**算法:**

1.  声明两个计数器数组，用于保持字符串的一半中的字符数，每个数组的大小为 26。
2.  现在运行一个循环，取两个变量 I 和 j，其中 I 从 0 开始，j 从(字符串长度–1)开始。
3.  对于字符串中的每个字符，转到计数器数组中相应的索引，将该值递增 1，递增 I，递减 j。这样做，直到 I 小于 j
4.  完成步骤 3 后，再次运行循环并比较计数器数组的值。如果第一个数组的值不等于第二个数组的值，则返回 false。
5.  如果所有计数都匹配，则返回 true。

以下是上述想法的实现:

## C++

```
// C++ program to check if it is
// possible to split string or not
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// function to check if we can split
// string or not
bool checkCorrectOrNot(string s)
{
    // Counter array initialized with 0
    int count1[MAX_CHAR] = {0};
    int count2[MAX_CHAR] = {0};

    // Length of the string
    int n = s.length();
    if (n == 1)
        return true;

    // traverse till the middle element
    // is reached
    for (int i=0,j=n-1; i<j; i++,j--)
    {
        // First half
        count1[s[i]-'a']++;

        // Second half
        count2[s[j]-'a']++;
    }

    // Checking if values are different
    // set flag to 1
    for (int i = 0; i<MAX_CHAR; i++)
        if (count1[i] != count2[i])
            return false;

    return true;
}

// Driver program to test above function
int main()
{
    // String to be checked
    string s = "abab";

    if (checkCorrectOrNot(s))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it two 
// half of string contain same Character
// set or not
public class GFG {

    static final int MAX_CHAR = 26;

    // function to check both halves
    // for equality
    static boolean checkCorrectOrNot(String s)
    {
        // Counter array initialized with 0
        int[] count1 = new int[MAX_CHAR];
        int[] count2 = new int[MAX_CHAR];

        // Length of the string
        int n = s.length();
        if (n == 1)
            return true;

        // traverse till the middle element
        // is reached
        for (int i = 0, j = n - 1; i < j; i++, j--)
        {
            // First half
            count1[s.charAt(i) - 'a']++;

            // Second half
            count2[s.charAt(j) - 'a']++;
        }

        // Checking if values are different
        // set flag to 1
        for (int i = 0; i < MAX_CHAR; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        // String to be checked
        String s = "abab";

        if (checkCorrectOrNot(s))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
// This code is contributed by Sumit Ghosh

```

## 蟒蛇 3

```
# Python3 program to check if it is
# possible to split string or not
MAX_CHAR = 26

# Function to check if we 
# can split string or not
def checkCorrectOrNot(s):

    global MAX_CHAR

    # Counter array initialized with 0
    count1 = [0] * MAX_CHAR
    count2 = [0] * MAX_CHAR

    # Length of the string
    n = len(s)

    if n == 1:
        return true

    # Traverse till the middle 
    # element is reached
    i = 0; j = n - 1

    while (i < j):

        # First half
        count1[ord(s[i]) - ord('a')] += 1

        # Second half
        count2[ord(s[j]) - ord('a')] += 1

        i += 1; j -= 1

    # Checking if values are 
    # different set flag to 1
    for i in range(MAX_CHAR):

        if count1[i] != count2[i]:
            return False

    return True

# Driver Code

# String to be checked
s = "ababc"

print("Yes" if checkCorrectOrNot(s) else "No")

# This code is contributed by Ansu Kumari.

```

## C#

```
// C# program to check if it two half of 
// string contain same Character set or not
using System;

class GFG {

    static int MAX_CHAR = 26;

    // function to check both halves for 
    // equality
    static bool checkCorrectOrNot(string s)
    {

        // Counter array initialized with 0
        int []count1 = new int[MAX_CHAR];
        int []count2 = new int[MAX_CHAR];

        // Length of the string
        int n = s.Length;
        if (n == 1)
            return true;

        // traverse till the middle element
        // is reached
        for (int i = 0, j = n - 1; i < j;
                                   i++, j--)
        {

            // First half
            count1[s[i] - 'a']++;

            // Second half
            count2[s[j] - 'a']++;
        }

        // Checking if values are different
        // set flag to 1
        for (int i = 0; i < MAX_CHAR; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    // Driver program to test above function
    public static void Main()
    {
        // String to be checked
        string s = "abab";

        if (checkCorrectOrNot(s))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php 
// PHP program to check if it is
// possible to split string or not
$MAX_CHAR = 26;

// function to check if we 
// can split string or not
function checkCorrectOrNot($s)
{
    global $MAX_CHAR;

    // Counter array initialized with 0
    $count1 = array_fill(0, $MAX_CHAR, NULL);
    $count2 = array_fill(0, $MAX_CHAR, NULL);

    // Length of the string
    $n = strlen($s);
    if ($n == 1)
        return true;

    // traverse till the middle 
    // element is reached
    for ($i = 0, $j = $n - 1; 
         $i < $j; $i++, $j--)
    {
        // First half
        $count1[$s[$i] - 'a']++;

        // Second half
        $count2[$s[$j] - 'a']++;
    }

    // Checking if values are 
    // different set flag to 1
    for ($i = 0; $i < $MAX_CHAR; $i++)
        if ($count1[$i] != $count2[$i])
            return false;

    return true;
}

// Driver Code

// String to be checked
$s = "abab";
if (checkCorrectOrNot($s))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed 
// by ChitraNayal
?>

```

## java 描述语言

```
<script>
// Javascript program to check if it two 
// half of string contain same Character
// set or not

    let MAX_CHAR = 26;

    // function to check both halves
    // for equality
    function checkCorrectOrNot(s)
    {
        // Counter array initialized with 0
        let count1 = new Array(MAX_CHAR);
        let count2 = new Array(MAX_CHAR);
        for(let i=0;i<MAX_CHAR;i++)
        {
            count1[i]=0;
            count2[i]=0;
        }

        // Length of the string
        let n = s.length;
        if (n == 1)
            return true;

        // traverse till the middle element
        // is reached
        for (let i = 0, j = n - 1; i < j; i++, j--)
        {
            // First half
            count1[s[i] - 'a']++;

            // Second half
            count2[s[j] - 'a']++;
        }

        // Checking if values are different
        // set flag to 1
        for (let i = 0; i < MAX_CHAR; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }    

    // Driver program to test above function

    // String to be checked
    let  s = "abab";
    if (checkCorrectOrNot(s))
        document.write("Yes");
    else
        document.write("No");

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
YES
```

**空间优化解:**
下图是上述方法的空间优化解。

1.  我们只用 1 个计数器阵列就能解决这个问题。
2.  取一个字符串，前半部分递增计数，后半部分递减计数。
3.  如果最终计数器数组为 0，则返回真，否则返回假。

以下是上述想法的实现:

## C++

```
// C++ program to check if it is
// possible to split string or not
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// function to check if we can split
// string or not
bool checkCorrectOrNot(string s)
{
    // Counter array initialized with 0
    int count[MAX_CHAR] = {0};

    // Length of the string
    int n = s.length();
    if (n == 1)
        return true;

    // traverse till the middle element
    // is reached
    for (int i=0,j=n-1; i<j; i++,j--)
    {
        // First half
        count[s[i]-'a']++;

        // Second half
        count[s[j]-'a']--;
    }

    // Checking if values are different
    // set flag to 1
    for (int i = 0; i<MAX_CHAR; i++)
        if (count[i] != 0)
            return false;

    return true;
}

// Driver program to test above function
int main()
{
    // String to be checked
    string s = "abab";

    if (checkCorrectOrNot(s))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it two 
// half of string contain same Character
// set or not
public class GFG {

    static final int MAX_CHAR = 26;

    // function to check both halves
    // for equality
    static boolean checkCorrectOrNot(String s)
    {
        // Counter array initialized with 0
        int[] count = new int[MAX_CHAR];

        // Length of the string
        int n = s.length();
        if (n == 1)
            return true;

        // traverse till the middle element
        // is reached
        for (int i = 0,j = n - 1; i < j; i++, j--)
        {
            // First half
            count[s.charAt(i) - 'a']++;

            // Second half
            count[s.charAt(j) - 'a']--;
        }

        // Checking if values are different
        // set flag to 1
        for (int i = 0; i < MAX_CHAR; i++)
            if (count[i] != 0)
                return false;

        return true;
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        // String to be checked
        String s = "abab";

        if (checkCorrectOrNot(s))
            System.out.println("Yes");
        else
           System.out.println("No");
    }
}
// This code is contributed by Sumit Ghosh

```

## 蟒蛇 3

```
# Python3 program to check if it is
# possible to split string or not
MAX_CHAR = 26

# Function to check if we  
# can split string or not
def checkCorrectOrNot(s):

    global MAX_CHAR

    # Counter array initialized with 0
    count = [0] * MAX_CHAR

    # Length of the string
    n = len(s)

    if n == 1:
        return true

    # Traverse till the middle 
    # element is reached
    i = 0; j = n-1

    while i < j:

        # First half
        count[ord(s[i]) - ord('a')] += 1

        # Second half
        count[ord(s[j])-ord('a')] -= 1

        i += 1; j -= 1

    # Checking if values are 
    # different, set flag to 1
    for i in range(MAX_CHAR):

        if count[i] != 0:
            return False

    return True

# Driver Code

# String to be checked
s = "abab"

print("Yes" if checkCorrectOrNot(s) else "No")

# This code is contributed by Ansu Kumari.

```

## C#

```
// C# program to check if it two 
// half of string contain same Character
// set or not
using System;

public class GFG {

    static int MAX_CHAR = 26;

    // function to check both halves
    // for equality
    static bool checkCorrectOrNot(String s)
    {

        // Counter array initialized with 0
        int[] count = new int[MAX_CHAR];

        // Length of the string
        int n = s.Length;
        if (n == 1)
            return true;

        // traverse till the middle element
        // is reached
        for (int i = 0, j = n - 1; i < j; i++, j--)
        {
            // First half
            count[s[i] - 'a']++;

            // Second half
            count[s[j] - 'a']--;
        }

        // Checking if values are different
        // set flag to 1
        for (int i = 0; i < MAX_CHAR; i++)
            if (count[i] != 0)
                return false;

        return true;
    }

    // Driver program to test above function
    public static void Main(String []args)
    {

        // String to be checked
        String s = "abab";

        if (checkCorrectOrNot(s))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by parashar.

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP 
// PHP program to check if it is
// possible to split string or not
$MAX_CHAR = 26;

// function to check if we 
// can split string or not
function checkCorrectOrNot($s)
{
    global $MAX_CHAR;

    // Counter array initialized with 0
    $count = array_fill(0, $MAX_CHAR, NULL);

    // Length of the string
    $n = strlen($s);
    if ($n == 1)
        return true;

    // traverse till the middle 
    // element is reached
    for ($i = 0, $j = $n - 1; 
         $i < $j; $i++, $j--)
    {
        // First half
        $count[$s[$i] - 'a']++;

        // Second half
        $count[$s[$j] - 'a']--;
    }

    // Checking if values are 
    // different set flag to 1
    for ($i = 0; $i < $MAX_CHAR; $i++)
        if ($count[$i] != 0)
            return false;

    return true;
}

// Driver Code

// String to be checked
$s = "abab";
if (checkCorrectOrNot($s))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed 
// by ChitraNayal
?>

```

## java 描述语言

```
<script>

// Javascript program to check if it two
// half of string contain same Character
// set or not

let MAX_CHAR = 26;

// Function to check both halves
// for equality
function checkCorrectOrNot(s)
{

    // Counter array initialized with 0
    let count = new Array(MAX_CHAR);
    for(let i = 0; i < count.length; i++)
    {
        count[i] = 0;
    }

    // Length of the string
    let n = s.length;
    if (n == 1)
        return true;

    // Traverse till the middle element
    // is reached
    for(let i = 0, j = n - 1; i < j; i++, j--)
    {

        // First half
        count[s[i] - 'a']++;

        // Second half
        count[s[j] - 'a']--;
    }

    // Checking if values are different
    // set flag to 1
    for(let i = 0; i < MAX_CHAR; i++)
        if (count[i] != 0)
            return false;

    return true;
}

// Driver Code
let s = "abab";

if (checkCorrectOrNot(s))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rag2127

</script>
```

**输出:**

```
YES
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。