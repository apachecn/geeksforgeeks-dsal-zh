# 从给定字符串中删除重复项的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-从给定字符串中删除重复项的程序/](https://www.geeksforgeeks.org/java-program-to-remove-duplicates-from-a-given-string/)

给定一个字符串 **S** ，任务是删除给定字符串中的所有重复项。
以下是删除字符串中重复项的不同方法。

**方法 1(简单)**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicate character
// from character array and print in sorted
// order
import java.util.*;

class GFG 
{
    static String removeDuplicate(char str[], int n)
    {
        // Used as index in the modified string
        int index = 0;

        // Traverse through all characters
        for (int i = 0; i < n; i++)
        {

            // Check if str[i] is present before it 
            int j;
            for (j = 0; j < i; j++) 
            {
                if (str[i] == str[j])
                {
                    break;
                }
            }

            // If not present, then add it to
            // result.
            if (j == i) 
            {
                str[index++] = str[i];
            }
        }
        return String.valueOf(Arrays.copyOf(str, index));
    }

    // Driver code
    public static void main(String[] args)
    {
        char str[] = "geeksforgeeks".toCharArray();
        int n = str.length;
        System.out.println(removeDuplicate(str, n));
    }
}

// This code is contributed by Rajput-Ji
```

**输出:**

```
geksfor
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(1)
保持元素顺序与输入相同。

**方法 2(使用 BST)**
使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，实现二叉查找树的自平衡。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicate character
// from character array and print in sorted
// order
import java.util.*;

class GFG {

    static void removeDuplicate(char str[], int n)
    {
       // Create a set using String characters
    // excluding '�'
        HashSet<Character> s = new LinkedHashSet<>(n - 1);
      // HashSet doesn't allow repetition of elements
        for (char x : str)
            s.add(x);

        // Print content of the set
        for (char x : s)
            System.out.print(x);
    }

    // Driver code
    public static void main(String[] args)
    {
        char str[] = "geeksforgeeks".toCharArray();
        int n = str.length;

        removeDuplicate(str, n);
    }
}

// This code is contributed by todaysgaurav
```

**输出:**

```
  efgkors
```

**时间复杂度**:O(n Log n)
T3】辅助空间 : O(n)

感谢阿尼维什·蒂瓦里 提出这种方法。

它不会保持元素的顺序与输入相同，而是按排序顺序打印它们。

**方法 3(使用排序)**
**算法:**

```
  1) Sort the elements.
  2) Now in a loop, remove duplicates by comparing the 
      current character with previous character.
  3)  Remove extra characters at the end of the resultant string.
```

**示例:**

```
Input string:  geeksforgeeks
1) Sort the characters
   eeeefggkkorss
2) Remove duplicates
    efgkorskkorss
3) Remove extra characters
     efgkors
```

请注意，此方法不保持输入字符串的原始顺序。例如，如果我们要删除 geeksforgeeks 的重复项，并保持字符的顺序不变，那么输出应该是 geksfor，但是上面的函数返回 efgkos。我们可以通过存储原始订单来修改此方法。

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicates, the order of
// characters is not maintained in this program

import java.util.Arrays;

public class GFG 
{
    /* Method to remove duplicates in a sorted array */
    static String removeDupsSorted(String str)
    {
        int res_ind = 1, ip_ind = 1;

        // Character array for removal of duplicate characters
        char arr[] = str.toCharArray();

        /* In place removal of duplicate characters*/
        while (ip_ind != arr.length)
        {
            if(arr[ip_ind] != arr[ip_ind-1])
            {
                arr[res_ind] = arr[ip_ind];
                res_ind++;
            }
            ip_ind++;

        }

        str = new String(arr);
        return str.substring(0,res_ind);
    }

    /* Method removes duplicate characters from the string
       This function work in-place and fills null characters
       in the extra space left */
    static String removeDups(String str)
    {
       // Sort the character array
       char temp[] = str.toCharArray();
       Arrays.sort(temp);
       str = new String(temp);

       // Remove duplicates from sorted
       return removeDupsSorted(str);
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println(removeDups(str));
    }
}
```

**输出:**

```
efgkors
```

**时间复杂度:** O(n log n)如果我们用一些 n log n 排序算法来代替快速排序。

**辅助空间:** O(1)

**方法 4(使用散列法)**

**算法:**

```
1: Initialize:
    str  =  "test string" /* input string */
    ip_ind =  0          /* index to  keep track of location of next
                             character in input string */
    res_ind  =  0         /* index to  keep track of location of
                            next character in the resultant string */
    bin_hash[0..255] = {0,0, ….} /* Binary hash to see if character is 
                                        already processed or not */
2: Do following for each character *(str + ip_ind) in input string:
              (a) if bin_hash is not set for *(str + ip_ind) then
                   // if program sees the character *(str + ip_ind) first time
                         (i)  Set bin_hash for *(str + ip_ind)
                         (ii)  Move *(str  + ip_ind) to the resultant string.
                              This is done in-place.
                         (iii) res_ind++
              (b) ip_ind++
  /* String obtained after this step is "te stringing" */
3: Remove extra characters at the end of the resultant string.
  /*  String obtained after this step is "te string" */
```

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicates
import java.util.*;

class RemoveDuplicates
{
    /* Function removes duplicate characters from the string
    This function work in-place */
    void removeDuplicates(String str)
    {
        LinkedHashSet<Character> lhs = new LinkedHashSet<>();
        for(int i=0;i<str.length();i++)
            lhs.add(str.charAt(i));

        // print string after deleting duplicate elements
        for(Character ch : lhs)
            System.out.print(ch);
    }

    /* Driver program to test removeDuplicates */
    public static void main(String args[])
    {
        String str = "geeksforgeeks";
        RemoveDuplicates r = new RemoveDuplicates();
        r.removeDuplicates(str);
    }
}

// This code has been contributed by Amit Khandelwal (Amit Khandelwal 1)
```

**输出:**

```
geksfor
```

**时间复杂度:** O(n)

**要点:**

*   方法 2 没有将字符保持为原始字符串，但是方法 4 保持了。
*   假设输入字符串中可能的字符数是 256。应该相应地改变字符数。
*   calloc()代替 malloc()用于计数数组(count)的内存分配，以将分配的内存初始化为“”。也可以使用 malloc()后跟 memset()。
*   如果给定数组中整数的范围，上述算法也适用于整数数组输入。一个示例问题是，假设输入数组只包含 1000 到 1100 之间的整数，则找出输入数组中出现的最大数字

**方法 5** (使用**索引 Of()** 方法):
T5】先决条件:T7】Java**索引 Of()** 方法

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create a unique string
import java.util.*;

class IndexOf {

    // Function to make the string unique
    public static String unique(String s)
    {
        String str = new String();
        int len = s.length();

        // loop to traverse the string and
        // check for repeating chars using
        // IndexOf() method in Java
        for (int i = 0; i < len; i++) 
        {
            // character at i'th index of s
            char c = s.charAt(i);

            // if c is present in str, it returns
            // the index of c, else it returns -1
            if (str.indexOf(c) < 0)
            {
                // adding c to str if -1 is returned
                str += c;
            }
        }

        return str;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Input string with repeating chars
        String s = "geeksforgeeks";

        System.out.println(unique(s));
    }
}
```

**输出:**

```
geksfor
```

感谢 [**debjitdbb**](https://auth.geeksforgeeks.org/user/debjitdbb/articles) 提出这个方法。

**方法 6** (使用**无序 _ 映射 STL** 方法):
**先决条件:** [无序 _ 映射 STL C++方法](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create a unique String using unordered_map

/* access time in unordered_map on is O(1) generally if no collisions occur 
and therefore it helps us check if an element exists in a String in O(1) 
time complexity with constant space. */
import java.util.*;

class GFG{ 
static char[] removeDuplicates(char []s,int n){
  Map<Character,Integer> exists = new HashMap<>();

  String st = "";
  for(int i = 0; i < n; i++){
    if(!exists.containsKey(s[i]))
    {
      st += s[i];
      exists.put(s[i], 1);
    }
  }
  return st.toCharArray();
}

// driver code
public static void main(String[] args){
  char s[] = "geeksforgeeks".toCharArray();
  int n = s.length;
  System.out.print(removeDuplicates(s,n));
}
}

// This code is contributed by gauravrajput1 
```

**输出:**

```
geksfor
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
谢谢，**艾伦·詹姆斯·维诺伊**提出这个方法。

更多详情请参考[从给定字符串](https://www.geeksforgeeks.org/remove-duplicates-from-a-given-string/)中删除重复项的完整文章！