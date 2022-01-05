# 打印给定字符串数组中的所有字谜对

> 原文:[https://www . geesforgeks . org/print-pairs-anagrams-给定-array-strings/](https://www.geeksforgeeks.org/print-pairs-anagrams-given-array-strings/)

给定一个字符串数组，查找给定数组中的所有字谜对。
**例:**

```
Input: arr[] =  {"geeksquiz", "geeksforgeeks", "abcd",
                 "forgeeksgeeks", "zuiqkeegs"};
Output: (geeksforgeeks, forgeeksgeeks), (geeksquiz, zuiqkeegs)
```

我们可以通过计数数组[在线性时间](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)内找到两个字符串是否为字谜(见本[方法二)。
一个简单的发现是否所有的字谜对的方法是运行两个嵌套循环。外部循环逐个挑选所有字符串。内部循环检查剩余的字符串是否是由外部循环挑选的字符串的字谜。
以下是本办法的实施情况:](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

/* function to check whether two strings are anagram of each other */
bool areAnagram(string str1, string str2)
{
    // Create two count arrays and initialize all values as 0
    int count[NO_OF_CHARS] = {0};
    int i;

    // For each character in input strings, increment count in
    // the corresponding count array
    for (i = 0; str1[i] && str2[i];  i++)
    {
        count[str1[i]]++;
        count[str2[i]]--;
    }

    // If both strings are of different length. Removing this condition
    // will make the program fail for strings like "aaca" and "aca"
    if (str1[i] || str2[i])
      return false;

    // See if there is any non-zero value in count array
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count[i])
            return false;
     return true;
}

// This function prints all anagram pairs in a given array of strings
void findAllAnagrams(string arr[], int n)
{
    for (int i = 0; i < n; i++)
        for (int j = i+1; j < n; j++)
            if (areAnagram(arr[i], arr[j]))
                cout << arr[i] << " is anagram of " << arr[j] << endl;
}

/* Driver program to test to print printDups*/
int main()
{
    string arr[] = {"geeksquiz", "geeksforgeeks", "abcd",
                    "forgeeksgeeks", "zuiqkeegs"};
    int n = sizeof(arr)/sizeof(arr[0]);
    findAllAnagrams(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Print all pairs of
// anagrams in a given array of strings
public class GFG
{
    static final int NO_OF_CHARS = 256;

    /* function to check whether two
    strings are anagram of each other */
    static boolean areAnagram(String str1, String str2)
    {
        // Create two count arrays and initialize
        // all values as 0
        int[] count = new int[NO_OF_CHARS];
        int i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i < str1.length() && i < str2.length();
                                                   i++)
        {
            count[str1.charAt(i)]++;
            count[str2.charAt(i)]--;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.length() != str2.length())
          return false;

        // See if there is any non-zero value in
        // count array
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count[i] != 0)
                return false;
         return true;
    }

    // This function prints all anagram pairs in a
    // given array of strings
    static void findAllAnagrams(String arr[], int n)
    {
        for (int i = 0; i < n; i++)
            for (int j = i+1; j < n; j++)
                if (areAnagram(arr[i], arr[j]))
                    System.out.println(arr[i] +
                       " is anagram of " + arr[j]);
    }

    /* Driver program to test to print printDups*/
    public static void main(String args[])
    {
        String arr[] = {"geeksquiz", "geeksforgeeks",
                        "abcd", "forgeeksgeeks",
                        "zuiqkeegs"};
        int n = arr.length;
        findAllAnagrams(arr, n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find
# best meeting point in 2D array
NO_OF_CHARS = 256

# function to check whether two strings
# are anagram of each other
def areAnagram(str1: str, str2: str) -> bool:

    # Create two count arrays and
    # initialize all values as 0
    count = [0] * NO_OF_CHARS
    i = 0

    # For each character in input strings,
    # increment count in the corresponding
    # count array
    while i < len(str1) and i < len(str2):
        count[ord(str1[i])] += 1
        count[ord(str2[i])] -= 1
        i += 1

    # If both strings are of different length.
    # Removing this condition will make the program
    # fail for strings like "aaca" and "aca"
    if len(str1) != len(str2):
        return False

    # See if there is any non-zero value
    # in count array
    for i in range(NO_OF_CHARS):
        if count[i]:
            return False
        return True

# This function prints all anagram pairs
# in a given array of strings
def findAllAnagrams(arr: list, n: int):
    for i in range(n):
        for j in range(i + 1, n):
            if areAnagram(arr[i], arr[j]):
                print(arr[i], "is anagram of", arr[j])

# Driver Code
if __name__ == "__main__":

    arr = ["geeksquiz", "geeksforgeeks",
           "abcd", "forgeeksgeeks", "zuiqkeegs"]
    n = len(arr)
    findAllAnagrams(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to Print all pairs of
// anagrams in a given array of strings
using System;

class GFG
{
    static int NO_OF_CHARS = 256;

    /* function to check whether two
    strings are anagram of each other */
    static bool areAnagram(String str1, String str2)
    {
        // Create two count arrays and initialize
        // all values as 0
        int[] count = new int[NO_OF_CHARS];
        int i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i < str1.Length &&
                    i < str2.Length; i++)
        {
            count[str1[i]]++;
            count[str2[i]]--;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.Length != str2.Length)
        return false;

        // See if there is any non-zero value in
        // count array
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count[i] != 0)
                return false;
        return true;
    }

    // This function prints all anagram pairs in a
    // given array of strings
    static void findAllAnagrams(String []arr, int n)
    {
        for (int i = 0; i < n; i++)
            for (int j = i+1; j < n; j++)
                if (areAnagram(arr[i], arr[j]))
                    Console.WriteLine(arr[i] +
                    " is anagram of " + arr[j]);
    }

    /* Driver program to test to print printDups*/
    public static void Main()
    {
        String []arr = {"geeksquiz", "geeksforgeeks",
                        "abcd", "forgeeksgeeks",
                        "zuiqkeegs"};
        int n = arr.Length;
        findAllAnagrams(arr, n);
    }
}

// This code is contributed by nitin mittal
```

## java 描述语言

```
<script>
// JavaScript program to find
// best meeting point in 2D array
let NO_OF_CHARS = 256

// function to check whether two strings
// are anagram of each other
function areAnagram(str1, str2){

    // Create two count arrays and
    // initialize all values as 0
    let count = [];
    for(let i = 0;i< NO_OF_CHARS;i++)
        count[i] = 0;
    let i = 0;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    while(i < (str1).length && i < (str2).length){
        count[ord(str1[i])] += 1;
        count[ord(str2[i])] -= 1;
        i += 1;
    }

    // If both strings are of different length.
    // Removing this condition will make the program
    // fail for strings like "aaca" and "aca"
    if ( (str1).length !=  (str2).length)
        return false;

    // See if there is any non-zero value
    // in count array
    for(let i = 0; i < NO_OF_CHARS; i++){
        if (count[i])
            return false;
        return True;
     }
}

// This function prints all anagram pairs
// in a given array of strings
function findAllAnagrams(arr, n){
    for(let i = 0; i < n; i++){
        for(let j = i + 1; j < n; j++){
            if areAnagram(arr[i], arr[j])
                document.write(arr[i]+"is anagram of"+arr[j])
        }
    }
}
    // Driver Code
    let arr = ["geeksquiz", "geeksforgeeks",
           "abcd", "forgeeksgeeks", "zuiqkeegs"];
    let n = (arr).length;
    findAllAnagrams(arr, n);

// This code is contributed by Rohitsingh07052.
</script>
```

**输出:**

```
geeksquiz is anagram of zuiqkeegs
geeksforgeeks is anagram of forgeeksgeeks
```

上述解的时间复杂度为 O(n <sup>2</sup> *m)，其中 n 为字符串个数，m 为字符串最大长度。
**优化:**
我们可以使用以下方法优化上述解决方案。
1) **使用排序:**我们可以对字符串数组进行排序，这样所有的字谜就都在一起了。然后通过线性遍历排序后的数组来打印所有的字谜。这个解决方案的时间复杂度是 O(mnLogn)(我们将在排序中进行 O(nLogn)比较，并且比较将花费 O(m)时间)
2) **使用哈希:**我们可以为一个字符串构建一个哈希函数，如异或或所有字符的 ASCII 值之和。使用这样的哈希函数，我们可以构建一个哈希表。在构建哈希表时，我们可以检查一个值是否已经被哈希。如果是，我们可以调用 areAnagrams()来检查两个字符串是否实际上是字谜(注意异或或 ASCII 值的和是不够的，参见 Kaushik Lele 的评论[这里](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/) )
本文由 Abhishek 供稿。如果您发现任何不正确的地方或想分享更多关于上述主题的信息，请写评论。