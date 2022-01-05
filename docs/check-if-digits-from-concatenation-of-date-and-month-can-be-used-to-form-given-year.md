# 检查日期和月份串联的数字是否可以形成给定的年份

> 原文:[https://www . geesforgeks . org/check-if-digits-from-concation-date-and-month-to-form-given-year/](https://www.geeksforgeeks.org/check-if-digits-from-concatenation-of-date-and-month-can-be-used-to-form-given-year/)

给定代表日期的三个字符串 **D** 、 **M** 和 **Y** 。任务是检查日期和月份的串联是否产生与年份相同的数字。

**示例**:

> **输入** : D = 20，M = 12，Y = 2001
> **输出**:是
> **解释**:下面是执行的操作:
> D + M = 2012，Set1 = 0，1，2
> Y = 2001，Set2 = 0，1，2
> Set1 = Set2，所以答案是肯定的。
> 
> **输入** : D = 26，M = 07，Y = 2001
> T3】输出:否

**逼近**:给定的问题可以用 Hashing 来解决。按照以下步骤解决给定的问题。

*   声明两张无序地图，比如 **s1** 和 **s2** ，它们将存储 **(char，boolean)** 对。
*   创建字符串 **total_concat** ，该字符串将存储 **D** + **M** 。
*   遍历 **total_concat** 和 **Y** ，分别在 **s1** 和 **s2** 中存储字符。
*   运行 for 循环，在集合 1 中插入 **total_concat** 的所有数字，在集合 2 中插入 Y。
*   比较两张地图 **s1** 和 **s2** :
    *   如果 **s1 = s2** ，返回**是**。
    *   否则返回**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return whether the
// date is special or not
bool check(string D, string M, string Y)
{

    unordered_map<char, bool> s1;
    unordered_map<char, bool> s2;

    // Concatenate date and month
    string total_concat = D + M;

    // Insert the elements in set
    for (int i = 0; i < 4; i++) {
        s1[total_concat[i]] = true;
        s2[Y[i]] = true;
    }

    // Return 0 if size of both set
    // are unequal
    if (s1.size() != s2.size())
        return 0;

    // Return 1 if both set contains
    // same set of numbers otherwise
    // return 0
    else
        return (s1 == s2) ? 1 : 0;
}

// Driver Code
int main()
{
    string D = "20";
    string M = "12";
    string Y = "2001";

    if (check(D, M, Y))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

public class GFG
{
    // Function to return whether the
    // date is special or not
    static boolean check(String D, String M, String Y)
    {

        HashMap<Character, Boolean> s1 = new HashMap<>();
        HashMap<Character, Boolean> s2 = new HashMap<>();

        // Concatenate date and month
        String total_concat = D + M;

        // Insert the elements in set
        for (int i = 0; i < 4; i++) {
            s1.put(total_concat.charAt(i), true);
            s2.put(Y.charAt(i), true);
        }

        // Return 0 if size of both set
        // are unequal
        if (s1.size() != s2.size())
            return false;

        // Return 1 if both set contains
        // same set of numbers otherwise
        // return 0
        else
            return s1.equals(s2);
    }

    // Driver Code
    public static void main(String[] args) {

        String D = "20";
        String M = "12";
        String Y = "2001";

        if (check(D, M, Y))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# python program for the above approach

# Function to return whether the
# date is special or not
def check(D, M, Y):

    s1 = {}
    s2 = {}

    # Concatenate date and month
    total_concat = D + M

    # Insert the elements in set
    for i in range(0, 4):
        s1[total_concat[i]] = True
        s2[Y[i]] = True

    # Return 0 if size of both set
    # are unequal
    if (len(s1) != len(s2)):
        return 0

    # Return 1 if both set contains
    # same set of numbers otherwise
    # return 0
    else:
        return s1 == s2

# Driver Code
if __name__ == "__main__":

    D = "20"
    M = "12"
    Y = "2001"

    if (check(D, M, Y)):
        print("Yes")
    else:
        print("No")

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to return whether the
        // date is special or not
        function check(D, M, Y) {

            let s1 = new Map();
            let s2 = new Map();

            // Concatenate date and month
            let total_concat = D + M;

            // Insert the elements in set
            for (let i = 0; i < 4; i++) {
                s1.set(total_concat.charAt(i), true);
                s2.set(Y.charAt(i), true);
            }

            // Return 0 if size of both set
            // are unequal
            if (s1.size != s2.size)
                return 0;

            // Return 1 if both set contains
            // same set of numbers otherwise
            // return 0
            else
                return (s1.keys == s2.keys) ? 1 : 0;
        }

        // Driver Code
        let D = "20";
        let M = "12";
        let Y = "2001";

        if (check(D, M, Y))
            document.write("Yes");
        else
            document.write("No");

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
Yes
```

**时间复杂度:** O(Y)，其中 Y 为年的大小。

**辅助空间:** O(1)