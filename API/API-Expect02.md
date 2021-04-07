

### `.toHaveReturnedWith(value)`

也在别名下：.toReturnWith(value)

使用.toHaveReturnedWith 来确保模拟函数返回特定的值。

例如，假设您有一个模拟饮料，它返回所消费饮料的名称。您可以写：

```
test('drink returns La Croix', () => {
  const beverage = {name: 'La Croix'};
  const drink = jest.fn(beverage => beverage.name);

  drink(beverage);

  expect(drink).toHaveReturnedWith('La Croix');
});
```



### `.toHaveLastReturnedWith(value)`

也在别名下：.lastReturnedWith(value)

使用.toHaveLastReturnedWith 测试模拟函数上次返回的特定值。如果对模拟函数的最后一次调用引发了错误，则无论您提供了什么值作为预期返回值，此匹配器都将失败。

例如，假设您有一个模拟 drink，它返回所消费饮料的名称。您可以写：

```
test('drink returns La Croix (Orange) last', () => {
  const beverage1 = {name: 'La Croix (Lemon)'};
  const beverage2 = {name: 'La Croix (Orange)'};
  const drink = jest.fn(beverage => beverage.name);

  drink(beverage1);
  drink(beverage2);

  expect(drink).toHaveLastReturnedWith('La Croix (Orange)');
});
```



### `.toHaveNthReturnedWith(nthCall, value)`

也在别名下：.nthReturnedWith(nthCall, value)

使用.toHaveNthReturnedWith 测试模拟函数为第n次调用返回的特定值。如果对模拟函数的第n次调用引发了错误，则无论您提供了什么值作为预期返回值，此匹配器都将失败。

例如，假设您有一个模拟drink ，它返回所消费饮料的名称。您可以写：

```
test('drink returns expected nth calls', () => {
  const beverage1 = {name: 'La Croix (Lemon)'};
  const beverage2 = {name: 'La Croix (Orange)'};
  const drink = jest.fn(beverage => beverage.name);

  drink(beverage1);
  drink(beverage2);

  expect(drink).toHaveNthReturnedWith(1, 'La Croix (Lemon)');
  expect(drink).toHaveNthReturnedWith(2, 'La Croix (Orange)');
});
```

注意：第n个参数必须是从1开始的正整数。



### `.toHaveLength(number)`

使用.toHaveLength 检查对象是否具有.length属性，并将其设置为特定的数值。

这对于检查数组或字符串大小特别有用。

```
expect([1, 2, 3]).toHaveLength(3);
expect('abc').toHaveLength(3);
expect('').not.toHaveLength(5);
```



### `.toHaveProperty(keyPath, value?)`

使用.toHaveProperty 检查对象是否存在提供的引用keyPath处的属性。要检查对象中的深度嵌套属性，您可以使用点表示法或包含深度引用keyPath的数组。

您可以提供一个可选的值参数来比较接收到的属性值（递归地用于对象实例的所有属性，也称为深度相等，如 toEqual 匹配器）。

以下示例包含具有嵌套属性的 houseForSale 对象。我们正在使用 toHaveProperty 来检查对象中各种属性的存在和值。

```
// Object containing house features to be tested
const houseForSale = {
  bath: true,
  bedrooms: 4,
  kitchen: {
    amenities: ['oven', 'stove', 'washer'],
    area: 20,
    wallColor: 'white',
    'nice.oven': true,
  },
  'ceiling.height': 2,
};

test('this house has my desired features', () => {
  // Example Referencing
  expect(houseForSale).toHaveProperty('bath');
  expect(houseForSale).toHaveProperty('bedrooms', 4);

  expect(houseForSale).not.toHaveProperty('pool');

  // Deep referencing using dot notation
  expect(houseForSale).toHaveProperty('kitchen.area', 20);
  expect(houseForSale).toHaveProperty('kitchen.amenities', [
    'oven',
    'stove',
    'washer',
  ]);

  expect(houseForSale).not.toHaveProperty('kitchen.open');

  // Deep referencing using an array containing the keyPath
  expect(houseForSale).toHaveProperty(['kitchen', 'area'], 20);
  expect(houseForSale).toHaveProperty(
    ['kitchen', 'amenities'],
    ['oven', 'stove', 'washer'],
  );
  expect(houseForSale).toHaveProperty(['kitchen', 'amenities', 0], 'oven');
  expect(houseForSale).toHaveProperty(['kitchen', 'nice.oven']);
  expect(houseForSale).not.toHaveProperty(['kitchen', 'open']);

  // Referencing keys with dot in the key itself
  expect(houseForSale).toHaveProperty(['ceiling.height'], 'tall');
});
```



### `.toBeCloseTo(number, numDigits?)`

使用 toBeCloseTo 比较浮点数的近似相等性。

可选的 numDigits 参数限制小数点后要检查的位数。对于默认值2，测试标准为 Math.abs(expected - received) < 0.005（即10 ** -2 / 2）。

直观的等式比较通常失败，因为十进制（以10为基数）值的算术在有限精度二进制（以2为基数）表示中通常有舍入误差。例如，此测试失败：

```
test('adding works sanely with decimals', () => {
  expect(0.2 + 0.1).toBe(0.3); // Fails!
});
```

它失败了，因为在JavaScript中，0.2 + 0.1实际上是0.30000000000000004。

例如，此测试以5位精度通过：

```
test('adding works sanely with decimals', () => {
  expect(0.2 + 0.1).toBeCloseTo(0.3, 5);
});
```

因为浮点错误是 toBeCloseTo 解决的问题，所以它不支持大整数值。



### `.toBeDefined()`

使用 .toBeDefined 检查变量是否未定义。例如，如果您想检查函数 fetchNewFlavorIdea() 是否返回了某些内容，您可以写入：

```
test('there is a new flavor idea', () => {
  expect(fetchNewFlavorIdea()).toBeDefined();
});
```

您可以编写 expect(fetchNewFlavorIdea()).not.toBe(undefined)，但更好的做法是避免直接在代码中引用 undefined。



### `.toBeFalsy()`

当您不关心值是什么，并且希望确保值在布尔上下文中为false时，请使用.toBeFalsy。例如，假设您有一些应用程序代码，看起来如下：

```
drinkSomeLaCroix();
if (!getErrors()) {
  drinkMoreLaCroix();
}
```

您可能不在乎getErrors返回什么，特别是 \- it  可能返回 false、null或0，并且您的代码仍然可以工作。所以，如果你想测试 drinking some La Croix 后没有错误，你可以写：

```
test('drinking La Croix does not lead to errors', () => {
  drinkSomeLaCroix();
  expect(getErrors()).toBeFalsy();
});
```

在JavaScript中，有六个假值：false、0、''、null、undefined 和 NaN。其他的都是真实的。



### `.toBeGreaterThan(number | bigint)`

使用 toBeGreaterThan 比较数字或大整数值的 received > expected 。例如，测试 ouncesPerCan() 返回的值是否超过10盎司：

```
test('ounces per can is more than 10', () => {
  expect(ouncesPerCan()).toBeGreaterThan(10);
});
```



### `.toBeGreaterThanOrEqual(number | bigint)`

使用 toBeGreaterThanOrEqual 比较 received >= expected 数字或大整数值。例如，测试 ouncesPerCan() 返回至少12 ounces 的值：

```
test('ounces per can is at least 12', () => {
  expect(ouncesPerCan()).toBeGreaterThanOrEqual(12);
});
```



### `.toBeLessThan(number | bigint)`

使用 toBeLessThan 比较 received < expected 数字或大整数值。例如，测试 ouncesPerCan() 返回的值小于20盎司：

```
test('ounces per can is less than 20', () => {
  expect(ouncesPerCan()).toBeLessThan(20);
});
```



### `.toBeLessThanOrEqual(number | bigint)`

使用 toBeLessThanOrEqual 比较 received <= expected 数字或大整数值。例如，测试 ouncesPerCan() 返回最多12盎司的值：

```
test('ounces per can is at most 12', () => {
  expect(ouncesPerCan()).toBeLessThanOrEqual(12);
});
```



### `.toBeInstanceOf(Class)`

使用 .toBeInstanceOf(Class) 检查对象是否为类的实例。此匹配器在下面使用 实例。

```
class A {}

expect(new A()).toBeInstanceOf(A);
expect(() => {}).toBeInstanceOf(Function);
expect(new A()).toBeInstanceOf(Function); // throws
```



### `.toBeNull()`

.toBeNull() 与 .toBe(null) 相同，但错误消息要好一点。因此，当您想检查某项内容是否为空时，请使用 .toBeNull()。

```
function bloop() {
  return null;
}

test('bloop returns null', () => {
  expect(bloop()).toBeNull();
});
```



### `.toBeTruthy()`

当您不在乎值是什么，并且希望确保值在布尔上下文中为真时，请使用.toBeTruthy。例如，假设您有一些应用程序代码，看起来如下：

```
drinkSomeLaCroix();
if (thirstInfo()) {
  drinkMoreLaCroix();
}
```

您可能不在乎 thirstInfo 返回什么，特别是 \- it 可能返回 true 或复杂对象，并且您的代码仍然可以工作。所以，如果你想测试 drinking some La Croix 后的 thirstInfo 是真实的，你可以写：

```
test('drinking La Croix leads to having thirst info', () => {
  drinkSomeLaCroix();
  expect(thirstInfo()).toBeTruthy();
});
```

在JavaScript中，有六个假值：false、0、''、null、undefined 和 NaN。其他的都是真实的。



### `.toBeUndefined()`

使用.toBeUndefined 检查变量是否未定义。例如，如果您想检查函数 bestDrinkForFlavor(flavor)是否为 “octopus” 口味返回 undefined，因为没有好的 octopus-flavored drink：

```
test('the best drink for octopus flavor is undefined', () => {
  expect(bestDrinkForFlavor('octopus')).toBeUndefined();
});
```

您可以编写 expect(bestDrinkForFlavor('octopus')).toBe(undefined) ，但更好的做法是避免直接在代码中引用 undefined。



### `.toBeNaN()`

当检查值是否为NaN时，使用.toBeNaN。

```
test('passes when value is NaN', () => {
  expect(NaN).toBeNaN();
  expect(1).not.toBeNaN();
});
```



### `.toContain(item)`

当您要检查项是否在数组中时，请使用.toContain。对于测试数组中的项，这使用===，严格的等式检查。.toContain 还可以检查字符串是否为另一个字符串的子字符串。

例如，如果 getAllFlavors() 返回一个 array of flavors，并且您希望确保 lime 在其中，您可以写入：

```
test('the flavor list contains lime', () => {
  expect(getAllFlavors()).toContain('lime');
});
```



### `.toContainEqual(item)`

当您要检查数组中是否包含具有特定结构和值的项时，请使用.toContainEqual。对于测试数组中的项，此匹配器递归检查所有字段的相等性，而不是检查对象标识。

```
describe('my beverage', () => {
  test('is delicious and not sour', () => {
    const myBeverage = {delicious: true, sour: false};
    expect(myBeverages()).toContainEqual(myBeverage);
  });
});
```



### `.toEqual(value)`

使用 .toEqual 递归比较对象实例的所有属性（也称为 "deep" 相等）。它调用 Object.is 来比较基元值，这比===严格等式运算符更适合测试。

例如，.toEqual 和 .toBe 在此测试套件中的行为不同，因此所有测试都通过：

```
const can1 = {
  flavor: 'grapefruit',
  ounces: 12,
};
const can2 = {
  flavor: 'grapefruit',
  ounces: 12,
};

describe('the La Croix cans on my desk', () => {
  test('have all the same properties', () => {
    expect(can1).toEqual(can2);
  });
  test('are not the exact same can', () => {
    expect(can1).not.toBe(can2);
  });
});
```

> 注意：.toEqual不会对两个错误执行深度相等检查。只有错误的 message 属性才被视为相等。建议使用.toThrow匹配器来测试错误。

如果属性之间的差异不能帮助您理解测试失败的原因，特别是如果报表很大，则您可以将比较移动到 expect 函数中。例如，使用 equals Buffer 方法来断言 buffers 是否包含相同的内容：

- rewrite `expect(received).toEqual(expected)` as `expect(received.equals(expected)).toBe(true)`
- rewrite `expect(received).not.toEqual(expected)` as `expect(received.equals(expected)).toBe(false)`



### `.toMatch(regexp | string)`

使用.toMatch检查字符串是否与正则表达式匹配。

例如，您可能不知道 essayOnTheBestFlavor() 到底返回了什么，但您知道它是一个很长的字符串，子字符串 grapefruit 应该在那里的某个地方。您可以使用以下方法测试此功能：

```
describe('an essay on the best flavor', () => {
  test('mentions grapefruit', () => {
    expect(essayOnTheBestFlavor()).toMatch(/grapefruit/);
    expect(essayOnTheBestFlavor()).toMatch(new RegExp('grapefruit'));
  });
});
```

此匹配器还接受字符串，它将尝试匹配该字符串：

```
describe('grapefruits are healthy', () => {
  test('grapefruits are a fruit', () => {
    expect('grapefruits').toMatch('fruit');
  });
});
```



### `.toMatchObject(object)`

使用 .toMatchObject 检查JavaScript对象是否与对象属性的子集匹配。它将将接收到的对象与不在预期对象中的属性匹配。

您还可以传递对象数组，在这种情况下，只有当接收到的数组中的每个对象都与预期数组中的相应对象匹配（在上面描述的toMatchObject 意义上）时，方法才会返回true。如果您想检查两个数组的元素数量是否匹配，而不是数组包含，这将非常有用，因为arrayContaining 允许在接收的数组中添加额外的元素。

您可以将属性与值或匹配器匹配。

```
const houseForSale = {
  bath: true,
  bedrooms: 4,
  kitchen: {
    amenities: ['oven', 'stove', 'washer'],
    area: 20,
    wallColor: 'white',
  },
};
const desiredHouse = {
  bath: true,
  kitchen: {
    amenities: ['oven', 'stove', 'washer'],
    wallColor: expect.stringMatching(/white|yellow/),
  },
};

test('the house has my desired features', () => {
  expect(houseForSale).toMatchObject(desiredHouse);
});
```

```
describe('toMatchObject applied to arrays', () => {
  test('the number of elements must match exactly', () => {
    expect([{foo: 'bar'}, {baz: 1}]).toMatchObject([{foo: 'bar'}, {baz: 1}]);
  });

  test('.toMatchObject is called for each elements, so extra object properties are okay', () => {
    expect([{foo: 'bar'}, {baz: 1, extra: 'quux'}]).toMatchObject([
      {foo: 'bar'},
      {baz: 1},
    ]);
  });
});
```



### `.toMatchSnapshot(propertyMatchers?, hint?)`

这可确保值与最新的快照匹配。有关详细信息，请参阅快照测试指南。

如果接收到的值将是对象实例，则可以提供一个可选的 propertyMatchers  对象参数，该参数将非对称匹配器作为预期属性子集的值。这就像为属性子集使用灵活的标准 toMatchObject ，然后是快照测试作为其余属性的精确标准。

您可以提供附加到测试名称的可选提示字符串参数。虽然Jest总是在快照名称的末尾附加一个数字，但简短的描述性提示可能比数字更有用，以区分单个 it 或 test 块中的多个快照。Jest在相应的.snap文件中按名称对快照进行排序。



### `.toMatchInlineSnapshot(propertyMatchers?, inlineSnapshot)`

确保值与最近的快照匹配。

如果接收到的值将是对象实例，则可以提供一个可选的 propertyMatchers 对象参数，该参数将非对称匹配器作为预期属性子集的值。这就像为属性子集使用灵活的标准 toMatchObject，然后是快照测试作为其余属性的精确标准。

Jest在测试第一次运行时将 inlineSnapshot 字符串参数添加到测试文件（而不是外部.snap文件）中的匹配器。

有关更多信息，请查看 [Inline Snapshots](https://www.jestjs.cn/docs/snapshot-testing#inline-snapshots) 部分。



### `.toStrictEqual(value)`

使用.toStrictEqual测试对象的类型和结构是否相同。

与.toEqual的区别：

- 检查具有未定义属性的键。例如，使用.toStrictEqual时，{a: undefined, b: 2} 不匹配{b: 2}。
- 检查数组稀疏性。例如，使用.toStrictEqual时，[, 1]与 [undefined, 1] 不匹配。
- 对象类型被检查为相等。例如，具有字段 a 和 b 的类实例将不等于具有字段 a 和 b 的文字对象。

```
class LaCroix {
  constructor(flavor) {
    this.flavor = flavor;
  }
}

describe('the La Croix cans on my desk', () => {
  test('are not semantically the same', () => {
    expect(new LaCroix('lemon')).toEqual({flavor: 'lemon'});
    expect(new LaCroix('lemon')).not.toStrictEqual({flavor: 'lemon'});
  });
});
```



### `.toThrow(error?)`

也在别名下：.toThrowError(error?)

使用 .toThrow 测试函数在调用时是否抛出。例如，如果我们想测试 drinkFlavor('octopus') 抛出，因为 octopus flavor 太恶心了，不能喝，我们可以写：

```
test('throws on octopus', () => {
  expect(() => {
    drinkFlavor('octopus');
  }).toThrow();
});
```

注意：您必须将代码包装在函数中，否则将不会捕获错误，断言将失败。

您可以提供一个可选参数来测试是否引发了特定错误：

- 正则表达式：错误消息匹配模式
- 字符串：错误消息包括子字符串
- 错误对象：错误消息等于对象的消息属性
- 错误类：错误对象是类的实例

例如，假设饮料口味的编码是这样的：

```
function drinkFlavor(flavor) {
  if (flavor == 'octopus') {
    throw new DisgustingFlavorError('yuck, octopus flavor');
  }
  // Do some other stuff
}
```

我们可以测试此错误以几种方式被抛出：

```
test('throws on octopus', () => {
  function drinkOctopus() {
    drinkFlavor('octopus');
  }

  // Test that the error message says "yuck" somewhere: these are equivalent
  expect(drinkOctopus).toThrowError(/yuck/);
  expect(drinkOctopus).toThrowError('yuck');

  // Test the exact error message
  expect(drinkOctopus).toThrowError(/^yuck, octopus flavor$/);
  expect(drinkOctopus).toThrowError(new Error('yuck, octopus flavor'));

  // Test that we get a DisgustingFlavorError
  expect(drinkOctopus).toThrowError(DisgustingFlavorError);
});
```



### `.toThrowErrorMatchingSnapshot(hint?)`

使用 .toThrowErrorMatchingSnapshot 测试函数在调用时是否抛出与最新快照匹配的错误。

您可以提供附加到测试名称的可选 hint 字符串参数。虽然Jest总是在快照名称的末尾附加一个数字，但简短的描述性提示可能比数字更有用，以区分单个 it` or `test 块中的多个快照。Jest在相应的.snap文件中按名称对快照进行排序。

例如，假设您有一个 drinkFlavor 函数，每当口味是 'octopus' 时，它就会抛出，编码如下：

```
function drinkFlavor(flavor) {
  if (flavor == 'octopus') {
    throw new DisgustingFlavorError('yuck, octopus flavor');
  }
  // Do some other stuff
}
```

此函数的测试将是这样的：

```
test('throws on octopus', () => {
  function drinkOctopus() {
    drinkFlavor('octopus');
  }

  expect(drinkOctopus).toThrowErrorMatchingSnapshot();
});
```

它将生成以下快照：

```
exports[`drinking flavors throws on octopus 1`] = `"yuck, octopus flavor"`;
```

有关快照测试的更多信息，请查看 [React Tree Snapshot Testing](https://www.jestjs.cn/blog/2016/07/27/jest-14) 。



### `.toThrowErrorMatchingInlineSnapshot(inlineSnapshot)`

使用 .toThrowErrorMatchingInlineSnapshot 测试函数在调用时是否抛出与最新快照匹配的错误。

Jest在测试第一次运行时将 inlineSnapshot 字符串参数添加到测试文件（而不是外部.snap文件）中的匹配器。

有关更多信息，请查看 [Inline Snapshots](https://www.jestjs.cn/docs/snapshot-testing#inline-snapshots)。
