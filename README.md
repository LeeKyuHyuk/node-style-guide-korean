# Node.js 스타일 안내서

이 글은 일관되고 보기 좋은 node.js 코드를 작성하기 위한 안내서입니다.

이 안내서는 [Felix Geisendörfer](http://felixge.de/)가 작성하였으며 [이규혁](http://kyuhyuk.kr)이 한국어로 번역하였습니다.

**기여하기**: 이 문서는 누구나 참여가 가능합니다.
 '[LeeKyuHyuk/node-style-guide-korean](https://github.com/LeeKyuHyuk/node-style-guide-korean)' 저장소에 pull-request 해주시기 바랍니다.

## 서식

### 들여쓰기 할 때는 2칸 스페이스

들여쓰기를 할 때는 2칸 <kbd>space</kbd>를 사용하며, 절대로 <kbd>tab</kbd>과 <kbd>space</kbd>를 섞어 쓰지 않습니다.

### 개행

UNIX 스타일의 개행 문자인 (`\n`)을 마지막 문자로 사용합니다. Windows 스타일의 (`\r\n`) 는 사용하지 않습니다.

### 공백 문자를 정리하자

매 식사 후에 양치를 하는 것처럼 커밋 하기 전에는 JS 파일의 공백 문자 들을 정리합니다.

### 세미콜론 사용

### 1줄당 80자

코드를 작성할 때 1줄당 80자로 제한하세요. 지난 몇 년 동안 화면은 점점 커지고 있습니다, 하지만 여러분의 두뇌는 그렇지 않습니다. 화면 분할을 위해 추가 공간을 사용합시다. 아마 대부분의 에디터는 지원할 것입니다.

### 작은 따옴표 사용

JSON을 작성하지 않는 한 작은따옴표를 사용합니다.

*올바른 예시:*

```js
var foo = 'bar';
```

*잘못된 예시:*

```js
var foo = "bar";
```

### 여는 중괄호는 명령문과 같은 줄에

여는 중괄호는 명령문과 같은 줄에 입력합니다.

*올바른 예시:*

```js
if (true) {
  console.log('winning');
}
```

*잘못된 예시:*

```js
if (true)
{
  console.log('losing');
}
```

또한 조건문 앞뒤에 있는 공백 문자 사용에 주의합니다.

### `var` 한 개당 하나의 변수만 선언

`var` 하나당 하나의 변수를 선언하면 행 순서를 쉽게 바꿀 수 있습니다. 그러나 [Crockford][crockfordconvention]를 무시하면 함수 내에서 변수를 더 자세히 선언할 수 있습니다.

*올바른 예시:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*잘못된 예시:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## 이름 지정 규칙

### 변수, 속성 및 함수 이름에는 lowerCamelCase 사용

> **lowerCamelCase:** camelCase에서, 맨 앞글자를 소문자로 표기하는 것을 뜻합니다.
> 나머지 뒤에 따라붙는 단어들의 앞글자는 모두 대문자로 표기합니다.

변수, 속성 및 함수의 이름은 `lowerCamelCase`를 사용해야 하며 설명이 있어야 합니다. 단일 문자 변수와 흔치 않은 약어는 되도록이면 피해야 합니다.

*올바른 예시:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*잘못된 예시:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

### 클래스 이름에는 UpperCamelCase 사용

> **UpperCamelCase:** camelCase에서, 맨 앞글자를 대문자로 표기하는 것을 뜻합니다.
> 나머지 뒤에 따라붙는 단어들의 앞글자는 모두 대문자로 표기합니다.

클래스 이름은 `UpperCamelCase`를 사용하여 대문자로 시작해야합니다.

*올바른 예시:*

```js
function BankAccount() {
}
```

*잘못된 예시:*

```js
function bank_Account() {
}
```

### 상수에는 대문자 사용

상수는 모두 대문자를 사용하여, 일반 변수 또는 정적 클래스 속성으로 선언해야 합니다.

*올바른 예시:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*잘못된 예시:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## 변수

### 객체 / 배열 생성

후행 쉼표를 사용하고 *short* 선언을 한 줄에 넣으세요. 인용 키는 인터프리터가 요구할 때 사용합니다.

*올바른 예시:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*잘못된 예시:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## 조건식

### `===` 연산자 사용

프로그래밍은 어리석은 규칙을 기억하지 않습니다. [`===`](https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators) 연산자를 사용하면 예상대로 작동됩니다.

*올바른 예시:*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*잘못된 예시:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```


### 여러 줄의 삼 항 연산자 사용

삼 항 연산자는 한 줄로 사용하면 안 됩니다. 여러 줄로 분할하여 사용합니다.

*올바른 예시:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*잘못된 예시:*

```js
var foo = (a === b) ? 1 : 2;
```

### 서술하는 조건 사용

모든 조건들은 이름이 설명적으로 작성돼 있는 변수나 함수에 할당되어야 합니다.

*올바른 예시:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*잘못된 예시:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## 함수

### 작은 함수 작성

함수를 짧게 유지합니다. 좋은 함수는 큰 방의 마지막 줄에 있는 사람들이 편안하게 읽을 수 있는 슬라이드와 같습니다. 좋은 가독성을 보여야 하며 함수마다 15줄의 코드로 제한되어야 합니다.

### 함수에서 일찍 반환

if 문에 깊이 들어가지 않으려면 가능한 한 빨리 함수의 값을 반환합니다.

*올바른 예시:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*잘못된 예시:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

이 특정 예제의 경우에는 아래와 같이 더욱 짧게 하는 것이 좋습니다.

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### 클로저 이름 지정

클로저 이름을 지정함으로써 더 나은 성능을 보여줍니다.

*올바른 예시:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*잘못된 예시:*

```js
req.on('end', function() {
  console.log('losing');
});
```

### 클로저는 중첩되지 않게

클로저를 사용할 때 중첩하는 것을 피합니다. 그렇지 않으면 코드가 엉망이 될 것입니다.

*올바른 예시:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*잘못된 예시:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```


### 메서드 체이닝

메서드를 연결하려면 한 줄에 하나의 메서드를 사용합니다.

이러한 메서드는 들여 쓰기 하여 동일한 체인의 일부임을 쉽게 알 수 있게 합니다.

*올바른 예시:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

*잘못된 예시:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

## 주석

### 주석에는 슬래시를 사용

한 줄 또는 여러 줄 주석 모두 슬래시를 사용합니다. 주석은 상위 수준의 메커니즘을 설명하거나 코드의 어려운 부분을 명확하게 설명하는 내용을 작성합니다. 사소한 것들을 말하기 위해 주석을 사용하는 것은 피합니다.

*올바른 예시:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*잘못된 예시:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## 여러 가지 잡다한 내용

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

당신은 아마 필요 없을 것입니다. 되도록이면 멀리 하십시오.

### Getters와 setters

Setter를 사용하지 마십시오. 소프트웨어를 사용하려는 사람들이 해결할 수있는 것보다 많은 문제를 일으킵니다.

콜렉션 클래스에 길이 속성을 제공하는 것과 같이 [부작용](http://en.wikipedia.org/wiki/Side_effect_(computer_science)) 없는 Getter를 자유롭게 사용할 수 있습니다.


### 기본 제공 프로토 타입을 확장하지 않습니다

기본 JavaScript 객체의 프로토 타입을 확장하지 마세요.

*올바른 예시:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*잘못된 예시:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

---

원문: [felixge/node-style-guide](https://github.com/felixge/node-style-guide/)

이 안내서는 [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/) 라이센스를 가지고 있습니다.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)
