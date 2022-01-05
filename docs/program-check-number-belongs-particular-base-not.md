# 检查数字是否属于特定基数的程序

> 原文:[https://www . geeksforgeeks . org/program-check-number-attributes-special-base-not/](https://www.geeksforgeeks.org/program-check-number-belongs-particular-base-not/)

给定一个数 **N** 和它的基数 **R** ，根据它的基数找出它是否有效。
查找从二进制到 base32 的任何基数的有效/无效数字。

**示例:**

```
Input : 1000101010001
Output : Valid
1000101010001 is valid binary number.

Input : 0xFFFAG
Output : invalid
0xFFFAG is not a valid hexa-decimal number because of character 'G' .
```

**所用方法:** strspn

*   **strspn :**

```
strspn(numStr, validNumber)
Strspan: 
returns number of matching digits from 
character-set provided, so here it will return 1 - N,
where N is length of validNumber String.
numStr[]  : 
And that number is provided to numStr[] array.
```

*   编号 Str :

```
numStr[strspn(numStr, validNumber)]
Using this number as index for numStr[] array,
we access the digit there and it will be NULL 
in case string is matched and it will be non-zero 
if string is not matched
```

*   **！最后我们使用反转操作符来反转结果，以匹配真实情况**！****

```
!numStr[strspn(numStr, validNumber)]
```

## C++

```
// Program to check if a number belongs
// to particular base or not#include

#include <cstdio>
#include <cstdlib>
#include <cstring>

#define BINARY_BASE 2 // Defining binary base
#define OCTAL_BASE 8 // Defining octal base
#define DECIMAL_BASE 10 // Defining decimal base
#define HEXA_BASE 16 // Defining hexa-decimal base
#define BASE32_BASE 32 // Defining base32 base

// Function prototypes
bool isValid(const char* numStr, int base);
const char* print(bool status);

// Main method for base check
int main(void)
{
    // Defining valid/invalid numbers in radix bases
    char* binaryStr = "1000101010001";
    char* decimalStr = "45221";
    char* base32Str = "AD22F";

    // invalid
    char* octalStr = "7778A";
    char* hexStr = "FAG463";

    // Printing status of radix bases
    printf("Binary string %s is %s\n", binaryStr,
           print(isValid(binaryStr, BINARY_BASE)));
    printf("Octal string %s is %s\n", octalStr,
           print(isValid(hexStr, OCTAL_BASE)));
    printf("Decimal string %s is %s\n", decimalStr,
           print(isValid(decimalStr, DECIMAL_BASE)));
    printf("Hex string %s is %s\n", hexStr,
           print(isValid(hexStr, HEXA_BASE)));
    printf("Base32 string %s is %s\n", base32Str,
           print(isValid(base32Str, BASE32_BASE)));

    return 0;
}

bool isValid(const char* numStr, int base)
{
    // Defining valid base strings
    const char* validBinary = "01";
    const char* validOctal = "01234567";
    const char* validDecimal = "0123456789";
    const char* validHex = "0123456789abcdefABCDEF";
    const char* validBase32 = "0123456789abcdefghijklmnopqrstuvABCDEFGHIJKLMNOPQRSTUV";
    const char* validNumber = NULL;

    // Checking for valid base
    validNumber = (base == BINARY_BASE)
                      ? validBinary
                      : ((base == OCTAL_BASE)
                             ? validOctal
                             : (base == DECIMAL_BASE)
                                   ? validDecimal
                                   : (base == HEXA_BASE)
                                         ? validHex
                                         : (base == BASE32_BASE)
                                               ? validBase32
                                               : NULL);

    // Error checking for invalid base
    if (validNumber == NULL) {
        fputs("Invalid base encountered", stderr);
        exit(EXIT_FAILURE);
    }

    // Check for valid base string using strspn
    return (!numStr[strspn(numStr, validNumber)]) ? true : false;
}

const char* print(bool status)
{
    return (status) ? "Valid" : "Invalid";
}
```

**输出:**

```
Binary string 1000101010001 is Valid
Octal string 7778A is Invalid
Decimal string 45221 is Valid
Hex string FAG463 is Invalid
Base32 string AD22F is Valid                                                                                         
```