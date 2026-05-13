# Diff

| 对比维度          | React                              | Vue                                         |
| ----------------- | ---------------------------------- | ------------------------------------------- |
| 更新触发方式      | 组件重新 render → 再 diff          | 依赖追踪：谁变了 → 更新谁                   |
| 更新粒度          | 组件级                             | 节点级（更细粒度）                          |
| diff 策略（数组） | 单向遍历 + lastIndex（非最优移动） | 双端 diff + LIS（接近最优移动）             |
| diff 内容（共性） | text / props / 事件 对比           | text / props / 事件 对比                    |
| diff 优化策略     | 运行时 diff（每次 render）         | 编译优化（patchFlag / block tree）减少 diff |
| 渲染机制          | 函数组件重新执行生成新树           | 模板编译 + 响应式依赖追踪                   |
| 调度能力          | 可中断（Fiber）+ 优先级调度        | 默认同步（一次性完成）                      |
| 性能优化方向      | 可中断、可调度（保证流畅）         | 少比较、少操作（减少 DOM）                  |
| 适用场景          | 高频交互、复杂 UI、需要响应优先级  | 稳定更新、CRUD、结构清晰的页面              |

## 单向遍历 + lastIndex

commit（统一更新dom）= 建立节点缓存 -> 先删除 -> 在新增 & 移动

<details>
  <summary>Example</summary>

```js
function diff(oldArr, newArr, key) {
  const oldMap = new Map();
  oldArr.forEach((item, index) => {
    const k = item[key];
    oldMap.set(k, index);
  });

  let lastIndex = 0;
  const usedSet = new Set();

  newArr.forEach((item, newIndex) => {
    const k = item[key];
    const oldIndex = oldMap.get(k);
    if (oldIndex === undefined) {
      console.log(`Item ${k} is new`);
    } else {
      usedSet.add(k);
      if (oldIndex < lastIndex) {
        console.log(`Item ${k} has moved`);
      } else {
        lastIndex = oldIndex;
      }
    }
  });

  oldArr.forEach((item, index) => {
    const k = item[key];
    if (!usedSet.has(k)) {
      console.log(`Item ${k} has been removed`);
    }
  });
}

const oldArr = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
  { id: 3, name: "Charlie" },
];
const newArr = [
  { id: 2, name: "Bob" },
  { id: 1, name: "Alice" },
  { id: 4, name: "David" },
];
diff(oldArr, newArr, "id");

// Output:
// Item 1 has moved
// Item 4 is new
// Item 3 has been removed
```

</details>

## 双端 diff + LIS

双端（头部和尾部相同, 只处理中间部分） -> 如果有纯新增/删除 -> 直接处理

乱序 -> 遍历旧数组（查询新数组是否存在） -> 不存在删除，存在进入移动区

移动区 -> LTS -> 决策是移动/新增

<details>
  <summary>Example</summary>

```js
const handleDiff = (oldChildren, newChildren) => {
  let i = 0;

  let oi = oldChildren.length - 1;
  let ni = newChildren.length - 1;

  console.log("oldChildren:", oldChildren);
  console.log("newChildren:", newChildren);
  console.log("\n");

  // 双端
  while (i <= oi && i <= ni) {
    if (oldChildren[i] === newChildren[i]) {
      console.log("头部相同：", newChildren[i]);
      i++;
    } else break;
  }

  while (i <= oi && i <= ni) {
    if (oldChildren[oi] === newChildren[ni]) {
      console.log("尾部相同：", newChildren[ni]);
      oi--;
      ni--;
    } else break;
  }

  if (i > oi) {
    while (i <= ni) {
      console.log("新增节点：", newChildren[i], `/ index = ${i}`);
      i++;
    }
    return;
  }

  if (i > ni) {
    while (i <= oi) {
      console.log("删除节点：", oldChildren[i], `/ index = ${i}`);
      i++;
    }
    return;
  }

  // 乱序部分
  console.log("\n");
  console.log("起始位置：", i);
  const osi = i;
  const nsi = i;

  //newChildren: key -> newIndex;
  const keyToNewIndexMap = new Map();
  for (let j = nsi; j <= ni; j++) {
    keyToNewIndexMap.set(newChildren[j], j);
  }
  console.log("newChildren：", keyToNewIndexMap);

  // newChildren: 乱序区间的长度
  const length = ni - nsi + 1;
  const newIndexToOldIndexMap = new Array(length).fill(0);
  console.log("newIndex to oldIndex - init:", newIndexToOldIndexMap);

  // oldChildren: 遍历
  for (let j = osi; j <= oi; j++) {
    const oldVNode = oldChildren[j];
    const newIndex = keyToNewIndexMap.get(oldVNode);
    if (newIndex === undefined) {
      console.log(
        `旧值：${oldVNode}, 旧索引：${j}，新索引：${newIndex} -> 删除`,
      );
    } else {
      console.log(`复用：${oldVNode}, 旧索引：${j}，新索引：${newIndex}`);

      // +1: Array(length).fill(0) 默认是0，要与其区分出来
      newIndexToOldIndexMap[newIndex - nsi] = j + 1;
    }
  }
  console.log("newIndex to oldIndex - update:", newIndexToOldIndexMap);
  console.log("\n");

  // 求LIS
  const LITArray = handleLIS(newIndexToOldIndexMap);
  console.log("LIS:", LITArray);
  console.log(
    "LIS对应的值：",
    LITArray.map((index) => newIndexToOldIndexMap[index]),
  );
  console.log("\n");

  // 倒序处理
  let l = LITArray.length - 1;
  let k = newIndexToOldIndexMap.length - 1;

  for (let j = k; j >= 0; j--) {
    const currentIndex = j + nsi;
    const currentVNode = newChildren[currentIndex];
    const anchor =
      currentIndex + 1 < newChildren.length
        ? newChildren[currentIndex + 1]
        : null;

    if (newIndexToOldIndexMap[j] === 0) {
      console.log("新增节点：", currentVNode, "，插入到：", anchor);
    } else if (j !== LITArray[l]) {
      console.log("移动节点：", currentVNode, "，插入到：", anchor);
    } else {
      console.log("不动节点：", currentVNode);
      l--;
    }
  }
};

const handleLIS = (arr) => {
  const p = arr.slice();

  const result = [0];

  let i, j, u, v, c;

  for (i = 0; i < arr.length; i++) {
    const arrI = arr[i];

    if (arrI === 0) continue;

    j = result[result.length - 1];

    if (arr[j] < arrI) {
      p[i] = j;

      result.push(i);

      continue;
    }

    u = 0;
    v = result.length - 1;

    while (u < v) {
      c = ((u + v) / 2) | 0;

      if (arr[result[c]] < arrI) {
        u = c + 1;
      } else {
        v = c;
      }
    }

    if (arrI < arr[result[u]]) {
      if (u > 0) {
        p[i] = result[u - 1];
      }

      result[u] = i;
    }
  }

  u = result.length;
  v = result[u - 1];

  while (u-- > 0) {
    result[u] = v;
    v = p[v];
  }

  return result;
};

const oldArr = ["A", "B", "C", "D"];
const newArr = ["A", "C", "D", "B", "E", "F"];
handleDiff(oldArr, newArr);

// oldChildren: [ 'A', 'B', 'C', 'D' ]
// newChildren: [ 'A', 'C', 'D', 'B', 'E', 'F' ]

// 头部相同： A

// 起始位置 1
// newChildren:  Map(5) { 'C' => 1, 'D' => 2, 'B' => 3, 'E' => 4, 'F' => 5 }
// newIndex to oldIndex - init: [ 0, 0, 0, 0, 0 ]
// 复用：B, 旧索引：1，新索引：3
// 复用：C, 旧索引：2，新索引：1
// 复用：D, 旧索引：3，新索引：2
// newIndex to oldIndex - update: [ 3, 4, 2, 0, 0 ]

// LIS: [ 0, 1 ]
// LIS对应的值： [ 3, 4 ]

// 新增节点： F ，插入到： null
// 新增节点： E ，插入到： F
// 移动节点： B ，插入到： E
// 不动节点： D
// 不动节点： C
```

</details>
