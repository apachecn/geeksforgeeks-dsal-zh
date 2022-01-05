# 异或密码

> 原文:[https://www.geeksforgeeks.org/xor-cipher/](https://www.geeksforgeeks.org/xor-cipher/)

异或加密是一种用于加密数据的加密方法，很难通过暴力破解，即生成随机加密密钥来匹配正确的密钥。

下面是 C++中的一个简单实现。实现的概念是首先定义异或加密密钥，然后用这个密钥对字符串中要加密的字符进行异或运算。为了解密加密的字符，我们必须用定义的密钥再次执行异或运算。这里我们对整个字符串进行加密。

## C++

```
// C++ program to implement XOR - Encryption
#include<bits/stdc++.h>

// The same function is used to encrypt and
// decrypt
void encryptDecrypt(char inpString[])
{
    // Define XOR key
    // Any character value will work
    char xorKey = 'P';

    // calculate length of input string
    int len = strlen(inpString);

    // perform XOR operation of key
    // with every character in string
    for (int i = 0; i < len; i++)
    {
        inpString[i] = inpString[i] ^ xorKey;
        printf("%c",inpString[i]);
    }
}

// Driver program to test above function
int main()
{
    char sampleString[] = "GeeksforGeeks";

    // Encrypt the string
    printf("Encrypted String: ");
    encryptDecrypt(sampleString);
    printf("\n");

    // Decrypt the string
    printf("Decrypted String: ");
    encryptDecrypt(sampleString);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement XOR - Encryption
class XOREncryption
{
    // The same function is used to encrypt and
    // decrypt
    static String encryptDecrypt(String inputString)
    {
        // Define XOR key
        // Any character value will work
        char xorKey = 'P';

        // Define String to store encrypted/decrypted String
        String outputString = "";

        // calculate length of input string
        int len = inputString.length();

        // perform XOR operation of key
        // with every character in string
        for (int i = 0; i < len; i++)
        {
            outputString = outputString +
            Character.toString((char) (inputString.charAt(i) ^ xorKey));
        }

        System.out.println(outputString);
        return outputString;
    }

    // Driver code
    public static void main(String[] args)
    {
        String sampleString = "GeeksforGeeks";

        // Encrypt the string
        System.out.println("Encrypted String");
        String encryptedString = encryptDecrypt(sampleString);

        // Decrypt the string
        System.out.println("Decrypted String");
        encryptDecrypt(encryptedString);
    }
}

// This code is contributed by Vivekkumar Singh
```

## 蟒蛇 3

```
# Python3 program to implement XOR - Encryption

# The same function is used to encrypt and
# decrypt
def encryptDecrypt(inpString):

    # Define XOR key
    # Any character value will work
    xorKey = 'P';

    # calculate length of input string
    length = len(inpString);

    # perform XOR operation of key
    # with every character in string
    for i in range(length):

        inpString = (inpString[:i] +
             chr(ord(inpString[i]) ^ ord(xorKey)) +
                     inpString[i + 1:]);
        print(inpString[i], end = "");

    return inpString;

# Driver Code
if __name__ == '__main__':
    sampleString = "GeeksforGeeks";

    # Encrypt the string
    print("Encrypted String: ", end = "");
    sampleString = encryptDecrypt(sampleString);
    print("\n");

    # Decrypt the string
    print("Decrypted String: ", end = "");
    encryptDecrypt(sampleString);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to implement XOR - Encryption
using System;

public class XOREncryption
{
    // The same function is used to encrypt and
    // decrypt
    static String encryptDecrypt(String inputString)
    {
        // Define XOR key
        // Any character value will work
        char xorKey = 'P';

        // Define String to store encrypted/decrypted String
        String outputString = "";

        // calculate length of input string
        int len = inputString.Length;

        // perform XOR operation of key
        // with every character in string
        for (int i = 0; i < len; i++)
        {
            outputString = outputString +
            char.ToString((char) (inputString[i] ^ xorKey));
        }

        Console.WriteLine(outputString);
        return outputString;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String sampleString = "GeeksforGeeks";

        // Encrypt the string
        Console.WriteLine("Encrypted String");
        String encryptedString = encryptDecrypt(sampleString);

        // Decrypt the string
        Console.WriteLine("Decrypted String");
        encryptDecrypt(encryptedString);
    }
}

// This code has been contributed by 29AjayKumar
```

**输出:**

```
Encrypted String: 55;#6?"55;#
Decrypted String: GeeksforGeeks
```

异或加密背后的基本思想是，如果在解密加密数据之前不知道异或加密密钥，就不可能解密数据。例如，如果你对两个未知变量进行异或运算，你就无法知道这些变量的输出是什么。考虑操作 A 异或 B，这返回真。现在，如果一个变量的值已知，我们就可以知道另一个变量的值。根据布尔异或运算的性质，如果 A 为真，那么 B 应该为假，或者如果 A 为假，那么 B 应该为真。在不知道其中一个值的情况下，我们无法解密数据，这个想法被用于异或加密。

**相关文章:**
[维根内尔密码](https://www.geeksforgeeks.org/vigenere-cipher/)
[凯撒密码](https://www.geeksforgeeks.org/caesar-cipher/)
本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。