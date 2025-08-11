# JavaScript Traversing an Array Methods

在 JavaScript 中，「遍歷」 (Traversal) 指的是依序訪問資料結構中的每一個元素，通常是用來讀取、檢查、處理或修改其值。

### 遍歷的主要目的

- 讀取所有資料 (例如：印出陣列的每個元素)

- 找特定條件的資料 (例如：找第一個大於 100 的數字)

- 轉換或修改資料 (例如：把每個數字都乘以 2)

- 累加或彙總 (例如：計算總和或平均值)

### 常見的遍歷對象

- 陣列 (Array)：最常見，因為陣列的元素有固定順序，可以從第一個到最後一個依序處理。

- 字串 (String)：字串其實就是一個個字元的序列，也能一個一個遍歷。

- 物件 (Object)：物件沒有順序，但可以遍歷它的屬性名稱與對應的值。

- Map / Set：ES6 引入的新資料結構，也有自己的遍歷方法。

「遍歷陣列」是日常操作中最常見的任務之一。除了傳統的 `for` Loop 外，ES6 以後更提供許多語法糖與高階函數，能更優雅、簡潔操作陣列。

以下是 JavaScript 的陣列 (Array) 遍歷方法整理。

<br />

## 主流遍歷方法

| 方法 | 是否可取索引 | 是否可中斷 | 是否回傳新值 | 適用情境 |
|-|-|-|-|-|
| `for` | ✅ | ✅ | ❌ | 需要索引或控制流程 |
| `for...of` | ❌ (可搭配 entries) | ✅ | ❌ | 簡單取值 |
| `forEach()` | ✅ | ❌ | ❌ | 每個元素執行副作用 |
| `map()` | ✅ | ❌ | ✅ 新陣列 | 對每個值轉換 |
| `filter()` | ✅ | ❌ | ✅ 子陣列 | 篩選條件符合者 |
| `reduce()` | ✅ | ❌ | ✅ 聚合值 | 總和、計算、合併 |
| `find()` / `findIndex()` | ✅ | ✅ | ✅ 符合條件第一項 | 搜尋首項 |
| `some()` / `every()` | ✅ | ✅ | ✅ Boolean | 是否符合條件 |
| `entries()` / `keys()` / `values()` | ✅ (entries) | ✅ | ❌ | 可讀性高、迭代索引或值 |

<br />

## `for` Loop (傳統索引遍歷)

最基礎的迴圈方式，透過索引從陣列頭到尾遍歷每一個元素。完全控制流程。

### 語法結構

```
for (初始化; 條件; 更新) {
  // 每次迴圈執行區塊
}
```

### 語法範例

```
const arr = ['a', 'b', 'c'];
for (let i = 0; i < arr.length; i++) {
  console.log(i, arr[i]);
}
```

### 試用情境

- 需要索引來處理元素或搭配條件判斷

- 需要跳出迴圈 (break)、跳過 (continue)

### 補充建議

- 冗長但具備最高自由度

- 適用於複雜情況與條件流程控制

<br />

## `for...of` 迴圈 (ES6 可疊代值)

針對「可疊代物件」的遍歷方式，最常用於陣列與字串。

### 語法結構

```
for (const value of array) {
  // 處理每一個值
}
```

### 語法範例

```
const arr = ['a', 'b', 'c'];
for (const value of arr) {
  console.log(value);
}
```

### 試用情境

- 不需要索引，只需處理值

- 語法簡潔、可讀性佳

### 補充建議：

- 若需索引，使用 `array.entries()` 搭配解構

```
for (const [index, value] of arr.entries()) {
  console.log(index, value);
}
```

<br />

## `forEach()` 方法 (ES5)

對陣列每個元素執行一次回呼函式，無回傳值。

### 語法結構

```
array.forEach((value, index, array) => {
  // 處理每一個元素
});
```

### 語法範例

```
const arr = [1, 2, 3];
arr.forEach((value, index) => {
  console.log(`第 ${index + 1} 個是 ${value}`);
});
```

### 試用情境

- 顯示資料、渲染 DOM、console.log 等副作用操作

- 資料不需轉換或回傳

### 補充建議：

- 無法使用 `break` / `continue` 跳出

- 不會回傳新陣列 (不同於 `map`)

<br />

## `map()`

對每個元素執行處理並「建立一個新的陣列」回傳。

### 語法結構

```
const newArray = array.map((value, index, array) => {
  return 處理後的新值;
});
```

### 語法範例

```
const nums = [1, 2, 3];
const squared = nums.map(n => n * n);   // [1, 4, 9]
```

### 試用情境

- 將原始資料轉換為新格式

- 保持資料純粹性與不可變性

### 補充建議：

- 一定要有 `return`，否則新陣列會是 undefined

<br />

## `filter()`

篩選陣列中符合條件的元素，並建立新的陣列。

### 語法結構

```
const filteredArray = array.filter((value, index, array) => {
  return 條件判斷式 (true/false);
});
```

### 語法範例

```
const nums = [1, 2, 3, 4];
const even = nums.filter(n => n % 2 === 0);   // [2, 4]
```

### 試用情境

- 從陣列中挑出特定條件資料 (如果找出未完成任務)

### 補充建議：

- 保留原始陣列不變

- 回傳的是一個新陣列

<br />

## `reduce()`

將陣列所有值「累加或聚合」成一個結果 (數字、字串、物件 等)。

### 語法結構

```
const result = array.reduce((accumulator, currentValue, index, array) => {
  return 累加後結果;
}, 初始值);
```

### 語法範例

```
const nums = [1, 2, 3];
const total = nums.reduce((sum, n) => sum + n, 0);   // 6
```

### 試用情境

- 計算總和、轉成物件、統計資料等

### 補充建議：

- 強大但需較熟練，初學者可先用 `map` + `filter` 組合
