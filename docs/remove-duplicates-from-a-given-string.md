# 从给定字符串中删除重复项

> 原文:[https://www . geesforgeks . org/remove-replications-from-a-给定字符串/](https://www.geeksforgeeks.org/remove-duplicates-from-a-given-string/)

给定一个字符串 **S** ，任务是删除给定字符串中的所有重复项。
以下是删除字符串中重复项的不同方法。

**方法 1(简单)**

## C++

```
// CPP program to remove duplicate character
// from character array and print in sorted
// order
#include <bits/stdc++.h>
using namespace std;

char *removeDuplicate(char str[], int n)
{
   // Used as index in the modified string
   int index = 0;   

   // Traverse through all characters
   for (int i=0; i<n; i++) {

     // Check if str[i] is present before it  
     int j;  
     for (j=0; j<i; j++) 
        if (str[i] == str[j])
           break;

     // If not present, then add it to
     // result.
     if (j == i)
        str[index++] = str[i];
   }

   return str;
}

// Driver code
int main()
{
   char str[]= "geeksforgeeks";
   int n = sizeof(str) / sizeof(str[0]);
   cout << removeDuplicate(str, n);
   return 0;
}
```

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

## 蟒蛇 3

```
string="geeksforgeeks"
p=""
for char in string:
    if char not in p:
        p=p+char
print(p)
k=list("geeksforgeeks")
```

## C#

```
// C# program to remove duplicate character
// from character array and print in sorted
// order
using System;
using System.Collections.Generic;
class GFG 
{
static String removeDuplicate(char []str, int n)
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
    char [] ans = new char[index];
    Array.Copy(str, ans, index);
    return String.Join("", ans);
}

// Driver code
public static void Main(String[] args)
{
    char []str = "geeksforgeeks".ToCharArray();
    int n = str.Length;
    Console.WriteLine(removeDuplicate(str, n));
}
}

// This code is contributed by PrinciRaj1992 
```

## java 描述语言

```
<script>

// JavaScript program to remove duplicate character
// from character array and print in sorted
// order
function removeDuplicate(str, n)
    {
        // Used as index in the modified string
        var index = 0;

        // Traverse through all characters
        for (var i = 0; i < n; i++)
        {

            // Check if str[i] is present before it 
            var j;
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

        return str.join("").slice(str, index);
    }

    // Driver code
        var str = "geeksforgeeks".split("");
        var n = str.length;
        document.write(removeDuplicate(str, n));

// This code is contributed by shivanisinghss2110

</script>
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

## C++

```
// CPP program to remove duplicate character
// from character array and print in sorted
// order
#include <bits/stdc++.h>
using namespace std;

char *removeDuplicate(char str[], int n)
{
    // create a set using string characters
    // excluding '\0'
    set<char>s (str, str+n-1);

    // print content of the set
    int i = 0;
    for (auto x : s)
       str[i++] = x;
    str[i] = '\0';

    return str;
}

// Driver code
int main()
{
   char str[]= "geeksforgeeks";
   int n = sizeof(str) / sizeof(str[0]);
   cout << removeDuplicate(str, n);
   return 0;
}
```

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
    // excluding '\0'
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

## 蟒蛇 3

```
# Python program to remove duplicate character
# from character array and print in sorted
# order
def removeDuplicate(str, n):
    s = set()

    # Create a set using String characters
    for i in str:
        s.add(i)

    # Print content of the set
    st = ""
    for i in s:
        st = st+i
    return st

# Driver code
str = "geeksforgeeks"
n = len(str)
print(removeDuplicate(list(str), n))

# This code is contributed by rajsanghavi9.
```

## C#

```
// C# program to remove duplicate character
// from character array and print in sorted
// order
using System;
using System.Collections.Generic;

public class GFG{

static char []removeDuplicate(char []str, int n)
{

    // Create a set using String characters
    // excluding '\0'
    HashSet<char>s = new HashSet<char>(n - 1);
    foreach(char x in str)
        s.Add(x);

    char[] st = new char[s.Count];

    // Print content of the set
    int i = 0;
    foreach(char x in s)
       st[i++] = x;

    return st;
}

// Driver code
public static void Main(String[] args)
{
   char []str= "geeksforgeeks".ToCharArray();
   int n = str.Length;

   Console.Write(removeDuplicate(str, n));
}
} 

// This code contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program to remove duplicate character
// from character array and print in sorted
// order

    function removeDuplicate( str , n) 
    {

        // Create a set using String characters
        // excluding '\0'
        var s = new Set();

        // HashSet doesn't allow repetition of elements
        for (var i = 0;i<n;i++)
            s.add(str[i]);

        // Print content of the set
        for (const v of s) {

            document.write(v);
    }
    }

    // Driver code
        var str = "geeksforgeeks";
        var n = str.length;

        removeDuplicate(str, n);

// This code is contributed by umadevi9616 
</script>
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

## C++

```
// C++ program to remove duplicates, the order of
// characters is not maintained in this program
#include<bits/stdc++.h>
using namespace std;

/* Function to remove duplicates in a sorted array */
char *removeDupsSorted(char *str)
{
    int res_ind = 1, ip_ind = 1;

    /* In place removal of duplicate characters*/
    while (*(str + ip_ind))
    {
        if (*(str + ip_ind) != *(str + ip_ind - 1))
        {
            *(str + res_ind) = *(str + ip_ind);
            res_ind++;
        }
        ip_ind++;
    }

    /* After above step string is efgkorskkorss.
       Removing extra kkorss after string*/
    *(str + res_ind) = '\0';

    return str;
}

/* Function removes duplicate characters from the string
   This function work in-place and fills null characters
   in the extra space left */
char *removeDups(char *str)
{
   int n = strlen(str);

   // Sort the character array
   sort(str, str+n);

   // Remove duplicates from sorted
   return removeDupsSorted(str);
}

/* Driver program to test removeDups */
int main()
{
  char str[] = "geeksforgeeks";
  cout << removeDups(str);
  return 0;
}
```

## C

```
// C++ program to remove duplicates, the order of
// characters is not maintained in this program
# include <stdio.h>
# include <stdlib.h>
# include <string.h>
/* Function to remove duplicates in a sorted array */
char *removeDupsSorted(char *str);

/* Utility function to sort array A[] */
void quickSort(char A[], int si, int ei);

/* Function removes duplicate characters from the string
   This function work in-place and fills null characters
   in the extra space left */
char *removeDups(char *str)
{
  int len = strlen(str);
  quickSort(str, 0, len-1);
  return removeDupsSorted(str);
}     

/* Function to remove duplicates in a sorted array */
char *removeDupsSorted(char *str)
{
  int res_ind = 1, ip_ind = 1;

  /* In place removal of duplicate characters*/
  while (*(str + ip_ind))
  {
    if (*(str + ip_ind) != *(str + ip_ind - 1))
    {
      *(str + res_ind) = *(str + ip_ind);
      res_ind++;
    }
    ip_ind++;
  }      

  /* After above step string is efgkorskkorss.
     Removing extra kkorss after string*/
  *(str + res_ind) = '\0';

  return str;
}

/* Driver program to test removeDups */
int main()
{
  char str[] = "geeksforgeeks";
  printf("%s", removeDups(str));
  getchar();
  return 0;
}

/* FOLLOWING FUNCTIONS ARE ONLY FOR SORTING
    PURPOSE */
void exchange(char *a, char *b)
{
  char temp;
  temp = *a;
  *a   = *b;
  *b   = temp;
}

int partition(char A[], int si, int ei)
{
  char x = A[ei];
  int i = (si - 1);
  int j;

  for (j = si; j <= ei - 1; j++)
  {
    if (A[j] <= x)
    {
      i++;
      exchange(&A[i], &A[j]);
    }
  }
  exchange (&A[i + 1], &A[ei]);
  return (i + 1);
}

/* Implementation of Quick Sort
A[] --> Array to be sorted
si  --> Starting index
ei  --> Ending index
*/
void quickSort(char A[], int si, int ei)
{
  int pi;    /* Partitioning index */
  if (si < ei)
  {
    pi = partition(A, si, ei);
    quickSort(A, si, pi - 1);
    quickSort(A, pi + 1, ei);
  }
}
```

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

## 计算机编程语言

```
# Python program to remove duplicates, the order of
# characters is not maintained in this program

# Utility function to convert string to list
def toMutable(string):
    temp = []
    for x in string:
        temp.append(x)
    return temp

# Utility function to convert string to list
def toString(List):
    return ''.join(List)

# Function to remove duplicates in a sorted array
def removeDupsSorted(List):
    res_ind = 1
    ip_ind = 1

    # In place removal of duplicate characters
    while ip_ind != len(List):
        if List[ip_ind] != List[ip_ind-1]:
            List[res_ind] = List[ip_ind]
            res_ind += 1
        ip_ind+=1

    # After above step string is efgkorskkorss.
    # Removing extra kkorss after string
    string = toString(List[0:res_ind])

    return string

# Function removes duplicate characters from the string
# This function work in-place and fills null characters
# in the extra space left
def removeDups(string):
    # Convert string to list
    List = toMutable(string)

    # Sort the character list
    List.sort()

    # Remove duplicates from sorted
    return removeDupsSorted(List)

# Driver program to test the above functions
string = "geeksforgeeks"
print removeDups(string)

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to remove duplicates, the order of
// characters is not maintained in this program
using System;

class GFG 
{
    /* Method to remove duplicates in a sorted array */
    static String removeDupsSorted(String str)
    {
        int res_ind = 1, ip_ind = 1;

        // Character array for removal of duplicate characters
        char []arr = str.ToCharArray();

        /* In place removal of duplicate characters*/
        while (ip_ind != arr.Length)
        {
            if(arr[ip_ind] != arr[ip_ind-1])
            {
                arr[res_ind] = arr[ip_ind];
                res_ind++;
            }
            ip_ind++;

        }

        str = new String(arr);
        return str.Substring(0,res_ind);
    }

    /* Method removes duplicate characters from the string
    This function work in-place and fills null characters
    in the extra space left */
    static String removeDups(String str)
    {
    // Sort the character array
    char []temp = str.ToCharArray();
    Array.Sort(temp);
    str = String.Join("",temp);

    // Remove duplicates from sorted
    return removeDupsSorted(str);
    }

    // Driver Method
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        Console.WriteLine(removeDups(str));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

function removeDuplicate(string)
{
   return string.split('')
    .filter(function(item, pos, self)
    {
      return self.indexOf(item) == pos;
    }
   ).join('');
}

var str = "geeksforgeeks";
document.write( " "+removeDuplicate(str));

//This code is contributed by SoumikMondal
</script>
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

## C++

```
#include <bits/stdc++.h>
using namespace std; 
# define NO_OF_CHARS 256 
# define bool int 

/* Function removes duplicate characters from the string 
This function work in-place and fills null characters 
in the extra space left */
char *removeDups(char str[]) 
{ 
    bool bin_hash[NO_OF_CHARS] = {0}; 
    int ip_ind = 0, res_ind = 0; 
    char temp; 

    /* In place removal of duplicate characters*/
    while (*(str + ip_ind)) 
    { 
        temp = *(str + ip_ind); 
        if (bin_hash[temp] == 0) 
        { 
            bin_hash[temp] = 1; 
            *(str + res_ind) = *(str + ip_ind); 
            res_ind++; 
        } 
        ip_ind++; 
    } 

    /* After above step string is stringiittg. 
        Removing extra iittg after string*/
    *(str+res_ind) = '\0'; 

    return str; 
} 

/* Driver code */
int main() 
{ 
    char str[] = "geeksforgeeks"; 
    cout << removeDups(str); 
    return 0; 
} 

// This code is contributed by rathbhupendra
```

## C

```
# include <stdio.h>
# include <stdlib.h>
# define NO_OF_CHARS 256
# define bool int

/* Function removes duplicate characters from the string
   This function work in-place and fills null characters
   in the extra space left */
char *removeDups(char *str)
{
  bool bin_hash[NO_OF_CHARS] = {0};
  int ip_ind = 0, res_ind = 0;
  char temp;    

  /* In place removal of duplicate characters*/
  while (*(str + ip_ind))
  {
    temp = *(str + ip_ind);
    if (bin_hash[temp] == 0)
    {
        bin_hash[temp] = 1;
        *(str + res_ind) = *(str + ip_ind);
        res_ind++;
    }
    ip_ind++;
  }      

  /* After above step string is stringiittg.
     Removing extra iittg after string*/
  *(str+res_ind) = '\0';   

  return str;
}

/* Driver program to test removeDups */
int main()
{
    char str[] = "geeksforgeeks";
    printf("%s", removeDups(str));
    getchar();
    return 0;
}
```

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

## 计算机编程语言

```
# Python program to remove duplicate characters from an
# input string
NO_OF_CHARS = 256

# Since strings in Python are immutable and cannot be changed
# This utility function will convert the string to list
def toMutable(string):
    List = []
    for i in string:
        List.append(i)
    return List

# Utility function that changes list to string
def toString(List):
    return ''.join(List)

# Function removes duplicate characters from the string
# This function work in-place and fills null characters
# in the extra space left
def removeDups(string):
    bin_hash = [0] * NO_OF_CHARS
    ip_ind = 0
    res_ind = 0
    temp = ''
    mutableString = toMutable(string)

    # In place removal of duplicate characters
    while ip_ind != len(mutableString):
        temp = mutableString[ip_ind]
        if bin_hash[ord(temp)] == 0:
            bin_hash[ord(temp)] = 1
            mutableString[res_ind] = mutableString[ip_ind]
            res_ind+=1
        ip_ind+=1

     # After above step string is stringiittg.
     # Removing extra iittg after string
    return toString(mutableString[0:res_ind])

# Driver program to test the above functions
string = "geeksforgeeks"
print(removeDups(string))

# A shorter version for this program is as follows
# import collections
# print ''.join(collections.OrderedDict.fromkeys(string))

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to remove duplicates
using System;
using System.Collections.Generic;

class GFG
{
    /* Function removes duplicate characters 
    from the string. This function work in-place */
    void removeDuplicates(String str)
    {
        HashSet<char> lhs = new HashSet<char>();
        for(int i = 0; i < str.Length; i++)
            lhs.Add(str[i]);

        // print string after deleting 
        // duplicate elements
        foreach(char ch in lhs)
            Console.Write(ch);
    }

    // Driver Code
    public static void Main(String []args)
    {
        String str = "geeksforgeeks";
        GFG r = new GFG();
        r.removeDuplicates(str);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to remove duplicates
    /*
     * Function removes duplicate characters from the string This function work
     * in-place
     */
    function removeDuplicates( str) {
        var lhs = new Set();
        for (var i = 0; i < str.length; i++)
            lhs.add(str[i]);

        // print string after deleting duplicate elements
        for (var ch of lhs)
            document.write(ch);
    }

    /* Driver program to test removeDuplicates */

        var str = "geeksforgeeks";
        removeDuplicates(str);

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
geksfor
```

**时间复杂度:** O(n)

**要点:**

*   方法 2 没有将字符保持为原始字符串，但是方法 4 保持了。
*   假设输入字符串中可能的字符数是 256。应该相应地改变字符数。
*   calloc()代替 malloc()用于计数数组(count)的内存分配，以将分配的内存初始化为“\0”。也可以使用 malloc()后跟 memset()。
*   如果给定数组中整数的范围，上述算法也适用于整数数组输入。一个示例问题是，假设输入数组只包含 1000 到 1100 之间的整数，则找出输入数组中出现的最大数字

**方法 5** (使用**索引 Of()** 方法):
T5】先决条件:T7】Java**索引 Of()** 方法

## C++

```
// C++ program to create a unique string
#include <bits/stdc++.h>
using namespace std;

// Function to make the string unique
string unique(string s)
{
    string str;
    int len = s.length();

    // loop to traverse the string and
    // check for repeating chars using
    // IndexOf() method in Java
    for(int i = 0; i < len; i++)
    {

        // character at i'th index of s
        char c = s[i];

        // If c is present in str, it returns
        // the index of c, else it returns npos
        auto found = str.find(c);
        if (found == std::string::npos) 
        {

            // Adding c to str if npos is returned
            str += c;
        }
    }
    return str;
}

// Driver code
int main()
{

    // Input string with repeating chars
    string s = "geeksforgeeks";

    cout << unique(s) << endl;
}

// This code is contributed by nirajgusain5
```

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

## 蟒蛇 3

```
# Python 3 program to create a unique string

# Function to make the string unique

def unique(s):

    st = ""
    length = len(s)

    # loop to traverse the string and
    # check for repeating chars using
    # IndexOf() method in Java
    for i in range(length):

        # character at i'th index of s
        c = s[i]

        # if c is present in str, it returns
        # the index of c, else it returns - 1
        # print(st.index(c))
        if c not in st:
            # adding c to str if -1 is returned
            st += c

    return st

# Driver code
if __name__ == "__main__":

    # Input string with repeating chars
    s = "geeksforgeeks"

    print(unique(s))

    # This code is contributed by ukasp.
```

## C#

```
// C# program to create a unique string
using System; 

public class IndexOf 
{

    // Function to make the string unique
    public static String unique(String s)
    {
        String str = "";
        int len = s.Length;

        // loop to traverse the string and
        // check for repeating chars using
        // IndexOf() method in Java
        for (int i = 0; i < len; i++) 
        {
            // character at i'th index of s
            char c = s[i];

            // if c is present in str, it returns
            // the index of c, else it returns -1
            if (str.IndexOf(c) < 0)
            {
                // adding c to str if -1 is returned
                str += c;
            }
        }

        return str;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Input string with repeating chars
        String s = "geeksforgeeks";

        Console.WriteLine(unique(s));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to create a unique string

    // Function to make the string unique
    function unique(s)
    {
        let str = "";
        let len = s.length;

        // loop to traverse the string and
        // check for repeating chars using
        // IndexOf() method in Java
        for (let i = 0; i < len; i++)
        {
            // character at i'th index of s
            let c = s[i];

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

      // Input string with repeating chars
    let s = "geeksforgeeks";

    document.write(unique(s));

</script>
```

**输出:**

```
geksfor
```

感谢 [**debjitdbb**](https://auth.geeksforgeeks.org/user/debjitdbb/articles) 提出这个方法。

**方法 6** (使用**无序 _ 映射 STL** 方法):
**先决条件:** [无序 _ 映射 STL C++方法](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)

## C++

```
// C++ program to create a unique string using unordered_map

/* access time in unordered_map on is O(1) generally if no collisions occur 
and therefore it helps us check if an element exists in a string in O(1) 
time complexity with constant space. */

#include <bits/stdc++.h> 
using namespace std; 
char* removeDuplicates(char *s,int n){
  unordered_map<char,int> exists;
  int index = 0; 
  for(int i=0;i<n;i++){
    if(exists[s[i]]==0)
    {
      s[index++] = s[i];
      exists[s[i]]++;
    }
  }
  return s;
}

//driver code
int main(){
  char s[] = "geeksforgeeks";
  int n = sizeof(s)/sizeof(s[0]);
  cout<<removeDuplicates(s,n)<<endl;
  return 0;
}
```

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

## C#

```
// C# program to create a unique String using unordered_map

/* access time in unordered_map on is O(1) generally if no collisions occur 
and therefore it helps us check if an element exists in a String in O(1) 
time complexity with constant space. */
using System;
using System.Collections.Generic;

public class GFG{ 
static char[] removeDuplicates(char []s,int n){
  Dictionary<char,int> exists = new Dictionary<char, int>();

  String st = "";
  for(int i = 0; i < n; i++){
    if(!exists.ContainsKey(s[i]))
    {
      st += s[i];
      exists.Add(s[i], 1);
    }
  }
  return st.ToCharArray();
}

// driver code
public static void Main(String[] args){
  char []s = "geeksforgeeks".ToCharArray();
  int n = s.Length;
  Console.Write(removeDuplicates(s,n));
}
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript program to create a unique String using unordered_map

/* access time in unordered_map on is O(1) generally if no collisions occur 
and therefore it helps us check if an element exists in a String in O(1) 
time complexity with constant space. */
     function removeDuplicates( s , n) {
        var exists = new Map();

        var st = "";
        for (var i = 0; i < n; i++) {
            if (!exists.has(s[i])) {
                st += s[i];
                exists.set(s[i], 1);
            }
        }
        return st;
    }

    // driver code

        var s = "geeksforgeeks";
        var n = s.length;
        document.write(removeDuplicates(s, n));
// This code contributed by umadevi9616
</script>
```

**输出:**

```
geksfor
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
谢谢，**艾伦·詹姆斯·维诺伊**提出这个方法。