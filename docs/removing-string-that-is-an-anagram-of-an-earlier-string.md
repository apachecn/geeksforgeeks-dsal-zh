# 移除作为较早字符串的字谜的字符串

> 原文:[https://www . geesforgeks . org/remove-string-即早期字符串的字谜/](https://www.geeksforgeeks.org/removing-string-that-is-an-anagram-of-an-earlier-string/)

给定一个字符串数组 **arr** ，任务是删除先前字符串的字谜，然后按排序顺序打印剩余的数组。

**示例:**

> **输入:** arr[] = {“极客”、“keegs”、“code”、“doce”}，N = 4
> **输出:**【“code”、“极客”】
> **解释:**
> “极客”和“keegs”都是字谜，所以我们去掉“keegs”。
> 同样，“code”和“doce”也是字谜，所以我们去掉了“doce”。
> 
> **输入:** arr[] = {“茶”、“吃了”、“字谜”、“吃了”、“格兰马安”}，N = 5
> **输出:**【“字谜”、“茶”】
> **说明:**“吃了”和“吃了”都是“茶”的字谜。
> “gramaan”是“字谜”的字谜。因此，array 变成[“字谜”、“茶”]。

**方法:**为了[检查给定的两个字符串是否是字谜而不是](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)，我们可以简单地对两个字符串进行排序并进行比较。此外，为了检查字符串是否出现，我们可以使用[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)。

1.  创建一个辅助数组来保存结果字符串，创建一个 hashmap 来保存到目前为止我们找到的字符串的标记。
2.  然后遍历给定的数组字符串，对当前字符串进行排序，并在 hashmap 中检查该字符串。
3.  如果在 hashmap 中没有找到当前字符串，那么在结果数组中按下 arr[i]，并将排序后的字符串插入 hashmap 中。
4.  最后，对结果数组进行排序，并打印每个字符串。

**以下是上述方法的实施。**

## C++

```
// C++ implementation to remove
// all the anagram strings
#include <bits/stdc++.h>
using namespace std;

// Function to remove the anagram string
void removeAnagrams(string arr[], int N)
{
    // vector to store the final result
    vector<string> ans;

    // data structure to keep a mark
    // of the previously occured string
    unordered_set<string> found;

    for (int i = 0; i < N; i++) {

        string word = arr[i];

        // Sort the characters
        // of the current string
        sort(begin(word), end(word));

        // Check if current string is not
        // present inside the hashmap
        // Then push it in the resultant vector
        // and insert it in the hashmap
        if (found.find(word) == found.end()) {

            ans.push_back(arr[i]);
            found.insert(word);
        }
    }

    // Sort the resultant vector of strings
    sort(begin(ans), end(ans));

    // Print the required array
    for (int i = 0; i < ans.size(); ++i) {
        cout << ans[i] << " ";
    }
}

// Driver code
int main()
{
    string arr[]
        = { "geeks", "keegs",
            "code", "doce" };
    int N = 4;

    removeAnagrams(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to remove
// all the anagram Strings
import java.util.*;

class GFG{

// Function to remove the anagram String
static void removeAnagrams(String arr[], int N)
{
    // vector to store the final result
    Vector<String> ans = new Vector<String>();

    // data structure to keep a mark
    // of the previously occured String
    HashSet<String> found = new HashSet<String> ();

    for (int i = 0; i < N; i++) {

        String word = arr[i];

        // Sort the characters
        // of the current String
        word = sort(word);

        // Check if current String is not
        // present inside the hashmap
        // Then push it in the resultant vector
        // and insert it in the hashmap
        if (!found.contains(word)) {

            ans.add(arr[i]);
            found.add(word);
        }
    }

    // Sort the resultant vector of Strings
    Collections.sort(ans);

    // Print the required array
    for (int i = 0; i < ans.size(); ++i) {
        System.out.print(ans.get(i)+ " ");
    }
}
static String sort(String inputString)
{
    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Driver code
public static void main(String[] args)
{
    String arr[]
        = { "geeks", "keegs",
            "code", "doce" };
    int N = 4;

    removeAnagrams(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to remove
# all the anagram strings

# Function to remove the anagram string
def removeAnagrams(arr, N):

    # vector to store the final result
    ans = []

    # data structure to keep a mark
    # of the previously occured string
    found = dict()

    for i in range(N):

        word = arr[i]

        # Sort the characters
        # of the current string
        word = " ".join(sorted(word))

        # Check if current is not
        # present inside the hashmap
        # Then push it in the resultant vector
        # and insert it in the hashmap
        if (word not in found):

            ans.append(arr[i])
            found[word] = 1

    # Sort the resultant vector of strings
    ans = sorted(ans)

    # Print the required array
    for i in range(len(ans)):
        print(ans[i], end=" ")

# Driver code
if __name__ == '__main__':
    arr=["geeks", "keegs","code", "doce"]
    N = 4

    removeAnagrams(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to remove
// all the anagram Strings
using System;
using System.Collections.Generic;

class GFG{

// Function to remove the anagram String
static void removeAnagrams(String []arr, int N)
{
    // vector to store the readonly result
    List<String> ans = new List<String>();

    // data structure to keep a mark
    // of the previously occured String
    HashSet<String> found = new HashSet<String> ();

    for (int i = 0; i < N; i++) {

        String word = arr[i];

        // Sort the characters
        // of the current String
        word = sort(word);

        // Check if current String is not
        // present inside the hashmap
        // Then push it in the resultant vector
        // and insert it in the hashmap
        if (!found.Contains(word)) {

            ans.Add(arr[i]);
            found.Add(word);
        }
    }

    // Sort the resultant vector of Strings
    ans.Sort();

    // Print the required array
    for (int i = 0; i < ans.Count; ++i) {
        Console.Write(ans[i]+ " ");
    }
}
static String sort(String inputString)
{
    // convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // sort tempArray
    Array.Sort(tempArray);

    // return new sorted string
    return String.Join("",tempArray);
}

// Driver code
public static void Main(String[] args)
{
    String []arr
        = { "geeks", "keegs",
            "code", "doce" };
    int N = 4;

    removeAnagrams(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to remove
// all the anagram Strings

// Function to remove the anagram String
function removeAnagrams(arr, N)
{

    // Vector to store the final result
    let ans = [];

    // Data structure to keep a mark
    // of the previously occured String
    let found = new Set();

    for(let i = 0; i < N; i++)
    {
        let word = arr[i];

        // Sort the characters
        // of the current String
        word = sort(word);

        // Check if current String is not
        // present inside the hashmap
        // Then push it in the resultant vector
        // and insert it in the hashmap
        if (!found.has(word))
        {
            ans.push(arr[i]);
            found.add(word);
        }
    }

    // Sort the resultant vector of Strings
    (ans).sort();

    // Print the required array
    for(let i = 0; i < ans.length; ++i)
    {
        document.write(ans[i] + " ");
    }
}

function sort(inputString)
{

    // Convert input string to char array
    let tempArray = inputString.split("");

    // Sort tempArray
    (tempArray).sort();

    // Return new sorted string
    return (tempArray).join("");
}

// Driver code
let arr = [ "geeks", "keegs",
            "code", "doce" ];
let N = 4;

removeAnagrams(arr, N);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
code geeks
```