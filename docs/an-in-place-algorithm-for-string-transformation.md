# 字符串转换的原位算法

> 原文:[https://www . geesforgeks . org/字符串转换就地算法/](https://www.geeksforgeeks.org/an-in-place-algorithm-for-string-transformation/)

给定一个字符串，将所有位置均匀的元素移动到字符串的末尾。移动元素时，保持所有偶数位置和奇数位置元素的相对顺序相同。例如，如果给定的字符串是“a1b2c3d 4e 5f 6 g7h 8i 9j 2k 3l 4”，则就地并以 O(n)时间复杂度将其转换为“abcdefghijklm1234567891234”。

以下是步骤:
**1。**剪切出 3^k + 1 形式大小最大的前缀子串。在这一步中，我们找到最大的非负整数 k，使得 3^k+1 小于或等于 n(字符串的长度)
**2。**从索引 1、3、9……开始，对这个子串应用循环前导迭代算法(下面已经讨论过了)。循环前导迭代算法将该子串的所有项目移动到它们的正确位置，即所有字母移动到该子串的左半部分，所有数字移动到该子串的右半部分。
**3。**使用步骤#1 和#2 递归处理剩余的子串。
**4。**现在，我们只需要将处理后的子串连接在一起。从任意一端开始(比如从左开始)，选择两个子字符串，应用以下步骤:
…。 **4.1** 反转第一个子串的后半部分。
…。 **4.2** 反转第二子串的前半部分。
…。 **4.3** 将第一子串的后半部分和第二子串的前半部分一起反转。
T22【5。重复步骤#4，直到所有子串连接。这类似于 k-way 合并，其中第一个子字符串与第二个子字符串连接。结果与第三个合并，以此类推。

让我们用一个例子来理解它:

请注意，在下面的示例中，我们使用了类似 10、11 和 12 的值。仅将这些值视为单个字符。这些值用于提高可读性。

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
a 1 b 2 c 3 d 4 e 5 f  6  g  7  h  8  i  9  j  10 k  11 l  12 m  13
```

在分解成 3^k + 1 形式的大小后，形成两个子串，每个子串的大小为 10。第三子串由尺寸 4 形成，第四子串由尺寸 2 形成。

```
0 1 2 3 4 5 6 7 8 9         
a 1 b 2 c 3 d 4 e 5         

10 11 12 13 14 15 16 17 18 19          
f  6  g  7  h  8  i  9  j  10           

20 21 22 23 
k  11 l  12 

24 25
m  13
```

将循环前导迭代算法应用于第一个子串后:

```
0 1 2 3 4 5 6 7 8 9          
a b c d e 1 2 3 4 5          

10 11 12 13 14 15 16 17 18 19          
f  6  g  7  h  8  i  9  j  10 

20 21 22 23 
k  11 l  12 

24 25
m  13
```

将循环前导迭代算法应用于第二子串后:

```
0 1 2 3 4 5 6 7 8 9          
a b c d e 1 2 3 4 5          

10 11 12 13 14 15 16 17 18 19           
f  g  h  i  j  6  7  8  9  10 

20 21 22 23 
k  11 l  12 

24 25
m 13
```

将循环前导迭代算法应用于第三个子串后:

```
0 1 2 3 4 5 6 7 8 9          
a b c d e 1 2 3 4 5          

10 11 12 13 14 15 16 17 18 19            
f  g  h  i  j  6  7  8  9  10

20 21 22 23 
k  l  11 12 

24 25
m  13
```

将循环前导迭代算法应用于第四个子串后:

```
0 1 2 3 4 5 6 7 8 9  
a b c d e 1 2 3 4 5  

10 11 12 13 14 15 16 17 18 19             
f  g  h  i  j  6  7  8  9  10   

20 21 22 23 
k  l  11 12 

24 25
m  13
```

*连接第一子串和第二子串:*
1。第一子串的后半部分和第二子串的前半部分颠倒。

```
0 1 2 3 4 5 6 7 8 9          
a b c d e 5 4 3 2 1            <--------- First Sub-string  

10 11 12 13 14 15 16 17 18 19             
j  i  h  g  f  6  7  8  9  10  <--------- Second Sub-string  

20 21 22 23 
k  l  11 12 

24 25
m  13
```

2.第一子串的后半部分和第二子串的前半部分一起反转(它们被合并，即现在只有三个子串)。

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
a b c d e f g h i j 1  2  3  4  5  6  7  8  9  10

20 21 22 23 
k  l  11 12 

24 25
m  13
```

连接第一子串和第二子串:
1。第一子串的后半部分和第二子串的前半部分颠倒。

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
a b c d e f g h i j 10 9  8  7  6  5  4  3  2  1 <--------- First Sub-string  

20 21 22 23 
l  k  11 12                                      <--------- Second Sub-string

24 25
m  13
```

2.第一子串的后半部分和第二子串的前半部分一起反转(它们被合并，即现在只有两个子串)。

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23  
a b c d e f g h i j k  l  1  2  3  4  5  6  7  8  9  10 11 12  

24 25
m  13 
```

*连接第一子串和第二子串:*
1。第一子串的后半部分和第二子串的前半部分颠倒。

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 
a b c d e f g h i j k  l  12 11 10 9  8  7  6  5  4  3  2  1 <----- First Sub-string

24 25
m  13   <----- Second Sub-string 
```

2.第一子串的后半部分和第二子串的前半部分一起反转(它们被合并，即现在只有一个子串)。

```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
a b c d e f g h i j k  l  m  1  2  3  4  5  6  7  8  9  10 11 12 13
```

由于所有子字符串都已连接在一起，我们就完成了。

**循环领导者迭代算法是如何工作的？**
让我们用一个例子来理解它:

```
Input:
0 1 2 3 4 5 6 7 8 9
a 1 b 2 c 3 d 4 e 5

Output:
0 1 2 3 4 5 6 7 8 9 
a b c d e 1 2 3 4 5

Old index    New index
0        0
1        5
2        1
3        6
4        2
5        7
6        3
7        8
8        4
9        9
```

设 len 为弦的长度。如果我们仔细观察，我们发现新的指数由下面的公式给出:

```
if( oldIndex is odd )
    newIndex = len / 2 + oldIndex / 2;
else
        newIndex = oldIndex / 2;
```

因此，问题简化为将元素转移到基于上述公式的新索引。
从形式 3^k 的指数开始，从 k = 0 开始，应用循环前导迭代算法。

以下是步骤:
**1。**在位置 I 找到项目的新位置。在将该项目放在新位置之前，将元素的备份保留在新位置。现在，把物品放在新的位置。
T4【2】。对新位置重复步骤#1，直到完成一个循环，即直到程序回到起始位置。
**3。**对表单的下一个索引应用循环前导迭代算法 3^k.重复此步骤，直到 3^k < len。
考虑大小为 28 的输入数组:
第一个循环领导者迭代，从索引 1 开始:
1->14->7->17->22->11->19->23->25->26->13->20->10->5->110

基于以上算法，下面是代码:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// A utility function to swap characters
void swap ( char* a, char* b )
{
    char t = *a;
    *a = *b;
    *b = t;
}

// A utility function to reverse string str[low..high]
void reverse ( char* str, int low, int high )
{
    while ( low < high )
    {
        swap( &str[low], &str[high] );
        ++low;
        --high;
    }
}

// Cycle leader algorithm to move all even
//  positioned elements at the end.
void cycleLeader ( char* str, int shift, int len )
{
    int j;
    char item;

    for (int i = 1; i < len; i *= 3 )
    {
        j = i;

        item = str[j + shift];
        do
        {
            // odd index
            if ( j & 1 )
                j = len / 2 + j / 2;
            // even index
            else
                j /= 2;

            // keep the back-up of element at new position
            swap (&str[j + shift], &item);
        }
        while ( j != i );
    }
}

// The main function to transform a string. This function 
// mainly uses cycleLeader() to transform
void moveNumberToSecondHalf( char* str )
{
    int k, lenFirst;

    int lenRemaining = strlen( str );
    int shift = 0;

    while ( lenRemaining )
    {
        k = 0;

        // Step 1: Find the largest prefix
        // subarray of the form 3^k + 1
        while ( pow( 3, k ) + 1 <= lenRemaining )
            k++;
        lenFirst = pow( 3, k - 1 ) + 1;
        lenRemaining -= lenFirst;

        // Step 2: Apply cycle leader algorithm
        // for the largest subarrau
        cycleLeader ( str, shift, lenFirst );

        // Step 4.1: Reverse the second half of first subarray
        reverse ( str, shift / 2, shift - 1 );

        // Step 4.2: Reverse the first half of second sub-string.
        reverse ( str, shift, shift + lenFirst / 2 - 1 );

        // Step 4.3 Reverse the second half of first sub-string
        // and first half of second sub-string together
        reverse ( str, shift / 2, shift + lenFirst / 2 - 1 );

        // Increase the length of first subarray
        shift += lenFirst;
    }
}

// Driver program to test above function
int main()
{
    char str[] = "a1b2c3d4e5f6g7";
    moveNumberToSecondHalf( str );
    cout<<str;
    return 0;
}

// This is code is contributed by rathbhupendra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG{

static char []str;

// A utility function to reverse
// String str[low..high]
static void reverse(int low, int high)
{
    while (low < high)
    {
        char t = str[low];
        str[low] = str[high];
        str[high] = t;
        ++low;
        --high;
    }
}

// Cycle leader algorithm to move all even
// positioned elements at the end.
static void cycleLeader(int shift, int len)
{
    int j;
    char item;

    for(int i = 1; i < len; i *= 3)
    {
        j = i;
        item = str[j + shift];

        do
        {

            // odd index
            if (j % 2 == 1)
                j = len / 2 + j / 2;

            // even index
            else
                j /= 2;

            // Keep the back-up of element at
            // new position
            char t = str[j + shift];
            str[j + shift] = item;
            item = t;
        }
        while (j != i);
    }
}

// The main function to transform a String.
// This function mainly uses cycleLeader()
// to transform
static void moveNumberToSecondHalf()
{
    int k, lenFirst;
    int lenRemaining = str.length;
    int shift = 0;

    while (lenRemaining > 0)
    {
        k = 0;

        // Step 1: Find the largest prefix
        // subarray of the form 3^k + 1
        while (Math.pow(3, k) + 1 <= lenRemaining)
            k++;

        lenFirst = (int)Math.pow(3, k - 1) + 1;
        lenRemaining -= lenFirst;

        // Step 2: Apply cycle leader algorithm
        // for the largest subarrau
        cycleLeader(shift, lenFirst);

        // Step 4.1: Reverse the second half
        // of first subarray
        reverse(shift / 2, shift - 1);

        // Step 4.2: Reverse the first half
        // of second sub-String.
        reverse(shift, shift + lenFirst / 2 - 1);

        // Step 4.3 Reverse the second half
        // of first sub-String and first half
        // of second sub-String together
        reverse(shift / 2, shift + lenFirst / 2 - 1);

        // Increase the length of first subarray
        shift += lenFirst;
    }
}

// Driver code
public static void main(String[] args)
{
    String st = "a1b2c3d4e5f6g7";
    str = st.toCharArray();

    moveNumberToSecondHalf();

    System.out.print(str);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of above approach

# A utility function to reverse string str[low..high]
def Reverse(string: list, low: int, high: int):
    while low < high:
        string[low], string[high] = string[high], string[low]
        low += 1
        high -= 1

# Cycle leader algorithm to move all even
# positioned elements at the end.
def cycleLeader(string: list, shift: int, len: int):
    i = 1
    while i < len:
        j = i
        item = string[j + shift]

        while True:

            # odd index
            if j & 1:
                j = len // 2 + j // 2

            # even index
            else:
                j //= 2

            # keep the back-up of element at new position
            string[j + shift], item = item, string[j + shift]

            if j == i:
                break
        i *= 3

# The main function to transform a string. This function
# mainly uses cycleLeader() to transform
def moveNumberToSecondHalf(string: list):
    k, lenFirst = 0, 0
    lenRemaining = len(string)
    shift = 0

    while lenRemaining:
        k = 0

        # Step 1: Find the largest prefix
        # subarray of the form 3^k + 1
        while pow(3, k) + 1 <= lenRemaining:
            k += 1
        lenFirst = pow(3, k - 1) + 1
        lenRemaining -= lenFirst

        # Step 2: Apply cycle leader algorithm
        # for the largest subarrau
        cycleLeader(string, shift, lenFirst)

        # Step 4.1: Reverse the second half of first subarray
        Reverse(string, shift // 2, shift - 1)

        # Step 4.2: Reverse the first half of second sub-string
        Reverse(string, shift, shift + lenFirst // 2 - 1)

        # Step 4.3 Reverse the second half of first sub-string
        # and first half of second sub-string together
        Reverse(string, shift // 2, shift + lenFirst // 2 - 1)

        # Increase the length of first subarray
        shift += lenFirst

# Driver Code
if __name__ == "__main__":

    string = "a1b2c3d4e5f6g7"
    string = list(string)
    moveNumberToSecondHalf(string)
    print(''.join(string))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

static char []str;

// A utility function to
// reverse String str[low
// ..high]
static void reverse(int low,
                    int high)
{
  while (low < high)
  {
    char t = str[low];
    str[low] = str[high];
    str[high] = t;
    ++low;
    --high;
  }
}

// Cycle leader algorithm to
// move all even positioned
// elements at the end.
static void cycleLeader(int shift,
                        int len)
{
  int j;
  char item;

  for(int i = 1;
          i < len; i *= 3)
  {
    j = i;
    item = str[j + shift];

    do
    {
      // odd index
      if (j % 2 == 1)
        j = len / 2 + j / 2;

      // even index
      else
        j /= 2;

      // Keep the back-up of
      // element at new position
      char t = str[j + shift];
      str[j + shift] = item;
      item = t;
    }
    while (j != i);
  }
}

// The main function to transform
// a String. This function mainly
// uses cycleLeader() to transform
static void moveNumberToSecondHalf()
{
  int k, lenFirst;
  int lenRemaining = str.Length;
  int shift = 0;

  while (lenRemaining > 0)
  {
    k = 0;

    // Step 1: Find the largest prefix
    // subarray of the form 3^k + 1
    while (Math.Pow(3, k) +
           1 <= lenRemaining)
      k++;

    lenFirst = (int)Math.Pow(3,
                             k - 1) + 1;
    lenRemaining -= lenFirst;

    // Step 2: Apply cycle leader
    // algorithm for the largest
    // subarrau
    cycleLeader(shift, lenFirst);

    // Step 4.1: Reverse the second
    // half of first subarray
    reverse(shift / 2,
            shift - 1);

    // Step 4.2: Reverse the
    // first half of second
    // sub-String.
    reverse(shift, shift +
            lenFirst / 2 - 1);

    // Step 4.3 Reverse the second
    // half of first sub-String and
    // first half of second sub-String
    // together
    reverse(shift / 2, shift +
            lenFirst / 2 - 1);

    // Increase the length of
    // first subarray
    shift += lenFirst;
  }
}

// Driver code
public static void Main(String[] args)
{
  String st = "a1b2c3d4e5f6g7";
  str = st.ToCharArray();
  moveNumberToSecondHalf();
  Console.Write(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

let str;

// A utility function to reverse
// String str[low..high]
function reverse(low,high)
{
    while (low < high)
    {
        let t = str[low];
        str[low] = str[high];
        str[high] = t;
        ++low;
        --high;
    }
}

// Cycle leader algorithm to move all even
// positioned elements at the end.
function cycleLeader(shift,len)
{
    let j;
    let item;

    for(let i = 1; i < len; i *= 3)
    {
        j = i;
        item = str[j + shift];

        do
        {

            // odd index
            if (j % 2 == 1)
                j = Math.floor(len / 2) + Math.floor(j / 2);

            // even index
            else
                j =Math.floor(j/2);

            // Keep the back-up of element at
            // new position
            let t = str[j + shift];
            str[j + shift] = item;
            item = t;
        }
        while (j != i);
    }
}

// The main function to transform a String.
// This function mainly uses cycleLeader()
// to transform
function moveNumberToSecondHalf()
{
    let k, lenFirst;
    let lenRemaining = str.length;
    let shift = 0;

    while (lenRemaining > 0)
    {
        k = 0;

        // Step 1: Find the largest prefix
        // subarray of the form 3^k + 1
        while (Math.pow(3, k) + 1 <= lenRemaining)
            k++;

        lenFirst = Math.floor(Math.pow(3, k - 1)) + 1;
        lenRemaining -= lenFirst;

        // Step 2: Apply cycle leader algorithm
        // for the largest subarrau
        cycleLeader(shift, lenFirst);

        // Step 4.1: Reverse the second half
        // of first subarray
        reverse(Math.floor(shift / 2), shift - 1);

        // Step 4.2: Reverse the first half
        // of second sub-String.
        reverse(shift, shift + Math.floor(lenFirst / 2) - 1);

        // Step 4.3 Reverse the second half
        // of first sub-String and first half
        // of second sub-String together
        reverse(Math.floor(shift / 2), shift + Math.floor(lenFirst / 2) - 1);

        // Increase the length of first subarray
        shift += lenFirst;
    }
}

// Driver code
let st = "a1b2c3d4e5f6g7";
    str = st.split("");

    moveNumberToSecondHalf();

    document.write(str.join(""));

// This code is contributed by rag2127
</script>
```

**输出:**

```
abcdefg1234567
```

点击这里查看各种测试用例。
**注释:**
**1。**如果数组大小已经是 3^k + 1 的形式，我们可以直接应用循环 leader 迭代算法。没必要加入。
**2。**循环前导迭代算法仅适用于 3^k + 1 形式的大小数组。

*时间复杂度 O(n)如何？*
一个周期内每个项目最多移位一次。因此循环前导算法的时间复杂度为 O(n)。反向运算的时间复杂度为 O(n)。我们将很快更新算法时间复杂性的数学证明。

*练习:*
给定形式为“abcdefg1234567”的字符串，就地转换为时间复杂度为 O(n)的“a1b2c3d4e5f6g7”。

**参考文献:**
[一种简单的 In-Shu 原地算法？例如](http://arxiv.org/pdf/0805.1598v1.pdf)
__ [阿瓦斯·巴纳瓦尔](http://www.facebook.com/barnwal.aashish)。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。