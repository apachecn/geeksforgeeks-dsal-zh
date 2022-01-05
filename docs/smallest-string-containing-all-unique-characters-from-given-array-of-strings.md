# 包含给定字符串数组中所有唯一字符的最小字符串

> 原文:[https://www . geesforgeks . org/包含给定字符串数组中所有唯一字符的最小字符串/](https://www.geeksforgeeks.org/smallest-string-containing-all-unique-characters-from-given-array-of-strings/)

给定一个由[字符串构成的](https://www.geeksforgeeks.org/string-data-structure/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]**，任务是找到包含给定字符串数组中所有字符的最小字符串。

**示例:**

> **输入:**arr[]= {“your”“you”“or”“yo”}
> **输出:** ruyo
> **说明:**字符串“ruyo”是包含给定数组的所有字符串中使用的所有字符的最小字符串。
> 
> **输入:**arr[]= {“abm”、“bmt”、“cd”、“TCA”}
> **输出:**abcdmm

**方法:**这个问题可以通过使用[集合数据结构](http://www.geeksforgeeks.org/hashset-in-java/)来解决。 **Set** 具有去除重复的能力，这是这个问题中为了最小化[串](https://www.geeksforgeeks.org/string-data-structure/)尺寸所需要的。从[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中的所有字符串中加入集合中的所有字符，组成一个包含集合中剩余所有字符的字符串，即为所需答案。

下面是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class GfG {

    public static String minSubstr(String s[])
    {
        // Stores the concatenated string
        // of all the given strings
        String str = "";

        // Loop to iterate through all
        // the given strings
        for (int i = 0; i < s.length; i++) {
            str += s[i];
        }

        // Set to store the characters
        Set<Character> set
            = new HashSet<Character>();

        // Loop to iterate over all
        // the characters in str
        for (int i = 0; i < str.length(); i++) {
            set.add(str.charAt(i));
        }

        // Stores the required answer
        String res = "";
        Iterator<Character> itr
            = set.iterator();

        // Loop to iterate over the set
        while (itr.hasNext()) {
            res += itr.next();
        }

        // Return Answer
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String arr[]
            = new String[] { "your", "you",
                             "or", "yo" };

        System.out.println(minSubstr(arr));
    }
}
```

**Output**

```
ruyo
```

***时间复杂度:** O(N*M)，其中 M 为给定数组中字符串的平均长度*
***辅助空间:** O(1)*