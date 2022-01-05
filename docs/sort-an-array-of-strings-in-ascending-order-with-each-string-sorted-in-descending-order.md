# 按升序排列字符串数组，每个字符串按降序排列

> 原文:[https://www . geesforgeks . org/sort-按升序排列字符串数组，每个字符串按降序排列/](https://www.geeksforgeeks.org/sort-an-array-of-strings-in-ascending-order-with-each-string-sorted-in-descending-order/)

给定一个大小为**N**(*1≤N≤10<sup>5</sup>*)的[字符串数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **S[]** ，则[按照降序对每个字符串的字符进行排序](https://www.geeksforgeeks.org/program-sort-string-descending-order/)，然后[按照升序打印字符串数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)。

**例:**

> ***输入:** s[] = {【苹果】、【盒子】、【猫咪】}*
> ***输出:**pplea TCA xob*
> ***解释:***
> *按降序对每个字符串进行排序，s[]修改为{“pplea”、“xob”、“TCA”}。*
> *对数组进行升序排序将 S[]修改为{pplea，tca，xob}。*
> 
> ***输入:**s[]= {“pqr”、“月亮”、“极客”}*
> ***输出:** oonm rqp skgee*

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   [按降序排列每个字符串](https://www.geeksforgeeks.org/program-sort-string-descending-order/)。q c2
*   对每个字符串进行排序后，[按升序对字符串数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   打印排序后的字符串数组。

下面是上述方法的实现。

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the strings in
// descending order and sort the
// array in ascending order
void sortStr(string s[], int N)
{

    // Traverse the array of strings
    for (int i = 0; i < N; i++) {

        // Sort each string in descending order
        sort(s[i].begin(), s[i].end(),
             greater<char>());
    }

    // Sort the array in ascending order
    sort(s, s + N);

    // Print the array of strings
    for (int i = 0; i < N; i++) {
        cout << s[i] << " ";
    }
}

// Driver Code
int main()
{
    string s[] = { "apple", "box", "cat" };
    int N = sizeof(s) / sizeof(s[0]);
    sortStr(s, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.Arrays;
class GFG{

  // Function to sort the Strings in
  // descending order and sort the
  // array in ascending order
  static void sortStr(String s[], int N)
  {

    // Traverse the array of Strings
    for (int i = 0; i < N; i++)
    {

      // Sort each String in descending order       
      s[i] = reverse(sortString(s[i]));
    }

    // Sort the array in ascending order
    Arrays.sort(s);

    // Print the array of Strings
    for (int i = 0; i < N; i++)
    {
      System.out.print(s[i]+ " ");
    }
  }
  static String sortString(String inputString)
  {

    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(tempArray);
  }
  static String reverse(String input)
  {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--)
    {
      char temp = a[l];
      a[l] = a[r];
      a[r] = temp;
    }
    return String.valueOf(a);
  }

  // Driver Code
  public static void main(String[] args)
  {
    String s[] = { "apple", "box", "cat" };
    int N = s.length;
    sortStr(s, N);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to sort the Strings in
# descending order and sort the
# array in ascending order
def sortStr(s, N):

    # Traverse the array of Strings
    for i in range(N):

        # Sort each String in descending order
        s[i] = "".join(reversed("".join(sorted(s[i])))) ;

    # Sort the array in ascending order
    s = " ".join(sorted(s))

    # Print the array of Strings
    print(s)

# Driver Code
if __name__ == '__main__':
    s = ["apple", "box", "cat"];
    N = len(s);
    sortStr(s, N);

    # This code is contributed by shikhasingrajput
```

## C#

```
// C# program of the above approach
using System;
class GFG {

  static void reverse(char[] a)
  {
    int i, n = a.Length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
      t = a[i];
      a[i] = a[n - i - 1];
      a[n - i - 1] = t;
    }
  }

  // Function to sort the strings in
  // descending order and sort the
  // array in ascending order
  static void sortStr(string[] s, int N)
  {

    // Traverse the array of strings
    for (int i = 0; i < N; i++)
    {
      char[] t = s[i].ToCharArray();

      // Sort each string
      Array.Sort(t);

      // Reverse the string
      reverse(t);
      s[i] = String.Join("", t);
    }

    // Sort the array in ascending order
    Array.Sort(s);

    // Print the array of strings
    for (int i = 0; i < N; i++)
    {
      Console.Write(s[i] + " ");
    }
  }

  // Driver Code
  public static void Main()
  {
    string[] s = { "apple", "box", "cat" };
    int N = s.Length;
    sortStr(s, N);
  }
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to sort the strings in
// descending order and sort the
// array in ascending order
function sortStr( s, N)
{

    // Traverse the array of strings
    for (var i = 0; i < N; i++) {

        // Sort each string in descending order
        s[i] = s[i].split('').sort((a,b)=>b>a).join('')
    }

    // Sort the array in ascending order
    s.sort();

    // Print the array of strings
    for (var i = 0; i < N; i++) {
        document.write( s[i] + " ");
    }
}

// Driver Code
var s = [ "apple", "box", "cat" ];
var N = s.length;
sortStr(s, N);

</script>
```

**Output:** 

```
pplea tca xob
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*