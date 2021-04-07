# API-Expect

当您编写测试时，您通常需要检查值是否满足某些条件。预期允许您访问许多“匹配器”，这些“匹配器”允许您验证不同的东西。

有关由Jest社区维护的其他Jest匹配器，请查看 [`jest-extended`](https://github.com/jest-community/jest-extended).

## 方法

- [`expect(value)`](https://www.jestjs.cn/docs/expect#expectvalue)
- [`expect.extend(matchers)`](https://www.jestjs.cn/docs/expect#expectextendmatchers)
- [`expect.anything()`](https://www.jestjs.cn/docs/expect#expectanything)
- [`expect.any(constructor)`](https://www.jestjs.cn/docs/expect#expectanyconstructor)
- [`expect.arrayContaining(array)`](https://www.jestjs.cn/docs/expect#expectarraycontainingarray)
- [`expect.assertions(number)`](https://www.jestjs.cn/docs/expect#expectassertionsnumber)
- [`expect.hasAssertions()`](https://www.jestjs.cn/docs/expect#expecthasassertions)
- [`expect.not.arrayContaining(array)`](https://www.jestjs.cn/docs/expect#expectnotarraycontainingarray)
- [`expect.not.objectContaining(object)`](https://www.jestjs.cn/docs/expect#expectnotobjectcontainingobject)
- [`expect.not.stringContaining(string)`](https://www.jestjs.cn/docs/expect#expectnotstringcontainingstring)
- [`expect.not.stringMatching(string | regexp)`](https://www.jestjs.cn/docs/expect#expectnotstringmatchingstring--regexp)
- [`expect.objectContaining(object)`](https://www.jestjs.cn/docs/expect#expectobjectcontainingobject)
- [`expect.stringContaining(string)`](https://www.jestjs.cn/docs/expect#expectstringcontainingstring)
- [`expect.stringMatching(string | regexp)`](https://www.jestjs.cn/docs/expect#expectstringmatchingstring--regexp)
- [`expect.addSnapshotSerializer(serializer)`](https://www.jestjs.cn/docs/expect#expectaddsnapshotserializerserializer)
- [`.not`](https://www.jestjs.cn/docs/expect#not)
- [`.resolves`](https://www.jestjs.cn/docs/expect#resolves)
- [`.rejects`](https://www.jestjs.cn/docs/expect#rejects)
- [`.toBe(value)`](https://www.jestjs.cn/docs/expect#tobevalue)
- [`.toHaveBeenCalled()`](https://www.jestjs.cn/docs/expect#tohavebeencalled)
- [`.toHaveBeenCalledTimes(number)`](https://www.jestjs.cn/docs/expect#tohavebeencalledtimesnumber)
- [`.toHaveBeenCalledWith(arg1, arg2, ...)`](https://www.jestjs.cn/docs/expect#tohavebeencalledwitharg1-arg2-)
- [`.toHaveBeenLastCalledWith(arg1, arg2, ...)`](https://www.jestjs.cn/docs/expect#tohavebeenlastcalledwitharg1-arg2-)
- [`.toHaveBeenNthCalledWith(nthCall, arg1, arg2, ....)`](https://www.jestjs.cn/docs/expect#tohavebeennthcalledwithnthcall-arg1-arg2-)
- [`.toHaveReturned()`](https://www.jestjs.cn/docs/expect#tohavereturned)
- [`.toHaveReturnedTimes(number)`](https://www.jestjs.cn/docs/expect#tohavereturnedtimesnumber)
- [`.toHaveReturnedWith(value)`](https://www.jestjs.cn/docs/expect#tohavereturnedwithvalue)
- [`.toHaveLastReturnedWith(value)`](https://www.jestjs.cn/docs/expect#tohavelastreturnedwithvalue)
- [`.toHaveNthReturnedWith(nthCall, value)`](https://www.jestjs.cn/docs/expect#tohaventhreturnedwithnthcall-value)
- [`.toHaveLength(number)`](https://www.jestjs.cn/docs/expect#tohavelengthnumber)
- [`.toHaveProperty(keyPath, value?)`](https://www.jestjs.cn/docs/expect#tohavepropertykeypath-value)
- [`.toBeCloseTo(number, numDigits?)`](https://www.jestjs.cn/docs/expect#tobeclosetonumber-numdigits)
- [`.toBeDefined()`](https://www.jestjs.cn/docs/expect#tobedefined)
- [`.toBeFalsy()`](https://www.jestjs.cn/docs/expect#tobefalsy)
- [`.toBeGreaterThan(number | bigint)`](https://www.jestjs.cn/docs/expect#tobegreaterthannumber--bigint)
- [`.toBeGreaterThanOrEqual(number | bigint)`](https://www.jestjs.cn/docs/expect#tobegreaterthanorequalnumber--bigint)
- [`.toBeLessThan(number | bigint)`](https://www.jestjs.cn/docs/expect#tobelessthannumber--bigint)
- [`.toBeLessThanOrEqual(number | bigint)`](https://www.jestjs.cn/docs/expect#tobelessthanorequalnumber--bigint)
- [`.toBeInstanceOf(Class)`](https://www.jestjs.cn/docs/expect#tobeinstanceofclass)
- [`.toBeNull()`](https://www.jestjs.cn/docs/expect#tobenull)
- [`.toBeTruthy()`](https://www.jestjs.cn/docs/expect#tobetruthy)
- [`.toBeUndefined()`](https://www.jestjs.cn/docs/expect#tobeundefined)
- [`.toBeNaN()`](https://www.jestjs.cn/docs/expect#tobenan)
- [`.toContain(item)`](https://www.jestjs.cn/docs/expect#tocontainitem)
- [`.toContainEqual(item)`](https://www.jestjs.cn/docs/expect#tocontainequalitem)
- [`.toEqual(value)`](https://www.jestjs.cn/docs/expect#toequalvalue)
- [`.toMatch(regexp | string)`](https://www.jestjs.cn/docs/expect#tomatchregexp--string)
- [`.toMatchObject(object)`](https://www.jestjs.cn/docs/expect#tomatchobjectobject)
- [`.toMatchSnapshot(propertyMatchers?, hint?)`](https://www.jestjs.cn/docs/expect#tomatchsnapshotpropertymatchers-hint)
- [`.toMatchInlineSnapshot(propertyMatchers?, inlineSnapshot)`](https://www.jestjs.cn/docs/expect#tomatchinlinesnapshotpropertymatchers-inlinesnapshot)
- [`.toStrictEqual(value)`](https://www.jestjs.cn/docs/expect#tostrictequalvalue)
- [`.toThrow(error?)`](https://www.jestjs.cn/docs/expect#tothrowerror)
- [`.toThrowErrorMatchingSnapshot(hint?)`](https://www.jestjs.cn/docs/expect#tothrowerrormatchingsnapshothint)
- [`.toThrowErrorMatchingInlineSnapshot(inlineSnapshot)`](https://www.jestjs.cn/docs/expect#tothrowerrormatchinginlinesnapshotinlinesnapshot)



## 参考信息



### `expect(value)`

每次要测试值时，都会使用 expect 函数。你很少会自己回调 expect 。相反，您将使用 expect 和 "matcher" 函数来断言有关值的一些东西。

用一个例子来理解这一点更容易。假设您有一个方法 bestLaCroixFlavor()，它应该返回字符串  'grapefruit' 。以下是您如何测试它：

```
test('the best flavor is grapefruit', () => {
  expect(bestLaCroixFlavor()).toBe('grapefruit');
});
```

在这种情况下，toBe 是匹配器函数。有很多不同的匹配器函数，记录在下面，以帮助您测试不同的东西。

expect 的参数应该是代码生成的值，匹配器的任何参数都应该是正确的值。如果你把它们混在一起，你的测试仍然可以工作，但失败测试的错误消息看起来会很奇怪。



### `expect.extend(matchers)`

您可以使用 expect.extend 将自己的匹配器添加到 Jest 中。例如，假设您正在测试一个数字实用程序库，并且您经常断言数字出现在其他数字的特定范围内。您可以将其抽象为 toBeWinRange 匹配器：

```
expect.extend({
  toBeWithinRange(received, floor, ceiling) {
    const pass = received >= floor && received <= ceiling;
    if (pass) {
      return {
        message: () =>
          `expected ${received} not to be within range ${floor} - ${ceiling}`,
        pass: true,
      };
    } else {
      return {
        message: () =>
          `expected ${received} to be within range ${floor} - ${ceiling}`,
        pass: false,
      };
    }
  },
});

test('numeric ranges', () => {
  expect(100).toBeWithinRange(90, 110);
  expect(101).not.toBeWithinRange(0, 100);
  expect({apples: 6, bananas: 3}).toEqual({
    apples: expect.toBeWithinRange(1, 10),
    bananas: expect.not.toBeWithinRange(11, 20),
  });
});
```

注意：在TypeScript中，例如使用 @types/jest 时，您可以在导入的模块中声明新的 toBeWithinRange 匹配器，如下所示：

```
declare global {
  namespace jest {
    interface Matchers<R> {
      toBeWithinRange(a: number, b: number): R;
    }
  }
}
```

#### 异步匹配程序

expect.extend 还支持异步匹配器。异步匹配器返回一个承诺，因此您需要等待返回值。让我们使用一个示例匹配器来说明它们的用法。我们将实现一个名为 toBeDiableByExtValue 的匹配器，其中可整除数将从外部源提取。

```
expect.extend({
  async toBeDivisibleByExternalValue(received) {
    const externalValue = await getExternalValueFromRemoteSource();
    const pass = received % externalValue == 0;
    if (pass) {
      return {
        message: () =>
          `expected ${received} not to be divisible by ${externalValue}`,
        pass: true,
      };
    } else {
      return {
        message: () =>
          `expected ${received} to be divisible by ${externalValue}`,
        pass: false,
      };
    }
  },
});

test('is divisible by external value', async () => {
  await expect(100).toBeDivisibleByExternalValue();
  await expect(101).not.toBeDivisibleByExternalValue();
});
```

#### 自定义匹配程序API

匹配器应返回带有两个键的对象（或是包含一个Promise的对象）。pass 指示是否存在匹配，message 提供了一个没有参数的函数，在失败时返回错误消息。因此，当pass为false时，消息应返回 expect(x).yourMatcher() 失败时的错误消息。当pass为true时，当expect(x).not.yourMatcher() 失败时，消息应返回错误消息。

调用匹配器的参数传递给 expect(x)，然后传递给 .youMatcher(y,z) 的参数：

```
expect.extend({
  yourMatcher(x, y, z) {
    return {
      pass: true,
      message: () => '',
    };
  },
});
```

这些帮助程序函数和属性可以在自定义匹配程序中找到：

##### `this.isNot`

一个布尔值，让您知道此匹配器是用否定的.not修饰符调用的，允许您显示清晰正确的匹配器提示（请参见示例代码）。

##### `this.promise`

允许您显示清晰正确的匹配器提示的字符串：

- 'rejects' -----如果使用promise .rejects修饰符调用了匹配程序
- 'resolves'----如果使用promise .resolves修饰符调用了匹配程序
- ''----------------如果没有使用promise修饰符调用匹配程序

##### `this.equals(a, b)`

这是一个深度等式函数，如果两个对象具有相同的值（递归），它将返回true。

##### `this.expand`

一个布尔值，让您知道此匹配器是用扩展选项调用的。当使用--expand标志调用Jest时，this.expand 可用于确定 Jest 是否应显示完整的差异和错误。

##### `this.utils`

在 this.utils 上公开了许多有用的工具，主要包括  [`jest-matcher-utils`](https://github.com/facebook/jest/tree/master/packages/jest-matcher-utils) 的导出。

最有用的是 matcherHint`, `printExpected ` 和 ` printReceived，以很好地格式化错误消息。例如，查看 toBe 匹配器的实现：

```
const diff = require('jest-diff');
expect.extend({
  toBe(received, expected) {
    const options = {
      comment: 'Object.is equality',
      isNot: this.isNot,
      promise: this.promise,
    };

    const pass = Object.is(received, expected);

    const message = pass
      ? () =>
          this.utils.matcherHint('toBe', undefined, undefined, options) +
          '\n\n' +
          `Expected: not ${this.utils.printExpected(expected)}\n` +
          `Received: ${this.utils.printReceived(received)}`
      : () => {
          const diffString = diff(expected, received, {
            expand: this.expand,
          });
          return (
            this.utils.matcherHint('toBe', undefined, undefined, options) +
            '\n\n' +
            (diffString && diffString.includes('- Expect')
              ? `Difference:\n\n${diffString}`
              : `Expected: ${this.utils.printExpected(expected)}\n` +
                `Received: ${this.utils.printReceived(received)}`)
          );
        };

    return {actual: received, message, pass};
  },
});
```

这将打印类似这样的东西：

```
  expect(received).toBe(expected)

    Expected value to be (using Object.is):
      "banana"
    Received:
      "apple"
```

当断言失败时，错误消息应向用户提供必要的信号，以便他们能够快速解决问题。您应该精心制作一个精确的失败消息，以确保自定义断言的用户有良好的开发人员体验。

#### 自定义快照匹配程序

要在自定义匹配器内使用快照测试，您可以导入 jest-snapshot 并从匹配器内使用它。

这里有一个快照匹配器，它修剪要存储给定长度的字符串，.toMatchTrimmedSnapshot(length)：

```
const {toMatchSnapshot} = require('jest-snapshot');

expect.extend({
  toMatchTrimmedSnapshot(received, length) {
    return toMatchSnapshot.call(
      this,
      received.substring(0, length),
      'toMatchTrimmedSnapshot',
    );
  },
});

it('stores only 10 characters', () => {
  expect('extra long string oh my gerd').toMatchTrimmedSnapshot(10);
});

/*
Stored snapshot will look like:

exports[`stores only 10 characters: toMatchTrimmedSnapshot 1`] = `"extra long"`;
*/
```

还可以为内联快照创建自定义匹配器，快照将正确添加到自定义匹配器。但是，当第一个参数是属性匹配器时，内联快照将始终尝试附加到第一个参数或第二个参数，因此不可能在自定义匹配器中接受自定义参数。

```
const {toMatchInlineSnapshot} = require('jest-snapshot');

expect.extend({
  toMatchTrimmedInlineSnapshot(received, ...rest) {
    return toMatchInlineSnapshot.call(this, received.substring(0, 10), ...rest);
  },
});

it('stores only 10 characters', () => {
  expect('extra long string oh my gerd').toMatchTrimmedInlineSnapshot();
  /*
  The snapshot will be added inline like
  expect('extra long string oh my gerd').toMatchTrimmedInlineSnapshot(
    `"extra long"`
  );
  */
});
```

#### 异步

如果您的自定义内联快照匹配程序是异步的，即使用 async-await，您可能会遇到类似“不支持同一调用的多个内联快照”的错误。Jest 需要其他上下文信息来查找自定义内联快照匹配器用于正确更新快照的位置。

```
const {toMatchInlineSnapshot} = require('jest-snapshot');

expect.extend({
  async toMatchObservationInlineSnapshot(fn, ...rest) {
    // The error (and its stacktrace) must be created before any `await`
    this.error = new Error();

    // The implementation of `observe` doesn't matter.
    // It only matters that the custom snapshot matcher is async.
    const observation = await observe(async () => {
      await fn();
    });

    return toMatchInlineSnapshot.call(this, recording, ...rest);
  },
});

it('observes something', async () => {
  await expect(async () => {
    return 'async action';
  }).toMatchTrimmedInlineSnapshot();
  /*
  The snapshot will be added inline like
  await expect(async () => {
    return 'async action';
  }).toMatchTrimmedInlineSnapshot(`"async action"`);
  */
});
```



### `expect.anything()`

expect.anything() 匹配除 null` or `undefined 外的任何内容。您可以在 toEqual 或 toBeCalledWith 内部使用它，而不是文字值。例如，如果要检查模拟函数是否使用非空参数调用：

```
test('map calls its argument with a non-null argument', () => {
  const mock = jest.fn();
  [1].map(x => mock(x));
  expect(mock).toBeCalledWith(expect.anything());
});
```



### `expect.any(constructor)`

expect.any(constructor) 匹配使用给定构造函数创建的任何内容。您可以在 toEqual 或 toBeCalledWith 内部使用它，而不是文字值。例如，如果要检查模拟函数是否使用数字调用：

```
function randocall(fn) {
  return fn(Math.floor(Math.random() * 6 + 1));
}

test('randocall calls its callback with a number', () => {
  const mock = jest.fn();
  randocall(mock);
  expect(mock).toBeCalledWith(expect.any(Number));
});
```



### `expect.arrayContaining(array)`

expect.arrayContaining(array) 匹配接收到的数组，该数组包含预期数组中的所有元素。也就是说，预期数组是接收数组的子集。因此，它匹配接收到的数组，该数组包含不在预期数组中的元素。

您可以使用它而不是文字值：

- 在 toEqual 或 toBeCalledWith 中
- 匹配 objectContain 或 toMatchObject 中的属性

```
describe('arrayContaining', () => {
  const expected = ['Alice', 'Bob'];
  it('matches even if received contains additional elements', () => {
    expect(['Alice', 'Bob', 'Eve']).toEqual(expect.arrayContaining(expected));
  });
  it('does not match if received does not contain expected elements', () => {
    expect(['Bob', 'Eve']).not.toEqual(expect.arrayContaining(expected));
  });
});
```

```
describe('Beware of a misunderstanding! A sequence of dice rolls', () => {
  const expected = [1, 2, 3, 4, 5, 6];
  it('matches even with an unexpected number 7', () => {
    expect([4, 1, 6, 7, 3, 5, 2, 5, 4, 6]).toEqual(
      expect.arrayContaining(expected),
    );
  });
  it('does not match without an expected number 2', () => {
    expect([4, 1, 6, 7, 3, 5, 7, 5, 4, 6]).not.toEqual(
      expect.arrayContaining(expected),
    );
  });
});
```



### `expect.assertions(number)`

expect.assertions(number) 验证在测试期间是否调用了一定数量的断言。这在测试异步代码时通常很有用，以确保回调中的断言实际上被调用。

例如，假设我们有一个函数doAsync，它接收两个回调callback1和callback2，它将以未知的顺序异步调用这两个回调。我们可以使用：

```
test('doAsync calls both callbacks', () => {
  expect.assertions(2);
  function callback1(data) {
    expect(data).toBeTruthy();
  }
  function callback2(data) {
    expect(data).toBeTruthy();
  }

  doAsync(callback1, callback2);
});
```

expect.assertions(2) 调用确保两个回调实际上都被调用。



### `expect.hasAssertions()`

expect.hasAssertions() 验证在测试期间是否至少调用了一个断言。这在测试异步代码时通常很有用，以确保回调中的断言实际上被调用。

例如，假设我们有几个函数都处理状态。prepareState 使用状态对象调用回调，validateState 在该状态对象上运行，waitOnState 返回一个承诺，等待所有 prepareState 回调完成。我们可以使用：

```
test('prepareState prepares a valid state', () => {
  expect.hasAssertions();
  prepareState(state => {
    expect(validateState(state)).toBeTruthy();
  });
  return waitOnState();
});
```

expect.hasAssertions() 调用确保实际调用了 prepareState 回调。



### `expect.not.arrayContaining(array)`

expect.not.arrayContaining(array) 匹配接收到的数组，该数组不包含预期数组中的所有元素。也就是说，预期数组不是接收数组的子集。

它是 `expect.arrayContaining` 的逆序。

```
describe('not.arrayContaining', () => {
  const expected = ['Samantha'];

  it('matches if the actual array does not contain the expected elements', () => {
    expect(['Alice', 'Bob', 'Eve']).toEqual(
      expect.not.arrayContaining(expected),
    );
  });
});
```



### `expect.not.objectContaining(object)`

expect.not.objectContaining(object) 匹配任何与预期属性不递归匹配的接收对象。也就是说，预期对象不是接收对象的子集。因此，它匹配接收到的对象，该对象包含不在预期对象中的属性。

它是 expect.objectContaining 的反面。

```
describe('not.objectContaining', () => {
  const expected = {foo: 'bar'};

  it('matches if the actual object does not contain expected key: value pairs', () => {
    expect({bar: 'baz'}).toEqual(expect.not.objectContaining(expected));
  });
});
```



### `expect.not.stringContaining(string)`

如果接收到的值不是字符串或不包含确切预期字符串的字符串，则 expect.not.stringContaining(string) 与接收到的值匹配。

它是 expect.stringContaining 的逆序。

```
describe('not.stringContaining', () => {
  const expected = 'Hello world!';

  it('matches if the received value does not contain the expected substring', () => {
    expect('How are you?').toEqual(expect.not.stringContaining(expected));
  });
});
```



### `expect.not.stringMatching(string | regexp)`

如果接收到的值不是字符串，或者是与预期字符串或正则表达式不匹配的字符串，则 expect.not.stringMatching(string | regexp) 将与接收到的值匹配。

它是  expect.stringMatching 的反面。

```
describe('not.stringMatching', () => {
  const expected = /Hello world!/;

  it('matches if the received value does not match the expected regex', () => {
    expect('How are you?').toEqual(expect.not.stringMatching(expected));
  });
});
```



### `expect.objectContaining(object)`

expect.objectContaining(object) 匹配递归匹配预期属性的任何接收到的对象。也就是说，预期对象是接收对象的子集。因此，它匹配接收到的对象，该对象包含预期对象中存在的属性。

您可以使用匹配器、expect.anything() 等，而不是预期对象中的文字属性值。

例如，假设我们希望使用 Event对象 调用 onPress 函数，我们只需要验证事件是否具有event.x和event.y属性。我们可以通过：

```
test('onPress gets called with the right thing', () => {
  const onPress = jest.fn();
  simulatePresses(onPress);
  expect(onPress).toBeCalledWith(
    expect.objectContaining({
      x: expect.any(Number),
      y: expect.any(Number),
    }),
  );
});
```



### `expect.stringContaining(string)`

如果接收到的值包含确切的预期字符串，则 expect.stringContaining(string) 与接收到的值匹配。



### `expect.stringMatching(string | regexp)`

如果接收到的值是与预期字符串或正则表达式匹配的字符串，则 expect.stringMatching(string | regexp) 将与接收到的值匹配。

您可以使用它而不是文字值：

- 在toEqual或toBeCalledWith中
- 匹配arrayContain中的元素
- 匹配objectContain或toMatchObject中的属性

此示例还展示了如何嵌套多个非对称匹配器，在 expect.arrayContaining 中使用 expect.stringMatching。

```
describe('stringMatching in arrayContaining', () => {
  const expected = [
    expect.stringMatching(/^Alic/),
    expect.stringMatching(/^[BR]ob/),
  ];
  it('matches even if received contains additional elements', () => {
    expect(['Alicia', 'Roberto', 'Evelina']).toEqual(
      expect.arrayContaining(expected),
    );
  });
  it('does not match if received does not contain expected elements', () => {
    expect(['Roberto', 'Evelina']).not.toEqual(
      expect.arrayContaining(expected),
    );
  });
});
```



### `expect.addSnapshotSerializer(serializer)`

您可以调用 expect.addSnapshotSerializer 来添加格式化应用程序特定数据结构的模块。

对于单个测试文件，添加的模块位于 snapshotSerializers 配置中的任何模块之前，这些模块位于内置JavaScript类型和React元素的默认快照序列化器之前。最后添加的模块是测试的第一个模块。

```
import serializer from 'my-serializer-module';
expect.addSnapshotSerializer(serializer);

// affects expect(value).toMatchSnapshot() assertions in the test file
```

如果您在单个测试文件中添加快照序列化程序，而不是将其添加到快照序列化程序配置中：

- 你可以使依赖项显式而不是隐式。
- 你可以避免可能导致您从create-react-app中弹出的配置限制。

有关详细信息，请参见 [configuring Jest](https://www.jestjs.cn/docs/configuration#snapshotserializers-arraystring)。



### `.not`

如果你知道如何测试某件事情，.not 你测试它的相反。例如，此代码测试 the best La Croix flavor is not coconut:

```
test('the best flavor is not coconut', () => {
  expect(bestLaCroixFlavor()).not.toBe('coconut');
});
```



### `.resolves`

使用 resolves 解包已实现的承诺的值，以便可以链接任何其他匹配器。如果承诺被拒绝，则断言将失败。

例如，此代码测试承诺是否解析，并且结果值是否为  'lemon' ：

```
test('resolves to lemon', () => {
  // make sure to add a return statement
  return expect(Promise.resolve('lemon')).resolves.toBe('lemon');
});
```

请注意，由于您仍在测试承诺，因此测试仍然是异步的。因此，您需要通过返回未包装的断言来告诉Jest等待。

或者，您可以将 async/await 与 .resolves 结合使用：

```
test('resolves to lemon', async () => {
  await expect(Promise.resolve('lemon')).resolves.toBe('lemon');
  await expect(Promise.resolve('lemon')).resolves.not.toBe('octopus');
});
```



### `.rejects`

使用 .rejects 打开被拒绝承诺的原因，以便可以链接任何其他匹配器。如果承诺已实现，则断言将失败。

例如，此代码测试承诺是否以 'octopus' 原因拒绝：

```
test('rejects to octopus', () => {
  // make sure to add a return statement
  return expect(Promise.reject(new Error('octopus'))).rejects.toThrow(
    'octopus',
  );
});
```

请注意，由于您仍在测试承诺，因此测试仍然是异步的。因此，您需要通过返回未包装的断言来告诉Jest等待。

或者，您可以将async/await与.rejects结合使用。

```
test('rejects to octopus', async () => {
  await expect(Promise.reject(new Error('octopus'))).rejects.toThrow('octopus');
});
```



### `.toBe(value)`

使用 .toBe 比较基元值或检查对象实例的引用标识。它调用 Object.is 来比较值，这比===严格相等运算符更适合测试。

例如，此代码将验证can对象的某些属性：

```
const can = {
  name: 'pamplemousse',
  ounces: 12,
};

describe('the can', () => {
  test('has 12 ounces', () => {
    expect(can.ounces).toBe(12);
  });

  test('has a sophisticated name', () => {
    expect(can.name).toBe('pamplemousse');
  });
});
```

不要将 .toBe 与浮点数一起使用。例如，由于四舍五入，在JavaScript 0.2 + 0.1中严格不等于0.3。如果您有浮点数，请尝试 .toBeCloseTo 。

虽然.toBe匹配器检查引用标识，但如果断言失败，它将报告值的深度比较。如果属性之间的差异不能帮助您理解测试失败的原因，特别是如果报表很大，则您可以将比较移动到预期函数中。例如，要断言元素是否为同一实例：

- rewrite `expect(received).toBe(expected)` as `expect(Object.is(received, expected)).toBe(true)`
- rewrite `expect(received).not.toBe(expected)` as `expect(Object.is(received, expected)).toBe(false)`



### `.toHaveBeenCalled()`

也在别名下：.toBeCalled()

使用 .toHaveBeenCalled 确保调用了模拟函数。

例如，假设您有一个 drinkAll(drink, flavour) 方法，它采取 drink 方法，并将其应用于所有可用的饮料。你可能想看看 drink 是 'lemon' 的，但不是 'octopus' 的，因为 'octopus' 的味道真的很奇怪，为什么任何东西都会有章鱼的味道？您可以使用此测试套件执行此操作：

```
function drinkAll(callback, flavour) {
  if (flavour !== 'octopus') {
    callback(flavour);
  }
}

describe('drinkAll', () => {
  test('drinks something lemon-flavoured', () => {
    const drink = jest.fn();
    drinkAll(drink, 'lemon');
    expect(drink).toHaveBeenCalled();
  });

  test('does not drink something octopus-flavoured', () => {
    const drink = jest.fn();
    drinkAll(drink, 'octopus');
    expect(drink).not.toHaveBeenCalled();
  });
});
```



### `.toHaveBeenCalledTimes(number)`

也在别名下：.toBeCalledTimes(number)

使用 .toHaveBeenCalledTimes 确保模拟函数被调用的确切次数。

例如，假设您有一个 drinkEach(drink, Array<flavor>) 函数，该函数采用 drink 函数并将其应用于传递的饮料数组。您可能需要检查饮料函数被调用的确切次数。您可以使用此测试套件执行此操作：

```
test('drinkEach drinks each drink', () => {
  const drink = jest.fn();
  drinkEach(drink, ['lemon', 'octopus']);
  expect(drink).toHaveBeenCalledTimes(2);
});
```



### `.toHaveBeenCalledWith(arg1, arg2, ...)`

也在别名下：.toBeCalledWith()

使用.toHaveBeenCalledWith 确保使用特定参数调用模拟函数。

例如，假设您可以使用 register 函数注册饮料，并且 applyToAll(f) 应将函数f应用于所有注册的饮料。为了确保这有效，你可以写：

```
test('registration applies correctly to orange La Croix', () => {
  const beverage = new LaCroix('orange');
  register(beverage);
  const f = jest.fn();
  applyToAll(f);
  expect(f).toHaveBeenCalledWith(beverage);
});
```



### `.toHaveBeenLastCalledWith(arg1, arg2, ...)`

也在别名下：.lastCalledWith(arg1, arg2, ...)

如果您有一个模拟函数，您可以使用 .toHaveBeenLastCalledWith 来测试它上次调用的参数。例如，假设您有一个 applyToAllFlavors(f)函数，该函数将f应用到一堆口味，您希望确保当您调用它时，它运行的最后一个口味是  'mango' 。您可以写：

```
test('applying to all flavors does mango last', () => {
  const drink = jest.fn();
  applyToAllFlavors(drink);
  expect(drink).toHaveBeenLastCalledWith('mango');
});
```



### `.toHaveBeenNthCalledWith(nthCall, arg1, arg2, ....)`

也在别名下：.nthCalledWith(nthCall, arg1, arg2, ...)

如果您有一个模拟函数，您可以使用.toHaveBeenNthCalledWith 来测试它第n次调用的参数。例如，假设您有一个将f应用于一堆口味的drinkEach(drink, Array<flavor>) 函数，并且您希望确保当您调用它时，它的第一种口味是 'lemon'，第二种口味是 'octopus'。您可以写：

```
test('drinkEach drinks each drink', () => {
  const drink = jest.fn();
  drinkEach(drink, ['lemon', 'octopus']);
  expect(drink).toHaveBeenNthCalledWith(1, 'lemon');
  expect(drink).toHaveBeenNthCalledWith(2, 'octopus');
});
```

注意：第n个参数必须是从1开始的正整数。



### `.toHaveReturned()`

也在别名下：.toReturn()

如果您有一个模拟函数，您可以使用.toHaveReturned 测试模拟函数是否成功返回（即，没有抛出错误）至少一次。例如，假设您有一个返回true的模拟 drink 。您可以写：

```
test('drinks returns', () => {
  const drink = jest.fn(() => true);

  drink();

  expect(drink).toHaveReturned();
});
```



### `.toHaveReturnedTimes(number)`

也在别名下：.toReturnTimes(number) 

使用.toHaveReturnedTimes 来确保模拟函数成功返回（即，没有抛出错误）准确的次数。对模拟函数的任何调用都不会计入函数返回的次数。

例如，假设您有一个返回true的模拟 drink。您可以写：

```
test('drink returns twice', () => {
  const drink = jest.fn(() => true);

  drink();
  drink();

  expect(drink).toHaveReturnedTimes(2);
});
```
