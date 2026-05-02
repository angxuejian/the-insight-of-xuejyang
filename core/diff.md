# Diff


| 对比维度 | React | Vue |
|----------|------|-----|
| 更新触发方式 | 组件重新 render → 再 diff | 依赖追踪：谁变了 → 更新谁 |
| 更新粒度 | 组件级 | 节点级（更细粒度） |
| diff 策略（数组） | 单向遍历 + lastIndex（非最优移动） | 双端 diff + LIS（接近最优移动） |
| diff 内容（共性） | text / props / 事件 对比 | text / props / 事件 对比 |
| diff 优化策略 | 运行时 diff（每次 render） | 编译优化（patchFlag / block tree）减少 diff |
| 渲染机制 | 函数组件重新执行生成新树 | 模板编译 + 响应式依赖追踪 |
| 调度能力 | 可中断（Fiber）+ 优先级调度 | 默认同步（一次性完成） |
| 性能优化方向 | 可中断、可调度（保证流畅） | 少比较、少操作（减少 DOM） |
| 适用场景 | 高频交互、复杂 UI、需要响应优先级 | 稳定更新、CRUD、结构清晰的页面 |

<!-- 

## 单向遍历 + lastIndex

commit（统一更新dom）= 建立节点缓存 -> 先删除 -> 在新增 & 移动

```js
function diff(oldArr, newArr, key) {
    const oldMap = new Map();
    oldArr.forEach((item, index) => {
        const k = item[key];
        oldMap.set(k, index);
    })

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
    })

    oldArr.forEach((item, index) => {
        const k = item[key];
        if (!usedSet.has(k)) {
            console.log(`Item ${k} has been removed`);
        }
    })
}

const oldArr = [{ id: 1, name: 'Alice' }, { id: 2, name: 'Bob' }, { id: 3, name: 'Charlie' }];
const newArr = [{ id: 2, name: 'Bob' }, { id: 1, name: 'Alice' }, { id: 4, name: 'David' }];
diff(oldArr, newArr, 'id');

// Output:
// Item 1 has moved
// Item 4 is new
// Item 3 has been removed
```

## 双端 diff + LIS

双端（头部和尾部相同, 只处理中间部分） -> 如果有纯新增/删除 -> 直接处理

乱序 -> 遍历旧数组（查询新数组是否存在） -> 不存在删除，存在进入移动区

移动区 -> LTS -> 决策是移动/新增

```js
function diff(oldArr, newArr, key) {
  let i = 0;
  let oi = oldArr.length - 1;
  let ni = newArr.length - 1;

  // --------------------------------------------------------------
  // 解决头部和尾部相同的情况时，在中间部分新增或删除

  // while (i <= oi && i <= ni) {
  //   if (oldArr[i][key] === newArr[i][key]) {
  //     i++;
  //   } else {
  //     break;
  //   }
  // }

  // while (i <= oi && i <= ni) {
  //   if (oldArr[oi][key] === newArr[ni][key]) {
  //     oi--;
  //     ni--;
  //   } else {
  //     break;
  //   }
  // }

  // console.log("i:", i);
  // console.log("oi:", oi, "ni:", ni);

  // if (i > oi || i > ni) { 
  //   console.log("\n------------------------------");
  //   console.log("解决头部和尾部相同的情况时，在中间部分新增或删除");

  //    // 纯新增
  //   if (i > oi) {
  //       for (let j = i; j <= ni; j++) {
  //       console.log("纯新增:", newArr[j]);
  //       }
  //   }

  //   // 纯删除
  //   if (i > ni) {
  //       for (let j = i; j <= oi; j++) {
  //       console.log("纯删除:", oldArr[j]);
  //       }
  //   }

  //   console.log("------------------------------\n");
  //   return;
  // }

  // --------------------------------------------------------------


  console.log(`\n------------------------------`);
  console.log("进入乱序区域");

  const osi = i;
  const nsi = i;

  // 构建新数组中 key 到索引的映射
  const keyToNewIndexMap = new Map();
  for (let j = nsi; j <= ni; j++) {
    const item = newArr[j];
    keyToNewIndexMap.set(item[key], j);
  }
  // console.log("keyToNewIndexMap:", keyToNewIndexMap);

  // 构建新数组索引到旧数组索引的映射，初始值为 -1 = 表示新数组中的元素在旧数组中不存在
  const len = ni - nsi + 1;
  const newIndexToOldIndex = new Array(len).fill(-1);

  for (let j = osi; j <= oi; j++) {
    const oldItem = oldArr[j];
    const newIndex = keyToNewIndexMap.get(oldItem[key]);

    // 如果 newIndex 是 undefined，说明旧数组中的元素在新数组中不存在，需要删除
    if (newIndex === undefined) {
      console.log("删除:", oldItem, "旧索引:", j);
    } else {
      // 否则，说明旧数组中的元素在新数组中存在，需要移动
      console.log("决策移动:", oldItem);
      const ntoIndex = newIndex - nsi; // “把 newArr 的局部索引 → 映射到 从 0 开始的数组”
      newIndexToOldIndex[ntoIndex] = j;
    }
  }
    console.log("newIndexToOldIndex:", newIndexToOldIndex);

 
  const seq = getLIS(newIndexToOldIndex)
  console.log("最长递增子序列:", seq);
  
  //  return
  let s = seq.length - 1
  for (let j = newIndexToOldIndex.length - 1; j >= 0; j--) {
    if (newIndexToOldIndex[j] === -1) {
      console.log("新增:", newArr[j + i]);
    } else if (j !== seq[s]) {
      console.log("移动:", newArr[j + i]);
    } else {
      s--
    }
  }

  console.log("------------------------------\n");
}

function getLIS(arr) {
  const p = arr.slice() // 记录前驱节点
  const result = [0]    // 存索引

  for (let i = 0; i < arr.length; i++) {
    const arrI = arr[i]

    // 跳过 -1（Vue diff 用）
    if (arrI === -1) continue

    let lastIndex = result[result.length - 1]

    // 1️⃣ 比最大还大 → 直接追加
    if (arr[lastIndex] < arrI) {
      p[i] = lastIndex
      result.push(i)
      continue
    }

    // 2️⃣ 二分查找替换位置
    let start = 0
    let end = result.length - 1

    while (start < end) {
      const mid = (start + end) >> 1
      if (arr[result[mid]] < arrI) {
        start = mid + 1
      } else {
        end = mid
      }
    }

    // 替换
    if (arrI < arr[result[start]]) {
      if (start > 0) {
        p[i] = result[start - 1]
      }
      result[start] = i
    }
  }

  // 3️⃣ 回溯生成最终序列
  let u = result.length
  let v = result[u - 1]

  while (u-- > 0) {
    result[u] = v
    v = p[v]
  }

  return result
}

// const oldList = [
//   { id: 'c', name: 'C' },
//   { id: 'd', name: 'D' },
//   { id: 'a', name: 'A' },
//   { id: 'b', name: 'B' }
// ]

// const newList = [
//   { id: 'a', name: 'A' },
//   { id: 'b', name: 'B' },
// ]

const oldList = [
  { id: "a", name: "A" },
  { id: "b", name: "B" },
  { id: "c", name: "C" },
  { id: "d", name: "D" },
];

const newList = [
  { id: "b", name: "B" },
  { id: "d", name: "D" },
  { id: "a", name: "A" },
  { id: "c", name: "C" },

  // { id: "e", name: "E" },
  // { id: "f", name: "F" },
];

console.log("oldList:", oldList);
console.log("newList:", newList);
diff(oldList, newList, "id");

``` -->