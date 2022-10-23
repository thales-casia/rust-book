# 数据类型


**rust**定义变量会自动指定类型，你也可以指定类型


类型主要分为以下——
- 整型(integer)
- 浮点数(floating-point number)
- 布尔值(booleans)
- 字符串(characters)
- 混合(compound)


## 整型


整数类型，没有分数部分。整型分为有符号(Signed)和无符号两种(Unsigned)

长度 | 有符号 | 无符号
---|---|---
8-bit | i8 | u8
16-bit | i16 | u16
32-bit | i32 | u32
64-bit | i64 | u64
128-bit | i128 | u128
arch | isize | usize


总得来说，就是`i`或者`u`加上位数就是整型的类型


### 取值范围


每一个有符号数的取值范围————

-(2<sup>n-1</sup>) 到 2<sup>n-1</sup> - 1 之间


无符号数的取值范围————


0 到 2<sup>n</sup> - 1 之间


比如`i8`，范围就是——


-(2<sup>8-1</sup>) < i8 < 2<sup>8-1</sup> - 1


-2<sup>7</sup> < i8 < 2<sup>7</sup> - 1


-128 < i8 < 127


也就是说`i8`的的取值范围为 *[-128, 127]*


如果给一个`i8`类型的变量赋值了在这个取值范围之外的数字


```rust
let n:i8 = 128;
```


就会报错


```
the literal `128` does not fit into the type `i8` whose range is `-128..=127`
```


注意，无符号的取值范围的幂没有`-1`就是`n`，所以`u8`的取值范围是


0 < u8 < 2<sup>n</sup> - 1


0 < u8 < 2<sup>8</sup> - 1


0 < u8 < 255


所以无符号的`u8`是 *[0, 255]*，比`i8`的 *128* 要大，其实等于取值范围整体在数轴右移到了 *0*


> 各种可以设置整型的有符号无符号的语言基本都是这种设置，比如**C/C++**、**java**、**SQL**


### 进制(Number literals)


进制 | 实例 | 备注
---|---|---
Decimal |	98_222 | 十进制
Hex | 0xff | 十六进制
Octal | 0o77 | 八进制
Binary | 0b1111_0000 | 二进制
Byte | b'A' | 字节(只能表示`u8`)


下面的`n`以16进制赋值`0xff`，输出为`255`


```rust
let n:u8 = 0xff;
println!("{}", n);
```


这里解释一下`Byte`，其实就是可以得到键盘上的`ascii`值


下面的赋值，可以看到大`A`的值是`65`，小`a`的值是`97`，叹号`!`的值是33


```rust
let A:u8 = b'a'; // 65
let a:u8 = b'a'; // 97
let exclamation:u8 = b'!'; // 33
```