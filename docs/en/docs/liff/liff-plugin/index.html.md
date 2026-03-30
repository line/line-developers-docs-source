# LIFF plugin

<!-- table of contents -->

## What is LIFF plugin 

LIFF plugin is a feature to extend the LIFF SDK. Using a LIFF plugin, you can add your own APIs to the LIFF SDK or change the behavior of LIFF APIs.

A LIFF plugin is an object or a class with specific properties and a specific method.

## Operating environment of LIFF Plugin 

LIFF plugin is available in LIFF v2.19.0 or later.

## Using a LIFF plugin 

Use the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method to activate a LIFF plugin. Passing a LIFF plugin to the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method activates the LIFF plugin. When the LIFF plugin is activated, the `liff` object will be extended and the API of the LIFF plugin will be available.

The following is an example of activating a LIFF plugin called `GreetPlugin` and executing the `liff.$greet.hello()` method.

### If the LIFF plugin is a class 

If the LIFF plugin is a class, you need to pass the instance to the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method.

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

### If the LIFF plugin is an object 

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

As you can see above, when a LIFF plugin is activated, a property is added to the `liff` object with a `$` prefix to the value of the `name` property. This allows you to use the API of a LIFF plugin in `liff.${value of the name property of the LIFF plugin}.{property name}` and `liff.${value of the name property of the LIFF plugin}.{method name}()` formats.

## Creating a LIFF plugin 

You can create a LIFF plugin as an object or a class that has the [`name`](https://developers.line.biz/en/docs/liff/liff-plugin/#name) property and the [`install()`](https://developers.line.biz/en/docs/liff/liff-plugin/#install) method.

The following is an example of a LIFF plugin called `GreetPlugin` which offers the `hello` method and the `goodbye()` method as APIs.

### If the LIFF plugin is a class 

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

### If the LIFF plugin is an object 

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

### name propery 

The value of the `name` property is the name of a LIFF plugin. Specify the `name` property a string.

The specified value will be the property name of the `liff` object, as in `liff.${value of the name property of the LIFF plugin}`.

### install() method 

The `install()` method is a function that does the following:

- [Describing the initialization process of the LIFF plugin](https://developers.line.biz/en/docs/liff/liff-plugin/#describe-initialization-process-for-liff-plugin)
- [Defining the API of the LIFF plugin](https://developers.line.biz/en/docs/liff/liff-plugin/#define-liff-plugin-api)

#### Describing the initialization process of the LIFF plugin 

The `install()` method will be executed by the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method when the LIFF plugin is activated. Therefore, you can describe the initialization process of the LIFF plugin within the `install()` method.

#### Defining the API of the LIFF plugin 

The API of the LIFF plugin is defined as the return value of the `install()` method. You can define multiple APIs by returning an object.

If the LIFF plugin has only one API, it's possible to use that API as the return value. The following is an example of the `install()` method that returns a function instead of an object.

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

#### Arguments of the `install()` method 

The `install()` method takes a [`context`](https://developers.line.biz/en/docs/liff/liff-plugin/#context) object as the first argument and an [`option`](https://developers.line.biz/en/docs/liff/liff-plugin/#option) as the second argument.

```js
class GreetPlugin {
  constructor() {
    this.name = "greet";
  }

  install(context, option) {}
}
```

##### `context` object 

The first argument of the `install()` method. The `context` object has the following two properties:

| Property | Value |
| --- | --- |
| `liff` | `liff` object |
| `hooks` | Object that provides methods for [registering a callback on a hook](https://developers.line.biz/en/docs/liff/liff-plugin/#register-callback-with-hook) |

##### `option` 

The second argument of the `install()` method. The value specified in the second argument of the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method is passed. If the second argument of the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method is unspecified, the value of `option` will be `undefined`.

You can use `option` to customize the behavior of a LIFF plugin by passing an argument to the [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method.

## About hook 

Hook is a mechanism in LIFF plugin that allows pre-registered callbacks to be executed at a specific time during the processing of a LIFF API. You can think of hook in the same way as event processing in JavaScript. If a callback is registered with a hook, the callback will be executed at the timing when the hook is fired.

In addition to using hooks provided by the LIFF API, LIFF plugins can provide their own hooks.

### Hooks for LIFF API 

At this time, the LIFF API provides hooks only for the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method.

<table>
  <thead>
    <tr>
      <th>LIFF API</th>
      <th>Hook</th>
      <th>Hook type</th>
      <th>When the hook fires</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2"><code>liff.init()</code>method</td>
      <td><code>before</code> hook</td>
      <td><a href="#async-hook">async hook</a></td>
      <td>Immediately after calling <code>liff.init()</code> (before the initialization of a LIFF app)</td>
    </tr>
    <tr>
      <td><code>after</code> hook</td>
      <td><a href="#async-hook">async hook</a></td>
      <td>Immediately before calling <code>successCallback</code> (after the initialization of a LIFF app)</td>
    </tr>
  </tbody>
</table>

### Hook types 

There are two types of hooks: [sync hook](https://developers.line.biz/en/docs/liff/liff-plugin/#sync-hook) and [async hook](https://developers.line.biz/en/docs/liff/liff-plugin/#async-hook).

#### Sync hook 

Sync hook processes registered callbacks synchronously. Registered callbacks are processed in the order in which they are registered. The return value of registered callbacks is ignored.

#### Async hook 

Async hook processes registered callbacks asynchronously. Registered callbacks are processed in parallel using the `Promise.all()` method. The return value of registered callbacks must be a `Promise` object.

### Registering a callback on a hook 

To register a callback on a hook, use the [`context.hooks`](https://developers.line.biz/en/docs/liff/liff-plugin/#context) property of the [`install()`](https://developers.line.biz/en/docs/liff/liff-plugin/#install) method.

The following is an example of registering callbacks on the `before` hook and the `after` hook of the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method. When the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method is executed, the `before` hook and the `after` hook will fire, and the registered callbacks will be executed.

Note that the `before` hook and the `after` hook are async hooks, so the registered callbacks must return a `Promise` object.

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

### Creating a hook 

You can create a hook as an instance of the `SyncHook` class or the `AsyncHook` class.

| Hook type                            | Class       |
| ------------------------------------ | ----------- |
| <a href="#sync-hook">sync hook</a>   | `SyncHook`  |
| <a href="#async-hook">async hook</a> | `AsyncHook` |

The following is an example of creating hooks called `helloBefore` and `helloAfter`. Note that you need to import the `SyncHook` class and the `AsyncHook` class from the `@liff/hooks` package.

To fire the created hooks, execute the [`call()`](https://developers.line.biz/en/docs/liff/liff-plugin/#call) method of the instances of the `SyncHook` class and the `AsyncHook` class.

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

The hooks created can be used by other LIFF plugins to register callbacks. The following is an example of registering callbacks on the `helloBefore` hook and the `helloAfter` hook of a LIFF plugin called `GreetPlugin`.

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

#### `call()` method 

The `call()` method is a function to fire a hook. You can pass any number of arguments to the `call()` method. The arguments passed to the `call()` method can be received as arguments by callbacks registered with the hook.

The following is an example of passing arguments to the `call()` method of hooks and having callbacks receive them.

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

## Official LIFF plugins 

We provide the following official LIFF plugins:

- [LIFF Inspector](https://developers.line.biz/en/docs/liff/liff-plugin/#liff-inspector)
- [LIFF Mock](https://developers.line.biz/en/docs/liff/liff-plugin/#liff-mock)

### LIFF Inspector 

LIFF Inspector is a LIFF plugin to debug your LIFF app. Using LIFF Inspector, you can debug your LIFF app with [Chrome DevTools](https://developer.chrome.com/docs/devtools/) on a different PC than the device on which you are running the LIFF app.

Fore more information on LIFF Inspector, see the [README](https://github.com/line/liff-inspector/blob/main/README.md) on GitHub or the **Readme** tab on [npm](https://www.npmjs.com/package/@line/liff-inspector).

- [GitHub](https://github.com/line/liff-inspector)
- [npm](https://www.npmjs.com/package/@line/liff-inspector)

### LIFF Mock 

LIFF Mock is a LIFF plugin to make testing your LIFF app easy. Using LIFF Mock, you can add the mock mode to the LIFF SDK. In the mock mode, your LIFF app is independent of the LIFF server and the LIFF API returns mock data. Therefore, you can perform unit testing or load testing more easily.

Fore more information on LIFF Mock, see the [README](https://github.com/line/liff-mock/blob/main/README.md) on GitHub or the **Readme** tab on [npm](https://www.npmjs.com/package/@line/liff-mock).

- [GitHub](https://github.com/line/liff-mock)
- [npm](https://www.npmjs.com/package/@line/liff-mock)
