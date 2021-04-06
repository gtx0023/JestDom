# API-Globals

在测试文件中，Jest将这些方法和对象中的每一个都放入全局环境中。您不需要或导入任何内容即可使用它们。但是，如果您更喜欢显式导入，则可以从“@jest/globals”中 import {describe, expect, test} 。

## Methods[#](https://www.jestjs.cn/docs/api#methods)

- [`afterAll(fn, timeout)`](https://www.jestjs.cn/docs/api#afterallfn-timeout)
- [`afterEach(fn, timeout)`](https://www.jestjs.cn/docs/api#aftereachfn-timeout)
- [`beforeAll(fn, timeout)`](https://www.jestjs.cn/docs/api#beforeallfn-timeout)
- [`beforeEach(fn, timeout)`](https://www.jestjs.cn/docs/api#beforeeachfn-timeout)
- [`describe(name, fn)`](https://www.jestjs.cn/docs/api#describename-fn)
- [`describe.each(table)(name, fn, timeout)`](https://www.jestjs.cn/docs/api#describeeachtablename-fn-timeout)
- [`describe.only(name, fn)`](https://www.jestjs.cn/docs/api#describeonlyname-fn)
- [`describe.only.each(table)(name, fn)`](https://www.jestjs.cn/docs/api#describeonlyeachtablename-fn)
- [`describe.skip(name, fn)`](https://www.jestjs.cn/docs/api#describeskipname-fn)
- [`describe.skip.each(table)(name, fn)`](https://www.jestjs.cn/docs/api#describeskipeachtablename-fn)
- [`test(name, fn, timeout)`](https://www.jestjs.cn/docs/api#testname-fn-timeout)
- [`test.concurrent(name, fn, timeout)`](https://www.jestjs.cn/docs/api#testconcurrentname-fn-timeout)
- [`test.concurrent.each(table)(name, fn, timeout)`](https://www.jestjs.cn/docs/api#testconcurrenteachtablename-fn-timeout)
- [`test.concurrent.only.each(table)(name, fn)`](https://www.jestjs.cn/docs/api#testconcurrentonlyeachtablename-fn)
- [`test.concurrent.skip.each(table)(name, fn)`](https://www.jestjs.cn/docs/api#testconcurrentskipeachtablename-fn)
- [`test.each(table)(name, fn, timeout)`](https://www.jestjs.cn/docs/api#testeachtablename-fn-timeout)
- [`test.only(name, fn, timeout)`](https://www.jestjs.cn/docs/api#testonlyname-fn-timeout)
- [`test.only.each(table)(name, fn)`](https://www.jestjs.cn/docs/api#testonlyeachtablename-fn-1)
- [`test.skip(name, fn)`](https://www.jestjs.cn/docs/api#testskipname-fn)
- [`test.skip.each(table)(name, fn)`](https://www.jestjs.cn/docs/api#testskipeachtablename-fn)
- [`test.todo(name)`](https://www.jestjs.cn/docs/api#testtodoname)



## 参考信息

### `afterAll(fn, timeout)`

在此文件中的所有测试完成后运行函数。如果函数返回一个承诺或是一个生成器，Jest将等待该承诺解析，然后再继续。

或者，您可以提供 timeout（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

如果您想清理跨测试共享的某些全局设置状态，这通常非常有用。

例如：

```
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterAll(() => {
  cleanUpDatabase(globalDatabase);
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```

在这里，afterAll确保在所有测试运行后调用清理数据库。

如果afterAll位于描述块内，则它在描述块的末尾运行。

如果您想在每次测试之后而不是在所有测试之后运行一些清理，请使用afterEach。

### `afterEach(fn, timeout)`

在此文件中的每个测试完成后运行函数。如果函数返回一个承诺或是一个生成器，Jest将等待该承诺解析，然后再继续。

或者，您可以提供超时（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

如果您想清理每个测试创建的一些临时状态，这通常很有用。

例如：

```
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterEach(() => {
  cleanUpDatabase(globalDatabase);
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```

在这里，afterEach确保在每次测试运行后调用cleanUpDatabase。

如果afterEach位于描述块内，则它仅在此描述块内的测试之后运行。

如果您想在所有测试运行后只运行一次清理，请使用afterAll。

### `beforeAll(fn, timeout)`

在运行此文件中的任何测试之前运行函数。如果函数返回一个承诺或是一个生成器，Jest在运行测试之前等待该承诺解析。

或者，您可以提供超时（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

如果您想设置一些将被许多测试使用的全局状态，这通常是很有用的。

例如：

```
const globalDatabase = makeGlobalDatabase();

beforeAll(() => {
  // Clears the database and adds some testing data.
  // Jest will wait for this promise to resolve before running tests.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});

// Since we only set up the database once in this example, it's important
// that our tests don't modify it.
test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});
```

在这里，beforeAll确保在测试运行之前设置数据库。如果设置是同步的，您可以在没有beforeAll的情况下执行此操作。关键是Jest将等待承诺解析，因此您也可以进行异步设置。

如果beforeAll位于 describe 块内，则它在描述块的开头运行。

如果您想在每次测试之前而不是在任何测试运行之前运行某项内容，请使用 beforeEach。

### `beforeEach(fn, timeout)`

在运行此文件中的每个测试之前运行函数。如果函数返回一个承诺或是一个生成器，Jest在运行测试之前等待该承诺解析。

或者，您可以提供超时（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

如果您想重置许多测试将使用的某些全局状态，这通常非常有用。

例如：

```
const globalDatabase = makeGlobalDatabase();

beforeEach(() => {
  // Clears the database and adds some testing data.
  // Jest will wait for this promise to resolve before running tests.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```

在这里，beforeEach 确保为每个测试重置数据库。
如果beforeEach 位于 describe 块内，则它为描述块中的每个测试运行。
如果您只需要在运行任何测试之前运行一次一些设置代码，请使用 beforeAll。

### `describe(name, fn)`

describe(name, fn) 创建一个块，该块将几个相关测试分组在一起。例如，如果您有一个 myBeverage 对象，它应该是美味的，但不酸的，您可以使用：

```
const myBeverage = {
  delicious: true,
  sour: false,
};

describe('my beverage', () => {
  test('is delicious', () => {
    expect(myBeverage.delicious).toBeTruthy();
  });

  test('is not sour', () => {
    expect(myBeverage.sour).toBeFalsy();
  });
});
```

这不是必需的-您可以直接在顶层写入测试块。但是，如果您更喜欢将测试组织成组，这可能会很方便。

如果您具有测试层次结构，您还可以嵌套 describe 块：

```
const binaryStringToNumber = binString => {
  if (!/^[01]+$/.test(binString)) {
    throw new CustomError('Not a binary number.');
  }

  return parseInt(binString, 2);
};

describe('binaryStringToNumber', () => {
  describe('given an invalid binary string', () => {
    test('composed of non-numbers throws CustomError', () => {
      expect(() => binaryStringToNumber('abc')).toThrowError(CustomError);
    });

    test('with extra whitespace throws CustomError', () => {
      expect(() => binaryStringToNumber('  100')).toThrowError(CustomError);
    });
  });

  describe('given a valid binary string', () => {
    test('returns the correct number', () => {
      expect(binaryStringToNumber('100')).toBe(4);
    });
  });
});
```

### `describe.each(table)(name, fn, timeout)`

如果您一直使用不同的数据复制相同的测试套件，请使用 describe.each 。describe.each 允许您写入一次测试套件并将数据传递到其中。

describe.each 有两个API：

#### 1. `describe.each(table)(name, fn, timeout)`

table：数组数组，其中包含传递到每行fn中的参数。

​	注意：如果传入一维基元数组，则在内部将映射到表，即[1,2,3]->[1],[2],[3]]

name：String 测试套件的标题。

通过使用printf格式的位置注入参数来生成唯一的测试标题：

- `%p` - [pretty-format](https://www.npmjs.com/package/pretty-format).
- `%s`- String.
- `%d`- Number.
- `%i` - Integer.
- `%f` - Floating point value.
- `%j` - JSON.
- `%o` - Object.
- `%#` - Index of the test case.
- `%%` - single percent sign ('%'). This does not consume an argument.

fn：Function 要运行的测试套件，这是一个函数，它将接收每行中的参数作为函数参数。

或者，您可以提供 timeout（以毫秒为单位），用于指定在中止之前等待每行的时间。注意：默认超时为5秒。

示例：

```
describe.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  test(`returns ${expected}`, () => {
    expect(a + b).toBe(expected);
  });

  test(`returned value not be greater than ${expected}`, () => {
    expect(a + b).not.toBeGreaterThan(expected);
  });

  test(`returned value not be less than ${expected}`, () => {
    expect(a + b).not.toBeLessThan(expected);
  });
});
```

#### 2. `describe.each`ˋtableˋ`(name, fn, timeout)`[#](https://www.jestjs.cn/docs/api#2-describeeachtablename-fn-timeout)

table：标记模板文字

- 变量名列标题的第一行，用|分隔
- 使用${value}语法作为模板文字表达式提供的一行或多行后续数据。

name：字符串测试套件的标题，使用$变量将测试数据从标记的模板表达式注入到套件标题中。

- 要注入嵌套对象值，您可以提供一个keyPath， i.e. `$variable.path.to.value`

fn：函数要运行的测试套件，这是接收测试数据对象的函数。

或者，您可以提供超时（以毫秒为单位），用于指定在中止之前等待每行的时间。注意：默认超时为5秒。
示例：

```
describe.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('$a + $b', ({a, b, expected}) => {
  test(`returns ${expected}`, () => {
    expect(a + b).toBe(expected);
  });

  test(`returned value not be greater than ${expected}`, () => {
    expect(a + b).not.toBeGreaterThan(expected);
  });

  test(`returned value not be less than ${expected}`, () => {
    expect(a + b).not.toBeLessThan(expected);
  });
});
```

### `describe.only(name, fn)`

也在别名下：fdescribe(name, fn)
只有当您只想运行一个描述块时，您才能使用 describe.only。

```
describe.only('my beverage', () => {
  test('is delicious', () => {
    expect(myBeverage.delicious).toBeTruthy();
  });

  test('is not sour', () => {
    expect(myBeverage.sour).toBeFalsy();
  });
});

describe('my other beverage', () => {
  // ... will be skipped
});
```

### `describe.only.each(table)(name, fn)`

也在别名下：fdescribe.each(table)(name, fn) 和 fdescribe.each`table`(name, fn)

如果您只希望运行数据驱动测试的特定测试套件，请使用 describe.only.each。

describe.only.each 有两个API：

#### 1.`describe.only.each(table)(name, fn)`

```
describe.only.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  test(`returns ${expected}`, () => {
    expect(a + b).toBe(expected);
  });
});

test('will not be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```

#### 2.`describe.only.each`ˋtableˋ`(name, fn)`

```
describe.only.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', ({a, b, expected}) => {
  test('passes', () => {
    expect(a + b).toBe(expected);
  });
});

test('will not be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```

### `describe.skip(name, fn)`

也在别名下：xdescribe(name, fn)

如果您不想运行特定的描述块，您可以使用 describe.skip：

```
describe('my beverage', () => {
  test('is delicious', () => {
    expect(myBeverage.delicious).toBeTruthy();
  });

  test('is not sour', () => {
    expect(myBeverage.sour).toBeFalsy();
  });
});

describe.skip('my other beverage', () => {
  // ... will be skipped
});
```

使用 describe.skip 通常是暂时注释掉一大块测试的更干净的替代方案。

### `describe.skip.each(table)(name, fn)`

也在别名下：xdescribe.each(table)(name, fn)  和  xdescribe.each`table`(name, fn)

如果要停止运行一组数据驱动测试，请使用  describe.skip.each。

describe.skip.each 有两个API：

#### 1.`describe.skip.each(table)(name, fn)`

```
describe.skip.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  test(`returns ${expected}`, () => {
    expect(a + b).toBe(expected); // will not be ran
  });
});

test('will be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```

#### 2.`describe.skip.each`  ˋtableˋ `(name, fn)`

```
describe.skip.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', ({a, b, expected}) => {
  test('will not be ran', () => {
    expect(a + b).toBe(expected); // will not be ran
  });
});

test('will be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```

### `test(name, fn, timeout)`

也在别名下：it(name, fn, timeout)

测试文件中所需要的只是运行测试的 test 方法。例如，假设有一个函数 inchesOfRain() 应该为零。你的整个测试可能是：

```
test('did not rain', () => {
  expect(inchesOfRain()).toBe(0);
});
```

第一个参数是测试名称；第二个参数是包含要测试的期望的函数。第三个参数（可选）是  timeout（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

注意：如果从测试中返回 **promise**，Jest将等待承诺解析，然后让测试完成。如果**你为测试函数提供参数**，Jest也将等待，通常 回调 done 。当您想测试回调时，这可能会很方便。在此处查看如何测试异步代码。

例如，假设 fetchBeverageList() 返回一个承诺，该承诺应该解析为其中包含 lemon 列表。您可以使用以下方法测试此功能：

```
test('has lemon in it', () => {
  return fetchBeverageList().then(list => {
    expect(list).toContain('lemon');
  });
});
```

即使对 test 的调用将立即返回，但在承诺也解决之前，测试不会完成。

### `test.concurrent(name, fn, timeout)`

也在别名下：it.concurrent(name, fn, timeout)

如果希望测试并发运行，请使用 test.concurrent。

> 注意：test.concurrent 被认为是实验性的-有关缺失功能和其他问题的详细信息，请参阅此处

第一个参数是测试名称；第二个参数是包含要测试的期望的异步函数。第三个参数（可选）是 timeout（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

```
test.concurrent('addition of 2 numbers', async () => {
  expect(5 + 3).toBe(8);
});

test.concurrent('subtraction 2 numbers', async () => {
  expect(5 - 3).toBe(2);
});
```

注意：在配置中使用 maxConcurities 来防止Jest同时执行超过指定数量的测试

### `test.concurrent.each(table)(name, fn, timeout)`

也在别名下：it.concurrent.each(table)(name, fn, timeout)

如果您一直使用不同的数据复制同一测试，请使用 test.concurrent.each。test.each 允许您写入一次测试并将数据传递进去，所有测试都是异步运行的。

test.concurrent.each 有两个API：

#### 1. `test.concurrent.each(table)(name, fn, timeout)`

- `table`: 数组数组，其中包含传递到每行测试fn中的参数。

  - 注意：如果传入一维基元数组，则在内部将映射到表，即[1,2,3]->[1],[2],[3]]

- `name`: 字符串测试块的标题。
  - 通过使用printf格式的位置注入参数来生成唯一的测试标题：
    - `%p` - [pretty-format](https://www.npmjs.com/package/pretty-format).
    - `%s`- String.
    - `%d`- Number.
    - `%i` - Integer.
    - `%f` - Floating point value.
    - `%j` - JSON.
    - `%o` - Object.
    - `%#` - Index of the test case.
    - `%%` - single percent sign ('%'). 这不会消耗参数。

- `fn`:  函数要运行的测试，这是一个函数，它将接收每行中的参数作为函数参数，这必须是一个异步函数。

- 或者，您可以提供超时（以毫秒为单位），用于指定在中止之前等待每行的时间。注意：默认超时为5秒。

示例：

```
test.concurrent.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  expect(a + b).toBe(expected);
});
```



#### 2. `test.concurrent.each`ˋtableˋ`(name, fn, timeout)`

- `table`: 标记模板文字
  - 变量名列标题的第一行，用|分隔
  - 使用${value}语法作为模板文字表达式提供的一行或多行后续数据。
- name：字符串测试的标题，使用 $variable 将测试数据从标记的模板表达式注入到测试标题中。
  - 要注入嵌套对象值，您可以提供一个keyPath，i.e.   $variable.path.to.value
- fn：函数要运行的测试，这是将接收测试数据对象的函数，这必须是一个异步函数。
- 或者，您可以提供 timeout（以毫秒为单位），用于指定在中止之前等待每行的时间。注意：默认超时为5秒。

示例：

```
test.concurrent.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', ({a, b, expected}) => {
  expect(a + b).toBe(expected);
});
```



### `test.concurrent.only.each(table)(name, fn)`

也在别名下：it.concurrent.only.each(table)(name, fn)

如果您只希望同时运行具有不同测试数据的特定测试，请使用 test.concurrent.only.each。

test.concurrent.only.each 有两个API：

#### `test.concurrent.only.each(table)(name, fn)`

```
test.concurrent.only.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', async (a, b, expected) => {
  expect(a + b).toBe(expected);
});

test('will not be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```

#### `test.only.each`ˋtableˋ`(name, fn)`

```
test.concurrent.only.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', async ({a, b, expected}) => {
  expect(a + b).toBe(expected);
});

test('will not be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```



### `test.concurrent.skip.each(table)(name, fn)`

也在别名下：it.concurrent.skip.each(table)(name, fn)

如果要停止运行异步数据驱动测试的集合，请使用 test.concurrent.skip.each。

test.concurrent.skip.each 有两个API：

#### `test.concurrent.skip.each(table)(name, fn)`

```
test.concurrent.skip.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', async (a, b, expected) => {
  expect(a + b).toBe(expected); // will not be ran
});

test('will be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```



#### `test.concurrent.skip.each`ˋtableˋ`(name, fn)`

```
test.concurrent.skip.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', async ({a, b, expected}) => {
  expect(a + b).toBe(expected); // will not be ran
});

test('will be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```



### `test.each(table)(name, fn, timeout)`

也在别名下：it.each(table)(name, fn) 和  it.each`table`(name, fn)

如果您一直使用不同的数据复制同一测试，请使用test.each。test.each 允许您写入一次测试并将数据传递进去。

test.each 有两个API：

#### 1. `test.each(table)(name, fn, timeout)`

- `table`: 数组数组，其中包含传递到每行测试fn中的参数。
  - 注意：如果传入一维基元数组，则在内部将映射到表，即[1,2,3]->[1],[2],[3]]
- name：字符串测试块的标题。
  - 通过使用printf格式的位置注入参数来生成唯一的测试标题：
    - `%p` - [pretty-format](https://www.npmjs.com/package/pretty-format).
    - `%s`- String.
    - `%d`- Number.
    - `%i` - Integer.
    - `%f` - Floating point value.
    - `%j` - JSON.
    - `%o` - Object.
    - `%#` - Index of the test case.
    - `%%` - single percent sign ('%'). 这不会消耗参数。
- fn：函数要运行的测试，这是一个函数，它将接收每行中的参数作为函数参数。
- 或者，您可以提供 timeout（以毫秒为单位），用于指定在中止之前等待每行的时间。注意：默认超时为5秒。

示例：

```
test.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  expect(a + b).toBe(expected);
});
```



#### 2. `test.each`ˋtableˋ`(name, fn, timeout)`

- `table`: 标记模板文字
  - 变量名列标题的第一行，用|分隔
  - 使用${value}语法作为模板文字表达式提供的一行或多行后续数据。
- name：字符串测试的标题，使用 $variable 将测试数据从标记的模板表达式注入到测试标题中。
  - 要注入嵌套对象值，您可以提供一个keyPath，i.e. `$variable.path.to.value`
- fn：函数要运行的测试，这是接收测试数据对象的函数。
- 或者，您可以提供  timeout（以毫秒为单位），用于指定在中止之前等待每行的时间。注意：默认超时为5秒。

示例：

```
test.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', ({a, b, expected}) => {
  expect(a + b).toBe(expected);
});
```



### `test.only(name, fn, timeout)`

也在别名下：it.only(name, fn, timeout) 和 fit(name, fn, timeout)

当您调试大型测试文件时，您通常只希望运行测试的子集。您可以使用 .only 指定要在该测试文件中运行的唯一测试。

或者，您可以提供  timeout（以毫秒为单位），用于指定中止前等待的时间。注意：默认超时为5秒。

例如，假设您进行了以下测试：

```
test.only('it is raining', () => {
  expect(inchesOfRain()).toBeGreaterThan(0);
});

test('it is not snowing', () => {
  expect(inchesOfSnow()).toBe(0);
});
```

只有“正在下雨”测试将在该测试文件中运行，因为它是使用 test.only 运行的。

通常，您不会使用 test.only 将代码检查到源代码管理中--您会使用它进行调试，并在修复损坏的测试后将其删除。



### `test.only.each(table)(name, fn)`

也在别名下：it.only.each(table)(name, fn) 、fit.each(table)(name, fn)、it.only.each`table`(name, fn) 和 fit.each`table`(name, fn)

如果您只希望运行具有不同测试数据的特定测试，请使用 test.only.each。

test.only.each 有两个API：

#### `test.only.each(table)(name, fn)`

```
test.only.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  expect(a + b).toBe(expected);
});

test('will not be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```

#### `test.only.each`ˋtableˋ`(name, fn)`

```
test.only.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', ({a, b, expected}) => {
  expect(a + b).toBe(expected);
});

test('will not be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```



### `test.skip(name, fn)`

也在别名下：it.skip(name, fn)、xit(name, fn) 和  xtest(name, fn)

当您维护一个大型代码库时，您有时可能会发现一个测试由于某种原因暂时中断。如果要跳过运行此测试，但不想删除此代码，可以使用test.skip 指定要跳过的一些测试。

例如，假设您进行了以下测试：

```
test('it is raining', () => {
  expect(inchesOfRain()).toBeGreaterThan(0);
});

test.skip('it is not snowing', () => {
  expect(inchesOfSnow()).toBe(0);
});
```

只有 “it is raining” 测试将运行，因为另一个测试是使用 test.skip 运行的。

您可以注释掉测试，但使用 test.skip 通常会更好一些，因为它将保持缩进和语法突出显示。



### `test.skip.each(table)(name, fn)`

也在别名下：it.skip.each(table)(name, fn)`, `xit.each(table)(name, fn)`, `xtest.each(table)(name, fn)`, `it.skip.each`table`(name, fn)`, `xit.each`table`(name, fn) 和 xtest.each`table`(name, fn)

如果要停止运行数据驱动测试的集合，请使用 test.skip.each。

test.skip.each 有两个API：

#### `test.skip.each(table)(name, fn)`

```
test.skip.each([
  [1, 1, 2],
  [1, 2, 3],
  [2, 1, 3],
])('.add(%i, %i)', (a, b, expected) => {
  expect(a + b).toBe(expected); // will not be ran
});

test('will be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```



#### `test.skip.each`ˋtableˋ`(name, fn)`

```
test.skip.each`
  a    | b    | expected
  ${1} | ${1} | ${2}
  ${1} | ${2} | ${3}
  ${2} | ${1} | ${3}
`('returns $expected when $a is added $b', ({a, b, expected}) => {
  expect(a + b).toBe(expected); // will not be ran
});

test('will be ran', () => {
  expect(1 / 0).toBe(Infinity);
});
```



### `test.todo(name)`

也在别名下：it.todo(name)

当您计划编写测试时，请使用 test.todo。这些测试将在最后的摘要输出中突出显示，以便您知道仍需要执行多少测试。

注意：如果提供测试回调函数，则 test.todo 将引发错误。如果您已经实现了测试，并且它已中断，并且不希望它运行，请使用 test.skip代替。

API编号

- name：字符串测试计划的标题。

示例：

```
const add = (a, b) => a + b;

test.todo('add should be associative');
```

