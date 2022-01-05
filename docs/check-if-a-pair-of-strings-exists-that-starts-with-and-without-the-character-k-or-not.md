# 检查是否存在一对以字符 K 开头和不包含字符 K 的字符串

> 原文:[https://www . geeksforgeeks . org/check-if-a-twist-with-with-and-not-the-character-k-or-not/](https://www.geeksforgeeks.org/check-if-a-pair-of-strings-exists-that-starts-with-and-without-the-character-k-or-not/)

给定一个由小写字符的字符串 **N** 和字符 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，使得任何字符串都可以以字符 **K** 开始，任务是检查是否存在任何一对开始和不开始的字符串(！))带有字符 **K** 。如果发现**为真**，则打印“**是**”。否则，打印“**否**”。

**示例:**

> **输入:** arr[] = {"a "，"！a、b、a！c " " d " "啊！d"}，K = '！'
> **输出:**是
> **解释:**
> 存在有效的字符串对是{(“a”、“！一”)，("！d "，" d")}。
> 
> **输入:** arr[] = {“红”“红”“红”、“！橙色”、“黄色”、“黄色！蓝色" "青色"、"！绿色" "棕色"！灰色" }，K = '！'
> T3】输出:否

**天真方法:**解决给定问题最简单的方法是[从数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中找到所有可能的对，并检查[字符串](https://www.geeksforgeeks.org/python-strings/)对是否满足给定条件。

***时间复杂度:** O(N <sup>2</sup> *M)，其中 M 是给定数组 **arr[]** 中字符串* *的最大* [*长度。*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)

**高效途径:**以上途径也可以使用[词典](https://www.geeksforgeeks.org/python-dictionary/)解决。按照以下步骤解决问题:

*   初始化一个[字典](https://www.geeksforgeeks.org/python-dictionary/)，比如说**访问了**来存储之前访问过的字符串。
*   遍历列表**arr【】**，在每次迭代中，如果当前字符串的起始字符是字符 **K** ，则在**访问的**中检查不带字符 **K** 的字符串，否则在**访问的**中检查带字符 **K** 的字符串。如果找到[串](https://www.geeksforgeeks.org/python-strings/)，则返回“**是**”。
*   在每次迭代中，将字符串 **S** 添加到地图**访问的**中。
*   完成上述步骤后，如果不满足上述条件，则打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a pair of
// strings exists satisfying the conditions
string checkhappy(vector<string> arr, char K, int N)
{

    // Stores the visited strings
    set<string> visited;

    // Iterate over the array arr[]
    for (string s : arr) {

        // If first character of current
           // string is K
        if(s[0] == K)
            if (visited.find(s.substr(1)) != visited.end())
                return "Yes";

        // Otherwise
        else
            if (visited.find((K + s)) != visited.end())
                return "Yes";

        // Adding to the visited
        visited.insert(s);
      }

    return "No";
}

// Driver Code
int main() {

    // Given Input
    vector<string> arr = {"a", "! a", "b", "! c", "d", "! d"};
    char K = '!';
    int N = arr.size();

    cout << checkhappy(arr, K, N) << endl;

    return 0;
}

// This code is contributed Dharanendra L V.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check whether a pair of
# strings exists satisfying the conditions
def checkhappy(arr, K, N):

    # Stores the visited strings
    visited = set()

    # Iterate over the array arr[]
    for s in arr:

        # If first character of current
        # string is K
        if(s[0] == K):
            if s[1:] in visited:
                return 'Yes'

        # Otherwise
        else:
            if (K + s) in visited:
                return 'Yes'

        # Adding to the visited
        visited.add(s)

    return "No"

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = ['a', '! a', 'b', '! c', 'd', '! d']
    K = '!'
    N = len(arr)

    print(checkhappy(arr, K, N))
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check whether a pair of
// strings exists satisfying the conditions
function checkhappy(arr, K, N)
{

    // Stores the visited strings
    let visited = new Set();

    // Iterate over the array arr[]
    for(let s of arr)
    {

        // If first character of current
        // string is K
        if (s[0] == K)
        {
            if (visited.has(s.slice(1)))
                return "Yes";
        }

        // Otherwise
        else
        {
            if (visited.has(K + s))
                return "Yes";
        }

        // Adding to the visited
        visited.add(s);
    }
    return "No";
}

// Driver Code

// Given Input
let arr = [ "a", "! a", "b", "! c",
            "d", "! d" ];
let K = "!";
let N = arr.length;

document.write(checkhappy(arr, K, N));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
No
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)