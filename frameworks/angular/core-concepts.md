# Angular 核心概念

## 目录

- [什么是 Angular](#什么是-angular)
- [Angular 的特点](#angular-的特点)
- [Angular 与其他框架的比较](#angular-与其他框架的比较)
- [Angular 核心概念](#angular-核心概念)
  - [组件](#组件)
  - [模板](#模板)
  - [指令](#指令)
  - [服务](#服务)
  - [依赖注入](#依赖注入)
  - [模块](#模块)
  - [路由](#路由)
  - [表单](#表单)
  - [HTTP 客户端](#http-客户端)
- [Angular 生命周期](#angular-生命周期)
- [Angular 状态管理](#angular-状态管理)
- [Angular 动画](#angular-动画)
- [Angular 测试](#angular-测试)
- [Angular 生态](#angular-生态)
- [Angular 最佳实践](#angular-最佳实践)
- [参考资源](#参考资源)

## 什么是 Angular

Angular 是一个由 Google 开发和维护的开源前端框架，用于构建单页应用（SPA）和复杂的企业级 Web 应用。它基于 TypeScript，并提供了一套完整的工具链和生态系统。

Angular 采用组件化架构，将应用划分为多个独立的组件，每个组件负责一部分 UI 和业务逻辑。它还提供了强大的依赖注入系统、路由管理、表单处理、HTTP 客户端等功能。

## Angular 的特点

1. **完整的框架**：提供了构建现代 Web 应用所需的所有功能
2. **组件化架构**：支持组件复用和组合
3. **TypeScript 支持**：默认使用 TypeScript，提供类型安全和更好的开发体验
4. **依赖注入**：内置强大的依赖注入系统
5. **响应式编程**：基于 RxJS 实现响应式数据流
6. **模块化设计**：支持模块封装和懒加载
7. **强大的 CLI 工具**：提供快速的项目生成和开发体验
8. **跨平台**：支持 Web、移动设备和桌面应用
9. **企业级支持**：由 Google 维护，适合大型企业应用
10. **丰富的生态系统**：拥有大量的官方和第三方库

## Angular 与其他框架的比较

| 特性 | Angular | React | Vue |
|------|---------|-------|-----|
| 类型 | 完整框架 | 库 | 渐进式框架 |
| 语言 | TypeScript | JavaScript/TypeScript | JavaScript/TypeScript |
| 架构 | 组件化 + 模块化 | 组件化 | 组件化 |
| 响应式系统 | RxJS | Virtual DOM | 响应式数据绑定 |
| 路由 | 内置 | React Router | Vue Router |
| 表单 | 内置（模板驱动 + 响应式） | 第三方库 | 内置（模板驱动 + 响应式） |
| 状态管理 | NgRx | Redux/Context API | Vuex/Pinia |
| 构建工具 | Angular CLI | Webpack/Vite | Vue CLI/Vite |
| 学习曲线 | 陡峭 | 中等 | 平缓 |
| 适合项目 | 大型企业应用 | 各种规模 | 各种规模 |

## Angular 核心概念

### 组件

组件是 Angular 应用的基本构建块，每个组件包含模板、样式和逻辑。

#### 组件结构

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root', // 组件选择器
  templateUrl: './app.component.html', // 模板文件
  styleUrls: ['./app.component.css'] // 样式文件
})
export class AppComponent {
  title = 'angular-app'; // 组件属性
  
  // 组件方法
  greet() {
    console.log('Hello, Angular!');
  }
}
```

#### 组件模板

```html
<!-- app.component.html -->
<h1>{{ title }}</h1>
<button (click)="greet()">点击我</button>
```

#### 组件样式

```css
/* app.component.css */
h1 {
  color: blue;
}

button {
  background-color: lightgray;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
```

### 模板

Angular 模板是一种特殊的 HTML，用于定义组件的 UI 结构。它支持数据绑定、指令和事件处理。

#### 数据绑定

- **插值绑定**：将组件属性显示到模板中
  ```html
  <h1>{{ title }}</h1>
  ```

- **属性绑定**：将组件属性绑定到 HTML 属性
  ```html
  <img [src]="imageUrl" [alt]="imageAlt">
  ```

- **事件绑定**：将模板事件绑定到组件方法
  ```html
  <button (click)="handleClick()">点击我</button>
  <input (keyup.enter)="handleEnter()">
  ```

- **双向绑定**：结合属性绑定和事件绑定
  ```html
  <input [(ngModel)]="name">
  ```

#### 模板表达式

模板中可以使用 JavaScript 表达式：

```html
<p>{{ 1 + 1 }}</p>
<p>{{ title.toUpperCase() }}</p>
<p>{{ isVisible ? '可见' : '不可见' }}</p>
```

### 指令

指令是 Angular 中用于修改 DOM 或组件行为的特殊标记。Angular 有三种类型的指令：

1. **组件指令**：带有模板的指令（组件本身就是一种指令）
2. **属性指令**：修改元素的外观或行为
3. **结构指令**：修改 DOM 结构

#### 内置属性指令

- **ngClass**：根据条件添加或移除 CSS 类
  ```html
  <div [ngClass]="{ 'active': isActive, 'disabled': isDisabled }"></div>
  ```

- **ngStyle**：动态设置 CSS 样式
  ```html
  <div [ngStyle]="{ 'color': textColor, 'font-size': fontSize + 'px' }"></div>
  ```

- **ngModel**：实现双向数据绑定
  ```html
  <input [(ngModel)]="name">
  ```

#### 内置结构指令

- **ngIf**：条件渲染
  ```html
  <div *ngIf="isVisible">可见内容</div>
  <div *ngIf="isVisible; else hiddenContent">可见内容</div>
  <ng-template #hiddenContent>不可见内容</ng-template>
  ```

- **ngFor**：列表渲染
  ```html
  <ul>
    <li *ngFor="let item of items; let i = index; trackBy: trackByFn">{{ i + 1 }}: {{ item.name }}</li>
  </ul>
  ```

- **ngSwitch**：根据条件渲染不同的内容
  ```html
  <div [ngSwitch]="status">
    <div *ngSwitchCase="'success'">成功</div>
    <div *ngSwitchCase="'warning'">警告</div>
    <div *ngSwitchCase="'error'">错误</div>
    <div *ngSwitchDefault>默认</div>
  </div>
  ```

#### 自定义指令

```typescript
// highlight.directive.ts
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  @Input() highlightColor = 'yellow';
  
  constructor(private el: ElementRef) {}
  
  @HostListener('mouseenter') onMouseEnter() {
    this.highlight(this.highlightColor);
  }
  
  @HostListener('mouseleave') onMouseLeave() {
    this.highlight('transparent');
  }
  
  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```

```html
<!-- 使用自定义指令 -->
<p [appHighlight]="'lightblue'">鼠标悬停时高亮</p>
```

### 服务

服务是用于封装可复用逻辑的类，如数据获取、业务逻辑等。

#### 创建服务

```typescript
// hero.service.ts
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';

@Injectable({
  providedIn: 'root' // 根注入器
})
export class HeroService {
  private heroes = [
    { id: 1, name: ' Superman' },
    { id: 2, name: ' Batman' },
    { id: 3, name: ' Wonder Woman' }
  ];
  
  getHeroes(): Observable<any[]> {
    return of(this.heroes);
  }
  
  getHero(id: number): Observable<any> {
    return of(this.heroes.find(hero => hero.id === id));
  }
}
```

#### 使用服务

```typescript
// hero.component.ts
import { Component, OnInit } from '@angular/core';
import { HeroService } from '../hero.service';

@Component({
  selector: 'app-hero',
  templateUrl: './hero.component.html'
})
export class HeroComponent implements OnInit {
  heroes: any[] = [];
  
  // 构造函数注入服务
  constructor(private heroService: HeroService) {}
  
  ngOnInit() {
    this.heroService.getHeroes().subscribe(heroes => {
      this.heroes = heroes;
    });
  }
}
```

### 依赖注入

依赖注入（DI）是 Angular 中的核心概念，用于管理组件和服务之间的依赖关系。

#### 依赖注入的优势

1. **松耦合**：组件不直接依赖具体的服务实现
2. **可测试性**：便于单元测试和模拟
3. **可维护性**：便于替换和升级服务
4. **可扩展性**：便于添加新的功能

#### 注入器层次结构

Angular 有一个注入器层次结构，从根注入器到组件注入器：

- **根注入器**：整个应用共享
- **模块注入器**：模块级别的注入器
- **组件注入器**：组件级别的注入器，继承自父组件注入器

### 模块

模块是 Angular 应用的组织单元，用于封装组件、服务、指令等。

#### 根模块

```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HeroComponent } from './hero/hero.component';

@NgModule({
  declarations: [ // 声明组件、指令和管道
    AppComponent,
    HeroComponent
  ],
  imports: [ // 导入其他模块
    BrowserModule,
    FormsModule,
    AppRoutingModule
  ],
  providers: [], // 提供服务
  bootstrap: [AppComponent] // 根组件
})
export class AppModule { }
```

#### 特性模块

```typescript
// heroes.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { HeroesRoutingModule } from './heroes-routing.module';
import { HeroListComponent } from './hero-list/hero-list.component';
import { HeroDetailComponent } from './hero-detail/hero-detail.component';

@NgModule({
  declarations: [
    HeroListComponent,
    HeroDetailComponent
  ],
  imports: [
    CommonModule,
    HeroesRoutingModule
  ],
  providers: []
})
export class HeroesModule { }
```

#### 懒加载模块

```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home/home.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  // 懒加载模块
  { 
    path: 'heroes', 
    loadChildren: () => import('./heroes/heroes.module').then(m => m.HeroesModule) 
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### 路由

Angular Router 用于管理应用的导航和 URL 路由。

#### 路由配置

```typescript
// heroes-routing.module.ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HeroListComponent } from './hero-list/hero-list.component';
import { HeroDetailComponent } from './hero-detail/hero-detail.component';

const routes: Routes = [
  { path: '', component: HeroListComponent },
  { path: ':id', component: HeroDetailComponent }
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class HeroesRoutingModule { }
```

#### 路由链接

```html
<!-- 基本路由链接 -->
<a routerLink="/heroes">英雄列表</a>

<!-- 动态路由链接 -->
<a [routerLink]="['/heroes', hero.id]">{{ hero.name }}</a>

<!-- 相对路由链接 -->
<a routerLink="./detail">详情</a>

<!-- 路由出口 -->
<router-outlet></router-outlet>
```

#### 路由守卫

路由守卫用于控制路由的访问权限：

```typescript
// auth.guard.ts
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}
  
  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): boolean {
    if (this.authService.isLoggedIn) {
      return true;
    } else {
      this.router.navigate(['/login']);
      return false;
    }
  }
}
```

```typescript
// app-routing.module.ts
const routes: Routes = [
  { 
    path: 'protected', 
    component: ProtectedComponent, 
    canActivate: [AuthGuard] 
  }
];
```

### 表单

Angular 提供了两种表单处理方式：

1. **模板驱动表单**：基于 HTML 表单元素和指令
2. **响应式表单**：基于代码驱动的表单控制

#### 模板驱动表单

```html
<!-- hero-form.component.html -->
<form #heroForm="ngForm" (ngSubmit)="onSubmit(heroForm)">
  <div class="form-group">
    <label for="name">姓名</label>
    <input type="text" id="name" name="name" ngModel required class="form-control">
  </div>
  
  <div class="form-group">
    <label for="power">超能力</label>
    <input type="text" id="power" name="power" ngModel required class="form-control">
  </div>
  
  <button type="submit" [disabled]="!heroForm.form.valid" class="btn btn-primary">提交</button>
</form>
```

```typescript
// hero-form.component.ts
import { Component } from '@angular/core';
import { NgForm } from '@angular/forms';

@Component({
  selector: 'app-hero-form',
  templateUrl: './hero-form.component.html'
})
export class HeroFormComponent {
  onSubmit(form: NgForm) {
    console.log('表单提交:', form.value);
  }
}
```

#### 响应式表单

```html
<!-- hero-reactive-form.component.html -->
<form [formGroup]="heroForm" (ngSubmit)="onSubmit()">
  <div class="form-group">
    <label for="name">姓名</label>
    <input type="text" id="name" formControlName="name" class="form-control">
    <div *ngIf="heroForm.get('name')?.invalid && heroForm.get('name')?.touched" class="text-danger">
      姓名是必填项
    </div>
  </div>
  
  <div class="form-group">
    <label for="power">超能力</label>
    <input type="text" id="power" formControlName="power" class="form-control">
  </div>
  
  <button type="submit" [disabled]="heroForm.invalid" class="btn btn-primary">提交</button>
</form>
```

```typescript
// hero-reactive-form.component.ts
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-hero-reactive-form',
  templateUrl: './hero-reactive-form.component.html'
})
export class HeroReactiveFormComponent implements OnInit {
  heroForm: FormGroup;
  
  constructor(private fb: FormBuilder) {}
  
  ngOnInit() {
    this.heroForm = this.fb.group({
      name: ['', Validators.required],
      power: ['', Validators.required]
    });
  }
  
  onSubmit() {
    console.log('表单提交:', this.heroForm.value);
  }
}
```

### HTTP 客户端

Angular 提供了 `HttpClientModule` 用于处理 HTTP 请求。

#### 配置 HTTP 客户端

```typescript
// app.module.ts
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    HttpClientModule
  ]
})
export class AppModule { }
```

#### 使用 HTTP 客户端

```typescript
// hero.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class HeroService {
  private apiUrl = 'https://jsonplaceholder.typicode.com/users';
  
  constructor(private http: HttpClient) {}
  
  getHeroes(): Observable<any[]> {
    return this.http.get<any[]>(this.apiUrl);
  }
  
  getHero(id: number): Observable<any> {
    return this.http.get<any>(`${this.apiUrl}/${id}`);
  }
  
  addHero(hero: any): Observable<any> {
    return this.http.post<any>(this.apiUrl, hero);
  }
  
  updateHero(hero: any): Observable<any> {
    return this.http.put<any>(`${this.apiUrl}/${hero.id}`, hero);
  }
  
  deleteHero(id: number): Observable<any> {
    return this.http.delete<any>(`${this.apiUrl}/${id}`);
  }
}
```

## Angular 生命周期

Angular 组件从创建到销毁的过程中会触发一系列生命周期钩子函数。

### 组件生命周期钩子

1. **ngOnChanges**：当输入属性变化时调用
2. **ngOnInit**：组件初始化完成后调用
3. **ngDoCheck**：自定义变更检测
4. **ngAfterContentInit**：内容投影完成后调用
5. **ngAfterContentChecked**：内容投影变更检测完成后调用
6. **ngAfterViewInit**：视图初始化完成后调用
7. **ngAfterViewChecked**：视图变更检测完成后调用
8. **ngOnDestroy**：组件销毁前调用

### 生命周期示例

```typescript
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-lifecycle-demo',
  templateUrl: './lifecycle-demo.component.html'
})
export class LifecycleDemoComponent implements OnInit, OnDestroy {
  constructor() {
    console.log('Constructor called');
  }
  
  ngOnChanges(changes: any) {
    console.log('ngOnChanges called', changes);
  }
  
  ngOnInit() {
    console.log('ngOnInit called');
    // 初始化逻辑，如数据获取
  }
  
  ngOnDestroy() {
    console.log('ngOnDestroy called');
    // 清理逻辑，如取消订阅
  }
}
```

## Angular 状态管理

Angular 应用的状态管理可以通过以下方式实现：

1. **组件状态**：组件内部管理的状态
2. **服务状态**：服务中管理的共享状态
3. **NgRx**：基于 Redux 模式的状态管理库

### NgRx 状态管理

```typescript
// hero.model.ts
export interface Hero {
  id: number;
  name: string;
  power: string;
}

// hero.actions.ts
import { createAction, props } from '@ngrx/store';
import { Hero } from './hero.model';

export const loadHeroes = createAction('[Hero] Load Heroes');
export const loadHeroesSuccess = createAction('[Hero] Load Heroes Success', props<{ heroes: Hero[] }>());
export const loadHeroesFailure = createAction('[Hero] Load Heroes Failure', props<{ error: any }>());
```

```typescript
// hero.reducer.ts
import { createReducer, on } from '@ngrx/store';
import { loadHeroes, loadHeroesSuccess, loadHeroesFailure } from './hero.actions';
import { Hero } from './hero.model';

export interface HeroState {
  heroes: Hero[];
  loading: boolean;
  error: any;
}

export const initialState: HeroState = {
  heroes: [],
  loading: false,
  error: null
};

export const heroReducer = createReducer(
  initialState,
  on(loadHeroes, state => ({ ...state, loading: true })),
  on(loadHeroesSuccess, (state, { heroes }) => ({ ...state, heroes, loading: false })),
  on(loadHeroesFailure, (state, { error }) => ({ ...state, error, loading: false }))
);
```

```typescript
// hero.effects.ts
import { Injectable } from '@angular/core';
import { Actions, createEffect, ofType } from '@ngrx/effects';
import { mergeMap, map, catchError } from 'rxjs/operators';
import { of } from 'rxjs';
import { HeroService } from './hero.service';
import { loadHeroes, loadHeroesSuccess, loadHeroesFailure } from './hero.actions';

@Injectable()
export class HeroEffects {
  loadHeroes$ = createEffect(() => {
    return this.actions$.pipe(
      ofType(loadHeroes),
      mergeMap(() => this.heroService.getHeroes().pipe(
        map(heroes => loadHeroesSuccess({ heroes })),
        catchError(error => of(loadHeroesFailure({ error })))
      ))
    );
  });
  
  constructor(
    private actions$: Actions,
    private heroService: HeroService
  ) {}
}
```

## Angular 动画

Angular 提供了强大的动画系统，用于创建复杂的动画效果。

```typescript
// app.module.ts
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

@NgModule({
  imports: [
    BrowserAnimationsModule
  ]
})
export class AppModule { }
```

```typescript
// hero.component.ts
import { Component } from '@angular/core';
import { trigger, transition, style, animate } from '@angular/animations';

@Component({
  selector: 'app-hero',
  templateUrl: './hero.component.html',
  animations: [
    trigger('fadeInOut', [
      transition(':enter', [
        style({ opacity: 0 }),
        animate('0.5s', style({ opacity: 1 }))
      ]),
      transition(':leave', [
        animate('0.5s', style({ opacity: 0 }))
      ])
    ])
  ]
})
export class HeroComponent {
  showHero = true;
  
  toggleHero() {
    this.showHero = !this.showHero;
  }
}
```

```html
<!-- hero.component.html -->
<div [@fadeInOut] *ngIf="showHero">
  <h2>英雄信息</h2>
  <p>姓名：Superman</p>
  <p>超能力：飞行、力量、速度</p>
</div>

<button (click)="toggleHero()">切换显示</button>
```

## Angular 测试

Angular 提供了完整的测试工具链，包括单元测试和 E2E 测试。

### 单元测试

```typescript
// hero.component.spec.ts
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { HeroComponent } from './hero.component';
import { HeroService } from '../hero.service';
import { of } from 'rxjs';

describe('HeroComponent', () => {
  let component: HeroComponent;
  let fixture: ComponentFixture<HeroComponent>;
  let mockHeroService: jasmine.SpyObj<HeroService>;
  
  beforeEach(async () => {
    mockHeroService = jasmine.createSpyObj(['getHeroes']);
    mockHeroService.getHeroes.and.returnValue(of([]));
    
    await TestBed.configureTestingModule({
      declarations: [HeroComponent],
      providers: [{ provide: HeroService, useValue: mockHeroService }]
    }).compileComponents();
    
    fixture = TestBed.createComponent(HeroComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });
  
  it('should create', () => {
    expect(component).toBeTruthy();
  });
  
  it('should call getHeroes on init', () => {
    expect(mockHeroService.getHeroes).toHaveBeenCalled();
  });
});
```

### E2E 测试

```typescript
// hero.e2e-spec.ts
import { browser, by, element } from 'protractor';

describe('Hero App', () => {
  beforeEach(() => {
    browser.get('/heroes');
  });
  
  it('should display hero list', () => {
    expect(element.all(by.css('app-hero')).count()).toBeGreaterThan(0);
  });
  
  it('should navigate to hero detail', () => {
    element(by.css('app-hero:first-child a')).click();
    expect(browser.getCurrentUrl()).toContain('/heroes/');
  });
});
```

## Angular 生态

1. **Angular Material**：官方 UI 组件库
2. **NgRx**：状态管理库
3. **Angular CLI**：命令行工具
4. **Protractor**：E2E 测试框架
5. **Jasmine**：单元测试框架
6. **Karma**：测试运行器
7. **Schematics**：代码生成工具

## Angular 最佳实践

1. **组件设计**：
   - 保持组件小而专注
   - 遵循单一职责原则
   - 使用 OnPush 变更检测策略提高性能
   - 合理使用内容投影

2. **模块设计**：
   - 使用特性模块组织代码
   - 实现懒加载优化性能
   - 合理划分模块边界

3. **服务设计**：
   - 使用 @Injectable(providedIn: 'root') 注册服务
   - 服务应该专注于单一功能
   - 避免在服务中存储状态（除非必要）

4. **性能优化**：
   - 使用 OnPush 变更检测
   - 实现虚拟滚动处理大量数据
   - 合理使用 ngFor 中的 trackBy
   - 避免在模板中使用复杂表达式

5. **代码风格**：
   - 遵循 Angular 官方风格指南
   - 使用 TypeScript 严格模式
   - 编写清晰的组件文档
   - 使用一致的命名约定

6. **测试**：
   - 编写单元测试覆盖核心功能
   - 使用 E2E 测试验证关键用户流程
   - 测试组件的输入输出
   - 测试服务的业务逻辑

## 参考资源

- [Angular 官方文档](https://angular.io/docs)
- [Angular CLI 文档](https://angular.io/cli)
- [NgRx 官方文档](https://ngrx.io/docs)
- [Angular Material 文档](https://material.angular.io/)
- [RxJS 文档](https://rxjs.dev/)
