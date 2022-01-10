# 第３章 パラダイムの概要

- 本章では３つのパラダイムの概要を紹介する
- ３つのパラダイムは：**構造化プログラミング**/**オブジェクト指向プログラミング**/**関数型プログラミング**

- **構造化プログラミング**は、直接的な制御の移行に規律を課すもの
- **オブジェクト指向プログラミング**は、間接的な制御の移行に規律を課すもの
- **関数型プログラミング**は、代入に規律を課すもの

## まとめ

- 紹介した３つのパラダイムは、アーキテクチャの３つの大きな関心事に対応している
- ３つの大きな関心事
  - **コンポーネントの分離**
  - **データ管理**
  - **機能**

TODO: **構造化プログラミング**/**オブジェクト指向プログラミング**/**関数型プログラミング**の概要と実装方法をここに残す

## （補足）構造化プログラミング

### 参照ページ

https://active.nikkeibp.co.jp/atclact/active/17/060100293/060800002/
https://e-words.jp/w/%E6%A7%8B%E9%80%A0%E5%8C%96%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0.html

### 構造化プログラミングとは？

- コンピュータプログラムの開発や理解、修正を円滑に行えるよう、プログラムを整理された構造の組み合わせによって構成すること。
- = 「順接」「反復」「分岐」の三つの制御構造によって処理の流れを記述すること

## （補足）関数型プログラミング

### 参照ページ

https://it-trend.jp/development_tools/article/32-0053
https://e-words.jp/w/%E9%96%A2%E6%95%B0%E5%9E%8B%E8%A8%80%E8%AA%9E.html

### 関数型プログラミングとは？

- 簡単に言うと、プログラム中の処理や制御を、関数の定義と適用の組み合わせでプログラミングすること。
- 簡潔な関数の組み合わせでコーディングするので、個々の関数は独立しており、実行中の処理の影響を受けない
  - コード全体がシンプルで分かりやすく、保守性や再利用性に優れている
  - 一方で関数が独立しているため、前の処理の引き継ぎを苦手とする

### 関数型プログラミングの例

- Haskell
- Lisp
- Scala
- F#

※Java や JavaScript、PHP などの有名プログラミング言語は命令型プログラミングに分類される