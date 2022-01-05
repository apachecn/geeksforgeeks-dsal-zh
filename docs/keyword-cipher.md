# 关键词密码

> 原文:[https://www.geeksforgeeks.org/keyword-cipher/](https://www.geeksforgeeks.org/keyword-cipher/)

关键词密码是[单字母替换](https://en.wikipedia.org/wiki/Monoalphabetic_substitution)的一种形式。关键字被用作密钥，它决定了密码字母表与普通字母表的字母匹配。删除单词中重复的字母，然后生成关键字与 A、B、C 等匹配的密码字母表。直到关键字用完，然后剩余的密文字母按字母顺序使用，不包括那些已经在关键字中使用的字母。

**加密**

输入的第一行包含您想要输入的关键字。第二行输入包含您必须加密的字符串。
**明文:**A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
**加密:**K R Y P T O S A B C D E F G H I J L M N Q U V W X Z
以氪星为关键字，all As 变成 Ks，all Bs 变成 R S，以此类推。使用关键字“Kryptos”加密消息“知识就是力量”:
加密消息:知识就是力量
编码消息:IlmWjbaEb GQ NmWbp
**示例:**

```
Input :
Keyword : secret
Message : Zombie Here
Output :
Ciphered String : ZLJEFT DTOT

Take the first example, we used "secret" keyword there.
Plain Text : A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
When "secret" keyword is used, the new encypting text becomes :
Encrypting : S E C R T A B D F G H I J K L M N O P Q U V W X Y Z
This means 'A' means 'S', 'B' means 'E' and 'C' means 'C' and so on.
Lets encode the given message "Zombie Here"
ZOMBIE HERE becomes ZLJEFT DTOT

Input :
Keyword : Star War
Message : Attack at dawn
Output :
Ciphered String : SPPSAG SP RSVJ
```

该方法需要注意的几点:

*   所有消息都用大写字母编码。
*   空白、特殊字符和数字不考虑关键字，尽管你可以把它们放进去。
*   加密邮件时，空白、特殊字符和数字不受影响。

## C++

```
// CPP program for encoding the string
// using classical cipher

#include<bits/stdc++.h>
using namespace std;

// Function generates the encoded text
string encoder(string key)
{
    string encoded = "";
    // This array represents the
    // 26 letters of alphabets
    bool arr[26] = {0};

    // This loop inserts the keyword
    // at the start of the encoded string
    for (int i=0; i<key.size(); i++)
    {
        if(key[i] >= 'A' && key[i] <= 'Z')
        {
            // To check whether the character is inserted
            // earlier in the encoded string or not
            if (arr[key[i]-65] == 0)
            {
                encoded += key[i];
                arr[key[i]-65] = 1;
            }
        }
        else if (key[i] >= 'a' && key[i] <= 'z')
        {
            if (arr[key[i]-97] == 0)
            {
                encoded += key[i] - 32;
                arr[key[i]-97] = 1;
            }
        }
    }

    // This loop inserts the remaining
    // characters in the encoded string.
    for (int i=0; i<26; i++)
    {
        if(arr[i] == 0)
        {
            arr[i]=1;
            encoded += char(i + 65);
        }
    }
    return encoded;
}

// Function that generates encodes(cipher) the message
string cipheredIt(string msg, string encoded)
{
    string cipher="";

    // This loop ciphered the message.
    // Spaces, special characters and numbers remain same.
    for (int i=0; i<msg.size(); i++)
    {
        if (msg[i] >='a' && msg[i] <='z')
        {
            int pos = msg[i] - 97;
            cipher += encoded[pos];
        }
        else if (msg[i] >='A' && msg[i] <='Z')
        {
            int pos = msg[i] - 65;
            cipher += encoded[pos];
        }
        else
        {
            cipher += msg[i];
        }
    }
    return cipher;
}

// Driver code
int main()
{
    // Hold the Keyword
    string key;
    key = "Computer";
    cout << "Keyword : " <<key << endl;

    // Function call to generate encoded text
    string encoded = encoder(key);

    // Message that need to encode
    string message = "GeeksforGeeks";
    cout << "Message before Ciphering : " << message << endl;

    // Function call to print ciphered text
    cout << "Ciphered Text : " << cipheredIt(message,encoded) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for encoding the string
// using classical cipher

class GFG
{

    // Function generates the encoded text
    static String encoder(char[] key)
    {
        String encoded = "";

        // This array represents the
        // 26 letters of alphabets
        boolean[] arr = new boolean[26];

        // This loop inserts the keyword
        // at the start of the encoded string
        for (int i = 0; i < key.length; i++)
        {
            if (key[i] >= 'A' && key[i] <= 'Z')
            {
                // To check whether the character is inserted
                // earlier in the encoded string or not
                if (arr[key[i] - 65] == false)
                {
                    encoded += (char) key[i];
                    arr[key[i] - 65] = true;
                }
            }
            else if (key[i] >= 'a' && key[i] <= 'z')
            {
                if (arr[key[i] - 97] == false)
                {
                    encoded += (char) (key[i] - 32);
                    arr[key[i] - 97] = true;
                }
            }
        }

        // This loop inserts the remaining
        // characters in the encoded string.
        for (int i = 0; i < 26; i++)
        {
            if (arr[i] == false)
            {
                arr[i] = true;
                encoded += (char) (i + 65);
            }
        }
        return encoded;
    }

    // Function that generates encodes(cipher) the message
    static String cipheredIt(String msg, String encoded)
    {
        String cipher = "";

        // This loop ciphered the message.
        // Spaces, special characters and numbers remain same.
        for (int i = 0; i < msg.length(); i++)
        {
            if (msg.charAt(i) >= 'a' && msg.charAt(i) <= 'z')
            {
                int pos = msg.charAt(i) - 97;
                cipher += encoded.charAt(pos);
            }
            else if (msg.charAt(i) >= 'A' && msg.charAt(i) <= 'Z')
            {
                int pos = msg.charAt(i) - 65;
                cipher += encoded.charAt(pos);
            }
            else
            {
                cipher += msg.charAt(i);
            }
        }
        return cipher;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Hold the Keyword
        String key;
        key = "Computer";
        System.out.println("Keyword : " + key);

        // Function call to generate encoded text
        String encoded = encoder(key.toCharArray());

        // Message that need to encode
        String message = "GeeksforGeeks";
        System.out.println("Message before Ciphering : " + message);

        // Function call to print ciphered text
        System.out.println("Ciphered Text : " + cipheredIt(message,
                encoded));
    }
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for encoding the string
// using classical cipher
using System;

class GFG
{

    // Function generates the encoded text
    static String encoder(char[] key)
    {
        String encoded = "";

        // This array represents the
        // 26 letters of alphabets
        Boolean[] arr = new Boolean[26];

        // This loop inserts the keyword
        // at the start of the encoded string
        for (int i = 0; i < key.Length; i++)
        {
            if (key[i] >= 'A' && key[i] <= 'Z')
            {
                // To check whether the character is inserted
                // earlier in the encoded string or not
                if (arr[key[i] - 65] == false)
                {
                    encoded += (char) key[i];
                    arr[key[i] - 65] = true;
                }
            }
            else if (key[i] >= 'a' && key[i] <= 'z')
            {
                if (arr[key[i] - 97] == false)
                {
                    encoded += (char) (key[i] - 32);
                    arr[key[i] - 97] = true;
                }
            }
        }

        // This loop inserts the remaining
        // characters in the encoded string.
        for (int i = 0; i < 26; i++)
        {
            if (arr[i] == false)
            {
                arr[i] = true;
                encoded += (char) (i + 65);
            }
        }
        return encoded;
    }

    // Function that generates encodes(cipher) the message
    static String cipheredIt(String msg, String encoded)
    {
        String cipher = "";

        // This loop ciphered the message.
        // Spaces, special characters and numbers remain same.
        for (int i = 0; i < msg.Length; i++)
        {
            if (msg[i] >= 'a' && msg[i] <= 'z')
            {
                int pos = msg[i] - 97;
                cipher += encoded[pos];
            }
            else if (msg[i] >= 'A' && msg[i] <= 'Z')
            {
                int pos = msg[i] - 65;
                cipher += encoded[pos];
            }
            else
            {
                cipher += msg[i];
            }
        }
        return cipher;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Hold the Keyword
        String key;
        key = "Computer";
        Console.WriteLine("Keyword : " + key);

        // Function call to generate encoded text
        String encoded = encoder(key.ToCharArray());

        // Message that need to encode
        String message = "GeeksforGeeks";
        Console.WriteLine("Message before Ciphering : " + message);

        // Function call to print ciphered text
        Console.WriteLine("Ciphered Text : " + cipheredIt(message,
                encoded));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program for encoding the string
// using classical cipher

// Function generates the encoded text
function encoder(key)
{
    let encoded = "";

        // This array represents the
        // 26 letters of alphabets
        let arr = new Array(26);
        for(let i=0;i<26;i++)
        {
            arr[i]=false;
        }

        // This loop inserts the keyword
        // at the start of the encoded string
        for (let i = 0; i < key.length; i++)
        {
            if (key[i].charCodeAt(0) >= 'A'.charCodeAt(0) &&
            key[i].charCodeAt(0) <= 'Z'.charCodeAt(0))
            {
                // To check whether the character is inserted
                // earlier in the encoded string or not
                if (arr[key[i].charCodeAt(0) - 65] == false)
                {
                    encoded += ( key[i]);
                    arr[key[i].charCodeAt(0) - 65] = true;
                }
            }
            else if (key[i].charCodeAt(0) >= 'a'.charCodeAt(0) &&
            key[i].charCodeAt(0) <= 'z'.charCodeAt(0))
            {
                if (arr[key[i].charCodeAt(0) - 97] == false)
                {
                    encoded +=
                    String.fromCharCode(key[i].charCodeAt(0) - 32);
                    arr[key[i].charCodeAt(0) - 97] = true;
                }
            }
        }

        // This loop inserts the remaining
        // characters in the encoded string.
        for (let i = 0; i < 26; i++)
        {
            if (arr[i] == false)
            {
                arr[i] = true;
                encoded += String.fromCharCode(i + 65);
            }
        }
        return encoded;
}

// Function that generates encodes(cipher) the message
function cipheredIt(msg,encoded)
{
     let cipher = "";

        // This loop ciphered the message.
        // Spaces, special characters and numbers remain same.
        for (let i = 0; i < msg.length; i++)
        {
            if (msg[i] >= 'a' && msg[i] <= 'z')
            {
                let pos = msg[i].charCodeAt(0) - 97;
                cipher += encoded[pos];
            }
            else if (msg[i] >= 'A' && msg[i] <= 'Z')
            {
                let pos = msg[i].charCodeAt(0) - 65;
                cipher += encoded[pos];
            }
            else
            {
                cipher += msg[i];
            }

        }
        return cipher;
}

// Driver code
// Hold the Keyword
let key;
key = "Computer";
document.write("Keyword : " + key+"<br>");

// Function call to generate encoded text
let encoded = encoder(key.split(""));

// Message that need to encode
let message = "GeeksforGeeks";
document.write("Message before Ciphering : " + message+"<br>");

// Function call to print ciphered text
document.write("Ciphered Text : " + cipheredIt(message,
                                                   encoded));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Keyword : Computer
Message before Ciphering : GeeksforGeeks
Ciphered Text : EUUDNTILEUUDN
```

**解密**

要解码消息，您需要检查给定消息在纯文本加密文本中的位置。
**明文:**A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
**加密:**K R Y P T O S A B C D E F G H I J L M N Q U V W X Z
消息:PTYBIATLEP
破译文本:破译
现在，我们如何生成破译字符串？
我们在加密文本中搜索“P”，并将其位置与纯文本字母进行比较，然后生成该字母。所以“P”变成“D”，“T”变成“E”，“Y”变成“C”等等。
**举例:**

```
Input :
Keyword : secret
Message : zljeft dtOT
Output :
Deciphered String : ZOMBIE HERE

Input :
Keyword : joker0O7hack123
Message : QjTijl
Output :
Deciphered String : BATMAN
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program for decoding the string
// which generate using classical cipher

#include<bits/stdc++.h>
using namespace std;

// Original Set of letters
string plaintext = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Function generates the encoded text
string encoder(string key)
{
    string encoded = "";
    bool arr[26] = {0};

    // This loop inserts the keyword
    // at the start of the encoded string
    for (int i=0; i<key.size(); i++)
    {
        if(key[i] >= 'A' && key[i] <= 'Z')
        {
            // To check whether the character is inserted
            // earlier in the encoded string or not
            if (arr[key[i]-65] == 0)
            {
                encoded += key[i];
                arr[key[i]-65] = 1;
            }
        }
        else if (key[i] >= 'a' && key[i] <= 'z')
        {
            if (arr[key[i]-97] == 0)
            {
                encoded += key[i] - 32;
                arr[key[i]-97] = 1;
            }
        }
    }

    // This loop inserts the remaining
    // characters in the encoded string.
    for (int i=0; i<26; i++)
    {
        if(arr[i] == 0)
        {
            arr[i]=1;
            encoded += char(i + 65);
        }
    }
    return encoded;
}

// This function will decode the message
string decipheredIt(string msg, string encoded)
{
    // Hold the position of every character (A-Z)
    // from encoded string
    map <char,int> enc;
    for(int i=0; i<encoded.size(); i++)
    {
        enc[encoded[i]]=i;
    }

    string decipher="";

    // This loop deciphered the message.
    // Spaces, special characters and numbers remain same.
    for (int i=0; i<msg.size(); i++)
    {
        if (msg[i] >='a' && msg[i] <='z')
        {
            int pos = enc[msg[i]-32];
            decipher += plaintext[pos];
        }
        else if(msg[i] >='A' && msg[i] <='Z')
        {
            int pos = enc[msg[i]];
            decipher += plaintext[pos];
        }
        else
        {
            decipher += msg[i];
        }
    }
    return decipher;
}

// Driver code
int main()
{
    // Hold the Keyword
    string key;
    key = "Computer";
    cout << "Keyword : "<< key << endl;

    // Function call to generate encoded text
    string encoded = encoder(key);

    // Message that need to decode
    string message = "EUUDN TIL EUUDN";
    cout << "Message before Deciphering : " << message << endl;

    // Function call to print deciphered text
    cout << "Deciphered Text : " << decipheredIt(message,encoded) << endl;

    return 0;
}
```

输出:

```
Keyword : Computer
Message before Deciphering : EUUDN TIL EUUDN
Deciphered Text : GEEKS FOR GEEKS
```

你也可以**改进**这个经典密码:关键字。这里我们只取纯文本的 A-Z。您也可以考虑大写字母、小写字母和数字。
**攻击关键词密码的方法:**在不知道关键词的情况下攻击关键词密码的最佳方法是通过已知明文**攻击**、**频率分析**，以及发现关键词(通常密码分析者会将这三种技术结合起来)。**关键字发现**允许立即解密，因为该表可以立即制作。
本文由**沙钦·毕斯特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。