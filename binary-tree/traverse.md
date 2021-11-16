# Traverse Binary Tree by Stack(none-recursive)

**Key point:**

 Firstly, you can write down the code of recursive form of traverse binary tree.

Then, simulating it.

And remember that stack is a data structure which is first in last out, so you should konw that the squence of traversal is reverse.

What's you need to do is simulate the process of pushing node in stack.

## 1. preorder

the order of preorder is [root left right]

In recursive traversal, the sequence is root -> left ->right

but stack is FILO, so it will be right -> left -> root.

When you need push root node,  you need to add a marker which means it'll be processed after finishing build stack.

```java
// preorder: [root left right]
// stack: [right left root]
public List<Integer> preorderTraversal(TreeNode root) {
  List<Integer> res = new ArrayList();

  if (root == null) {
    return res;
  }

  Deque<TreeNode> stack = new LinkedList();  // you can't use ArrayList, because it'll have null pointer error.
  stack.addLast(root);

  while(!stack.isEmpty()) {
    TreeNode top = stack.pollLast();
    if (top != null) {
      if (top.right != null) {
        stack.addLast(top.right);   // push right node
      }
      
      if (top.left != null) {
        stack.addLast(top.left);    // push left node
      }
      
      stack.addLast(top);           // push root node
      stack.addLast(null);          // push marker
    } else {
      res.add(stack.pollLast().val);// process node when meet marker(answer is exactly the last node of marker/null)
    }
  }

  return res;
}
```

## 2. inorder

the order of inorder is [left root right]

In recursive traversal, the sequence is left -> root ->right

but stack is FILO, so it will be right -> root -> left.

When you need push root node,  you need to add a marker which means it'll be processed after finishing build stack.

```java
// inorder: [left root right]
// stack: [right root left]
public List<Integer> inorderTraversal(TreeNode root) {
  List<Integer> res = new ArrayList();
  if (root == null) {
    return res;
  }

  Deque<TreeNode> stack = new LinkedList();
  stack.addLast(root);

  while(!stack.isEmpty()) {
    TreeNode top = stack.pollLast();
    if (top != null) {
      if (top.right != null) {
        stack.addLast(top.right);    // push right node
      }

      stack.addLast(top);            // push root node
      stack.addLast(null);           // add marker

      if (top.left != null) {
        stack.addLast(top.left);     // push left node
      }
    } else {
      res.add(stack.pollLast().val); // process node when meet marker
    }
  }

  return res;
}
```

## 3. postorder

the order of inorder is [left right root]

In recursive traversal, the sequence is left -> right -> root

but stack is FILO, so it will be root -> right -> left.

When you need push root node,  you need to add a marker which means it'll be processed after finishing build stack.

```java
// postorder: [left right root]
// stack: [root right left]
public List<Integer> postorderTraversal(TreeNode root) {
  List<Integer> res = new ArrayList();
  if (root == null) {
    return res;
  }

  Deque<TreeNode> stack = new LinkedList();
  stack.addLast(root);

  while(!stack.isEmpty()) {
    TreeNode top = stack.pollLast();
    if (top != null) {
      stack.addLast(top);              // push root node
      stack.addLast(null);             // push marker

      if (top.right != null) {
        stack.addLast(top.right);      // push right node
      }

      if (top.left != null) {
        stack.addLast(top.left);       // push left node
      }
    } else {
      res.add(stack.pollLast().val);   // process node when meet marker
    }
  }

  return res;
}
```

