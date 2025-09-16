# Angular Decorators

以下是 Angular 的 Decorators (裝飾器) 整理。

<br />

## 類別裝飾器 (Class Decorators)

類別裝飾器用於將 TypeScript 類別標記為 Angular 的特定類型，並提供元資料供框架使用。

### `@Component`

- 用途：宣告一個類別為元件 (Component)。元件是 Angular 應用程式中最基本的建構區塊，負責管理一個網頁區塊 (View) 並與使用者互動。

- 語法

    ```typescript
    import { Component, ViewEncapsulation, ChangeDetectionStrategy } from '@angular/core';

	@Component({
	  selector: 'app-my-component',
	  templateUrl: './my-component.component.html',
	  styleUrls: ['./my-component.component.css'],
	  // 或使用內聯模式
	  // template: '<p>Hello World</p>',
	  // styles: ['p { color: blue; }'],

	  encapsulation: ViewEncapsulation.Emulated,         // 樣式封裝模式
	  changeDetection: ChangeDetectionStrategy.Default   // 變更檢測策略
	})
	export class MyComponent {
	  title = 'My Component';
	}
    ```

- 說明

    - `@Component`：一種特殊的 `@Directive`，帶有額外的屬性 (例如：`template`、`styles`)，用來定義元件的視圖。

    - `selector`：定義一個自訂的 HTML 標籤。Angular 在模板中解析到該標籤時，會建立對應的元件實例並插入 DOM。

    - `templateUrl`/`template`：定義元件的 HTML 模板，也就是控制的視圖結構。

    - `styleUrls`/`styles`：定義元件的樣式表。這些樣式通常作用域化，只影響該元件的模板。
