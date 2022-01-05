# 打印字符串不同排列的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序到打印-字符串的不同排列/](https://www.geeksforgeeks.org/java-program-to-print-distinct-permutations-of-a-string/)

给定一个字符串 **str** ，任务是打印 **str** 的所有不同排列。
排列是一组物体的全部或部分的排列，与排列的顺序有关。
例如，单词“bat”和“tab”代表相似的三个字母单词的两个不同排列(或排列)。

**示例:**

> **输入**【abbb】
> **输出**【abbb、babb、bbb、bbb】
> 
> **输入:**str = " ABC "
> T3】输出:【ABC、bac、bca、acb、cab、cba】

**方法:**编写一个递归函数，它将生成字符串的所有排列。终止条件将是当传递的字符串为空时，在这种情况下，函数将返回一个空的[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)。在添加生成的字符串之前，只需检查它之前是否已经生成，以获得不同的排列。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.ArrayList;

public class GFG {

    // Function that returns true if string s
    // is present in the Arraylist
    static boolean isPresent(String s, ArrayList<String> Res)
    {

        // If present then return true
        for (String str : Res) {

            if (str.equals(s))
                return true;
        }

        // Not present
        return false;
    }

    // Function to return an ArrayList containg
    // all the distinct permutations of the string
    static ArrayList<String> distinctPermute(String str)
    {

        // If string is empty
        if (str.length() == 0) {

            // Return an empty arraylist
            ArrayList<String> baseRes = new ArrayList<>();
            baseRes.add("");
            return baseRes;
        }

        // Take first character of str
        char ch = str.charAt(0);

        // Rest of the string after excluding
        // the first character
        String restStr = str.substring(1);

        // Recurvise call
        ArrayList<String> prevRes = distinctPermute(restStr);

        // Store the generated sequence into
        // the resultant Arraylist
        ArrayList<String> Res = new ArrayList<>();
        for (String s : prevRes) {
            for (int i = 0; i <= s.length(); i++) {
                String f = s.substring(0, i) + ch + s.substring(i);

                // If the generated string is not
                // already present in the Arraylist
                if (!isPresent(f, Res))

                    // Add the generated string to the Arraylist
                    Res.add(f);
            }
        }

        // Return the resultant arraylist
        return Res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abbb";
        System.out.println(distinctPermute(s));
    }
}
```

**Output:**

```
[abbb, babb, bbab, bbba]

```

 **优化:**我们可以优化上面的解决方案，用 HashSet 存储结果字符串来代替 **Res** ArrayList。