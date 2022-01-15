# 第１１章 DIP:依存関係逆転の原則

## 安定した抽象

- 抽象インターフェースの変更は、それに対応する具象実装の変更につながる
- 具象実装を変更してもインターフェースの変更が必要になることはあまりない
- つまり、インターフェースは実装よりも変化しにくい
  - ソフトウェア設計の基本として、出来る限りインターフェースの変更なしで済ませられるようにするがある

安定したソフトウェアアーキテクチャに必要なプラクティス

- **変化しやすい具象クラスを参照しない**
  - 一般的には Abstract Factory パターンを使う
- **変化しやすい具象クラスを継承しない**
- **具象関数をオーバーライドしない**

## 補足

<!-- @see https://postd.cc/solid-principles-every-developer-should-know/ -->

**依存関係逆転の原則(DIP)**：

- 依存性は、具体化ではなく抽象化でなければならない
- 高水準モジュールは低水準モジュールに依存してはならない。両者は、抽象化に依存するべき
- 抽象化は、詳細に依存してはならない。詳細は、抽象化に依存するべきである

### 例

- `Http` は高水準コンポーネントで、`HttpService` は低水水準コンポーネントとする
  - DIP の「高水準モジュールは低水準モジュールに依存してはならない。両者は、抽象化に依存するべきである」の法則に違反している
  - この `Http` クラスは、`XMLHttpService` クラスに依存することを強いられてしまっている

```ts
class XMLHttpService extends XMLHttpRequestService {}

class Http {
  constructor(private xmlhttpService: XMLHttpService) {}
  get(url: string, options: any) {
    this.xmlhttpService.request(url, "GET");
  }
  post() {
    this.xmlhttpService.request(url, "POST");
  }
  //...
}
```

違反を解決させるためには…

1. `request`メソッドを持った `Connection` インターフェースを作成し、Http クラスに `Connection` 型の引数を渡す

```ts
interface Connection {
  request(url: string, opts: any);
}
```

```ts
class Http {
  constructor(private httpConnection: Connection) {}
  get(url: string, options: any) {
    this.httpConnection.request(url, "GET");
  }
  post() {
    this.httpConnection.request(url, "POST");
  }
  //...
}
```

2. `Connection` インターフェースを実装するために、`XMLHttpService`クラスを再実装

```ts
class XMLHttpService implements Connection {
  xhr = new XMLHttpRequest();
  //...
  request(url: string, opts: any) {
    xhr.open();
    xhr.send();
  }
}
```

これで多くの `HttpConnection` のクラス（Node.js や Mock 用など）を作成し、`Http` クラスに渡すことが出来る

```ts
class NodeHttpService implements Connection {
  request(url: string, opts: any) {
    //...
  }
}

class MockHttpService implements Connection {
  request(url: string, opts: any) {
    //...
  }
}
```
