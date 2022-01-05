# 写一个程序把两个数字加在 14 的基数上

> 原文:[https://www . geesforgeks . org/write-a-program-add-two-in-numbers-base-14/](https://www.geeksforgeeks.org/write-a-program-to-add-two-numbers-in-base-14/)

安莎问。
下面是 14 进制数的不同加法方式。
**方法 1**
感谢拉吉提出这个方法。

```
  1\. Convert both i/p base 14 numbers to base 10.
  2\. Add numbers.
  3\. Convert the result back to base 14.
```

**方法 2**
就像我们在 10 进制中那样，把 14 进制中的数字相加。从右向左逐一添加两个数字的数字。如果在添加两个数字时有一个进位，考虑用于添加下一个数字的进位。
让我们考虑 14 进制数与十六进制数相同的表示方式

```
   A --> 10
   B --> 11
   C --> 12
   D --> 13
```

```
Example:
   num1 =       1  2  A
   num2 =       C  D  3   

   1\. Add A and 3, we get 13(D). Since 13 is smaller than 
14, carry becomes 0 and resultant numeral becomes D         

  2\. Add 2, D and carry(0). we get 15\. Since 15 is greater 
than 13, carry becomes 1 and resultant numeral is 15 - 14 = 1

  3\. Add 1, C and carry(1). we get 14\. Since 14 is greater 
than 13, carry becomes 1 and resultant numeral is 14 - 14 = 0

Finally, there is a carry, so 1 is added as leftmost numeral and the result becomes 
101D 
```

**实施方法 2**

## C++

```
#include <bits/stdc++.h>
using namespace std;
# define bool int

int getNumeralValue(char );
char getNumeral(int );

/* Function to add two numbers in base 14 */
char *sumBase14(char num1[], char num2[])
{
    int l1 = strlen(num1);
    int l2 = strlen(num2);
    char *res;
    int i;
    int nml1, nml2, res_nml;
    bool carry = 0;

    if(l1 != l2)
    {
        cout << "Function doesn't support numbers of different"
                " lengths. If you want to add such numbers then"
                " prefix smaller number with required no. of zeroes";
        assert(0);
    }

    /* Note the size of the allocated memory is one
        more than i/p lengths for the cases where we
        have carry at the last like adding D1 and A1 */
    res = new char[(sizeof(char)*(l1 + 1))];

    /* Add all numerals from right to left */
    for(i = l1-1; i >= 0; i--)
    {
        /* Get decimal values of the numerals of
        i/p numbers*/   
        nml1 = getNumeralValue(num1[i]);
        nml2 = getNumeralValue(num2[i]);

        /* Add decimal values of numerals and carry */
        res_nml = carry + nml1 + nml2;

        /* Check if we have carry for next addition
            of numerals */
        if(res_nml >= 14)
        {
            carry = 1;
            res_nml -= 14;
        }
        else
        {
               carry = 0;
        }
        res[i+1] = getNumeral(res_nml);
    }

    /* if there is no carry after last iteration
        then result should not include 0th character
        of the resultant string */
    if(carry == 0)
        return (res + 1);

    /* if we have carry after last iteration then
        result should include 0th character */
    res[0] = '1';
    return res;
}

/* Function to get value of a numeral
For example it returns 10 for input 'A'
1 for '1', etc */
int getNumeralValue(char num)
{
    if( num >= '0' && num <= '9')
        return (num - '0');
    if( num >= 'A' && num <= 'D')
        return (num - 'A' + 10);

    /* If we reach this line caller is giving
        invalid character so we assert and fail*/
    assert(0);
}

/* Function to get numeral for a value.
For example it returns 'A' for input 10
'1' for 1, etc */
char getNumeral(int val)
{
    if( val >= 0 && val <= 9)
        return (val + '0');
    if( val >= 10 && val <= 14)
        return (val + 'A' - 10);

    /* If we reach this line caller is giving
        invalid no. so we assert and fail*/
    assert(0);
}

/*Driver code*/
int main()
{
    char num1[] = "DC2";
    char num2[] = "0A3";

    cout<<"Result is "<<sumBase14(num1, num2);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
# include <stdio.h>
# include <stdlib.h>
# define bool int

int getNumeralValue(char );
char getNumeral(int );

/* Function to add two numbers in base 14 */
char *sumBase14(char *num1,  char *num2)
{
   int l1 = strlen(num1);
   int l2 = strlen(num2); 
   char *res;
   int i;
   int nml1, nml2, res_nml;  
   bool carry = 0;

   if(l1 != l2)
   {
     printf("Function doesn't support numbers of different"
            " lengths. If you want to add such numbers then"
            " prefix smaller number with required no. of zeroes");
     getchar();        
     assert(0);
   }     

   /* Note the size of the allocated memory is one
     more than i/p lengths for the cases where we
     have carry at the last like adding D1 and A1 */  
   res = (char *)malloc(sizeof(char)*(l1 + 1));

   /* Add all numerals from right to left */
   for(i = l1-1; i >= 0; i--)
   {
     /* Get decimal values of the numerals of
       i/p numbers*/         
     nml1 = getNumeralValue(num1[i]);
     nml2 = getNumeralValue(num2[i]);

     /* Add decimal values of numerals and carry */
     res_nml = carry + nml1 + nml2;

     /* Check if we have carry for next addition
        of numerals */
     if(res_nml >= 14)
     {
       carry = 1;
       res_nml -= 14;
     }  
     else
     {
       carry = 0;    
     }      
     res[i+1] = getNumeral(res_nml);
   }

   /* if there is no carry after last iteration
      then result should not include 0th character
      of the resultant string */
   if(carry == 0)
     return (res + 1);  

   /* if we have carry after last iteration then
     result should include 0th character */
   res[0] = '1';
   return res;
}

/* Function to get value of a numeral
  For example it returns 10 for input 'A'
  1 for '1', etc */
int getNumeralValue(char num)
{
  if( num >= '0' && num <= '9')
    return (num - '0');
  if( num >= 'A' && num <= 'D') 
    return (num - 'A' + 10);

  /* If we reach this line caller is giving
    invalid character so we assert and fail*/ 
  assert(0);
}

/* Function to get numeral for a value.  
  For example it returns 'A' for input 10
  '1' for 1, etc */
char getNumeral(int val)
{
  if( val >= 0 && val <= 9)
    return (val + '0');
  if( val >= 10 && val <= 14) 
    return (val + 'A' - 10);

  /* If we reach this line caller is giving
    invalid no. so we assert and fail*/     
  assert(0);
}

/*Driver program to test above functions*/
int main()
{
    char *num1 = "DC2";
    char *num2 = "0A3";

    printf("Result is %s", sumBase14(num1, num2));    
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to add two
// numbers in base 14
static String sumBase14(char num1[],
                        char num2[])
{
  int l1 = num1.length;
  int l2 = num2.length;
  char []res;
  int i;
  int nml1, nml2, res_nml;
  int carry = 0;

  if(l1 != l2)
  {
    System.out.print("Function doesn't support " +
                     "numbers of different " +
                     "lengths. If you want to " +
                     "dd such numbers then " +
                     "prefix smaller number " +
                     "with required no. of zeroes"); 
  }

  // Note the size of the allocated
  // memory is one more than i/p
  // lengths for the cases where we
  // have carry at the last like
  // adding D1 and A1
  res = new char[(4 * (l1 + 1))];

  // Add all numerals from
  // right to left
  for(i = l1 - 1; i >= 0; i--)
  {
    // Get decimal values of the
    // numerals of i/p numbers  
    nml1 = getNumeralValue(num1[i]);
    nml2 = getNumeralValue(num2[i]);

    // Add decimal values of
    // numerals and carry
    res_nml = carry + nml1 + nml2;

    // Check if we have carry for
    // next addition of numerals
    if(res_nml >= 14)
    {
      carry = 1;
      res_nml -= 14;
    }
    else
    {
      carry = 0;
    }
    res[i + 1] = getNumeral(res_nml);
  }

  // If there is no carry after
  // last iteration then result
  // should not include 0th
  // character of the resultant
  // String
  if(carry == 0)
    return String.valueOf(res);

  // If we have carry after last
  // iteration then result should
  // include 0th character
  res[0] = '1';
  return String.valueOf(res);
}

// Function to get value of a numeral
// For example it returns 10 for input
// 'A' 1 for '1', etc
static int getNumeralValue(char num)
{
  if(num >= '0' && num <= '9')
    return (num - '0');
  if(num >= 'A' && num <= 'D')
    return (num - 'A' + 10);

  // If we reach this line
  // caller is giving invalid
  // character so we assert
  // and fail
  // assert(0);
  return 0;
}

// Function to get numeral
// for a value. For example
// it returns 'A' for input 10
// '1' for 1, etc
static char getNumeral(int val)
{
  if(val >= 0 && val <= 9)
    return (char)(val + '0');
  if(val >= 10 && val <= 14)
    return (char)(val + 'A' - 10);

  // If we reach this line
  // caller is giving invalid
  // no. so we assert and fail
  // assert(0);
  return '0';
}

// Driver code
public static void main(String[] args)
{
  char num1[] = {'D','C','2'};
  char num2[] = {'0','A','3'};
  System.out.print("Result is " +
                    sumBase14(num1,
                              num2));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Function to get value of a numeral
# For example it returns 10 for input 'A'
# 1 for '1', etc
def getNumeralValue(num) :

    if( num >= '0' and num <= '9') :
        return ord(num) - ord('0')
    if( num >= 'A' and num <= 'D') :
        return ord(num ) - ord('A') + 10

# Function to get numeral for a value.
# For example it returns 'A' for input 10
# '1' for 1, etc
def getNumeral(val):

    if( val >= 0 and val <= 9):
        return chr(val + ord('0'))
    if( val >= 10 and val <= 14) :
        return chr(val + ord('A') - 10)

# Function to add two numbers in base 14
def sumBase14(num1, num2):

    l1 = len(num1)
    l2 = len(num2)
    carry = 0

    if(l1 != l2) :

        print("Function doesn't support numbers of different"
                " lengths. If you want to add such numbers then"
                " prefix smaller number with required no. of zeroes")

    # Note the size of the allocated memory is one
    # more than i/p lengths for the cases where we
    # have carry at the last like adding D1 and A1
    res = [0]*(l1 + 1)

    # dd all numerals from right to left
    for i in range(l1 - 1, -1, -1):

        # Get decimal values of the numerals of
        # i/p numbers
        nml1 = getNumeralValue(num1[i])
        nml2 = getNumeralValue(num2[i])

        # Add decimal values of numerals and carry
        res_nml = carry + nml1 + nml2;

        # Check if we have carry for next addition
        # of numerals
        if(res_nml >= 14) :
            carry = 1
            res_nml -= 14
        else:
            carry = 0
        res[i+1] = getNumeral(res_nml)

    # if there is no carry after last iteration
    # then result should not include 0th character
    # of the resultant string
    if(carry == 0):
        return (res + 1)

    # if we have carry after last iteration then
    # result should include 0th character
    res[0] = '1'
    return res

# Driver code
if __name__ == "__main__":

    num1 = "DC2"
    num2 = "0A3"

    print("Result is ",end="")
    res = sumBase14(num1, num2)
    for i in range(len(res)):
        print(res[i],end="")

# This code is contributed by chitranayal   
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to add two
// numbers in base 14
static String sumBase14(char []num1,
                        char []num2)
{
  int l1 = num1.Length;
  int l2 = num2.Length;
  char []res;
  int i;
  int nml1, nml2, res_nml;
  int carry = 0;

  if(l1 != l2)
  {
    Console.Write("Function doesn't support " +
                  "numbers of different " +
                  "lengths. If you want to " +
                  "dd such numbers then " +
                  "prefix smaller number " +
                  "with required no. of zeroes"); 
  }

  // Note the size of the allocated
  // memory is one more than i/p
  // lengths for the cases where we
  // have carry at the last like
  // adding D1 and A1
  res = new char[(4 * (l1 + 1))];

  // Add all numerals from
  // right to left
  for(i = l1 - 1; i >= 0; i--)
  {
    // Get decimal values of the
    // numerals of i/p numbers  
    nml1 = getNumeralValue(num1[i]);
    nml2 = getNumeralValue(num2[i]);

    // Add decimal values of
    // numerals and carry
    res_nml = carry + nml1 + nml2;

    // Check if we have carry for
    // next addition of numerals
    if(res_nml >= 14)
    {
      carry = 1;
      res_nml -= 14;
    }
    else
    {
      carry = 0;
    }
    res[i + 1] = getNumeral(res_nml);
  }

  // If there is no carry after
  // last iteration then result
  // should not include 0th
  // character of the resultant
  // String
  if(carry == 0)
    return String.Join("", res);

  // If we have carry after last
  // iteration then result should
  // include 0th character
  res[0] = '1';
  return String.Join("", res);
}

// Function to get value of a numeral
// For example it returns 10 for input
// 'A' 1 for '1', etc
static int getNumeralValue(char num)
{
  if(num >= '0' && num <= '9')
    return (num - '0');
  if(num >= 'A' && num <= 'D')
    return (num - 'A' + 10);

  // If we reach this line
  // caller is giving invalid
  // character so we assert
  // and fail
  // assert(0);
  return 0;
}

// Function to get numeral
// for a value. For example
// it returns 'A' for input 10
// '1' for 1, etc
static char getNumeral(int val)
{
  if(val >= 0 && val <= 9)
    return (char)(val + '0');
  if(val >= 10 && val <= 14)
    return (char)(val + 'A' - 10);

  // If we reach this line
  // caller is giving invalid
  // no. so we assert and fail
  // assert(0);
  return '0';
}

// Driver code
public static void Main(String[] args)
{
  char []num1 = {'D','C','2'};
  char []num2 = {'0','A','3'};
  Console.Write("Result is " +
                sumBase14(num1,
                          num2));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Function to add two
    // numbers in base 14
    function sumBase14(num1,num2)
    {
        let l1 = num1.length;
        let l2 = num2.length;

        // Note the size of the allocated
        // memory is one more than i/p
        // lengths for the cases where we
        // have carry at the last like
        // adding D1 and A1
        let res = new Array(4 * (l1 + 1));
        let i = 0;
        let nml1 = 0, nml2 = 0, res_nml = 0;
        let carry = 0;
        if(l1 != l2)
        {
            document.write("Function doesn't support " +
                     "numbers of different " +
                     "lengths. If you want to " +
                     "dd such numbers then " +
                     "prefix smaller number " +
                     "with required no. of zeroes");

        }

        // Add all numerals from
        // right to left
        for(i = l1 - 1; i >= 0; i--)
        {

            // Get decimal values of the
            // numerals of i/p numbers 
            nml1 = getNumeralValue(num1[i]);
            nml2 = getNumeralValue(num2[i]);

            // Add decimal values of
            // numerals and carry
            res_nml = carry + nml1 + nml2;

            // Check if we have carry for
            // next addition of numerals
            if(res_nml >= 14)
            {
                carry = 1;
                res_nml -= 14;
            }
            else
            {
                carry = 0;
            }
            res[i + 1] = getNumeral(res_nml);
        }

        // If there is no carry after
        // last iteration then result
        // should not include 0th
        // character of the resultant
        // String
        if(carry == 0)
        {
            return res;
        }

        // If we have carry after last
        // iteration then result should
        // include 0th character
        res[0] = '1';
        return res.join('');
    }

    // Function to get value of a numeral
    // For example it returns 10 for input
    // 'A' 1 for '1', etc
    function getNumeralValue(num)
    {
        if(num >= '0' && num <= '9')
        {
            return (num.charCodeAt(0) - '0'.charCodeAt(0));
        }
        if(num >= 'A' && num <= 'D')
        {
            return (num.charCodeAt(0) - 'A'.charCodeAt(0) + 10);
        }

        // If we reach this line
        // caller is giving invalid
        // character so we assert
        // and fail
        // assert(0);
        return 0;
    }

    // Function to get numeral
    // for a value. For example
    // it returns 'A' for input 10
    // '1' for 1, etc
    function getNumeral(val)
    {
        if(val >= 0 && val <= 9)
        {
            return String.fromCharCode(val + '0'.charCodeAt(0));
        }
        if(val >= 10 && val <= 14)
        {
            return String.fromCharCode(val + 'A'.charCodeAt(0) - 10);
        }

        // If we reach this line
        // caller is giving invalid
        // no. so we assert and fail
        // assert(0);
        return 0;
    }

    // Driver code
    let num1 = ['D','C','2'];
    let num2 = ['0','A','3'];

    document.write("Result is " + sumBase14(num1, num2));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Result is 1085
```

***时间复杂度:** O(|num1|)*

***辅助空间:** O(|num1|)*

**注:**
以上方法可以用来给任意基数加数字。如果基数小于 10，我们就不用做字符串运算了。
可以尝试将上述程序扩展为不同长度的号码。
如果您发现程序中有任何错误或更好的方法，请发表评论。