# 写一个高效的 C 程序来反转一个数的位

> 原文:[https://www . geesforgeks . org/write-a-a-efficient-c-program-to-reverse-bit-of-a-number/](https://www.geeksforgeeks.org/write-an-efficient-c-program-to-reverse-bits-of-a-number/)

给定一个无符号整数，反转它的所有位，并返回具有反转位的数字。

```
Input : n = 1
Output : 2147483648  
On a machine with size of unsigned
bit as 32\. Reverse of 0....001 is
100....0.

Input : n = 2147483648
Output : 1                          

```

**方法 1–简单**
循环遍历整数的所有位。如果在 i/p 号中设置了第 I 个位置的位，则将该位设置为(NO_OF_BITS–1)–I in o/p，其中 NO _ OF _ BITS 是给定数字中的位数。

```
/* Function to reverse bits of num */
unsigned int reverseBits(unsigned int num)
{
    unsigned int  NO_OF_BITS = sizeof(num) * 8;
    unsigned int reverse_num = 0, i, temp;

    for (i = 0; i < NO_OF_BITS; i++)
    {
        temp = (num & (1 << i));
        if(temp)
            reverse_num |= (1 << ((NO_OF_BITS - 1) - i));
    }

    return reverse_num;
}

/* Driver function to test above function */
int main()
{
    unsigned int x = 2; 
    printf("%u", reverseBits(x));
    getchar();
}
```

上述程序可以通过取消使用变量 temp 来优化。见下面修改后的代码。

```
unsigned int reverseBits(unsigned int num)
{
    unsigned int  NO_OF_BITS = sizeof(num) * 8;
    unsigned int reverse_num = 0;
    int i;
    for (i = 0; i < NO_OF_BITS; i++)
    {
        if((num & (1 << i)))
           reverse_num |= 1 << ((NO_OF_BITS - 1) - i);  
   }
    return reverse_num;
}
```

时间复杂度:O(n)
空间复杂度:O(1)

**方法 2–标准**
想法是将 num 的设定位保持在 reverse_num，直到 num 变为零。num 变为零后，移位 reverse_num 的剩余位。

让 num 用 8 位存储，num 为 00000110。循环之后，您将得到 reverse_num 作为 00000011。现在，您需要再向左移动 reverse_num 5 次，您将得到精确的 reverse 01100000。

```
unsigned int reverseBits(unsigned int num)
{
    unsigned int count = sizeof(num) * 8 - 1;
    unsigned int reverse_num = num;

    num >>= 1; 
    while(num)
    {
       reverse_num <<= 1;       
       reverse_num |= num & 1;
       num >>= 1;
       count--;
    }
    reverse_num <<= count;
    return reverse_num;
}

int main()
{
    unsigned int x = 1;
    printf("%u", reverseBits(x));
    getchar();
}
```

时间复杂度:O(log n)
空间复杂度:O(1)

**方法 3–查找表:**
如果我们知道一个数字的大小，我们可以将它的位反转为 O(1)。我们可以使用查找表来实现它。详见 O(1)时间中[使用查找表反位。](https://www.geeksforgeeks.org/reverse-bits-using-lookup-table-in-o1-time/)

**来源:**T2[https://graphics.stanford.edu/~seander/bithacks.html](https://graphics.stanford.edu/~seander/bithacks.html)