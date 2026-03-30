# LIFFプラグイン

<!-- table of contents -->

## LIFFプラグインとは 

LIFFプラグインとは、LIFF SDKを拡張できる機能です。LIFFプラグインを使うと、LIFF SDKに独自のAPIを追加したり、LIFF APIの挙動を変更したりできます。

LIFFプラグインの実態は、特定のプロパティやメソッドを持つ、オブジェクトあるいはクラスです。

## LIFFプラグインの動作環境 

LIFFプラグインはLIFF v2.19.0以降で利用できます。

## LIFFプラグインを使用する 

LIFFプラグインは、[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドを使用して有効化します。[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドにLIFFプラグインを渡すと、LIFFプラグインが有効化されます。LIFFプラグインを有効化すると、`liff`オブジェクトが拡張され、LIFFプラグインのAPIを利用できるようになります。

以下は、LIFFプラグイン`GreetPlugin`を有効化し、`liff.$greet.hello()`メソッドを実行する例です。

### LIFFプラグインがクラスの場合 

LIFFプラグインがクラスの場合、[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドにインスタンスを渡す必要があります。

```js
class GreetPlugin {
  constructor() {
    this.name = "greet";
  }

  install() {
    return {
      hello: this.hello,
    };
  }

  hello() {
    console.log("Hello, World!");
  }
}

liff.use(new GreetPlugin());

liff.$greet.hello(); // Hello, World!

liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    // ...
  });
```

### LIFFプラグインがオブジェクトの場合 

```js
const hello = () => {
  console.log("Hello, World!");
};

const greetPlugin = {
  name: "greet",
  install() {
    return {
      hello,
    };
  },
};

liff.use(greetPlugin);

liff.$greet.hello(); // Hello, World!

liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    // ...
  });
```

このように、LIFFプラグインを有効化すると、`name`プロパティの値に`$`の接頭語がついたプロパティが`liff`オブジェクトに追加されます。これにより、LIFFプラグインのAPIを`liff.${LIFFプラグインのnameプロパティの値}.{プロパティ}`や`liff.${LIFFプラグインのnameプロパティの値}.{メソッド}()`の形式で利用できます。

## LIFFプラグインを作成する 

LIFFプラグインは、[`name`](https://developers.line.biz/ja/docs/liff/liff-plugin/#name)プロパティと[`install()`](https://developers.line.biz/ja/docs/liff/liff-plugin/#install)メソッドを持つ、オブジェクトあるいはクラスとして作成できます。

以下は、APIとして`hello()`メソッドと`goodbye()`メソッドを提供する、LIFFプラグイン`GreetPlugin`の例です。

### LIFFプラグインがクラスの場合 

```js
class GreetPlugin {
  constructor() {
    this.name = "greet";
  }

  install() {
    return {
      hello: this.hello,
      goodbye: this.goodbye,
    };
  }

  hello() {
    console.log("Hello, World!");
  }

  goodbye() {
    console.log("Goodbye, World!");
  }
}

liff.use(new GreetPlugin());

liff.$greet.hello(); // Hello, World!
liff.$greet.goodbye(); // Goodbye, World!
```

### LIFFプラグインがオブジェクトの場合 

```js
const hello = () => {
  console.log("Hello, World!");
};

const goodbye = () => {
  console.log("Goodbye, World!");
};

const greetPlugin = {
  name: "greet",
  install() {
    return {
      hello,
      goodbye,
    };
  },
};

liff.use(greetPlugin);

liff.$greet.hello(); // Hello, World!
liff.$greet.goodbye(); // Goodbye, World!
```

### nameプロパティ 

`name`プロパティは、LIFFプラグインの名前です。文字列で指定します。

指定した値は、`liff.${LIFFプラグインのnameプロパティの値}`のように、`liff`オブジェクトのプロパティ名となります。

### install()メソッド 

`install()`メソッドは、以下のことを行う関数です。

- [LIFFプラグインの初期化処理を記述する](https://developers.line.biz/ja/docs/liff/liff-plugin/#describe-initialization-process-for-liff-plugin)
- [LIFFプラグインのAPIを定義する](https://developers.line.biz/ja/docs/liff/liff-plugin/#define-liff-plugin-api)

#### LIFFプラグインの初期化処理を記述する 

`install()`メソッドは、LIFFプラグインの有効化時に[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドによって実行されます。そのため、LIFFプラグインの初期化処理を`install()`メソッド内に記述できます。

#### LIFFプラグインのAPIを定義する 

LIFFプラグインのAPIは、`install()`メソッドの返り値として定義されます。オブジェクトを返すことで、複数のAPIを定義できます。

なお、LIFFプラグインのAPIが1つのみの場合、そのAPIを返り値とすることも可能です。以下は、`install()`メソッドの返り値として、オブジェクトではなく関数を返す例です。

```js
class GreetPlugin {
  constructor() {
    this.name = "greet";
  }

  install() {
    return this.hello;
  }

  hello() {
    console.log("Hello, World!");
  }
}

liff.use(new GreetPlugin());

liff.$greet(); // Hello, World!
```

#### install()メソッドの引数 

`install()`メソッドは、第1引数に[`context`](https://developers.line.biz/ja/docs/liff/liff-plugin/#context)オブジェクト、第2引数に[`option`](https://developers.line.biz/ja/docs/liff/liff-plugin/#option)を取ります。

```js
class GreetPlugin {
  constructor() {
    this.name = "greet";
  }

  install(context, option) {}
}
```

##### `context`オブジェクト 

`install()`メソッドの第1引数です。以下の2つのプロパティを持ちます。

| プロパティ | 値 |
| --- | --- |
| `liff` | `liff`オブジェクト |
| `hooks` | [フックにコールバックを登録する](https://developers.line.biz/ja/docs/liff/liff-plugin/#register-callback-with-hook)ためのメソッドを提供するオブジェクト |

##### `option` 

`install()`メソッドの第2引数です。[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドの第2引数に指定した値が渡されます。[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドの第2引数が未指定の場合、`option`の値は`undefined`となります。

`option`は、[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッド側からLIFFプラグインの挙動をカスタマイズできるようにする、といった用途に利用できます。

## フックについて 

フックとは、LIFF APIの処理中の特定のタイミングで、事前に登録されたコールバックを実行させるためのLIFFプラグインの仕組みです。フックは、JavaScriptのイベント処理と同じように考えることができます。フックにコールバックを登録しておくと、フックが発火したタイミングで、コールバックが実行されます。

LIFF APIが提供するフックを利用するだけでなく、LIFFプラグインが独自のフックを提供することも可能です。

### LIFF APIのフック 

現時点では、LIFF APIは[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッドのみ、フックを提供しています。

<table>
  <thead>
    <tr>
      <th>LIFF API</th>
      <th>フック</th>
      <th>フックの種類</th>
      <th>フックの発火タイミング</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2"><code>liff.init()</code>メソッド</td>
      <td><code>before</code>フック</td>
      <td><a href="#async-hook">非同期フック</a></td>
      <td><code>liff.init()</code>の呼び出し直後（LIFFアプリの初期化前）</td>
    </tr>
    <tr>
      <td><code>after</code>フック</td>
      <td><a href="#async-hook">非同期フック</a></td>
      <td><code>successCallback</code>の呼び出し直前（LIFFアプリの初期化後）</td>
    </tr>
  </tbody>
</table>

### フックの種類 

フックには[同期フック](https://developers.line.biz/ja/docs/liff/liff-plugin/#sync-hook)と[非同期フック](https://developers.line.biz/ja/docs/liff/liff-plugin/#async-hook)の2種類があります。

#### 同期フック 

同期フックは、登録されたコールバックを同期的に処理します。登録されたコールバックは、登録された順番に処理されます。登録されたコールバックの返り値は無視されます。

#### 非同期フック 

非同期フックは、登録されたコールバックを非同期的に処理します。登録されたコールバックは、`Promise.all()`メソッドを使って、並列に処理されます。登録されたコールバックの返り値は`Promise`オブジェクトである必要があります。

### フックにコールバックを登録する 

フックにコールバックを登録するには、[`install()`](https://developers.line.biz/ja/docs/liff/liff-plugin/#install)メソッドの[`context.hooks`](https://developers.line.biz/ja/docs/liff/liff-plugin/#context)プロパティを使います。

以下は、[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッドの`before`フックと`after`フックにコールバックを登録する例です。[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッドが実行されると、`before`フックと`after`フックが発火し、登録されたコールバックが実行されます。

`before`フックと`after`フックは[非同期フック](https://developers.line.biz/ja/docs/liff/liff-plugin/#async-hook)のため、`Promise`オブジェクトを返す必要がある点に注意してください。

```js
class GreetPlugin {
  constructor() {
    this.name = "greet";
  }

  install(context) {
    context.hooks.init.before(this.initBefore);
    context.hooks.init.after(this.initAfter);
    return {
      hello: this.hello,
      goodbye: this.goodbye,
    };
  }

  hello() {
    console.log("Hello, World!");
  }

  goodbye() {
    console.log("Goodbye, World!");
  }

  initBefore() {
    console.log("before hook is called");
    return Promise.resolve();
  }

  initAfter() {
    console.log("after hook is called");
    return Promise.resolve();
  }
}

liff.use(new GreetPlugin());

liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    // ...
  });
```

### フックを作成する 

フックは、`SyncHook`クラスあるいは`AsyncHook`クラスのインスタンスとして作成できます。

| フックの種類                           | クラス      |
| -------------------------------------- | ----------- |
| <a href="#sync-hook">同期フック</a>    | `SyncHook`  |
| <a href="#async-hook">非同期フック</a> | `AsyncHook` |

以下は、`helloBefore`フックと`helloAfter`フックを作成する例です。`SyncHook`クラスと`AsyncHook`クラスは、`@liff/hooks`パッケージからインポートする必要がある点に注意してください。

作成したフックを発火するには、`SyncHook`クラスのインスタンスや`AsyncHook`クラスのインスタンスの[`call()`](https://developers.line.biz/ja/docs/liff/liff-plugin/#call)メソッドを実行します。

```js
import { SyncHook, AsyncHook } from "@liff/hooks";

class GreetPlugin {
  constructor() {
    this.name = "greet";
    this.hooks = {
      helloBefore: new SyncHook(),
      helloAfter: new AsyncHook(),
    };
  }

  install(context) {
    return {
      hello: this.hello.bind(this),
      goodbye: this.goodbye,
    };
  }

  hello() {
    this.hooks.helloBefore.call();
    console.log("Hello, World!");
    this.hooks.helloAfter.call();
  }

  goodbye() {
    console.log("Goodbye, World!");
  }
}
```

作成したフックは、別のLIFFプラグインがコールバックを登録するのに利用できます。以下は、LIFFプラグイン`GreetPlugin`の`helloBefore`フックと`helloAfter`フックにコールバックを登録する例です。

```js
import { SyncHook, AsyncHook } from "@liff/hooks";

class GreetPlugin {
  constructor() {
    this.name = "greet";
    this.hooks = {
      helloBefore: new SyncHook(),
      helloAfter: new AsyncHook(),
    };
  }

  install(context) {
    return {
      hello: this.hello.bind(this),
      goodbye: this.goodbye,
    };
  }

  hello() {
    this.hooks.helloBefore.call();
    console.log("Hello, World!");
    this.hooks.helloAfter.call();
  }

  goodbye() {
    console.log("Goodbye, World!");
  }
}

class OtherPlugin {
  constructor() {
    this.name = "other";
  }

  install(context) {
    context.hooks.$greet.helloBefore(this.greetBefore);
    context.hooks.$greet.helloAfter(this.greetAfter);
  }

  greetBefore() {
    console.log("helloBefore hook is called");
  }

  greetAfter() {
    console.log("helloAfter hook is called");
    return Promise.resolve();
  }
}

liff.use(new GreetPlugin());
liff.use(new OtherPlugin());
liff.$greet.hello();
// helloBefore hook is called
// Hello, World!
// helloAfter hook is called
```

#### `call()`メソッド 

`call()`メソッドはフックを発火するための関数です。`call()`メソッドには、任意の数の引数を渡すことができます。`call()`メソッドに渡した引数は、フックに登録したコールバックが引数として受け取ることができます。

以下は、フックの`call()`メソッドに引数を渡し、それをコールバックが受け取る例です。

```js
import { SyncHook, AsyncHook } from "@liff/hooks";

class GreetPlugin {
  constructor() {
    this.name = "greet";
    this.hooks = {
      helloBefore: new SyncHook(),
      helloAfter: new AsyncHook(),
    };
  }

  install(context) {
    return {
      hello: this.hello.bind(this),
      goodbye: this.goodbye,
    };
  }

  hello() {
    this.hooks.helloBefore.call("foo");
    console.log("Hello, World!");
    this.hooks.helloAfter.call("foo", 0);
  }

  goodbye() {
    console.log("Goodbye, World!");
  }
}

class OtherPlugin {
  constructor() {
    this.name = "other";
  }

  install(context) {
    context.hooks.$greet.helloBefore(this.greetBefore);
    context.hooks.$greet.helloAfter(this.greetAfter);
  }

  greetBefore(foo) {
    console.log(foo); // foo
  }

  greetAfter(foo, bar) {
    console.log(foo, bar); // foo 0
    return Promise.resolve();
  }
}

liff.use(new GreetPlugin());
liff.use(new OtherPlugin());
liff.$greet.hello(); // Hello, World!
```

## 公式LIFFプラグイン 

以下の公式LIFFプラグインを公開しています。

- [LIFF Inspector](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-inspector)
- [LIFF Mock](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-mock)

### LIFF Inspector 

LIFF Inspectorは、LIFFアプリをデバッグするためのLIFFプラグインです。LIFF Inspectorを使うと、LIFFアプリを実行している端末とは別のPC上の[Chrome DevTools](https://developer.chrome.com/docs/devtools/)を使って、LIFFアプリをデバッグできます。

LIFF Inspectorについて詳しくは、GitHubの[README](https://github.com/line/liff-inspector/blob/main/README_ja.md)や[npm](https://www.npmjs.com/package/@line/liff-inspector)の［**Readme**］タブを参照してください。

- [GitHub](https://github.com/line/liff-inspector)
- [npm](https://www.npmjs.com/package/@line/liff-inspector)

### LIFF Mock 

LIFF Mockは、LIFFアプリのテストを簡単にするためのLIFFプラグインです。LIFF Mockを使うと、LIFF SDKにモックモードを追加できます。モックモードでは、LIFFアプリがLIFFサーバーから独立し、LIFF APIがモックデータを返すため、単体テストや負荷テストをより簡単に行うことができます。

LIFF Mockについて詳しくは、GitHubの[README](https://github.com/line/liff-mock/blob/main/README.md)や[npm](https://www.npmjs.com/package/@line/liff-mock)の［**Readme**］タブを参照してください。

- [GitHub](https://github.com/line/liff-mock)
- [npm](https://www.npmjs.com/package/@line/liff-mock)
