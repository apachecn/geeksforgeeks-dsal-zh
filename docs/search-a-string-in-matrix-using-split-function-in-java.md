# 使用 Java 中的 Split 函数在 Matrix 中搜索字符串

> 原文:[https://www . geesforgeks . org/search-a-string-in-matrix-using-split-function-in-Java/](https://www.geeksforgeeks.org/search-a-string-in-matrix-using-split-function-in-java/)

给定一个字符串 **str** 和一个由小写英文字母组成的矩阵 **mat[][]** ，任务是找出字符串 *str* 是否出现在矩阵中(行方向或列方向)。

**示例:**

```
Input: str = "GFG"
            mat[][] = {{'G', 'E', 'E', 'K', 'S'}, 
                             {'F', 'O', 'R', 'A', 'N'}, 
                             {'G', 'E', 'E', 'K', 'S'}}
**Output:** Yes
GFG is present in the first column.

**Input**: str = "SSS"
            mat[][] = {{'G', 'E', 'E', 'K', 'S'}, 
                              {'F', 'O', 'R', 'A', 'N'}, 
                              {'G', 'E', 'E', 'K', 'S'}}
**Output:** No 
```

****方法:**
如果搜索字符串出现在矩阵的任何一行，拆分函数将产生以下结果:**

1.  **如果字符串占据了整行，那么[分割函数](https://www.geeksforgeeks.org/split-string-java-examples/)将返回一个长度为零的数组。**
2.  **如果字符串出现在字符之间，那么数组长度将大于 1。**
3.  **如果数组长度是 1，那么可能有三种情况-

    *   字符串出现在前半部分。
    *   字符串出现在后半部分。
    *   该字符串不在该行中。** 
4.  **要逐列搜索字符串[，转置矩阵](https://www.geeksforgeeks.org/program-to-find-transpose-of-a-matrix/)并重复第一步。**
5.  **打印*是*如果找到字符串，则打印*否*。**

**下面是上述方法的实现:**

```
// Java program to search a string in
// the matrix using split function
import java.util.*;
public class GFG {

    // Function to check the occurrence of string in the matrix
    public static int check(String[] matrix, String string)
    {
        // Looping the contents in the matrix
        for (String input : matrix) {

            // using split operator
            String[] value = input.split(string);

            if (value.length >= 2 || value.length == 0) {
                return 1;
            }
            else if (value.length == 1
                     && input.length() != value[0].length()) {
                return 1;
            }
        }
        return 0;
    }

    // Function to transpose the given matrix
    public static String[] vertical(String[] matrix)
    {
        String[] vertical_value = new String[matrix[0].length()];
        for (int i = 0; i < matrix[0].length(); i++) {
            String temp = "";
            for (int j = 0; j < matrix.length; j++)
                temp += matrix[j].charAt(i);
            vertical_value[i] = temp;
        }

        // returning the transposed matrix
        return vertical_value;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Input matrix of characters
        String[] matrix = { "GEEKS", "FORAN", "GEEKS" };

        // element to be searched
        String search = "GFG";

        // Transpose of the matrix
        String[] verticalMatrix = vertical(matrix);

        // Searching process
        int horizontal_search = check(matrix, search);
        int vertical_search = check(verticalMatrix, search);

        // If found
        if (horizontal_search == 1 || vertical_search == 1)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

****Output:**

```
Yes

```**