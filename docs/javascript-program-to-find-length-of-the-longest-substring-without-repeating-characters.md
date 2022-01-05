# 不重复字符寻找最长子串长度的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-to-find-长度最长的无重复字符子串/](https://www.geeksforgeeks.org/javascript-program-to-find-length-of-the-longest-substring-without-repeating-characters/)

给定一个字符串 **str** ，求最长子串的长度，不重复字符。

*   对于“ABDEFGABEF”，最长的子串是“BDEFGA”和“DEFGAB”，长度为 6。
*   对于“BBBB”，最长的子串是“B”，长度为 1。
*   对于“GEEKSFORGEEKS”，下图中显示了两个最长的子字符串，长度为 7

![](img/a1ffd4fb24aa41edf65c169443d770a5.png) ![](img/717cbaa4f75840cdd674a28b6ff0986b.png) ![](img/1a0da2e0ec22126e85a959b3a8469428.png)

期望的时间复杂度是 O(n)，其中 n 是字符串的长度。

**方法 1(简单:O(n<sup>3</sup>)**:我们可以逐个考虑所有子串，检查每个子串是否包含所有唯一字符。将有 n*(n+1)/2 个子字符串。一个子串是否包含所有唯一的字符，可以通过从左到右扫描并保存一个被访问字符的映射来在线性时间内检查。这个解决方案的时间复杂度是 O(n^3).

## java 描述语言

```
<script>

// JavaScript program to find the length of the
// longest substring without repeating
// characters
// This function returns true if all characters in
// str[i..j] are distinct, otherwise returns false
function areDistinct(str, i, j)
{

    // Note : Default values in visited are false
    var visited = new [26];

    for(var k = i; k <= j; k++)
    {
        if (visited[str.charAt(k) - 'a'] == true)
            return false;

        visited[str.charAt(k) - 'a'] = true;
    }
    return true;
}

// Returns length of the longest substring
// with all distinct characters.
function longestUniqueSubsttr(str)
{
    var n = str.length();

    // Result
    var res = 0; 

    for(var i = 0; i < n; i++)
        for(var j = i; j < n; j++)
            if (areDistinct(str, i, j))
                res = Math.max(res, j - i + 1);

    return res;
}

// Driver code
    var str = "geeksforgeeks";
    document.write("The input string is " + str);

    var len = longestUniqueSubsttr(str);

    document.write("The length of the longest " +
                       "non-repeating character " + 
                       "substring is " + len);

// This code is contributed by shivanisinghss2110.

</script>
```

**Output**

```
The input string is geeksforgeeks
The length of the longest non-repeating character substring is 7
```

**方法二(更好:O(n<sup>2</sup>)**思路是用[滑窗](https://www.geeksforgeeks.org/window-sliding-technique/)。每当我们看到重复时，我们就移除先前的事件并滑动窗口。

## java 描述语言

```
<script>

// JavaScript program to find the length of the 
// longest substring without repeating
// characters

function longestUniqueSubsttr(str)
{
    var n = str.length();

    // Result
    var res = 0;

    for(var i = 0; i < n; i++)
    {

        // Note : Default values in visited are false
        var visited = new [256];

        for(var j = i; j < n; j++)
        {

            // If current character is visited
            // Break the loop
            if (visited[str.charAt(j)] == true)
                break;

            // Else update the result if
            // this window is larger, and mark
            // current character as visited.
            else
            {
                res = Math.max(res, j - i + 1);
                visited[str.charAt(j)] = true;
            }
        }

        // Remove the first character of previous
        // window
        visited[str.charAt(i)] = false;
    }
    return res;
}

// Driver code
    var str = "geeksforgeeks";
    document.write("The input string is " + str);

    var len = longestUniqueSubsttr(str);
    document.write("The length of the longest " +
                       "non-repeating character " +
                       "substring is " + len);

// This code is contributed by shivanisinghss2110     
</script>
```

**Output**

```
The input string is geeksforgeeks
The length of the longest non-repeating character substring is 7
```

**方法 4(线性时间)**:现在来说说线性时间解。这个解决方案使用额外的空间来存储已经访问过的字符的最后索引。这个想法是从左到右扫描字符串，跟踪到目前为止在 **res** 中看到的最大长度的非重复字符子字符串。当我们遍历字符串时，为了知道当前窗口的长度，我们需要两个索引。
1)尾盘指数( **j** ):我们认为当前指数为尾盘指数。
2)起始索引( **i** ):如果当前字符不在前一窗口中，则与前一窗口相同。为了检查当前字符是否出现在前一个窗口中，我们将每个字符的最后一个索引存储在一个数组中 **lasIndex[]** 。如果 lastIndex[str[j]] + 1 比之前的开始多，那么我们更新开始索引 I，否则我们保持相同的 I。

下面是上述方法的实现:

## java 描述语言

```
<script>

// JavaScript program to find the length of the longest substring
// without repeating characters
var NO_OF_CHARS = 256;

function longestUniqueSubsttr(str)
    {
        var n = str.length();

        var res = 0; // result

        // last index of all characters is initialized
        // as -1
        var lastIndex = new [NO_OF_CHARS];
        Arrays.fill(lastIndex, -1);

        // Initialize start of current window
        var i = 0;

        // Move end of current window
        for (var j = 0; j < n; j++) {

            // Find the last index of str[j]
            // Update i (starting index of current window)
            // as maximum of current value of i and last
            // index plus 1
            i = Math.max(i, lastIndex[str.charAt(j)] + 1);

            // Update result if we get a larger window
            res = Math.max(res, j - i + 1);

            // Update last index of j.
            lastIndex[str.charAt(j)] = j;
        }
        return res;
    }

    /* Driver program to test above function */

        var str = "geeksforgeeks";
        document.write("The input string is " + str);
        var len = longestUniqueSubsttr(str);
        document.write("The length of the longest non repeating character is " + len);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
The input string is geeksforgeeks
The length of the longest non-repeating character substring is 7
```

**时间复杂度:** O(n + d)，其中 n 为输入字符串的长度，d 为输入字符串字母表中的字符数。例如，如果字符串由小写英文字符组成，那么 d 的值是 26。
T3【辅助空间: O(d)

详情请参考完整的[最长子串长度不重复字符](https://www.geeksforgeeks.org/length-of-the-longest-substring-without-repeating-characters/)一文！