# JavaScript Math Methods

以下是 JavaScript 的 Math Methods 詳細整理。

<br />

## Math.random()

`Math.random()` 是 JavaScript 提供的一個內建方法，用來生成一個介於 0 (包含) 到 1 (不包含) 之間的隨機小數。這個隨機小數通常用來處理一些需要隨機性質的需求，例如：遊戲中的隨機事件、隨機顏色生成、或是從資料中隨機選取某個項目等。

### 基本語法

```
let randomNumber = Math.random();
```

這段程式碼會將 Math.random() 產生的隨機數字賦值給變數 randomNumber，該隨機數會是一個介於 0 到 1 之間 (開區間) 的浮點數，例如：0.834、0.527 之類的數值。

### 詳細說明

- 應用場景

    - 隨機數字生成

        若想生成一個指定範圍的隨機數，物做法是將隨機數乘以一個範圍，然後進行取整數。

        ```
    	// 生成 0 到 9 之間的隨機整數
    	let randomInt = Math.floor(Math.random() * 10);
    	```

        上面的範例中，`Math.random()` 生成的數字被乘以 10，使結果範圍變成 0 (包含) 到 10 (不包含)。`Math.floor(x)` 用來將浮點數取整數，最終結果是一個 0 到 9 之間的隨機整數。

    - 隨機抽取陣列中的元素

        常用於從一個陣列中隨機選取一個元素。

    	```
    	let items = ['aaa', 'bbb', 'ccc'];
    	let randomItem = items[Math.floor(Math.random() * items.length)];
    	console.log(randomItem);   // 可能是 "aaa", "bbb" 或 "ccc"
    	```

    - 生成不同範圍的隨機數

        如果想生成一個指定範圍的隨機數字 (例如：5 到 15 之間的數字)，可以使用以下方法

    	```
    	function getRandom(min, max) {
    	    return Math.random() * (max - min) + min;
    	}

    	console.log(getRandom(5, 15));   // 生成 5 到 15 之間的隨機數 (不含 15)
    	```

    - 生成隨機整數

        如果想在某個範圍內生成整數 (例如：1 到 100)，可以使用下列方法

    	```
    	function getRandomInt(min, max) {
    	    return Math.floor(Math.random() * (max - min + 1)) + min;
    	}

        console.log(getRandomInt(1, 100));   // 生成 1 到 100 之間的隨機整數 (包含 1 和 100)
        ```

-  注意事項

    - 隨機性與可預測性

        `Math.random()` 的隨機性在大多數應用情況下已經足夠，但如果需要更高等級的隨機性 (例如：加密、金融交易等領域)，這種隨機數生成方式可能不夠安全，因為 `Math.random()` 是偽隨機數生成器 (Pseudo-Random Number Generator, PRNG)。也就是說，`Math.random()` 是基於一個演算法，雖然看起來隨機，但其實可以預測。

### 常見問題

- 為什麼不能生成 1

    因為 `Math.random()` 的設計原理，所以生成的隨機數總是介於 0 (包含) 到 1 (不包含) 之間。這樣的設計確保了無論在什麼情況下，生成的數字永遠不會達到上界 (1)，這在很多情況中可以避免邊界問題。

- 如何生成帶有小數點的隨機數

    `Math.random()` 生成的數字本來就是浮點數，但如果想控制小數點後的位數，可以使用 `toFixed()` 方法

    ```
    let randomNum = (Math.random() * 100).toFixed(2);
    console.log(randomNum);   // 生成一個有兩位小數的隨機數，例如：43.70
    ```

### 總結

`Math.random()` 是一個非常常用的工具，無論是用來生成隨機整數、浮點數，還是用來從陣列中隨機選取元素，都有廣泛的應用。雖然 `Math.random()` 的隨機性在一般情況下蠻夠用的，但是在一些需要高安全性的情況可能會有所限制。

<br />

## Math.round(x)

`Math.round(x)` 是 JavaScript 中用來四捨五入數字的內建方法，會根據小數點後的數字來決定向上或向下取整數或直接等於該數。

### 基本語法

```
Math.round(x);
```

- x：要進行四捨五入的數字。

### 詳細說明

- 四捨五入的規則

    當小數部分小於 0.5 時，會將數字向下取整數，即捨去小數部分。

    當小數部分大於或等於 0.5 時，會將數字向上取整數，即將整數部分加 1。

- 範例

    - 當 x 是正數

    	```
    	console.log(Math.round(4.3));   // 4
		console.log(Math.round(4.7));   // 5
		console.log(Math.round(5.5));   // 6
    	```

        `Math.round(4.3)` 中，小數點後的 0.3 小於 0.5，會向下取整數為 4。

        `Math.round(4.7)` 中，小數點後的 0.7 大於 0.5，會向上取整數為 5。

        `Math.round(5.5)` 中，小數點後正好是 0.5，所以會向上取整數為 6。

    - 當 x 是負數

        ```
        console.log(Math.round(-4.3));   // -4
		console.log(Math.round(-4.7));   // -5
		console.log(Math.round(-5.5));   // -5
        ```

        `Math.round(-4.3)` 中，小數點後的 0.3 小於 0.5，向下取整數為 -4 (更接近 -4 而不是 -5)。

        `Math.round(-4.7)` 中，小數點後的 0.7 大於 0.5，向上取整為 -5 (更接近 -5 而不是 -4)。

        `Math.round(-5.5)` 中，小數點後是 0.5，結果是 -5 (JavaScript 對負數四捨五入時遵循的是向 0 方向取整數)。

- 應用場景

    - 顯示數值

        `Math.round(x)` 常用在一些需要對顯示的數字進行簡單處理。
        
        例如：當希望將計算結果四捨五入到最接近的整數

        ```
        let price = 4.56;
        console.log(Math.round(price));   // 5
        ```

    - 計算平均值

        計算多個數字的平均值時，使用 `Math.round(x)` 來四捨五入平均值

        ```
        let avg = (3.5 + 4.8 + 5.1) / 3;
        console.log(Math.round(avg));   // 4
        ```

- 與其他取整數方法的差異

    - `Math.round(x)`：將數字四捨五入，依據小數點後的數值來決定向上或向下取整數。

    - `Math.floor(x)`：將數字向下取整數，不論小數是多少，結果永遠是最接近的較小整數。

    - `Math.ceil(x)`：將數字向上取整數，不論小數是多少，結果永遠是最接近的較大整數。

    - `Math.trunc(x)`：直接捨棄小數部分，不進行四捨五入。

    範例對比

    ```
    console.log(Math.round(4.5));   // 5
    console.log(Math.floor(4.5));   // 4
    console.log(Math.ceil(4.5));   // 5
    console.log(Math.trunc(4.5));   // 4
    ```

### 常見誤區

- 四捨五入負數：有些人可能會誤以為負數的四捨五入與正數相同，但其實在負數的情況下，JavaScript 的四捨五入是向 0 靠攏的。也就是說，`Math.round(-5.5)` 結果是 -5，而不是 -6。

### 總結

`Math.round(x)` 是一個非常常用的四捨五入方法，能夠依據小數部分自動決定向上或向下取整數，無論是正數還是負數都能夠準確返回最接近的整數。與 `Math.floor(x)` 和 `Math.ceil(x)` 等取整數方法相比，`Math.round(x)` 更具靈活性，特別適合需要進行四捨五入的情境。

<br />

## Math.floor(x)

`Math.floor(x)` 是 JavaScript 中用來將數字向下取整數的內建方法，也就是將數字「無條件捨去小數部分」，返回比原數字小或相等的整數。

### 基本語法

```
Math.floor(x);
```

- x：要進行向下取整數的數字。

### 詳細說明

- 向下取整數的規則

    不論小數部分是多少，只要存在小數，`Math.floor(x)` 都會將數字向負無窮大到取整數。

    如果 x 本身已經是整數，結果就會是該數字本身，不會進行任何變化。

    - 如果 x 是正數，`Math.floor(x)` 的效果類似於「無條件捨去」。

    - 如果 x 是負數，會返回比 x 更小的整數。

- 範例

    - 當 x 是正數

		```
		console.log(Math.floor(4.7));   // 4
		console.log(Math.floor(9.1));   // 9
		```

        `Math.floor(4.7)` 將小數點後的 0.7 移除，向下取整數為 4。

        `Math.floor(9.1)` 將小數點後的 0.1 移除，向下取整數為 9。

    - 當 x 是負數

		```
		console.log(Math.floor(-3.7));   // -4
		console.log(Math.floor(-2.1));   // -3
		```

        `Math.floor(-3.7)` 將小數點後的 0.7 移除，向下取整數為 -4 (不是 -3，因為 -4 是小於 -3.7 的最大整數)。

        `Math.floor(-2.1)` 將小數點後的 0.1 移除，向下取整數為 -3。

- 應用場景

    - 隨機數生成

        `Math.floor(x)` 常與 `Math.random()` 搭配使用，用來生成一個範圍內的隨機整數。

        例如：生成 0 到 9 之間的隨機整數

        ```
        let randomInt = Math.floor(Math.random() * 10);
        console.log(randomInt);   // 結果可能是 0 到 9 之間的隨機整數
        ```

    - 分頁功能

        當處理分頁顯示資料時，可能需要計算總頁數。

        ```
        let totalItems = 53;
		let itemsPerPage = 10;
		let totalPages = Math.floor(totalItems / itemsPerPage);
		console.log(totalPages);   // 5
        ```

        在這個範例中，儘管總共 53 筆資料，但每頁只能顯示 10 筆，因此向下取整數的結果是 5 頁。

- 與其他取整數方法的差異

    - `Math.round(x)`：將數字四捨五入，依據小數點後的數值來決定向上或向下取整數。

    - `Math.floor(x)`：將數字向下取整數，不論小數是多少，結果永遠是最接近的較小整數。

    - `Math.ceil(x)`：將數字向上取整數，不論小數是多少，結果永遠是最接近的較大整數。

    - `Math.trunc(x)`：直接捨棄小數部分，不進行四捨五入。

    範例對比

    ```
    console.log(Math.round(4.5));   // 5
    console.log(Math.floor(4.5));   // 4
    console.log(Math.ceil(4.5));   // 5
    console.log(Math.trunc(4.5));   // 4
    ```

### 常見誤區

- 負數的處理：有些人可能會誤以為 `Math.floor(x)` 對負數會「無條件捨去」，但其實是向負無窮大取整數。

### 總結

`Math.floor(x)` 的主要功能是將數字向下取整數，適用於很多需要處理整數的情境，例如：隨機數生成、分頁計算等。與 `Math.ceil(x)` 和 `Math.round(x)` 相比，`Math.floor(x)` 更加注重數值的向下捨去。

<br />

## Math.ceil(x)

`Math.ceil(x)` 是 JavaScript 中用來將數字向上取整的內建方法，也就是將數字「無條件捨去小數部分」，返回比原數字大的最小整數或相等的整數。

### 基本語法

```
Math.ceil(x);
```

- x：是要進行向上取整數的數字。

### 詳細說明

- 向上取整的規則

    不論小數部分是多少，只要存在小數，`Math.ceil(x)` 都會將數字向無窮大到取整數。

    如果 x 本身已經是整數，結果就會是該數字本身，不會進行任何變化。

- 範例

    - 當 x 是正數

		```
		console.log(Math.ceil(4.3));   // 5
		console.log(Math.ceil(4.7));   // 5
		```

        `Math.ceil(4.3)` 將小數點後的 0.3 移除，向上取整數為 5。

        `Math.ceil(4.7)` 將小數點後的 0.7 移除，向上取整數為 5。

    - 當 x 是負數

		```
		console.log(Math.ceil(-4.3));   // -4
		console.log(Math.ceil(-4.7));   // -4
		```

        `Math.ceil(-4.3)` 將小數點後的 0.3 移除，向上取整數為 -4。

        `Math.ceil(-4.7)` 將小數點後的 0.7 移除，向上取整數為 -4。

- 應用場景

    - 計算需要的最小數量

        `Math.ceil(x)` 常用在需要確保結果至少是某個整數的時候。

        例如：假設有 53 個項目，每個盒子可以裝 10 個項目，需要多少個盒子才能裝完所有項目

        ```
        let totalItems = 53;
		let itemsPerBox = 10;
		let boxesNeeded = Math.ceil(totalItems / itemsPerBox);
		console.log(boxesNeeded);   // 6
        ```

        在這個範例中，雖然 53 除以 10 等於 5.3，但必須向上取整數以確保有足夠的盒子來裝所有項目。

    - 處理時間進位
    
        假設需要將時間從分鐘轉換為小時並進行進位，使用 `Math.ceil(x)` 確保不會丟失時間。

        ```
        let minutes = 130;
		let hours = Math.ceil(minutes / 60);
		console.log(hours);   // 3
        ```

        在這個範例中，30 分鐘約等於 2.17 小時，但因為還有多出的 0.17 小時，結果被向上取整數為 3 小時。

- 與其他取整數方法的差異

    - `Math.round(x)`：將數字四捨五入，依據小數點後的數值來決定向上或向下取整數。

    - `Math.floor(x)`：將數字向下取整數，不論小數是多少，結果永遠是最接近的較小整數。

    - `Math.ceil(x)`：將數字向上取整數，不論小數是多少，結果永遠是最接近的較大整數。

    - `Math.trunc(x)`：直接捨棄小數部分，不進行四捨五入。

    範例對比

    ```
    console.log(Math.round(4.5));   // 5
    console.log(Math.floor(4.5));   // 4
    console.log(Math.ceil(4.5));   // 5
    console.log(Math.trunc(4.5));   // 4
    ```

### 常見誤區

- 負數的向上取整數：有些人可能會誤以為 `Math.ceil(x)` 對負數也是簡單的「無條件捨去」，但其實是會將負數向無窮大取整數。因此，`Math.ceil(-4.7)` 的結果是 -4，而不是 -5。

### 總結

`Math.ceil(x)` 是用來將數字向上取整數的工具，無論小數部分是多小，只要不是整數，結果都會進位到下一個整數。`Math.ceil(x)` 的應用範圍很廣，尤其在處理需要進位或確保整數結果的情況。與 `Math.floor(x)` 和 `Math.round(x)` 等取整數方法相比，`Math.ceil(x)` 的最大特點就是永遠向上取整數，特別是在負數的情況下，能夠精準進行向上取整數。

<br />

## Math.trunc(x)

`Math.trunc(x)` 是 JavaScript 中用來去掉數字的小數部分，並只保留整數部分的內建方法。簡單來說，`Math.trunc(x)` 的作用是直接截取數字小數點之前的整數，不進行任何四捨五入或取整數操作。

### 基本語法

```
Math.trunc(x);
```

- x：是要進行截取小數的數字。

### 詳細說明

- 截取小數部分的規則

    `Math.trunc(x)` 會直接捨去小數部分，不管小數是正數還是負數。

    如果 x 是整數，那結果就是 x 本身，沒有任何變化。

- 範例

    - 當 x 是正數

    	```
		console.log(Math.trunc(4.9));   // 4
		console.log(Math.trunc(4.1));   // 4
		console.log(Math.trunc(5.0));   // 5
    	```

    - 當 x 是負數

        ```
		console.log(Math.trunc(-4.9));   // -4
		console.log(Math.trunc(-4.1));   // -4
		console.log(Math.trunc(-5.0));   // -5
        ```

- 應用場景

    - 截取整數部分

        `Math.trunc(x)` 在需要忽略數字的小數只保留整數時是最直接的方法。

    	```
    	let price = 9.99;
		let integerPrice = Math.trunc(price);
		console.log(integerPrice);   // 9
    	```

- 與其他取整數方法的差異

    - `Math.round(x)`：將數字四捨五入，依據小數點後的數值來決定向上或向下取整數。

    - `Math.floor(x)`：將數字向下取整數，不論小數是多少，結果永遠是最接近的較小整數。

    - `Math.ceil(x)`：將數字向上取整數，不論小數是多少，結果永遠是最接近的較大整數。

    - `Math.trunc(x)`：直接捨棄小數部分，不進行四捨五入。

    範例對比

    ```
    console.log(Math.round(4.5));   // 5
    console.log(Math.floor(4.5));   // 4
    console.log(Math.ceil(4.5));   // 5
    console.log(Math.trunc(4.5));   // 4
    ```

### 常見誤區

- `Math.trunc(x)` 不會四捨五入：有些人可能會誤以為 `Math.trunc(x)` 會進行某種取整數操作，實際上只是簡單捨去小數部分，而不是根據數字的大小進行向上或向下取整數。

- 負數處理：與 `Math.floor()` 相比，`Math.trunc(x)` 不會將負數向負無窮大方向取整數，而是簡單捨去負數的小數部分。因此，`Math.trunc(-4.7)` 的結果是 -4，而不是 -5。

### 總結

`Math.trunc(x)` 是用來去掉數字小數部分用工具，不進行任何四捨五入或取整數，只是單純截取整數部分。無論是正數還是負數，都會直接捨去小數點後的數字。

<br />

## Math.abs(x)

`Math.abs(x)` 是 JavaScript 中用來取得數字絕對值的內建方法，絕對值就是指不帶正負號的數值。無論 x 是正數還是負數，`Math.abs(x)` 會返回這個數字的非負數。

### 基本語法

```
Math.abs(x);
```

- x：想要取得絕對值的數字。

### 詳細說明

- 什麼是絕對值

    絕對值是數字與 0 之間的距離，不考慮方向。因此，無論數字是正數還是負數，結果都是非負數。

    對於任何一個正數或負數 x，`Math.abs(x)` 都會將其轉換為正數。

    - `Math.abs(5)` 結果是 5。

    - `Math.abs(-5)` 結果也是 5。

- 範例

    - 當 x 是正數

    	```
		console.log(Math.abs(4));   // 4
		console.log(Math.abs(7.5));   // 7.5
    	```

    - 當 x 是負數

        ```
		console.log(Math.abs(-4));   // 4
		console.log(Math.abs(-7.5));   // 7.5
        ```

    - 當 x 是 0

        ```
        console.log(Math.abs(0));   // 0
        ```

        0 的絕對值還是 0，因為 0 本身就是沒有正負的數值。

    - 當 x 是 NaN (非數值)

        ```
        console.log(Math.abs(NaN));   // NaN
        ```
- 應用場景

    - 計算兩個數字的差距
    
        絕對值常被用在需要計算兩個數字之間的距離。這樣無論順序如何，結果都能表示兩個數字的距離。

        ```
        let a = 10;
		let b = 4;
		let difference = Math.abs(a - b);
		console.log(difference);   // 6
        ```

        不論是 `a - b` 還是 `b - a`，`Math.abs(x)` 保證結果總是正數，表示兩個數字之間的距離。

    - 在物理或運動中的應用
    
        絕對值常用於表示實際距離或大小

        例如：速度、距離等不應該有負數的情境。

        ```
        let velocity = -20;
		let speed = Math.abs(velocity);
		console.log(speed);   // 20
        ```

        這裡速度的值被轉換為正值，因為速度不應該是負數。

    - 取代條件判斷：當只關心數字的大小，不在意正負號時，使用 `Math.abs(x)` 可以省去額外的條件判斷。例如：判斷一個數字是否超過某個範圍。

        ```
        let number = -12;
        if (Math.abs(number) > 10) {
            console.log('超過範圍');
        }
        ```

        以上範例中，不論 number 是正數還是負數，只要其絕對值超過 10，都會觸發條件。

- 與其他 Math method 的關聯

    - 與 `Math.sign(x)` 結合使用時，`Math.abs(x)` 可以幫助將數字的符號和大小分離。

    	```
    	let num = -9.5;
    	console.log(Math.sign(num) * Math.abs(num));   // -9.5
        ```

        以上範例，可以理解為先取絕對值，再根據原來的符號進行修正。

### 常見誤區

- 絕對值不適用於非數字：`Math.abs(x)` 只對數字有效，對於其他類型的變數 (例如：字串或物件)，會返回 NaN。

    ```
    console.log(Math.abs("hello"));   // NaN
    ```

### 總結

`Math.abs(x)` 是一個用來取得數字絕對值的簡單工具，會將任何正數或負數轉換為非負數，非常適合用於計算數字之間的差距或處理實際物理量。

`Math.abs(x)` 不會影響數字的小數部分，也不會對 NaN 或非數值資料進行處理。

<br />

## Math.sign(x)

`Math.sign(x)` 是 JavaScript 中用來判斷一個數字符號的內建方法，會根據傳入數字不同而返回相對應的結果，具體可以分為以下五種

- 正數 -> 1

- 負數 -> -1

- 正 0 -> 0

- 負 0 -> -0

- NaN (非數字) -> NaN

### 基本語法

```
Math.sign(x);
```

- x：想要判斷符號的數字。

### 詳細說明

- 符號判斷的規則

    `Math.sign(x)` 根據數字的符號來返回對應的結果，不改變數字本身的大小或精度，主要是用來快速判斷一個數字是正數還是負數，或是否為 0。

    `Math.sign(x)` 對 +0 和 -0 做了區分。

- 範例

    - 當 x 是正數

		```
		console.log(Math.sign(5));   // 1
		console.log(Math.sign(3.2));   // 1
		console.log(Math.sign('123'));   // 1
		```

        正數的符號為 1，不論是整數還是小數。

    - 當 x 是負數

		```
		console.log(Math.sign(-5));   // -1
		console.log(Math.sign(-3.2));   // -1
		console.log(Math.sign('-123'));   // -1
		```

        負數的符號為 -1，不論負數是整數還是小數。

    - 當 x 是 0 或 -0

        ```
        console.log(Math.sign(0));   // 0
        console.log(Math.sign('0'));   // 0
        console.log(Math.sign(-0));   // -0
        console.log(Math.sign('-0'));   // -0
        ```

        雖然 +0 和 -0 看起來相同，但 `Math.sign(x)` 會進行區分。在大多數情況下，+0 和 -0 的行為幾乎一致，但在某些運算 (例如：除法) 中可能會產生不同的結果。

    - 當 x 是 NaN (非數字)

        ```
        console.log(Math.sign(NaN));   // NaN
        console.log(Math.sign('aaa'));   // NaN
        ```

- 應用場景

    - 快速判斷數字的符號

        `Math.sign(x)` 常用在需要知道一個數字是正數、負數還是 0 的時候。

        ```
        let num = -8;
        if (Math.sign(num) === 1) {
            console.log('這是正數');
        } else if (Math.sign(num) === -1) {
            console.log('這是負數');
        } else {
            console.log('這是 0');
        }
        ```

    - 配合絕對值進行運算
    
        與 `Math.abs(x)` 一起使用時，可以將一個數字的符號與大小分離。

        ```
		let num = -9.5;
		let sign = Math.sign(num);
		let absValue = Math.abs(num);
		console.log(sign * absValue);   // -9.5
        ```

        以上方法可以在保留原始符號的情況下，進行其他計算。

### 常見誤區

- 對非數字的處理：如果傳入的是非數值類型，Math.sign(x) 會返回 NaN，因此需要注意確保傳入的值是數字。

    ```
    console.log(Math.sign("text"));   // NaN
    ```

### 總結

`Math.sign(x)` 是用來判斷數字符號的實用方法，返回的結果可以幫助快速了解數字是正數、負數還是 0，並且還能區分 +0 和 -0。

`Math.sign(x)` 的應用範圍廣泛，特別是在需要根據數字符號進行條件判斷時，非常方便。與 `Math.abs(x)` 結合使用時，也能靈活處理數字的大小和符號分離操作。
