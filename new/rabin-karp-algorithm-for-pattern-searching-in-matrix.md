# 用于矩阵搜索的 Rabin-Karp 算法

给定尺寸为 **m1 x m2** 的矩阵 **txt [] []** 和尺寸为 **n1 x n2** 的图案 **pat [] []** 任务是检查矩阵中是否存在某个模式，如果存在，则在 **txt [] []** 中打印 **pat [] []** 的顶部 mot 索引。 假设 **m1，m2≥n1，n2**

**示例**：

```
Input:
txt[][] = {{G, H, I, P}
           {J, K, L, Q}
           {R, G, H, I}  
           {S, J, K, L}
          }
pat[][] = {{G, H, I},
           {J, K, L}
          }
Output:
Pattern found at ( 0, 0 )
Pattern found at ( 2, 1 )
Explanation:
![](img/9ae378efb0c74ab7f8a71c9c75ef4a0b.png)

Input:
txt[][] = { {A, B, C},
            {D, E, F},
            {G, H, I}
          }
pat[][] = { {E, F},
            {H, I}
          }
Output:
Pattern found at (1, 1)

```

**方法**：为了使用 [Rabin-Karp 算法](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)在二维数组中找到图案，请考虑输入矩阵 **txt [m1] [m2]** 和 模式 **pat [n1] [n2]** 。 这个想法是找到 **mat [] []** 和 **pat [] []** 每列的[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)并比较哈希值。 对于任何列，如果哈希值等于，则检查相应的行值。 步骤如下：

1.  在 **txt [] []** 和 **pat [] []** 矩阵中找到前 **N1** 行的每一列的哈希值。

2.  通过为步骤 1 中找到的列哈希查找哈希值来应用 Rabin-Karp 算法。

3.  如果找到匹配项，则比较特定行和列的 **txt [] []** 和 **pat [] []** 矩阵。

4.  否则，使用[滚动哈希](https://www.geeksforgeeks.org/string-hashing-using-polynomial-rolling-hash-function/)将 txt 矩阵中的列哈希值向下滑动 1 行。

5.  对所有哈希值重复步骤 2 到 4，如果我们在 **txt [] []** 中找到任何 **pat [] []** 匹配项，然后在[ **txt [] []** 。

**查找哈希值**：为了使用滚动哈希在文本中查找大小为 **N** 的子字符串的哈希值，请执行以下步骤：

1.  从字符串中删除第一个字符： **hash（txt [s：s + n-1]）-（radix **（n-1）* txt [s]）％prime_number**

2.  将下一个字符添加到字符串中： **hash（txt [s：s + n-1]）* radix + txt [n]**

下面是上述方法的实现：

## Python3

```py

# Python implementation for the  
# pattern matching in 2-D matrix 

# Function to find the hash-value  
# of the given columns of text 
def findHash(arr, col, row): 
    hashCol = [] 
    add = 0
    radix = 256

    # For each column 
    for i in range(0, col): 

        for j in reversed(range(0, row)): 
            add = add + (radix**(row-j-1) * 
                         ord(arr[j][i]))% 101
        hashCol.append(add % 101); 
        add = 0
    return hashCol 

# Function to check equality of the  
# two strings 
def checkEquality(txt, row, col, flag): 
    txt = [txt[i][col:patCol + col]  
           for i in range(row, patRow + row)] 

# If pattern found 
    if txt == pat: 
        flag = 1
        print("Pattern found at", \ 
              "(", row, ", ", col, ")") 
    return flag 

# Function to find the hash value of 
# of the next column using rolling-hash 
# of the Rabin-karp 
def colRollingHash(txtHash, nxtRow): 

    radix = 256

    # Find the hash of the matrix 
    for j in range(len(txtHash)): 
        txtHash[j] = (txtHash[j]*radix \ 
                      + ord(txt[nxtRow][j]))% 101
        txtHash[j] = txtHash[j] - (radix**(patRow) * 
                     ord(txt[nxtRow-patRow][j]))% 101 
        txtHash[j] = txtHash[j]% 101
    return txtHash 

# Function to match a pattern in  
# the given 2D Matrix 
def search(txt, pat): 

# List of the hashed value for 
    # the text and pattern columns 
    patHash = [] 
    txtHash = [] 

    # Hash value of the  
    # pat_hash and txt_hash 
    patVal = 0
    txtVal = 0 

    # Radix value for the input characters 
    radix = 256

    # Variable to determine if 
    # pattern was found or not 
    flag = 0

    # Function call to find the 
    # hash value of columns 
    txtHash = findHash(txt, txtCol, patRow)   
    patHash = findHash(pat, patCol, patRow) 

    # Calculate hash value for patHash 
    for i in range(len(patHash)): 
        patVal = patVal \ 
                 + (radix**(len(patHash)-i-1) * 
                 patHash[i]% 101) 
    patVal = patVal % 101

    # Applying Rabin-Karp to compare 
    # txtHash and patHash 
    for i in range(patRow-1, txtRow): 
        col = 0
        txtVal = 0

        # Find the hash value txtHash  
        for j in range(len(patHash)): 
            txtVal = txtVal\ 
                     + (radix**(len(patHash)-j-1) * 
                     txtHash[j])% 101
        txtVal = txtVal % 101

        if txtVal == patVal: 
            flag = checkEquality(\ 
                     txt, i + 1-patRow, col, flag) 

        else: 

            # Roll the txt window by one character  
            for k in range(len(patHash), len(txtHash)): 

                txtVal = txtVal \ 
                         * radix + (txtHash[k])% 101
                txtVal = txtVal \ 
                         - (radix**(len(patHash)) *
                         (txtHash[k-len(patHash)]))% 101
                txtVal = txtVal % 101
                col = col + 1

                # Check if txtVal and patVal are equal 
                if patVal == txtVal: 
                    flag = checkEquality(\ 
                           txt, i + 1-patRow, col, flag)    
                else: 
                    continue

        # To make sure i does not exceed txtRow 
        if i + 1<txtRow: 
            txtHash = colRollingHash(txtHash, i + 1) 

    if flag == 0: 
        print("Pattern not found") 

# Driver Code 
if __name__ == "__main__": 

  # Given Text 
  txt = [['A', 'B', 'C'], \ 
         ['D', 'E', 'F'], \ 
         ['G', 'H', 'I']] 

  # Given Pattern 
  pat = [['E', 'F'], ['H', 'I']] 

  # Dimensions of the text 
  txtRow = 3
  txtCol = 3

  # Dimensions for the pattern 
  patRow = 2
  patCol = 2

  # Function Call 
  search(txt, pat) 

```

**Output:**

```
Pattern found at ( 1 ,  1 )

```

**DSA Self Paced Course** at a student-friendly price and become industry ready.

* * *

* * *



