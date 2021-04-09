# API-The Jest Object

`jest`对象自动在每个测试文件的作用域中。`jest`对象中的方法有助于创建模拟，并允许您控制Jest的整体行为。它也可以通过 import {jest} from '@jest/globals' 显式导入。



## Mock Modules[#](https://www.jestjs.cn/docs/jest-object#mock-modules)

### `jest.disableAutomock()`[#](https://www.jestjs.cn/docs/jest-object#jestdisableautomock)

禁用模块加载器中的自动模拟。

>有关更多信息，请参见[configuration](https://www.jestjs.cn/docs/configuration#automock-boolean) 

调用此方法后，所有`require()`都将返回每个模块的真实版本（而不是模拟版本）。

Jest 配置：

```
{
  "automock": true
}
```

示例：

```
// utils.js
export default {
  authorize: () => {
    return 'token';
  },
};
```

```
// __tests__/disableAutomocking.js
import utils from '../utils';

jest.disableAutomock();

test('original implementation', () => {
  // now we have the original implementation,
  // even if we set the automocking in a jest configuration
  expect(utils.authorize()).toBe('token');
});
```

当您遇到要模拟的依赖项数量远小于不模拟的依赖项数量的场景时，这通常很有用。例如，如果您正在为使用大量依赖项的模块编写测试，这些依赖项可以合理地归类为模块的“实现细节”，那么您可能不想嘲笑它们。

可以被视为“实现细节”的依赖项示例包括从语言内置（例如Array.prototype方法）到高度常见的实用程序方法（例如下划线/lo-dash、数组工具函数、等）和整个库，如React.js。

返回用于链接的`jest`对象。

*注意：此方法以前称为`autoMockOff`。使用`babel-jest`时，对`disableAutomock`的调用将自动提升到代码块的顶部。如果要显式避免此行为，请使用`autoMockOff `。*



### `jest.enableAutomock()`[#](https://www.jestjs.cn/docs/jest-object#jestenableautomock)

在模块加载器中启用自动模拟。

返回用于链接的jest对象。

有关详细信息，请参阅配置的自动模拟部分

示例：

```
// utils.js
export default {
  authorize: () => {
    return 'token';
  },
  isAuthorized: secret => secret === 'wizard',
};
```

```
// __tests__/enableAutomocking.js
jest.enableAutomock();

import utils from '../utils';

test('original implementation', () => {
  // now we have the mocked implementation,
  expect(utils.authorize._isMockFunction).toBeTruthy();
  expect(utils.isAuthorized._isMockFunction).toBeTruthy();
});
```

注意：此方法以前称为 autoMockOn。当使用 babel-jest 时，*`enableAutomock`*  的调用将自动提升到代码块的顶部。如果要显式避免此行为，请使用 `autoMockOn` 。



### `jest.createMockFromModule(moduleName)`[#](https://www.jestjs.cn/docs/jest-object#jestcreatemockfrommodulemodulename)

##### renamed in Jest **26.0.0+**[#](https://www.jestjs.cn/docs/jest-object#renamed-in-jest-2600)

也在别名下：.genMockFromModule(moduleName)

给定模块的名称，请使用自动模拟系统为您生成模块的模拟版本。

当您希望创建扩展  [manual mock](https://www.jestjs.cn/docs/manual-mocks)  行为的手动模拟时，这非常有用。

示例：

```
// utils.js
export default {
  authorize: () => {
    return 'token';
  },
  isAuthorized: secret => secret === 'wizard',
};
```

```
// __tests__/createMockFromModule.test.js
const utils = jest.createMockFromModule('../utils').default;
utils.isAuthorized = jest.fn(secret => secret === 'not wizard');

test('implementation created by jest.createMockFromModule', () => {
  expect(utils.authorize.mock).toBeTruthy();
  expect(utils.isAuthorized('not wizard')).toEqual(true);
});
```

This is how `createMockFromModule` will mock the following data types:

#### `Function`[#](https://www.jestjs.cn/docs/jest-object#function)

创建一个新的  [mock function](https://www.jestjs.cn/docs/mock-functions)。新函数没有形式参数，调用时将返回 `undefined`。此功能也适用于异步函数。

#### `Class`[#](https://www.jestjs.cn/docs/jest-object#class)

创建新类。原始类的接口将被维护，所有类成员函数和属性都将被模拟。

#### `Object`[#](https://www.jestjs.cn/docs/jest-object#object)

创建新的深度克隆对象。对象键将被维护，其值将被模拟。

#### `Array`[#](https://www.jestjs.cn/docs/jest-object#array)

创建一个新的空数组，忽略原始数组。

#### `Primitives`[#](https://www.jestjs.cn/docs/jest-object#primitives)

创建与原始属性具有相同基元值的新属性。

示例：

```
// example.js
module.exports = {
  function: function square(a, b) {
    return a * b;
  },
  asyncFunction: async function asyncSquare(a, b) {
    const result = await a * b;
    return result;
  },
  class: new class Bar {
    constructor() {
      this.array = [1, 2, 3];
    }
    foo() {}
  },
  object: {
    baz: 'foo',
    bar: {
      fiz: 1,
      buzz: [1, 2, 3],
    },
  },
  array: [1, 2, 3],
  number: 123,
  string: 'baz',
  boolean: true,
  symbol: Symbol.for('a.b.c'),
};
```

```
// __tests__/example.test.js
const example = jest.createMockFromModule('./example');

test('should run example code', () => {
  // creates a new mocked function with no formal arguments.
  expect(example.function.name).toEqual('square');
  expect(example.function.length).toEqual(0);

  // async functions get the same treatment as standard synchronous functions.
  expect(example.asyncFunction.name).toEqual('asyncSquare');
  expect(example.asyncFunction.length).toEqual(0);

  // creates a new class with the same interface, member functions and properties are mocked.
  expect(example.class.constructor.name).toEqual('Bar');
  expect(example.class.foo.name).toEqual('foo');
  expect(example.class.array.length).toEqual(0);

  // creates a deeply cloned version of the original object.
  expect(example.object).toEqual({
    baz: 'foo',
    bar: {
      fiz: 1,
      buzz: [],
    },
  });

  // creates a new empty array, ignoring the original array.
  expect(example.array.length).toEqual(0);

  // creates a new property with the same primitive value as the original property.
  expect(example.number).toEqual(123);
  expect(example.string).toEqual('baz');
  expect(example.boolean).toEqual(true);
  expect(example.symbol).toEqual(Symbol.for('a.b.c'));
});
```



### `jest.mock(moduleName, factory, options)`[#](https://www.jestjs.cn/docs/jest-object#jestmockmodulename-factory-options)

在需要时，使用自动模拟版本模拟模块。factory 和 options 是可选的。例如：

```
// banana.js
module.exports = () => 'banana';

// __tests__/test.js
jest.mock('../banana');

const banana = require('../banana'); // banana will be explicitly mocked.

banana(); // will return 'undefined' because the function is auto-mocked.
```

第二个参数可用于指定正在运行的显式模块工厂，而不是使用Jest的自动模拟功能：

```
jest.mock('../moduleName', () => {
  return jest.fn(() => 42);
});

// This runs the function specified as second argument to `jest.mock`.
const moduleName = require('../moduleName');
moduleName(); // Will return '42';
```

当将 factory 参数用于具有默认导出的ES6模块时，需要指定 __esModule: true 属性。此属性通常由 Babel/TypeScript 生成，但在这里需要手动设置。导入默认导出时，它是一条指令，用于从导出对象导入名为default的属性：

```
import moduleName, {foo} from '../moduleName';

jest.mock('../moduleName', () => {
  return {
    __esModule: true,
    default: jest.fn(() => 42),
    foo: jest.fn(() => 43),
  };
});

moduleName(); // Will return 42
foo(); // Will return 43
```

第三个参数可用于创建虚拟模拟——系统中任何地方都不存在的模块的模拟：

```
jest.mock(
  '../moduleName',
  () => {
    /*
     * Custom implementation of a module that doesn't exist in JS,
     * like a generated module or a native module in react-native.
     */
  },
  {virtual: true},
);
```

警告：在设置文件中导入模块（由 setupTestFrameworkScriptFile 指定）将防止对有关模块以及它导入的所有模块进行模拟。

使用 jest.mock 模拟的模块仅对调用 jest.mock 的文件进行模拟。导入模块的另一个文件将获得原始实现，即使它在模拟模块的测试文件之后运行。

返回用于链接的 jest 对象。



### `jest.unmock(moduleName)`[#](https://www.jestjs.cn/docs/jest-object#jestunmockmodulename)

指示模块系统永远不应从 require() 返回指定模块的模拟版本（例如，它应始终返回真实模块）。

此API最常见的用途是指定给定测试打算测试的模块（因此不希望自动模拟）。

返回用于链接的jest对象。



### `jest.doMock(moduleName, factory, options)`[#](https://www.jestjs.cn/docs/jest-object#jestdomockmodulename-factory-options)

当使用babel-jest时，对模拟的调用将自动提升到代码块的顶部。如果要显式避免此行为，请使用此方法。

一个有用的示例是，当您希望在同一文件中以不同的方式模拟模块时：

```
beforeEach(() => {
  jest.resetModules();
});

test('moduleName 1', () => {
  jest.doMock('../moduleName', () => {
    return jest.fn(() => 1);
  });
  const moduleName = require('../moduleName');
  expect(moduleName()).toEqual(1);
});

test('moduleName 2', () => {
  jest.doMock('../moduleName', () => {
    return jest.fn(() => 2);
  });
  const moduleName = require('../moduleName');
  expect(moduleName()).toEqual(2);
});
```

将 jest.doMock() 与ES6导入一起使用需要其他步骤。如果您不想在测试中使用要求，请遵循以下操作：

- 我们必须指定 __esModule: true 属性（有关详细信息，请参见 jest.mock(）API)。
- 静态ES6模块导入被提升到文件的顶部，因此我们必须使用 import() 动态导入它们。
- 最后，我们需要一个支持动态导入的环境。有关初始设置，请参阅[Using Babel](https://www.jestjs.cn/docs/getting-started#using-babel)。然后，将插件 [babel-plugin-dynamic-import-node](https://www.npmjs.com/package/babel-plugin-dynamic-import-node) 或等效节点添加到Babel配置中，以在Node中启用动态导入。

```
beforeEach(() => {
  jest.resetModules();
});

test('moduleName 1', () => {
  jest.doMock('../moduleName', () => {
    return {
      __esModule: true,
      default: 'default1',
      foo: 'foo1',
    };
  });
  return import('../moduleName').then(moduleName => {
    expect(moduleName.default).toEqual('default1');
    expect(moduleName.foo).toEqual('foo1');
  });
});

test('moduleName 2', () => {
  jest.doMock('../moduleName', () => {
    return {
      __esModule: true,
      default: 'default2',
      foo: 'foo2',
    };
  });
  return import('../moduleName').then(moduleName => {
    expect(moduleName.default).toEqual('default2');
    expect(moduleName.foo).toEqual('foo2');
  });
});
```

返回用于链接的jest对象。



### `jest.dontMock(moduleName)`[#](https://www.jestjs.cn/docs/jest-object#jestdontmockmodulename)

当使用 babel-jest 时，unmock 的调用将自动提升到代码块的顶部。如果要显式避免此行为，请使用此方法。

返回用于链接的 jest 对象。



### `jest.setMock(moduleName, moduleExports)`[#](https://www.jestjs.cn/docs/jest-object#jestsetmockmodulename-moduleexports)

显式提供模块系统应为指定模块返回的模拟对象。

有时，模块系统通常为您提供的自动生成的模拟不足以满足您的测试需求。通常，在这种情况下，您应该编写一个更适合有关模块的 [manual mock](https://www.jestjs.cn/docs/manual-mocks) 。然而，在极其罕见的情况下，即使是手动模拟也不适合您的目的，您需要在测试中自己构建模拟。

在这些罕见的情况下，您可以使用此API手动填充模块系统的模拟模块注册表中的插槽。

返回用于链接的 jest 对象。

注意：建议使用 jest.mock() 代替。jest.mock  API的第二个参数是模块工厂，而不是预期的导出模块对象。



### `jest.requireActual(moduleName)`[#](https://www.jestjs.cn/docs/jest-object#jestrequireactualmodulename)

返回实际模块而不是模拟，绕过对模块是否应接收模拟实现的所有检查。

示例：

```
jest.mock('../myModule', () => {
  // Require the original module to not be mocked...
  const originalModule = jest.requireActual('../myModule');

  return {
    __esModule: true, // Use it when dealing with esModules
    ...originalModule,
    getRandom: jest.fn().mockReturnValue(10),
  };
});

const getRandom = require('../myModule').getRandom;

getRandom(); // Always returns 10
```



### `jest.requireMock(moduleName)`[#](https://www.jestjs.cn/docs/jest-object#jestrequiremockmodulename)

返回一个模拟模块而不是实际模块，绕过对模块是否应正常需要的所有检查。



### `jest.resetModules()`[#](https://www.jestjs.cn/docs/jest-object#jestresetmodules)

重置模块注册表-所有所需模块的缓存。这对于隔离测试之间本地状态可能冲突的模块非常有用。

示例：

```
const sum1 = require('../sum');
jest.resetModules();
const sum2 = require('../sum');
sum1 === sum2;
// > false (Both sum modules are separate "instances" of the sum module.)
```

测试示例：

```
beforeEach(() => {
  jest.resetModules();
});

test('works', () => {
  const sum = require('../sum');
});

test('works too', () => {
  const sum = require('../sum');
  // sum is a different copy of the sum module from the previous test.
});
```

返回用于链接的 jest 对象。



### `jest.isolateModules(fn)`[#](https://www.jestjs.cn/docs/jest-object#jestisolatemodulesfn)

jest.isolateModules(fn) 比 jest.resetModules()  更进一步，并为加载在回调函数中的模块创建沙箱注册表。这对于隔离每个测试的特定模块非常有用，以便本地模块状态不会在测试之间发生冲突。

```
let myModule;
jest.isolateModules(() => {
  myModule = require('myModule');
});

const otherCopyOfMyModule = require('myModule');
```



## Mock functions[#](https://www.jestjs.cn/docs/jest-object#mock-functions)

### `jest.fn(implementation)`[#](https://www.jestjs.cn/docs/jest-object#jestfnimplementation)

返回一个新的、未使用的 [mock function](https://www.jestjs.cn/docs/mock-function-api)。（可选）采用模拟实现。

```
const mockFn = jest.fn();
mockFn();
expect(mockFn).toHaveBeenCalled();

// With a mock implementation:
const returnsTrue = jest.fn(() => true);
console.log(returnsTrue()); // true;
```



### `jest.isMockFunction(fn)`[#](https://www.jestjs.cn/docs/jest-object#jestismockfunctionfn)

确定给定函数是否为模拟函数。



### `jest.spyOn(object, methodName)`[#](https://www.jestjs.cn/docs/jest-object#jestspyonobject-methodname)

创建一个类似于 jest.fn 的模拟函数，但也跟踪对  object[methodName] 的调用。返回Jest  [mock function](https://www.jestjs.cn/docs/mock-function-api) 。

注意：默认情况下，*`jest.spyOn`*  也会调用 ***spied*** 方法。这与大多数其他测试库不同。如果要覆盖原始函数，可以使用*`jest.spyOn(object, methodName).mockImplementation(() => customImplementation)`*  或*`object[methodName] = jest.fn(() => customImplementation)`*;

示例：

```
const video = {
  play() {
    return true;
  },
};

module.exports = video;
```

示例测试：

```
const video = require('./video');

test('plays video', () => {
  const spy = jest.spyOn(video, 'play');
  const isPlaying = video.play();

  expect(spy).toHaveBeenCalled();
  expect(isPlaying).toBe(true);

  spy.mockRestore();
});
```



### `jest.spyOn(object, methodName, accessType?)`[#](https://www.jestjs.cn/docs/jest-object#jestspyonobject-methodname-accesstype)

自 Jest 22.1.0+ 以来，jest.spyOn 方法采用 accessType 的可选第三个参数，该参数可以是“get”或“set”，当您想分别监视getter或setter时，这被证明是有用的。

示例：

```
const video = {
  // it's a getter!
  get play() {
    return true;
  },
};

module.exports = video;

const audio = {
  _volume: false,
  // it's a setter!
  set volume(value) {
    this._volume = value;
  },
  get volume() {
    return this._volume;
  },
};

module.exports = audio;
```

示例测试：

```
const audio = require('./audio');
const video = require('./video');

test('plays video', () => {
  const spy = jest.spyOn(video, 'play', 'get'); // we pass 'get'
  const isPlaying = video.play;

  expect(spy).toHaveBeenCalled();
  expect(isPlaying).toBe(true);

  spy.mockRestore();
});

test('plays audio', () => {
  const spy = jest.spyOn(audio, 'volume', 'set'); // we pass 'set'
  audio.volume = 100;

  expect(spy).toHaveBeenCalled();
  expect(audio.volume).toBe(100);

  spy.mockRestore();
});
```



### `jest.clearAllMocks()`[#](https://www.jestjs.cn/docs/jest-object#jestclearallmocks)

清除所有模拟的 mock.calls 和 mock.instances 属性。相当于在每个模拟函数上调用  [`.mockClear()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockclear) 。

返回用于链接的 jest 对象。



### `jest.resetAllMocks()`[#](https://www.jestjs.cn/docs/jest-object#jestresetallmocks)

重置所有模拟的状态。相当于在每个模拟函数上调用  [`.mockReset()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockreset) 。

返回用于链接的jest对象。



### `jest.restoreAllMocks()`[#](https://www.jestjs.cn/docs/jest-object#jestrestoreallmocks)

将所有模拟恢复到其原始值。相当于在每个模拟函数上调用 [`.mockRestore()`](https://www.jestjs.cn/docs/mock-function-api#mockfnmockrestore) 。请注意，jest.restoreAllMocks() 仅在使用 jest.spyOn 创建模拟时有效；其他模拟将要求您手动恢复它们。



## Mock timers[#](https://www.jestjs.cn/docs/jest-object#mock-timers)

### `jest.useFakeTimers(implementation?: 'modern' | 'legacy')`[#](https://www.jestjs.cn/docs/jest-object#jestusefaketimersimplementation-modern--legacy)

指示Jest使用标准计时器函数的假版本 (`setTimeout`, `setInterval`, `clearTimeout`, `clearInterval`, `nextTick`, `setImmediate` and `clearImmediate`以及 `Date`)。

如果您将 `'legacy'` 作为参数传递，则将使用Jest的传统实现，而不是基于 [`@sinonjs/fake-timers`](https://github.com/sinonjs/fake-timers)的实现。

返回用于链接的 jest 对象。



### `jest.useRealTimers()`[#](https://www.jestjs.cn/docs/jest-object#jestuserealtimers)

指示Jest使用标准计时器函数的实际版本。

返回用于链接的jest对象。



### `jest.runAllTicks()`[#](https://www.jestjs.cn/docs/jest-object#jestrunallticks)

耗尽 **micro**-task queue （通常通过 `process.nextTick`在节点中接口）。

调用此API时，将执行所有通过  `process.nextTick`  排队的待处理微任务。此外，如果这些微任务本身调度新的微任务，则这些微任务将不断耗尽，直到队列中没有更多的微任务剩余。



### `jest.runAllTimers()`[#](https://www.jestjs.cn/docs/jest-object#jestrunalltimers)

耗尽 宏任务队列（即，由 `setTimeout()`, `setInterval()`, and `setImmediate()`)排队的所有任务)，和微任务队列（通常通过process.nextTick在节点中接口）。

调用此API时，将执行所有挂起的 宏任务 和 微任务。如果这些任务本身计划新任务，则这些任务将不断耗尽，直到队列中没有更多的任务剩余。

这通常对于在测试期间同步执行setTimeout非常有用，以便同步断言只有在执行  `setTimeout()` or `setInterval()`  回调之后才会发生的某些行为。有关更多信息，请参见 [Timer mocks](https://www.jestjs.cn/docs/timer-mocks) 文档。



### `jest.runAllImmediates()`[#](https://www.jestjs.cn/docs/jest-object#jestrunallimmediates)

耗尽 setImmediate() 排队的所有任务。

> 注意：使用现代假计时器实现时，此函数不可用



### `jest.advanceTimersByTime(msToRun)`[#](https://www.jestjs.cn/docs/jest-object#jestadvancetimersbytimemstorun)

仅执行宏任务队列（即由 `setTimeout()` or `setInterval()` and `setImmediate()`排队的所有任务)。

调用此API时，所有计时器都会提前 msToRun 毫秒。所有已通过 setTimeout() 或 setInterval() 排队并将在此时间范围内执行的挂起的“宏任务”都将被执行。此外，如果这些宏任务计划在同一时间框架内执行的新宏任务，则这些宏任务将被执行，直到队列中没有更多的宏任务，这些宏任务应在 msToRun 毫秒内运行。



### `jest.runOnlyPendingTimers()`[#](https://www.jestjs.cn/docs/jest-object#jestrunonlypendingtimers)

仅执行当前挂起的宏任务（即，仅执行到目前为止已由setTimeout(）或setInterval()排队的任务)。如果任何当前挂起的宏任务计划新的宏任务，则此调用将不会执行这些新任务。

这对于以下场景非常有用，例如正在测试的模块调度一个setTimeout()，该setTimeout()的回调递归调度另一个setTimeout()（这意味着调度永远不会停止）。在这些情况下，能够一次一步地向前运行是很有用的。



### `jest.advanceTimersToNextTimer(steps)`[#](https://www.jestjs.cn/docs/jest-object#jestadvancetimerstonexttimersteps)

将所有计时器提前所需的毫秒，以便仅运行下一个超时/间隔。

或者，您可以提供步骤，因此它将运行下一个超时/间隔的步骤量。

### `jest.clearAllTimers()`[#](https://www.jestjs.cn/docs/jest-object#jestclearalltimers)

从计时器系统中删除任何挂起的计时器。

这意味着，如果任何计时器已计划（但尚未执行），它们将被清除，并且将来永远没有机会执行。



### `jest.getTimerCount()`[#](https://www.jestjs.cn/docs/jest-object#jestgettimercount)

返回仍需运行的假计时器数量。



### `jest.setSystemTime(now?: number | Date)`[#](https://www.jestjs.cn/docs/jest-object#jestsetsystemtimenow-number--date)

设置假计时器使用的当前系统时间。模拟用户在程序运行时更改系统时钟。它影响当前时间，但它本身不会导致计时器触发；它们将与没有调用 jest.setSystemTime() 的情况完全一样触发。

> 注意：此函数仅在使用现代假计时器实现时可用



### `jest.getRealSystemTime()`[#](https://www.jestjs.cn/docs/jest-object#jestgetrealsystemtime)

当mock 时，Date.now()也将被 mock。如果您出于某种原因需要访问实际当前时间，您可以调用此函数。

> 注意：此函数仅在使用现代假计时器实现时可用



## Misc[#](https://www.jestjs.cn/docs/jest-object#misc)

### `jest.setTimeout(timeout)`[#](https://www.jestjs.cn/docs/jest-object#jestsettimeouttimeout)

设置测试和挂接前/挂接后的默认超时时间（以毫秒为单位）。这仅影响调用此函数的测试文件。

注意：如果不调用此方法，默认超时时间为5秒。

注意：如果要设置所有测试文件的超时，则在 *`setupFilesAfterEnv`* 中进行此操作的好。

示例：

```
jest.setTimeout(1000); // 1 second
```



### `jest.retryTimes()`[#](https://www.jestjs.cn/docs/jest-object#jestretrytimes)

运行失败的测试n次，直到它们通过或直到最大重试次数耗尽。这只适用于默认的 [jest-circus](https://github.com/facebook/jest/tree/master/packages/jest-circus)  运行！

测试示例：

```
jest.retryTimes(3);
test('will fail', () => {
  expect(true).toBe(false);
});
```

返回`jest`链式对象。

