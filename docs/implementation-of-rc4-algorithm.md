# RC4 算法的实现

> 原文:[https://www . geeksforgeeks . org/implementation-of-RC4-algorithm/](https://www.geeksforgeeks.org/implementation-of-rc4-algorithm/)

[RC4](https://www.geeksforgeeks.org/rc4-encryption-algorithm/) 是一种对称流密码和变密钥长度算法。这种对称密钥算法同样用于[加密和解密](https://www.geeksforgeeks.org/difference-between-encryption-and-decryption/)，这样数据流只需用生成的密钥序列[异或](https://www.geeksforgeeks.org/xor-encryption-shifting-plaintext/)。该算法是串行的，因为它需要基于密钥序列连续交换状态条目。该算法分两个阶段工作:

**<u>关键调度算法(KSA)</u> :**

*   它用于通过使用由 **0** 到 **256 字节**组成的可变长度密钥应用排列来生成状态数组。
*   状态向量被标识为 **S[0]** 、 **S[1]…。S[255]** 用 **{0，1，2，…，255}** 初始化。按键 **K[0]** 、 **K[1]、…。，K[255]** 可以是从 **0** 到 **256 字节**的任意长度，用于初始化置换 S，每个 K[I]和 S[I]都是一个字节。
*   如果密钥长度为 256 字节，则 K 是一个临时数组，复制后将其复制到 K，否则 K 的剩余位置将被重复的密钥值填充，直到填满。

```
S[] is permutation of 0, 1, ..., 255
key[] contains N bytes of key

for i = 0 to 255
    S[i] = i

    // Selects a keystream byte from
    // the table
    K[i] = key[i (mod N)]
    i++
j = 0

for i = 0 to 255
    j = (j + S[i] + K[i]) mod 256

    // Swaps elements in the current
    // lookup table
    swap(S[i], S[j])
i = j = 0
```

**<u>伪随机生成算法(PRGA)</u> :** 用于多一轮置换后从状态向量数组生成密钥流字节。

```
Keystream Generation(i := 0, j := 0 )

while Generating Output:
    i = (i + 1) mod 256
    j = (j + S[i]) mod 256
    swap(S[i], S[j])
    t = (S[i] + S[j]) mod 256
    keystreamByte = S[t]

At each iteration, swap elements in table
and select keystream byte
```

然后，对生成的密钥流和用于加密的纯文本进行异或运算。

解密时遵循与上面相同的过程，用密文代替明文。

**示例:**

> **输入:**纯文本= 001010010010，密钥= 10100100001，n= 3
> **输出:**
> 密文= 110011100011
> 解密文本= 001010010010
> 
> **输入:**纯文本= 11110000000001111，密钥= 0101011001010，n= 4
> **输出:**
> 密文= 00110110100010
> 解密文本= 1111000000000111

下面是上述方法的实现，详细输出了所有涉及的重要步骤:

## 蟒蛇 3

```
# Python3 program for the above approach
# of RC4 algorithm

# Function for encryption
def encryption():

    global key, plain_text, n

    # Given text and key
    plain_text = "001010010010"
    key = "101001000001"

    # n is the no: of bits to
    # be considered at a time
    n = 3

    print("Plain text : ", plain_text)
    print("Key : ", key)
    print("n : ", n)

    print(" ")

    # The initial state vector array
    S = [i for i in range(0, 2**n)]
    print("S : ", S)

    key_list = [key[i:i + n] for i in range(0, len(key), n)]

    # Convert to key_stream to decimal
    for i in range(len(key_list)):
        key_list[i] = int(key_list[i], 2)

    # Convert to plain_text to decimal
    global pt

    pt = [plain_text[i:i + n] for i in range(0, len(plain_text), n)]

    for i in range(len(pt)):
        pt[i] = int(pt[i], 2)

    print("Plain text ( in array form ): ", pt)

    # Making key_stream equal
    # to length of state vector
    diff = int(len(S)-len(key_list))

    if diff != 0:
        for i in range(0, diff):
            key_list.append(key_list[i])

    print("Key list : ", key_list)
    print(" ")

    # Perform the KSA algorithm
    def KSA():
        j = 0
        N = len(S)

        # Iterate over the range [0, N]
        for i in range(0, N):

            # Find the key
            j = (j + S[i]+key_list[i]) % N

            # Update S[i] and S[j]
            S[i], S[j] = S[j], S[i]
            print(i, " ", end ="")

            # Print S
            print(S)

        initial_permutation_array = S

        print(" ")
        print("The initial permutation array is : ",
              initial_permutation_array)

    print("KSA iterations : ")
    print(" ")
    KSA()
    print(" ")

    # Perform PGRA algorithm
    def PGRA():

        N = len(S)
        i = j = 0
        global key_stream
        key_stream = []

        # Iterate over [0, length of pt]
        for k in range(0, len(pt)):
            i = (i + 1) % N
            j = (j + S[i]) % N

            # Update S[i] and S[j]
            S[i], S[j] = S[j], S[i]
            print(k, " ", end ="")
            print(S)
            t = (S[i]+S[j]) % N
            key_stream.append(S[t])

        # Print the key stream
        print("Key stream : ", key_stream)
        print(" ")

    print("PGRA iterations : ")
    print(" ")
    PGRA()

    # Performing XOR between generated
    # key stream and plain text
    def XOR():
        global cipher_text
        cipher_text = []
        for i in range(len(pt)):
            c = key_stream[i] ^ pt[i]
            cipher_text.append(c)

    XOR()

    # Convert the encrypted text to
    # bits form
    encrypted_to_bits = ""
    for i in cipher_text:
        encrypted_to_bits += '0'*(n-len(bin(i)[2:]))+bin(i)[2:]

    print(" ")
    print("Cipher text : ", encrypted_to_bits)

encryption()

print("---------------------------------------------------------")

# Function for decryption of data
def decryption():

    # The initial state vector array
    S = [i for i in range(0, 2**n)]

    key_list = [key[i:i + n] for i in range(0, len(key), n)]

    # Convert to key_stream to decimal
    for i in range(len(key_list)):
        key_list[i] = int(key_list[i], 2)

    # Convert to plain_text to decimal
    global pt

    pt = [plain_text[i:i + n] for i in range(0, len(plain_text), n)]

    for i in range(len(pt)):
        pt[i] = int(pt[i], 2)

    # making key_stream equal
    # to length of state vector
    diff = int(len(S)-len(key_list))

    if diff != 0:
        for i in range(0, diff):
            key_list.append(key_list[i])

    print(" ")

    # KSA algorithm
    def KSA():
        j = 0
        N = len(S)

        # Iterate over the range [0, N]
        for i in range(0, N):
            j = (j + S[i]+key_list[i]) % N

            # Update S[i] and S[j]
            S[i], S[j] = S[j], S[i]
            print(i, " ", end ="")
            print(S)

        initial_permutation_array = S
        print(" ")
        print("The initial permutation array is : ",
              initial_permutation_array)

    print("KSA iterations : ")
    print(" ")
    KSA()
    print(" ")

    # Perform PRGA algorithm
    def do_PGRA():

        N = len(S)
        i = j = 0
        global key_stream
        key_stream = []

        # Iterate over the range
        for k in range(0, len(pt)):
            i = (i + 1) % N
            j = (j + S[i]) % N

            # Update S[i] and S[j]
            S[i], S[j] = S[j], S[i]
            print(k, " ", end ="")
            print(S)
            t = (S[i]+S[j]) % N
            key_stream.append(S[t])

    print("Key stream : ", key_stream)
    print(" ")

    print("PGRA iterations : ")
    print(" ")
    do_PGRA()

    # Perform XOR between generated
    # key stream  and cipher text
    def do_XOR():
        global original_text
        original_text = []
        for i in range(len(cipher_text)):
            p = key_stream[i] ^ cipher_text[i]
            original_text.append(p)

    do_XOR()

    # convert the decrypted text to
    # the bits form
    decrypted_to_bits = ""
    for i in original_text:
        decrypted_to_bits += '0'*(n-len(bin(i)[2:]))+bin(i)[2:]

    print(" ")
    print("Decrypted text : ",
          decrypted_to_bits)

# Driver Code
decryption()
```

**Output:** 

```
Plain text :  001010010010
Key :  101001000001
n :  3

S :  [0, 1, 2, 3, 4, 5, 6, 7]
Plain text ( in array form ):  [1, 2, 2, 2]
Key list :  [5, 1, 0, 1, 5, 1, 0, 1]

KSA iterations : 

0  [5, 1, 2, 3, 4, 0, 6, 7]
1  [5, 7, 2, 3, 4, 0, 6, 1]
2  [5, 2, 7, 3, 4, 0, 6, 1]
3  [5, 2, 7, 0, 4, 3, 6, 1]
4  [5, 2, 7, 0, 6, 3, 4, 1]
5  [5, 2, 3, 0, 6, 7, 4, 1]
6  [5, 2, 3, 0, 6, 7, 4, 1]
7  [1, 2, 3, 0, 6, 7, 4, 5]

The initial permutation array is :  [1, 2, 3, 0, 6, 7, 4, 5]

PGRA iterations : 

0  [1, 3, 2, 0, 6, 7, 4, 5]
1  [1, 3, 6, 0, 2, 7, 4, 5]
2  [1, 3, 6, 2, 0, 7, 4, 5]
3  [1, 3, 6, 2, 0, 7, 4, 5]
Key stream :  [7, 1, 6, 1]

Cipher text :  110011100011
---------------------------------------------------------

KSA iterations : 

0  [5, 1, 2, 3, 4, 0, 6, 7]
1  [5, 7, 2, 3, 4, 0, 6, 1]
2  [5, 2, 7, 3, 4, 0, 6, 1]
3  [5, 2, 7, 0, 4, 3, 6, 1]
4  [5, 2, 7, 0, 6, 3, 4, 1]
5  [5, 2, 3, 0, 6, 7, 4, 1]
6  [5, 2, 3, 0, 6, 7, 4, 1]
7  [1, 2, 3, 0, 6, 7, 4, 5]

The initial permutation array is :  [1, 2, 3, 0, 6, 7, 4, 5]

Key stream :  [7, 1, 6, 1]

PGRA iterations : 

0  [1, 3, 2, 0, 6, 7, 4, 5]
1  [1, 3, 6, 0, 2, 7, 4, 5]
2  [1, 3, 6, 2, 0, 7, 4, 5]
3  [1, 3, 6, 2, 0, 7, 4, 5]

Decrypted text :  001010010010
```