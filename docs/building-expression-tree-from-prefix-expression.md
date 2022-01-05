# 根据前缀表达式构建表达式树

> 原文:[https://www . geesforgeks . org/building-expression-tree-from-prefix-expression/](https://www.geeksforgeeks.org/building-expression-tree-from-prefix-expression/)

给定一个字符数组**一个表示前缀表达式的[]** 。任务是为表达式构建一个[表达式树](https://www.geeksforgeeks.org/expression-tree/)，然后打印所构建的树的**中缀**和**后缀**表达式。
**举例:**

> **输入:** a[] = "*+ab-cd"
> **输出:**中缀表达式为:
> a+b * c–d
> 后缀表达式为:
> a b+ c d –*
> **输入:** a[] = "+ab"
> **输出:**中缀表达式为:
> a + b
> 后缀表达式为:
> a b +

**方法:**如果字符是操作数，即 **X** ，那么它将是所需树的叶节点，因为所有操作数都在表达式树的叶上。否则，如果该字符是一个操作符，并且是**操作符 X Y** 的形式，那么它将是一个内部节点，左子节点作为**表达式控件(X)** ，右子节点作为**表达式控件(Y)** ，这可以使用递归函数来求解。
以下是上述方法的实施:

## C

```
// C program to construct an expression tree
// from prefix expression
#include <stdio.h>
#include <stdlib.h>

// Represents a node of the required tree
typedef struct node {
    char data;
    struct node *left, *right;
} node;

// Function to recursively build the expression tree
char* add(node** p, char* a)
{

    // If its the end of the expression
    if (*a == '\0')
        return '\0';

    while (1) {
        char* q = "null";
        if (*p == NULL) {

            // Create a node with *a as the data and
            // both the children set to null
            node* nn = (node*)malloc(sizeof(node));
            nn->data = *a;
            nn->left = NULL;
            nn->right = NULL;
            *p = nn;
        }
        else {

            // If the character is an operand
            if (*a >= 'a' && *a <= 'z') {
                return a;
            }

            // Build the left sub-tree
            q = add(&(*p)->left, a + 1);

            // Build the right sub-tree
            q = add(&(*p)->right, q + 1);

            return q;
        }
    }
}

// Function to print the infix expression for the tree
void inr(node* p) // recursion
{
    if (p == NULL) {
        return;
    }
    else {
        inr(p->left);
        printf("%c ", p->data);
        inr(p->right);
    }
}

// Function to print the postfix expression for the tree
void postr(node* p)
{
    if (p == NULL) {
        return;
    }
    else {
        postr(p->left);
        postr(p->right);
        printf("%c ", p->data);
    }
}

// Driver code
int main()
{
    node* s = NULL;
    char a[] = "*+ab-cd";
    add(&s, a);
    printf("The Infix expression is:\n ");
    inr(s);
    printf("\n");
    printf("The Postfix expression is:\n ");
    postr(s);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to construct an expression tree
# from prefix expression

# Represents a node of the required tree
class node:
    def __init__(self,c):
        self.data=c
        self.left=self.right=None

# Function to recursively build the expression tree
def add(a):

    # If its the end of the expression
    if (a == ''):
        return ''

    # If the character is an operand
    if a[0]>='a' and a[0]<='z':
        return node(a[0]),a[1:]
    else:
        # Create a node with a[0] as the data and
        # both the children set to null
        p=node(a[0])
        # Build the left sub-tree
        p.left,q=add(a[1:])
        # Build the right sub-tree
        p.right,q=add(q)
        return p,q

# Function to print the infix expression for the tree
def inr(p): #recursion

    if (p == None):
        return
    else:
        inr(p.left)
        print(p.data,end=' ')
        inr(p.right)

# Function to print the postfix expression for the tree
def postr(p):

    if (p == None):
        return
    else:
        postr(p.left)
        postr(p.right)
        print(p.data,end=' ')

# Driver code
if __name__ == '__main__':

    a = "*+ab-cd"
    s,a=add(a)
    print("The Infix expression is:")
    inr(s)
    print()
    print("The Postfix expression is:")
    postr(s)

# This code is contributed by Amartya Ghosh
```

**Output:** 

```
The Infix expression is:
 a + b * c - d 
The Postfix expression is:
 a b + c d - *
```