# 生成所有二进制排列，使得在所有排列的每个点之前都有多于或等于 0 的 1

> 原文:[https://www . geesforgeks . org/generate-binary-排列-1s-0s-每点-排列/](https://www.geeksforgeeks.org/generate-binary-permutations-1s-0s-every-point-permutations/)

生成给定长度的所有置换，使得每个置换在置换的所有前缀中具有大于或等于 0 的 1。

**示例:**

```
Input: len = 4
Output: 1111 1110 1101 1100 1011 1010
Note that a permutation like 0101 can not be in output because
there are more 0's from index 0 to 2 in this permutation.

Input: len = 3
Output: 111 110 101

Input: len = 2
Output: 11 10 
```

像排列生成问题一样，递归是解决这个问题最简单的方法。我们从一个空字符串开始，在它上面附加 1 并重复。循环时，如果我们在任一点上发现更多的 1，我们就追加一个 0，再进行一次递归调用。
下面是实现:

## C++

```
// C++ program to generate all permutations of 1's and 0's such that
// every permutation has more 1's than 0's at all indexes.
#include <iostream>
#include <cstring>
using namespace std;

// ones & zeroes --> counts of 1's and 0's in current string 'str'
// len ---> desired length of every permutation
void generate(int ones, int zeroes, string str, int len)
{
    // If length of current string becomes same as desired length
    if (len == str.length())
    {
        cout << str << "  ";
        return;
    }

    // Append a 1 and recur
    generate(ones+1, zeroes, str+"1", len);

    // If there are more 1's, append a 0 as well, and recur
    if (ones > zeroes)
        generate(ones, zeroes+1, str+"0", len);
}

// Driver program to test above function
int main()
{
    string str = "";
    generate(0, 0, str, 4);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate all permutations of 1's and 0's such that
// every permutation has more 1's than 0's at all indexes.

class GFG {

// ones & zeroes --> counts of 1's and 0's in current string 'str'
// len ---> desired length of every permutation
    static void generate(int ones, int zeroes, String str, int len) {
        // If length of current string becomes same as desired length
        if (len == str.length()) {
            System.out.print(str + " ");
            return;
        }

        // Append a 1 and recur
        generate(ones + 1, zeroes, str + "1", len);

        // If there are more 1's, append a 0 as well, and recur
        if (ones > zeroes) {
            generate(ones, zeroes + 1, str + "0", len);
        }
    }

// Driver program to test above function
    public static void main(String[] args) {
        String str = "";
        generate(0, 0, str, 4);
    }
}

/* This Java code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python 3 program to generate all permutations of 1's and 0's such that
# every permutation has more 1's than 0's at all indexes.

# ones & zeroes --> counts of 1's and 0's in current string 'str'
# len ---> desired length of every permutation
def generate(ones, zeroes, str, len1):
    # If length of current string becomes same as desired length
    if (len1 == len(str)):
        print(str,end =" ")
        return

    # Append a 1 and recur
    generate(ones+1, zeroes, str+"1", len1)

    # If there are more 1's, append a 0 as well, and recur
    if (ones > zeroes):
        generate(ones, zeroes+1, str+"0", len1)

# Driver program to test above function
if __name__ == '__main__':
    str = ""
    generate(0, 0, str, 4)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to generate all permutations of 1's and 0's such that
// every permutation has more 1's than 0's at all indexes.

using System;

public class GFG {

// ones & zeroes --> counts of 1's and 0's in current string 'str'
// len ---> desired length of every permutation
    static void generate(int ones, int zeroes, String str, int len) {
        // If length of current string becomes same as desired length
        if (len == str.Length) {
            Console.Write(str + " ");
            return;
        }

        // Append a 1 and recur
        generate(ones + 1, zeroes, str + "1", len);

        // If there are more 1's, append a 0 as well, and recur
        if (ones > zeroes) {
            generate(ones, zeroes + 1, str + "0", len);
        }
    }

// Driver program to test above function
    public static void Main() {
        String str = "";
        generate(0, 0, str, 4);
    }
}

/* This Java code is contributed by 29AjayKumar*/
```

## java 描述语言

```
<script>
      // JavaScript program to generate all permutations of 1's and 0's such that
      // every permutation has more 1's than 0's at all indexes.

      // ones & zeroes --> counts of 1's and 0's in current string 'str'
      // len ---> desired length of every permutation
      function generate(ones, zeroes, str, len) {
          // If length of current string becomes same as desired length
        if (len === str.length) {
            document.write(str + " ");
              return;
        }

        // Append a 1 and recur
        generate(ones + 1, zeroes, str + "1", len);

        // If there are more 1's, append a 0 as well, and recur
        if (ones > zeroes) {
              generate(ones, zeroes + 1, str + "0", len);
        }
      }

      // Driver program to test above function
      var str = "";
      generate(0, 0, str, 4);
</script>
```

**输出:**

```
1111  1110  1101  1100  1011  1010
```

本文由**沙钦**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。