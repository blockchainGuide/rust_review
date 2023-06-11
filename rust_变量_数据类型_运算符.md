# Rust 语言基础教程

在本文中，我们将详解 Rust 语言的基础知识点，包括变量、数据类型、运算符等。Rust 是一种系统编程语言，注重安全、并发和内存效率。Rust 的设计目标是提供高级抽象而不损失底层控制。本文假设你已经对编程有一定了解，但不需要 Rust 语言的经验。

<a name="rust-简介"></a>
## 1. Rust 简介

Rust 是一种多范式、编译型的系统编程语言，它的设计目标是提供内存安全、并发和性能。Rust 采用了一种独特的所有权系统，它可以在编译时防止数据竞争和空悬指针等问题，从而提高了程序的安全性。

<a name="安装-rust"></a>
## 2. 安装 Rust

在开始之前，你需要安装 Rust。访问 [官方安装页面](https://www.rust-lang.org/tools/install)，根据你的操作系统进行安装。安装完成后，打开终端或命令提示符，运行 `rustc --version`，如果显示 Rust 的版本信息，说明安装成功。

<a name="hello-world"></a>
## 3. Hello, World!

创建一个新的文件夹，然后在文件夹内创建一个名为 `main.rs` 的文件。将以下内容写入 `main.rs`：

```rust
fn main() {
    println!("Hello, World!");
}
```

在终端中，将当前目录切换到包含 `main.rs` 的文件夹，然后运行 `rustc main.rs` 编译程序。编译完成后，运行生成的可执行文件（在 Windows 上为 `main.exe`，在其他系统上为 `./main`）。你应该看到输出 "Hello, World!"。

恭喜！你已经成功编写并运行了第一个 Rust 程序。

<a name="变量与绑定"></a>
## 4. 变量与绑定

在 Rust 中，变量默认是不可变的，这有助于保持代码的安全性和易理解性。要声明一个变量，使用 `let` 关键字。以下是一些变量声明的示例：

```rust
fn main() {
    let x = 5;
    let y: i32 = 10;
    let z: f64 = 3.14;
    println!("x = {}, y = {}, z = {}", x, y, z);
}
```

要声明一个可变变量，使用 `mut` 关键字：

```rust
fn main() {
    let mut a = 42;
    println!("Before: {}", a);
    a = 13;
    println!("After: {}", a);
}
```

请注意，尝试修改不可变变量将导致编译错误。

<a name="数据类型"></a>
## 5. 数据类型

Rust 是一种静态类型语言，这意味着每个变量都有一个明确的类型。Rust 的数据类型分为两类：标量（Scalar）和复合（Compound）。

### 标量类型

标量类型包括整数、浮点数、布尔值和字符。它们分别表示单个值。

<a name="整数类型"></a>
#### 5.1 整数类型

整数类型包括有符号整数（i8、i16、i32、i64、i128）和无符号整数（u8、u16、u32、u64、u128）。数字表示位数。例如，i32 表示 32 位有符号整数。默认情况下，整数类型是 `i32`。

```rust
let a: i8 = -128;
let b: u8 = 255;
```

<a name="浮点数类型"></a>
#### 5.2 浮点数类型

浮点数类型包括 `f32` 和 `f64`，分别表示 32 位和 64 位浮点数。默认情况下，浮点数类型是 `f64`。

```rust
let x: f32 = 3.14;
let y: f64 = 2.71828;
```

<a name="布尔类型"></a>
#### 5.3 布尔类型

布尔类型有两个值：`true` 和 `false`。它在逻辑表达式和条件语句中使用。

```rust
let is_true: bool = true;
let is_false: bool = false;
```

<a name="字符类型"></a>
#### 5.4 字符类型

字符类型表示单个 Unicode 字符，使用单引号（`'`）表示。字符类型是 `char`。

```rust
let c: char = 'A';
let emoji: char = '😃';
```

### 复合类型

复合类型包括元组（Tuple）和数组（Array）。它们用于将多个值组合成一个复合值。

<a name="元组类型"></a>
#### 5.5 元组类型

元组是一种固定长度的、有序的值列表。元组中的值可以是不同类型。要声明一个元组，使用圆括号将值括起来。

```rust
let tuple: (i32, f64, bool) = (42, 3.14, true);
```

要访问元组中的值，使用句点（`.`）后跟索引。

```rust
let first = tuple.0;
let second = tuple.1;
let third = tuple.2;
println!("first = {}, second = {}, third = {}", first, second, third);
```

<a name="数组与切片类型"></a>
#### 5.6 数组与切片类型

数组是一种固定长度的、有序的相同类型值列表。要声明一个数组，使用方括号将值括起来。

```rust
let array: [i32; 5] = [1, 2, 3, 4, 5];
```

要访问数组中的值，使用方括号内的索引。

```rust
let first = array[0];
let second = array[1];
println!("first = {}, second = {}", first, second);
```

切片是数组的引用，它不包含所有权。要创建一个切片，使用数组名后跟方括号内的范围。

```rust
let slice: &[i32] = &array[1..4];
```

<a name="运算符"></a>
## 6. 运算符

Rust 支持多种运算符，用于执行算术、比较、逻辑、位操作等。

<a name="算术运算符"></a>
### 6.1 算术运算符

算术运算符包括加（`+`）、减（`-`）、乘（`*`）、除（`/`）和取模（`%`）。

```rust
let a = 10;
let b = 3;

let add = a + b;
let sub = a - b;
let mul = a * b;
let div = a / b;
let rem = a % b;

println!("add = {}, sub = {}, mul = {}, div = {}, rem = {}", add, sub, mul, div, rem);
```

<a name="关系运算符"></a>
### 6.2 关系运算符

关系运算符包括等于（`==`）、不等于（`!=`）、小于（`<`）、大于（`>`）、小于等于（`<=`）和大于等于（`>=`）。

```rust
let x = 10;
let y = 20;

let eq = x == y;
let ne = x != y;
let lt = x < y;
let gt = x > y;
let le = x <= y;
let ge = x >= y;

println!("eq = {}, ne = {}, lt = {}, gt = {}, le = {}, ge = {}", eq, ne, lt, gt, le, ge);
```

<a name="逻辑运算符"></a>
### 6.3 逻辑运算符

逻辑运算符包括逻辑与（`&&`）、逻辑或（`||`）和逻辑非（`!`）。

```rust
let a = true;
let b = false;

let and = a && b;
let or = a || b;
let not = !a;

println!("and = {}, or = {}, not = {}", and, or, not);
```

<a name="位运算符"></a>
### 6.4 位运算符

位运算符包括按位与（`&`）、按位或（`|`）、按位异或（`^`）、按位非（`!`）、左移（`<<`）和右移（`>>`）。

```rust
let a = 0b1100;
let b = 0b1010;

let bit_and = a & b;
let bit_or = a | b;
let bit_xor = a ^ b;
let bit_not = !a;
let left_shift = a << 2;
let right_shift = a >> 2;

println!("bit_and = {:b}, bit_or = {:b}, bit_xor = {:b}, bit_not = {:b}, left_shift = {:b}, right_shift = {:b}",
         bit_and, bit_or, bit_xor, bit_not, left_shift, right_shift);
```

<a name="赋值运算符"></a>
### 6.5 赋值运算符

赋值运算符包括简单赋值（`=`）和复合赋值（`+=`、`-=`、`*=`、`/=`、`%=`、`&=`、`|=`、`^=`、`<<=`、`>>=`）。

```rust
let mut a = 10;

a += 5;
a -= 3;
a *= 2;
a /= 4;
a %= 3;

println!("a = {}", a);
```

<a name="其他运算符"></a>
### 6.6 其他运算符

Rust 还有一些其他运算符，如范围运算符（`..`、`..=`）和条件运算符（`?`）等。这些运算符在实际编程中使用较少，但在需要时会非常有用。

<a name="总结"></a>
## 7. 总结

本文详细介绍了 Rust 语言的基础知识点，包括变量、数据类型和运算符。Rust 是一种强大、安全和高效的编程语言，对于系统编程、Web 开发和其他领域有广泛的应用。希望本文能为你学习 Rust 提供一个良好的起点。接下来，你可以尝试学习 Rust 的更高级功能，如条件语句、循环、函数、结构体、枚举、模式匹配、错误处理、并发等。