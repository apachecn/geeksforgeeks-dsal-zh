# 使用数组列表

打印字符串的所有排列

> 原文:[https://www . geesforgeks . org/print-all-置换字符串-使用-arraylist/](https://www.geeksforgeeks.org/print-all-permutation-of-a-string-using-arraylist/)

给定一个字符串 **str** ，任务是打印 **str** 的所有排列。
排列是一组物体的全部或部分的排列，与排列的顺序有关。
例如，单词“bat”和“tab”代表相似的三个字母单词的两个不同排列(或排列)。
**举例:**

> **输入:**【str = " ABC】
> **输出:** abc acb bac bca cba cab
> **输入:**【str = " bat】**输出:** bat bta abt atb tba tab】

**方法:**编写一个递归函数，它将生成字符串的所有排列。终止条件将是当传递的字符串为空时，在这种情况下，函数将返回一个空的[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)。
以下是上述方法的实施:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;

public class GFG {

    // Utility function to print the contents
    // of the ArrayList
    static void printArrayList(ArrayList<String> arrL)
    {
        arrL.remove("");
        for (int i = 0; i < arrL.size(); i++)
            System.out.print(arrL.get(i) + " ");
    }

    // Function to returns the arraylist which contains
    // all the permutation of str
    public static ArrayList<String> getPermutation(String str)
    {

        // If string is empty
        if (str.length() == 0) {

            // Return an empty arraylist
            ArrayList<String> empty = new ArrayList<>();
            empty.add("");
            return empty;
        }

        // Take first character of str
        char ch = str.charAt(0);

        // Take sub-string starting from the
        // second character
        String subStr = str.substring(1);

        // Recurvise call
        ArrayList<String> prevResult = getPermutation(subStr);

        // Store the generated permutations
        // into the resultant arraylist
        ArrayList<String> Res = new ArrayList<>();

        for (String val : prevResult) {
            for (int i = 0; i <= val.length(); i++) {
                Res.add(val.substring(0, i) + ch + val.substring(i));
            }
        }

        // Return the resultant arraylist
        return Res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abc";
        printArrayList(getPermutation(str));
    }
}
```

## C#

```
// C# implementation of the approach
using System.Collections.Generic;
using System;

class GFG
{

    // Utility function to print the contents
    // of the ArrayList
    static void printArrayList(List<String> arrL)
    {
        arrL.Remove("");
        for (int i = 0; i < arrL.Count; i++)
            Console.Write(arrL[i] + " ");
    }

    // Function to returns the arraylist which contains
    // all the permutation of str
    public static List<String> getPermutation(String str)
    {

        // If string is empty
        if (str.Length == 0)
        {

            // Return an empty arraylist
            List<String> empty = new List<String>();
            empty.Add("");
            return empty;
        }

        // Take first character of str
        char ch = str[0];

        // Take sub-string starting from the
        // second character
        String subStr = str.Substring(1);

        // Recurvise call
        List<String> prevResult = getPermutation(subStr);

        // Store the generated permutations
        // into the resultant arraylist
        List<String> Res = new List<String>();

        foreach (String val in prevResult)
        {
            for (int i = 0; i <= val.Length; i++)
            {
                Res.Add(val.Substring(0, i) + ch + val.Substring(i));
            }
        }

        // Return the resultant arraylist
        return Res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "abc";
        printArrayList(getPermutation(str));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Utility function to print the contents
    // of the ArrayList
function printArrayList(arrL)
{

        for (let i = 0; i < arrL.length; i++)
            document.write(arrL[i] + " ");
}

// Function to returns the arraylist which contains
    // all the permutation of str
function getPermutation(str)
{
    // If string is empty
        if (str.length == 0) {

            // Return an empty arraylist
            let empty = [];
            empty.push("");
            return empty;
        }

        // Take first character of str
        let ch = str[0];

        // Take sub-string starting from the
        // second character
        let subStr = str.substring(1);

        // Recurvise call
        let prevResult = getPermutation(subStr);

        // Store the generated permutations
        // into the resultant arraylist
        let Res = [];

        for (let val of prevResult) {
            for (let i = 0; i <= val.length; i++) {
                Res.push(val.substring(0, i) + ch + val.substring(i));
            }
        }

        // Return the resultant arraylist
        return Res;
}

// Driver code
let str = "abc";
printArrayList(getPermutation(str));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
abc bac bca acb cab cba
```