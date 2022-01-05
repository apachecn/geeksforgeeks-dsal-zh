# 生成仅允许相邻互换的置换

> 原文:[https://www . geesforgeks . org/generate-排列-相邻-交换-允许/](https://www.geeksforgeeks.org/generate-permutations-adjacent-swaps-allowed/)

给定一个长度为 n 的字符串。您只能交换相邻的元素，并且每个元素可以在大气中交换一次。找出在执行上述交换后可以生成的字符串排列数。
**例:**

```
Input : 12345
Output : 12345 12354 12435 13245 13254 
         21345 21354 21435
```

来源:[高盛采访](https://www.geeksforgeeks.org/goldman-sachs-interview-experience-set-28-on-campus-for-full-time/)

考虑字符串中的第 I 个字符。这个角色有两种可能:
1。)不要交换，即不要对这个角色做任何事情，移动到下一个角色。
2。)交换一下。因为它可以与其相邻的、
……..a .)用下一个字符替换它。因为每个角色可以在大气中交换一次，所以我们将移动到位置(i+2)。
……。b .)用前一个字符替换它–我们不需要单独考虑这种情况，因为第 I 个字符是第(i-1)个字符的下一个字符，这与情况 2.a.
相同

## C++

```
// CPP program to generate permutations with only
// one swap allowed.
#include <cstring>
#include <iostream>
using namespace std;

void findPermutations(char str[], int index, int n)
{
    if (index >= n || (index + 1) >= n) {
        cout << str << endl;
        return;
    }

    // don't swap the current position
    findPermutations(str, index + 1, n);

    // Swap with the next character and
    // revert the changes. As explained
    // above, swapping with previous is
    // is not needed as it anyways happens
    // for next character.
    swap(str[index], str[index + 1]);
    findPermutations(str, index + 2, n);
    swap(str[index], str[index + 1]);
}

// Driver code
int main()
{
    char str[] = { "12345" };
    int n = strlen(str);
    findPermutations(str, 0, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate permutations with only
// one swap allowed.

class GFG {

    static void findPermutations(char str[], int index, int n) {
        if (index >= n || (index + 1) >= n) {
            System.out.println(str);
            return;
        }

        // don't swap the current position
        findPermutations(str, index + 1, n);

        // Swap with the next character and
        // revert the changes. As explained
        // above, swapping with previous is
        // is not needed as it anyways happens
        // for next character.
        swap(str, index);
        findPermutations(str, index + 2, n);
        swap(str, index);
    }

    static void swap(char arr[], int index) {
        char temp = arr[index];
        arr[index] = arr[index + 1];
        arr[index + 1] = temp;
    }
// Driver code

    public static void main(String[] args) {
        char str[] = "12345".toCharArray();
        int n = str.length;
        findPermutations(str, 0, n);
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to generate permutations
# with only one swap allowed.
def findPermutations(string, index, n):
    if index >= n or (index + 1) >= n:
        print(''.join(string))
        return

    # don't swap the current position
    findPermutations(string, index + 1, n)

    # Swap with the next character and
    # revert the changes. As explained
    # above, swapping with previous is
    # is not needed as it anyways happens
    # for next character.
    string[index], \
    string[index + 1] = string[index + 1], \
                        string[index]

    findPermutations(string, index + 2, n)

    string[index], \
    string[index + 1] = string[index + 1], \
                        string[index]

# Driver Code
if __name__ == "__main__":
    string = list("12345")
    n = len(string)
    findPermutations(string, 0, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to generate permutations with only
// one swap allowed.
using System;
public class GFG {

    static void findPermutations(char []str, int index, int n) {
        if (index >= n || (index + 1) >= n) {
            Console.WriteLine(str);
            return;
        }

        // don't swap the current position
        findPermutations(str, index + 1, n);

        // Swap with the next character and
        // revert the changes. As explained
        // above, swapping with previous is
        // is not needed as it anyways happens
        // for next character.
        swap(str, index);
        findPermutations(str, index + 2, n);
        swap(str, index);
    }

    static void swap(char []arr, int index) {
        char temp = arr[index];
        arr[index] = arr[index + 1];
        arr[index + 1] = temp;
    }
// Driver code

    public static void Main() {
        char []str = "12345".ToCharArray();
        int n = str.Length;
        findPermutations(str, 0, n);
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate permutations
// with only one swap allowed.

function findPermutations($str, $index, $n)
{
    if ($index >= $n || ($index + 1) >= $n)
    {
        echo $str, "\n";
        return;
    }

    // don't swap the current position
    findPermutations($str, $index + 1, $n);

    // Swap with the next character and
    // revert the changes. As explained
    // above, swapping with previous is
    // is not needed as it anyways happens
    // for next character.
    list($str[$index],
         $str[$index + 1]) = array($str[$index + 1],
                                   $str[$index]);

    findPermutations($str, $index + 2, $n);
    list($str[$index],
         $str[$index + 1]) = array($str[$index + 1],
                                   $str[$index]);
}

// Driver code
$str = "12345" ;
$n = strlen($str);
findPermutations($str, 0, $n);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

      // JavaScript program to generate
      // permutations with only
      // one swap allowed.
      function findPermutations(str, index, n) {
        if (index >= n || index + 1 >= n) {
          document.write(str.join("") + "<br>");
          return;
        }

        // don't swap the current position
        findPermutations(str, index + 1, n);

        // Swap with the next character and
        // revert the changes. As explained
        // above, swapping with previous is
        // is not needed as it anyways happens
        // for next character.
        swap(str, index);
        findPermutations(str, index + 2, n);
        swap(str, index);
      }

      function swap(arr, index) {
        var temp = arr[index];
        arr[index] = arr[index + 1];
        arr[index + 1] = temp;
      }
      // Driver code

      var str = "12345".split("");
      var n = str.length;
      findPermutations(str, 0, n);

</script>
```

**输出:**

```
12345
12354
12435
13245
13254
21345
21354
21435
```

本文由 [**ekta1994**](https://auth.geeksforgeeks.org/profile.php?user=ekta1994) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。