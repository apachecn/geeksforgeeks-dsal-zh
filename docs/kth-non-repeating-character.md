# 第 K 个不重复字符

> 原文:[https://www.geeksforgeeks.org/kth-non-repeating-character/](https://www.geeksforgeeks.org/kth-non-repeating-character/)

给定一个字符串和一个数字 k，找到字符串中第 k 个不重复的字符。考虑一个包含大量字符和一个小字符集的大输入字符串。如何只对输入字符串做一次遍历就能找到字符？
**例:**

```
Input : str = geeksforgeeks, k = 3
Output : r
First non-repeating character is f,
second is o and third is r.

Input : str = geeksforgeeks, k = 2
Output : o

Input : str = geeksforgeeks, k = 4
Output : Less than k non-repeating
         characters in input.
```

这个问题主要是[第一个不重复字符问题](https://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)的延伸。
**方法 1(简单:O(n)<sup>2</sup>)**
一个简单的解决方法是运行两个循环。从左侧开始穿越。对于每个字符，检查它是否重复。如果字符不重复，增加非重复字符的计数。当计数变成 k 时，返回字符。
**方法 2 (O(n)但需要两次遍历)**

1.  创建一个空散列。
2.  从左到右扫描输入字符串，并在哈希中插入值及其计数。
3.  从左到右扫描输入字符串，并保留计数超过 1 的字符数。当计数变为 k 时，返回字符。

**方法 3 (O(n)并且需要一次遍历)**
想法是使用两个大小为 256 的辅助数组(假设使用 8 位存储字符)。这两个阵列是:

```
count[x] : Stores count of character 'x' in str.
           If x is not present, then it stores 0.

index[x] : Stores indexes of non-repeating characters
           in str. If a character 'x' is not  present
           or x is repeating, then it stores  a value
           that cannot be a valid index in str[]. For 
           example, length of string.
```

1.  将 count[]中的所有值初始化为 0，将 index[]中的所有值初始化为 n，其中 n 是字符串长度。
2.  遍历输入字符串 str，并对每个字符 c = str[i]执行以下操作。
    *   递增计数[x]。
    *   如果计数[x]为 1，则将 x 的索引存储在索引[x]中，即索引[x] = i
    *   如果计数[x]为 2，则从索引[]中移除 x，即索引[x] = n
3.  现在，index[]具有所有非重复字符的索引。按照递增的顺序对索引[]进行排序，以便我们在索引[k]处获得第 k 个最小元素。请注意，此步骤需要 O(1)个时间，因为索引[]中只有 256 个元素。

下面是上述想法的实现。

## C++

```
// C++ program to find k'th non-repeating character
// in a string
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 256;

// Returns index of k'th non-repeating character in
// given string str[]
int kthNonRepeating(string str, int k)
{
    int n = str.length();

    // count[x] is going to store count of
    // character 'x' in str. If x is not present,
    // then it is going to store 0.
    int count[MAX_CHAR];

    // index[x] is going to store index of character
    // 'x' in str.  If x is not  present or x is
    // repeating, then it is going to store  a value
    // (for example, length of string) that cannot be
    // a valid index in str[]
    int index[MAX_CHAR];

    // Initialize counts of all characters and indexes
    // of non-repeating  characters.
    for (int i = 0; i < MAX_CHAR; i++)
    {
        count[i] = 0;
        index[i] = n;  // A value more than any index
                       // in str[]
    }

    // Traverse the input string
    for (int i = 0; i < n; i++)
    {
        // Find current character and increment its
        // count
        char x = str[i];
        ++count[x];

        // If this is first occurrence, then set value
        // in index as index of it.
        if (count[x] == 1)
            index[x] = i;

        // If character repeats, then remove it from
        // index[]
        if (count[x] == 2)
            index[x] = n;
    }

    // Sort index[] in increasing order.  This step
    // takes O(1) time as size of index is 256 only
    sort(index, index+MAX_CHAR);

    // After sorting, if index[k-1] is value, then
    // return it, else return -1.
    return (index[k-1] != n)? index[k-1] : -1;
}

// Driver code
int main()
{
   string str = "geeksforgeeks";
   int k = 3;
   int res = kthNonRepeating(str, k);
   (res == -1)? cout << "There are less than k non-"
                        "repeating characters"
              : cout << "k'th non-repeating character"
                       " is  "<< str[res];
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k'th non-repeating character
// in a string

import java.util.Arrays;

class GFG
{
    public static int MAX_CHAR = 256;

    // Returns index of k'th non-repeating character in
    // given string str[]
    static int kthNonRepeating(String str, int k)
    {
        int n = str.length();

        // count[x] is going to store count of
        // character 'x' in str. If x is not present,
        // then it is going to store 0.
        int[] count = new int[MAX_CHAR];

        // index[x] is going to store index of character
        // 'x' in str.  If x is not  present or x is
        // repeating, then it is going to store  a value
        // (for example, length of string) that cannot be
        // a valid index in str[]
        int[] index = new int[MAX_CHAR];

        // Initialize counts of all characters and indexes
        // of non-repeating  characters.
        for (int i = 0; i < MAX_CHAR; i++)
        {
            count[i] = 0;
            index[i] = n;  // A value more than any index
                           // in str[]
        }

        // Traverse the input string
        for (int i = 0; i < n; i++)
        {
            // Find current character and increment its
            // count
            char x = str.charAt(i);
            ++count[x];

            // If this is first occurrence, then set value
            // in index as index of it.
            if (count[x] == 1)
                index[x] = i;

            // If character repeats, then remove it from
            // index[]
            if (count[x] == 2)
                index[x] = n;
        }

        // Sort index[] in increasing order.  This step
        // takes O(1) time as size of index is 256 only
        Arrays.sort(index);

        // After sorting, if index[k-1] is value, then
        // return it, else return -1.
        return (index[k-1] != n)? index[k-1] : -1;
    }

    // driver program
    public static void main (String[] args)
    {
        String str = "geeksforgeeks";
        int k = 3;
        int res = kthNonRepeating(str, k);

        System.out.println(res == -1 ? "There are less than k non-repeating characters" :
                           "k'th non-repeating character is  " + str.charAt(res));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to find k'th
# non-repeating character in a string
MAX_CHAR = 256

# Returns index of k'th non-repeating
# character in given string str[]
def kthNonRepeating(str, k):

    n = len(str)

    # count[x] is going to store count of 
    # character 'x' in str. If x is not
    # present, then it is going to store 0.
    count = [0] * MAX_CHAR

    # index[x] is going to store index of
    # character 'x' in str. If x is not
    # present or x is repeating, then it
    # is going to store a value (for example,
    # length of string) that cannot be a valid
    # index in str[]
    index = [0] * MAX_CHAR

    # Initialize counts of all characters
    # and indexes of non-repeating characters.
    for i in range( MAX_CHAR):
        count[i] = 0
        index[i] = n # A value more than any
                     # index in str[]

    # Traverse the input string
    for i in range(n):

        # Find current character and
        # increment its count
        x = str[i]
        count[ord(x)] += 1

        # If this is first occurrence, then
        # set value in index as index of it.
        if (count[ord(x)] == 1):
            index[ord(x)] = i

        # If character repeats, then remove
        # it from index[]
        if (count[ord(x)] == 2):
            index[ord(x)] = n

    # Sort index[] in increasing order. This step
    # takes O(1) time as size of index is 256 only
    index.sort()

    # After sorting, if index[k-1] is value,
    # then return it, else return -1.
    return index[k - 1] if (index[k - 1] != n) else -1

# Driver code
if __name__ == "__main__":
    str = "geeksforgeeks"
    k = 3
    res = kthNonRepeating(str, k)
    if(res == -1):
        print("There are less than k",
              "non-repeating characters")
    else:
        print("k'th non-repeating character is",
                                       str[res])

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find k'th non-repeating
// character in a string
using System;

class GFG {

    public static int MAX_CHAR = 256;

    // Returns index of k'th non-repeating
    // character in given string str[]
    static int kthNonRepeating(String str, int k)
    {

        int n = str.Length;

        // count[x] is going to store count of
        // character 'x' in str. If x is not
        // present, then it is going to store 0.
        int []count = new int[MAX_CHAR];

        // index[x] is going to store index of
        // character 'x' in str. If x is not
        // present or x is repeating, then it
        // is going to store a value (for
        // example, length of string) that
        // cannot be a valid index in str[]
        int []index = new int[MAX_CHAR];

        // Initialize counts of all characters
        // and indexes of non-repeating
        // characters.
        for (int i = 0; i < MAX_CHAR; i++)
        {
            count[i] = 0;

            // A value more than any index
            // in str[]
            index[i] = n;
        }

        // Traverse the input string
        for (int i = 0; i < n; i++)
        {

            // Find current character and
            // increment its count
            char x = str[i];
            ++count[x];

            // If this is first occurrence,
            // then set value in index as
            // index of it.
            if (count[x] == 1)
                index[x] = i;

            // If character repeats, then
            // remove it from index[]
            if (count[x] == 2)
                index[x] = n;
        }

        // Sort index[] in increasing order.
        // This step takes O(1) time as size
        // of index is 256 only
        Array.Sort(index);

        // After sorting, if index[k-1] is
        // value, then return it, else
        // return -1.
        return (index[k-1] != n) ?
                           index[k-1] : -1;
    }

    // driver program
    public static void Main ()
    {
        String str = "geeksforgeeks";
        int k = 3;
        int res = kthNonRepeating(str, k);

    Console.Write(res == -1 ? "There are less"
         + " than k non-repeating characters" :
            "k'th non-repeating character is "
                                   + str[res]);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>
// Javascript program to find k'th non-repeating character
// in a string

let MAX_CHAR = 256;

// Returns index of k'th non-repeating character in
    // given string str[]
function kthNonRepeating(str,k)
{
    let n = str.length;

        // count[x] is going to store count of
        // character 'x' in str. If x is not present,
        // then it is going to store 0.
        let count = new Array(MAX_CHAR);

        // index[x] is going to store index of character
        // 'x' in str.  If x is not  present or x is
        // repeating, then it is going to store  a value
        // (for example, length of string) that cannot be
        // a valid index in str[]
        let index = new Array(MAX_CHAR);

        // Initialize counts of all characters and indexes
        // of non-repeating  characters.
        for (let i = 0; i < MAX_CHAR; i++)
        {
            count[i] = 0;
            index[i] = n;  // A value more than any index
                           // in str[]
        }

        // Traverse the input string
        for (let i = 0; i < n; i++)
        {
            // Find current character and increment its
            // count
            let x = str[i];
            ++count[x.charCodeAt(0)];

            // If this is first occurrence, then set value
            // in index as index of it.
            if (count[x.charCodeAt(0)] == 1)
                index[x.charCodeAt(0)] = i;

            // If character repeats, then remove it from
            // index[]
            if (count[x.charCodeAt(0)] == 2)
                index[x.charCodeAt(0)] = n;
        }

        // Sort index[] in increasing order.  This step
        // takes O(1) time as size of index is 256 only
        (index).sort(function(a,b){return a-b;});

        // After sorting, if index[k-1] is value, then
        // return it, else return -1.
        return (index[k-1] != n)? index[k-1] : -1;
}

// driver program
let str = "geeksforgeeks";
let k = 3;
let res = kthNonRepeating(str, k);
document.write(res == -1 ? "There are less than k non-repeating characters" :
                           "k'th non-repeating character is  " + str[res]);

// This code is contributed by ab2127
</script>
```

**Output:** 

```
k'th non-repeating character is  r
```

**空间优化解决方案:**
这可以进行空间优化，并且只能使用单索引数组来解决。下面是空间优化解决方案:

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define MAX_CHAR 256
int kthNonRepeating(string input, int k)
{
    int inputLength = input.length();

    /*
     * indexArr will store index of non-repeating
     * characters, inputLength for characters not in input
     * and inputLength+1 for repeated characters.
     */
    int indexArr[MAX_CHAR];

    // initialize all values in indexArr as inputLength.
    for (int i = 0; i < MAX_CHAR; i++) {
        indexArr[i] = inputLength;
    }
    for (int i = 0; i < inputLength; i++) {
        char c = input[i];
        if (indexArr == inputLength) {
            indexArr = i;
        }
        else {
            indexArr = inputLength + 2;
        }
    }

    sort(indexArr, indexArr + MAX_CHAR);
    return (indexArr[k - 1] != inputLength)
               ? indexArr[k - 1]
               : -1;
}

int main()
{
    string input = "geeksforgeeks";
    int k = 3;
    int res = kthNonRepeating(input, k);
    if (res == -1)
        cout << "There are less than k non-repeating "
                "characters";
    else
        cout << "k'th non-repeating character is  "
             << input[res];
    return 0;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class GFG {
    public static int MAX_CHAR = 256;

    public static void main (String[] args) 
    {
        final String input = "geeksforgeeks";
        int k = 3;
        int res = kthNonRepeating(input, k);

        System.out.println(res == -1 ? "There are less than k non-repeating characters" :
                           "k'th non-repeating character is  " + input.charAt(res));
    }

    public static int kthNonRepeating(final String input, final int k) {
        final int inputLength = input.length();

        /*
         * indexArr will store index of non-repeating characters,
         * inputLength for characters not in input and
         * inputLength+1 for repeated characters.
         */
        final int[] indexArr = new int[MAX_CHAR];

        // initialize all values in indexArr as inputLength.
        Arrays.fill(indexArr, inputLength);

        for (int i = 0; i < inputLength ; i++) {
            final char c = input.charAt(i);
            if (indexArr == inputLength) {
                indexArr = i;
            } else {
                indexArr = inputLength + 2;
            }
        }

        Arrays.sort(indexArr);

        return (indexArr[k-1] != inputLength) ? indexArr[k-1] : -1;
    }
}
// Contributed by AK
```

## 蟒蛇 3

```
MAX_CHAR = 256

def kthNonRepeating(Input,k):
    inputLength = len(Input)

    # indexArr will store index of non-repeating characters,
    # inputLength for characters not in input and
    # inputLength+1 for repeated characters.

    # initialize all values in indexArr as inputLength.
    indexArr = [inputLength for i in range(MAX_CHAR)]

    for i in range(inputLength):
        c = Input[i]
        if (indexArr[ord(c)] == inputLength):
            indexArr[ord(c)] = i
        else:
            indexArr[ord(c)] = inputLength + 2
    indexArr.sort()
    if(indexArr[k - 1] != inputLength):
        return indexArr[k - 1]
    else:
        return -1

Input = "geeksforgeeks"
k = 3
res = kthNonRepeating(Input, k)
if(res == -1):
    print("There are less than k non-repeating characters")
else:
    print("k'th non-repeating character is", Input[res])

# This code is contributed by rag2127
```

## C#

```
using System;

public class GFG
{
    public static int MAX_CHAR = 256;
    static public void Main ()
    {
        string input = "geeksforgeeks"; 
        int k = 3; 
        int res = kthNonRepeating(input, k); 

        Console.WriteLine(res == -1 ? "There are less than k non-repeating characters" : 
                           "k'th non-repeating character is  " + input[res]);
    }

    public static int kthNonRepeating(string input, int k) {
        int inputLength = input.Length;

        /*
         * indexArr will store index of non-repeating characters,
         * inputLength for characters not in input and
         * inputLength+1 for repeated characters.
         */
        int[] indexArr = new int[MAX_CHAR];

        // initialize all values in indexArr as inputLength.
        Array.Fill(indexArr, inputLength);

        for (int i = 0; i < inputLength ; i++) {
            char c = input[i];
            if (indexArr == inputLength) {
                indexArr = i;
            } else {
                indexArr = inputLength + 2;
            }
        }

        Array.Sort(indexArr);
        return (indexArr[k - 1] != inputLength) ? indexArr[k - 1] : -1; 
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

let MAX_CHAR = 256;

function kthNonRepeating(input, k)
{
    let inputLength = input.length;

        /*
         * indexArr will store index of non-repeating characters,
         * inputLength for characters not in input and
         * inputLength+1 for repeated characters.
         */
        let indexArr = new Array(MAX_CHAR);

        // initialize all values in indexArr as inputLength.
        for(let i=0;i<MAX_CHAR;i++)
        {
            indexArr[i]=inputLength;
        }

        for (let i = 0; i < inputLength ; i++) {
            let c = input[i];
            if (indexArr == inputLength) {
                indexArr = i;
            } else {
                indexArr = inputLength + 2;
            }
        }

        (indexArr).sort(function(a,b){return a-b;});

        return (indexArr[k-1] != inputLength) ? indexArr[k-1] : -1;
}

let input = "geeksforgeeks";
let k = 3;
let res = kthNonRepeating(input, k);
document.write(res == -1 ? "There are less than k non-repeating characters" :
                           "k'th non-repeating character is  " + input[res]);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
k'th non-repeating character is  r
```

本文由希瓦姆·古普塔供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息