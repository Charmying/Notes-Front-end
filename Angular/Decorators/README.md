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

- `encapsulation` (樣式封裝模式)

    Angular 提供 3 種封裝模式來控制元件樣式的影響範圍。

	| 模式 | 說明 | 影響範圍 | 適用情境 |
	| - | - | - | - |
	| `ViewEncapsulation.Emulated` (預設) | 模擬 Shadow DOM，Angular 會在元素上加上獨特屬性選擇器，讓樣式只影響該元件。 | 僅影響本元件 | 預設建議，最常用 |
	| `ViewEncapsulation.None` | 不做封裝，樣式直接作用於全域。 | 影響所有 DOM 元素 | 元素需要全域樣式或覆蓋外部樣式時 |
	| `ViewEncapsulation.ShadowDom` | 使用瀏覽器原生 Shadow DOM 進行隔離。 | 僅影響本元件 (真正隔離) | 需要原生 Shadow DOM 特性時 |

    ```typescript
    @Component({
	  selector: 'app-demo',
	  template: '<p class="red">Demo Works!</p>',
	  styles: ['.red { color: red; }'],
	  encapsulation: ViewEncapsulation.None
	})
	export class DemoComponent {}
    ```

    在 `None` 模式下，`.red { color: red; }` 會影響整個應用程式中所有 `.red`。

- `changeDetection` (變更檢測策略)

    Angular 提供 2 種變更檢測策略，控制元件何時重新檢查資料並更新畫面。

    | 策略 | 說明 | 適用情境 |
	| - | - | - |
	| `ChangeDetectionStrategy.Default` | 預設模式，Angular 偵測到任何可能的變化時都會重新檢查。 | 適用於大多數情境，開發方便但效能開銷較大。 |
	| `ChangeDetectionStrategy.OnPush`  | 僅在 `@Input` 值改變 or 事件/`Observable` 推送時觸發檢查。 | 適用於資料不常變動或需要最佳化效能的元件。 |

    ```typescript
    @Component({
	  selector: 'app-counter',
	  template: '{{ count }}',
	  changeDetection: ChangeDetectionStrategy.OnPush
	})
	export class CounterComponent {
	  @Input() count = 0;
	}
    ```

    以上範例中，只有當 `count` 的值真的改變時，Angular 才會重新檢查並更新畫面。


### `@Directive`

- 用途：宣告一個類別為指令 (Directive)，用於為現有 DOM 元素添加新的行為。與元件不同，指令沒有自己的模板。

- 語法

    ```typescript
    import { Directive, ElementRef, HostListener } from '@angular/core';

	@Directive({
	  selector: '[appHighlight]'   // 屬性選擇器，用 [] 包起來
	})
	export class HighlightDirective {
      constructor(private el: ElementRef) {}

	  @HostListener('mouseenter') onMouseEnter() {
	    this.highlight('yellow');
	  }

	  @HostListener('mouseleave') onMouseLeave() {
	    this.highlight(null);
	  }

	  private highlight(color: string | null) {
	    this.el.nativeElement.style.backgroundColor = color;
	  }
    }
    ```

- 說明

    - 常見的應用範圍

        - 改變元素的樣式。

        - 監聽宿主元素事件。

        - 控制 DOM 結構 (新增/移除節點)。

    - 可以視為「沒有模板的元件」。
