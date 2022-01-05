# 子串排序

> 原文:[https://www.geeksforgeeks.org/substring-sort/](https://www.geeksforgeeks.org/substring-sort/)

给定 n 个字符串，我们需要对这些字符串进行排序，使得每个字符串都是其后面的所有字符串**的子字符串。如果无法排序，则打印相同的内容。
**例:**** 

```
Input : {"d", "zddsaaz", "ds", "ddsaa", "dds"}
Output :
    d
    ds
    dds
    ddsaa
    zddsaaz

Input : {"geeks", "ee", "geeksforgeeks", "forgeeks", "ee"}
Output :
    ee
    ee
    geeks
    forgeeks
    geeksforgeeks
```

**观察 1**
如果 B 的 A 子串
那么 A 的长度<= B 的长度
T5【观察 2
如果(B 的 A 子串)和(C 的 B 子串)
那么 C 的 A 子串
**解决方案**
基于以上两个观察，解决方案如下

1.  将所有字符串从短到长排序
2.  验证每个字符串是以下字符串的子字符串

如果我们验证每个字符串是下面字符串的子串，那么根据观察 2，每个字符串是它后面所有字符串的子串。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to sort substrings
import java.util.Arrays;
import java.util.Comparator;

public class Demo {
    public static void substringSort(String[] arr, int n)
    {
        // sort the given array from shorter string to longer
        Arrays.sort(arr, new Comparator<String>() {
            public int compare(String s1, String s2)
            {
                return Integer.compare(s1.length(), s2.length());
            }
        });

        // validate that each string is a substring of
        // the following one'
        for (int i = 0; i < n - 1; i++) {
            if (!arr[i + 1].contains(arr[i])) {

                // the array can't be sorted
                System.out.println("Cannot be sorted");
                return;
            }
        }

        // The array is valid and sorted
        // print the strings in order
        for (int i = 0; i < n - 1; i++) {
            System.out.println(arr[i]);
        }
    }

    public static void main(String[] args)
    {
        // Test 1
        String[] arr1 = { "d", "zddsaaz", "ds", "ddsaa", "dds" };
        substringSort(arr1, arr1.length);

        // Test 2
        String[] arr2 = { "for", "rof" };
        substringSort(arr2, arr2.length);
    }
}
```

**Output:** 

```
d
ds
dds
ddsaa
Cannot be sorted
```