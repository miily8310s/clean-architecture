# 第１０章 ISP:インターフェース分離の原則

## インターフェース分離の原則（ISP）と言語との関係

- Java のような静的型付け言語は、`import`/`use`/`include`といった宣言をプログラマに強要する
- なのでこれらの宣言のために、再コンパイルが必要になってしまう
- 一方 Python のような動的型付け言語にはこうした宣言はなく、実行時に推論される
- つまり再コンパイルを強制するソースコードの依存性は存在しない
- 静的型付け言語よりも動的型付け言語のほうが柔軟で疎結合なシステムを作れる

## 補足

<!-- @see https://postd.cc/solid-principles-every-developer-should-know/ -->

**インターフェース分離の原則(ISP)**：

- インターフェースは１つのジョブだけを（SRP の原則と同様に）実行するべき
- 利用することのないメソッドはすべて取り除き、他のインターフェースに移動させるべき

### 例

- `IShape` インターフェースおよび `Shape` インターフェースを実装している `Circle` `クラス、Square` クラス、`Rectangle` クラスがあるとする
  - `Circle` クラス、`Square` クラス、`Rectangle` クラスは各メソッド `drawCircle()`、`drawSquare()`、`drawRectangle()`を定義しなければいけない
- ただしそれぞれのクラスでは利用することのないメソッドが実装されてしまった、奇妙なコードになっている
  - Rectangle クラスは利用することのない `drawCircle` メソッドと `drawSquare` メソッドを実装
  - 同様に Square クラスは `drawCircle` メソッドと `drawRectangle` メソッドを実装
  - 同様に Circle クラスは、`drawSquare` メソッドと `drawRectangle` メソッドを実装

```ts
interface IShape {
  drawCircle();
  drawSquare();
  drawRectangle();
}
```

```ts
class Circle implements IShape {
  drawCircle() {
    //...
  }
  drawSquare() {
    //...
  }
  drawRectangle() {
    //...
  }
}

class Square implements IShape {
  drawCircle() {
    //...
  }
  drawSquare() {
    //...
  }
  drawRectangle() {
    //...
  }
}

class Rectangle implements IShape {
  drawCircle() {
    //...
  }
  drawSquare() {
    //...
  }
  drawRectangle() {
    //...
  }
}
```

この `IShape` インターフェースを ISP の原則に従わせるために…

- 方法その１. action を異なるインターフェースに分離させる

```ts
interface IShape {
  draw();
}

interface ICircle {
  drawCircle();
}

interface ISquare {
  drawSquare();
}

interface IRectangle {
  drawRectangle();
}

interface ITriangle {
  drawTriangle();
}

class Circle implements ICircle {
  drawCircle() {
    //...
  }
}

class Square implements ISquare {
  drawSquare() {
    //...
  }
}

class Rectangle implements IRectangle {
  drawRectangle() {
    //...
  }
}

class Triangle implements ITriangle {
  drawTriangle() {
    //...
  }
}

class CustomShape implements IShape {
  draw() {
    //...
  }
}
```

- 方法その２. クラス（`Circle`、`Rectangle`、`Square`、`Triangle` など）は、`IShape` インターフェースから単に継承させ、それぞれの `draw` の behavior を実装する

```ts
class Circle implements IShape {
  draw() {
    //...
  }
}

class Triangle implements IShape {
  draw() {
    //...
  }
}

class Square implements IShape {
  draw() {
    //...
  }
}

class Rectangle implements IShape {
  draw() {
    //...
  }
}
```
