# 找到重复的和丢失的 | 3 种新增方法

> 原文： [https://www.geeksforgeeks.org/find-a-repeating-and-a-missing-number/](https://www.geeksforgeeks.org/find-a-repeating-and-a-missing-number/)

给定大小为`n`的未排序数组。 数组元素的范围是 1 到`n`。 集合`{1, 2, …, n}`中的一个数字丢失，并且一个数字在数组中出现两次。 找到这两个数字。

**示例**：

```

Input: arr[] = {3, 1, 3}
Output: Missing = 2, Repeating = 3
Explanation: In the array, 
2 is missing and 3 occurs twice 

Input: arr[] = {4, 3, 6, 2, 1, 1}
Output: Missing = 5, Repeating = 1

```



**以下是解决问题的各种方法**：

**方法 1（使用字符串）**：

**方法**：

1.  对输入数组进行排序。

2.  遍历数组并检查是否丢失和重复。

**时间复杂度**：`O(nLogn)`。

感谢 **LoneShadow** 提出了此方法。

**方法 2（使用计数数组）**：

**方法**：

1.  创建一个大小为`n`的临时数组`temp[]`，所有初始值均为 0。

2.  遍历输入数组`arr[]`，并对每个`arr[i]`执行以下操作：

    *   `if(temp[arr [i]] == 0) temp[arr[i]] = 1;`。

    *   `if(temp[arr [i]] == 1)`输出`arr[i]`。

3.  遍历`temp[]`并输出值为 0 的数组元素（这是缺少的元素）

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。

**方法 3（使用元素作为索引并标记访问过的位置）**：

**方法**：

遍历数组。 遍历时，将每个元素的绝对值用作索引，并使该索引处的值为负，以将其标记为已访问。 如果某些内容已标记为否，则为重复元素。 要查找丢失的内容，请再次遍历数组并寻找一个正值。

## C++ 

```

// C++ program to Find the repeating 
// and missing elements 

#include <bits/stdc++.h> 
using namespace std; 

void printTwoElements(int arr[], int size) 
{ 
    int i; 
    cout << " The repeating element is "; 

    for (i = 0; i < size; i++) { 
        if (arr[abs(arr[i]) - 1] > 0) 
            arr[abs(arr[i]) - 1] = -arr[abs(arr[i]) - 1]; 
        else
            cout << abs(arr[i]) << "\n"; 
    } 

    cout << "and the missing element is "; 
    for (i = 0; i < size; i++) { 
        if (arr[i] > 0) 
            cout << (i + 1); 
    } 
} 

/* Driver code */
int main() 
{ 
    int arr[] = { 7, 3, 4, 5, 5, 6, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printTwoElements(arr, n); 
} 

// This code is contributed by Shivi_Aggarwal 

```

## C

```

// C program to Find the repeating 
// and missing elements 

#include <stdio.h> 
#include <stdlib.h> 

void printTwoElements(int arr[], int size) 
{ 
    int i; 
    printf("\n The repeating element is"); 

    for (i = 0; i < size; i++) { 
        if (arr[abs(arr[i]) - 1] > 0) 
            arr[abs(arr[i]) - 1] = -arr[abs(arr[i]) - 1]; 
        else
            printf(" %d ", abs(arr[i])); 
    } 

    printf("\nand the missing element is "); 
    for (i = 0; i < size; i++) { 
        if (arr[i] > 0) 
            printf("%d", i + 1); 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 7, 3, 4, 5, 5, 6, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printTwoElements(arr, n); 
    return 0; 
} 

```

## Java

```

// Java program to Find the repeating 
// and missing elements 

import java.io.*; 

class GFG { 

    static void printTwoElements(int arr[], int size) 
    { 
        int i; 
        System.out.print("The repeating element is "); 

        for (i = 0; i < size; i++) { 
            int abs_val = Math.abs(arr[i]); 
            if (arr[abs_val - 1] > 0) 
                arr[abs_val - 1] = -arr[abs_val - 1]; 
            else
                System.out.println(abs_val); 
        } 

        System.out.print("And the missing element is "); 
        for (i = 0; i < size; i++) { 
            if (arr[i] > 0) 
                System.out.println(i + 1); 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 7, 3, 4, 5, 5, 6, 2 }; 
        int n = arr.length; 
        printTwoElements(arr, n); 
    } 
} 

// This code is contributed by Gitanjali 

```

## Python3

```

# Python3 code to Find the repeating  
# and the missing elements 

def printTwoElements( arr, size): 
    for i in range(size): 
        if arr[abs(arr[i])-1] > 0: 
            arr[abs(arr[i])-1] = -arr[abs(arr[i])-1] 
        else: 
            print("The repeating element is", abs(arr[i])) 

    for i in range(size): 
        if arr[i]>0: 
            print("and the missing element is", i + 1) 

# Driver program to test above function */ 
arr = [7, 3, 4, 5, 5, 6, 2] 
n = len(arr) 
printTwoElements(arr, n) 

# This code is contributed by "Abhishek Sharma 44" 

```

## C# 

```

// C# program to Find the repeating 
// and missing elements 

using System; 

class GFG { 
    static void printTwoElements(int[] arr, int size) 
    { 
        int i; 
        Console.Write("The repeating element is "); 

        for (i = 0; i < size; i++) { 
            int abs_val = Math.Abs(arr[i]); 
            if (arr[abs_val - 1] > 0) 
                arr[abs_val - 1] = -arr[abs_val - 1]; 
            else
                Console.WriteLine(abs_val); 
        } 

        Console.Write("And the missing element is "); 
        for (i = 0; i < size; i++) { 
            if (arr[i] > 0) 
                Console.WriteLine(i + 1); 
        } 
    } 

    // Driver program 
    public static void Main() 
    { 
        int[] arr = { 7, 3, 4, 5, 5, 6, 2 }; 
        int n = arr.Length; 
        printTwoElements(arr, n); 
    } 
} 
// This code is contributed by Sam007 

```

## PHP

```

<?php 
// PHP program to Find the repeating 
// and missing elements 

function printTwoElements($arr, $size) 
{ 
    $i; 
    echo "The repeating element is", " "; 

    for($i = 0; $i < $size; $i++) 
    { 
        if($arr[abs($arr[$i]) - 1] > 0) 
            $arr[abs($arr[$i]) - 1] =  
            - $arr[abs($arr[$i]) - 1]; 
        else
            echo ( abs($arr[$i])); 
    } 

    echo "\nand the missing element is "; 
    for($i = 0; $i < $size; $i++) 
    { 
        if($arr[$i] > 0) 
            echo($i + 1); 
    } 
} 

    // Driver Code 
    $arr = array(7, 3, 4, 5, 5, 6, 2); 
    $n = count($arr); 
    printTwoElements($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
The repeating element is 5
and the missing element is 1

```

**时间复杂度**：`O(n)`。

感谢 **Manish Mishra** 提出了此方法。

**方法 4（创建两个方程）**：

**方法**：

1.  令`x`为缺失元素，`y`为重复元素。

2.  使用公式获得所有数字的总和`S = n (n + 1) / 2 – x + y`。

3.  使用公式获得所有数字的乘积`P = 1 * 2 * 3 * ... * n * y / x`。

4.  上面的两个步骤为我们提供了两个方程，我们可以求解方程并获得`x`和`y`的值。

**时间复杂度**：`O(n)`。

感谢**消失了**提出了这种解决方案。

**注意**：当我们计算所有数组元素的乘积和总和时，此方法可能导致算术溢出。

**方法 5（使用 XOR）**：

**方法**：

*   令`x`和`y`为所需的输出元素。

*   计算所有数组元素的 XOR。

    `xor1 = arr[0] ^ arr[1] ^ arr[2] ..... arr[n-1]`

*   将结果与 1 到`n`之间的所有数字进行 XOR 运算。

    `xor1 = xor1 ^ 1 ^ 2 ^ ..... ^ n`

*   在结果`xor1`中，除`x`和`y`外，所有元素都将彼此作废。 `xor1`中设置的所有位都将设置为`x`或`y`。 因此，如果我们取`xor1`的任何设置位（我们在代码中选择了最右边的设置位），然后将数组的元素分为两组-一组具有相同位的元素，而另一组未设置相同的位。 这样，我们将在一组中获得`x`，在另一组中获得`y`。 现在，如果我们对第一个集合中的所有元素进行 XOR，我们将得到`x`，而在其他集合中进行同样的操作，我们将得到`y`。

下面是上述方法的实现：

## C++

```
// C++ program to Find the repeating 
// and missing elements 
  
#include <bits/stdc++.h> 
using namespace std; 
  
/* The output of this function is stored at 
*x and *y */
void getTwoElements(int arr[], int n, 
                    int* x, int* y) 
{ 
    /* Will hold xor of all elements  
    and numbers from 1 to n */
    int xor1; 
  
    /* Will have only single set bit of xor1 */
    int set_bit_no; 
  
    int i; 
    *x = 0; 
    *y = 0; 
  
    xor1 = arr[0]; 
  
    /* Get the xor of all array elements */
    for (i = 1; i < n; i++) 
        xor1 = xor1 ^ arr[i]; 
  
    /* XOR the previous result with numbers  
    from 1 to n*/
    for (i = 1; i <= n; i++) 
        xor1 = xor1 ^ i; 
  
    /* Get the rightmost set bit in set_bit_no */
    set_bit_no = xor1 & ~(xor1 - 1); 
  
    /* Now divide elements into two  
    sets by comparing a rightmost set 
    bit of xor1 with the bit at the same  
    position in each element. Also,  
    get XORs of two sets. The two 
    XORs are the output elements.  
    The following two for loops  
    serve the purpose */
    for (i = 0; i < n; i++) { 
        if (arr[i] & set_bit_no) 
            /* arr[i] belongs to first set */
            *x = *x ^ arr[i]; 
  
        else
            /* arr[i] belongs to second set*/
            *y = *y ^ arr[i]; 
    } 
    for (i = 1; i <= n; i++) { 
        if (i & set_bit_no) 
            /* i belongs to first set */
            *x = *x ^ i; 
  
        else
            /* i belongs to second set*/
            *y = *y ^ i; 
    } 
  
    /* *x and *y hold the desired 
        output elements */
} 
  
/* Driver code */
int main() 
{ 
    int arr[] = { 1, 3, 4, 5, 5, 6, 2 }; 
    int* x = (int*)malloc(sizeof(int)); 
    int* y = (int*)malloc(sizeof(int)); 
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    getTwoElements(arr, n, x, y); 
    cout << " The missing element is " << *x << " and the repeating"
         << " number is " << *y; 
    getchar(); 
} 
  
// This code is contributed by Code_Mech
```

## C

```
// C program to Find the repeating 
// and missing elements 
  
#include <stdio.h> 
#include <stdlib.h> 
  
/* The output of this function is stored at 
   *x and *y */
void getTwoElements(int arr[], int n, int* x, int* y) 
{ 
    /* Will hold xor of all elements and numbers  
       from 1 to n */
    int xor1; 
  
    /* Will have only single set bit of xor1 */
    int set_bit_no; 
  
    int i; 
    *x = 0; 
    *y = 0; 
  
    xor1 = arr[0]; 
  
    /* Get the xor of all array elements */
    for (i = 1; i < n; i++) 
        xor1 = xor1 ^ arr[i]; 
  
    /* XOR the previous result with numbers  
       from 1 to n*/
    for (i = 1; i <= n; i++) 
        xor1 = xor1 ^ i; 
  
    /* Get the rightmost set bit in set_bit_no */
    set_bit_no = xor1 & ~(xor1 - 1); 
  
    /* Now divide elements in two sets by comparing  
    rightmost set bit of xor1 with bit at same  
    position in each element. Also, get XORs of two  
    sets. The two XORs are the output elements. The 
    following two for loops serve the purpose */
    for (i = 0; i < n; i++) { 
        if (arr[i] & set_bit_no) 
            /* arr[i] belongs to first set */
            *x = *x ^ arr[i]; 
  
        else
            /* arr[i] belongs to second set*/
            *y = *y ^ arr[i]; 
    } 
    for (i = 1; i <= n; i++) { 
        if (i & set_bit_no) 
            /* i belongs to first set */
            *x = *x ^ i; 
  
        else
            /* i belongs to second set*/
            *y = *y ^ i; 
    } 
  
    /* *x and *y hold the desired output elements */
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr[] = { 1, 3, 4, 5, 5, 6, 2 }; 
    int* x = (int*)malloc(sizeof(int)); 
    int* y = (int*)malloc(sizeof(int)); 
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    getTwoElements(arr, n, x, y); 
    printf(" The missing element is %d"
           " and the repeating number"
           " is %d", 
           *x, *y); 
    getchar(); 
}
```

## Java

```
// Java program to Find the repeating 
// and missing elements 
  
import java.io.*; 
  
class GFG { 
    static int x, y; 
  
    static void getTwoElements(int arr[], int n) 
    { 
        /* Will hold xor of all elements 
       and numbers from 1 to n  */
        int xor1; 
  
        /* Will have only single set bit of xor1 */
        int set_bit_no; 
  
        int i; 
        x = 0; 
        y = 0; 
  
        xor1 = arr[0]; 
  
        /* Get the xor of all array elements  */
        for (i = 1; i < n; i++) 
            xor1 = xor1 ^ arr[i]; 
  
        /* XOR the previous result with numbers from  
       1 to n*/
        for (i = 1; i <= n; i++) 
            xor1 = xor1 ^ i; 
  
        /* Get the rightmost set bit in set_bit_no */
        set_bit_no = xor1 & ~(xor1 - 1); 
  
        /* Now divide elements into two sets by comparing 
    rightmost set bit of xor1 with the bit at the same  
    position in each element. Also, get XORs of two 
    sets. The two XORs are the output elements. The  
    following two for loops serve the purpose */
        for (i = 0; i < n; i++) { 
            if ((arr[i] & set_bit_no) != 0) 
                /* arr[i] belongs to first set */
                x = x ^ arr[i]; 
  
            else
                /* arr[i] belongs to second set*/
                y = y ^ arr[i]; 
        } 
        for (i = 1; i <= n; i++) { 
            if ((i & set_bit_no) != 0) 
                /* i belongs to first set */
                x = x ^ i; 
  
            else
                /* i belongs to second set*/
                y = y ^ i; 
        } 
  
        /* *x and *y hold the desired output elements */
    } 
    /* Driver program to test above function */
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 3, 4, 5, 1, 6, 2 }; 
  
        int n = arr.length; 
        getTwoElements(arr, n); 
        System.out.println(" The missing element is  "
                           + x + "and the "
                           + "repeating number is "
                           + y); 
    } 
} 
  
// This code is contributed by Gitanjali.
```

## Python3

```
# Python3 program to find the repeating  
# and missing elements  
  
# The output of this function is stored  
# at x and y  
def getTwoElements(arr, n): 
      
    global x, y 
    x = 0
    y = 0
      
    # Will hold xor of all elements  
    # and numbers from 1 to n  
    xor1 = arr[0] 
      
    # Get the xor of all array elements 
    for i in range(1, n): 
        xor1 = xor1 ^ arr[i] 
          
    # XOR the previous result with numbers  
    # from 1 to n 
    for i in range(1, n + 1): 
        xor1 = xor1 ^ i 
      
    # Will have only single set bit of xor1 
    set_bit_no = xor1 & ~(xor1 - 1) 
      
    # Now divide elements into two  
    # sets by comparing a rightmost set  
    # bit of xor1 with the bit at the same  
    # position in each element. Also,  
    # get XORs of two sets. The two  
    # XORs are the output elements.  
    # The following two for loops  
    # serve the purpose 
    for i in range(n): 
        if (arr[i] & set_bit_no) != 0: 
              
            # arr[i] belongs to first set 
            x = x ^ arr[i] 
        else: 
              
            # arr[i] belongs to second set 
            y = y ^ arr[i] 
              
    for i in range(1, n + 1): 
        if (i & set_bit_no) != 0: 
              
            # i belongs to first set 
            x = x ^ i 
        else: 
              
            # i belongs to second set 
            y = y ^ i  
          
    # x and y hold the desired  
    # output elements  
      
# Driver code 
arr = [ 1, 3, 4, 5, 5, 6, 2 ] 
n = len(arr) 
      
getTwoElements(arr, n) 
  
print("The missing element is", x, 
      "and the repeating number is", y) 
      
# This code is contributed by stutipathak31jan
```

## C#

```
// C# program to Find the repeating 
// and missing elements 
  
using System; 
  
class GFG { 
    static int x, y; 
  
    static void getTwoElements(int[] arr, int n) 
    { 
        /* Will hold xor of all elements 
        and numbers from 1 to n */
        int xor1; 
  
        /* Will have only single set bit of xor1 */
        int set_bit_no; 
  
        int i; 
        x = 0; 
        y = 0; 
  
        xor1 = arr[0]; 
  
        /* Get the xor of all array elements */
        for (i = 1; i < n; i++) 
            xor1 = xor1 ^ arr[i]; 
  
        /* XOR the previous result with numbers from  
        1 to n*/
        for (i = 1; i <= n; i++) 
            xor1 = xor1 ^ i; 
  
        /* Get the rightmost set bit in set_bit_no */
        set_bit_no = xor1 & ~(xor1 - 1); 
  
        /* Now divide elements in two sets by comparing 
        rightmost set bit of xor1 with bit at same  
        position in each element. Also, get XORs of two 
        sets. The two XORs are the output elements.The  
        following two for loops serve the purpose */
        for (i = 0; i < n; i++) { 
            if ((arr[i] & set_bit_no) != 0) 
  
                /* arr[i] belongs to first set */
                x = x ^ arr[i]; 
  
            else
  
                /* arr[i] belongs to second set*/
                y = y ^ arr[i]; 
        } 
        for (i = 1; i <= n; i++) { 
            if ((i & set_bit_no) != 0) 
  
                /* i belongs to first set */
                x = x ^ i; 
  
            else
  
                /* i belongs to second set*/
                y = y ^ i; 
        } 
  
        /* *x and *y hold the desired output elements */
    } 
  
    // Driver program 
    public static void Main() 
    { 
        int[] arr = { 1, 3, 4, 5, 1, 6, 2 }; 
  
        int n = arr.Length; 
        getTwoElements(arr, n); 
        Console.Write(" The missing element is "
                      + x + "and the "
                      + "repeating number is "
                      + y); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```
<?php 
// PHP program to Find the repeating 
// and missing elements 
  
function getTwoElements(&$arr, $n) 
{ 
  
    /* Will hold xor of all elements 
    and numbers from 1 to n */
    $xor1; 
  
    /* Will have only single set bit of xor1 */
    $set_bit_no; 
  
    $i; 
    $x = 0; 
    $y = 0; 
  
    $xor1 = $arr[0]; 
  
    /* Get the xor of all array elements */
    for ($i = 1; $i < $n; $i++) 
        $xor1 = $xor1 ^ $arr[$i]; 
  
    /* XOR the previous result with numbers  
    from 1 to n*/
    for ($i = 1; $i <= $n; $i++) 
        $xor1 = $xor1 ^ $i; 
  
    /* Get the rightmost set bit in set_bit_no */
    $set_bit_no = $xor1 & ~($xor1 - 1); 
  
    /* Now divide elements in two sets by comparing 
    rightmost set bit of xor1 with bit at same  
    position in each element. Also, get XORs of two 
    sets. The two XORs are the output elements.The  
    following two for loops serve the purpose */
    for ($i = 0; $i < $n; $i++)  
    { 
        if (($arr[$i] & $set_bit_no) != 0) 
          
            /* arr[i] belongs to first set */
            $x = $x ^ $arr[$i]; 
  
        else
          
            /* arr[i] belongs to second set*/
            $y = $y ^ $arr[$i]; 
    } 
      
    for ($i = 1; $i <= $n; $i++) 
    { 
        if (($i & $set_bit_no) != 0) 
          
            /* i belongs to first set */
            $x = $x ^ $i; 
  
        else
          
            /* i belongs to second set*/
            $y = $y ^ $i; 
    } 
  
    /* *x and *y hold the desired output elements */
    echo("The missing element is " . $x .  
         " and the repeating number is " . $y); 
} 
  
// Driver Code 
$arr = array( 1, 3, 4, 5, 1, 6, 2 ); 
$n = sizeof($arr); 
getTwoElements($arr, $n); 
  
// This code is contributed by Code_Mech
```

输出：

```
The missing element is 7 and the repeating number is 5
```

时间复杂度：`O(n)`。

此方法不会导致溢出，但不会告诉您哪一个发生了两次而哪一个丢失了。 我们可以再增加一个步骤，以检查缺少的一个和重复的一个。 这很容易在`O(n)`时间内完成。

方法 6（使用映射）：

方法：

此方法涉及在映射的帮助下创建哈希表。 在这种情况下，元素被映射到其自然索引。 在此过程中，如果一个元素被映射两次，那么它就是重复元素。 如果元素的映射不存在，则它是缺少的元素。

下面是上述方法的实现：

## Java

```
// Java program to find the 
// repeating and missing elements 
// using Maps 
  
import java.util.*; 
  
public class Test1 { 
  
    public static void main(String[] args) 
    { 
  
        int[] arr = { 4, 3, 6, 2, 1, 1 }; 
  
        Map<Integer, Boolean> numberMap 
            = new HashMap<>(); 
  
        int max = arr.length; 
  
        for (Integer i : arr) { 
  
            if (numberMap.get(i) == null) { 
                numberMap.put(i, true); 
            } 
            else { 
                System.out.println("Repeating = " + i); 
            } 
        } 
        for (int i = 1; i <= max; i++) { 
            if (numberMap.get(i) == null) { 
                System.out.println("Missing = " + i); 
            } 
        } 
    } 
}
```

## Python3

```
# Python3 program to find the  
# repeating and missing elements  
# using Maps 
def main(): 
      
    arr = [ 4, 3, 6, 2, 1, 1 ] 
      
    numberMap = {} 
      
    max = len(arr) 
    for i in arr: 
        if not i in numberMap: 
            numberMap[i] = True
              
        else: 
            print("Repeating =", i) 
      
    for i in range(1, max + 1): 
        if not i in numberMap: 
            print("Missing =", i) 
main() 
  
# This code is contributed by stutipathak31jan
```

## C#

```
// C# program to find the 
// repeating and missing elements 
// using Maps 
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
    public static void Main(String[] args) 
    { 
        int[] arr = { 4, 3, 6, 2, 1, 1 }; 
  
        Dictionary<int, Boolean> numberMap = 
                   new Dictionary<int, Boolean>(); 
  
        int max = arr.Length; 
  
        foreach (int i in arr)  
        { 
            if (!numberMap.ContainsKey(i))  
            { 
                numberMap.Add(i, true); 
            } 
            else 
            { 
                Console.WriteLine("Repeating = " + i); 
            } 
        } 
        for (int i = 1; i <= max; i++)  
        { 
            if (!numberMap.ContainsKey(i))  
            { 
                Console.WriteLine("Missing = " + i); 
            } 
        } 
    } 
} 
  
// This code is contributed by PrinciRaj1992
```

输出：

```
Repeating = 1
Missing = 5
```

方法 7（使用和和平方和制作两个方程式）：

方法：

1.  令`x`为缺失元素，`y`为重复元素。
2.  令`N`为数组的大小。
3.  使用公式`S = N(N + 1) / 2`获得所有数字的总和。
4.  使用公式`SumSq = N(N + 1)(2N + 1)/ 6`获取所有数字的乘积。
5.  从`i = 1…N`循环遍历。
6.  `S -= A [i]`。
7.  `SumSq -= (A[i] * A[i])`。
8.  它将给出两个方程：

    ```
    x-y = S – (1)
    x ^ 2 – y ^ 2 = SumSq
    x + y = (SumSq / S) – (2)
    ```

时间复杂度：`O(n)`。

## C++

```
#include <bits/stdc++.h>  
  
using namespace std; 
  
vector<int>repeatedNumber(const vector<int> &A) { 
    long long int len = A.size(); 
    long long int Sum_N = (len * (len+1) ) /2, Sum_NSq = (len * (len +1) *(2*len +1) )/6; 
    long long int missingNumber=0, repeating=0; 
      
    for(int i=0;i<A.size(); i++){ 
       Sum_N -= (long long int)A[i]; 
       Sum_NSq -= (long long int)A[i]*(long long int)A[i]; 
    } 
      
    missingNumber = (Sum_N + Sum_NSq/Sum_N)/2; 
    repeating= missingNumber - Sum_N; 
    vector <int> ans; 
    ans.push_back(repeating); 
    ans.push_back(missingNumber); 
    return ans; 
      
} 
  
  
int main(void){ 
        std::vector<int> v = {4, 3, 6, 2, 1, 6,7}; 
    vector<int> res = repeatedNumber(v); 
    for(int x: res){ 
        cout<< x<<"  "; 
    } 
    cout<<endl; 
}
```

## Java

```
import java.util.*; 
  
class GFG  
{ 
    static Vector<Integer> repeatedNumber(int[] A)  
    { 
        int len = A.length; 
        int Sum_N = (len * (len + 1)) / 2; 
        int Sum_NSq = (len * (len + 1) *  
                         (2 * len + 1)) / 6; 
        int missingNumber = 0, repeating = 0; 
  
        for (int i = 0; i < A.length; i++)  
        { 
            Sum_N -= A[i]; 
            Sum_NSq -= A[i] * A[i]; 
        } 
  
        missingNumber = (Sum_N + Sum_NSq /  
                                 Sum_N) / 2; 
        repeating = missingNumber - Sum_N; 
        Vector<Integer> ans = new Vector<>(); 
        ans.add(repeating); 
        ans.add(missingNumber); 
        return ans; 
    } 
  
    // Driver Code 
    public static void main(String[] args)  
    { 
        int[] v = { 4, 3, 6, 2, 1, 6, 7 }; 
        Vector<Integer> res = repeatedNumber(v); 
        for (int x : res)  
        { 
            System.out.print(x + " "); 
        } 
    } 
} 
  
// This code is contributed by Rajput-Ji
```

## Python3

```
def repeatedNumber(A): 
      
    length = len(A) 
    Sum_N = (length * (length + 1)) // 2
    Sum_NSq = ((length * (length + 1) * 
                     (2 * length + 1)) // 6) 
      
    missingNumber, repeating = 0, 0
      
    for i in range(len(A)): 
        Sum_N -= A[i] 
        Sum_NSq -= A[i] * A[i] 
          
    missingNumber = (Sum_N + Sum_NSq // 
                             Sum_N) // 2
    repeating = missingNumber - Sum_N 
      
    ans = [] 
    ans.append(repeating) 
    ans.append(missingNumber) 
      
    return ans 
  
# Driver code 
v = [ 4, 3, 6, 2, 1, 6, 7 ] 
res = repeatedNumber(v) 
  
for i in res: 
    print(i, end = " ") 
  
# This code is contributed by stutipathak31jan
```

## C#

```
using System; 
using System.Collections.Generic; 
  
class GFG  
{ 
    static List<int> repeatedNumber(int[] A)  
    { 
        int len = A.Length; 
        int Sum_N = (len * (len + 1)) / 2; 
        int Sum_NSq = (len * (len + 1) *  
                        (2 * len + 1)) / 6; 
        int missingNumber = 0, repeating = 0; 
  
        for (int i = 0; i < A.Length; i++)  
        { 
            Sum_N -= A[i]; 
            Sum_NSq -= A[i] * A[i]; 
        } 
  
        missingNumber = (Sum_N + Sum_NSq /  
                                 Sum_N) / 2; 
        repeating = missingNumber - Sum_N; 
        List<int> ans = new List<int>(); 
        ans.Add(repeating); 
        ans.Add(missingNumber); 
        return ans; 
    } 
  
    // Driver Code 
    public static void Main(String[] args)  
    { 
        int[] v = { 4, 3, 6, 2, 1, 6, 7 }; 
        List<int> res = repeatedNumber(v); 
        foreach (int x in res)  
        { 
            Console.Write(x + " "); 
        } 
    } 
} 
  
// This code is contributed by PrinciRaj1992
```

输出：

```
6 5 
```
