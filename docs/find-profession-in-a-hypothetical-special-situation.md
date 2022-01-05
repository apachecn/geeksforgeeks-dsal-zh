# 在特殊家庭找职业

> 原文:[https://www . geesforgeks . org/find-profession-in-a-假想-特殊情况/](https://www.geeksforgeeks.org/find-profession-in-a-hypothetical-special-situation/)

考虑一个特殊的工程师和医生家族，其规则如下:

1.  每个人都有两个孩子。
2.  工程师的第一个孩子是工程师，第二个孩子是医生。
3.  医生的第一个孩子是医生，第二个孩子是工程师。
4.  所有一代的医生和工程师都是从工程师开始的。

我们可以用下图来表示这种情况:

```
                E
           /        
          E          D
        /          /  
       E     D     D    E
      /    /    /    / 
     E   D D   E  D  E  E  D
```

给定一个人在上面祖先树中的级别和位置，找到这个人的职业。
**例:**

```
Input : level = 4, pos = 2
Output : Doctor

Input : level = 3, pos = 4
Output : Engineer
```

**方法 1(递归)**
这个想法是基于一个人的职业取决于以下两个事实。

1.  父母的职业。
2.  节点的位置:如果一个节点的位置是奇数，那么它的职业就是它的父节点。其他职业与其父母不同。

我们递归找到父节点的职业，然后用上面的点 2 找到当前节点的职业。
以下是上述思路的实现。

> ## C++
> 
> ```
> // C++ program to find profession of a person at
> // given level and position.
> #include<bits/stdc++.h>
> using namespace std;
>  
> // Returns 'e' if profession of node at given level
> // and position is engineer. Else doctor. The function
> // assumes that given position and level have valid values.
> char findProffesion(int level, int pos)
> {
>     // Base case
>     if (level == 1)
>         return 'e';
>  
>     // Recursively find parent's profession. If parent
>     // is a Doctor, this node will be a Doctor if it is
>     // at odd position and an engineer if at even position
>     if (findProffesion(level-1, (pos+1)/2) == 'd')
>         return (pos%2)? 'd' : 'e';
>  
>     // If parent is an engineer, then current node will be
>     // an engineer if at add position and doctor if even
>     // position.
>     return (pos%2)?  'e' : 'd';
> }
>  
> // Driver code
> int main(void)
> {
>     int level = 4, pos = 2;
>     (findProffesion(level, pos) == 'e')? cout << "Engineer"
>                                        : cout << "Doctor" ;
>     return 0;
> }
> ```
> 
> ## Java language (a computer language, Especially for creating websites)
> 
> ```
> // Java program to find
> // profession of a person
> // at given level and position
> import java.io.*;
>  
> class GFG
> {
>  
> // Returns 'e' if profession
> // of node at given level
> // and position is engineer.
> // Else doctor. The function
> // assumes that given position
> // and level have valid values.
> static char findProffesion(int level,
>                            int pos)
> {
>     // Base case
>     if (level == 1)
>         return 'e';
>  
>     // Recursively find parent's
>     // profession. If parent
>     // is a Doctor, this node
>     // will be a Doctor if it
>     // is at odd position and an
>     // engineer if at even position
>     if (findProffesion(level - 1,
>                       (pos + 1) / 2) == 'd')
>         return (pos % 2 > 0) ?
>                          'd' : 'e';
>  
>     // If parent is an engineer,
>     // then current node will be
>     // an engineer if at add
>     // position and doctor if even
>     // position.
>     return (pos % 2 > 0) ?
>                      'e' : 'd';
> }
>  
> // Driver code
> public static void main (String[] args)
> {
>     int level = 4, pos = 2;
>     if(findProffesion(level,
>                       pos) == 'e')
>     System.out.println("Engineer");
>     else
>     System.out.println("Doctor");
> }
> }
>  
> // This code is contributed
> // by anuj_67.
> ```
> 
> ## Python 3
> 
> ```
> # python 3 program to find profession of a person at
> # given level and position.
>  
> # Returns 'e' if profession of node at given level
> # and position is engineer. Else doctor. The function
> # assumes that given position and level have valid values.
> def findProffesion(level, pos):
>     # Base case
>     if (level == 1):
>         return 'e'
>  
>     # Recursively find parent's profession. If parent
>     # is a Doctor, this node will be a Doctor if it is
>     # at odd position and an engineer if at even position
>     if (findProffesion(level-1, (pos+1)//2) == 'd'):
>         if (pos%2):
>             return 'd'
>         else:
>             return 'e'
>  
>     # If parent is an engineer, then current node will be
>     # an engineer if at add position and doctor if even
>     # position.
>     if(pos%2):
>         return 'e'
>     else:
>         return 'd'
>  
> # Driver code
> if __name__ == '__main__':
>     level = 3
>     pos = 4
>     if(findProffesion(level, pos) == 'e'):
>         print("Engineer")
>     else:
>         print("Doctor")
>          
> # This code is contributed by
> # Surendra_Gangwar
> ```
> 
> ## C #
> 
> ```
> // C# program to find
> // profession of a person
> // at given level and position
> using System;
>  
> class GFG
> {
>  
> // Returns 'e' if profession
> // of node at given level
> // and position is engineer.
> // Else doctor. The function
> // assumes that given position
> // and level have valid values.
> static char findProffesion(int level,
>                            int pos)
> {
>     // Base case
>     if (level == 1)
>         return 'e';
>  
>     // Recursively find parent's
>     // profession. If parent
>     // is a Doctor, this node
>     // will be a Doctor if it
>     // is at odd position and an
>     // engineer if at even position
>     if (findProffesion(level - 1,
>                       (pos + 1) / 2) == 'd')
>         return (pos % 2 > 0) ?
>                          'd' : 'e';
>  
>     // If parent is an engineer,
>     // then current node will be
>     // an engineer if at add
>     // position and doctor if even
>     // position.
>     return (pos % 2 > 0) ?
>                      'e' : 'd';
> }
>  
> // Driver code
> public static void Main ()
> {
>     int level = 4, pos = 2;
>     if(findProffesion(level,
>                     pos) == 'e')
>     Console.WriteLine("Engineer");
>     else
>     Console.WriteLine("Doctor");
> }
> }
>  
> // This code is contributed
> // by anuj_67.
> ```
> 
> ## Server-side programming language (abbreviation of professional hypertext preprocessor)
> 
> ```
> <?php
> // PHP program to find profession
> // of a person at given level
> // and position.
>  
> // Returns 'e' if profession of
> // node at given level and position
> // is engineer. Else doctor. The
> // function assumes that given
> // position and level have valid values.
> function findProffesion($level, $pos)
> {
>     // Base case
>     if ($level == 1)
>         return 'e';
>  
>     // Recursively find parent's
>     // profession. If parent is
>     // a Doctor, this node will
>     // be a doctor if it is at
>     // odd position and an engineer
>     // if at even position
>     if (findProffesion($level - 1,
>                       ($pos + 1) / 2) == 'd')
>         return ($pos % 2) ? 'd' : 'e';
>  
>     // If parent is an engineer, then
>     // current node will be an engineer
>     // if at odd position and doctor
>     // if even position.
>     return ($pos % 2) ? 'e' : 'd';
> }
>  
> // Driver code
> $level = 4; $pos = 2;
> if((findProffesion($level,
>                    $pos) == 'e') == true)
>     echo "Engineer";
> else
>     echo "Doctor" ;
>      
> // This code is contributed by ajit
> ?>
> ```
> 
> ## java description language
> 
> ```
> <script>
>  
> // JavaScript program to find
> // profession of a person
> // at given level and position
>  
> // Returns 'e' if profession
> // of node at given level
> // and position is engineer.
> // Else doctor. The function
> // assumes that given position
> // and level have valid values.
> function findProffesion(level,
>                            pos)
> {
>     // Base case
>     if (level == 1)
>         return 'e';
>   
>     // Recursively find parent's
>     // profession. If parent
>     // is a Doctor, this node
>     // will be a Doctor if it
>     // is at odd position and an
>     // engineer if at even position
>     if (findProffesion(level - 1,
>                       (pos + 1) / 2) == 'd')
>         return (pos % 2 > 0) ?
>                          'd' : 'e';
>   
>     // If parent is an engineer,
>     // then current node will be
>     // an engineer if at add
>     // position and doctor if even
>     // position.
>     return (pos % 2 > 0) ?
>                      'e' : 'd';
> }
>  
> // Driver Code
>  
>     let level = 4, pos = 2;
>     if(findProffesion(level,
>                       pos) == 'e')
>     document.write("Engineer");
>     else
>     document.write("Doctor");
>                          
> </script>
> ```

**输出:**

```
Doctor
```

**方法 2(使用按位运算符)**

```
Level 1: E
Level 2: ED
Level 3: EDDE
Level 4: EDDEDEED
Level 5: EDDEDEEDDEEDEDDE 
```

级别输入不是必需的(如果我们忽略最大位置限制)，因为第一个元素是相同的。
结果基于位置减 1 的二进制表示中 1 的计数。如果 1 的计数是偶数，那么结果是工程师，否则是医生。
当然位置限制是 2^(Level-1)

## C++

```
// C++ program to find profession of a person at
// given level and position.
#include<bits/stdc++.h>
using namespace std;

/* Function to get no of set bits in binary
   representation of passed binary no. */
int countSetBits(int n)
{
    int count = 0;
    while (n)
    {
      n &= (n-1) ;
      count++;
    }
    return count;
}

// Returns 'e' if profession of node at given level
// and position is engineer. Else doctor. The function
// assumes that given position and level have valid values.
char findProffesion(int level, int pos)
{
    // Count set bits in 'pos-1'
    int c = countSetBits(pos-1);

    // If set bit count is odd, then doctor, else engineer
    return (c%2)?  'd' : 'e';
}

// Driver code
int main(void)
{
    int level = 3, pos = 4;
    (findProffesion(level, pos) == 'e')? cout << "Engineer"
                                       : cout << "Doctor" ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find profession of a person at
// given level and position.
class GFG{
/* Function to get no of set bits in binary
representation of passed binary no. */
static int countSetBits(int n)
{
    int count = 0;
    while (n!=0)
    {
    n &= (n-1) ;
    count++;
    }
    return count;
}

// Returns 'e' if profession of node at given level
// and position is engineer. Else doctor. The function
// assumes that given position and level have valid values.
static char findProffesion(int level, int pos)
{
    // Count set bits in 'pos-1'
    int c = countSetBits(pos-1);

    // If set bit count is odd, then doctor, else engineer
    return (c%2 !=0)? 'd' : 'e';
}

// Driver code
public static void main(String [] args)
{
    int level = 3, pos = 4;
    String prof = (findProffesion(level, pos) == 'e')? "Engineer"
                                    : "Doctor"  ;
    System.out.print(prof);
}
}
```

## 蟒蛇 3

```
# Python3 program to find profession of a person at
# given level and position.

""" Function to get no of set bits in binary
   representation of passed binary no. """
def countSetBits(n):
    count = 0
    while n > 0:
      n &= (n-1)
      count+=1
    return count

# Returns 'e' if profession of node at given level
# and position is engineer. Else doctor. The function
# assumes that given position and level have valid values.
def findProffesion(level, pos):
    # Count set bits in 'pos-1'
    c = countSetBits(pos-1)

    # If set bit count is odd, then doctor, else engineer
    if c%2 == 0:
        return 'e'
    else:
        return 'd'

level, pos = 3, 4
if findProffesion(level, pos) == 'e':
    print("Engineer")
else:
    print("Doctor")

    # This code is contributed by divyeshrabadiya07.
```

## C#

```
using System;

// c# program to find profession of a person at 
// given level and position. 
public class GFG
{
/* Function to get no of set bits in binary 
representation of passed binary no. */
public static int countSetBits(int n)
{
    int count = 0;
    while (n != 0)
    {
    n &= (n - 1);
    count++;
    }
    return count;
}

// Returns 'e' if profession of node at given level 
// and position is engineer. Else doctor. The function 
// assumes that given position and level have valid values. 
public static char findProffesion(int level, int pos)
{
    // Count set bits in 'pos-1' 
    int c = countSetBits(pos - 1);

    // If set bit count is odd, then doctor, else engineer 
    return (c % 2 != 0)? 'd' : 'e';
}

// Driver code 
public static void Main(string[] args)
{
    int level = 3, pos = 4;
    string prof = (findProffesion(level, pos) == 'e')? "Engineer" : "Doctor";
    Console.Write(prof);
}
}

  // This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find profession
// of a person at given level and position.

// Function to get no of set
// bits in binary representation
// of passed binary no.
function countSetBits($n)
{
    $count = 0;
    while ($n)
    {
        $n &= ($n - 1) ;
        $count++;
    }
    return $count;
}

// Returns 'e' if profession of
// node at given level and position
// is engineer. Else doctor. The
// function assumes that given
// position and level have valid values.
function findProffesion($level, $pos)
{
    // Count set bits in 'pos-1'
    $c = countSetBits($pos - 1);

    // If set bit count is odd,
    // then doctor, else engineer
    return ($c % 2) ? 'd' : 'e';
}

// Driver Code
$level = 3;
$pos = 4;
if((findProffesion($level,
                   $pos) == 'e') == true)
        echo "Engineer \n";
    else
        echo "Doctor \n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // profession of a person at
    // given level and position.

    /* Function to get no of set bits in binary
    representation of passed binary no. */
    function countSetBits(n)
    {
        let count = 0;
        while (n != 0)
        {
          n &= (n - 1);
          count++;
        }
        return count;
    }

    // Returns 'e' if profession of node at given level
    // and position is engineer. Else doctor.
    // The function assumes that given position and
    // level have valid values.
    function findProffesion(level, pos)
    {
        // Count set bits in 'pos-1'
        let c = countSetBits(pos - 1);

        // If set bit count is odd, then doctor,
        // else engineer
        return (c % 2 != 0)? 'd' : 'e';
    }

    let level = 3, pos = 4;
    let prof = (findProffesion(level, pos) == 'e')?
                "Engineer" : "Doctor";
    document.write(prof);

</script>
```

**输出:**

```
Engineer
```

感谢富尔坎·乌斯卢提出这个方法。
本文由**严酷帕里克**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。