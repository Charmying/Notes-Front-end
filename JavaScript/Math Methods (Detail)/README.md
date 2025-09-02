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

<br />

## Math.max(...values)

`Math.max(...values)` 是 JavaScript 中用來找出一組數字中最大值的內建方法，接受多個數值作為參數，並返回其中最大的那個數字。如果沒有任何參數，則返回 -Infinity，表示在空集合中沒有最大值。如果傳入的參數包含 NaN，則返回 NaN。

### 基本語法

```
Math.max(value1, value2, ..., valueN);
```

- value1, value2, ..., valueN 是想要比較的數字。

### 詳細說明

- 多個數值比較

    `Math.max(...values)` 可以接受任意數量的數值，並從中找出最大的數。當傳入多個參數時會逐一比較，並返回其中最大的數字。

- 範例

    - 多個正數

        ```
        console.log(Math.max(1, 3, 5, 7, 9));   // 9
        ```

    - 多個負數

        ```
        console.log(Math.max(-3, -7, -10));   // -3
        ```

    - 混合正數與負數

        ```
        console.log(Math.max(-1, -5, 10, 0, 8));   // 10
        ```

    - 無參數的情況

        ```
        console.log(Math.max());   // -Infinity
        ```

    - NaN 的情況

        ```
        console.log(Math.max(1, 2, NaN, 4));   // NaN
        ```

- 應用場景

    - 比較一組數字的大小
    
        `Math.max(...values)` 常被用來快速比較一組數字，找到其中的最大值。

        例如：需要找到一組成績中的最高分

        ```
        let scores = [70, 85, 92, 88];
		let highestScore = Math.max(...scores);
		console.log(highestScore);   // 92
        ```

        在這個範例中，使用了展開運算符 (`...`)，將陣列轉換成多個參數傳入 `Math.max(...values)`，找到最高的分數。

    - 動態處理資料

        當資料是動態產生時，可以使用 `Math.max(...values)` 找出其中的最大值。

        例如：從一組來自表單輸入的數字中找出最大值

        ```
        let userInputs = [10, -5, 100, 23];
		let maxInput = Math.max(...userInputs);
		console.log(maxInput);   // 100
        ```

- 與 `Math.min(...values)` 的比較

    - `Math.max(...values)` 返回一組數字中的最大值，而 `Math.min(...values)` 則返回最小值。兩者在功能上是互補的，可以一起使用來同時找到最大值和最小值

        ```
        let numbers = [3, 7, -2, 0, 15];
		console.log(Math.max(...numbers));   // 15
		console.log(Math.min(...numbers));   // -2
        ```

### 常見誤區

- `Math.max(...values)`  不接受陣列作為參數：`Math.max(...values)`  的參數必須是數字，而不是陣列。如果想從一個陣列中找出最大值，需要使用展開運算符 (`...`) 來將陣列展開成多個數字

    ```
	let arr = [4, 9, 1];
	console.log(Math.max(arr));   // NaN
	console.log(Math.max(...arr));   // 9    
    ```

### 總結

`Math.max(...values)` 是一個用來找出多個數字中最大值的方法，可以比較任意數量的數字，並返回其中的最大值。常用於數字比較、資料處理等場景。需要注意的是，如果參數中有 NaN，結果會是 NaN，而無參數時則返回 -Infinity。

<br />

## Math.min(...values)

`Math.min(...values)` 是 JavaScript 中用來找出一組數字中最小值的內建方法，接受多個數值作為參數，並返回其中最小的那個數字。如果沒有任何參數，則返回 -Infinity，表示在空集合中沒有最小值。如果傳入的參數包含 NaN，則返回 NaN。

### 基本語法

```
Math.min(value1, value2, ..., valueN);
```

- value1, value2, ..., valueN 是想要比較的數字。

### 詳細說明

- 多個數值比較

    `Math.max(...values)` 可以接受任意數量的數值，並從中找出最小的數。當傳入多個參數時會逐一比較，並返回其中最小的數字。

- 範例

    - 多個正數

        ```
        console.log(Math.min(3, 7, 1, 9));   // 1
        ```

    - 多個負數

        ```
        console.log(Math.min(-8, -5, -10));   // -10
        ```

    - 混合正數與負數

        ```
        console.log(Math.min(-3, 5, -1, 2));   // -3
        ```

    - 無參數的情況

        ```
        console.log(Math.min());   // -Infinity
        ```

    - NaN 的情況

        ```
        console.log(Math.min(1, 2, NaN, 4));   // NaN
        ```

- 應用場景

    - 比較一組數字的大小
    
        `Math.min(...values)` 常被用來快速比較一組數字，找到其中的最小值。

        例如：在一組資料中找出最低價格或最小數量

        ```
		let prices = [500, 200, 300, 150];
		let lowestPrice = Math.min(...prices);
		console.log(lowestPrice);   // 150
        ```

        在這個範例中，使用了展開運算符 (`...`)，將陣列轉換成多個參數傳入 `Math.min(...values)`，找到最小的價格。

    - 動態處理資料

        當資料是動態產生時，可以使用 `Math.min(...values)` 找出其中的最小值。

        例如：從一組來自表單輸入的數字中找出最小值

        ```
		let userInputs = [20, -10, 30, 5];
		let minInput = Math.min(...userInputs);
		console.log(minInput);   // -10
        ```

- 與 `Math.max(...values)` 的比較

    - `Math.min(...values)` 返回一組數字中的最小值，而 `Math.max(...values)` 則返回最大值。兩者在功能上是互補的，可以一起使用來同時找到最小值和最大值

        ```
        let numbers = [3, 7, -2, 0, 15];
		console.log(Math.min(...numbers));   // -2
		console.log(Math.max(...numbers));   // 15
        ```

### 常見誤區

- `Math.min(...values)`  不接受陣列作為參數：`Math.min(...values)`  的參數必須是數字，而不是陣列。如果想從一個陣列中找出最小值，需要使用展開運算符 (`...`) 來將陣列展開成多個數字

    ```
	let arr = [4, 9, 1];
	console.log(Math.min(arr));   // NaN
	console.log(Math.min(...arr));   // 1
    ```

### 總結

`Math.min(...values)` 是一個用來找出多個數字中最小值的方法，可以比較任意數量的數字，並返回其中的最小值。常用於數字比較、資料處理等場景。需要注意的是，如果參數中有 NaN，結果會是 NaN，而無參數時則返回 -Infinity。

<br />

## Math.pow(base, exponent)

`Math.pow(base, exponent)` 是 JavaScript 中用來計算次方的內建方法，其中 base (底數) 和 exponent (指數)，返回底數 base 的 exponent 次方結果。也就是說，`Math.pow(base, exponent)` 會將底數提升到指數的冪次，並返回該數值。

### 基本語法

```
Math.pow(base, exponent);
```

- base：要被提升次方的數字 (底數)。

- exponent：提升的次數 (指數)。

### 詳細說明

- 指數運算的基本概念

    `Math.pow(base, exponent)` 是計算 base 提升到 exponent 次方。
    
    例如：如果想計算 2 的 3 次方 (2^3)

    ```
    console.log(Math.pow(2, 3));   // 8
    ```

- 範例

    - 正數指數

        當底數和指數都是正數的情況。

        ```
        console.log(Math.pow(3, 2));   // 9
        console.log(Math.pow(5, 3));   // 125
        ```
    - 負數指數

        當指數是負數時，`Math.pow(base, exponent)` 計算的是該底數的倒數。

        ```
        console.log(Math.pow(2, -3));   // 0.125
        console.log(Math.pow(10, -2));   // 0.01
        ```

    - 指數為零

        根據數學規則，任何數字的 0 次方都是 1。

        ```
        console.log(Math.pow(5, 0));   // 1
        console.log(Math.pow(100, 0));   // 1
        ```

    - 負數底數

        如果底數是負數，且指數是正整數，`Math.pow(base, exponent)` 會正常計算。

        ```
        console.log(Math.pow(-3, 3));   // -27
        console.log(Math.pow(-2, 4));   // 16
        ```

		當底數是負數且指數為奇數時，結果是負數（例如：-3^3 = -27）。
		
        當底數是負數且指數為偶數時，結果是正數（例如：-2^4 = 16）。

    - 小數指數

        `Math.pow(base, exponent)` 也可以處理小數指數。當指數為小數時，計算的結果是底數的根值。

        ```
        console.log(Math.pow(9, 0.5));   // 3   (9 的平方根)
        console.log(Math.pow(27, 1/3));   // 3   (27 的立方根)
        ```

    - NaN 和 Infinity

        如果傳入的參數中包含無效值 (例如：非數字)，`Math.pow(base, exponent)` 會返回 NaN。根據數學規則，某些情況下結果會是 Infinity 或 -Infinity

        ```
        console.log(Math.pow(0, -1));   // Infinity   (0 的負次方是無窮大)
        console.log(Math.pow(Infinity, 2));   // Infinity   (無窮大的平方還是無窮大)
        ```

- 應用場景

    - 指數運算：`Math.pow(base, exponent)` 可以用來計算科學或金融中的指數運算，例如：利息、增長率等。

    - 平方和立方：可以用來計算平方 `Math.pow(x, 2)` 或立方 `Math.pow(x, 3)`，也可以計算根號 (例如：平方根 `Math.pow(x, 0.5)`)。

### 替代方法

在 ES6 中，除了 `Math.pow(base, exponent)`，也可以使用指數運算符 (**) 來進行相同的運算。

```
console.log(2 ** 3);   // 8
console.log(5 ** 2);   // 25
```

### 範例總結

- 基本次方運算

    ```
    console.log(Math.pow(4, 3));   // 64
    ```

- 負數次方

    ```
    console.log(Math.pow(2, -2));   // 0.25
    ```

- 平方根計算

    ```
    console.log(Math.pow(16, 0.5));   // 4
    ```

- 倒數運算

    ```
    console.log(Math.pow(10, -1));   // 0.1
    ```

### 總結

`Math.pow(base, exponent)` 是用來計算次方的方法，允許將一個數字提升到特定的冪次。

`Math.pow(base, exponent)` 支援正數、負數和小數的指數運算，並能處理各種複雜的數學運算場景。無論是計算平方、立方或根值，`Math.pow(base, exponent)` 都是非常好用的方法。

<br />

## Math.sqrt(x)

`Math.sqrt(x)` 是 JavaScript 中用來計算平方根的內建方法。也就是說，當一個數字平方 (乘以自身) 等於 x 時，這個數字就是 x 的平方根。如果 x 是正數，返回其平方根；如果 x 是負數，則會返回 NaN，因為負數在實數範圍內沒有平方根。

### 基本語法

```
Math.sqrt(x);
```

- x：想要計算平方根的數字。

### 詳細說明

- 範例

    - 正數的平方根

        `Math.sqrt(x)` 會返回 x 的平方根。

        ```
        console.log(Math.sqrt(9));   // 3
        console.log(Math.sqrt(16));   // 4
        ```

    - 負數的平方根

        如果 x 是負數，`Math.sqrt(x)` 會返回 NaN (Not a Number)，因為在實數範圍內負數沒有平方根。

        ```
        console.log(Math.sqrt(-1));   // NaN
        ```

    - 0 的平方根

        如果 x 是 0，則平方根也是 0。

        ```
        console.log(Math.sqrt(0));   // 0
        ```

    - 小數的平方根

        `Math.sqrt(x)` 也可以處理小數，並返回該小數的平方根。

        ```
        console.log(Math.sqrt(0.25));   // 0.5
        console.log(Math.sqrt(2.25));   // 1.5
        ```

- 應用場景

    - 數學運算：`Math.sqrt(x)` 常用於數學計算中，例如：幾何問題或物理問題中，需要計算距離或面積時可能會用到平方根。

    - 計算歐幾里得距離：在計算兩點之間的距離時，`Math.sqrt(x)` 可以用來計算平方和的根值。

        ```
        let x1 = 3, y1 = 4;
		let x2 = 0, y2 = 0;
		let distance = Math.sqrt(Math.pow(x1 - x2, 2) + Math.pow(y1 - y2, 2));
		console.log(distance);   // 5
        ```

### 與 `Math.pow(base, exponent)` 的比較

`Math.sqrt(x)` 等同於 `Math.pow(x, 0.5)`，兩者都可以用來計算平方根

```
console.log(Math.sqrt(25));   // 5
console.log(Math.pow(25, 0.5));   // 5
```

### 常見誤區

- 負數的處理：`Math.sqrt(x)` 無法處理負數的平方根。如果需要處理負數的平方根，就需要進行複數運算，而 JavaScript 的內建 `Math.sqrt(x)` 並不支援複數運算。

### 總結

`Math.sqrt(x)` 是計算數字平方根的方法，常用於數學計算和科學應用中。對於正數會返回其平方根，對於負數則會返回 NaN。

<br />

## Math.cbrt(x)

`Math.cbrt(x)` 是 JavaScript 中用來計算立方根的內建方法。也就是說，當一個數字立方等於 x 時，這個數字就是 x 的立方根。與平方根不同，立方根可以接受負數，因為負數也有對應的立方根。

### 基本語法

```
Math.cbrt(x);
```

- x：想要計算立方根的數字。

### 詳細說明

- 範例

    - 正數的立方根

        如果 x 是正數，`Math.cbrt(x)` 會返回正的立方根

        ```
		console.log(Math.cbrt(8));   // 2
		console.log(Math.cbrt(27));   // 3
        ```

    - 負數的立方根

        與平方根不同，負數也有立方根。`Math.cbrt(x)` 可以計算負數的立方根。

        ```
        console.log(Math.cbrt(-8));   // -2
        console.log(Math.cbrt(-27));   // -3
        ```

    - 0 的立方根

        如果 x 是 0，則立方根也是 0。

        ```
        console.log(Math.cbrt(0));   // 0
        ```

    - 小數的立方根

        `Math.cbrt(x)`  也可以處理小數，並返回該小數的立方根。

        ```
        console.log(Math.cbrt(0.125));   // 0.5
        console.log(Math.cbrt(1.331));   // 1.1
        ```

- 應用場景

    - 數學運算：`Math.cbrt(x)`  常用於數學計算中，例如：計算三維體積或需要求解立方方程式的情況。

    - 幾何應用：計算立方體的邊長，當已知體積時，可以通過立方根來求出邊長。

        ```
		let volume = 64;
		let edgeLength = Math.cbrt(volume);
		console.log(edgeLength);   // 4
        ```

### 與 Math.pow(base, exponent) 的比較

雖然可以使用 `Math.pow(x, 1/3)` 來計算立方根，但 `Math.cbrt(x)` 是更精確和直接的方法，因為可以避免浮點運算中的誤差，特別是在處理負數時更為精確。

```
console.log(Math.cbrt(-1.331));   // -1.1
console.log(Math.pow(-1.331, 1/3));   // NaN
```

- `Math.cbrt(x)` 方法是專門用來計算數字的立方根，並且可以處理負數。

- `Math.pow(base, exponent)` 使用的是乘方計算式，無法處理帶有分數次方的負數。在數學上，對於負數的分數次方會涉及到複數的計算，因為 JavaScript 的 `Math.pow(base, exponent)` 無法直接處理複數，所以返回 NaN (Not a Number)，表示結果無法計算。


### 總結

`Math.cbrt(x)` 是用來計算立方根的方法，無論是正數、負數、小數還是零，都能給出正確的結果。與平方根不同，負數也有立方根，因此 `Math.cbrt(x)` 在處理負數時更好用。

<br />

## Math.log(x)

`Math.log(x)` 是 JavaScript 中用來計算自然對數的內建方法。自然對數是以指數函數 (數學常數) e (約等於 2.718) 為底的對數，簡單來說，就是計算當 e 的多少次方等於 x。在數學上，`Math.log(x)` 會返回一個數字，使得 e 的這個次方等於 x。

### 基本語法

```
Math.log(x);
```

- x：想要計算自然對數的數字，必須大於 0。

### 詳細說明

- 自然對數的基本概念

    `Math.log(x)` 計算的是自然對數，底數為 e (約等於 2.718)。也就是說，`Math.log(x)` 代表 e 的多少次方會等於 x
    
    例如：`Math.log(1)` 等於 0，因為 e 的 0 次方等於 1

    ```
    console.log(Math.log(1));   // 0
    ```

- 範例

    - 自然對數為正數

        當 x 是大於 0 的數字，`Math.log(x)` 會返回對應的自然對數值。

        ```
        console.log(Math.log(10));  // 結果：2.302585092994046
        console.log(Math.log(2));   // 結果：0.6931471805599453
        ```

    -  自然對數為 1

        `Math.log(1)` 返回 0，因為 e 的 0 次方等於 1。

        ```
        console.log(Math.log(1));   // 0
        ```

    - 自然對數為負數與 0

        `Math.log(x)` 只適用於 x > 0 的數字。如果 x 是 0 或負數，`Math.log(x)` 會返回 NaN，因為在實數範圍內沒有定義 0 或負數的自然對數。


        ```
        console.log(Math.log(0));   // -Infinity (負無窮大)
        console.log(Math.log(-1));   // NaN
        ```

    - 自然對數為小數

        `Math.log(x)` 也可以處理小於 1 的正數，返回的自然對數會是負數。

        ```
        console.log(Math.log(0.5));   // -0.6931471805599453
        ```

- 應用場景

    - 科學與工程：自然對數常用於描述指數增長、衰減的情況，例如：計算放射性衰變、複利利息等。

    - 經濟與統計：在經濟學中，自然對數用於計算投資的複利增長，或處理非線性數據時轉換數據進行線性回歸。


### 常用對數的變換

除了自然對數，如果想要計算 10 為底的對數，可以使用 `Math.log10(x)`，也可以通過數學公式轉換。

```
function log10(x) {
    return Math.log(x) / Math.LN10;
}

console.log(log10(100));   // 2
```

### `Math.log(x)` 與 `Math.exp(x)` 的關係

`Math.exp(x) 是計算 e 的 x 次方`，而 `Math.log(x)` 則是計算 x 的自然對數，兩者互為反函數。

```
console.log(Math.exp(Math.log(5)));   // 5
console.log(Math.log(Math.exp(2)));   // 2
```

### 總結

`Math.log(x)` 是用來計算自然對數的工具，在數學、科學和經濟等領域有廣泛應用。`Math.log(x)` 能夠處理大於 0 的正數，返回以 e 為底的對數值。自然對數特別適用在描述指數增長和衰減的問題，但要注意，x 必須是正數，否則會返回 NaN 或 -Infinity。

<br />

## Math.log10(x)

`Math.log10(x)` 是 JavaScript 中用來計算以 10 為底數的對數的內建方法。也就是說，`Math.log10(x)` 會返回一個數字，使得 10 的這個次方等於 x。對數運算在科學、工程和數據分析中經常用來處理大範圍的數值，特別是當數據以指數方式增長或衰減時。

### 基本語法

```
Math.log10(x);
```

- x：想要計算以 10 為底的對數數字，必須大於 0。

### 詳細說明

- 以 10 為底的對數基本概念

    - `Math.log10(x)` 計算的是以 10 為底的對數，表示的是 10 的多少次方等於 x。

- 範例

    - 以 10 為底對數為正數

        當 x 是大於 0 的正數時，`Math.log10(x)` 會返回對應的對數值。

        ```
        console.log(Math.log10(10));   // 1
        console.log(Math.log10(100));   // 2
        ```

    - 以 10 為底對數為 1

        `Math.log10(1)` 返回 0，因為 10 的 0 次方等於 1。

        ```
        console.log(Math.log10(1));   // 0
        ```

    -  以 10 為底對數為負數與 0

        `Math.log10(x)` 只適用於 x > 0 的數字。如果 x 是 0 或負數，`Math.log10(x)` 會返回 NaN 或 -Infinity。

        ```
        console.log(Math.log10(0));   // -Infinity
        console.log(Math.log10(-10));   // NaN
        ```

    - 以 10 為底對數為小數

        當 x 是介於 0 到 1 之間的小數時，返回的對數值是負數。

        ```
        console.log(Math.log10(0.1));   // -1
        console.log(Math.log10(0.01));   // -2
        ```

- 應用場景

    - 數據處理：以 10 為底的對數在數據處理中被廣泛應用，特別是在處理數據範圍很大的時候，對數有助於壓縮數據範圍，便於觀察和分析。

    - 工程與科學計算：在電學、聲學等領域，對數用於表示數值差異，例如：分貝 (dB) 表示音量的差異。

### 與 `Math.log(x)` 的比較

- `Math.log10(x)` 是專門用來計算以 10 為底的對數，而 `Math.log(x)` 則是計算自然對數 (底數是 e)。兩者的底數不同，但都屬於對數運算。

- 使用 `Math.log(x) / Math.LN10` 也可以實現相同效果，因為 `Math.LN10` 是自然對數 `log(10)` 的常數。

    ```
    function log10(x) {
        return Math.log(x) / Math.LN10;
    }

    console.log(log10(100));   // 2
    ```

### 總結

`Math.log10(x)` 是用來計算以 10 為底對數的方法，能夠快速計算正數的對數值，並且在處理大範圍數據或指數增長問題時也非常有用。需要注意的是 x 必須是大於 0 的正數，否則會返回 NaN 或負無窮大。

<br />

## Math.log2(x)

`Math.log2(x)` 是 JavaScript 中用來計算以 2 為底數的對數的內建方法。也就是說，`Math.log2(x)` 會返回一個數字，使得  2 的這個次方等於 x。二進位對數在電腦科學、數據分析和許多計算領域中相當常見，因為二進位制是數位電腦的基礎。

### 基本語法

```
Math.log2(x);
```

- x：想要計算以 2 為底的對數數字，必須大於 0。

### 詳細說明

- 以 2 為底的對數基本概念

    - `Math.log2(x)` 計算的是以 2 為底的對數，意思是 2 的多少次方會等於 x。

    - 以 2 為底的對數特別常見於電腦科學，因為電腦使用二進位制，計算記憶體大小、處理器運算次數等，都會用到以 2 為底的對數。

- 範例

    - 以 2 為底對數為正數

        當 x 是大於 0 的正數時，`Math.log2(x)` 會返回對應的對數值。

        ```
		console.log(Math.log2(8));   // 3
		console.log(Math.log2(32));   // 5
        ```

    - 以 2 為底對數為 1

        `Math.log2(1)` 返回 0，因為 2 的 0 次方等於 1。

        ```
        console.log(Math.log2(1));   // 0
        ```

    - 以 2 為底對數為負數與 0

        `Math.log2(x)` 只適用於 x > 0 的數字。如果 x 是 0 或負數，`Math.log2(x)` 會返回 NaN 或 -Infinity。

        ```
		console.log(Math.log2(0));   // -Infinity
		console.log(Math.log2(-4));   // NaN
        ```

    - 以 2 為底對數為小數

        當 x 是介於 0 到 1 之間的小數時，返回的對數值是負數。

        ```
		console.log(Math.log2(0.5));   // -1
		console.log(Math.log2(0.25));   // -2
        ```

- 應用場景

    - 電腦科學：二進位對數用於分析算法的複雜度，特別是二分搜尋、樹狀結構、加密等運算。

    - 數據壓縮與編碼：在處理訊息和數據時，二進位對數可以幫助壓縮數據和計算熵值。

    - 處理大型數據：處理大範圍數據時，使用二進位對數可以使數據範圍更可管理。

### 與 `Math.log(x)` 的比較

- `Math.log2(x)` 是專門用來計算以 2 為底的對數，而 `Math.log(x)` 則是計算自然對數 (底數是 e)。兩者的底數不同，但都屬於對數運算。

- 使用 `Math.log(x) / Math.LN2` 也可以實現相同效果，因為 `Math.LN2` 是自然對數 log(2) 的常數。

    ```
	function log2(x) {
	    return Math.log(x) / Math.LN2;
	}

	console.log(log2(8));  // 結果：3
    ```

### 總結

`Math.log2(x)` 是用來計算以 2 為底對數的方法，特別適用於電腦科學和數據處理領域。`Math.log2(x)` 能夠快速計算二進位對數，對於處理指數增長、數據壓縮等問題非常有幫助。

<br />

## Math.exp(x)

`Math.exp(x)` 是 JavaScript 中用來計算以指數函數 (數學常數) e (約等於 2.718) 為底的指數的內建方法。e 是自然對數的基礎。`Math.exp(x)` 會返回 e 的 x 次方結果，也就是說，計算的是 `e^x`。

### 基本語法

```
Math.exp(x);
```

- x：要計算的次方指數。

### 詳細說明

- 指數的基本概念

    - `Math.exp(x)` 用來計算數學中的指數運算，底數是自然數 e，這個數字在數學和科學中非常重要。`Math.exp(x)` 就是 `e^x`，也就是 e 的 x 次方。

- 範例

    - 指數為正數

        當 x 是正數時，`Math.exp(x)` 會返回 e 的正數次方。

        ```
		console.log(Math.exp(2));   // 7.38905609893065
		console.log(Math.exp(3));   // 20.085536923187668
        ```

    - 指數為 0

        `Math.exp(0)` 返回 1，因為任何數字的 0 次方都是 1，包括 e 也是。

        ```
        console.log(Math.exp(0));   // 1
        ```

    - 指數為負數

        當 x 是負數時，`Math.exp(x)` 會返回 e 的負數次方，也就是說，計算的是 `1 / e^x`。

        ```
		console.log(Math.exp(-1));   // 0.36787944117144233
		console.log(Math.exp(-2));   // 0.1353352832366127
        ```

- 應用場景

    - 科學與工程：`Math.exp(x)` 常用於處理自然增長和衰減現象，例如：計算放射性衰變、複利利息、人口增長等。除此之外還在熱力學、電學、經濟學中有著廣泛的應用。

    - 計算自然對數的反函數：`Math.exp(x)` 是自然對數 `Math.log(x)` 的反函數，也就是說，兩者可以互相抵消。

        ```
        console.log(Math.exp(Math.log(5)));   // 5
        console.log(Math.log(Math.exp(2)));   // 2
        ```

### 總結

`Math.exp(x)` 是用來計算自然數 e 的 x 次方的方法，特別是在處理指數增長或衰減問題時，常見於科學、經濟學和工程領域。`Math.exp(x)` 也是自然對數的反函數，因此可以用來還原通過自然對數計算出的結果。可以特別注意的是，當 x 是 0 時，結果是 1，而 x 是負數時，結果是 e 的倒數。

<br />

## Math.sin(x)

`Math.sin(x)` 是 JavaScript 中用來計算一個角度正弦值的內建方法。正弦函數是三角學中的基本函數之一，用來描述一個直角三角形中對邊與斜邊的比值。`Math.sin(x)` 輸入的 x 是一個弧度 (radians)，而不是角度 degrees)。

### 基本語法

```
Math.sin(x);
```

- x：要計算正弦值的角度 (以弧度為單位)。

### 詳細說明

- 角度與弧度的轉換

    - 在 JavaScript 中，`Math.sin(x)` 接收的是弧度。如果想用角度來計算，要先將角度轉換成弧度。
    
        弧度 = 角度 × (π/180)

    - 例如：30 度等於 `30 × Math.PI / 180`，這樣會轉換成約 0.5236 弧度。

- 正弦函數的基本定義

    - 正弦函數是在一個直角三角形中，對應角的對邊長度與斜邊長度的比值。`Math.sin(x)` 返回的值範圍在 -1 到 1 之間。

    - 例如：`Math.sin(0)` 返回 0，因為 0 度 (或 0 弧度) 的正弦值是 0。

- 常見的正弦值

    - `Math.sin(0)` 返回 0，因為 0 弧度的正弦值是 0。

    - `Math.sin(Math.PI / 2)` 返回 1，因為 90 度 (π/2 弧度) 的正弦值是 1。

    - `Math.sin(Math.PI)` 返回 1.2246467991473532e-16 (因為浮點數精度限制導致)，在數學上 180 度 (π 弧度) 的正弦值是 0。

        解決方法

        - 使用容差範圍 (epsilon)

            ```
            const result = Math.sin(Math.PI);
            const epsilon = 1e-10;   // 容許的誤差範圍

            if (Math.abs(result) < epsilon) {
                console.log(0);   // 如果結果接近 0，輸出 0
            } else {
                console.log(result);   // 否則輸出原始結果
            }
            ```

        - 使用 `toFixed()` 來限制小數位數

            ```
            console.log(Math.sin(Math.PI).toFixed(10));   // 0.0000000000
            ```

- 範例

    - 弧度為正數

        計算 π/2 弧度的正弦值 (90 度)。
        
        ```
        console.log(Math.sin(Math.PI / 2));   // 1
        ```

    - 弧度為 0

        ```
        console.log(Math.sin(0));   // 0
        ```

    - 弧度為負數

        當輸入負數弧度時，`Math.sin(x)` 會返回相應的負數值。

    	```
    	console.log(Math.sin(-Math.PI / 2));   // -1
    	```

    - 弧度為小數點

        當輸入小數弧度時，`Math.sin(x)` 會返回該弧度的正弦值。

    	```
    	console.log(Math.sin(0.5));   // 0.479425538604203
    	```

    - 轉換角度為弧度並計算正弦值

        ```
        let angle = 60;
		let radian = angle * (Math.PI / 180);
		console.log(Math.sin(radian));   // 0.8660254037844386
        ```

- 範例程式碼

    ```
    // 計算 30 度的正弦值
    let degrees = 30;
    let radians = degrees * (Math.PI / 180);
    console.log(Math.sin(radians));   // 0.49999999999999994 (約等於 0.5)

    // 計算 90 度的正弦值
    console.log(Math.sin(Math.PI / 2));   // 1
    ```

- 應用場景

    - 波動與震盪：正弦函數常被用來描述週期性運動，例如：聲波、光波或電磁波的震盪。

    - 物理學：在力學中，描述簡諧運動或圓周運動的物體時，就會使用到正弦函數。

    - 電學與訊號處理：在分析交變電流或正弦波訊號時，正弦函數非常重要。

### 總結

`Math.sin(x)` 是用來計算角度的正弦值的函數，常用於描述週期運動、波動以及其他相關的物理現象。計算時需要注意 JavaScript 中的角度必須先轉換為弧度才能進行正弦計算。正弦值的範圍介於 -1 到 1 之間。
