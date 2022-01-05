# 柱状换位密码

> 原文:[https://www . geesforgeks . org/column-transposition-cipher/](https://www.geeksforgeeks.org/columnar-transposition-cipher/)

给定一条纯文本消息和一个数字密钥，使用柱状置换密码对给定文本进行加密/解密

柱状换位密码是换位密码的一种形式，就像[围栏密码](https://www.geeksforgeeks.org/rail-fence-cipher-encryption-decryption/)一样。列转置包括逐行写出明文，然后逐列读出密文。

**示例:**

```
Encryption
Input : Geeks for Geeks
Key = HACK
Output : e  kefGsGsrekoe_
Decryption
Input : e  kefGsGsrekoe_
Key = HACK
Output : Geeks for Geeks 

Encryption
Input :  Geeks on work
Key = HACK
Output : e w_eoo_Gs kknr_
Decryption
Input : e w_eoo_Gs kknr_
Key = HACK
Output : Geeks on work

```

**加密**

在换位密码中，字母的顺序被重新排列以获得密码文本。

1.  消息以固定长度的行写出，然后逐列再次读出，列以某种加扰的顺序选择。
2.  行的宽度和列的排列通常由关键字定义。
3.  例如，单词 HACK 的长度为 4(因此行的长度为 4)，排列由关键字中字母的字母顺序定义。在这种情况下，顺序是“3 1 2 4”。
4.  任何备用空间都用空值填充，或者留空，或者用字符放置(例如:_)。
5.  最后，按照关键字指定的顺序，按列读取消息。

[![columnar-transposition-cipher](img/7292bf8ea0f3d6cd468ea3eb5a1a2c5f.png)](https://media.geeksforgeeks.org/wp-content/uploads/columnar-transposition-cipher1.png)

**解密**

1.  为了破译它，接收者必须通过将消息长度除以密钥长度来计算出列长度。
2.  Then, write the message out in columns again, then re-order the columns by reforming the key word.

    ## C++

    ```
    // CPP program for illustrating
    // Columnar Transposition Cipher
    #include<bits/stdc++.h>
    using namespace std;

    // Key for Columnar Transposition
    string const key = "HACK"; 
    map<int,int> keyMap;

    void setPermutationOrder()
    {             
        // Add the permutation order into map 
        for(int i=0; i < key.length(); i++)
        {
            keyMap[key[i]] = i;
        }
    }

    // Encryption 
    string encryptMessage(string msg)
    {
        int row,col,j;
        string cipher = "";

        /* calculate column of the matrix*/
        col = key.length(); 

        /* calculate Maximum row of the matrix*/
        row = msg.length()/col; 

        if (msg.length() % col)
            row += 1;

        char matrix[row][col];

        for (int i=0,k=0; i < row; i++)
        {
            for (int j=0; j<col; )
            {
                if(msg[k] == '\0')
                {
                    /* Adding the padding character '_' */
                    matrix[i][j] = '_';     
                    j++;
                }

                if( isalpha(msg[k]) || msg[k]==' ')
                { 
                    /* Adding only space and alphabet into matrix*/
                    matrix[i][j] = msg[k];
                    j++;
                }
                k++;
            }
        }

        for (map<int,int>::iterator ii = keyMap.begin(); ii!=keyMap.end(); ++ii)
        {
            j=ii->second;

            // getting cipher text from matrix column wise using permuted key
            for (int i=0; i<row; i++)
            {
                if( isalpha(matrix[i][j]) || matrix[i][j]==' ' || matrix[i][j]=='_')
                    cipher += matrix[i][j];
            }
        }

        return cipher;
    }

    // Decryption 
    string decryptMessage(string cipher)
    {
        /* calculate row and column for cipher Matrix */
        int col = key.length();

        int row = cipher.length()/col;
        char cipherMat[row][col];

        /* add character into matrix column wise */
        for (int j=0,k=0; j<col; j++)
            for (int i=0; i<row; i++)
                cipherMat[i][j] = cipher[k++];

        /* update the order of key for decryption */
        int index = 0;
        for( map<int,int>::iterator ii=keyMap.begin(); ii!=keyMap.end(); ++ii)
            ii->second = index++;

        /* Arrange the matrix column wise according 
        to permutation order by adding into new matrix */
        char decCipher[row][col];
        map<int,int>::iterator ii=keyMap.begin();
        int k = 0;
        for (int l=0,j; key[l]!='\0'; k++)
        {
            j = keyMap[key[l++]];
            for (int i=0; i<row; i++)
            {
                decCipher[i][k]=cipherMat[i][j];
            }
        }

        /* getting Message using matrix */
        string msg = "";
        for (int i=0; i<row; i++)
        {
            for(int j=0; j<col; j++)
            {
                if(decCipher[i][j] != '_')
                    msg += decCipher[i][j];
            }
        }
        return msg;
    }

    // Driver Program
    int main(void)
    {
        /* message */
        string msg = "Geeks for Geeks"; 

        setPermutationOrder();

        // Calling encryption function
        string cipher = encryptMessage(msg);
        cout << "Encrypted Message: " << cipher << endl;

        // Calling Decryption function
        cout << "Decrypted Message: " << decryptMessage(cipher) << endl;

        return 0;
    }
    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation of 
    # Columnar Transposition
    import math

    key = "HACK"

    # Encryption
    def encryptMessage(msg):
        cipher = ""

        # track key indices
        k_indx = 0

        msg_len = float(len(msg))
        msg_lst = list(msg)
        key_lst = sorted(list(key))

        # calculate column of the matrix
        col = len(key)

        # calculate maximum row of the matrix
        row = int(math.ceil(msg_len / col))

        # add the padding character '_' in empty
        # the empty cell of the matix 
        fill_null = int((row * col) - msg_len)
        msg_lst.extend('_' * fill_null)

        # create Matrix and insert message and 
        # padding characters row-wise 
        matrix = [msg_lst[i: i + col] 
                  for i in range(0, len(msg_lst), col)]

        # read matrix column-wise using key
        for _ in range(col):
            curr_idx = key.index(key_lst[k_indx])
            cipher += ''.join([row[curr_idx] 
                              for row in matrix])
            k_indx += 1

        return cipher

    # Decryption
    def decryptMessage(cipher):
        msg = ""

        # track key indices
        k_indx = 0

        # track msg indices
        msg_indx = 0
        msg_len = float(len(cipher))
        msg_lst = list(cipher)

        # calculate column of the matrix
        col = len(key)

        # calculate maximum row of the matrix
        row = int(math.ceil(msg_len / col))

        # convert key into list and sort 
        # alphabetically so we can access 
        # each character by its alphabetical position.
        key_lst = sorted(list(key))

        # create an empty matrix to 
        # store deciphered message
        dec_cipher = []
        for _ in range(row):
            dec_cipher += [[None] * col]

        # Arrange the matrix column wise according 
        # to permutation order by adding into new matrix
        for _ in range(col):
            curr_idx = key.index(key_lst[k_indx])

            for j in range(row):
                dec_cipher[j][curr_idx] = msg_lst[msg_indx]
                msg_indx += 1
            k_indx += 1

        # convert decrypted msg matrix into a string
        try:
            msg = ''.join(sum(dec_cipher, []))
        except TypeError:
            raise TypeError("This program cannot",
                            "handle repeating words.")

        null_count = msg.count('_')

        if null_count > 0:
            return msg[: -null_count]

        return msg

    # Driver Code
    msg = "Geeks for Geeks"

    cipher = encryptMessage(msg)
    print("Encrypted Message: {}".
                   format(cipher))

    print("Decryped Message: {}".
           format(decryptMessage(cipher)))

    # This code is contributed by Aditya K
    ```

    **Output:**

    ```
    Encrypted Message: e  kefGsGsrekoe_
    Decrypted Message: Geeks for Geeks

    ```

    **自己试试:**双柱状换位(一战美军就用过，只是一个柱状换位后再来一个柱状换位)。

    本文由**亚辛·扎法尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。