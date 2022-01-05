# 检查一个字符串是否包含所有频率相同的字符，允许有一个变化

> 原文:[https://www . geesforgeks . org/check-if-a-string-all-characters-同频同变-允许/](https://www.geeksforgeeks.org/check-if-a-string-has-all-characters-with-same-frequency-with-one-variation-allowed/)

给定一串小写字母，通过删除 1 或 0 个字符来查找它是否可以转换为有效字符串。“有效”字符串是字符串**字符串**，这样对于**字符串**中的所有不同字符，每个这样的字符在其中出现的次数都相同。
例子:

```
Input : string str = "abbca"
Output : Yes
We can make it valid by removing "c"

Input : string str = "aabbcd"
Output : No
We need to remove at least two characters
to make it valid.

Input : string str = "abbccd"
Output : No
```

我们只允许遍历字符串一次。

这个想法是使用一个存储所有字符频率的频率数组。一旦我们有了一个数组中所有字符的频率，我们就会检查不同值和非零值的总数是否不超过 2。此外，两个允许的不同频率的计数之一必须小于或等于 2。下面是 idea 的实现。

## C++

```
// C++ program to check if a string can be made
// valid by removing at most 1 character.
#include<bits/stdc++.h>
using namespace std;

// Assuming only lower case characters
const int CHARS = 26;

/* To check a string S can be converted to a “valid”
   string by removing less than or equal to one
   character. */
bool isValidString(string str)
{
    int freq[CHARS] = {0};

    // freq[] : stores the  frequency of each
    // character of a string
    for (int i=0; i<str.length(); i++)
        freq[str[i]-'a']++;

    // Find first character with non-zero frequency
    int i, freq1 = 0, count_freq1 = 0;
    for (i=0; i<CHARS; i++)
    {
        if (freq[i] != 0)
        {
            freq1  = freq[i];
            count_freq1 = 1;
            break;
        }
    }

    // Find a character with frequency different
    // from freq1.
    int j, freq2 = 0, count_freq2 = 0;
    for (j=i+1; j<CHARS; j++)
    {
        if (freq[j] != 0)
        {
            if (freq[j] == freq1)
               count_freq1++;
            else
            {
                count_freq2 = 1;
                freq2 = freq[j];
                break;
            }
        }
    }

    // If we find a third non-zero frequency
    // or count of both frequencies become more
    // than 1, then return false
    for (int k=j+1; k<CHARS; k++)
    {
        if (freq[k] != 0)
        {
            if (freq[k] == freq1)
               count_freq1++;
            if (freq[k] == freq2)
               count_freq2++;
            else  // If we find a third non-zero freq
               return false;
        }

        // If counts of both frequencies is more than 1
        if (count_freq1 > 1 && count_freq2 > 1)
           return false;
    }

    // Return true if we reach here
    return true;
}

// Driver code
int main()
{
    char str[] = "abcbc";

    if (isValidString(str))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string can be made
// valid by removing at most 1 character.
public class GFG {

// Assuming only lower case characters
    static int CHARS = 26;

    /* To check a string S can be converted to a “valid”
   string by removing less than or equal to one
   character. */
    static boolean isValidString(String str) {
        int freq[] = new int[CHARS];

        // freq[] : stores the  frequency of each
        // character of a string
        for (int i = 0; i < str.length(); i++) {
            freq[str.charAt(i) - 'a']++;
        }

        // Find first character with non-zero frequency
        int i, freq1 = 0, count_freq1 = 0;
        for (i = 0; i < CHARS; i++) {
            if (freq[i] != 0) {
                freq1 = freq[i];
                count_freq1 = 1;
                break;
            }
        }

        // Find a character with frequency different
        // from freq1.
        int j, freq2 = 0, count_freq2 = 0;
        for (j = i + 1; j < CHARS; j++) {
            if (freq[j] != 0) {
                if (freq[j] == freq1) {
                    count_freq1++;
                } else {
                    count_freq2 = 1;
                    freq2 = freq[j];
                    break;
                }
            }
        }

        // If we find a third non-zero frequency
        // or count of both frequencies become more
        // than 1, then return false
        for (int k = j + 1; k < CHARS; k++) {
            if (freq[k] != 0) {
                if (freq[k] == freq1) {
                    count_freq1++;
                }
                if (freq[k] == freq2) {
                    count_freq2++;
                } else // If we find a third non-zero freq
                {
                    return false;
                }
            }

            // If counts of both frequencies is more than 1
            if (count_freq1 > 1 && count_freq2 > 1) {
                return false;
            }
        }

        // Return true if we reach here
        return true;
    }

// Driver code
    public static void main(String[] args) {
        String str = "abcbc";

        if (isValidString(str)) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to check if
# a string can be made
# valid by removing at most 1 character.

# Assuming only lower case characters
CHARS = 26

# To check a string S can be converted to a “valid”
# string by removing less than or equal to one
# character.

def isValidString(str):

    freq = [0]*CHARS

    # freq[] : stores the frequency of each
    # character of a string
    for i in range(len(str)):
        freq[ord(str[i])-ord('a')] += 1

    # Find first character with non-zero frequency
    freq1 = 0
    count_freq1 = 0
    for i in range(CHARS):

        if (freq[i] != 0):

            freq1 = freq[i]
            count_freq1 = 1
            break

    # Find a character with frequency different
    # from freq1.
    freq2 = 0
    count_freq2 = 0
    for j in range(i+1,CHARS):

        if (freq[j] != 0):

            if (freq[j] == freq1):
                count_freq1 += 1
            else:

                count_freq2 = 1
                freq2 = freq[j]
                break

    # If we find a third non-zero frequency
    # or count of both frequencies become more
    # than 1, then return false
    for k in range(j+1,CHARS):

        if (freq[k] != 0):

            if (freq[k] == freq1):
                count_freq1 += 1
            if (freq[k] == freq2):
                count_freq2 += 1

            # If we find a third non-zero freq
            else:
                return False

        # If counts of both frequencies is more than 1
        if (count_freq1 > 1 and count_freq2 > 1):
            return False

    # Return true if we reach here
    return True

# Driver code
if __name__ == "__main__":
    str= "abcbc"

    if (isValidString(str)):
        print("YES")
    else:
        print("NO")

# this code is contributed by
# ChitraNayal
```

## C#

```
// C# program to check if a string can be made
// valid by removing at most 1 character.
using System;
public class GFG {

// Assuming only lower case characters
    static int CHARS = 26;

    /* To check a string S can be converted to a “valid”
string by removing less than or equal to one
character. */
    static bool isValidString(String str) {
        int []freq = new int[CHARS];
        int i=0;
        // freq[] : stores the frequency of each
        // character of a string
        for ( i= 0; i < str.Length; i++) {
            freq[str[i] - 'a']++;
        }

        // Find first character with non-zero frequency
        int freq1 = 0, count_freq1 = 0;
        for (i = 0; i < CHARS; i++) {
            if (freq[i] != 0) {
                freq1 = freq[i];
                count_freq1 = 1;
                break;
            }
        }

        // Find a character with frequency different
        // from freq1.
        int j, freq2 = 0, count_freq2 = 0;
        for (j = i + 1; j < CHARS; j++) {
            if (freq[j] != 0) {
                if (freq[j] == freq1) {
                    count_freq1++;
                } else {
                    count_freq2 = 1;
                    freq2 = freq[j];
                    break;
                }
            }
        }

        // If we find a third non-zero frequency
        // or count of both frequencies become more
        // than 1, then return false
        for (int k = j + 1; k < CHARS; k++) {
            if (freq[k] != 0) {
                if (freq[k] == freq1) {
                    count_freq1++;
                }
                if (freq[k] == freq2) {
                    count_freq2++;
                } else // If we find a third non-zero freq
                {
                    return false;
                }
            }

            // If counts of both frequencies is more than 1
            if (count_freq1 > 1 && count_freq2 > 1) {
                return false;
            }
        }

        // Return true if we reach here
        return true;
    }

// Driver code
    public static void Main() {
        String str = "abcbc";

        if (isValidString(str)) {
            Console.WriteLine("YES");
        } else {
            Console.WriteLine("NO");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to check if a string can be made
// valid by removing at most 1 character.

// Assuming only lower case characters
let CHARS = 26;

/* To check a string S can be converted to a “valid”
   string by removing less than or equal to one
   character. */
function isValidString(str)
{
    let freq = new Array(CHARS);
    for(let i=0;i<CHARS;i++)
    {
        freq[i]=0;
    }

        // freq[] : stores the  frequency of each
        // character of a string
        for (let i = 0; i < str.length; i++) {
            freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // Find first character with non-zero frequency
        let i, freq1 = 0, count_freq1 = 0;
        for (i = 0; i < CHARS; i++) {
            if (freq[i] != 0) {
                freq1 = freq[i];
                count_freq1 = 1;
                break;
            }
        }

        // Find a character with frequency different
        // from freq1.
        let j, freq2 = 0, count_freq2 = 0;
        for (j = i + 1; j < CHARS; j++) {
            if (freq[j] != 0) {
                if (freq[j] == freq1) {
                    count_freq1++;
                } else {
                    count_freq2 = 1;
                    freq2 = freq[j];
                    break;
                }
            }
        }

        // If we find a third non-zero frequency
        // or count of both frequencies become more
        // than 1, then return false
        for (let k = j + 1; k < CHARS; k++) {
            if (freq[k] != 0) {
                if (freq[k] == freq1) {
                    count_freq1++;
                }
                if (freq[k] == freq2) {
                    count_freq2++;
                } else // If we find a third non-zero freq
                {
                    return false;
                }
            }

            // If counts of both frequencies is more than 1
            if (count_freq1 > 1 && count_freq2 > 1) {
                return false;
            }
        }

        // Return true if we reach here
        return true;
}

// Driver code
let str = "abcbc";

        if (isValidString(str)) {
            document.write("YES");
        } else {
            document.write("NO");
        }

// This code is contributed by ab2127

</script>
```

**输出:**

```
YES
```

我们只遍历一次字符串。第一个循环之后的三个循环总共运行 CHARS 次。
**另一种方法:**(使用 HashMap)
下面是实现。

## C++

```
// C++ program to check if a string can be made
// valid by removing at most 1 character using hashmap.
#include <bits/stdc++.h>
using namespace std;

// To check a string S can be converted to a variation
// string 
bool checkForVariation(string str)
{
    if(str.empty() || str.length() != 0)
    {
        return true;
    }
    map<char, int> mapp;

    // Run loop form 0 to length of string
    for(int i = 0; i < str.length(); i++)
    {
        mapp[str[i]]++;
    }

    // declaration of variables
    bool first = true, second = true;
    int val1 = 0, val2 = 0;
    int countOfVal1 = 0, countOfVal2 = 0;

    map<char, int>::iterator itr;
    for (itr = mapp.begin(); itr != mapp.end(); ++itr)
    {
        int i = itr->first;

        // if first is true than countOfVal1 increase
        if(first) 
        {
            val1 = i;
            first = false;
            countOfVal1++;
            continue;
        }
        if(i == val1)
        {
            countOfVal1++;
            continue;
        }

        // if second is true than countOfVal2 increase
        if(second)
        {
            val2 = i;
            countOfVal2++;
            second = false;
            continue;
        }

        if(i == val2)
        {
            countOfVal2++;
            continue;
        }

        return false;
    }

    if(countOfVal1 > 1 && countOfVal2 > 1) 
    {
        return false;
    }
    else
    {
        return true;
    }    

}

// Driver code
int main() {
    if(checkForVariation("abcbcvf"))
        cout << "true" << endl;
    else
        cout << "false" << endl;

    return 0;
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string can be made
// valid by removing at most 1 character using hashmap.
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class AllCharsWithSameFrequencyWithOneVarAllowed {

    // To check a string S can be converted to a variation
    // string
    public static boolean checkForVariation(String str) {
        if(str == null || str.isEmpty()) {
            return true;
        }

        Map<Character, Integer> map = new HashMap<>();

        // Run loop form 0 to length of string
        for(int i = 0; i < str.length(); i++) {
            map.put(str.charAt(i), map.getOrDefault(str.charAt(i), 0) + 1);
        }
        Iterator<Integer> itr = map.values().iterator();

        // declaration of variables
        boolean first = true, second = true;
        int val1 = 0, val2 = 0;
        int countOfVal1 = 0, countOfVal2 = 0;

        while(itr.hasNext()) {
            int i = itr.next();

            // if first is true than countOfVal1 increase
            if(first) {
                val1 = i;
                first = false;
                countOfVal1++;
                continue;
            }

            if(i == val1) {
                countOfVal1++;
                continue;
            }

            // if second is true than countOfVal2 increase
            if(second) {
                val2 = i;
                countOfVal2++;
                second = false;
                continue;
            }

            if(i == val2) {
                countOfVal2++;
                continue;
            }

            return false;
        }

        if(countOfVal1 > 1 && countOfVal2 > 1) {
            return false;
        }else {
            return true;
        }

    }

    // Driver code
    public static void main(String[] args)
    {

        System.out.println(checkForVariation("abcbc"));
    }
}
```

## 蟒蛇 3

```
# Python program to check if a string can be made
# valid by removing at most 1 character using hashmap.

# To check a string S can be converted to a variation
# string
def checkForVariation(strr):
    if(len(strr) == 0):
        return True

    mapp = {}

    # Run loop form 0 to length of string   
    for i in range(len(strr)):
        if strr[i] in mapp:
            mapp[strr[i]] += 1
        else:
            mapp[strr[i]] = 1

    # declaration of variables
    first = True
    second = True
    val1 = 0
    val2 = 0
    countOfVal1 = 0
    countOfVal2 = 0

    for itr in mapp:
        i = itr

        # if first is true than countOfVal1 increase
        if(first):
            val1 = i
            first = False
            countOfVal1 += 1
            continue

        if(i == val1):
            countOfVal1 += 1
            continue

        # if second is true than countOfVal2 increase
        if(second):
            val2 = i
            countOfVal2 += 1
            second = False
            continue

        if(i == val2):
            countOfVal2 += 1
            continue
    if(countOfVal1 > 1 and countOfVal2 > 1):
        return False

    else:
        return True

# Driver code
print(checkForVariation("abcbc"))

# This code is contributed by rag2127
```

## C#

```
// C# program to check if a string can be made
// valid by removing at most 1 character using hashmap.
using System;
using System.Collections.Generic;

public class AllCharsWithSameFrequencyWithOneVarAllowed
{

    // To check a string S can be converted to a variation
    // string
    public static bool checkForVariation(String str)
    {
        if(str == null || str.Length != 0)
        {
            return true;
        }

        Dictionary<char, int> map = new Dictionary<char, int>();

        // Run loop form 0 to length of string
        for(int i = 0; i < str.Length; i++)
        {
            if(map.ContainsKey(str[i]))
                map[str[i]] = map[str[i]]+1;
            else
                map.Add(str[i], 1);
        }

        // declaration of variables
        bool first = true, second = true;
        int val1 = 0, val2 = 0;
        int countOfVal1 = 0, countOfVal2 = 0;

        foreach(KeyValuePair<char, int> itr in map)
        {
            int i = itr.Key;

            // if first is true than countOfVal1 increase
            if(first)
            {
                val1 = i;
                first = false;
                countOfVal1++;
                continue;
            }

            if(i == val1)
            {
                countOfVal1++;
                continue;
            }

            // if second is true than countOfVal2 increase
            if(second)
            {
                val2 = i;
                countOfVal2++;
                second = false;
                continue;
            }

            if(i == val2)
            {
                countOfVal2++;
                continue;
            }

            return false;
        }

        if(countOfVal1 > 1 && countOfVal2 > 1)
        {
            return false;
        }
        else
        {
            return true;
        }

    }

    // Driver code
    public static void Main(String[] args)
    {

        Console.WriteLine(checkForVariation("abcbc"));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to check if a string can be made
// valid by removing at most 1 character using hashmap.

 // To check a string S can be converted to a variation
    // string
function checkForVariation(str)
{
    if(str == null || str.length==0) {
            return true;
        }

        let map = new Map();

        // Run loop form 0 to length of string
        for(let i = 0; i < str.length; i++) {
            if(!map.has(str[i]))
                map.set(str[i],0);
            map.set(str[i], map.get(str[i]) + 1);
        }

        // declaration of variables
        let first = true, second = true;
        let val1 = 0, val2 = 0;
        let countOfVal1 = 0, countOfVal2 = 0;

        for(let [key, value] of map.entries()) {
            let i = value;

            // if first is true than countOfVal1 increase
            if(first) {
                val1 = i;
                first = false;
                countOfVal1++;
                continue;
            }

            if(i == val1) {
                countOfVal1++;
                continue;
            }

            // if second is true than countOfVal2 increase
            if(second) {
                val2 = i;
                countOfVal2++;
                second = false;
                continue;
            }

            if(i == val2) {
                countOfVal2++;
                continue;
            }

            return false;
        }

        if(countOfVal1 > 1 && countOfVal2 > 1) {
            return false;
        }else {
            return true;
        }
}

 // Driver code
document.write(checkForVariation("abcbc"));

// This code is contributed by patel2127

</script>
```

**输出:**

```
true
```

#### 另一种方法:使用内置的 Python 函数

*   使用 [**【计数器()**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能计算所有字符的频率。
*   将这些频率转换到列表中。
*   使用计数器再次计算此列表的频率。
*   如果计数器的长度为 1，则返回真。
*   如果计数器的长度是 2，如果最小值是 1，则返回真。
*   否则返回假。

下面是实现:

## 蟒蛇 3

```
# Python program
from collections import Counter

# To check a string S can be
# converted to a variation
# string
def checkForVariation(strr):

    freq = Counter(strr)

    # Converting these values to list
    valuelist = list(freq.values())

    # Counting frequencies again
    ValueCounter = Counter(valuelist)
    if(len(ValueCounter) == 1):
        return True
    elif(len(ValueCounter) == 2 and
         min(ValueCounter.values()) == 1):
        return True

    # If no conditions satisfied return false
    return False

# Driver code
string = "abcbc"

# passing string to checkForVariation Function
print(checkForVariation(string))

# This code is contributed by vikkycirus
```

**输出:**

```
true
```

**时间复杂度:** O(n)

**空间复杂度:** O(n)

本文由 **Nishant_singh(pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。