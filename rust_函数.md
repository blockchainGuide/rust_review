# Rust 函数详解

在本文中，我们将详解 Rust 中的函数，包括函数定义、参数、返回值以及作用域。函数是一段可重用的代码块，可以接受输入参数并返回输出。Rust 是一种静态类型语言，这意味着每个函数参数和返回值都有一个明确的类型。本文假设你已经对 Rust 的基本知识有一定了解。


<a name="函数定义"></a>
## 1. 函数定义

在 Rust 中，函数使用 `fn` 关键字定义。函数名应遵循小驼峰命名规则（snake_case），即所有单词小写，单词之间用下划线（_）分隔。以下是一个简单的函数定义示例：

```rust
fn greet() {
    println!("Hello, Rust!");
}

fn main() {
    greet();  // 调用 greet 函数
}
```

<a name="函数参数"></a>
## 2. 函数参数

函数可以接受零个或多个参数。参数是在函数名后的括号内定义的，每个参数由名称和类型组成，参数之间用逗号分隔。以下是一个带参数的函数示例：

```rust
fn greet(name: &str, age: u32) {
    println!("Hello, {}. You are {} years old.", name, age);
}

fn main() {
    let name = "Alice";
    let age = 30;
    greet(name, age);  // 调用 greet 函数，并传入 name 和 age 参数
}
```

注意，函数参数默认是不可变的。如果需要在函数内修改参数，需要使用 `mut` 关键字声明可变参数。

<a name="返回值"></a>
## 3. 返回值

函数可以返回一个值。返回值类型在函数参数后的箭头（`->`）之后定义。函数返回值可以使用 `return` 关键字显式返回，也可以省略 `return` 关键字，将最后一个表达式的值隐式返回。

以下是一个带返回值的函数示例：

```rust
// 使用 return 关键字显式返回
fn add_explicit(a: i32, b: i32) -> i32 {
    return a + b;
}

// 省略 return 关键字，隐式返回
fn add_implicit(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let a = 10;
    let b = 20;
    let sum_explicit = add_explicit(a, b);
    let sum_implicit = add_implicit(a, b);
    println!("sum_explicit = {}, sum_implicit = {}", sum_explicit, sum_implicit);
}
```

<a name="作用域"></a>
## 4. 作用域

作用域是编程语言中一个重要的概念，它定义了变量和函数的可见性和生命周期。在 Rust 中，作用域以块（block）为单位，由一对花括号（`{}`）界定。变量的作用域从声明它的地方开始，直到包含它的块结束。

### 4.1 局部变量与全局变量

变量根据其定义位置可分为局部变量和全局变量。局部变量在函数内定义，只在函数内部可见。全局变量在函数外定义，可以在整个程序中使用。全局变量应谨慎使用，以避免潜在的数据竞争和代码维护问题。

以下是一个局部变量和全局变量的示例：

```rust
const GLOBAL: i32 = 42;  // 全局变量，使用 const 关键字定义

fn print_global() {
    println!("Global variable: {}", GLOBAL);
}

fn main() {
    let local = 10;  // 局部变量
    println!("Local variable: {}", local);
    print_global();
}
```

### 4.2 函数作用域

函数作用域指函数可以访问的范围。在 Rust 中，函数可以访问其参数、局部变量以及在其之前定义的全局变量和其他函数。函数不能访问在其之后定义的全局变量和其他函数，这称为“前向引用”。

以下是一个函数作用域的示例：

```rust
fn function1() {
    println!("This is function1");
    function2();  // 可以调用在 function1 之前定义的 function2
}

fn function2() {
    println!("This is function2");
}

fn main() {
    function1();
}
```

<a name="高阶函数与闭包"></a>
## 5. 高阶函数与闭包

高阶函数是接受其他函数作为参数或将函数作为返回值的函数。Rust 支持高阶函数和闭包（匿名函数）。

### 5.1 高阶函数

以下是一个高阶函数示例，该函数接受一个函数作为参数：

```rust
fn apply(func: fn(i32, i32) -> i32, a: i32, b: i32) -> i32 {
    func(a, b)
}

fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let a = 10;
    let b = 20;
    let result = apply(add, a, b);
    println!("Result: {}", result);
}
```

### 5.2 闭包

闭包是匿名函数，可以捕获其定义环境中的变量。闭包使用 `|` 分隔输入参数和函数体。闭包表达式会自动推导输入参数和返回值的类型，但也可以显式指定。

以下是一个闭包示例：

```rust
fn main() {
    let a = 10;
    let b = 20;
    let add = |x: i32, y: i32| -> i32 { x + y };
    let result = add(a, b);
    println!("Result: {}", result);
}
```

闭包可以捕获其定义环境中的变量，包括通过引用捕获（`&`）、可变引用捕获（`&mut`）和值捕获（`move`）。

以下是一个捕获环境变量的闭包示例：

```rust
fn main() {
    let x = 10;
    let add_x = |y: i32| x + y; // 捕获 x
    let result = add_x(20);
    println!("Result: {}", result);
}
```

<a name="总结"></a>
## 6. 总结

本文详细介绍了 Rust 中函数的定义、参数、返回值以及作用域的理解。我们还讨论了高阶函数和闭包的概念。Rust 是一种功能强大的编程语言，对于系统编程、Web 开发和其他领域有广泛的应用。希望本文能为你学习 Rust 提供一个良好的起点。接下来，你可以尝试学习 Rust 的更高级功能，如结构体、枚举、模式匹配、错误处理、并发等。