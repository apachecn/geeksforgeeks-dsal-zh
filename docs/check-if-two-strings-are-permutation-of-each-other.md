# 检查两个字符串是否相互排列

> 原文:[https://www . geesforgeks . org/check-if-two-string-相互排列/](https://www.geeksforgeeks.org/check-if-two-strings-are-permutation-of-each-other/)

写一个函数，检查两个给定的字符串是否是彼此的[置换](http://en.wikipedia.org/wiki/Permutation)。一个字符串的排列是另一个包含相同字符的字符串，只有字符的顺序可以不同。例如，“abcd”和“dabc”是相互置换的。

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/anagram-1587115620/1)

**方法 1(使用排序)**
1)对两个字符串进行排序
2)比较排序后的字符串

## C++

```
// C++ program to check whether two strings are
// Permutations of each other
#include <bits/stdc++.h>
using namespace std;

/* function to check whether two strings are
   Permutation of each other */
bool arePermutation(string str1, string str2)
{
    // Get lengths of both strings
    int n1 = str1.length();
    int n2 = str2.length();

    // If length of both strings is not same,
    // then they cannot be Permutation
    if (n1 != n2)
      return false;

    // Sort both strings
    sort(str1.begin(), str1.end());
    sort(str2.begin(), str2.end());

    // Compare sorted strings
    for (int i = 0; i < n1;  i++)
       if (str1[i] != str2[i])
         return false;

    return true;
}

/* Driver program to test to print printDups*/
int main()
{
    string str1 = "test";
    string str2 = "ttew";
    if (arePermutation(str1, str2))
      printf("Yes");
    else
      printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether two strings are
// Permutations of each other
import java.util.*;
class GfG {

/* function to check whether two strings are
Permutation of each other */
static boolean arePermutation(String str1, String str2)
{
    // Get lengths of both strings
    int n1 = str1.length();
    int n2 = str2.length();

    // If length of both strings is not same,
    // then they cannot be Permutation
    if (n1 != n2)
    return false;
    char ch1[] = str1.toCharArray();
    char ch2[] = str2.toCharArray();

    // Sort both strings
    Arrays.sort(ch1);
    Arrays.sort(ch2);

    // Compare sorted strings
    for (int i = 0; i < n1; i++)
    if (ch1[i] != ch2[i])
        return false;

    return true;
}

/* Driver program to test to print printDups*/
public static void main(String[] args)
{
    String str1 = "test";
    String str2 = "ttew";
    if (arePermutation(str1, str2))
    System.out.println("Yes");
    else
    System.out.println("No");

}
}
```

## 蟒蛇 3

```
# Python3 program to check whether two
# strings are Permutations of each other

# function to check whether two strings
# are Permutation of each other */
def arePermutation(str1, str2):

    # Get lengths of both strings
    n1 = len(str1)
    n2 = len(str2)

    # If length of both strings is not same,
    # then they cannot be Permutation
    if (n1 != n2):
        return False

    # Sort both strings
    a = sorted(str1)
    str1 = " ".join(a)
    b = sorted(str2)
    str2 = " ".join(b)

    # Compare sorted strings
    for i in range(0, n1, 1):
        if (str1[i] != str2[i]):
            return False

    return True

# Driver Code
if __name__ == '__main__':
    str1 = "test"
    str2 = "ttew"
    if (arePermutation(str1, str2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to check whether two strings are
// Permutations of each other
using System;

class GfG
{

/* function to check whether two strings are
Permutation of each other */
static bool arePermutation(String str1, String str2)
{
    // Get lengths of both strings
    int n1 = str1.Length;
    int n2 = str2.Length;

    // If length of both strings is not same,
    // then they cannot be Permutation
    if (n1 != n2)
        return false;
    char []ch1 = str1.ToCharArray();
    char []ch2 = str2.ToCharArray();

    // Sort both strings
    Array.Sort(ch1);
    Array.Sort(ch2);

    // Compare sorted strings
    for (int i = 0; i < n1; i++)
        if (ch1[i] != ch2[i])
            return false;

    return true;
}

/* Driver code*/
public static void Main(String[] args)
{
    String str1 = "test";
    String str2 = "ttew";
    if (arePermutation(str1, str2))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to check whether two
// strings are Permutations of each other

// Function to check whether two strings are
// Permutation of each other
function arePermutation(str1, str2)
{

    // Get lengths of both strings
    let n1 = str1.length;
    let n2 = str2.length;

    // If length of both strings is not same,
    // then they cannot be Permutation
    if (n1 != n2)
        return false;

    let ch1 = str1.split(' ');
    let ch2 = str2.split(' ');

    // Sort both strings
    ch1.sort();
    ch2.sort();

    // Compare sorted strings
    for(let i = 0; i < n1; i++)
        if (ch1[i] != ch2[i])
            return false;

    return true;
}

// Driver Code
let str1 = "test";
let str2 = "ttew";

if (arePermutation(str1, str2))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by suresh07

</script>
```

**输出:**

```
No
```

**时间复杂度:**该方法的时间复杂度取决于所使用的排序技术。在上面的实现中，在最坏的情况下使用快速排序(可能是 O(n^2)。如果我们使用像合并排序这样的 O(nLogn)排序算法，那么复杂度就变成 O(nLogn)

**方法 2(计数字符)**
该方法假设两个字符串中可能的字符集都很小。在下面的实现中，假设使用 8 位存储字符，并且可能有 256 个字符。
1)为两个字符串创建大小为 256 的计数数组。将计数数组中的所有值初始化为 0。
2)遍历两个字符串的每个字符，并增加相应计数数组中的字符数。
3)比较计数阵列。如果两个计数数组相同，则返回 true。

## C++

```
// C++ program to check whether two strings are
// Permutations of each other
#include <bits/stdc++.h>
using namespace std;
# define NO_OF_CHARS 256

/* function to check whether two strings are
   Permutation of each other */
bool arePermutation(string str1, string str2)
{
    // Create 2 count arrays and initialize
    // all values as 0
    int count1[NO_OF_CHARS] = {0};
    int count2[NO_OF_CHARS] = {0};
    int i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for (i = 0; str1[i] && str2[i];  i++)
    {
        count1[str1[i]]++;
        count2[str2[i]]++;
    }

    // If both strings are of different length.
    // Removing this condition will make the
    // program fail for strings like "aaca"
    // and "aca"
    if (str1[i] || str2[i])
      return false;

    // Compare count arrays
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count1[i] != count2[i])
            return false;

    return true;
}

/* Driver program to test to print printDups*/
int main()
{
    string str1 = "geeksforgeeks";
    string str2 = "forgeeksgeeks";
    if ( arePermutation(str1, str2) )
      printf("Yes");
    else
      printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if two strings
// are Permutations of each other
import java.io.*;
import java.util.*;

class GFG{

    static int NO_OF_CHARS = 256;

    /* function to check whether two strings
    are Permutation of each other */
    static boolean arePermutation(char str1[], char str2[])
    {
        // Create 2 count arrays and initialize
        // all values as 0
        int count1[] = new int [NO_OF_CHARS];
        Arrays.fill(count1, 0);
        int count2[] = new int [NO_OF_CHARS];
        Arrays.fill(count2, 0);
        int i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i <str1.length && i < str2.length ;
                                                 i++)
        {
            count1[str1[i]]++;
            count2[str2[i]]++;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.length != str2.length)
            return false;

        // Compare count arrays
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    /* Driver program to test to print printDups*/
    public static void main(String args[])
    {
        char str1[] = ("geeksforgeeks").toCharArray();
        char str2[] = ("forgeeksgeeks").toCharArray();

        if ( arePermutation(str1, str2) )
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to check if two strings are
# Permutations of each other
NO_OF_CHARS = 256

# Function to check whether two strings are
# Permutation of each other
def arePermutation(str1, str2):

    # Create two count arrays and initialize
    # all values as 0
    count1 = [0] * NO_OF_CHARS
    count2 = [0] * NO_OF_CHARS

    # For each character in input strings,
    # increment count in the corresponding
    # count array
    for i in str1:
        count1[ord(i)]+=1

    for i in str2:
        count2[ord(i)]+=1

    # If both strings are of different length.
    # Removing this condition will make the
    # program fail for strings like
    # "aaca" and "aca"
    if len(str1) != len(str2):
        return 0

    # Compare count arrays
    for i in xrange(NO_OF_CHARS):
        if count1[i] != count2[i]:
            return 0

    return 1

# Driver program to test the above functions
str1 = "geeksforgeeks"
str2 = "forgeeksgeeks"
if arePermutation(str1, str2):
    print "Yes"
else:
    print "No"

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check if two strings
// are Permutations of each other
using System;
class GFG{

    static int NO_OF_CHARS = 256;

    /* function to check whether two strings
    are Permutation of each other */
    static bool arePermutation(char []str1, char []str2)
    {
        // Create 2 count arrays and initialize
        // all values as 0
        int []count1 = new int [NO_OF_CHARS];
        int []count2 = new int [NO_OF_CHARS];
        int i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i <str1.Length && i < str2.Length ;
                                                i++)
        {
            count1[str1[i]]++;
            count2[str2[i]]++;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.Length != str2.Length)
            return false;

        // Compare count arrays
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    /* Driver code*/
    public static void Main(String []args)
    {
        char []str1 = ("geeksforgeeks").ToCharArray();
        char []str2 = ("forgeeksgeeks").ToCharArray();

        if ( arePermutation(str1, str2) )
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to check if two strings
// are Permutations of each other
let NO_OF_CHARS = 256;

/* Function to check whether two strings
are Permutation of each other */
function arePermutation(str1, str2)
{

    // Create 2 count arrays and initialize
    // all values as 0
    let count1 = Array(NO_OF_CHARS);
    let count2 = Array(NO_OF_CHARS);
    count1.fill(0);
    count2.fill(0);
    let i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for(i = 0;
        i < str1.length && i < str2.length;
        i++)
    {
        count1[str1[i]]++;
        count2[str2[i]]++;
    }

    // If both strings are of different length.
    // Removing this condition will make the program
    // fail for strings like "aaca" and "aca"
    if (str1.length != str2.length)
        return false;

    // Compare count arrays
    for(i = 0; i < NO_OF_CHARS; i++)
        if (count1[i] != count2[i])
            return false;

    return true;
}

// Driver code  
let str1 = ("geeksforgeeks").split('');
let str2 = ("forgeeksgeeks").split('');

if (arePermutation(str1, str2) )
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
Yes
```

上面的实现可以进一步仅使用一个计数数组而不是两个。我们可以在 str1 中增加字符计数数组中的值，在 str2 中减少字符计数数组中的值。最后，如果所有计数值都是 0，那么这两个字符串是相互置换的。感谢[高手](https://www.geeksforgeeks.org/archives/18752/comment-page-1#comment-8051)提出这个优化。

## C++

```
// C++ function to check whether two strings are
// Permutations of each other
bool arePermutation(string str1, string str2)
{
    // Create a count array and initialize all
    // values as 0
    int count[NO_OF_CHARS] = {0};
    int i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for (i = 0; str1[i] && str2[i];  i++)
    {
        count[str1[i]]++;
        count[str2[i]]--;
    }

    // If both strings are of different length.
    // Removing this condition  will make the
    // program fail for strings like "aaca" and
    // "aca"
    if (str1[i] || str2[i])
      return false;

    // See if there is any non-zero value in
    // count array
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count[i])
            return false;
     return true;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java function to check whether two strings are 
// Permutations of each other
static boolean arePermutation(char str1[], char str2[])
{

    // Create a count array and initialize all
    // values as 0
    int count[] = new int[NO_OF_CHARS];
    int i;

    // For each character in input strings, 
    // increment count in the corresponding 
    // count array
    for (i = 0; str1[i] && str2[i];  i++)
    {
        count[str1[i]]++;
        count[str2[i]]--;
    }

    // If both strings are of different length.
    // Removing this condition  will make the
    // program fail for strings like "aaca" and
    // "aca"
    if (str1[i] || str2[i])
      return false;

    // See if there is any non-zero value in 
    // count array
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count[i] != 0)
            return false;
     return true;
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 function to check whether two strings are
# Permutations of each other
def arePermutation(str1, str2):

    # Create a count array and initialize all
    # values as 0
    count = [0 for i in range(NO_OF_CHARS)]   
    i = 0

    # For each character in input strings,
    # increment count in the corresponding
    # count array
    while(str1[i] and str2[i]):

        count[str1[i]] += 1
        count[str2[i]] -= 1

    # If both strings are of different length.
    # Removing this condition  will make the
    # program fail for strings like "aaca" and
    # "aca"
    if (str1[i] or str2[i]):
      return False;

    # See if there is any non-zero value in
    # count array
    for i in range(NO_OF_CHARS):
        if (count[i]):
            return False;
    return True;

# This code is contributed by pratham76.
```

## C#

```
// C# function to check whether two strings are 
// Permutations of each other
static bool arePermutation(char[] str1, char[] str2)
{

    // Create a count array and initialize all
    // values as 0
    int[] count = new int[NO_OF_CHARS];
    int i;

    // For each character in input strings, 
    // increment count in the corresponding 
    // count array
    for (i = 0; str1[i] && str2[i];  i++)
    {
        count[str1[i]]++;
        count[str2[i]]--;
    }

    // If both strings are of different length.
    // Removing this condition  will make the
    // program fail for strings like "aaca" and
    // "aca"
    if (str1[i] || str2[i])
      return false;

    // See if there is any non-zero value in 
    // count array
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count[i] != 0)
            return false;
     return true;
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript function to check whether two strings are
// Permutations of each other

function arePermutation(str1,str2)
{
    // Create a count array and initialize all
    // values as 0
    let count = new Array(NO_OF_CHARS);
    let i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for (i = 0; str1[i] && str2[i];  i++)
    {
        count[str1[i]]++;
        count[str2[i]]--;
    }

    // If both strings are of different length.
    // Removing this condition  will make the
    // program fail for strings like "aaca" and
    // "aca"
    if (str1[i] || str2[i])
      return false;

    // See if there is any non-zero value in
    // count array
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count[i] != 0)
            return false;
     return true;
}

// This code is contributed by patel2127
</script>
```

如果可能的字符集只包含英文字母，那么我们可以将数组的大小减少到 58，并使用*str[I]–“A”*作为计数数组的索引，因为“A”的 ASCII 值是 65，“B”是 66，…..，Z 是 90，“a”是 97，“b”是 98，……，“Z”是 122。这将进一步优化这种方法。

**时间复杂度:** O(n)
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。