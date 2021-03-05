[toc]

# TREE

## Definition of Tree

```java
class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;
  TreeNode() {}
  TreeNode(int val) { this.val = val; }
  TreeNode(int val, TreeNode left, TreeNode right) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}
```

## Preorder traversal

### recursion

```java
public void preorderRecursion(TreeNode node) {
  if(node != null) {
    System.out.println(node.val);
    preorderRecursion(node.left);
    preorderRecursion(node.right);
  }
}
```

### non-recursion

```java
public void preorderNonRecursion(TreeNode node) {
	if(node == null) return;
  Stack<TreeNode> stack = new Stack<TreeNode>();
  stack.push(node);
  while(!stack.isEmpty()) {
    TreeNode temp = stack.pop();
    System.out.println(temp.val);
    if(temp.right != null) stack.push(temp.right);
    if(temp.left != null) stack.push(temp.left);
  }
}
```

## Midorder traversal

### recurison

```java
public void midorderRecursion(TreeNode node) {
  if(node != null) {
    midorderRecursion(node.left);
    System.out.println(node.val);
    midorderRecursion(node.right);
  }
}
```

### non-recursion

```java
public void midorderNonRecursion(TreeNode node) {
  Stack<TreeNode> stack = new Stack<TreeNode>();
  TreeNode pre = node;
  while(pre != null || !stack.isEmpty()) {
    if(pre != null) {
      stack.push(pre);
      pre = pre.left;
    }else {
      TreeNode temp = stack.pop();
      System.out.println(temp.val);
      pre = temp.right;
    }
  }
}
```

## Postorder traversal

### recursion

```java
public void postorderRecursion(TreeNode node) {
  if(node != null) {
    postorderRecursion(node.left);
    postorderRecursion(node.right);
    System.out.println(node.val);
  }
}
```

### non-recursion

```java
public void postorderNonRecursion(TreeNode node) {
  Stack<TreeNode> stack = new Stack<TreeNode>();
  TreeNode pre = null;
  TreeNode cur;
  stack.push(node);
  while(!stack.isEmpty()) {
    cur = stack.peek();
    if((cur.left == null && cur.right == null) || (pre != null && (pre == cur.left || pre == cur.right))) {
      System.out.println(stack.pop().val);
      pre = cur;
    }else {
      if(cur.right != null) stack.push(cur.right);
      if(cur.left != null) stack.push(cur.left);
    }
  }
}
```

## Level traversal

```java
public static void levelTraversal(TreeNode node) {
  LinkedList<TreeNode> list = new LinkedList<TreeNode>();
  list.offer(node);
  while(!list.isEmpty()) {
    TreeNode temp = list.poll();
    System.out.println(temp.val);
    if(temp.left != null) list.offer(temp.left);
    if(temp.right != null) list.offer(temp.right);
  }
}
```

## Tree depth

```java
public int maxDepth(TreeNode root){
  if(root != null){
    int left = maxDepth(root.left);
    int right = maxDepth(root.right);
    return (left > right ? left : right) + 1;
  }
	return 0;
}
```

## Tree Leave Number

```java
public int leaveNums(TreeNode node) {
  if(node == null) return 0;
  if(node.left == null && node.right == null) return 1;
  return leaveNums(node.left) + leaveNums(node.right);
}
```

# Stack

Null

# LinkedList

Null