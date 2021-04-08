# API-Mock Functions

模拟函数也被称为“监视者”，因为它们允许您监视由其他代码间接调用的函数的行为，而不仅仅是测试输出。您可以使用 jest.fn() 创建模拟函数。如果没有给出实现，则调用模拟函数时将返回undefined。

## Methods[#](https://www.jestjs.cn/docs/mock-function-api#methods)

- Reference
  - [`mockFn.getMockName()`](https://www.jestjs.cn/docs/mock-function-api#mockfngetmockname)
  - [`mockFn.mock.calls`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockcalls)
  - [`mockFn.mock.results`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockresults)
  - [`mockFn.mock.instances`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockinstances)
  - [`mockFn.mockClear()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockclear)
  - [`mockFn.mockReset()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreset)
  - [`mockFn.mockRestore()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrestore)
  - [`mockFn.mockImplementation(fn)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockimplementationfn)
  - [`mockFn.mockImplementationOnce(fn)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockimplementationoncefn)
  - [`mockFn.mockName(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmocknamevalue)
  - [`mockFn.mockReturnThis()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreturnthis)
  - [`mockFn.mockReturnValue(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreturnvaluevalue)
  - [`mockFn.mockReturnValueOnce(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreturnvalueoncevalue)
  - [`mockFn.mockResolvedValue(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockresolvedvaluevalue)
  - [`mockFn.mockResolvedValueOnce(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockresolvedvalueoncevalue)
  - [`mockFn.mockRejectedValue(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrejectedvaluevalue)
  - [`mockFn.mockRejectedValueOnce(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrejectedvalueoncevalue)
- TypeScript
  - [`jest.MockedFunction`](https://www.jestjs.cn/docs/mock-function-api#jestmockedfunction)
  - [`jest.MockedClass`](https://www.jestjs.cn/docs/mock-function-api#jestmockedclass)



## 参考信息

### [`mockFn.getMockName()`](https://www.jestjs.cn/docs/mock-function-api#mockfngetmockname)

返回回调 mockFn.mockName(value) 设置的模拟名称字符串



### [`mockFn.mock.calls`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockcalls)

包含已对此模拟函数进行的所有调用的调用参数的数组。数组中的每个项都是调用期间传递的参数数组。

例如：已调用两次的模拟函数f，使用参数 f（'arg1'，'arg2'），然后使用参数 f（'arg3'，'arg4'），将有一个看起来如下的 mock.calls 数组：

```
[
  ['arg1', 'arg2'],
  ['arg3', 'arg4'],
];
```



### [`mockFn.mock.results`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockresults)

一个数组，包含对此模拟函数进行的所有调用的结果。此数组中的每个条目都是包含 type 属性的对象，value 属性。type 将是以下之一：

- `'return'` - 指示调用通过正常返回完成。

- `'throw'` - 指示通过抛出值完成调用。

- `'incomplete'` - 表示调用尚未完成。如果您从模拟函数本身中测试结果，或从模拟调用的函数中测试结果，则会发生这种情况。

value属性的值 包含 thrown 或 returned。当 type === 'incomplete' 时，value为 undefined 。

例如：已调用三次的模拟函数 f，返回 'result1'，抛出错误，然后返回 'result2'，将具有一个看起来如下的 mock.results：

```
[
  {
    type: 'return',
    value: 'result1',
  },
  {
    type: 'throw',
    value: {
      /* Error instance */
    },
  },
  {
    type: 'return',
    value: 'result2',
  },
];
```



### [`mockFn.mock.instances`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockinstances)

包含使用 new 从此模拟函数实例化的所有对象实例的数组。

例如：实例化两次的模拟函数将具有以下 mock.instances 数组：

```
const mockFn = jest.fn();

const a = new mockFn();
const b = new mockFn();

mockFn.mock.instances[0] === a; // true
mockFn.mock.instances[1] === b; // true
```



### [`mockFn.mockClear()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockclear)

重置存储在 [`mockFn.mock.calls`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockcalls) 和 [`mockFn.mock.instances`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockinstances)  数组中的所有信息。

当您希望在两个断言之间清理模拟的使用数据时，这通常很有用。

请注意，mockClear 将取代 mockFn.mock，而不仅仅是 [`mockFn.mock.calls`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockcalls) 和 [`mockFn.mock.instances`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockinstances) 。因此，您应该避免将mockFn.mock 分配给其他变量，不管是临时的还是非临时的，以确保您不会访问过时的数据。

[`clearMocks`](https://www.jestjs.cn/docs/configuration#clearmocks-boolean) 配置选项可用于在测试之间自动清除模拟。



### [`mockFn.mockReset()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreset)

执行 [`mockFn.mockClear()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockclear) 所做的一切，并删除任何模拟的返回值或实现。

当您希望将模拟完全重置为其初始状态时，这非常有用。（请注意，重置间谍将导致没有返回值的函数）。

请注意，mockReset 将取代 mockFn.mock，而不仅仅是 [`mockFn.mock.calls`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockcalls) 和 [`mockFn.mock.instances`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockinstances)。因此，您应该避免将  mockFn.mock分配给其他变量，不管是临时的还是非临时的，以确保您不会访问过时的数据。



### [`mockFn.mockRestore()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrestore)

执行 [`mockFn.mockReset()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreset) 所做的一切，并恢复原始（非模拟）实现。

当您希望模拟某些测试用例中的函数并恢复其他测试用例中的原始实现时，这非常有用。

请注意，只有在使用 jest.spyOn 创建模拟时，mockFn.mockRestore 才有效。因此，在手动分配 jest.fn() 时，您必须自己处理恢复。

[`restoreMocks`](https://www.jestjs.cn/docs/configuration#restoremocks-boolean)  配置选项可用于在测试之间自动恢复模拟。



### [`mockFn.mockImplementation(fn)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockimplementationfn)

接受应用作模拟实现的函数。模拟本身仍将记录所有进入的调用和来自自身的实例——唯一的区别是，在调用模拟时，实现也将执行。

注：*`jest.fn(implementation)`* 是 *`jest.fn().mockImplementation(implementation)`* 的缩写。

例如：

```
const mockFn = jest.fn().mockImplementation(scalar => 42 + scalar);
// or: jest.fn(scalar => 42 + scalar);

const a = mockFn(0);
const b = mockFn(1);

a === 42; // true
b === 43; // true

mockFn.mock.calls[0][0] === 0; // true
mockFn.mock.calls[1][0] === 1; // true
```

mockImplementation 也可以用于模拟类构造函数：

```
// SomeClass.js
module.exports = class SomeClass {
  m(a, b) {}
};

// OtherModule.test.js
jest.mock('./SomeClass'); // this happens automatically with automocking
const SomeClass = require('./SomeClass');
const mMock = jest.fn();
SomeClass.mockImplementation(() => {
  return {
    m: mMock,
  };
});

const some = new SomeClass();
some.m('a', 'b');
console.log('Calls to m: ', mMock.mock.calls);
```



### [`mockFn.mockImplementationOnce(fn)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockimplementationoncefn)

接受一个函数，该函数将用作对模拟函数的一次调用的模拟实现。可以链接，以便多个函数调用产生不同的结果。

```
const myMockFn = jest
  .fn()
  .mockImplementationOnce(cb => cb(null, true))
  .mockImplementationOnce(cb => cb(null, false));

myMockFn((err, val) => console.log(val)); // true

myMockFn((err, val) => console.log(val)); // false
```

当模拟函数用完了用模拟实现Once定义的实现时，如果调用了 `jest.fn(() => defaultValue)` 或 .mockImplementation(() => defaultValue)，它将执行默认实现集：

```
const myMockFn = jest
  .fn(() => 'default')
  .mockImplementationOnce(() => 'first call')
  .mockImplementationOnce(() => 'second call');

// 'first call', 'second call', 'default', 'default'
console.log(myMockFn(), myMockFn(), myMockFn(), myMockFn());
```



### [`mockFn.mockName(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmocknamevalue)

接受一个字符串，以代替 “jest.fn()” 在测试结果输出中使用，以指示引用的是哪个模拟函数。

例如：

```
const mockFn = jest.fn().mockName('mockedFunction');
// mockFn();
expect(mockFn).toHaveBeenCalled();
```

将导致此错误：

```
expect(mockedFunction).toHaveBeenCalled()

Expected mock function "mockedFunction" to have been called, but it was not called.
```



### [`mockFn.mockReturnThis()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreturnthis)

语法糖函数：

```
jest.fn(function () {
  return this;
});
```



### [`mockFn.mockReturnValue(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreturnvaluevalue)

接受每当调用模拟函数时将返回的值。

```
const mock = jest.fn();
mock.mockReturnValue(42);
mock(); // 42
mock.mockReturnValue(43);
mock(); // 43
```



### [`mockFn.mockReturnValueOnce(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreturnvalueoncevalue)

接受对模拟函数的一次调用将返回的值。可以链接，以便对模拟函数的连续调用返回不同的值。当没有更多的 mockReturnValueOnce 值可使用时，调用将返回由 mockReturnValue 指定的值。

```
const myMockFn = jest
  .fn()
  .mockReturnValue('default')
  .mockReturnValueOnce('first call')
  .mockReturnValueOnce('second call');

// 'first call', 'second call', 'default', 'default'
console.log(myMockFn(), myMockFn(), myMockFn(), myMockFn());
```



### [`mockFn.mockResolvedValue(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockresolvedvaluevalue)

语法糖函数：

```
jest.fn().mockImplementation(() => Promise.resolve(value));
```

用于模拟异步测试中的异步函数：

```
test('async test', async () => {
  const asyncMock = jest.fn().mockResolvedValue(43);

  await asyncMock(); // 43
});
```



### [`mockFn.mockResolvedValueOnce(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockresolvedvalueoncevalue)

语法糖函数：

```
jest.fn().mockImplementationOnce(() => Promise.resolve(value));
```

用于解析多个异步调用上的不同值：

```
test('async test', async () => {
  const asyncMock = jest
    .fn()
    .mockResolvedValue('default')
    .mockResolvedValueOnce('first call')
    .mockResolvedValueOnce('second call');

  await asyncMock(); // first call
  await asyncMock(); // second call
  await asyncMock(); // default
  await asyncMock(); // default
});
```



### [`mockFn.mockRejectedValue(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrejectedvaluevalue)

语法糖函数：

```
jest.fn().mockImplementation(() => Promise.reject(value));
```

用于创建始终拒绝的异步模拟函数：

```
test('async test', async () => {
  const asyncMock = jest.fn().mockRejectedValue(new Error('Async error'));

  await asyncMock(); // throws "Async error"
});
```



### [`mockFn.mockRejectedValueOnce(value)`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrejectedvalueoncevalue)

语法糖函数：

```
jest.fn().mockImplementationOnce(() => Promise.reject(value));
```

用法示例：

```
test('async test', async () => {
  const asyncMock = jest
    .fn()
    .mockResolvedValueOnce('first call')
    .mockRejectedValueOnce(new Error('Async error'));

  await asyncMock(); // first call
  await asyncMock(); // throws "Async error"
});
```



## TypeScript

Jest本身是用TypeScript编写的。

如果您使用的是 [Create React App](https://create-react-app.dev/) ，那么 [TypeScript template](https://create-react-app.dev/docs/adding-typescript/)  具有开始在TypeScript中编写测试所需的一切。

否则，请参见我们的  [Getting Started](https://www.jestjs.cn/docs/getting-started#using-typescript) ，了解如何使用TypeScript进行设置。

您可以在我们的  [GitHub repository](https://github.com/facebook/jest/tree/master/examples/typescript) 中看到将Jest与TypeScript一起使用的示例。



### [`jest.MockedFunction`](https://www.jestjs.cn/docs/mock-function-api#jestmockedfunction)

> jest.MockedFunction 可在24.9.0版的 @types/jest 模块中使用。

以下示例将假定您了解  [Jest mock functions work with JavaScript](https://www.jestjs.cn/docs/mock-functions)。

您可以使用 jest.MockedFunction 来表示已被Jest模拟替换的函数。

使用  [automatic `jest.mock`](https://www.jestjs.cn/docs/jest-object#jestmockmodulename-factory-options) 的示例：

```
// Assume `add` is imported and used within `calculate`.
import add from './add';
import calculate from './calc';

jest.mock('./add');

// Our mock of `add` is now fully typed
const mockAdd = add as jest.MockedFunction<typeof add>;

test('calculate calls add', () => {
  calculate('Add', 1, 2);

  expect(mockAdd).toBeCalledTimes(1);
  expect(mockAdd).toBeCalledWith(1, 2);
});
```

使用 [`jest.fn`](https://www.jestjs.cn/docs/jest-object#jestfnimplementation) 的示例：

```
// Here `add` is imported for its type
import add from './add';
import calculate from './calc';

test('calculate calls add', () => {
  // Create a new mock that can be used in place of `add`.
  const mockAdd = jest.fn() as jest.MockedFunction<typeof add>;

  // Note: You can use the `jest.fn` type directly like this if you want:
  // const mockAdd = jest.fn<ReturnType<typeof add>, Parameters<typeof add>>();
  // `jest.MockedFunction` is a more friendly shortcut.

  // Now we can easily set up mock implementations.
  // All the `.mock*` API can now give you proper types for `add`.
  // https://jestjs.io/docs/mock-function-api

  // `.mockImplementation` can now infer that `a` and `b` are `number`
  // and that the returned value is a `number`.
  mockAdd.mockImplementation((a, b) => {
    // Yes, this mock is still adding two numbers but imagine this
    // was a complex function we are mocking.
    return  a + b
  }));

  // `mockAdd` is properly typed and therefore accepted by
  // anything requiring `add`.
  calculate(mockAdd, 1 , 2);

  expect(mockAdd).toBeCalledTimes(1);
  expect(mockAdd).toBeCalledWith(1, 2);
})
```



### [`jest.MockedClass`](https://www.jestjs.cn/docs/mock-function-api#jestmockedclass)

> jest.MockedClass 可在24.9.0版的 @types/jest 模块中使用。

以下示例将假设您了解 [Jest mock classes work with JavaScript](https://www.jestjs.cn/docs/es6-class-mocks)。

您可以使用 jest.MockedClass 来表示已被Jest模拟替换的类。

转换  [ES6 Class automatic mock example](https://www.jestjs.cn/docs/es6-class-mocks#automatic-mock)  如下所示：

```
import SoundPlayer from '../sound-player';
import SoundPlayerConsumer from '../sound-player-consumer';

jest.mock('../sound-player'); // SoundPlayer is now a mock constructor

const SoundPlayerMock = SoundPlayer as jest.MockedClass<typeof SoundPlayer>;

beforeEach(() => {
  // Clear all instances and calls to constructor and all methods:
  SoundPlayerMock.mockClear();
});

it('We can check if the consumer called the class constructor', () => {
  const soundPlayerConsumer = new SoundPlayerConsumer();
  expect(SoundPlayerMock).toHaveBeenCalledTimes(1);
});

it('We can check if the consumer called a method on the class instance', () => {
  // Show that mockClear() is working:
  expect(SoundPlayerMock).not.toHaveBeenCalled();

  const soundPlayerConsumer = new SoundPlayerConsumer();
  // Constructor should have been called again:
  expect(SoundPlayerMock).toHaveBeenCalledTimes(1);

  const coolSoundFileName = 'song.mp3';
  soundPlayerConsumer.playSomethingCool();

  // mock.instances is available with automatic mocks:
  const mockSoundPlayerInstance = SoundPlayerMock.mock.instances[0];

  // However, it will not allow access to `.mock` in TypeScript as it
  // is returning `SoundPlayer`. Instead, you can check the calls to a
  // method like this fully typed:
  expect(SoundPlayerMock.prototype.playSoundFile.mock.calls[0][0]).toEqual(
    coolSoundFileName,
  );
  // Equivalent to above check:
  expect(SoundPlayerMock.prototype.playSoundFile).toHaveBeenCalledWith(
    coolSoundFileName,
  );
  expect(SoundPlayerMock.prototype.playSoundFile).toHaveBeenCalledTimes(1);
});
```

