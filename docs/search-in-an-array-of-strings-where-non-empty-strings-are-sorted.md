# 在字符串数组中搜索非空字符串排序

> 原文:[https://www . geeksforgeeks . org/字符串数组中的搜索-其中非空字符串被排序/](https://www.geeksforgeeks.org/search-in-an-array-of-strings-where-non-empty-strings-are-sorted/)

给定一个字符串数组。数组既有空字符串，也有非空字符串。所有非空字符串都按排序顺序排列。空字符串可以出现在非空字符串之间的任何位置。

**示例:**

```
Input :  arr[] =  {"for", "", "", "", "geeks", 
                   "ide", "", "practice", "" , 
                   "", "quiz", "", ""};
          str = "quiz"
Output :   10
The string "quiz" is present at index 10 in 
given array.
```

一个简单解决方案是在字符串数组中线性搜索给定的字符串。

一个**更好的解决方案**就是做改装二分搜索法。像普通二分搜索法一样，我们将给定字符串与中间字符串进行比较。如果中间字符串是空的，我们会找到最近的非空字符串 x(通过在两边线性搜索)。一旦我们找到 x，我们就做标准二分搜索法，也就是说，我们把给定的 str 与 x 进行比较。如果 str 与 x 相同，我们返回 x 的索引。如果 str 更大，我们对右半部分进行递归，否则我们对左半部分进行递归。

下面是这个想法的实现:

## C++

```
// C++ program to find location of a str in
// an array of strings which is sorted and
// has empty strings between strings.
#include <bits/stdc++.h>
using namespace std;

// Compare two string equals are not
int compareStrings(string str1, string str2)
{
    int i = 0;
    while (str1[i] == str2[i] && str1[i] != '\0')
        i++;
    if (str1[i] > str2[i])
        return -1;

    return (str1[i] < str2[i]);
}

// Main function to find string location
int searchStr(string arr[], string str, int first,
                                        int last)
{
    if (first > last)
        return -1;

    // Move mid to the middle
    int mid = (last+first)/2;

    // If mid is empty , find closest non-empty string
    if (arr[mid].empty())
    {
        // If mid is empty, search in both sides of mid
        // and find the closest non-empty string, and
        // set mid accordingly.
        int left  = mid - 1;
        int right = mid + 1;
        while (true)
        {
            if (left < first && right > last)
                return -1;
            if (right<=last && !arr[right].empty())
            {
                mid = right;
                break;
            }
            if (left>=first && !arr[left].empty())
            {
                mid = left;
                break;
            }
            right++;
            left--;
        }
    }

    // If str is found at mid
    if (compareStrings(str, arr[mid]) == 0)
        return mid;

    // If str is greater than mid
    if (compareStrings(str, arr[mid]) < 0)
        return searchStr(arr, str, mid+1, last);

    // If str is smaller than mid
    return searchStr(arr, str, first, mid-1);
}

// Driver Code
int main()
{
    // Input arr of Strings.
    string arr[] = {"for", "", "", "", "geeks", "ide", "",
                     "practice", "" , "", "quiz", "", ""};

    // input Search String
    string str = "quiz";
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << searchStr(arr, str, 0, n-1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find location of a str in
// an array of strings which is sorted and
// has empty strings between strings.
import java.util.*;

class GFG
{

    // Compare two string equals are not
    static int compareStrings(String str1,
                              String str2)
    {
        int i = 0;
        while (i < str1.length() - 1 &&
                   str1.charAt(i) == str2.charAt(i))
            i++;

        if (str1.charAt(i) > str2.charAt(i))
            return -1;

        if (str1.charAt(i) < str2.charAt(i))
            return 1;
        else
            return 0;
    }

    // Main function to find string location
    static int searchStr(String[] arr, String str,
                            int first, int last)
    {
        if (first > last)
            return -1;

        // Move mid to the middle
        int mid = (last + first) / 2;

        // If mid is empty,
        // find closest non-empty string
        if (arr[mid].isEmpty())
        {

            // If mid is empty, search in both sides of mid
            // and find the closest non-empty string, and
            // set mid accordingly.
            int left = mid - 1;
            int right = mid + 1;
            while (true)
            {
                if (left < right && right > last)
                    return -1;
                if (right <= last && !arr[right].isEmpty())
                {
                    mid = right;
                    break;
                }
                if (left >= right && !arr[left].isEmpty())
                {
                    mid = left;
                    break;
                }
                right++;
                left--;
            }
        }

        // If str is found at mid
        if (compareStrings(str, arr[mid]) == 0)
            return mid;

        // If str is greater than mid
        if (compareStrings(str, arr[mid]) < 0)
            return searchStr(arr, str, mid + 1, last);

        // If str is smaller than mid
        return searchStr(arr, str, first, mid - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input arr of Strings.
        String[] arr = { "for", "", "", "", "geeks",
                         "ide", "", "practice", "",
                         "", "quiz", "", "" };

        // input Search String
        String str = "quiz";
        int n = arr.length;

        System.out.println(searchStr(arr, str, 0, n - 1));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find the location of
# an str in an array of strings which is sorted
# and has empty strings between strings.

# Compare two string equals are not
def compareStrings(str1, str2):

    i = 0
    while i < len(str1) - 1 and str1[i] == str2[i]:
        i += 1
    if str1[i] > str2[i]:
        return -1

    return str1[i] < str2[i]

# Main function to find string location
def searchStr(arr, string, first, last):

    if first > last:
        return -1

    # Move mid to the middle
    mid = (last + first) // 2

    # If mid is empty , find closest non-empty string
    if len(arr[mid]) == 0:

        # If mid is empty, search in both sides of mid
        # and find the closest non-empty string, and
        # set mid accordingly.
        left, right = mid - 1, mid + 1
        while True:

            if left < first and right > last:
                return -1

            if right <= last and len(arr[right]) != 0:
                mid = right
                break

            if left >= first and len(arr[left]) != 0:
                mid = left
                break

            right += 1
            left -= 1

    # If str is found at mid
    if compareStrings(string, arr[mid]) == 0:
        return mid

    # If str is greater than mid
    if compareStrings(string, arr[mid]) < 0:
        return searchStr(arr, string, mid+1, last)

    # If str is smaller than mid
    return searchStr(arr, string, first, mid-1)

# Driver Code
if __name__ == "__main__":

    # Input arr of Strings.
    arr = ["for", "", "", "", "geeks", "ide", "",
                    "practice", "" , "", "quiz", "", ""]

    # input Search String
    string = "quiz"
    n = len(arr)

    print(searchStr(arr, string, 0, n-1))

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>
    // Javascript program to find location of a str in
    // an array of strings which is sorted and
    // has empty strings between strings.

    // Compare two string equals are not
    function compareStrings(str1, str2)
    {
        let i = 0;
        while (i < str1.length - 1 &&
                   str1[i] == str2[i])
            i++;

        if (str1[i] > str2[i])
            return -1;

        if (str1[i] < str2[i])
            return 1;
        else
            return 0;
    }

    // Main function to find string location
    function searchStr(arr, str, first, last)
    {
        if (first > last)
            return -1;

        // Move mid to the middle
        let mid = parseInt((last + first) / 2, 10);

        // If mid is empty,
        // find closest non-empty string
        if (arr[mid] == "")
        {

            // If mid is empty, search in both sides of mid
            // and find the closest non-empty string, and
            // set mid accordingly.
            let left = mid - 1;
            let right = mid + 1;
            while (true)
            {
                if (left < right && right > last)
                    return -1;
                if (right <= last && arr[right] != "")
                {
                    mid = right;
                    break;
                }
                if (left >= right && !arr[left] == "")
                {
                    mid = left;
                    break;
                }
                right++;
                left--;
            }
        }

        // If str is found at mid
        if (compareStrings(str, arr[mid]) == 0)
            return mid;

        // If str is greater than mid
        if (compareStrings(str, arr[mid]) < 0)
            return searchStr(arr, str, mid + 1, last);

        // If str is smaller than mid
        return searchStr(arr, str, first, mid - 1);
    }

    // Input arr of Strings.
    let arr = [ "for", "", "", "", "geeks",
                    "ide", "", "practice", "",
                    "", "quiz", "", "" ];

    // input Search String
    let str = "quiz";
    let n = arr.length;

    document.write(searchStr(arr, str, 0, n - 1));

// This code is contributed by vaibhavrabadiya3.
</script>
```

**输出:**

```
  10
```

使用线性搜索会得到 O(L*N)，其中 L 是字符串比较。为了优化运行时间，我们使用二分搜索法使时间复杂度为 0(1(LogN))。

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。