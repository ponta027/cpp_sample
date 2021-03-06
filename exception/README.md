# 例外

例外(Exception)は、実行を例外ハンドラーに移す機能。
例外はスレッドごとに存在する。
実行を例外ハンドラーに移す際に、オブジェクトを渡すことができる。
例外ハンドラーに実行を移すには、tryブロックの中か、tryブロックの中で呼ばれている関数の中でthrow式を使う。



## noexcept

例外を投げる可能性がない関数にはnoexceptを指定する。
もう一つの意味は、式が例外を投げる可能性があるかどうか判定する演算子。
noexcept(f(arg))のようにnoexcept演算子に式を指定することができる。
式が例外を投げる可能性があるかどうかコンパイル時に取得できる。

* noexceptは、代表的には以下の2つの用途で使用できる：
    * パフォーマンス向上  
      例外を送出しないという保証があることで、コンパイラは例外送出によるスタック巻き戻しのためのスタックを確保する必要がなくなる
    * 例外を決して送出しない強い例外安全性の保証(No-throw guarantee)  
      例外安全性で有名な問題としてstackのpop操作がある。  
      要素型Tのコピーコンストラクタが例外を送出する可能性があるためにpopの関数はTを返すのではなく戻り値型voidとする必要があった。  
      しかしreturn文に指定する式が決して例外を送出しないという保証があることで、popの関数はT型のオブジェクトを返せるようになる。
      参照： ジェネリックコンポーネントにおける例外安全性 - boostjp


noexceptをつけた関数がthrowする場合、g++ではコンパイル時に警告が出力される。
実行した場合、関数をtry/catchでくくってもcatchできない。

[sample](/exception/src/exceptionthrow.cpp)

## 補足

例外は、例外的条件に対してのみ使用すべき。
通常の制御フローに対して、例外を使用すべきではない。

https://www.slideshare.net/t_wada/exception-design-by-contract


### 例外種別

検査例外と非検査例外というものが存在する。
検査例外は実装時に例外処理を記述しないとコンパイルエラーとなる。
C++は検査例外は未サポート

* 検査例外
    * システムが事前に想定出来る業務エラーを例外として扱う  
      throwsのようにエラーハンドリングが必要な旨を構文で記述できる
      例外が発生するメソッド呼び出し側でcatchしてエラーハンドリングを記述しないとコンパイルエラーとなる
      Java、Swiftで採用 (他にあったら教えてください)
* 非検査例外
    * システムが事前に想定出来ないエラーを例外として扱う
      構文として記述しなくてもコンパイル可能
      Java、Swift以外で採用。Ruby / C++ / C# / JavaScript / Kotlin 等




以上
