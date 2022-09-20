# 变量和常量


## 变量的改变


我们首先看一段代码


```rust
fn main() {
  let x = 5;
  println!("The value of x is: {x}");
  x = 6;
  println!("The value of x is: {x}");
}
```


你觉得结果是什么呢？


你一定认为是 ——
```bash
The value of x is: 5
The value of x is: 6
```

可实际上报错了 ——

```bash
error[E0384]: cannot assign twice to immutable variable `x`
 --> src\main.rs:4:5
  |
2 |     let x = 5;
  |         -
  |         |
  |         first assignment to `x`
  |         help: consider making this binding mutable: `mut x`
3 |     println!("The value of x is: {x}");
4 |     x = 6;
  |     ^^^^^ cannot assign twice to immutable variable

For more information about this error, try `rustc --explain E0384`.
error: could not compile `rust-rookie` due to previous error
```


把错误翻译一下
> 不管什么语言，运行出错时候，把错误翻译一下很大概率就能找到解决办法
> 就算英语薄弱，翻译软件也有很多

- cannot assign twice to immutable variable \`x\`
---- 翻译 ----
- 不能对不可改变的变量`x`进行两次赋值

## 可变变量


定义变量时候，加一个`mut`（mutable），变量就可以改变了


```rust
fn main() {
  let mut x = 5;
  println!("The value of x is: {x}");
  x = 6;
  println!("The value of x is: {x}");
}
```


现在是你所预期的 ——
```bash
The value of x is: 5
The value of x is: 6
```


## 常量


几乎大部分语言，定义常量都用的关键字——`const`


```rust
const TWO_HOURS_IN_SECONDS:u32 = 60 * 60 * 2
```


虽然**常量**和没有设置`mut`的**变量**都是不能重复赋值，但是有一定的区别


1. 多次赋值同名变量


```rust
let x = 5;
let x = 6;
```


2. 先定义变量不赋值，后面再赋值


```rust
let x;
x = 5;
```


3. 常量必须指定类型


```rust
const X:u32 = 60;
```


如果不指定类型`u32`会报错


```rust
const X = 60;
```

> Syntax Error: missing type for `const` or `static`