# 查找字符串中最大和最小 ASCII 值字符的程序

> 原文:[https://www . geesforgeks . org/program-to-find-最大最小 ascii 值字符串字符/](https://www.geeksforgeeks.org/program-to-find-the-largest-and-smallest-ascii-valued-characters-in-a-string/)

给定一个由小写和大写字符组成的字符串，您的任务是找到字符串中最大和最小的字母表(根据 ASCII 值)。请注意，在 ASCII 中，所有大写字母都在所有小写字母之前。
示例:

```
Input : sample string
Output : Largest = t, Smallest = a

Input : Geeks
Output : Largest = s, Smallest = G
Explanation: According to alphabetical order 
largest alphabet in this string is 's' 
and smallest alphabet in this string is
'G'( not 'e' according to the ASCII value)

Input : geEks
Output : Largest = s, Smallest = E
```

最大可能值可以是“z”，最小可能值可以是“A”。

## C++

```
// C++ program to find largest and smallest
// characters in a string.
#include <iostream>
using namespace std;

// function that return the largest alphabet.
char largest_alphabet(char a[], int n)
{
    // initializing max alphabet to 'a'
    char max = 'A';

    // find largest alphabet
    for (int i=0; i<n; i++)   
        if (a[i] > max)
            max = a[i];   

    // returning largest element
    return max;
}

// function that return the smallest alphabet
char smallest_alphabet(char a[], int n)
{
    // initializing smallest alphabet to 'z'
    char min = 'z';

    // find smallest alphabet
    for (int i=0; i<n-1; i++)   
        if (a[i] < min)
            min = a[i];   

    // returning smallest alphabet
    return min;
}

// Driver Code
int main()
{
    // Character array
    char a[]= "GeEksforGeeks";

    // Calculating size of the string
    int size = sizeof(a) / sizeof(a[0]);

    // calling functions and print returned value
    cout << "Largest and smallest alphabet is : ";

    cout << largest_alphabet(a,size)<< " and ";
    cout << smallest_alphabet(a,size)<<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest and 
// smallest characters in a string.
public class GFG {    

    // function that return the largest alphabet.
    static char largest_alphabet(String a, int n)
    {
        // initializing max alphabet to 'a'
        char max = 'A';

        // find largest alphabet
        for (int i=0; i<n; i++)   
            if (a.charAt(i) > max)
                max = a.charAt(i);   

        // returning largest element
        return max;
    }

    // function that return the smallest alphabet
    static char smallest_alphabet(String a, int n)
    {
        // initializing smallest alphabet to 'z'
        char min = 'z';

        // find smallest alphabet
        for (int i=0; i<n-1; i++)   
            if (a.charAt(i) < min)
                min = a.charAt(i);   

        // returning smallest alphabet
        return min;
    }

    // Driver Code
    public static void main(String args[])
    {
        // Input String
        String a= "GeEksforGeeks";

        // Calculating size of the string
        int size = a.length();

        // calling functions and print returned value
        System.out.print("Largest and smallest alphabet is : ");

        System.out.print(largest_alphabet(a,size) + " and ");
        System.out.println(smallest_alphabet(a,size));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find largest and 
# smallest characters in a string

# Function that return the largest alphabet
def largest_alphabet(a, n) :

    # Initializing max alphabet to 'a'
    max = 'A'

    # Find largest alphabet
    for i in range(n) :
        if (a[i] > max):
            max = a[i]

    # Returning largest element
    return max

# Function that return the smallest alphabet
def smallest_alphabet(a, n) :

    # Initializing smallest alphabet to 'z'
    min = 'z';

    # Find smallest alphabet
    for i in range (n - 1) :
        if (a[i] < min):
            min = a[i]

    # Returning smallest alphabet
    return min

# Driver code
if __name__ == '__main__' :

    # Character array
    a = "GeEksforGeeks"

    # Calculating size of the string
    size = len(a)

    # Calling functions and print returned value
    print( "Largest and smallest alphabet is : ", end = "")

    print(largest_alphabet(a, size), end = " and ")
    print(smallest_alphabet(a, size))

# This code is contributed by 'rishabh_jain'
```

## C#

```
// C# program to find largest and
// smallest characters in a string.
using System;

class GFG {    

    // function that return the
    // largest alphabet.
    static char largest_alphabet(String a,
                                 int n)
    {

        // initializing max
        // alphabet to 'a'
        char max = 'A';

        // find largest alphabet
        for (int i = 0; i < n; i++)
            if (a[i] > max)
                max = a[i];

        // returning largest element
        return max;
    }

    // function that return the
    // smallest alphabet
    static char smallest_alphabet(String a,
                                  int n)
    {

        // initializing smallest
        // alphabet to 'z'
        char min = 'z';

        // find smallest alphabet
        for (int i = 0; i < n - 1; i++)
            if (a[i] < min)
                min = a[i];

        // returning smallest alphabet
        return min;
    }

    // Driver Code
    public static void Main()
    {
        // Input String
        String a= "GeEksforGeeks";

        // Calculating size
        // of the string
        int size = a.Length;

        // calling functions and
        // print returned value
        Console.Write("Largest and smallest alphabet is : ");

        Console.Write(largest_alphabet(a, size) + " and ");
        Console.Write(smallest_alphabet(a, size));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find largest and smallest
// characters in a string.

// function that return the largest alphabet.
function largest_alphabet($a, $n)
{
    // Initializing max alphabet to 'a'
    $max = 'A';

    // Find largest alphabet
    for ($i = 0; $i < $n; $i++)
        if ($a[$i] > $max)
            $max = $a[$i];

    // Returning largest element
    return $max;
}

// function that return the smallest alphabet
function smallest_alphabet($a, $n)
{
    // initializing smallest alphabet to 'z'
    $min = 'z';

    // find smallest alphabet
    for ($i = 0; $i < $n-1; $i++)
        if ($a[$i] < $min)
            $min = $a[$i];

    // returning smallest alphabet
    return $min;
}

// Driver Code

    // Character array
    $a = "GeEksforGeeks";

    // Calculating size of the string
    $size = strlen($a);

    // calling functions and print returned value
    echo "Largest and smallest alphabet is : ";

    echo largest_alphabet($a, $size). " and ";
    echo smallest_alphabet($a, $size);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find largest and
    // smallest characters in a string.

    // function that return the
    // largest alphabet.
    function largest_alphabet(a, n)
    {

        // initializing max
        // alphabet to 'a'
        let max = 'A';

        // find largest alphabet
        for (let i = 0; i < n; i++)
            if (a[i].charCodeAt() > max.charCodeAt())
                max = a[i];

        // returning largest element
        return max;
    }

    // function that return the
    // smallest alphabet
    function smallest_alphabet(a, n)
    {

        // initializing smallest
        // alphabet to 'z'
        let min = 'z';

        // find smallest alphabet
        for (let i = 0; i < n - 1; i++)
            if (a[i].charCodeAt() < min.charCodeAt())
                min = a[i];

        // returning smallest alphabet
        return min;
    }

    // Input String
    let a= "GeEksforGeeks";

    // Calculating size
    // of the string
    let size = a.length;

    // calling functions and
    // print returned value
    document.write("Largest and smallest alphabet is : ");

    document.write(largest_alphabet(a, size) + " and ");
    document.write(smallest_alphabet(a, size));

</script>
```

**输出:**

```
Largest and smallest alphabet is : s and E
```

本文由**萨赫勒拉杰普特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。