# 打印输入字符串中的所有副本

> 原文:[https://www . geesforgeks . org/print-all-the-replicates-in-input-string/](https://www.geeksforgeeks.org/print-all-the-duplicates-in-the-input-string/)

**编写一个高效的程序，打印输入字符串中的所有副本及其计数**

**方法 1:** 使用哈希
**算法:**让输入字符串为“geeksforgeeks”
**1:**从输入字符串构建字符计数数组。
count[' e ']= 4
count[' g ']= 2
count[' k ']= 2
……
**2:**打印构造数组中值大于 1 的所有索引。
**解决方案**

## C++14

```
// C++ program to count all duplicates
// from string using hashing
#include <iostream>
using namespace std;
# define NO_OF_CHARS 256

class gfg
{
    public :

    /* Fills count array with
    frequency of characters */
    void fillCharCounts(char *str, int *count)
    {
        int i;
        for (i = 0; *(str + i); i++)
        count[*(str + i)]++;
    }

    /* Print duplicates present
    in the passed string */
    void printDups(char *str)
    {

        // Create an array of size 256 and fill
        // count of every character in it
        int *count = (int *)calloc(NO_OF_CHARS,
                                      sizeof(int));
        fillCharCounts(str, count);

        // Print characters having count more than 0
        int i;
        for (i = 0; i < NO_OF_CHARS; i++)
        if(count[i] > 1)
            printf("%c, count = %d \n", i, count[i]);

        free(count);
    }
};

/* Driver code*/
int main()
{
    gfg g ;
    char str[] = "test string";
    g.printDups(str);
    //getchar();
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
// C program to count all duplicates
// from string using hashing
# include <stdio.h>
# include <stdlib.h>
# define NO_OF_CHARS 256

/* Fills count array with
   frequency of characters */
void fillCharCounts(char *str, int *count)
{
   int i;
   for (i = 0; *(str+i);  i++)
      count[*(str+i)]++;
}

/* Print duplicates present
   in the passed string */
void printDups(char *str)
{

  // Create an array of size 256 and
  // fill count of every character in it
  int *count = (int *)calloc(NO_OF_CHARS,
                             sizeof(int));
  fillCharCounts(str, count);

  // Print characters having count more than 0
  int i;
  for (i = 0; i < NO_OF_CHARS; i++)
    if(count[i] > 1)
        printf("%c,  count = %d \n", i,  count[i]);

  free(count);
}

/* Driver program to test to print printDups*/
int main()
{
    char str[] = "test string";
    printDups(str);
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all
// duplicates from string using
// hashing

public class GFG {
    static final int NO_OF_CHARS = 256;

    /* Fills count array with
       frequency of characters */
    static void fillCharCounts(String str,
                                   int[] count)
    {
        for (int i = 0; i < str.length(); i++)
            count[str.charAt(i)]++;
    }

    /* Print duplicates present
      in the passed string */
    static void printDups(String str)
    {
        // Create an array of size
        // 256 and fill count of
        // every character in it
        int count[] = new int[NO_OF_CHARS];
        fillCharCounts(str, count);

        for (int i = 0; i < NO_OF_CHARS; i++)
            if (count[i] > 1)
                System.out.println((char)(i) +
                          ", count = " + count[i]);
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "test string";
        printDups(str);
    }
}
```

## 计算机编程语言

```
# Python program to count all
# duplicates from string using hashing
NO_OF_CHARS = 256

# Fills count array with
# frequency of characters
def fillCharCounts(string, count):
    for i in string:
        count[ord(i)] += 1
    return count

# Print duplicates present
# in the passed string
def printDups(string):

    # Create an array of size 256
    # and fill count of every character in it
    count = [0] * NO_OF_CHARS
    count = fillCharCounts(string,count)

    # Utility Variable
    k = 0

    # Print characters having
    # count more than 0
    for i in count:
        if int(i) > 1:
            print chr(k) + ", count = " + str(i)
        k += 1

# Driver program to test the above function
string = "test string"
print printDups(string)

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to count all duplicates
// from string using hashing
using System;

class GFG
{

    static int NO_OF_CHARS = 256;

    /* Fills count array with
       frequency of characters */
    static void fillCharCounts(String str,
                                 int[] count)
    {
        for (int i = 0; i < str.Length; i++)
            count[str[i]]++;
    }

    /* Print duplicates present in
    the passed string */
    static void printDups(String str)
    {

        // Create an array of size 256 and
        // fill count of every character in it
        int []count = new int[NO_OF_CHARS];
        fillCharCounts(str, count);

        for (int i = 0; i < NO_OF_CHARS; i++)
            if(count[i] > 1)
                Console.WriteLine((char)i + ", " +
                              "count = " + count[i]);
    }

    // Driver Method
    public static void Main()
    {
        String str = "test string";
        printDups(str);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// all duplicates from
// string using hashing
function fillCharCounts($str, $count)
{
    for ($i = 0; $i < strlen($str); $i++)
        $count[ord($str[$i])]++;

    for ($i = 0; $i < 256; $i++)
        if($count[$i] > 1)
            echo chr($i) . ", " ."count = " .
                         ($count[$i]) . "\n";
}

// Print duplicates present
// in the passed string
function printDups($str)
{
    // Create an array of size
    // 256 and fill count of
    // every character in it
    $count = array();
    for ($i = 0; $i < 256; $i++)
    $count[$i] = 0;
    fillCharCounts($str, $count);

}

// Driver Code
$str = "test string";
printDups($str);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to count all duplicates
    // from string using hashing

    let NO_OF_CHARS = 256;

    /* Print duplicates present in
    the passed string */
    function printDups(str)
    {

        // Create an array of size 256 and
        // fill count of every character in it
        let count = new Array(NO_OF_CHARS);
        count.fill(0);

        for (let i = 0; i < str.length; i++)
            count[str[i].charCodeAt()]++;

        for (let i = 0; i < NO_OF_CHARS; i++)
        {
            if(count[i] > 1)
            {
                document.write(String.fromCharCode(i) + ", " +
                "count = " + count[i] + "</br>");
            }
        }    
    }

    let str = "test string";
      printDups(str);

</script>
```

**Output**

```
s, count = 2 
t, count = 3 
```

**时间复杂度:** O(n)，其中 n =传递的字符串长度

**空间复杂度**:0(无字符)

**注意:**散列涉及每次使用固定大小的数组，不管字符串是什么。

例如，str = " aaaaaaaaaa "。

大小为 256 的数组用于 str，总大小(256)中只有 1 个块将用于存储 str 中“a”的出现次数(即计数[“a”]= 10)。

剩余 256–1 = 255 个块仍未使用。

因此，在这种情况下，空间复杂性可能很高。因此，为了避免任何差异并提高空间复杂性，地图通常比大尺寸阵列更受欢迎。

**方法 2:** 使用地图

**方法:**方法与**方法 1** 中讨论的方法相同，但是，使用地图存储计数。

**解决方案:**

## C++

```
// C++ program to count all duplicates
// from string using maps
#include <bits/stdc++.h>
using namespace std;
void printDups(string str)
{
    map<char, int> count;
    for (int i = 0; i < str.length(); i++) {
        count[str[i]]++;
    }

    for (auto it : count) {
        if (it.second > 1)
            cout << it.first << ", count = " << it.second
                 << "\n";
    }
}
/* Driver code*/
int main()
{
    string str = "test string";
    printDups(str);
    return 0;
}
// This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all duplicates
// from string using maps
import java.util.*;

class GFG {

    static void printDups(String str)
    {
        HashMap<Character, Integer> count = new HashMap<>();
        /*Store duplicates present
        in the passed string */
        for (int i = 0; i < str.length(); i++) {
            if (!count.containsKey(str.charAt(i)))
                count.put(str.charAt(i), 1);
            else
                count.put(str.charAt(i),
                          count.get(str.charAt(i)) + 1);
        }

        /*Print duplicates in sorted order*/
        for (Map.Entry mapElement : count.entrySet()) {
            char key = (char)mapElement.getKey();
            int value = ((int)mapElement.getValue());

            if (value > 1)
                System.out.println(key
                                   + ", count = " + value);
        }
    }
    // Driver code
    public static void main(String[] args)
    {
        String str = "test string";
        printDups(str);
    }
}
// This code is contributed by yashbeersingh42
```

## 蟒蛇 3

```
# Python 3 program to count all duplicates
# from string using maps
from collections import defaultdict

def printDups(st):

    count = defaultdict(int)
    for i in range(len(st)):
        count[st[i]] += 1

    for it in count:
        if (count[it] > 1):
            print(it, ", count = ", count[it])

# Driver code
if __name__ == "__main__":

    st = "test string"
    printDups(st)

    # This code is contributed by ukasp.
```

## C#

```
// C# program to count all duplicates
// from string using maps
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

static void printDups(String str)
{
    Dictionary<char,
               int> count = new Dictionary<char,
                                           int>();

    for(int i = 0; i < str.Length; i++)
    {
        if (count.ContainsKey(str[i]))
            count[str[i]]++;
        else
            count[str[i]] = 1;
    }

    foreach(var it in count.OrderBy(key => key.Value))
    {
        if (it.Value > 1)
            Console.WriteLine(it.Key + ", count = " +
                              it.Value);
    }
}

// Driver code
static public void Main()
{
    String str = "test string";
    printDups(str);
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
//Javascript Implementation
//  to count all duplicates
// from string using maps

function printDups(str)
{
    var count = {};
    for (var i = 0; i < str.length; i++) {
        count[str[i]] = 0;
    }

    for (var i = 0; i < str.length; i++) {
        count[str[i]]++;
    }

    for (var it in count) {
        if (count[it] > 1)
            document.write(it + ", count = " + count[it] + "<br>");
    }
}
/* Driver code*/
var str = "test string";
printDups(str);

// This code is contributed by shubhamsingh10
</script>
```

**Output**

```
s, count = 2
t, count = 3
```

**时间复杂度** : O(N log N)，其中 N =传递的字符串长度，在映射中插入一个元素一般需要 log N 的时间。

**空间复杂度** : O(K)，其中 K =地图大小(**0<= K<= input _ string _ length**)。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。

## C++

```
// C++ program to count all duplicates
// from string using maps
#include <bits/stdc++.h>
using namespace std;
void printDups(string str)
{
    unordered_map<char, int> count;
    for (int i = 0; i < str.length(); i++) {
        count[str[i]]++;  //increase the count of characters by 1
    }

    for (auto it : count) {   //iterating through the unordered map
        if (it.second > 1)   //if the count of characters is greater then 1 then duplicate found
            cout << it.first << ", count = " << it.second
                 << "\n";
    }
}
/* Driver code*/
int main()
{
    string str = "test string";
    printDups(str);
    return 0;
}
```

**Output**

```
s, count = 2
t, count = 3
```

> **时间复杂度:**
> 
> O(N)，其中 N =传递的字符串长度，在无序映射中插入和访问任何元素需要 O(1)个时间

> **空间复杂度:**
> 
> O(K)，其中 K =映射的大小(0<=K<=input_string_length)。