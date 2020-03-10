---
version: 1.0.0
example_title: 変数
---

# 変数

Vの変数は`:=`演算子で宣言および初期化できます。Vの変数はこれ以外の方法では宣言できません。つまり、いかなる変数にも初期値が存在するということです。変数の型は、右辺の値から推測されます。Vの変数はデフォルトでイミュータブル（immutable: 値を改変できない）です。

```v
age := 23               // int
name := 'Alice'         // string
is_adult := age > 21    // bool

println(age_str)        // 23
println(name)           // Alice
println(is_adult)       // true
```

> メモ: 変数の定義は、関数の内側でしか行なえません。Vにはグローバル変数もグローバルステートも存在しません。

変数の値を変更するには、変数がミュータブル（mutable: 改変可能）になっている必要があります。変数の宣言時に`mut`キーワードを用いることで、変数をミュータブルにできます。変数に新しい値を代入するには`=`を用います。

```v
mut age := 20       // ミュータブルな変数ageを宣言して値20を代入する
println(age)        // 20
age = 21            // ageに新しい値を代入する
println(age)        // 21
```

上のコードは`mut`キーワードがないとエラーになります（イミュータブルな変数の値は変更できない）。
v
```v
fn main() {
    age = 20
    println(age)
}
```

上のコードはコンパイルの段階でエラーになります（変数`age`が宣言されていないため）。


```v
fn main() {
    mut age := 20       // ミュータブルなage変数を宣言して値20を代入
    println(age)        // 20
    age := 21           // ERROR
}
```

上の`age := 21`では、別のエラーがコンパイル時に発生します（変数`age`が同じスコープ内で既に定義されているため）。非常にシンプルで覚えやすいルールです。値の宣言は`:=`で、以後の代入は`=`と覚えておきましょう。

Goと同様、不要な値は`_`で受け止めて無視できます。これは値を複数返す関数で使われるのが普通です【TBD】。

```v
_, a := foo()
println(_) // ERROR: Cannot use `_` as value
```

## 命名のルール

以下は、変数の命名で守るべきルールの一覧です。

- 大文字を含んではならない（✖`AlphaTest`）
- 区切り文字にはアンダースコアを用いる（○`hello_world`）
- できるかぎり、意味の明快な名前を付けること
- 名前に`__`を含んではならない
- 名前に（種類を問わず）スペース文字を含んではならない
- 名前が11文字を超えたら必ず`_`で区切らなければならない

上のルールは[`snake_case`](https://en.wikipedia.org/wiki/Snake_case)が由来です。Vではsnake_caseスタイルが用いられ、また推奨されます（読みやすく、書きやすく、理解しやすいため）。

### 正しい名前

```v
boby
john_dads
myfamily_number
```

### 正しくない名前

```v
IamNotValid
new Make
```