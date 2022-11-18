# 数据类型


**rust**定义变量会自动指定类型，你也可以指定类型


类型主要分为以下——
- 整型(integer)
- 浮点数(floating-point number)
- 布尔值(booleans)
- 字符(characters)
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


### 可读性分隔符


为了方便阅读超大的数字，Rust 语言允许使用一个*虚拟的分隔符*也就是*下划线*(`_`)来对数字进行可读性分隔符。


比如为了提高`50000`的可读性，我们可以写成`50_000`。


```rust
let int_with_separator = 100_000;
```


**Rust**语言会在编译时移除数字可读性分隔符`_`



## 浮点型


Rust 与其它语言一样支持32位浮点数(f32)和64位浮点数(f64)。默认情况下赋值有小数点的数字将表示**64位浮点数**，因为现代计算机处理器对两种浮点数计算的速度几乎相同，但64位浮点数精度更高。


```rust
let x = 2.0; // 默认64位浮点数
let y: f32 = 3.0; // 设定为32位浮点数
```


> https://ieeexplore.ieee.org/document/5976968
> 按照** IEEE-754**标准，32位浮点数是单精度，64位浮点数是双精度


### 运算


Rust支持各种基本的数学算法，有加减乘除以及求余


```rust
// 加法
let sum = 5 + 10;

// 减法
let difference = 95.5 - 4.3;

// 乘法
let product = 4 * 30;

// 除法
let quotient = 56.7 / 32.2;
let floored = 2 / 3; // 结果为0，整型除法，最后结果位整数部分

// 求余
let remainder = 43 % 5; // 结果为3，按照计算，商为8，余3
```


### 可读性分隔符


浮点数一样可以使用`_`来增加可读性


```rust
let float_with_separator = 11_000.789_001;
```


## 布尔值


跟其他计算机语言一样，**Rust**的**布尔值**有两种值：`true`和`false`。布尔值占用一个字节，类型用`bool`表示


```rust
let t = true;
let f: bool = false;
```


## 字符


使用单引号或者双引号，可以设置字符。字符占4个字节，它比**ASCII**指代的内容更多，有且不限于中文、日文、韩文等各国语言字符，甚至还有表情以及没有宽度的空格


```rust
let c = 'z';
let z: char = 'ℤ';
let heart_eyed_cat = '😻';
```


字符使用`unicode`，范围从`U+0000`到`U+D7FF`和`U+E000`到`U+10FFFF`


> 实际上`字符`并不是在`unicode`的一个真正的概念，后面还会说


## 混合


### 元组


元组(Tuple)用一对` ( ) `包括的一组数据，可以包含不同种类的数据


```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
```


用匹配的方式可以从**元组**中获取各个参数


```rust
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
println!("The value of y is: {y}"); // The value of y is: 6.4
```


元组使用点`.`按照顺序来指向元祖中的值


```rust
let x: (i32, f64, u8) = (500, 6.4, 1);
let five_hundred = x.0; // 500
let six_point_four = x.1; // 6.4
let one = x.2; // 1
```


### 数组


数组(Array)是用一对` [ ] `(中括号)包含一组数据，但是跟元组不一样，数据类型必须一致


```rust
let a = [1, 2, 3, 4, 5];
let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
```


你可以在中括号中设置类型，并且在` ; `(分号)后面设定数组长度


```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```


也可以设置一个初始值的数组，比如设置`5`个`3`组成的数组


```rust
let a = [3; 5]; // [ 3, 3, 3, 3, 3 ]
```


获取入组中的元素，需要用中括号按照元素的索引(index)取数据


```rust
let a = [1, 2, 3, 4, 5];

let first = a[0]; // 1
let second = a[1]; // 2
```

注意，索引必须小于数组的尺寸，比如数组有5个元素，那么索引只能是0~4，如果超过限定，比如5，就是经典的错误*下标越界*


```rust
let a = [1, 2, 3, 4, 5];

let v = a[5]; // index out of bounds: the length is 5 but the index is 5
```

