# TypeScript 基础概念

## 1. 什么是 TypeScript

TypeScript 是 JavaScript 的超集，它添加了静态类型定义和其他特性，最终会被编译成纯 JavaScript 代码。TypeScript 由 Microsoft 开发和维护，旨在提高大型应用程序的可维护性和开发效率。

### 1.1 TypeScript 的优势

- **静态类型检查**：在编译阶段就能发现类型错误，减少运行时错误
- **更好的 IDE 支持**：提供智能提示、代码补全和重构功能
- **清晰的代码结构**：类型定义使代码更具可读性和自文档性
- **渐进式采用**：可以逐步将 JavaScript 项目迁移到 TypeScript
- **支持最新 JavaScript 特性**：TypeScript 支持 ES2015+ 的所有特性

### 1.2 TypeScript 与 JavaScript 的关系

```
TypeScript = JavaScript + 类型系统 + 其他特性
```

## 2. 基础语法

### 2.1 类型注解

TypeScript 使用冒号 `:` 来指定变量、函数参数和返回值的类型：

```typescript
// 变量类型注解
let message: string = "Hello, TypeScript";
let count: number = 42;
let isActive: boolean = true;

// 函数参数和返回值类型注解
function greet(name: string): string {
  return `Hello, ${name}!`;
}
```

### 2.2 基本类型

TypeScript 提供了以下基本类型：

| 类型 | 描述 | 示例 |
|------|------|------|
| `number` | 数值类型 | `100`, `3.14`, `NaN` |
| `string` | 字符串类型 | `"hello"`, `'world'`, `` `template` `` |
| `boolean` | 布尔类型 | `true`, `false` |
| `null` | 空值类型 | `null` |
| `undefined` | 未定义类型 | `undefined` |
| `symbol` | 符号类型 | `Symbol("key")` |
| `bigint` | 大整数类型 | `100n` |

### 2.3 数组类型

```typescript
// 方式一：类型 + 方括号
let numbers: number[] = [1, 2, 3, 4, 5];

// 方式二：泛型数组
let strings: Array<string> = ["a", "b", "c"];
```

### 2.4 元组类型

元组用于表示固定长度和固定类型顺序的数组：

```typescript
let person: [string, number] = ["Alice", 30];
let coordinates: [number, number, number] = [10, 20, 30];
```

### 2.5 枚举类型

枚举用于定义一组命名常量：

```typescript
// 数字枚举（默认从 0 开始）
enum Direction {
  Up,
  Down,
  Left,
  Right
}

// 字符串枚举
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE"
}

// 使用枚举
let direction: Direction = Direction.Up;
let color: Color = Color.Red;
```

### 2.6 任意类型

使用 `any` 类型可以表示任意类型的值：

```typescript
let anyValue: any = 42;
anyValue = "Hello";
anyValue = true;
```

### 2.7 未知类型

`unknown` 类型是 TypeScript 3.0 引入的安全替代 `any` 的类型：

```typescript
let unknownValue: unknown = 42;
unknownValue = "Hello";

// 需要类型断言才能使用
let str: string = unknownValue as string;
```

### 2.8 空类型

`void` 用于表示函数没有返回值：

```typescript
function logMessage(message: string): void {
  console.log(message);
  // 没有 return 语句或 return undefined
}
```

### 2.9 从不类型

`never` 用于表示那些永不存在的值的类型：

```typescript
// 抛出异常的函数
function throwError(message: string): never {
  throw new Error(message);
}

// 无限循环的函数
function infiniteLoop(): never {
  while (true) {
    // 无限循环
  }
}
```

## 3. 接口

接口用于定义对象的结构和类型：

```typescript
interface Person {
  name: string;
  age: number;
  email?: string; // 可选属性
  readonly id: number; // 只读属性
  greet(): string; // 方法
}

// 实现接口
const alice: Person = {
  name: "Alice",
  age: 30,
  id: 1,
  greet() {
    return `Hello, my name is ${this.name}`;
  }
};
```

## 4. 类型别名

类型别名用于给类型起一个新的名字：

```typescript
type Point = { x: number; y: number };
type Coordinates = [number, number];
type Status = "active" | "inactive" | "pending"; // 联合类型

type User = {
  id: number;
  name: string;
  email: string;
  status: Status;
};
```

## 5. 泛型

泛型允许在定义函数、接口或类时不指定具体类型，而是在使用时指定：

### 5.1 泛型函数

```typescript
function identity<T>(value: T): T {
  return value;
}

// 使用泛型函数
let result1 = identity<string>("Hello");
let result2 = identity<number>(42);
let result3 = identity(true); // 类型推断
```

### 5.2 泛型接口

```typescript
interface Container<T> {
  value: T;
  getValue(): T;
}

const stringContainer: Container<string> = {
  value: "Hello",
  getValue() {
    return this.value;
  }
};
```

### 5.3 泛型类

```typescript
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }
}

// 使用泛型类
const numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push(2);
```

## 6. 类与继承

TypeScript 支持面向对象编程，包括类、继承、接口实现等：

```typescript
// 基类
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound(): void {
    console.log("Animal makes sound");
  }
}

// 派生类
class Dog extends Animal {
  private breed: string;

  constructor(name: string, breed: string) {
    super(name);
    this.breed = breed;
  }

  makeSound(): void {
    console.log("Woof! Woof!");
  }

  getBreed(): string {
    return this.breed;
  }
}

// 实现接口
interface Playable {
  play(): void;
}

class Cat extends Animal implements Playable {
  constructor(name: string) {
    super(name);
  }

  makeSound(): void {
    console.log("Meow!");
  }

  play(): void {
    console.log(`${this.name} is playing`);
  }
}
```

## 7. 高级类型

### 7.1 联合类型

联合类型表示一个值可以是多种类型之一：

```typescript
type StringOrNumber = string | number;

function printValue(value: StringOrNumber): void {
  console.log(value);
}

printValue("Hello");
printValue(42);
```

### 7.2 交叉类型

交叉类型将多个类型合并为一个类型：

```typescript
interface A {
  a: string;
}

interface B {
  b: number;
}

type C = A & B;

const c: C = {
  a: "Hello",
  b: 42
};
```

### 7.3 类型守卫

类型守卫用于在运行时检查类型：

```typescript
function isString(value: any): value is string {
  return typeof value === "string";
}

function isNumber(value: any): value is number {
  return typeof value === "number";
}

function processValue(value: string | number): void {
  if (isString(value)) {
    console.log(`String: ${value.toUpperCase()}`);
  } else if (isNumber(value)) {
    console.log(`Number: ${value.toFixed(2)}`);
  }
}
```

### 7.4 索引类型

索引类型允许我们操作对象的属性类型：

```typescript
interface Person {
  name: string;
  age: number;
  email: string;
}

// 获取 Person 所有属性的类型
type PersonKeys = keyof Person; // "name" | "age" | "email"

type PersonValues = Person[keyof Person]; // string | number
```

### 7.5 映射类型

映射类型允许我们基于现有类型创建新类型：

```typescript
interface Person {
  name: string;
  age: number;
  email: string;
}

// 只读映射类型
type ReadonlyPerson = Readonly<Person>;

// 可选映射类型
type PartialPerson = Partial<Person>;

// 选取映射类型
type PickPerson = Pick<Person, "name" | "email">;

// 排除映射类型
type OmitPerson = Omit<Person, "age">;
```

## 8. 装饰器

装饰器是一种特殊类型的声明，可以附加到类声明、方法、属性或参数上。装饰器使用 `@expression` 语法：

```typescript
// 类装饰器
function logClass(target: any) {
  console.log(`Class ${target.name} was decorated`);
}

// 属性装饰器
function logProperty(target: any, propertyKey: string) {
  console.log(`Property ${propertyKey} was decorated`);
}

// 方法装饰器
function logMethod(target: any, methodName: string, descriptor: PropertyDescriptor) {
  console.log(`Method ${methodName} was decorated`);
}

@logClass
class User {
  @logProperty
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  @logMethod
  getName() {
    return this.name;
  }
}
```

## 9. 模块系统

TypeScript 使用 ES 模块系统：

```typescript
// 导出
export interface User {
  id: number;
  name: string;
}

export function createUser(id: number, name: string): User {
  return { id, name };
}

// 导入
import { User, createUser } from "./user";

const user: User = createUser(1, "Alice");
```

## 10. 编译配置

TypeScript 项目通过 `tsconfig.json` 文件进行配置：

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "jsx": "react",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

## 11. 最佳实践

### 11.1 类型使用

- 尽量避免使用 `any` 类型
- 优先使用接口而不是类型别名定义对象结构
- 合理使用泛型提高代码复用性
- 使用类型守卫处理联合类型

### 11.2 代码组织

- 每个文件只包含一个主要类型或类
- 使用模块系统组织代码
- 合理使用命名空间

### 11.3 编译配置

- 使用严格模式 `"strict": true`
- 针对目标环境设置合适的 `target` 和 `lib`
- 配置合适的 `module` 和 `moduleResolution`

### 11.4 性能考虑

- 避免过度使用复杂的泛型和高级类型
- 合理使用类型断言
- 考虑类型检查的性能影响

## 12. 学习资源

- [TypeScript 官方文档](https://www.typescriptlang.org/docs/)
- [TypeScript Handbook (中文)](https://typescript.bootcss.com/)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
- [TypeScript 实战指南](https://ts.xcatliu.com/)

## 13. 工具链

- **编辑器**：VS Code (内置 TypeScript 支持)
- **构建工具**：Webpack, Vite, Rollup
- **包管理器**：npm, Yarn, pnpm
- **测试框架**：Jest, Vitest, Mocha
- **Linting**：ESLint + @typescript-eslint/eslint-plugin

## 14. 常见问题

### 14.1 类型错误

```typescript
// 错误：类型 "string" 不能赋值给类型 "number"
let count: number = "42";

// 错误：对象文字可以只指定已知属性，并且 "extra" 不在类型 "Person" 中
const person: Person = {
  name: "Alice",
  age: 30,
  extra: "value" // 多余属性
};
```

### 14.2 类型断言

```typescript
// 类型断言语法
let str: string = someValue as string;
let str2: string = <string>someValue; // JSX 中不推荐
```

### 14.3 声明文件

对于没有类型定义的第三方库，需要安装声明文件：

```bash
npm install --save-dev @types/node
npm install --save-dev @types/react
npm install --save-dev @types/lodash
```

## 15. 未来发展

TypeScript 持续发展，未来可能会引入更多特性：

- 更强大的类型系统
- 更好的性能
- 更完善的工具链集成
- 更多的生态系统支持

TypeScript 已经成为现代前端开发的重要组成部分，掌握 TypeScript 对于构建大型、可维护的前端应用至关重要。