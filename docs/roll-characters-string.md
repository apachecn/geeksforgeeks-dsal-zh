# 滚动字符串的字符

> 原文:[https://www.geeksforgeeks.org/roll-characters-string/](https://www.geeksforgeeks.org/roll-characters-string/)

给定一个字符串 s 和一个数组 roll，其中 roll[i]表示字符串中滚动的第一个 roll[i]字符。我们需要在弦上应用每一个滚动[i]并输出最终的弦。滚动意味着增加字符的 ASCII 值，如滚动“z”会得到“a”，滚动“b”会得到“c”等。

约束:
1<= | s |<= 10^5
1<=罗尔【I】<= 10^5

示例:

```
Input : s = "bca"
        roll[] = {1, 2, 3}         
Output : eeb

Explanation :
arr[0] = 1 means roll first character of string -> cca
arr[1] = 2 means roll first two characters of string -> dda
arr[2] = 3 means roll first three characters of string -> eeb
So final ans is "eeb"

Input : s = "zcza"
        roll[] = {1, 1, 3, 4}
Output : debb

```

**问题来源:** [Airtel 采访体验|第一集(FTE 校内)](https://www.geeksforgeeks.org/airtel-interview-experience-set-1-fte-campus/)

**简单方法:**继续为每一卷改变字符串的字符【I】
时间复杂度= 0(卷数组的大小*字符串的长度)= 0(n<sup>2</sup>

**高效方法:**更好的方法是创建一个数组并存储要对其中每个字符执行的总滚动操作，然后遍历字符串并执行滚动操作。

该方法的代码:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to roll the string
import java.util.stream.IntStream;

class StringRoller {

    public static String roll(String toRoll, int roll[]) {

        int toRollLength = toRoll.length();
        int each_character_roll[] = new int[toRollLength];
        char[] toRollCharArr = toRoll.toCharArray();

        for (int i = 0; i < roll.length; ++i) {
            ++each_character_roll[0];
            int noOfRoll = roll[i];
            if (noOfRoll >= each_character_roll.length)
                continue;
            else
                --each_character_roll[noOfRoll];
        }

        IntStream.range(1, toRollLength).forEach(index -> {
            each_character_roll[index] = each_character_roll[index] + each_character_roll[index - 1];
        });

        IntStream.range(0, toRollLength).forEach(index -> {
            toRollCharArr[index] = roll_character(toRollCharArr[index], each_character_roll[index]);
        });

        return String.valueOf(toRollCharArr);

    }

    public static char roll_character(char c, int roll) {
        roll = roll % 26;
        int character = c - 'a';

        return (char) ('a' + (character + roll) % 26);
    }

    // Driver code
    public static void main(String[] args) {
        String s = "geeks";
        int k[] = {1, 2, 5};
        System.out.println(roll(s, k));
    }
}
// Code is contributed by Snehashish.
```

**Output:**

```
jgflt
```

**时间复杂度:**O(n+m)
T3】空间复杂度: O(n)

本文由 **[曼德普·辛格](https://github.com/msdeep14)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。