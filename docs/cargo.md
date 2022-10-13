# cargo


使用**cargo**类似于**Python**的**anaconda**，以及**JavaScript**的**npm**


## 查看版本


只要安装完rust，就会顺便安装完cargo


可以用`cargo --version`命令看一下版本


```shell
> cargo --version
cargo 1.64.0 (387270bc7 2022-09-16)
```


## 更换源


就好比**conda**和**npm**换国内源一样，**cargo**也可以换源，达到比较快的下载速度


*windows*一般在用户目录有个`cargo`


> 一般电脑目录为`C:\Users\Administrator\.cargo`


目录下创建一个`config`文件，写入下面内容


```
[source.crates-io]
replace-with = 'tuna'

[source.tuna]
registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"
```


## 创建项目


使用`cargo`的`new`命令可以创建一个新的的项目


比如创建一个叫`hello_cargo`的项目


```shell
> cargo new hello_cargo
Created binary (application) `hello_cargo` package
> cd hello_cargo
hello_cargo>ls
    目录: D:\project\hello_cargo


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        2022/10/13     16:02                src
-a----        2022/10/13     16:02              8 .gitignore
-a----        2022/10/13     16:02            180 Cargo.toml
```


新建的项目有一个`src`目录，一个`Carfo.toml`文件，以及用于忽略git提交的配置文件`.gitignore`


`src`目录有一个`main.rs`文件，内容为


```rust
fn main() {
    println!("Hello, world!");
}
```


> toml文件是cargo的配置文件，格式可以看 https://toml.io/


使用`build`命令，可以编译项目


```shell
> cargo build
   Compiling hello_cargo v0.1.0 (D:\project\hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.40s
```


这时候会生成一个`target`目录，里面有一个`debug`目录，里面有个`hello_cargo.exe`文件


> 如果是**linux**系统，文件是`hello_cargo`，没有`exe`后缀


执行之后可以得到输出


```shell
> .\target\debug\hello_cargo.exe
Hello, world!
```


使用`run`命令，可以直接执行结果


```shell
> cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
     Running `target\debug\hello_cargo.exe`
Hello, world!
```


使用`clean`命令，可以清空`target`的临时信息


> 清空项目，并不会有输出


```shell
> cargo clean
```


实际上使用`run`命令，如果没有编译的话，会自动执行`build`


```shell
> cargo run
   Compiling hello_cargo v0.1.0 (D:\thales\casia\hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.38s
     Running `target\debug\hello_cargo.exe`
Hello, world!
```


使用`check`命令可以快速检测代码（不编译）


比如我故意写错一个关键字，把`pintln`错写成`println`


```rust
fn main() {
    println!("Hello, world!");
}
```

执行之后会得到错误报告


```shell
> cargo check
    Checking hello_cargo v0.1.0 (D:\project\hello_cargo)
error: cannot find macro `pintln` in this scope
   --> src\main.rs:2:5
    |
2   |     pintln!("Hello, world!");
    |     ^^^^^^ help: a macro with a similar name exists: `println`
    |
   ::: C:\Users\Administrator\.rustup\toolchains\stable-x86_64-pc-windows-msvc\lib/rustlib/src/rust\library\std\src\macros.rs:101:1
    |
101 | macro_rules! println {
    | -------------------- similarly named macro `println` defined here

error: could not compile `hello_cargo` due to previous error
```


可以看到，现在的报错信息非常智能，不止告诉你不存在`pintln`，还告诉你，是不是想写`println`


## 发行版


项目发行时，要删除各种**debug**信息，并且做一定优化，最终版本会比测试版小，并且不会暴露调试信息


`build`命令，增加`release`参数，就可以生成发行版


```shell
> cargo build --release
   Compiling hello_cargo v0.1.0 (D:\project\hello_cargo)
    Finished release [optimized] target(s) in 0.33s
```