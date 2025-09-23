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

- 指令的三種類型

    - Component (元件型指令)：特殊的指令，帶有模板與樣式，例如：`@Component`。

    - Attribute Directive (屬性型指令)：改變元素外觀或行為，不改變 DOM 結構，例如：`ngClass`、`ngStyle`、自訂 `appHighlight`。

    - Structural Directive (結構型指令)：改變 DOM 結構，語法通常加上 `*`，例如：`*ngIf`、`*ngFor`、`*ngSwitchCase`。

### `@NgModule`

- 用途：將相關的元件 (Component)、指令 (Directive)、管道 (Pipe) 和服務 (Service) 組織成模組 (Module)，讓應用程式更有結構性、可維護性。

    - 根模組 (Root Module)：每個 Angular 應用程式至少有一個，用於啟動整個應用。

    - 功能模組 (Feature Module)：封裝特定功能的元件或服務，可在 `AppModule` 或其他模組中引用。

- 語法

    ```typescript
	import { NgModule, CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';
	import { CommonModule } from '@angular/common';
	import { FormsModule } from '@angular/forms';

	@NgModule({
	  declarations: [MyComponent, HighlightDirective, CapitalizePipe],   // 模組內的元件、指令、管道
	  imports: [CommonModule, FormsModule],                              // 引入其他模組
	  providers: [MyService],                                            // 提供服務 (非必要，推薦用 providedIn)
	  exports: [MyComponent, CapitalizePipe],                            // 對外導出
	  bootstrap: [AppComponent],                                         // 根模組才需要
	  schemas: [CUSTOM_ELEMENTS_SCHEMA]                                  // 可選，允許自定義元素
	})
	export class AppModule {}
    ```

- 說明

    - `declarations`：模組內的元件、指令和管道，必須宣告才能在模板中使用。

    - `imports`：引入其他模組，使用導出的元件、指令或服務。

    - `providers`：在模組範圍提供服務，Angular 透過依賴注入管理生命週期。

    - `exports`：導出模組內的元件、指令或管道，供其他模組引用。

    - `bootstrap`：僅在根模組使用，指定啟動元件。

    - `schemas`：允許使用非 Angular 元件或自定義元素

        - `CUSTOM_ELEMENTS_SCHEMA`：允許自定義 Web Components。

        - `NO_ERRORS_SCHEMA`：忽略 Angular 不認識的屬性與元素 (用得少，避免濫用)。

    - `AppModule`：每個 Angular 用程式至少有一個 `AppModule` (根模組)，定義應用程式範圍，告訴 Angular 如何組裝應用程式。

- 補充

    - 懶加載 (Lazy Loading)：功能模組可透過 Angular Router 延遲載入，提升效能。

    - `providers` vs `providedIn`

        - `providers: [Service]`：服務實例只存在於該模組。

        - `@Injectable({ providedIn: 'root' })`：全應用單例，支援 Tree-Shaking。

    - 模組化優勢

        - 隔離功能 (例如：`UserModule`、`AdminModule`)。

        - 減少耦合，提高可維護性。

        - 提供可重複使用的模組 (例如：`SharedModule`)。

### `@Pipe`

- 用途：宣告一個類別為管道 (Pipe)，用於在模板中轉換資料，例如：i18n 翻譯、日期格式化、文字格式化等。

- 語法

    ```typescript
	@Pipe({
	  name: 'capitalize',
	  pure: true   // 預設為純管道
	})
	export class CapitalizePipe implements PipeTransform {
	  transform(value: string, ...args: any[]): string {
	    if (!value) return '';
	    return value.charAt(0).toUpperCase() + value.slice(1).toLowerCase();
	  }
	}
    ```

- 使用方式

    ```html
	<!-- 基本使用 -->
	{{ message | capitalize }}

	<!-- 帶參數的管道 -->
	{{ date | date:'yyyy-MM-dd' }}

	<!-- 鏈式管道 (可串接多個管道) -->
	{{ price | currency:'USD' | lowercase }}
    ```

- 說明

    - `@Pipe` 必須實作 `PipeTransform` 介面，並提供 `transform` 方法處理資料。

    - `name`：管道在模板中的名稱。

    - `pure`：管道是否為純管道

        - `true` (預設)：僅在輸入值改變時執行。

        - `false`：每次變更檢測都會執行，適合處理非純函數或外部狀態，但可能影響效能。

    - `transform`

        - 第一個參數是輸入值。

        - 之後的參數對應模板中的管道參數。

- 內建常用管道

    - 文字處理：`uppercase`、`lowercase`、`titlecase`。

    - 數字/貨幣：`number`、`percent`、`currency`。

    - 日期：`date` (支援格式化字串，例如：yyyy-MM-dd)。

    - JSON & Slice：`json`、`slice`。

    - 非同步：`async` (自動訂閱 `Observable`/`Promise`)。
