# 按照扩展名的字典顺序排列文件名

> 原文:[https://www . geeksforgeeks . org/sort-file-name-in-accordinate-order-of-their-extensions/](https://www.geeksforgeeks.org/sort-file-names-in-lexicographical-order-of-their-extensions/)

给定代表某些文件名称的字符串数组 **【文件】**，任务是[根据文件名扩展名的字典顺序对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。如果多个文件具有相同的扩展名，则按照字典顺序对它们进行排序。

**示例:**

> **输入:**文件[]= {“ajay . CPP”、“pchy.pdf”、“loki.docx”、“raju . zip”}
> **输出:** ajay.cpp、loki.docx、pchy.pdf、raju.zip
> **解释:**
> 按字典顺序排序的“CPP”<【docx】<【pdf】<“zip”
> 
> **输入:**文件[]= {“abc.cpp”、“bcd.cpp”、“ab.cpp”、“EFG . zip”}
> **输出:** ab.cpp、ABC . CPP、bcd.cpp、efg.zip
> **解释:**
> 由于文件名{“ABC . CPP”、“bcd.cpp”、“ab . CPP”}具有相同的扩展名，因此按照其名称的字典顺序进行排序。

**方法:**按照以下步骤解决问题:

*   [使用](https://www.geeksforgeeks.org/sort-the-array-of-strings-according-to-alphabetical-order-defined-by-another-string/)[比较器功能](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)基于扩展对字符串数组进行排序。
*   对于任何一对具有相同扩展名的文件，请按照其名称的字典顺序对它们进行排序。
*   最后[打印字符串的数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort an array of strings
// based on the extension of their file names
bool custom(string s1, string s2)
{

    // Stores index of '.' in s1
    size_t i = s1.find('.');

    // Stores index of '.' in s2
    size_t j = s2.find('.');

    // Stores name of extension of s2
    string d = s1.substr(i + 1);

    // Stores name of extension of s2
    string e = s2.substr(j + 1);

    // If both files have the
    // same extension name
    if (d == e) {

        // Return lexicographically
        // smaller of the two strings
        return s1 < s2;
    }

    return d < e;
}

// Function to sort the files names
// based on the name of their extension
void sortfromextension(vector<string>& files)
{

    // Sort file names in lexicographical
    // order of their extensions
    sort(files.begin(), files.end(), custom);

    // Print files in sorted form
    // based on extension names
    for (auto s : files) {
        cout << s << ", ";
    }
}

// Driver Code
int main()
{
    vector<string> files
        = { "ajay.cpp", "pchy.pdf",
            "loki.docx", "raju.zip" };

    sortfromextension(files);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class GFG
{

  // Function to sort the files names
  // based on the name of their extension
  static void sortfromextension(String[] files)
  {

    // Sort file names in lexicographical
    // order of their extensions
    Arrays.sort(files, new Comparator<String>(){

      public int compare(String s1,String s2){

        // Stores index of '.' in s1
        int i = s1.indexOf('.');

        // Stores index of '.' in s2
        int j = s2.indexOf('.');

        // Stores name of extension of s2
        String d = s1.substring(i + 1);

        // Stores name of extension of s2
        String e = s2.substring(j + 1);  
        return (d.equals(e))?(s1.compareTo(s2)<0?-1:1):(d.compareTo(e)<0?-1:1);
      }

    });

    // Print files in sorted form
    // based on extension names
    for (int i = 0; i < files.length - 1; i++)
    {
      System.out.print(files[i] + ", ");
    }
    System.out.print(files[files.length - 1]);
  }
  // Driver function
  public static void main (String[] args)
  {
    String[] files
      = { "ajay.cpp", "pchy.pdf",
         "loki.docx", "raju.zip" };

    sortfromextension(files);
  }
}

// This code is contributed by offbeat
```

**Output**

```
ajay.cpp, loki.docx, pchy.pdf, raju.zip, 
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*