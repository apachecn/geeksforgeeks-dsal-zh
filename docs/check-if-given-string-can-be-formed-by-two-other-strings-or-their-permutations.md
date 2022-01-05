# 检查给定的字符串是否可以由另外两个字符串或它们的排列组成

> 原文:[https://www . geesforgeks . org/check-if-给定字符串可以由两个其他字符串或它们的排列组成/](https://www.geeksforgeeks.org/check-if-given-string-can-be-formed-by-two-other-strings-or-their-permutations/)

给定一个字符串 **str** 和一个字符串数组 **arr[]** ，任务是检查给定的字符串是否可以由数组中的任何字符串对或它们的排列组成。

**示例:**

> **输入:** str = "amazon "，arr[] = {"loa "、" azo "、" ft "、" amn "、" lka"}
> **输出:** Yes
> 选择的字符串为“amn”和“azo”
> ，可以重新排列为“amazon”。
> 
> **输入:** str = "geeksforgeeks "，arr[] = {"geeks "，" geek "，" for"}
> **输出:**否

**方法 1:** 我们首先对给定的字符串进行排序，然后运行两个嵌套循环，一次从给定的数组中选择两个字符串并将其连接起来，然后对结果字符串进行排序。
排序后，我们检查它是否等于我们给定的排序字符串。
因此，总时间复杂度将为 0(n * mlogm)，其中 n 是给定数组的大小，m 是字符串的长度(最大值)。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
bool isPossible(vector<string> v, string str)
{

    // Sort the given string
    sort(str.begin(), str.end());

    // Select two strings at a time from given vector
    for (int i = 0; i < v.size() - 1; i++) {
        for (int j = i + 1; j < v.size(); j++) {

            // Get the concatenated string
            string temp = v[i] + v[j];

            // Sort the resultant string
            sort(temp.begin(), temp.end());

            // If the resultant string is equal
            // to the given string str
            if (temp.compare(str) == 0) {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Driver code
int main()
{
    string str = "amazon";
    vector<string> v{ "fds", "oxq", "zoa", "epw", "amn" };

    if (isPossible(v, str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
static boolean isPossible(Vector<String> v, String str)
{

    // Sort the given string
    str = sortString(str);

    // Select two strings at a time from given vector
    for (int i = 0; i < v.size() - 1; i++)
    {
        for (int j = i + 1; j < v.size(); j++)
        {

            // Get the concatenated string
            String temp = v.get(i) + v.get(j);

            // Sort the resultant string
            temp = sortString(temp);

            // If the resultant string is equal
            // to the given string str
            if (temp.compareTo(str) == 0)
            {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Method to sort a string alphabetically
public static String sortString(String inputString)
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
    String str = "amazon";
    String []arr = { "fds", "oxq", "zoa", "epw", "amn" };
    Vector<String> v = new Vector<String>(Arrays.asList(arr));

    if (isPossible(v, str))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if str can be
# generated from any permutation of the
# two strings selected from the given vector
def isPossible(v, string ) :

    char_list = list(string)

    # Sort the given string
    char_list.sort()

    # Select two strings at a time from given vector
    for i in range(len(v)-1) :
        for j in range(len(v)) :

            # Get the concatenated string
            temp = v[i] + v[j];

            # Sort the resultant string
            temp_list = list(temp)
            temp_list.sort()

            # If the resultant string is equal
            # to the given string str
            if (temp_list == char_list) :
                return True;

    # No valid pair found
    return False;

# Driver code
if __name__ == "__main__" :

    string = "amazon";
    v = [ "fds", "oxq", "zoa", "epw", "amn" ];

    if (isPossible(v, string)):
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
static Boolean isPossible(List<String> v, String str)
{

    // Sort the given string
    str = sortString(str);

    // Select two strings at a time from given vector
    for (int i = 0; i <v.Count - 1; i++)
    {
        for (int j = i + 1; j <v.Count; j++)
        {

            // Get the concatenated string
            String temp = v[i] + v[j];

            // Sort the resultant string
            temp = sortString(temp);

            // If the resultant string is equal
            // to the given string str
            if (temp.CompareTo(str) == 0)
            {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Method to sort a string alphabetically
public static String sortString(String inputString)
{
    // convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // sort tempArray
    Array.Sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Driver code
public static void Main(String[] args)
{
    String str = "amazon";
    String []arr = { "fds", "oxq", "zoa", "epw", "amn" };
    List<String> v = new List<String>(arr);

    if (isPossible(v, str))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
function isPossible(v, str)
{

    // Sort the given string
    str = str.split('').sort().join('');

    // Select two strings at a time from given vector
    for (var i = 0; i < v.length - 1; i++) {
        for (var j = i + 1; j < v.length; j++) {

            // Get the concatenated string
            var temp = v[i] + v[j];

            // Sort the resultant string
            temp = temp.split('').sort().join('');

            // If the resultant string is equal
            // to the given string str
            if (temp === (str)) {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Driver code
var str = "amazon";
var v = ["fds", "oxq", "zoa", "epw", "amn"];
if (isPossible(v, str))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**方法二:** [计数排序](https://www.geeksforgeeks.org/counting-sort/)可以用来减少上述方法的运行时间。计数排序使用一个表来存储每个字符的计数。我们有 26 个字母，因此我们制作了一个大小为 26 的数组来存储字符串中每个字符的计数。然后按照递增的顺序取字符，得到排序后的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 26

// Function to sort the given string
// using counting sort
void countingsort(string& s)
{
    // Array to store the count of each character
    int count[MAX] = { 0 };
    for (int i = 0; i < s.length(); i++) {
        count[s[i] - 'a']++;
    }
    int index = 0;

    // Insert characters in the string
    // in increasing order
    for (int i = 0; i < MAX; i++) {
        int j = 0;
        while (j < count[i]) {
            s[index++] = i + 'a';
            j++;
        }
    }
}

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
bool isPossible(vector<string> v, string str)
{

    // Sort the given string
    countingsort(str);

    // Select two strings at a time from given vector
    for (int i = 0; i < v.size() - 1; i++) {
        for (int j = i + 1; j < v.size(); j++) {

            // Get the concatenated string
            string temp = v[i] + v[j];

            // Sort the resultant string
            countingsort(temp);

            // If the resultant string is equal
            // to the given string str
            if (temp.compare(str) == 0) {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Driver code
int main()
{
    string str = "amazon";
    vector<string> v{ "fds", "oxq", "zoa", "epw", "amn" };

    if (isPossible(v, str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 26;

// Function to sort the given string
// using counting sort
static String countingsort(char[] s)
{

    // Array to store the count of each character
    int []count = new int[MAX];
    for (int i = 0; i < s.length; i++)
    {
        count[s[i] - 'a']++;
    }
    int index = 0;

    // Insert characters in the string
    // in increasing order
    for (int i = 0; i < MAX; i++)
    {
        int j = 0;
        while (j < count[i])
        {
            s[index++] = (char)(i + 'a');
            j++;
        }
    }
        return String.valueOf(s);
}

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
static boolean isPossible(Vector<String> v,
                                 String str)
{

    // Sort the given string
    str=countingsort(str.toCharArray());

    // Select two strings at a time from given vector
    for (int i = 0; i < v.size() - 1; i++)
    {
        for (int j = i + 1; j < v.size(); j++)
        {

            // Get the concatenated string
            String temp = v.get(i) + v.get(j);

            // Sort the resultant string
            temp = countingsort(temp.toCharArray());

            // If the resultant string is equal
            // to the given string str
            if (temp.equals(str))
            {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Driver code
public static void main(String[] args)
{
    String str = "amazon";
    String []arr = { "fds", "oxq", "zoa", "epw", "amn" };
    Vector<String> v = new Vector<String>(Arrays.asList(arr));

    if (isPossible(v, str))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 26

# Function to sort the given string
# using counting sort
def countingsort(s):
    # Array to store the count of each character
    count = [0 for i in range(MAX)]
    for i in range(len(s)):
        count[ord(s[i]) - ord('a')] += 1
    index = 0

    # Insert characters in the string
    # in increasing order

    for i in range(MAX):
        j = 0
        while (j < count[i]):
            s = s.replace(s[index],chr(97+i))
            index += 1
            j += 1

# Function that returns true if str can be
# generated from any permutation of the
# two strings selected from the given vector
def isPossible(v, str1):
    # Sort the given string
    countingsort(str1);

    # Select two strings at a time from given vector
    for i in range(len(v)-1):
        for j in range(i + 1,len(v),1):
            # Get the concatenated string
            temp = v[i] + v[j]

            # Sort the resultant string
            countingsort(temp)

            # If the resultant string is equal
            # to the given string str
            if (temp == str1):
                return False

    # No valid pair found
    return True

# Driver code
if __name__ == '__main__':
    str1 = "amazon"
    v = ["fds", "oxq", "zoa", "epw", "amn"]

    if (isPossible(v, str1)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 26;

// Function to sort the given string
// using counting sort
static String countingsort(char[] s)
{

    // Array to store the count of each character
    int []count = new int[MAX];
    for (int i = 0; i < s.Length; i++)
    {
        count[s[i] - 'a']++;
    }

    int index = 0;

    // Insert characters in the string
    // in increasing order
    for (int i = 0; i < MAX; i++)
    {
        int j = 0;
        while (j < count[i])
        {
            s[index++] = (char)(i + 'a');
            j++;
        }
    }
        return String.Join("", s);
}

// Function that returns true if str can be
// generated from any permutation of the
// two strings selected from the given vector
static Boolean isPossible(List<String> v,
                               String str)
{

    // Sort the given string
    str = countingsort(str.ToCharArray());

    // Select two strings at a time from given vector
    for (int i = 0; i < v.Count - 1; i++)
    {
        for (int j = i + 1; j < v.Count; j++)
        {

            // Get the concatenated string
            String temp = v[i] + v[j];

            // Sort the resultant string
            temp = countingsort(temp.ToCharArray());

            // If the resultant string is equal
            // to the given string str
            if (temp.Equals(str))
            {
                return true;
            }
        }
    }

    // No valid pair found
    return false;
}

// Driver code
public static void Main(String[] args)
{
    String str = "amazon";
    String []arr = { "fds", "oxq",
                     "zoa", "epw", "amn" };
    List<String> v = new List<String>(arr);

    if (isPossible(v, str))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let MAX = 26;

    // Function to sort the given string
    // using counting sort
    function countingsort(s)
    {

        // Array to store the count of each character
        let count = new Array(MAX);
        count.fill(0);
        for (let i = 0; i < s.length; i++)
        {
            count[s[i].charCodeAt() - 'a'.charCodeAt()]++;
        }
        let index = 0;

        // Insert characters in the string
        // in increasing order
        for (let i = 0; i < MAX; i++)
        {
            let j = 0;
            while (j < count[i])
            {
                s[index++] = String.fromCharCode(i + 'a'.charCodeAt());
                j++;
            }
        }
          return s.join("");
    }

    // Function that returns true if str can be
    // generated from any permutation of the
    // two strings selected from the given vector
    function isPossible(v, str)
    {

        // Sort the given string
        str = countingsort(str.split(''));

        // Select two strings at a time from given vector
        for (let i = 0; i < v.length - 1; i++)
        {
            for (let j = i + 1; j < v.length; j++)
            {

                // Get the concatenated string
                let temp = v[i] + v[j];

                // Sort the resultant string
                temp = countingsort(temp.split(''));

                // If the resultant string is equal
                // to the given string str
                if (temp == str)
                {
                    return true;
                }
            }
        }

        // No valid pair found
        return false;
    }

    let str = "amazon";
    let v = [ "fds", "oxq", "zoa", "epw", "amn" ];

    if (isPossible(v, str))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```