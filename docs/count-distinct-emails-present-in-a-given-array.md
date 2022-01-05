# 统计给定数组中存在的不同电子邮件

> 原文:[https://www . geesforgeks . org/count-distinct-emails-present-in-a-给定阵列/](https://www.geeksforgeeks.org/count-distinct-emails-present-in-a-given-array/)

给定一个由**N**T6】字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中每个字符串代表一个由英文字母组成的电子邮件地址，**'，'+'** 和 **'@'** ，任务是根据以下规则计算数组中不同电子邮件的数量:

*   一个电子邮件地址可以拆分为两个子字符串，**“@”**的前缀和后缀，分别是本地名称和域名。
*   “**”**本地名称中字符串中的字符被忽略。
*   在本地名称中，忽略“ **+** ”后的每个字符。

**示例:**

> **输入:**arr[]= {“raghav . agg @ geeksforgeeks . com”“raghavag @ geeksforgeeks . com”}
> **输出:** 1
> **解释:**移除所有“.”“@”前的 s 将字符串修改为{“raghavagg @ geeksforgeeks . com”、“raghavagg @ geeksforgeeks . com”}。因此，字符串中出现的不同电子邮件总数为 1。
> 
> **输入:**arr[]= {【AVR uty+dhir+gfg @ geeksforgeeks . com】，“avruty+gfg@geeksforgeeks.com”，“av . ruty @ geeksforgeeks . com”}
> **输出:** 1

**方法:**给定的问题可以通过将每个电子邮件按照给定的规则填充后存储在 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 中并打印获得的 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 的大小来解决。按照以下步骤解决问题:

*   初始化一个 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) ，比如说 **S** ，根据给定的规则填充后存储所有不同的字符串。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   找到 **'@'** 的位置并存储在变量中，比如 **pos2** 。
    *   删除所有的**。”**前**字符 pos2** 使用[擦除()](https://www.geeksforgeeks.org/stdstringerase-in-cpp/)功能。
    *   更新 **'@'** 的位置，即 **pos2 = find('@')** 并找到 **'+'** 的位置并将其存储在变量 say **pos1** 中作为 **S.find('+')** 。
    *   现在，擦除 **pos1** 之后和 **pos2** 之前的所有字符。
    *   将所有更新的字符串插入到一个**哈希集中**T2 中。
*   完成以上步骤后，打印**大小的 HashSet** **S** 作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count all the distinct
// emails after preprocessing according
// to the given rules
int distinctEmails(vector<string>& emails)
{
    // Traverse the given array of
    // strings arr[]
    for (auto& x : emails) {

        // Stores the position of '@'
        // in the string
        auto pos2 = x.find('@');

        // If pos2 < x.size()
        if (pos2 < x.size())

            // Erases all the occurrences
            // of '.' before pos2
            x.erase(
                remove(x.begin(),
                    x.begin() + pos2, '.'),
                x.begin() + pos2);

        // Stores the position of the
        // first '+'
        auto pos1 = x.find('+');

        // Update the position pos2
        pos2 = x.find('@');

        // If '+' exists then erase
        // characters after '+' and
        // before '@'
        if (pos1 < x.size()
            and pos2 < x.size()) {
            x.erase(pos1, pos2 - pos1);
        }
    }

    // Insert all the updated strings
    // inside the set
    unordered_set<string> ans(
        emails.begin(),
        emails.end());

    // Return the size of set ans
    return ans.size();
}

// Driver Code
int main()
{
    vector<string> arr
        = { "raghav.agg@geeksforgeeks.com",
            "raghavagg@geeksforgeeks.com" };

    // Function Call
    cout << distinctEmails(arr);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count all the distinct
# emails after preprocessing according
# to the given rules
def distinctEmails(emails):

  ans = set([])

  # Traverse the given array of
  # strings arr[]
  for x in emails:

    # Stores the position of '@'
    # in the string
    pos2 = x.find('@')

    # If pos2 < x.size()
    if (pos2 < len(x)):

      # Erases all the occurrences
      # of '.' before pos2
      p = x[:pos2]
      p = p.replace(".", "")
      x = p + x[pos2:]

      # Stores the position of the
      # first '+'
      pos1 = x.find('+')

      # Update the position pos2
      pos2 = x.find('@')

      # If '+' exists then erase
      # characters after '+' and
      # before '@'
      if (pos1 > 0 and pos1 < len(x) and
          pos2 < len(x)):
        x = x[:pos1] + x[pos2:]

      # Insert all the updated strings
      # inside the set
      ans.add(x)

  # Return the size of set ans
  return len(ans)

# Driver Code
if __name__ == "__main__":

    arr = ["raghav.agg@geeksforgeeks.com",
           "raghavagg@geeksforgeeks.com"]

    # Function Call
    print(distinctEmails(arr))

# This code is contributed by ukasp
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*