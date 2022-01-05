# 按升序排列数值字符串的向量

> 原文:[https://www . geesforgeks . org/sort-vector-of-numeric-strings-in-升序/](https://www.geeksforgeeks.org/sort-vector-of-numeric-strings-in-ascending-order/)

给定一个数值字符串的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**arr[]**，任务是按升序对给定的数值字符串向量进行排序。

**示例:**

> **输入:**arr[]= {“120000”、“2”、“33”}
> **输出:**{“2”、“33”、“120000”}
> 
> **输入:**arr[]= {“120”、“2”、“3”}
> **输出:**{“2”、“3”、“120”}

**方法:**[c++](https://www.geeksforgeeks.org/c-plus-plus/)[STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)中的[排序()函数](https://www.geeksforgeeks.org/sort-c-stl/)能够对字符串的向量进行[排序](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)如果且仅当它包含单个数字字符，例如{ '1 '，' ' }，但是要对包含多个字符的字符串的数字向量进行排序，例如{'12 '，' 56 '，' 14' }应该在 sort()函数中编写自己的比较器。按照升序逻辑排序的比较器函数如下:

> 让我们考虑下面给出的两种情况来构建一个比较器函数:
> 
> *   **情况 1:** 如果[字符串](https://www.geeksforgeeks.org/string-data-structure/)的长度不相同，那么首先放置一个较小长度的字符串，例如，{'12 '，' 2'}将' 2 '放在' 12 '之前，因为' 2 '小于' 12 '。
> *   **情况 2:** 如果长度相同，则将数值较小的字符串放在前面，例如，“1”，“2”将“1”放在“2”之前。

下面是实现上述方法的 [C++程序](https://www.geeksforgeeks.org/c-plus-plus/):

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator Function
bool myCmp(string s1, string s2)
{

    // If size of numeric strings
    // are same the put lowest value
    // first
    if (s1.size() == s2.size()) {
        return s1 < s2;
    }

    // If size is not same put the
    // numeric string with less
    // number of digits first
    else {
        return s1.size() < s2.size();
    }
}

// Driver Code
int main()
{
    vector<string> v
        = { "12", "2", "10", "6", "4", "99", "12" };

    // Calling sort function with
    // custom comparator
    sort(v.begin(), v.end(), myCmp);

    // Print the vector values after
    // sorting
    for (auto it : v) {
        cout << it << " ";
    }

    cout << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Comparator Function
static List<String> sort(List<String> list)
{
    Comparator<String> cmp = (o1, o2) -> {
        // If size of numeric Strings
        // are same the put lowest value
        // first
        if (o1.length() == o2.length()) {
            return Integer.valueOf(o1)-Integer.valueOf(o2);
        }

        // If size is not same put the
        // numeric String with less
        // number of digits first
        else {
            return o1.length()-o2.length();
        }
    };
    Collections.sort(list, cmp);
    return list;
}

// Driver Code
public static void main(String[] args)
{
    List<String> v
        = Arrays.asList( "12", "2", "10", "6", "4", "99", "12" );

    // Calling sort function with
    // custom comparator
    v = sort(v);

    // Print the vector values after
    // sorting
    for (String it : v) {
        System.out.print(it+ " ");
    }

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Comparator Function
        function myCmp(s1, s2) {

            // If size of numeric strings
            // are same the put lowest value
            // first
            if (s1.length == s2.length) {
                return parseInt(s1) - parseInt(s2);
            }

            // If size is not same put the
            // numeric string with less
            // number of digits first
            else {
                return s1.length - s2.length;
            }
        }

        // Driver Code

        let v
            = ["12", "2", "10", "6", "4", "99", "12"];

        // Calling sort function with
        // custom comparator
        v.sort(myCmp)

        // Print the vector values after
        // sorting
        for (let i = 0; i < v.length; i++) {
            document.write(v[i] + " ")
        }

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2 4 6 10 12 12 99
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*