# CMSC131 Notes for Exam 1

> Exam 1: Oct 7，课堂 50 分钟，closed-book，铅笔。题型：short answer / code analysis（找错、写输出）/ code writing（写 static method）。
>
> **不考**：StringBuffer、Pseudocode、Constructors、Instance variables、Non-static methods、`toString`、`equals` 的定义、Heap/Stack、Memory maps。

## 1. Computer Organization & Java 基础

* 1 byte = 8 bits；n 个 bit 有 `2ⁿ` 种 pattern；代码和数据都是 bit pattern（如 ASCII `'A'` = `01000001`）
* **OS**：系统软件，管理资源（process、memory、I/O、security）；**Application**：用户直接用的程序
* **Compiler**：运行前把 source 翻译成 machine code（快）；**Interpreter**：逐行执行（慢）
* Java is **portable**：`.java` → compiler → bytecode (`.class`) → 各机器上的 **JVM** 解释执行
* **Object-oriented** 术语：Object（程序操作的实体）、Class（object 的蓝图）、Method（procedure）
* **Main method**：程序执行的起点，`public static void main(String[] args)`
* Statements：Declaration、Assignment、Method invocation、Control flow、Expression
* `=` 赋值，`==` 比较
* 注释：`// 单行`　`/* 多行 */`
* `println` 打印后换行，`print` 不换行

| Error | 何时 | 例子 |
|:----:|:----:|:----|
| Compile-time | 编译时（语法/类型） | 缺 `;`、`int x = "a";`、变量出 scope |
| Run-time | 运行时 crash（Exception） | 整数 `/ 0`、`charAt` 越界 |
| Logical | 能运行但结果错 | 条件写反、整数除法 |

## 2. Variables & Types

### Primitive types

|Type|Size|说明|
|:----:|:----:|:----|
|byte|1|-128 ~ 127|
|short|2||
|int|4|约 ±21 亿|
|long|8||
|float|4|约 7 位精度|
|double|8|约 15 位精度|
|char|2|单个字符，单引号 `'A'`|
|boolean|1|`true` / `false`|

* `String` **不是** primitive，是 class
* **`long` 要加 `L`，`float` 要加 `F`**：`long a = 123L;`　`float f = 3.14F;`（整数字面量默认 `int`，小数默认 `double`）
* 转义：`\"`　`\'`　`\\`　`\n`　`\t`

### Identifiers

* 以 **字母 / `$` / `_`** 开头，后面可跟字母、`$`、`_`、数字；区分大小写；不能是 keyword
* Valid：`R2D2`、`INT`、`_year_95_`、`String`、`HELLOWORLD`
* Invalid：`30DayAbs`、`rice&beans`、`C-3PO`、`private`、`return`、`float`、`@name`、`my.name`、`hello!`
* Convention：变量/方法 camelCase（`currentItem`），Class 首字母大写（`MyClass`），常量全大写（`MAX_TEMP`）

## 3. Operators

* 比较：`== != < > <= >=`　算术：`+ - * / %`
* **整数除法截断**：`7 / 2 → 3`，`7.0 / 2 → 3.5`；`23 % 4 → 3`
* `x++`（返回旧值再加）vs `++x`（先加再返回新值）；`x += 2` 即 `x = x + 2`
* **Assignment 也是 expression**（有 side effect）：`x = y = 1;`；`if (b = (x <= y))` 把结果赋给 b

### Precedence（高 → 低）

`()` → 一元 `+ - ++ -- !` → `* / %` → `+ -` → `< > <= >=` → `== !=` → `&&` → `||` → 赋值 `= += ...`

* 赋值 **right-to-left**，其余 left-to-right；`1 - 2 + 3 * 4 = 11`；拿不准就加括号

### Casting

* 顺序：`double > float > long > int > short > byte`
* **Widening**（往上）自动：`double y = 6;` ✔　`float x = 3;` ✔
* **Narrowing**（往下）要 cast：`int x = 3.5;` ✘　`int x = (int) 3.5;` ✔（截断）；`byte x = 155;` ✘
* `float x = 3 / 4;` → `0.0`（先整数除法）；`(float) 3 / 4` → `0.75`
* 类型不兼容：`b = 5`（int→boolean）、`c = x`（int→char）✘

## 4. Strings

* **Concatenation 从左到右**，不加空格：
  * `(1 + 2) + "5"` → `"35"`；`"CMSC" + 131 + 10` → `"CMSC13110"`；`131 + 10 + "CMSC"` → `"141CMSC"`
  * `String str = 5 + 7;` ✘ 编译错误（int 不能给 String）
* **比较 String 不能用 `==`**（比的是 reference）→ `s.equals(t)`；`compareTo`：`<0` / `0` / `>0` 表示 s 小于 / 等于 / 大于 t
* String 是 immutable：方法都返回新字符串，不改原来的

|Method|作用|
|:----|:----|
|`length()`|长度|
|`charAt(i)`|第 i 个 **char**（从 0 开始），越界 → run-time error|
|`equals(t)` / `equalsIgnoreCase(t)`|内容比较|
|`toLowerCase()` / `toUpperCase()`|转大小写|
|`Character.isDigit(c)` / `isLetter(c)`|判断 char|

* `String s = name.charAt(0);` ✘（`charAt` 返回 `char`）
* 遍历：`for (int i = 0; i < str.length(); i++)`；写成 `i <= str.length()` 会越界

## 5. Scanner

```java
import java.util.Scanner;
Scanner sc = new Scanner(System.in);
int age = sc.nextInt();
```

* `nextInt() nextDouble() nextBoolean() ...`（类型不对会报错）
* `next()`：读到下一个 **whitespace**；`nextLine()`：读到**换行**（整行）
* 读 char：`sc.next().charAt(0)`
* 只创建**一个** Scanner
* 坑：`nextInt()` 后接 `nextLine()` 会读到残留换行

## 6. Number Bases

* Base-x 有 x 个数字；超过 9 用字母 `A=10 … F=15`
* **→ Base-10**：每位 × 基数的幂：`253₆ = 2·36 + 5·6 + 3 = 105`；`136₇ = 76`；`423₅ = 113`
* **Base-10 →**：不断除以基数记余数，直到商为 0，**余数倒着读**
  * `25 → 11001₂`；`52 → 202₅`；`189 → BD₁₆`

## 7. Conditionals

```java
if (cond1) { ... } else if (cond2) { ... } else { ... }
```

* `else` 不能单独存在
* **多个 `if`**：每个都检查，可能执行多个；**`else if`**：一个成立后面全跳过
* **Dangling else**：else 属于最近的 if → 总是加 `{ }`
* **Empty statement bug**：`if (x == 0);` / `while (cond);` 的 `;` 让它们变成空语句
* `&&`（都 true 才 true）、`||`（有一个 true 就 true）、`!`
* **Short-circuit**（从左到右，结果确定就停）：
  * `&&` 左边 false → 右边不执行；`||` 左边 true → 右边不执行
  * `int x = 4, y = 0; if (x > 2 || ++y > 0)` → `++y` 没执行，y 还是 0
* **Scope**：local variable 只在声明它的 `{ }` 内（声明之后）有效；不同 method 可用同名变量
  ```java
  if (true) { int score = 100; }
  System.out.println(score);   // ✘ compile error
  ```
* `final int MAX = 99;`：常量，必须初始化，之后再赋值会报错；避免 magic numbers

## 8. Loops

| 循环 | 检查条件 | 特点 |
|:----|:----|:----|
| `while (cond) { }` | body **之前** | 可能一次都不执行；后面不加 `;` |
| `do { } while (cond);` | body **之后** | **至少执行一次**；末尾要 `;`；常用于输入验证 |
| `for (init; cond; update) { }` | body 之前 | 顺序：init（一次）→ cond → body → update → cond … |

* 所有 while 都能改写成 for（TRUE）
* **Infinite loop**：条件永不为 false（忘记 update）、`while (cond);` 多了分号 → 先把终止语句（如 `i++`）写进 body
* **Nested loop**：外层每走一次，内层完整走一轮；做输出题用 **trace table**（每个变量一列）
* 长方形：内层 `j <= n`；直角三角形：内层 `j <= i`（见 [[Notes for writing code on paper]]）
* Random：`import java.util.Random;` → `new Random().nextInt(6) + 1` 得 1~6（`nextInt(bound)` 范围 `[0, bound)`）

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print(j);
    }
    System.out.println();
}
// 1
// 12
// 123
```

## 9. Static Methods

```java
public static <返回类型> name(<参数列表>) { body }
```

* 好处：组织代码、**复用**；Static 不需要 object 就能调用，Non-static 需要（`scanner.nextInt()`）
* `public`：任何人可调用；`private`：只有同一 class 的 method 可调用
* 不返回值 → return type 是 **`void`**（可用 `return;` 提前结束）
* **Parameter**：定义里 `( )` 中的变量；**Argument**：调用时传入的值（可以是表达式，先求值）；两者名字无关
* **Pass-by-value**：parameter 是 argument 的**副本**；parameters 和 local variables 在 method 结束时销毁
* `return` 立刻结束 method，返回值类型必须匹配；尽量不超过 2 个 return
* 同一个 class 内调用可省略 class 名

```java
public static int mystery(int x, int y) {
    if (x > y) { return x - y; }
    return x + y;
}
// mystery(8, 3) → 5;  mystery(2, 7) → 9
```

## 10. Java API & 其他

* **Package** = 一组相关 class；用法：`import java.util.Scanner;` 或 `import java.util.*;`；`java.lang`（String、Math）自动 import
* **Math** 全是 static：`Math.abs()`、`Math.pow()`、`Math.ceil()`、`Math.floor()`
* 整数 `/ 0` → exception；浮点 `/ 0` → `Infinity`
* 浮点数不精确（`3.9 - 3.8 ≠ 0.1`）→ 不要用 `==` 比较，用 `Math.abs(a - b) < EPSILON`

## 11. 考前 Checklist

* [ ] 输出题：整数除法、`x++` vs `++x`、字符串 `+` 从左到右、short-circuit
* [ ] 找错题：`charAt` 赋给 String、scope、`String = int`、缺 `;`、`byte b = 155`、`i <= str.length()`
* [ ] 死循环：忘记 update / `while (...);`
* [ ] 嵌套循环输出；进制转换
* [ ] 写 method：先想用哪种循环 / if，再手动 trace 一个例子

### 常见编程题

```java
// 反转字符串
public static String reverse(String str) {
    String result = "";
    for (int i = str.length() - 1; i >= 0; i--) {
        result += str.charAt(i);
    }
    return result;
}

// 找 char 第一次出现的位置，没有返回 -1
public static int findCharacter(String str, char target) {
    for (int i = 0; i < str.length(); i++) {
        if (str.charAt(i) == target) {
            return i;
        }
    }
    return -1;
}

// 数小写元音（不含首尾字符）
public static int countLowerCaseVowels(String str) {
    int count = 0;
    for (int i = 1; i < str.length() - 1; i++) {
        char c = str.charAt(i);
        if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
            count++;
        }
    }
    return count;
}
```
