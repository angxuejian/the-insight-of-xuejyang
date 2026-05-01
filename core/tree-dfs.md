# 树结构遍历范式：深度优先搜索（DFS）的三种序（前序 / 中序 / 后序）

## 二叉树

固定两个口（left/right）→ 二叉树

```js
//       A
//     /   \
//    B     C
//   / \   / \
//  D   E F   G

const tree = {
  val: "A",
  left: {
    val: "B",
    left: { val: "D", left: null, right: null },
    right: { val: "E", left: null, right: null },
  },
  right: {
    val: "C",
    left: { val: "F", left: null, right: null },
    right: { val: "G", left: null, right: null },
  },
};
```

### Pre-order

根 → 左 → 右

```js
function preorder(node) {
  if (!node) return;

  console.log(node.val); // 根
  preorder(node.left); // 左
  preorder(node.right); // 右
}

preorder(tree);
// 输出: A B D E C F G
```

### In-order

左 → 根 → 右

```js
function inorder(node) {
  if (!node) return;

  inorder(node.left); // 左
  console.log(node.val); // 根
  inorder(node.right); // 右
}

inorder(tree);
// 输出: D B E A F C G
```

### Post-order

左 → 右 → 根

```js
function postorder(node) {
  if (!node) return;

  postorder(node.left); // 左
  postorder(node.right); // 右
  console.log(node.val); // 根
}

postorder(tree);
// 输出: D E B F G C A
```

## N叉树

一堆孩子（children[]） → n 叉树

```js
//        A
//     /  |  \
//    B   C   D
//   / \      |
//  E   F     G

const tree = {
  val: "A",
  children: [
    {
      val: "B",
      children: [
        { val: "E", children: [] },
        { val: "F", children: [] },
      ],
    },
    {
      val: "C",
      children: [],
    },
    {
      val: "D",
      children: [{ val: "G", children: [] }],
    },
  ],
};
```

### Pre-order

根 → 子节点（从左到右）

```js
function preorder(node) {
  if (!node) return;

  console.log(node.val); // 先处理自己

  for (const child of node.children) {
    preorder(child); // 再处理所有子节点
  }
}

preorder(tree);
// 输出: A B E F C D G
```

### Post-order

子节点（从左到右） → 根

```js
function postorder(node) {
  if (!node) return;

  for (const child of node.children) {
    postorder(child); // 先处理子节点
  }

  console.log(node.val); // 最后处理自己
}

postorder(tree);
// 输出: E F B C G D A
```
