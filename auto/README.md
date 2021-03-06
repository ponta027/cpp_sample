# auto

C++11から変数宣言時に具体的な型の代わりにautoキーワードを指定することで、
変数の型を初期化から推論できるようになった。

auto による型推論は、以下の場所で初期化子がある場合のみ使用可能である。

* ブロックスコープでの変数宣言
* 名前空間スコープでの変数宣言
* for 文の初期化文部での変数宣言
* if 文、switch 文、for 文、while 文の条件部での変数宣言
* new 式の型名指定部
* クラス定義内での静的メンバ宣言


[auto](/auto/src/autosample.cpp)

## decltype


オペランドで指定した型を取得する機能。
型を指定する必用がある箇所で、変数に対してdecltypeを呼び出すと型名が取得できる。

```
int i = 0;
decltype(i) j = 0;                      // j は int 型
```

* 経緯

C++03までで、関数テンプレートの戻り値の型をあらゆるケースで正確に表現できることは不可能。

```cpp
template <class Func, class T>
??? trace(Func f, T t) { std::cout << "Calling f"; return f(t); }
```

C++11では関数宣言構文を使用することで下記のように書くことができた。

```cpp

template <class Func, class T>
auto trace(Func f, T t) -> decltype(f(t)) { std::cout << "Calling f"; return f(t); }```

```

以上

