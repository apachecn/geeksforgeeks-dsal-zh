# Java 中块链的实现

> 原文:[https://www . geeksforgeeks . org/Java 中区块链的实现/](https://www.geeksforgeeks.org/implementation-of-blockchain-in-java/)

[区块链](https://www.geeksforgeeks.org/blockchain-technology-introduction/)是数字密码货币 [比特币](https://www.geeksforgeeks.org/what-is-bitcoin/)的骨干[技术。](https://www.geeksforgeeks.org/what-is-a-cryptocurrency/)

*   区块链是被称为区块的记录列表，它们使用[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)和[加密技术](https://www.geeksforgeeks.org/cryptography-and-its-types/)链接在一起。
*   每个数据块都包含自己的数字指纹 [Hash](https://www.geeksforgeeks.org/hashing-set-1-introduction/) 、前一个数据块的 Hash、时间戳和所做交易的数据，这使得它对任何类型的数据泄露都更加安全。
*   因此，如果一个块的数据改变了，那么它的散列也将改变。如果散列被改变，那么它的散列将不同于包含前一个块的散列的下一个块，影响它之后的块的所有散列。改变哈希值，然后与其他块进行比较，这样我们就可以检查区块链。

**区块链的实现:**以下是在实现区块链中使用的功能。

*   **创建块:**要创建块，需要实现一个**块**类。在“块”类中:
    *   **哈希**将包含块的哈希，并且
    *   **previousHash** 将包含前一个块的 Hash。
    *   字符串**数据**用于存储块的数据
    *   **“长时间戳”**用于存储块的时间戳。这里长数据类型用于存储毫秒数。
    *   **计算哈希()**生成哈希

下面是类块的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for creating
// a block in a Blockchain

import java.util.Date;

public class Block {

    // Every block contains
    // a hash, previous hash and
    // data of the transaction made
    public String hash;
    public String previousHash;
    private String data;
    private long timeStamp;

    // Constructor for the block
    public Block(String data,
                 String previousHash)
    {
        this.data = data;
        this.previousHash
            = previousHash;
        this.timeStamp
            = new Date().getTime();
        this.hash
            = calculateHash();
    }

    // Function to calculate the hash
    public String calculateHash()
    {
        // Calling the "crypt" class
        // to calculate the hash
        // by using the previous hash,
        // timestamp and the data
        String calculatedhash
            = crypt.sha256(
                previousHash
                + Long.toString(timeStamp)
                + data);

        return calculatedhash;
    }
}
```

*   **生成哈希:**要生成哈希，使用 [SHA256](https://www.geeksforgeeks.org/sha-256-hash-in-java/) 算法。
    下面是算法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Generating Hashes

import java.security.MessageDigest;

public class crypt {

    // Function that takes the string input
    // and returns the hashed string.
    public static String sha256(String input)
    {
        try {
            MessageDigest sha
                = MessageDigest
                      .getInstance(
                          "SHA-256");
            int i = 0;

            byte[] hash
                = sha.digest(
                    input.getBytes("UTF-8"));

            // hexHash will contain
            // the Hexadecimal hash
            StringBuffer hexHash
                = new StringBuffer();

            while (i < hash.length) {
                String hex
                    = Integer.toHexString(
                        0xff & hash[i]);
                if (hex.length() == 1)
                    hexHash.append('0');
                hexHash.append(hex);
                i++;
            }

            return hexHash.toString();
        }
        catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
}
```

*   **存储块:**现在，让我们通过调用**块类**的构造函数，将块及其哈希值存储在**块**类型的[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)中。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to store
// blocks in an ArrayList

import java.util.ArrayList;

public class GFG {

    // ArrayList to store the blocks
    public static ArrayList<Block> blockchain
        = new ArrayList<Block>();

    // Driver code
    public static void main(String[] args)
    {
        // Adding the data to the ArrayList
        blockchain.add(new Block(
            "First block", "0"));
        blockchain.add(new Block(
            "Second block",
            blockchain
                .get(blockchain.size() - 1)
                .hash));

        blockchain.add(new Block(
            "Third block",
            blockchain
                .get(blockchain.size() - 1)
                .hash));

        blockchain.add(new Block(
            "Fourth block",
            blockchain
                .get(blockchain.size() - 1)
                .hash));

        blockchain.add(new Block(
            "Fifth block",
            blockchain
                .get(blockchain.size() - 1)
                .hash));
    }
}
```

*   **区块链有效性:**最后，我们需要通过创建一个检查有效性的布尔方法来检查区块链的有效性。此方法将在“Main”类中实现，并检查哈希是否等于计算的哈希。如果所有的散列都等于计算的散列，则该块是有效的。
    以下是有效期的执行情况:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// validity of the blockchain

// Function to check
// validity of the blockchain
public static Boolean isChainValid()
{
    Block currentBlock;
    Block previousBlock;

    // Iterating through
    // all the blocks
    for (int i = 1;
         i < blockchain.size();
         i++) {

        // Storing the current block
        // and the previous block
        currentBlock = blockchain.get(i);
        previousBlock = blockchain.get(i - 1);

        // Checking if the current hash
        // is equal to the
        // calculated hash or not
        if (!currentBlock.hash
                 .equals(
                     currentBlock
                         .calculateHash())) {
            System.out.println(
                "Hashes are not equal");
            return false;
        }

        // Checking of the previous hash
        // is equal to the calculated
        // previous hash or not
        if (!previousBlock
                 .hash
                 .equals(
                     currentBlock
                         .previousHash)) {
            System.out.println(
                "Previous Hashes are not equal");
            return false;
        }
    }

    // If all the hashes are equal
    // to the calculated hashes,
    // then the blockchain is valid
    return true;
}
```

**区块链的优势:**

1.  区块链是[分布式系统网络](https://www.geeksforgeeks.org/comparison-centralized-decentralized-and-distributed-systems/)。因此，数据泄露很难实施。
2.  由于区块链生成了每个区块的哈希，因此很难进行[恶意攻击](https://www.geeksforgeeks.org/basic-network-attacks-in-computer-network/)。
3.  数据篡改将改变每个块的散列，这将使区块链无效