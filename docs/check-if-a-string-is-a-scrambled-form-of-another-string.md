# 检查一个字符串是否是另一个字符串的加扰形式

> 原文:[https://www . geesforgeks . org/check-if-a-string-is-a-scrambled-form-of-other-string/](https://www.geeksforgeeks.org/check-if-a-string-is-a-scrambled-form-of-another-string/)

给定两个长度相等的字符串 **S1** 和 **S2** ，任务是确定 S2 是否是 S1 的混乱形式。
**置乱字符串:**
给定字符串 **str** ，我们可以将其递归划分为两个非空子字符串，表示为[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)。
**注意:**加扰字符串与[字谜](https://www.geeksforgeeks.org/tag/anagram/)
不同以下是 str = **【编码器】** :
的一种可能表示

```
    coder
   /    \
  co    der
 / \    /  \
c   o  d   er
           / \
          e   r
```

为了打乱字符串，我们可以选择任何非叶节点并交换它的两个子节点。
假设，我们选择节点“co”并交换它的两个子节点，它会产生一个加扰的字符串“ocder”。

```
    ocder
   /    \
  oc    der
 / \    /  \
o   c  d   er
           / \
          e   r
```

因此，**“ocder”**是一串被打乱的**“编码器”**。
同样，如果我们继续交换节点**“der”**和**“er”**的子节点，会产生一个加扰的字符串**“ocred”**。

```
    ocred
   /    \
  oc    red
 / \    /  \
o   c  re  d
       / \
      r   e
```

因此，**“ocred”**是一串被打乱的**“编码器”**。
**例:**

> **输入:** S1=【编码器】，S2 =【ocder】
> **输出:**是
> **解释:**
> 【ocder】是“编码器”
> **的置乱形式输入:**S1 =【abcde】，S2 =【caebd】
> **输出:**否
> **解释:**
> “caebd”不是“abcde”的置乱形式

**逼近**
为了解决这个问题，我们采用[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)的方法。
给定两个等长的字符串(比如 n+1)，S1[0…n]和 S2[0…n]。如果 S2 是 S1 的一个加扰形式，那么必须存在一个指数 I，使得至少以下条件之一为真:

*   S2[0…i]是 S1[0…i]的加扰串，S2[i+1…n]是 S1[i+1…n]的加扰串。
*   S2[0…i]是 S1[n-i…n]的加扰串，S2[i+1…n]是 S1[0…n-i-1]的加扰串。

**注意:**这里要考虑的一个优化步骤是预先检查[两个字符串是否是彼此的字谜。](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)如果不是，则表示字符串包含不同的字符，不能是彼此的加扰形式。
以下是上述方法的实施:

## C++

```
// C++ Program to check if a
// given string is a scrambled
// form of another string

#include <bits/stdc++.h>
using namespace std;

bool isScramble(string S1, string S2)
{
    // Strings of non-equal length
    // cant' be scramble strings
    if (S1.length() != S2.length()) {
        return false;
    }

    int n = S1.length();

    // Empty strings are scramble strings
    if (n == 0) {
        return true;
    }

    // Equal strings are scramble strings
    if (S1 == S2) {
        return true;
    }

    // Check for the condition of anagram
    string copy_S1 = S1, copy_S2 = S2;

    sort(copy_S1.begin(), copy_S1.end());
    sort(copy_S2.begin(), copy_S2.end());

    if (copy_S1 != copy_S2) {
        return false;
    }

    for (int i = 1; i < n; i++) {

        // Check if S2[0...i] is a scrambled
        // string of S1[0...i] and if S2[i+1...n]
        // is a scrambled string of S1[i+1...n]
        if (isScramble(S1.substr(0, i), S2.substr(0, i))
            && isScramble(S1.substr(i, n - i),
                          S2.substr(i, n - i))) {
            return true;
        }

        // Check if S2[0...i] is a scrambled
        // string of S1[n-i...n] and S2[i+1...n]
        // is a scramble string of S1[0...n-i-1]
        if (isScramble(S1.substr(0, i),
                       S2.substr(n - i, i))
            && isScramble(S1.substr(i, n - i),
                          S2.substr(0, n - i))) {
            return true;
        }
    }

    // If none of the above
    // conditions are satisfied
    return false;
}

// Driver Code
int main()
{
    string S1 = "coder";
    string S2 = "ocred";

    if (isScramble(S1, S2)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// given string is a scrambled
// form of another string
import java.util.*;

class GFG{

static boolean isScramble(String S1,
                          String S2)
{

    // Strings of non-equal length
    // cant' be scramble strings
    if (S1.length() != S2.length())
    {
        return false;
    }

    int n = S1.length();

    // Empty strings are scramble strings
    if (n == 0)
    {
        return true;
    }

    // Equal strings are scramble strings
    if (S1.equals(S2))
    {
        return true;
    }

    // Converting string to
    // character array
    char[] tempArray1 = S1.toCharArray();
    char[] tempArray2 = S2.toCharArray();

    // Checking condition for Anagram
    Arrays.sort(tempArray1);
    Arrays.sort(tempArray2);

    String copy_S1 = new String(tempArray1);
    String copy_S2 = new String(tempArray2);

    if (!copy_S1.equals(copy_S2))
    {
        return false;
    }

    for(int i = 1; i < n; i++)
    {

        // Check if S2[0...i] is a scrambled
        // string of S1[0...i] and if S2[i+1...n]
        // is a scrambled string of S1[i+1...n]
        if (isScramble(S1.substring(0, i),
                       S2.substring(0, i)) &&
            isScramble(S1.substring(i, n),
                       S2.substring(i, n)))
        {
            return true;
        }

        // Check if S2[0...i] is a scrambled
        // string of S1[n-i...n] and S2[i+1...n]
        // is a scramble string of S1[0...n-i-1]
        if (isScramble(S1.substring(n - i, n),
                       S2.substring(0, i)) &&
            isScramble(S1.substring(0, n - i),
                       S2.substring(i, n)))
        {
            return true;
        }
    }

    // If none of the above
    // conditions are satisfied
    return false;
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "coder";
    String S2 = "ocred";

    if (isScramble(S1, S2))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by dadi madhav
```

## 蟒蛇 3

```
# Python3 program to check if a
# given string is a scrambled
# form of another string
def isScramble(S1: str, S2: str):

    # Strings of non-equal length
    # cant' be scramble strings
    if len(S1) != len(S2):
        return False

    n = len(S1)

    # Empty strings are scramble strings
    if not n:
        return True

    # Equal strings are scramble strings
    if S1 == S2:
        return True

    # Check for the condition of anagram
    if sorted(S1) != sorted(S2):
        return False

    for i in range(1, n):

        # Check if S2[0...i] is a scrambled
        # string of S1[0...i] and if S2[i+1...n]
        # is a scrambled string of S1[i+1...n]
        if (isScramble(S1[:i], S2[:i]) and
            isScramble(S1[i:], S2[i:])):
            return True

        # Check if S2[0...i] is a scrambled
        # string of S1[n-i...n] and S2[i+1...n]
        # is a scramble string of S1[0...n-i-1]
        if (isScramble(S1[-i:], S2[:i]) and
            isScramble(S1[:-i], S2[i:])):
            return True

    # If none of the above
    # conditions are satisfied
    return False

# Driver Code
if __name__ == "__main__":

    S1 = "coder"
    S2 = "ocred"

    if (isScramble(S1, S2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by sgshah2
```

## C#

```
// C# program to check if a
// given string is a scrambled
// form of another string
using System;
using System.Collections.Generic;
class GFG {

    static bool isScramble(string S1, string S2)
    {

        // Strings of non-equal length
        // cant' be scramble strings
        if (S1.Length != S2.Length) 
        {
            return false;
        }

        int n = S1.Length;

        // Empty strings are scramble strings
        if (n == 0) 
        {
            return true;
        }

        // Equal strings are scramble strings
        if (S1.Equals(S2))
        {
            return true;
        }

        // Converting string to 
        // character array
        char[] tempArray1 = S1.ToCharArray();
        char[] tempArray2 = S2.ToCharArray();

        // Checking condition for Anagram
        Array.Sort(tempArray1);
        Array.Sort(tempArray2);

        string copy_S1 = new string(tempArray1);
        string copy_S2 = new string(tempArray2);

        if (!copy_S1.Equals(copy_S2)) 
        {
            return false;
        }

        for(int i = 1; i < n; i++)
        {

            // Check if S2[0...i] is a scrambled
            // string of S1[0...i] and if S2[i+1...n]
            // is a scrambled string of S1[i+1...n]
            if (isScramble(S1.Substring(0, i), 
                           S2.Substring(0, i)) && 
                isScramble(S1.Substring(i, n - i),
                           S2.Substring(i, n - i)))
            {
                return true;
            }

            // Check if S2[0...i] is a scrambled
            // string of S1[n-i...n] and S2[i+1...n]
            // is a scramble string of S1[0...n-i-1]
            if (isScramble(S1.Substring(0, i),
                           S2.Substring(n - i, i)) && 
                isScramble(S1.Substring(i, n - i),
                           S2.Substring(0, n - i))) 
            {
                return true;
            }
        }

        // If none of the above
        // conditions are satisfied
        return false;
    }

  // Driver code
  static void Main()
  {
        string S1 = "coder";
        string S2 = "ocred";

        if (isScramble(S1, S2)) 
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program to check if a
    // given string is a scrambled
    // form of another string

    function isScramble(S1, S2)
    {

        // Strings of non-equal length
        // can't be scramble strings
        if (S1.length != S2.length)
        {
            return false;
        }

        let n = S1.length;

        // Empty strings are scramble strings
        if (n == 0)
        {
            return true;
        }

        // Equal strings are scramble strings
        if (S1 == S2)
        {
            return true;
        }

        // Converting string to
        // character array
        let tempArray1 = S1.split('');
        let tempArray2 = S2.split('');

        // Checking condition for Anagram
        tempArray1.sort();
        tempArray2.sort();

        let copy_S1 = tempArray1.join("");
        let copy_S2 = tempArray2.join("");

        if (copy_S1 != copy_S2)
        {
            return false;
        }

        for(let i = 1; i < n; i++)
        {

            // Check if S2[0...i] is a scrambled
            // string of S1[0...i] and if S2[i+1...n]
            // is a scrambled string of S1[i+1...n]
            if (isScramble(S1.substring(0, i),
                           S2.substring(0, i)) &&
                isScramble(S1.substring(i, i + n),
                           S2.substring(i, i + n)))
            {
                return true;
            }

            // Check if S2[0...i] is a scrambled
            // string of S1[n-i...n] and S2[i+1...n]
            // is a scramble string of S1[0...n-i-1]
            if (isScramble(S1.substring(n - i, n - i + n),
                           S2.substring(0, i)) &&
                isScramble(S1.substring(0, n - i),
                           S2.substring(i, i + n)))
            {
                return true;
            }
        }

        // If none of the above
        // conditions are satisfied
        return false;
    }

    let S1 = "coder";
    let S2 = "ocred";

    if (isScramble(S1, S2))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

// This code is contributed by decode2207.
</script>
```

**Output**

```
Yes
```

**时间复杂度** : O(2^k + 2^(n-k)，其中 k 和 n-k 是两个子串的长度。

**辅助空间** : O(2^N)，递归栈。

**动态编程解决方案:**上面的递归代码可以通过将子串的布尔值存储在一个无序的映射中来优化，所以如果必须再次检查相同的子串，我们可以很容易地只从映射中获取值，而不是执行函数调用。

**记忆代码:**

## C++

```
// C++ Program to check if a
// given string is a scrambled
// form of another string

#include <bits/stdc++.h>
using namespace std;

// map declaration for storing key value pair
// means for storing subproblem result
unordered_map<string, bool> mp;

bool isScramble(string S1, string S2)
{
    // Strings of non-equal length
    // cant' be scramble strings
    if (S1.length() != S2.length()) {
        return false;
    }

    int n = S1.length();

    // Empty strings are scramble strings
    if (n == 0) {
        return true;
    }

    // Equal strings are scramble strings
    if (S1 == S2) {
        return true;
    }
    // Check for the condition of anagram
    string copy_S1 = S1, copy_S2 = S2;

    sort(copy_S1.begin(), copy_S1.end());
    sort(copy_S2.begin(), copy_S2.end());

    if (copy_S1 != copy_S2) {
        return false;
    }

    // make key of type string for search in map
    string key = (S1 + " " + S2);
    // checking if both string are before calculated or not
    // if calculated means find in map then return it's
    // value
    if (mp.find(key) != mp.end()) {
        return mp[key];
    }

    // declaring flag variable to store result
    bool flag = false;

    for (int i = 1; i < n; i++) {

        // Check if S2[0...i] is a scrambled
        // string of S1[0...i] and if S2[i+1...n]
        // is a scrambled string of S1[i+1...n]
        if (isScramble(S1.substr(0, i), S2.substr(0, i))
            && isScramble(S1.substr(i, n - i),
                          S2.substr(i, n - i))) {
            flag = true;
            return true;
        }

        // Check if S2[0...i] is a scrambled
        // string of S1[n-i...n] and S2[i+1...n]
        // is a scramble string of S1[0...n-i-1]
        if (isScramble(S1.substr(0, i), S2.substr(n - i, i))
            && isScramble(S1.substr(i, n - i),
                          S2.substr(0, n - i))) {
            flag = true;
            return true;
        }
    }

    // add key & flag value to map (store for future use)
    // so next time no required to calculate it again
    mp[key] = flag;

    // If none of the above conditions are satisfied
    return false;
}

// Driver Code
int main()
{
    string S1 = "coder";
    string S2 = "ocred";

    if (isScramble(S1, S2)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a
// given string is a scrambled
// form of another string
import java.util.*;
public class Main
{
    // map declaration for storing key value pair
    // means for storing subproblem result
    static HashMap<String, Boolean> mp = new HashMap<String, Boolean>();

    static boolean isScramble(String S1, String S2)
    {

        // Strings of non-equal length
        // cant' be scramble strings
        if (S1.length() != S2.length()) {
            return false;
        }

        int n = S1.length();

        // Empty strings are scramble strings
        if (n != 0) {
            return true;
        }

        // Equal strings are scramble strings
        if (S1 == S2) {
            return true;
        }
        // Check for the condition of anagram
        String copy_S1 = S1, copy_S2 = S2;
        char[] t1 = copy_S1.toCharArray();
        char[] t2 = copy_S2.toCharArray();
        Arrays.sort(t1);
        Arrays.sort(t2);
        copy_S1 = new String(t1);
        copy_S2 = new String(t2);

        if (!copy_S1.equals(copy_S2)) {
            return false;
        }

        // make key of type string for search in map
        String key = (S1 + " " + S2);
        // checking if both string are before calculated or not
        // if calculated means find in map then return it's
        // value
        if (mp.containsKey(key)) {
            return mp.get(key);
        }

        // declaring flag variable to store result
        boolean flag = false;

        for (int i = 1; i < n; i++) {

            // Check if S2[0...i] is a scrambled
            // string of S1[0...i] and if S2[i+1...n]
            // is a scrambled string of S1[i+1...n]
            if (isScramble(S1.substring(0, i), S2.substring(0, i))
                && isScramble(S1.substring(i, n), S2.substring(i, n))) {
                flag = true;
                return true;
            }

            // Check if S2[0...i] is a scrambled
            // string of S1[n-i...n] and S2[i+1...n]
            // is a scramble string of S1[0...n-i-1]
            if (isScramble(S1.substring(0, i), S2.substring(n - i, n))
                && isScramble(S1.substring(i, n),
                              S2.substring(0, n - i))) {
                flag = true;
                return true;
            }
        }

        // add key & flag value to map (store for future use)
        // so next time no required to calculate it again
        mp.put(key, flag);

        // If none of the above conditions are satisfied
        return false;
    }

    public static void main(String[] args) {
        String S1 = "coder";
        String S2 = "ocred";

        if (isScramble(S1, S2)) {
            System.out.print("Yes");
        }
        else {
            System.out.print("No");
        }
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Declaring unordered map globally
map={}
# Python3 program to check if a
# given string is a scrambled
# form of another string
def isScramble(S1: str, S2: str):

    # Strings of non-equal length
    # cant' be scramble strings
    if len(S1) != len(S2):
        return False

    n = len(S1)

    # Empty strings are scramble strings
    if not n:
        return True

    # Equal strings are scramble strings
    if S1 == S2:
        return True

    # Check for the condition of anagram
    if sorted(S1) != sorted(S2):
        return False

    # Checking if both Substrings are in
    # map or are already calculated or not
    if(S1+' '+S2 in map):
        return map[S1+' '+S2]

    # Declaring a flag variable
    flag = False

    for i in range(1, n):

        # Check if S2[0...i] is a scrambled
        # string of S1[0...i] and if S2[i+1...n]
        # is a scrambled string of S1[i+1...n]
        if (isScramble(S1[:i], S2[:i]) and
            isScramble(S1[i:], S2[i:])):
            flag = True
            return True

        # Check if S2[0...i] is a scrambled
        # string of S1[n-i...n] and S2[i+1...n]
        # is a scramble string of S1[0...n-i-1]
        if (isScramble(S1[-i:], S2[:i]) and
            isScramble(S1[:-i], S2[i:])):
            flag = True
            return True

    # Storing calculated value to map
    map[S1+" "+S2] = flag

    # If none of the above
    # conditions are satisfied
    return False

# Driver Code
if __name__ == "__main__":

    S1 = "great"
    S2 = "rgate"

    if (isScramble(S1, S2)):
        print("Yes")
    else:
        print("No")
```

## C#

```
// C# Program to check if a
// given string is a scrambled
// form of another string
using System;
using System.Collections.Generic;
class GFG {

    // map declaration for storing key value pair
    // means for storing subproblem result
    static Dictionary<string, bool> mp = new Dictionary<string, bool>();

    static bool isScramble(string S1, string S2)
    {

        // Strings of non-equal length
        // cant' be scramble strings
        if (S1.Length != S2.Length) {
            return false;
        }

        int n = S1.Length;

        // Empty strings are scramble strings
        if (n == 0) {
            return true;
        }

        // Equal strings are scramble strings
        if (S1 == S2) {
            return true;
        }
        // Check for the condition of anagram
        string copy_S1 = S1, copy_S2 = S2;
        char[] t1 = copy_S1.ToCharArray();
        char[] t2 = copy_S2.ToCharArray();
        Array.Sort(t1);
        Array.Sort(t2);
        copy_S1 = new string(t1);
        copy_S2 = new string(t2);

        if (copy_S1 != copy_S2) {
            return false;
        }

        // make key of type string for search in map
        string key = (S1 + " " + S2);
        // checking if both string are before calculated or not
        // if calculated means find in map then return it's
        // value
        if (mp.ContainsKey(key)) {
            return mp[key];
        }

        // declaring flag variable to store result
        bool flag = false;

        for (int i = 1; i < n; i++) {

            // Check if S2[0...i] is a scrambled
            // string of S1[0...i] and if S2[i+1...n]
            // is a scrambled string of S1[i+1...n]
            if (isScramble(S1.Substring(0, i), S2.Substring(0, i))
                && isScramble(S1.Substring(i, n - i), S2.Substring(i, n - i))) {
                flag = true;
                return true;
            }

            // Check if S2[0...i] is a scrambled
            // string of S1[n-i...n] and S2[i+1...n]
            // is a scramble string of S1[0...n-i-1]
            if (isScramble(S1.Substring(0, i), S2.Substring(n - i, i))
                && isScramble(S1.Substring(i, n - i),
                              S2.Substring(0, n - i))) {
                flag = true;
                return true;
            }
        }

        // add key & flag value to map (store for future use)
        // so next time no required to calculate it again
        mp[key] = flag;

        // If none of the above conditions are satisfied
        return false;
    }

  static void Main() {
    string S1 = "coder";
    string S2 = "ocred";

    if (isScramble(S1, S2)) {
        Console.Write("Yes");
    }
    else {
        Console.Write("No");
    }
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript Program to check if a
    // given string is a scrambled
    // form of another string

    // map declaration for storing key value pair
    // means for storing subproblem result
    let mp = new Map();

    function isScramble(S1, S2)
    {
        // Strings of non-equal length
        // cant' be scramble strings
        if (S1.length != S2.length) {
            return false;
        }

        let n = S1.length;

        // Empty strings are scramble strings
        if (n == 0) {
            return true;
        }

        // Equal strings are scramble strings
        if (S1 == S2) {
            return true;
        }
        // Check for the condition of anagram
        let copy_S1 = S1, copy_S2 = S2;
        let t1 = copy_S1.split('')
        let t2 = copy_S2.split('')
        t1.sort();
        t2.sort();
        copy_S1 = t1.join("");
        copy_S2 = t2.join("");

        if (copy_S1 != copy_S2) {
            return false;
        }

        // make key of type string for search in map
        let key = (S1 + " " + S2);
        // checking if both string are before calculated or not
        // if calculated means find in map then return it's
        // value
        if (mp.has(key)) {
            return mp[key];
        }

        // declaring flag variable to store result
        let flag = false;

        for (let i = 1; i < n; i++) {

            // Check if S2[0...i] is a scrambled
            // string of S1[0...i] and if S2[i+1...n]
            // is a scrambled string of S1[i+1...n]
            if (isScramble(S1.substring(0, i), S2.substring(0, i))
                && isScramble(S1.substring(i, n),
                              S2.substring(i, n))) {
                flag = true;
                return true;
            }

            // Check if S2[0...i] is a scrambled
            // string of S1[n-i...n] and S2[i+1...n]
            // is a scramble string of S1[0...n-i-1]
            if (isScramble(S1.substring(0, i), S2.substring(n - i, n))
                && isScramble(S1.substring(i, n),
                              S2.substring(0, n - i))) {
                flag = true;
                return true;
            }
        }

        // add key & flag value to map (store for future use)
        // so next time no required to calculate it again
        mp[key] = flag;

        // If none of the above conditions are satisfied
        return false;
    }

    let S1 = "coder";
    let S2 = "ocred";

    if (isScramble(S1, S2)) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }

// This code is contributed by suresh07.
</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(N^2)，其中 n 是给定字符串的长度。
**辅助空间:** O(N^2)，因为我们需要在 mp 地图中存储 O(N^2)字符串。