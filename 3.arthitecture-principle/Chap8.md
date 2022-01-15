# 第８章 OCP:オープン・クローズドの原則

TODO: バックエンドの知識を蓄えたら、内容追記する

## まとめ

- **オープン・クローズドの原則(OCP)**はシステムのアーキテクチャの隠れた原動力
- **オープン・クローズドの原則(OCP)**の目的：変更の影響を受けずにシステムを拡張しやすくすること
  - システムをコンポーネントに分割して、コンポーネントの依存関係を階層構造にする
  - 上位レベルのコンポーネントが下位レベルのコンポーネントの変更の影響を受けないように

## 補足

<!-- @see https://postd.cc/solid-principles-every-developer-should-know/ -->

- ※元記事では「オープン・クローズドの原則」 → 「開放閉鎖の原則」として紹介されている

**オープン・クローズドの原則(OCP)**：

- ソフトウェアのエンティティ（`クラス、モジュール、関数`）は`拡張`に対して開き、`修正`に対して閉じていなければならない。

### 例

`Animal`クラスと、その`Animal`クラスのインスタンス（`animal`）のリストを順に処理し、その鳴き声を出すメソッドがあったとする。
新しい`animal`、Snake を追加したら、`AnimalSound`メソッドを変更する必要が出てしまう。

```ts
class Animal {
  constructor(name: string) {}
  getAnimalName() {}
}
```

```diff
const animals: Animal[] = [
    new Animal('lion'),
    new Animal('mouse')
+   new Animal('snake')
];
function AnimalSound(a: Animal[]) {
    for(int i = 0; i <= a.length; i++) {
        if(a[i].name == 'lion')
            log('roar');
        if(a[i].name == 'mouse')
            log('squeak');
+       if(a[i].name == 'snake')
+           log('squeak');
    }
}
AnimalSound(animals);
```

OCP に一致させるためには以下の通りにする。

- `Animal` クラス に仮想メソッド `makeSound` を追加
- それぞれの `animal` を `Animal` クラスに拡張させ、仮想の `makeSound` メソッドを実装
  - あらゆる `animal` は `makeSound` の中で、泣き声を出す方法について独自の実装を追加出来る
- `AnimalSound`メソッド は `animal` の配列を順に処理し、`makeSound` メソッドをただ呼び出す
  - それぞれの `animal` を `Animal` クラスに拡張させたおかげで、新しい `animal` を `animal` 配列に追加するだけになった

```ts
class Animal {
  makeSound();
  //...
}
class Lion extends Animal {
  makeSound() {
    return "roar";
  }
}
class Squirrel extends Animal {
  makeSound() {
    return "squeak";
  }
}
class Snake extends Animal {
  makeSound() {
    return "hiss";
  }
}
```

```ts
function AnimalSound(a: Array<Animal>) {
  for(int i = 0; i <= a.length; i++) {
      log(a[i].makeSound());
  }
}
AnimalSound(animals);
```
