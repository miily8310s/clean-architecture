# 第 Ⅲ 部 設計の原則

- よくできたソフトウェアシステムは、クリーンなコードを書くことから始まる
- そこで「SOLID 原則」を使用する
- 「SOLID 原則」は、関数やデータ構造をどのようにクラスに組み込みのか、そしてクラスの相互接続をどのようにするのかを教えてくれる
  - ここでいうクラス = 単にいくつかの機能やデータをとりまとめたもの
- 「SOLID 原則」の目的は以下のような性質を持つ中間レベル（モジュールレベル）のソフトウェア構造を作ること
  - 変更に強いこと
  - 理解しやすいこと
  - コンポーネントの基盤として、多くのソフトウェアシステムで利用できること
- 「SOLID 原則」は以下の法則群からなる
  - 単一責任の原則：
    - 個々のモジュールを変更する理由が一つだけになるように
  - オープン・クローズドの原則：
    - 既存のコードの変更よりも新しいコードの追加によって、システムの振る舞いを変更できるように設計すべき
  - リスコフの置換原則
    - 交換可能としたパーツを使って、ソフトウェアシステムを構築する
  - インターフェース分離の原則
    - ソフトウェアを設計する際には、使っていないものへの依存を回避すべき
  - 依存関係逆転の原則
    - 上位レベルの方針の実装コードは、下位レベルの詳細の実装コードに依存すべきではなく、逆に詳細側が方針に依存すべき

## 目次

| 章名                                    | リンク                                                                                                  |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| 第７章 SRP:単一責任の原則               | [メモ](https://github.com/miily8310s/clean-architecture/blob/master/3.arthitecture-principle/Chap7.md)  |
| 第８章 OCP:オープン・クローズドの原則   | [メモ](https://github.com/miily8310s/clean-architecture/blob/master/3.arthitecture-principle/Chap8.md)  |
| 第９章 LSP:リスコフの置換原則           | [メモ](https://github.com/miily8310s/clean-architecture/blob/master/3.arthitecture-principle/Chap9.md)  |
| 第１０章 ISP:インターフェース分離の原則 | [メモ](https://github.com/miily8310s/clean-architecture/blob/master/3.arthitecture-principle/Chap10.md) |
| 第１１章 DIP:依存関係逆転の原則         | [メモ](https://github.com/miily8310s/clean-architecture/blob/master/3.arthitecture-principle/Chap11.md) |
