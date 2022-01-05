# 在给定字符串的特定位置添加空格后生成字符串

> 原文:[https://www . geesforgeks . org/给定字符串中特定位置添加空格后生成字符串/](https://www.geeksforgeeks.org/generate-string-after-adding-spaces-at-specific-positions-in-a-given-string/)

给定一个字符串 **s** 和一个数组 **spaces[]** ，描述原始字符串的索引，其中将添加空格。任务是在**空格[]** 的给定位置添加空格，并打印形成的字符串。

**示例:**

> **输入:** s = "GeeksForGeeK "，空格= {1，5，10}
> **输出:**【G eeks ForGe eK】
> **解释:**G**<u>e</u>**eks**<u>F</u>**orGe**<u>e</u>**K 中带下划线的字符与指数 1、5 和 10 相关。之后，在这些字符前面加上空格。
> 
> **输入:**s = " ilovegeekforgek "，空格= {1，5，10，13}
> **输出:**“我爱极客换极客”

**方法:**这个问题是基于简单字符串实现的。按照以下步骤解决给定的问题。按照以下步骤解决给定的问题。

*   用两个数组长度之和**大小的新字符串中的一个**空格**初始化。**
*   访问索引，只要索引等于**空间[]** 数组中的当前空间值，就跳过它，因为空间已经存在。
*   否则继续从主字符串赋值
*   这里在第{ **if(l < N 和 i==sp[l]+l)** 行添加 **'l'** 是非常有趣的观察:
    *   空间数组中的值基本上是根据旧的输入字符串。
    *   但是在新的字符串中，这些空间值或索引基本上是按照之前找到的空间数量移动的。
*   打印最后形成的字符串。

下面是上述方法的实现

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to add space in required positions
string spaceintegration(string s, vector<int>& sp)
{
    int M = s.size(), N = sp.size(), l = 0, r = 0;

    string res(M + N, ' ');

    // Iterate over M+N length
    for (int i = 0; i < M + N; i++) {

        if (l < N and i == sp[l] + l)
            l++;
        else
            res[i] = s[r++];
    }

    // Return the requried string
    return res;
}

// Driver Code
int main()
{

    string s = "ilovegeeksforgeeks";

    vector<int> space = { 1, 5, 10, 13 };

    // Function Call
    cout << spaceintegration(s, space) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
class GFG
{

  // Function to add space in required positions
  static String spaceintegration(String s, int []sp)
  {
    int M = s.length(), N = sp.length, l = 0, r = 0;
    String res = newstr(M + N, ' ');

    // Iterate over M+N length
    for (int i = 0; i < M + N; i++) {

      if (l < N && i == sp[l] + l)
        l++;
      else
        res = res.substring(0,i)+s.charAt(r++)+res.substring(i+1);
    }

    // Return the requried String
    return res;
  }

  static String newstr(int i, char c) {
    String str = "";
    for (int j = 0; j < i; j++) {
      str+=c;       
    }
    return str;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String s = "ilovegeeksforgeeks";
    int[] space = { 1, 5, 10, 13 };

    // Function Call
    System.out.print(spaceintegration(s, space) +"\n");

  }
}

// This code contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to add space in required positions
def spaceintegration(s, sp):

    M = len(s)
    N = len(sp)
    l = 0
    r = 0

    res = [' '] * (M + N)

    # Iterate over M+N length
    for i in range(M + N):
        if (l < N and i == sp[l] + l):
            l += 1
        else:
            res[i] = s[r]
            r += 1

    # Return the requried string
    return ''.join(res)

# Driver Code
if __name__ == "__main__":

    s = "ilovegeeksforgeeks"

    space = [ 1, 5, 10, 13 ]

    # Function Call
    print(spaceintegration(s, space))

# This code is contributed by ukasp
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to add space in required positions
      function spaceintegration(s, sp)
      {
          let M = s.length, N = sp.length, l = 0, r = 0;
          let res = new Array(M + N).fill(' ');

          // Iterate over M+N length
          for (let i = 0; i < M + N; i++) {

              if (l < N && i == sp[l] + l)
                  l++;
              else
                  res[i] = s[r++];
          }

          // Return the requried string
          return res.join('');
      }

      // Driver Code
      let s = "ilovegeeksforgeeks";
      let space = [1, 5, 10, 13];

      // Function Call
      document.write(spaceintegration(s, space) + '<br>');

// This code is contributed by Potta Lokesh
  </script>
```

**Output:** 

```
i love geeks for geeks
```

**时间复杂度:**O(M+N)
T3】辅助空间: O(M+N)