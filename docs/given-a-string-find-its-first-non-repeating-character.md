# 给定一个字符串，找到它的第一个非重复字符

> 原文:[https://www . geesforgeks . org/给定字符串-查找其第一个非重复字符/](https://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)

给定一个字符串，找到其中的第一个非重复字符。例如，如果输入字符串是“GeeksforGeeks”，那么输出应该是“f”，如果输入字符串是“GeeksQuiz”，那么输出应该是“G”。

![find-first-non-repeated-character-in-a-string](img/b6a262da4da0b0bf9c7db07dcb1adecc.png)

**示例:**

```
Input: "geeksforgeeks"
Explanation:
Step 1: Construct a character count array 
        from the input string.
   ....
  count['e'] = 4
  count['f'] = 1
  count['g'] = 2
  count['k'] = 2
  ……

Step 2: Get the first character who's 
        count is 1 ('f').
```

**<u>方法 1</u> :** [哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)和双字符串方法遍历。
**方法:**如果一个字符在字符串中的频率是单位，则称该字符不重复。现在要找到这样的字符，需要找到字符串中所有字符的频率，并检查哪个字符有**单位频率**。这个任务可以使用 **hash_map** 高效地完成，它将把字符映射到各自的频率，并且我们可以在恒定的时间内同时更新遇到的任何字符的频率。 **ASCII 系统中最大不同字符为 256** 。所以 **hash_map** 的最大尺寸为 **256** 。现在再读一遍字符串，我们发现的第一个字符有一个频率，因为单位是答案。
**算法:**

1.  制作一个**哈希映射**，将字符映射到各自的频率。
2.  使用指针遍历给定的字符串。
3.  增加当前字符在**哈希 _ 映射**中的计数。
4.  现在再次遍历字符串，检查当前字符是否有**频率=1** 。
5.  如果**频率> 1** 继续遍历。
6.  否则**断开**循环，打印当前字符作为答案。

**伪码:**

```
for ( i=0 to str.length())
hash_map[str[i]]++;

for(i=0 to str.length())
  if(hash_map[str[i]]==1)
  return str[i]
  break 
```

## C++

```
// C++ program to find first
// non-repeating character
#include <iostream>
using namespace std;
#define NO_OF_CHARS 256

/* Returns an array of size 256 containing count
of characters in the passed char array */
int* getCharCountArray(char* str)
{
    int* count = (int*)calloc(sizeof(int), NO_OF_CHARS);
    int i;
    for (i = 0; *(str + i); i++)
        count[*(str + i)]++;
    return count;
}

/* The function returns index of first
non-repeating character in a string. If all
characters are repeating then returns -1 */
int firstNonRepeating(char* str)
{
    int* count = getCharCountArray(str);
    int index = -1, i;

    for (i = 0; *(str + i); i++) {
        if (count[*(str + i)] == 1) {
            index = i;
            break;
        }
    }

    // To avoid memory leak
    free(count);
    return index;
}

/* Driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    int index = firstNonRepeating(str);
    if (index == -1)
        cout << "Either all characters are repeating or "
            "string is empty";
    else
        cout << "First non-repeating character is "<<
            str[index];
    getchar();
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to find first
// non-repeating character
#include <stdio.h>
#include <stdlib.h>
#define NO_OF_CHARS 256

/* Returns an array of size 256 containing count
   of characters in the passed char array */
int* getCharCountArray(char* str)
{
    int* count = (int*)calloc(sizeof(int), NO_OF_CHARS);
    int i;
    for (i = 0; *(str + i); i++)
        count[*(str + i)]++;
    return count;
}

/* The function returns index of first
   non-repeating character in a string. If all
   characters are repeating then returns -1 */
int firstNonRepeating(char* str)
{
    int* count = getCharCountArray(str);
    int index = -1, i;

    for (i = 0; *(str + i); i++) {
        if (count[*(str + i)] == 1) {
            index = i;
            break;
        }
    }

    // To avoid memory leak
    free(count);
    return index;
}

/* Driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    int index = firstNonRepeating(str);
    if (index == -1)
        printf("Either all characters are repeating or "
               "string is empty");
    else
        printf("First non-repeating character is %c",
               str[index]);
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first
// non-repeating character
class GFG {
    static final int NO_OF_CHARS = 256;
    static char count[] = new char[NO_OF_CHARS];

    /* calculate count of characters
       in the passed string */
    static void getCharCountArray(String str)
    {
        for (int i = 0; i < str.length(); i++)
            count[str.charAt(i)]++;
    }

    /* The method returns index of first non-repeating
       character in a string. If all characters are repeating
       then returns -1 */
    static int firstNonRepeating(String str)
    {
        getCharCountArray(str);
        int index = -1, i;

        for (i = 0; i < str.length(); i++) {
            if (count[str.charAt(i)] == 1) {
                index = i;
                break;
            }
        }

        return index;
    }

    // Driver method
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int index = firstNonRepeating(str);

        System.out.println(
            index == -1
                ? "Either all characters are repeating or string "
                      + "is empty"
                : "First non-repeating character is "
                      + str.charAt(index));
    }
}
```

## 计算机编程语言

```
# Python program to print the first non-repeating character
NO_OF_CHARS = 256

# Returns an array of size 256 containing count
# of characters in the passed char array
def getCharCountArray(string):
    count = [0] * NO_OF_CHARS
    for i in string:
        count[ord(i)]+= 1
    return count

# The function returns index of first non-repeating
# character in a string. If all characters are repeating
# then returns -1
def firstNonRepeating(string):
    count = getCharCountArray(string)
    index = -1
    k = 0

    for i in string:
        if count[ord(i)] == 1:
            index = k
            break
        k += 1

    return index

# Driver program to test above function
string = "geeksforgeeks"
index = firstNonRepeating(string)
if index == 1:
    print "Either all characters are repeating or string is empty"
else:
    print "First non-repeating character is " + string[index]

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to find first non-repeating character
using System;
using System.Globalization;

class GFG {

    static int NO_OF_CHARS = 256;
    static char[] count = new char[NO_OF_CHARS];

    /* calculate count of characters
    in the passed string */
    static void getCharCountArray(string str)
    {
        for (int i = 0; i < str.Length; i++)
            count[str[i]]++;
    }

    /* The method returns index of first non-repeating
    character in a string. If all characters are
    repeating then returns -1 */
    static int firstNonRepeating(string str)
    {
        getCharCountArray(str);
        int index = -1, i;

        for (i = 0; i < str.Length; i++) {
            if (count[str[i]] == 1) {
                index = i;
                break;
            }
        }

        return index;
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        int index = firstNonRepeating(str);

        Console.WriteLine(index == -1 ? "Either "
                                            + "all characters are repeating or string "
                                            + "is empty"
                                      : "First non-repeating character"
                                            + " is " + str[index]);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// first non-repeating
// character
$NO_OF_CHARS = 256;
$count=array_fill(0, 200, 0);

/* calculate count
   of characters in 
   the passed string */
function getCharCountArray($str)
{
    global $count;
    for ($i = 0;
         $i < strlen($str); $i++)
        $count[ord($str[$i])]++;
}

/* The method returns index
of first non-repeating
character in a string. If
all characters are repeating
then returns -1 */
function firstNonRepeating($str)
{
    global $count;
    getCharCountArray($str);
    $index = -1;
    for ($i = 0;
         $i < strlen($str); $i++)
    {
        if ($count[ord($str[$i])] == 1)
        {
            $index = $i;
            break;
        }
    }

return $index;
}

// Driver code
$str = "geeksforgeeks";
$index = firstNonRepeating($str);
if($index == -1)
echo "Either all characters are" .
     " repeating or string is empty";
else
echo "First non-repeating ".
            "character is ".
               $str[$index];

// This code is contributed by mits
?>
```

**Output**

```
First non-repeating character is f
```

**只遍历一次字符串可以做到吗？**
以上做法耗费 **O(n)** 时间，但在实践中可以改进。算法的第一部分贯穿字符串来构造计数数组(在 **O(n)** 时间)。这是合理的。但是第二部分关于再次运行字符串只是为了找到第一个非中继器不是一个好的做法。
在真实情况下，字符串预计会比你的字母表大得多。以脱氧核糖核酸序列为例，它们可能有数百万个字母长，只有 4 个字母。如果非中继器在字符串的末尾会发生什么？那么我们将不得不扫描很长时间(再次)。
**<u>方法二</u> :** [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 和单串遍历。
**方法:**制作一个计数数组，而不是最大字符数(256)的 hash_map。我们不仅可以存储计数，还可以存储第一次遇到字符**时的索引，例如“a”的(3，26)，这意味着“a”被计数了 3 次，第一次出现在位置 26。**所以说到找到第一个非中继器，我们只需要扫描计数数组，而不是字符串。感谢本提出这种方法。
**算法:**

1.  制作一个 **count_array** ，它有两个字段，即**频率，第一次出现一个字符**。
2.  **计数 _ 数组**的大小为**【256】**。
3.  使用指针遍历给定的字符串。
4.  增加当前字符的计数并更新出现次数。
5.  现在这里有一个陷阱，数组将包含有效的第一次出现的字符，该字符的频率是统一的，否则第一次出现会不断更新。
6.  现在遍历 count_array，找到第一次出现的**最小值**和频率值为 1 的字符。
7.  返回字符

**伪码:**

```
for ( i=0 to str.length())
count_arr[str[i]].first++;
count_arr[str[i]].second=i;

int res=INT_MAX;
for(i=0 to count_arr.size())
  if(count_arr[str[i]].first==1)
  res=min(min, count_arr[str[i]].second)

return res
```

## C++

```
// CPP program to find first non-repeating
// character
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

/* The function returns index of the first
   non-repeating character in a string. If
   all characters are repeating then
   returns INT_MAX */
int firstNonRepeating(char* str)
{
    pair<int, int> arr[NO_OF_CHARS];

    for (int i = 0; str[i]; i++) {
        (arr[str[i]].first)++;
        arr[str[i]].second = i;
    }

    int res = INT_MAX;
    for (int i = 0; i < NO_OF_CHARS; i++)

        // If this character occurs only
        // once and appears before the
        // current result, then update the
        // result
        if (arr[i].first == 1)
            res = min(res, arr[i].second);

    return res;
}

/* Driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    int index = firstNonRepeating(str);
    if (index == INT_MAX)
        printf("Either all characters are "
               "repeating or string is empty");
    else
        printf("First non-repeating character"
               " is %c",
               str[index]);
    return 0;
}
```

## C

```
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>
#define NO_OF_CHARS 256

// Structure to store count of a
// character and index of the first
// occurrence in the input string
struct countIndex {
    int count;
    int index;
};

/* Returns an array of above
structure type. The size of
array is NO_OF_CHARS */
struct countIndex* getCharCountArray(char* str)
{
    struct countIndex* count = (struct countIndex*)calloc(
        sizeof(struct countIndex), NO_OF_CHARS);
    int i;
    for (i = 0; *(str + i); i++) {
        (count[*(str + i)].count)++;

        // If it's first occurrence,
        // then store the index
        if (count[*(str + i)].count == 1)
            count[*(str + i)].index = i;
    }
    return count;
}

/* The function returns index of the
    first non-repeating character in
    a string. If all characters are
    repeating then returns INT_MAX */
int firstNonRepeating(char* str)
{
    struct countIndex* count
        = getCharCountArray(str);
    int result = INT_MAX, i;

    for (i = 0; i < NO_OF_CHARS; i++) {
        // If this character occurs
        // only once and appears
        // before the current result,
        // then update the result
        if (count[i].count == 1
            && result > count[i].index)
            result = count[i].index;
    }

    // To avoid memory leak
    free(count);
    return result;
}

/* Driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    int index = firstNonRepeating(str);
    if (index == INT_MAX)
        printf("Either all characters are"
               " repeating or string is empty");
    else
        printf("First non-repeating character"
               " is %c",
               str[index]);
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first
// non-repeating character
// Note : hashmap is used

import java.util.*;

class CountIndex {
    int count, index;

    // constructor for first occurrence
    public CountIndex(int index)
    {
        this.count = 1;
        this.index = index;
    }

    // method for updating count
    public void incCount()
    {
        this.count++;
    }
}
class GFG {
    static final int NO_OF_CHARS = 256;

    static HashMap<Character, CountIndex> hm
        = new HashMap<Character, CountIndex>(NO_OF_CHARS);

    /* calculate count of characters
       in the passed string */
    static void getCharCountArray(String str)
    {
        for (int i = 0; i < str.length(); i++) {
            // If character already occurred,
            if (hm.containsKey(str.charAt(i))) {
                // updating count
                hm.get(str.charAt(i)).incCount();
            }

            // If it's first occurrence, then store
            // the index and count = 1
            else {
                hm.put(str.charAt(i), new CountIndex(i));
            }
        }
    }

    /* The method returns index of first non-repeating
       character in a string. If all characters are repeating
       then returns -1 */
    static int firstNonRepeating(String str)
    {
        getCharCountArray(str);
        int result = Integer.MAX_VALUE, i;
        for (Map.Entry<Character, CountIndex> entry : hm.entrySet())
        {
            int c=entry.getValue().count;
            int ind=entry.getValue().index;
            if(c==1 && ind < result)
            {
                result=ind;
            }
        }

        return result;
    }

    // Driver method
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int index = firstNonRepeating(str);

        System.out.println(
            index == Integer.MAX_VALUE
                ? "Either all characters are repeating "
                      + " or string is empty"
                : "First non-repeating character is "
                      + str.charAt(index));
    }
}
```

## C#

```
// C# program to find first
// non-repeating character
// Note : hashmap is used
using System;
using System.Collections.Generic;

class CountIndex {
    public int count, index;

    // constructor for first occurrence
    public CountIndex(int index)
    {
        this.count = 1;
        this.index = index;
    }

    // method for updating count
    public virtual void incCount()
    {
        this.count++;
    }
}

class GFG {
    public const int NO_OF_CHARS = 256;

    public static Dictionary<char,
                             CountIndex>
        hm = new Dictionary<char,
                            CountIndex>(NO_OF_CHARS);

    /* calculate count of characters
    in the passed string */
    public static void getCharCountArray(string str)
    {
        for (int i = 0; i < str.Length; i++) {
            // If character already occurred,
            if (hm.ContainsKey(str[i])) {
                // updating count
                hm[str[i]].incCount();
            }

            // If it's first occurrence, then
            // store the index and count = 1
            else {
                hm[str[i]] = new CountIndex(i);
            }
        }
    }

    /* The method returns index of first
    non-repeating character in a string.
    If all characters are repeating then
    returns -1 */
    internal static int firstNonRepeating(string str)
    {
        getCharCountArray(str);
        int result = int.MaxValue, i;

        for (i = 0; i < str.Length; i++) {
            // If this character occurs only
            // once and appears before the
            // current result, then update the result
            if (hm[str[i]].count == 1 && result > hm[str[i]].index) {
                result = hm[str[i]].index;
            }
        }

        return result;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string str = "geeksforgeeks";
        int index = firstNonRepeating(str);

        Console.WriteLine(
            index == int.MaxValue
                ? "Either all characters are repeating "
                      + " or string is empty"
                : "First non-repeating character is "
                      + str[index]);
    }
}

// This code is contributed by Shrikant13
```

**Output**

```
First non-repeating character is f
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    因为绳子至少需要穿过一次。
*   **辅助空间:** O(n)。
    空间被使用 **count_array/hash_map** 来跟踪频率所占据。

**方法#3:计数数组和单串遍历:**

**进场:**

创建一个最大字符数(256)的计数数组。我们可以将这个数组中的所有元素初始化为-1。然后一个字符一个字符地遍历我们的字符串，检查以这个字符作为索引的数组元素是否为-1。如果它是-1，那么把它改成 I，如果它不是-1，那么这意味着这个字符以前已经出现过，所以把它改成-2。

最后，所有重复字符将被更改为-2，所有非重复字符将包含它们出现的索引。现在我们可以循环遍历所有不重复的字符，找到最小索引或第一个索引。

## C++

```
// CPP program to find first non-repeating
// character
# include<iostream>
# include<climits>

using namespace std;

// this function return the index of first non-repeating
// character if found, or else it returns -1
int firstNonRepeating(string str) {
    int fi[256]; // array to store First Index

    // initializing all elements to -1
    for(int i = 0; i<256; i++)
        fi[i] = -1;

    // sets all repeating characters to -2 and non-repeating characters
      // contain the index where they occur
    for(int i = 0; i<str.length(); i++) {
        if(fi[str[i]] == -1) {
            fi[str[i]] = i;
        }else {
            fi[str[i]] = -2;
        }
    }

    int res = INT_MAX;

    for(int i = 0; i<256; i++) {

        // If this character is not -1 or -2 then it
        // means that this character occurred only once
        // so find the min index of all characters that
        // occur only once, that's our first index
        if(fi[i] >= 0)
            res = min(res, fi[i]);
    }

    // if res remains INT_MAX, it means there are no
    // characters that repeat only once or the string is empty
    if(res == INT_MAX) return -1;
    else return res;
}

int main(){
    string str;
      str = "geeksforgeeks";
    int firstIndex = firstNonRepeating(str);
    if (firstIndex == -1)
        cout<<"Either all characters are repeating or string is empty";
    else
        cout<<"First non-repeating character is "<< str[firstIndex];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find first non-repeating
// character
public class GFG {

// this function return the index of first non-repeating
// character if found, or else it returns -1
public static int firstNonRepeating(String str) {
    int[] fi = new int [256]; // array to store First Index

    // initializing all elements to -1
    for(int i = 0; i<256; i++)
        fi[i] = -1;

    // sets all repeating characters to -2 and non-repeating characters
      // contain the index where they occur
    for(int i = 0; i<str.length(); i++) {
        if(fi[str.charAt(i)] == -1) {
            fi[str.charAt(i)] = i;
        }else {
            fi[str.charAt(i)] = -2;
        }
    }

    int res =  Integer.MAX_VALUE;

    for(int i = 0; i<256; i++) {

        // If this character is not -1 or -2 then it
        // means that this character occurred only once
        // so find the min index of all characters that
        // occur only once, that's our first index
        if(fi[i] >= 0)
            res = Math.min(res, fi[i]);
    }

    // if res remains  Integer.MAX_VALUE, it means there are no
    // characters that repeat only once or the string is empty
    if(res ==  Integer.MAX_VALUE) return -1;
    else return res;
}

public static void main(String args[]){
    String str;
    str = "geeksforgeeks";
    int firstIndex = firstNonRepeating(str);
    if (firstIndex == -1)
       System.out.println("Either all characters are repeating or string is empty");
    else
       System.out.println("First non-repeating character is "+ str.charAt(firstIndex));
    }
}
//This code is contributed by SoumikMondal
```

## C#

```
// C# program to find first non-repeating
// character
using System;
public class GFG {

    // this function return the index of first non-repeating
    // character if found, or else it returns -1
    public static int firstNonRepeating(string str)
    {
        int[] fi
            = new int[256]; // array to store First Index

        // initializing all elements to -1
        for (int i = 0; i < 256; i++)
            fi[i] = -1;

        // sets all repeating characters to -2 and
        // non-repeating characters contain the index where
        // they occur
        for (int i = 0; i < str.Length; i++) {
            if (fi[str[i]] == -1) {
                fi[str[i]] = i;
            }
            else {
                fi[str[i]] = -2;
            }
        }

        int res = Int32.MaxValue;

        for (int i = 0; i < 256; i++) {

            // If this character is not -1 or -2 then it
            // means that this character occurred only once
            // so find the min index of all characters that
            // occur only once, that's our first index
            if (fi[i] >= 0)
                res = Math.Min(res, fi[i]);
        }

        // if res remains  Integer.MAX_VALUE, it means there
        // are no characters that repeat only once or the
        // string is empy
        if (res == Int32.MaxValue)
            return -1;
        else
            return res;
    }

    public static void Main()
    {
        string str;
        str = "geeksforgeeks";
        int firstIndex = firstNonRepeating(str);
        if (firstIndex == -1)
            Console.WriteLine(
                "Either all characters are repeating or string is empty");
        else
            Console.WriteLine(
                "First non-repeating character is "
                + str[firstIndex]);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// this function return the index of first non-repeating
// character if found, or else it returns -1
function firstNonRepeating(str)
{
    var fi=new Array(256);

    // array to store First Index
    fi.fill(-1);

    // initializing all elements to -1
    for(var i = 0; i<256; i++)
        fi[i] = -1;

    // sets all repeating characters to -2 and non-repeating characters
    // contain the index where they occur
    for(var i = 0; i<str.length; i++)
    {
        if(fi[str.charCodeAt(i)] ==-1)
        {
            fi[str.charCodeAt(i)] = i;

        }
        else
        {
            fi[str.charCodeAt(i)] = -2;
        }
    }

    var res = Infinity;

    for(var i = 0; i<256; i++) {

        // If this character is not -1 or -2 then it
        // means that this character occurred only once
        // so find the min index of all characters that
        // occur only once, that's our first index
        if(fi[i] >= 0)
            res = Math.min(res, fi[i]);
    }

    // if res remains INT_MAX, it means there are no
    // characters that repeat only once or the string is empty
    if(res == Infinity) return -1;
    else return res;
}

var str;
    str = "geeksforgeeks";
    var firstIndex = firstNonRepeating(str);
    if (firstIndex === -1)
        document.write("Either all characters are repeating or string is empty");
    else
        document.write("First non-repeating character is "+ str.charAt(firstIndex));

// This code is contributed by akshitsaxenaa09.   
</script>
```

**输出**

```
First non-repeating character is f
```

**复杂度分析:**

*   **时间复杂度** : O(n)。

因为字符串需要遍历一次

*   **辅助空间:** O(n)。

使用**计数阵列**跟踪频率，占用空间。

#### 方法 4:使用内置的 Python 函数:

#### 方法:

1.  使用[计数器()](https://www.geeksforgeeks.org/python-counter-objects-elements/)功能计算所有字符的所有频率。
2.  遍历字符串并检查是否有频率为 1 的元素。
3.  打印字符并断开循环。

**下面是实现:**

## 蟒蛇 3

```
# Python implementation
from collections import Counter

# Function which repeats
# first Nonrepeating character
def printNonrepeated(string):

    # Calculating frequencies
    # using Counter function
    freq = Counter(string)

    # Traverse the string
    for i in string:
        if(freq[i] == 1):
            print(i)
            break

# Driver code
string = "geeksforgeeks"

# passing string to printNonrepeated function
printNonrepeated(string)

# this code is contributed by vikkycirus
```

**Output**

```
f
```