# 通过交换相邻的偶数对和奇数对获得的最小数量

> 原文:[https://www . geeksforgeeks . org/通过交换相邻奇偶对获得最小可能数/](https://www.geeksforgeeks.org/smallest-number-possible-by-swapping-adjacent-even-odd-pairs/)

给定一个数字字符串 **str** ，任务是找到可以通过交换不同奇偶校验的相邻数字形成的最小整数。

**示例:**

> **输入:** 836360
> **输出:** 338660
> **解释:**
> 第一次交换: **83** 6360 - > 386360
> 第二次交换:38**63**60->383660
> 第三次交换:3 **83** 660 -
> 
> **输入:**1003
> T3】输出: 13

**方法:**
我们可以观察到，在重复的互换中，我们可以将 **str** 的[偶数和奇数位](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)分成两个独立的区块。它们各自块中的数字顺序将与它们在字符串中的出现顺序相同，因为不允许在块内进行交换(*相同奇偶校验*)。因此，在将 **str** 分成两个独立的块之后，我们需要遍历这两个块，并将当前指向的两个值中的最小值附加到答案中。此操作后生成的最后一个字符串，如果有前导 0，则删除前导 0，是必需的答案。

**例:**
836360 中出现顺序中的偶数和奇数块分别为{8，6，6，0}和{3，3}。
因此形成的最小数量 **ans** 如下:

1.  年=年+分(8.3)= >年= 3
2.  年=年+分(8.3)= >年= 33
3.  因为所有的奇数都用完了，剩下的偶数需要一个一个地加。
4.  因此，要求的答案是 338660

下面是上述方法的实现:

## C++

```
// C++ Program to find the
// smallest number possible
// by swapping adjacent digits
// of different parity

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// smallest number possible
string findAns(string s)
{
    int digit;

    // Arrays to store odd and
    // even digits in the order
    // of their appearance in
    // the given string
    vector<int> odd;
    vector<int> even;

    // Insert the odd and
    // even digits
    for (auto c : s) {
        digit = c - '0';
        if (digit & 1)
            odd.push_back(digit);
        else
            even.push_back(digit);
    }

    // pointer to odd digit
    int i = 0;
    // pointer to even digit
    int j = 0;

    string ans = "";

    while (i < odd.size()
           and j < even.size()) {

        if (odd[i] < even[j])
            ans += (char)(odd[i++] + '0');
        else
            ans += (char)(even[j++] + '0');
    }

    // In case number of even and
    // odd digits are not equal

    // If odd digits are remaining
    while (i < odd.size())
        ans += (char)(odd[i++] + '0');

    // If even digits are remaining
    while (j < even.size())
        ans += (char)(even[j++] + '0');

    // Removal of leading 0's
    while (ans[0] == '0') {
        ans.erase(ans.begin());
    }

    return ans;
}
int main()
{

    string s = "894687536";
    cout << findAns(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest 
// number possible by swapping adjacent 
// digits of different parity
import java.util.*;

class GFG{

// Function to return the
// smallest number possible
static String findAns(String s)
{
    int digit;

    // Arrays to store odd and even 
    // digits in the order their 
    // appearance in the given String
    Vector<Integer> odd =new Vector<Integer>();
    Vector<Integer> even = new Vector<Integer>();

    // Insert the odd and
    // even digits
    for(char c : s.toCharArray())
    {
       digit = c - '0';
       if (digit % 2 == 1)
           odd.add(digit);
       else
           even.add(digit);
    }

    // Pointer to odd digit
    int i = 0;

    // Pointer to even digit
    int j = 0;

    String ans = "";

    while (i < odd.size() && j < even.size())
    {
        if (odd.get(i) < even.get(j))
            ans += (char)(odd.get(i++) + '0');
        else
            ans += (char)(even.get(j++) + '0');
    }

    // In case number of even and
    // odd digits are not equal
    // If odd digits are remaining
    while (i < odd.size())
        ans += (char)(odd.get(i++) + '0');

    // If even digits are remaining
    while (j < even.size())
        ans += (char)(even.get(j++) + '0');

    // Removal of leading 0's
    while (ans.charAt(0) == '0')
    {
        ans = ans.substring(1);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "894687536";

    System.out.print(findAns(s));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to find the 
# smallest number possible 
# by swapping adjacent digits 
# of different parity 

# Function to return the 
# smallest number possible 
def findAns(s):

    # Arrays to store odd and 
    # even digits in the order 
    # of their appearance in 
    # the given string 
    odd = []
    even = [] 

    # Insert the odd and 
    # even digits 

    for c in s:
        digit = int(c)
        if (digit & 1):
            odd.append(digit)
        else:
            even.append(digit)

    # pointer to odd digit 
    i = 0

    # pointer to even digit 
    j = 0

    ans = ""

    while (i < len(odd) and j < len(even)):

        if (odd[i] < even[j]):
            ans += str(odd[i])
            i = i + 1
        else:
            ans += str(even[j])
            j = j + 1

    # In case number of even and 
    # odd digits are not equal 

    # If odd digits are remaining 
    while (i < len(odd)):
        ans += str(odd[i])
        i = i + 1

    # If even digits are remaining 
    while (j < len(even)):
        ans += str(even[j])
        j = j + 1

    # Removal of leading 0's 
    while (ans[0] == '0'):
        ans = ans[1:]

    return ans

# Driver Code
s = "894687536"
print(findAns(s))

# This code is contributed by yatin
```

## C#

```
// C# program to find the smallest 
// number possible by swapping adjacent 
// digits of different parity
using System;
using System.Collections.Generic;

class GFG{

// Function to return the
// smallest number possible
static String findAns(String s)
{
    int digit;

    // Arrays to store odd and even 
    // digits in the order their 
    // appearance in the given String
    List<int> odd = new List<int>();
    List<int> even = new List<int>();

    // Insert the odd and
    // even digits
    foreach(char c in s.ToCharArray())
    {
        digit = c - '0';
        if (digit % 2 == 1)
            odd.Add(digit);
        else
            even.Add(digit);
    }

    // Pointer to odd digit
    int i = 0;

    // Pointer to even digit
    int j = 0;

    String ans = "";

    while (i < odd.Count && j < even.Count)
    {
        if (odd[i] < even[j])
            ans += (char)(odd[i++] + '0');
        else
            ans += (char)(even[j++] + '0');
    }

    // In case number of even and
    // odd digits are not equal
    // If odd digits are remaining
    while (i < odd.Count)
        ans += (char)(odd[i++] + '0');

    // If even digits are remaining
    while (j < even.Count)
        ans += (char)(even[j++] + '0');

    // Removal of leading 0's
    while (ans[0] == '0')
    {
        ans = ans.Substring(1);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s = "894687536";

    Console.Write(findAns(s));
}
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
846869753

```

**时间复杂度:** *O(N)* ，其中 N 是给定字符串的大小。