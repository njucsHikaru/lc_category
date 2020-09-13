# Tree



preorder / inorder / postorder traversal



recursion 

stack



通过遍历构建树

\105. Construct Binary Tree from Preorder and Inorder Traversal

\106. Construct Binary Tree from Inorder and Postorder Traversal

\109. Convert Sorted List to Binary Search Tree



### inorder traversal

中序遍历的路径：先找到左子树最下边的节点

```java
while(node != null) {
  st.push(node);	// 遍历完左子树后，需要借助根节点进入右子树
  node = node.left;
}

// 当node为空时，node的parent有右子树，或没有。 =》 访问node的parent node
// 若有右子树，先push，push后下一次pop则需要遍历左子树
// 若无右子树，下一次pop出来的是当前节点的parent，无需遍历左子树
```



### 101. Symmetric Tree

两个节点，分别t1.left == t2.right && t1.right == t2.left

###116. Populating Next Right Pointers in Each Node

