# 找到所有给定字符串都可以用其字符生成的最小字符串

> 原文:[https://www . geeksforgeeks . org/find-最小字符串-带有谁的字符-所有给定的字符串都可以生成/](https://www.geeksforgeeks.org/find-smallest-string-with-whose-characters-all-given-strings-can-be-generated/)

给定一组字符串 **arr[]。**任务是生成包含数组中所有字符串的所有字符且大小最小的字符串。可以有许多这样的可能字符串，任何一个都是可以接受的。

**示例**:

> **输入:** arr[] = {“你的”、“你的”、“或”、“哟”}
> **输出:** ruyo
> **说明:**字符串“ruyo”是包含 arr[]中所有字符串中存在的所有字符的字符串。
> 可以有许多其他大小为 4 的字符串，例如“oury”。这些也是可以接受的。
> 
> **输入:**arr[]= {“abm”、“bmt”、“cd”、“TCA”}
> **输出:**abcdmm

**逼近**:这个问题可以用**集合数据结构**解决。Set 能够删除重复项，这是这个问题中为了最小化字符串大小所需要的。从数组**arr【】**中的所有字符串中，将集合中的所有字符相加，组成一个包含集合中剩余所有字符的字符串，即为所需答案。

下面是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach
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
        Set<Character> set = 
            new HashSet<Character>();

        // Loop to iterate over all
        // the characters in str
        for (int i = 0; i < str.length(); 
             i++) {
            set.add(str.charAt(i));
        }

        // Stores the required answer
        String res = "";
        Iterator<Character> itr = 
            set.iterator();

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

***时间复杂度** :* O(N*M)，其中 M 为给定数组中字符串的平均长度
***辅助空间:*** O(1)