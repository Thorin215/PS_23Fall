# 作业错题整理 

## HW1 (Algorithm Analysis)
 
>The Fibonacci number sequence ${F_N​}$ is defined as: F0​=0, F1​=1, FN​=FN−1​+FN−2​, N=2, 3, .... The time complexity of the function which calculates FN​ recursively is Θ(N!).    __Answer : F__
>>Reason :  $O((\frac{\sqrt{5}+1}{2})^n)$


>The Fibonacci number sequence {FN} is defined as: F0=0, F1=1, FN=FN-1+FN-2, N=2, 3, .... The space complexity of the function which calculates FN recursively is O(logN).   __Answer : F__
>> Reason : $O(N)$


>P1: T(1)=1, T(N)=T(N/2)+1;
P2: T(1)=1, T(N)=2T(N/2)+1;
>>P1是O(logN)，P2是O(N)

## HW2 (Linear ADT)

>For a sequentially stored linear list of length N, the time complexities for query and insertion are O(1) and O(N), respectively.
>> Both are $O(1)$ *Insert in list just need three steps*

```c
//Reverse the list
List Reverse( List L ){
    List left = L,right=L->Next;
    if(right){
        left=right;
        right=right->Next;
    }else{
        return left;
    }
    int flag=0;
    while(right){
        List temp = right->Next;
        if(!flag){
            left->Next=NULL;
            right->Next=left;
            flag = 1;
        }else{
            right->Next=left;
        }
        left = right;
        right = temp;
    }
    L->Next=left;
    return L;
}
```

## HW4 (Tree)

!!!Note
    **Important Equation** : 
    - $n_0+n_1+n_2 = \sum{node}$
    - $n_1 + 2*n_2 + 1(root) = \sum{node}$
    - $n_0 = n_2 + 1$

>There exists a binary tree with 2016 nodes in total, and with 16 nodes having only one child.   __Answer : F__
>> $2*n_2 = 1999 \rightarrow wrong$


>Given a tree of degree 3. Suppose that there are 3 nodes of degree 2 and 2 nodes of degree 3. Then the number of leaf nodes must be ____.
>> $n_0 = 2*n_3 + 1*n_2 + 1 = 8$


>If a general tree T is converted into a binary tree BT, then which of the following BT traversals gives the same sequence as that of the post-order traversal of T?
>> In-order traversal


!!! note Threaded Binary Tree
    **If the left child is null, this point to its Ltag(前驱)**
    **If the right child is null, this point to its Rtag(后驱)** 


## HW5


!!! 
    Binary Search Tree(BST)定义
    - 二叉树
    - 左孩子<根<右孩子
    - 左右子树都是BST


>In a binary search tree, the keys on the same level from left to right must be in sorted (non-decreasing) order.  __Answer : Yes__
>> Difinition

[关于折半查找二叉树](https://blog.csdn.net/weixin_43305485/article/details/120619942)

*通俗的来讲：要一直符合左子树比右子树大一或者右子树比左子树大一*

>For a binary search tree, in which order of traversal that we can obtain a non-decreasing sequence?
>> inorder traversal

## HW6 (HEAP)

>The preorder traversal sequence of any min-heap must be in sorted (non-decreasing) order. F
>> The sibling node is not sorted


>Using the linear algorithm to build a min-heap from the sequence {15, 26, 32, 8, 7, 20, 12, 13, 5, 19}, and then insert 6. Which one of the following statements is
>> The array will be {5,6,12,8,7,20,32,13,,26,19,15}
>> process the last parent node

## HW7


![](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/2b2d86c3bf46d03665ea88c0847df9d5.png)


```c
SetType Find ( ElementType X, DisjSet S )
{   
   ElementType root, trail, lead;

   for ( root = X; S[root] > 0; root = S[root]);  
   for ( trail = X; trail != root; trail = lead ) {
      lead = S[trail] ;   
      S[trail] = root;   
   } 
   return root;
}
```
