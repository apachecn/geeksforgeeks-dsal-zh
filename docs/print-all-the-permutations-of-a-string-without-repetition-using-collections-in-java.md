# 使用 Java 中的 Collections 打印字符串的所有排列，不重复

> 原文:[https://www . geeksforgeeks . org/print-所有不重复的字符串排列-使用 java 中的集合/](https://www.geeksforgeeks.org/print-all-the-permutations-of-a-string-without-repetition-using-collections-in-java/)

给定一个字符串 **str** ，任务是打印 **str** 的所有排列。排列是一组对象的全部或部分的排列，与排列的顺序有关。一个置换不应该在输出中有重复的字符串。

**示例:**

> **输入:** str = "aa"
> **输出:**
> aa
> 注意“aa”只打印一次
> 不允许重复。
> 
> **输入:**str = " ab "
> T3】输出:T5】ab
> ba

**方法:**编写一个递归函数，从原始字符串中逐个删除一个字符，并通过追加这些删除的字符生成一个新字符串。基本条件是所有字符都已被使用。在这种情况下，将生成的字符串(原始字符串的置换)插入到[集合](https://www.geeksforgeeks.org/set-in-java/)中，以避免重复。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.*;
public class GFG {

    static Set<String> hash_Set = new HashSet<>();

    // Recursive function to generate
    // permutations of the string
    static void Permutation(String str, String ans)
    {

        // If string is empty
        if (str.length() == 0) {

            // Add the generated permutation to the
            // set in order to avoid duplicates
            hash_Set.add(ans);
            return;
        }

        for (int i = 0; i < str.length(); i++) {

            // ith character of str
            char ch = str.charAt(i);

            // Rest of the string after excluding
            // the ith character
            String ros = str.substring(0, i)
                         + str.substring(i + 1);

            // Recurvise call
            Permutation(ros, ans + ch);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "ab";

        // Generate permutations
        Permutation(s, "");

        // Print the generated permutations
        hash_Set.forEach((n) -> System.out.println(n));
    }
}
```

**Output:**

```
ab
ba

```