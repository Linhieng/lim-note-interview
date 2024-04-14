# 学习 rust

由于是学习，所以格式相关内容就按着喜欢的样式来！

## 语言核心概念

    变量
        变量绑定、所有权
        变量可变性、常量
        变量遮蔽（shadowing）
        变量解构
    类型
        有符号整数、无符号整数、有理数、复数
        字符串字面量、字符串切片
        布尔 true false
        字符（Unicode 字符）
        单元类型 ()
    数值类型
        运算符重载
        整形溢出：
            wrapping_
            checked_
            overflowing_
            saturating_
        浮点数陷阱。0.1 + 0.2、f32 和 f64
        NaN。不可比较，不可运算。
        数学运算 + - * / %
        位运算 & | ! ^ << >> （有无符号根据类型判断）
        序列 range


## cargo 和命令行

- 可参考资料

    - [设置 - Cargo 手册 中文版 (rustwiki.org)]
    - [Cargo 使用指南 - Rust语言圣经(Rust Course)]

cargo 包管理器

    总结：
```sh
        cargo new <project>
        cargo run [--release]
        cargo build [--release]
        cargo check
        cargo add <package>
```

    详细：

```sh
        cargo new world_hello
        # 创建新项目

        cargo run
        # 运行项目
        # 等同于
            cargo build # 编译
            ./target/debug/world_hello # 运行
        # 添加 --release 提高性能（优化）
        cargo run --release
            cargo build --release
            ./target/release/world_hello #  项目名为 world_hello

        cargo check
        # 检查代码能否编译通过（快速）

```
    Cargo.toml 和 Cargo.lock

        Cargo.toml 是 cargo 特有的项目数据描述文件
        Cargo.lock 文件是 cargo 工具根据同一项目的 toml 文件生成的项目依赖详细清单
        TOML: Tom's Obvious Minimal Language

rustc

```sh
        rustc
        rustc --version
```

## 读懂代码

代码片段：

```rs
        fn main() {
            let x =define_x();
            let y = define_y();
            println!("{}, world", x);
            println!("{}, world", y);
            let mut z = 1;
            println!("{}", z);
            z = 2;
            let z = z;
            println!("{}", z);
            test_unused_variables();

            let (mut i, j) = (1, 2);
            assert_eq!(i, 1);
            i = 2;
            assert_eq!(i, 2);
            assert_eq!(j, 2);
        }
        fn define_x() -> String {
            let x = "hello".to_string();
            return x
        }
        fn define_y() -> &'static str {
            let x = "hello";
            x
        }
        #[allow(unused_variables)]
        fn test_unused_variables() {
            let x = 123;
        }
```

读懂代码：

```rs
        let _something = "42".parse::<i32>().expect("Not a number!");
```

读懂代码

```rs
        fn main() {
            assert_eq!(9, u8::MAX.wrapping_add(10));
            assert_eq!(None, u8::MAX.checked_add(10));
            assert_eq!((9, true), u8::MAX.overflowing_add(10));
            assert_eq!(255, u8::MAX.saturating_add(10));
            // println!("{}", 10_u8.checked_add(10));
            println!("{:?}", 10_u8.checked_add(10)); // Option<u8>
        }
```

读懂代码

```rs
        fn main() {
            let abc: (f32, f32, f32) = (0.1, 0.2, 0.3);
            let xyz: (f64, f64, f64) = (0.1, 0.2, 0.3);
            println!("abc (f32)");
            println!("   0.1 + 0.2: {:x}", (abc.0 + abc.1).to_bits());
            println!("         0.3: {:x}", (abc.2).to_bits());
            println!();
            println!("xyz (f64)");
            println!("   0.1 + 0.2: {:x}", (xyz.0 + xyz.1).to_bits());
            println!("         0.3: {:x}", (xyz.2).to_bits());
            println!();
            assert!(abc.0 + abc.1 == abc.2); // 不报错
            assert!(xyz.0 + xyz.1 == xyz.2); // 报错
        }
```

看懂代码

```rs
        fn main() {
            let x = (-1.0_f32).sqrt();
            assert_ne!(x, x); // NaN != NaN
            if x.is_nan() {
                println!("未定义的数学行为");
            }
        }
```

    看懂代码
```rs
        fn main() {
            // 编译器会进行自动推导，给予twenty i32的类型
            let twenty = 20;
            // 类型标注
            let twenty_one: i32 = 21;
            // 通过类型后缀的方式进行类型标注：22是i32类型
            let twenty_two = 22i32;
            // 只有同样类型，才能运算
            let addition = twenty + twenty_one + twenty_two;
            println!(
                "{} + {} + {} = {}",
                twenty, twenty_one, twenty_two, addition
            );
            // 对于较长的数字，可以用_进行分割，提升可读性
            let one_million: i64 = 1_000_000;
            println!("{}", one_million.pow(2));
            // 定义一个f32数组，其中42.0会自动被推导为f32类型
            let forty_twos = [42.0, 42f32, 42.0_f32];
            // 打印数组中第一个值，并控制小数位为2位
            println!("{:.2}", forty_twos[0]);
        }
```

看懂代码

```rs
        fn main() {
            for i in 1..5 {
                print!("{} ", i);
            }
            println!(""); // 1 2 3 4
            for i in 1..=5 {
                print!("{} ", i);
            }
            println!(""); // 1 2 3 4 5
            for c in 'a'..'f' {
                print!("{} ", c);
            }
            println!(""); // a b c d e
            for c in 'a'..='f' {
                print!("{} ", c);
            }
            println!(""); // a b c d e f
        }
```





[设置 - Cargo 手册 中文版 (rustwiki.org)]: https://rustwiki.org/zh-CN/cargo/reference/config.html
[Cargo 使用指南 - Rust语言圣经(Rust Course)]: https://course.rs/cargo/intro.html
