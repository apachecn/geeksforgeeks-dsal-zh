# 检查给定的字符串是否可以通过给定的可能交换转换成另一个字符串

> 原文:[https://www . geesforgeks . org/check-如果给定的字符串可以通过给定的可能交换转换为另一个字符串/](https://www.geeksforgeeks.org/check-if-a-given-string-can-be-converted-to-another-by-given-possible-swaps/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str1** 和 **str2** ，任务是通过多次执行以下操作来检查字符串 **str1** 是否可以转换为字符串 **str2** :

*   交换 **str1** 的任意两个字符。
*   将所有出现的 **str1** 字符替换为所有出现的 **str1** 的任何其他不同字符。

**示例:**

> **输入:**str1 =“xyyzzll”，str2 =“yllzzxxx”
> T3】输出: True
> **解释:**
> 交换 str1[0]和 str1[1]的所有出现将 str1 修改为“yxzzll”
> 交换 str1[1]和 str1[5]的所有出现将 str1 修改为“yllzzxxx”
> 由于 str 1 和 str 2 相等，因此，所需的输出为 True。
> 
> **输入:**str 1 =“xyyzzvl”，str 2 =“yllzzvac”
> T3】输出:假

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如**has h1【256】**和**has H2【256】**分别存储 **str1** 和 **str2** 每个不同元素的频率。
*   初始化两个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如 **st1** 和 **st2** 来存储 **str1** 和 **str2** 的不同字符。
*   遍历字符串并存储 **str1** 和 **str2** 每个不同字符的频率。
*   [排序](https://www.geeksforgeeks.org/sort-c-stl/) **哈斯 h1[]****哈斯 h2[]** 阵。
*   如果 **st1** 和 **st2** 不相等，则打印假。
*   使用变量 **i** 遍历**has h1【】**和**has H2【】**数组，检查**的值是否为(hash1[i]！= hash2[i])** 是真还是假。如果发现是真的，则打印**假的**。
*   否则，打印**真**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

bool checkStr1CanConStr2(string& str1,
                         string& str2)
{
    // Stores length of str1
    int N = str1.length();

    // Stores length of str2
    int M = str2.length();

    // Stores distinct characters
    // of str1
    set<int> st1;

    // Stores distinct characters
    // of str2
    set<int> st2;

    // Stores frequency of
    // each character of str1
    int hash1[256] = { 0 };

    // Traverse the string str1
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of str1[i]
        hash1[str1[i]]++;
    }

    // Traverse the string str1
    for (int i = 0; i < N; i++) {

        // Insert str1[i]
        // into st1
        st1.insert(str1[i]);
    }

    // Traverse the string str2
    for (int i = 0; i < M; i++) {

        // Insert str1[i]
        // into st1
        st2.insert(str2[i]);
    }

    // If distinct characters in
    // str1 and str2 are not same
    if (st1 != st2) {
        return false;
    }

    // Stores frequency of
    // each character of str2
    int hash2[256] = { 0 };

    // Traverse the string str2
    for (int i = 0; i < M; i++) {

        // Update frequency
        // of str2[i]
        hash2[str2[i]]++;
    }

    // Sort hash1[] array
    sort(hash1, hash1 + 256);

    // Sort hash2[] array
    sort(hash2, hash2 + 256);

    // Traverse hash1[] and hash2[]
    for (int i = 0; i < 256; i++) {

        // If hash1[i] not
        // equal to hash2[i]
        if (hash1[i] != hash2[i]) {
            return false;
        }
    }
    return true;
}

// Driver Code
int main()
{
    string str1 = "xyyzzlll";
    string str2 = "yllzzxxx";
    if (checkStr1CanConStr2(str1, str2)) {
        cout << "True";
    }
    else {
        cout << "False";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static boolean checkStr1CanConStr2(String str1,
                         String str2)
{
    // Stores length of str1
    int N = str1.length();

    // Stores length of str2
    int M = str2.length();

    // Stores distinct characters
    // of str1
    HashSet<Integer> st1 = new HashSet<>();

    // Stores distinct characters
    // of str2
    HashSet<Integer> st2 =  new  HashSet<>();

    // Stores frequency of
    // each character of str1
    int hash1[] = new int[256];

    // Traverse the String str1
    for (int i = 0; i < N; i++)
    {

        // Update frequency
        // of str1[i]
        hash1[str1.charAt(i)]++;
    }

    // Traverse the String str1
    for (int i = 0; i < N; i++)
    {

        // Insert str1[i]
        // into st1
        st1.add((int)str1.charAt(i));
    }

    // Traverse the String str2
    for (int i = 0; i < M; i++)
    {

        // Insert str1[i]
        // into st1
        st2.add((int)str2.charAt(i));
    }

    // If distinct characters in
    // str1 and str2 are not same
    if (!st1.equals(st2))
    {
        return false;
    }

    // Stores frequency of
    // each character of str2
    int hash2[] = new int[256];

    // Traverse the String str2
    for (int i = 0; i < M; i++)
    {

        // Update frequency
        // of str2[i]
        hash2[str2.charAt(i)]++;
    }

    // Sort hash1[] array
    Arrays.sort(hash1);

    // Sort hash2[] array
    Arrays.sort(hash2);

    // Traverse hash1[] and hash2[]
    for (int i = 0; i < 256; i++)
    {

        // If hash1[i] not
        // equal to hash2[i]
        if (hash1[i] != hash2[i])
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    String str1 = "xyyzzlll";
    String str2 = "yllzzxxx";
    if (checkStr1CanConStr2(str1, str2))
    {
        System.out.print("True");
    }
    else
    {
        System.out.print("False");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
def checkStr1CanConStr2(str1, str2):

    # Stores length of str1
    N = len(str1)

    # Stores length of str2
    M = len(str2)

    # Stores distinct characters
    # of str1
    st1 = set([])

    # Stores distinct characters
    # of str2
    st2 = set([])

    # Stores frequency of
    # each character of str1
    hash1 = [0] * 256

    # Traverse the string str1
    for i in range(N):

        # Update frequency
        # of str1[i]
        hash1[ord(str1[i])] += 1

    # Traverse the string str1
    for i in range(N):

        # Insert str1[i]
        # into st1
        st1.add(str1[i])

    # Traverse the string str2
    for i in range(M):

        # Insert str1[i]
        # into st1
        st2.add(str2[i])

    # If distinct characters in
    # str1 and str2 are not same
    if (st1 != st2):
        return False

    # Stores frequency of
    # each character of str2
    hash2 = [0] * 256

    # Traverse the string str2
    for i in range(M):

        # Update frequency
        # of str2[i]
        hash2[ord(str2[i])] += 1

    # Sort hash1[] array
    hash1.sort()

    # Sort hash2[] array
    hash2.sort()

    # Traverse hash1[] and hash2[]
    for i in range(256):

        # If hash1[i] not
        # equal to hash2[i]
        if (hash1[i] != hash2[i]):
            return False

    return True

# Driver Code
if __name__ == "__main__":

    str1 = "xyyzzlll"
    str2 = "yllzzxxx"

    if (checkStr1CanConStr2(str1, str2)):
        print("True")
    else:
        print("False")

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static bool checkStr1CanConStr2(String str1,
                         String str2)
{
    // Stores length of str1
    int N = str1.Length;

    // Stores length of str2
    int M = str2.Length;

    // Stores distinct characters
    // of str1
    HashSet<int> st1 = new HashSet<int>();

    // Stores distinct characters
    // of str2
    HashSet<int> st2 =  new  HashSet<int>();

    // Stores frequency of
    // each character of str1
    int []hash1 = new int[256];

    // Traverse the String str1
    for (int i = 0; i < N; i++)
    {

        // Update frequency
        // of str1[i]
        hash1[str1[i]]++;
    }

    // Traverse the String str1
    for (int i = 0; i < N; i++)
    {

        // Insert str1[i]
        // into st1
        st1.Add(str1[i]);
    }

    // Traverse the String str2
    for (int i = 0; i < M; i++)
    {

        // Insert str1[i]
        // into st1
        st2.Add(str2[i]);
    }

    // If distinct characters in
    // str1 and str2 are not same
    if (st1.Equals(st2))
    {
        return false;
    }

    // Stores frequency of
    // each character of str2
    int []hash2 = new int[256];

    // Traverse the String str2
    for (int i = 0; i < M; i++)
    {

        // Update frequency
        // of str2[i]
        hash2[str2[i]]++;
    }

    // Sort hash1[] array
    Array.Sort(hash1);

    // Sort hash2[] array
    Array.Sort(hash2);

    // Traverse hash1[] and hash2[]
    for (int i = 0; i < 256; i++)
    {

        // If hash1[i] not
        // equal to hash2[i]
        if (hash1[i] != hash2[i])
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    String str1 = "xyyzzlll";
    String str2 = "yllzzxxx";
    if (checkStr1CanConStr2(str1, str2))
    {
        Console.Write("True");
    }
    else
    {
        Console.Write("False");
    }
}
}

 // This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

function checkStr1CanConStr2(str1, str2)
{
    // Stores length of str1
    var N = str1.length;

    // Stores length of str2
    var M = str2.length;

    // Stores distinct characters
    // of str1
    var st1 = new Set();

    // Stores distinct characters
    // of str2
    var st2 = new Set();

    // Stores frequency of
    // each character of str1
    var hash1 = Array(256).fill(0);

    // Traverse the string str1
    for (var i = 0; i < N; i++) {

        // Update frequency
        // of str1[i]
        hash1[str1[i].charCodeAt(0)]++;
    }

    // Traverse the string str1
    for (var i = 0; i < N; i++) {

        // Insert str1[i]
        // into st1
        st1.add(str1[i]);
    }

    // Traverse the string str2
    for (var i = 0; i < M; i++) {

        // Insert str1[i]
        // into st1
        st2.add(str2[i]);
    }

    // If distinct characters in
    // str1 and str2 are not same
    if (st1.size != st2.size) {
        return false;
    }

    // Stores frequency of
    // each character of str2
    var hash2 = Array(256).fill(0);

    // Traverse the string str2
    for (var i = 0; i < M; i++) {

        // Update frequency
        // of str2[i]
        hash2[str2[i].charCodeAt(0)]++;
    }

    // Sort hash1[] array
    hash1.sort((a,b)=>a-b);
    hash2.sort((a,b)=>a-b);

    // Traverse hash1[] and hash2[]
    for (var i = 0; i < 256; i++) {

        // If hash1[i] not
        // equal to hash2[i]
        if (hash1[i] != hash2[i]) {

            return false;
        }
    }
    return true;
}

// Driver Code
var str1 = "xyyzzlll";
var str2 = "yllzzxxx";
if (checkStr1CanConStr2(str1, str2)) {
    document.write( "True");
}
else {
    document.write( "False");
}

</script>
```

**Output:** 

```
True
```

***时间复杂度:**O(N+M+256)*
T5**辅助空间:** O(256)