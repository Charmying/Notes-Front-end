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

### `@Injectable`

- 用途：將類別標記為可被 Angular 依賴注入 (Dependency Injection，簡稱：DI) 系統管理的服務。當類別需要注入其他服務，或需要指定提供範圍時，必須加上 `@Injectable`。

- 語法

    ```typescript
	@Injectable({
	  providedIn: 'root'   // 在根注入器提供，整個應用程式共享
	})
	export class DataService {
	  private apiUrl = 'https://api.example.com';

	  constructor(private http: HttpClient) {}

	  getData(): Observable<any[]> {
	    return this.http.get<any[]>(`${this.apiUrl}/data`);
	  }
	}
    ```

- 說明

    - `@Injectable` 標記的類別由 Angular DI 容器管理生命週期，一般不直接用 `new` 建立。

    - `providedIn` 屬性：定義服務的可用範圍

        - `'root'`：在 根注入器 提供，整個應用程式共用單一實例 (最常用，支援 Tree-shaking)。

        - `'platform'`：在平台注入器提供，跨多個 Angular 應用程式共用。

        - `'any'`：每個 延遲載入模組 或 注入器 會建立自己的實例。

        - 特定模組：`providedIn: SomeModule`，僅在該模組範圍內可用。

- 補充

    - 如果服務不需要注入其他依賴，可以省略 `@Injectable`，但若要使用 `providedIn`，則必須加上。

    - 建議使用 `providedIn: 'root'`，可減少 `providers` 的設定並提升效能。

<br />

## 屬性裝飾器 (Property Decorators)

屬性裝飾器用於裝飾類別中的屬性，定義其在模板中與 DOM 互動的方式。

### `@Input`

- 用途：將屬性標記為輸入屬性 (Input Property)，允許父元件將資料傳遞給子元件。

- 語法

    ```typescript
	export class ChildComponent {
	  /** 基本用法 */
	  @Input() title: string = '';

	  /** 使用別名 */
	  @Input('user-data') userData: User | null = null;

	  /** 使用 setter 處理資料 */
	  private _count = 0;
	  @Input()
	  set count(value: number) {
	    this._count = value < 0 ? 0 : value;
	  }
	  get count(): number {
	    return this._count;
	  }

	  /** 具備預設值的輸入屬性 */
	  @Input() theme: 'light' | 'dark' = 'light';
	}
    ```

- 父元件使用方式

    ```html
	<app-child 
	  [title]="parentTitle"
	  [user-data]="currentUser"
	  [count]="itemCount"
	  theme="dark">
	</app-child>
    ```

- 說明

    - 在父元件模板中使用子元件選擇器時，可透過 屬性綁定 (`[property]="value"`) 傳遞資料，子元件透過 `@Input` 接收。

    - 支援任何 TypeScript 型別：基本型別、物件、陣列、自訂型別等。

    - 可搭配 setter，在資料更新時執行程式 (例如：驗證、轉換)。

    - 別名可讓模板屬性名稱與類別屬性名稱不同 (`@Input('alias')`)。

    - Angular 變更檢測 (Change Detection) 會自動追蹤 `@Input` 的更新，並在子元件中觸發 `ngOnChanges()` 生命週期鉤子。

    - `@Input` 屬性應為公開 (Public)，否則 Angular 無法存取。

### `@Output`

- 用途：將屬性標記為輸出屬性 (Output Property)，讓子元件發出事件通知父元件。

- 語法

    ```typescript
	export class ChildComponent {
	  /** 基本事件發射器 */
	  @Output() clicked = new EventEmitter<void>();

	  /** 帶資料事件 */
	  @Output() dataChanged = new EventEmitter<string>();

	  /** 使用別名 */
	  @Output('item-selected') itemSelected = new EventEmitter<number>();

	  onButtonClick() {
	    this.clicked.emit();
	  }

	  onInputChange(value: string) {
	    this.dataChanged.emit(value);
	  }

	  selectItem(id: number) {
	    this.itemSelected.emit(id);
	  }
	}
    ```

- 父元件監聽方式

    ```html
	<app-child 
	  (clicked)="onChildClicked()"
	  (dataChanged)="onDataChanged($event)"
	  (item-selected)="onItemSelected($event)">
	</app-child>
    ```

- 說明

    - `@Output` 屬性必須是 `EventEmitter<T>` 的實例。

    - 在父元件模板中使用事件綁定 (`(event)="handler($event)"`) 來接收事件。

    - 搭配型別化 `EventEmitter<T>` 可增加型別安全。

    - 使用 `emit()` 方法觸發事件並傳遞資料給父元件。

### `@ViewChild` 和 `@ViewChildren`

- 用途：查詢元件模板中自己的視圖 (View) 元素或子元件。

    - `@ViewChild`：取得第一個符合條件的實例。

    - `@ViewChildren`：取得所有符合條件的實例 (回傳 `QueryList<T>`)。

- 語法

    ```typescript
	export class ParentComponent implements AfterViewInit {
	  /** 查詢單一元件 */
	  @ViewChild(ChildComponent) childComponent!: ChildComponent;

	  /** 查詢單一 DOM 元素 (模板引用變數) */
	  @ViewChild('myInput') inputElement!: ElementRef<HTMLInputElement>;

	  /** 查詢單一元素並指定回傳類型 */
	  @ViewChild('myTemplate', { read: TemplateRef }) 
	  template!: TemplateRef<any>;

	  /** 查詢多個元件 */
	  @ViewChildren(ChildComponent) 
	  childComponents!: QueryList<ChildComponent>;

	  /** 查詢多個元素 */
	  @ViewChildren('item', { read: ElementRef }) 
	  items!: QueryList<ElementRef>;

	  /** 靜態查詢 (在 ngOnInit 前即可取得) */
	  @ViewChild('staticElement', { static: true }) 
	  staticElement!: ElementRef;

      /** ViewChild 和 ViewChildren 在這裡才會初始化 */
	  ngAfterViewInit() {
	    console.log(this.childComponent);
	    console.log(this.inputElement.nativeElement.value);

	    this.childComponents.forEach(child => {
	      console.log(child);
	    });
	  }
	}
    ```

- 說明

    - 這兩個裝飾器預設在 `ngAfterViewInit` 生命週期中初始化，用於存取模板中的 DOM 元素或元件實例。

    - `static` 選項

        - `static: true`：在 ngOnInit 前就可取得 (適合靜態元素)。

        - `static: false` (預設)：需等到 ngAfterViewInit 才能取得 (適合動態元素)。

    - 可搭配 `read` 選項指定取回型別，例如：`ElementRef`、`TemplateRef`、元件或指令。

    - `@ViewChild` 回傳第一個符合條件的實例。

    - `@ViewChildren` 回傳 `QueryList<T>`，支援集合操作，例如：`forEach`、`map`。

### `@ContentChild` 和 `@ContentChildren`

- 用途：查詢投影到元件 `<ng-content>` 區域中的元素或子元件。

    - `@ContentChild`：取得第一個符合條件的實例。

    - `@ContentChildren`：取得所有符合條件的實例 (回傳 `QueryList<T>`)。

- 語法

    ```typescript
	export class WrapperComponent implements AfterContentInit {
	  /** 查詢投影的單一元件 */
	  @ContentChild(ProjectedComponent) 
	  projectedComponent!: ProjectedComponent;

	  /** 查詢投影的單一元素 */
	  @ContentChild('projectedElement') 
	  element!: ElementRef;

	  /** 查詢投影的多個元件 */
	  @ContentChildren(ProjectedComponent) 
	  projectedComponents!: QueryList<ProjectedComponent>;

	  /** 查詢特定指令 */
	  @ContentChild(MyDirective) 
	  directive!: MyDirective;

	  /** ContentChild 和 ContentChildren 在這裡才會初始化 */
	  ngAfterContentInit() {
	    console.log(this.projectedComponent);
	    
	    this.projectedComponents.forEach(component => {
	      console.log(component);
	    });
	  }
	}
    ```

- 說明

    - 這兩個裝飾器會在內容投影完成後才有值，初始化於 `ngAfterContentInit`。

    - `@ContentChildren` 的 `QueryList` 若內容變動會自動更新，支援集合操作，例如：`forEach`、`map`。

    - 與 `@ViewChild`/`@ViewChildren` 的差異

        - `ViewChild`/`ViewChildren` 查詢元件自己的模板。

        - `ContentChild`/`ContentChildren` 查詢父元件投影進來的內容。

    - 可搭配 `{ static, read }` 選項控制查詢時機與回傳型別。

    - 適用於實現可重複使用的容器元件。
