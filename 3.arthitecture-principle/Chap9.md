# 第９章 LSP:リスコフの置換原則

## LSP:リスコフの置換原則とは

以下のプログラムがあるとする。

```md
S 型のオブジェクト o1
T 型のオブジェクト o2 → o1 の各々に対応する
T を使って定義されたプログラム P が存在する
```

o2 の代わりに o1 を使っても P の振る舞いが変わらない場合、S は T の派生型といえる

これを**LSP:リスコフの置換原則**という

## 補足

<!-- @see https://postd.cc/solid-principles-every-developer-should-know/ -->

**リスコフの置換原則(LSP)**：

- サブクラスがエラー無く、そのスーパークラスの場所を引き継げなければならない
  - スーパークラスがスーパークラス型のパラメータを受け入れるメソッドを持っている場合：
    - → そのサブクラスも引数として、スーパークラス型あるいは、サブクラス型を受け入れなければならない
  - スーパークラスがスーパークラス型を返す場合：
    - → そのサブクラスはスーパークラス型あるいは、サブクラス型を返さなければならない
- コードでクラスの型をチェックしているのであれば、この原則に違反している可能性が高い

### 例

- これは、`LSP` の原則に（さらに `OCP` の原則にも）違反している。
- `animal` を新しく追加するたび、新しい `animal` を受け入れるために関数を変更する必要が出てしまう。

```ts
function AnimalLegCount(a: Animal[]) {
    for(int i = 0; i <= a.length; i++) {
        if(typeof a[i] == Lion)
            log(LionLegCount(a[i]));
        if(typeof a[i] == Mouse)
            log(MouseLegCount(a[i]));
        if(typeof a[i] == Snake)
            log(SnakeLegCount(a[i]));
    }
}
AnimalLegCount(animals);
```

違反を解決させるためには…

1. `AnimalLegCount` 関数を以下のように `LegCount` メソッドを呼び出すだけの形で再実装

```ts
function AnimalLegCount(a: Array<Animal>) {
  for (let i = 0; i <= a.length; i++) {
    a[i].LegCount();
  }
}
AnimalLegCount(animals);
```

2. `Animal` クラスおよびそのサブクラスに `LegCount` メソッドを実装、定義する

```ts
class Animal {
  //...
  LegCount();
}
```

```ts
//...
class Lion extends Animal {
  //...
  LegCount() {
    //...
  }
}
//...
```
