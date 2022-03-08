# Object 오브젝트

## ES3 기준

### new Object()

인스턴스를 생성하여 반환한다. 파라미터의 데이터 타입에 따라 생성할 인스턴스의 타입이 결정된다. Number 타입이면 Number 인스턴스를 생성하고 String 타입이면 String 인스턴스를 생성한다.

```jsx
let val = new Object();

//파라미터 값이 undefined, null이면 빈 object 인스턴스를 반환한다.
log(val); //{}
```

### Object()

Object 인스턴스를 생성한다. 파라미터는 {name : value} 형태.

```jsx
let val = Object({name : "테스트"});
log(val); //{name : 테스트}

//파라미터를 작성하지 않으면 new Object()와 같다.
let val = Object();
log(val); //{}
```

👉 let abc = {}와 let abc = Object()는 같다.

### valueOf()

data 위치에 작성한 Object 인스턴스의 프리미티브 값을 반환한다.

```jsx
let val = {name : "테스트"};
log(val.valueOf()); //{name : 테스트}
```

## 프로퍼티 처리 메소드

### hasOwnProperty()

인스턴스에 파라미터 이름이 존재하면 true를 반환한다.

```jsx
var obj = {value : 123};
var own = obj.hasOwnProperty("value");
log(own); //true

//값은 체크하지 않고 존재 여부만 체크한다.
var obj = {value : undefined};
var own = obj.hasOwnProperty("value");
log(own); //true

//자신이 만든 것이 아니라 상속받은 프로퍼티면 false를 반환한다.
var obj = {};
var own = obj.hasOwnProperty("hasOwnProperty");
log(own); //false
```

### propertyIsEnumerable()

오브젝트에서 프로퍼티를 열거할 수 있으면 true를 반환한다.

```jsx
var obj = {sports : "축구"};
var own = obj.propertyIsEnumerable("sports");
log(own); //true

//ES5 내용
var obj = {sports : "축구"};
Object.defineProperty({obj, "sports", {
	eummerable : false
});
var own = obj.propertyIsEnumerable("sports");
log(own); //false

for(let name in obj) {
	log(name); //아무것도 출력되지 않음. 열거할 수 없는 상태이기 때문
}
```

### isPrototypeOf()

파라미터에 작성한 오브젝트에 object 위치에 작성한 prototype이 존재하면 true를 반환한다.

```jsx
var numObj = new Number(123);
log(Object.prototype.isPrototypeOf(numObj)); //true
```

### toString()

인스턴스 타입을 문자열로 표시한다.

```jsx
var point = {book : "책"};
log(point.toString()); //[object Object]

var obj = new Number(123);
log(Object.prototype.toString.call(obj)); //[object Number] -> [인스턴스 타입]
```

> object는 인스턴스를 나타내고 Object는 빌트인 Object를 나타낸다.
> 

### toLocaleString()

지역화 문자 변환 메소드를 대체하여 호출한다. Array, Number, Date 오브젝트의 toLocaleString() 메소드가 먼저 호출되고 Array, Number, Date 오브젝트가 아닐 경우 빌트인 오브젝트의 toLocaleString() 메소드가 호출된다. 에러 발생을 방지하기 위한 것이다(Object의 toLocaleString()이 없으면 에러가 발생하니까).

## ES5 기준

### ES5 Object의 특징

함수가 추가되었다. 메소드는 하나도 없음. 빌트인 Object의 모든 메소드는 대부분의 빌트인 오브젝트에 첨부되는데, 이렇게 되면 연결이 많이 발생한다. 함수는 첨부되지 않으므로 연결 부하를 줄일 수 있다.

### [defineProperty()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) / defineProperties()

프로퍼티 추가, 속성 변경. 데이터 보호의 목적. 프로퍼티마다 상태(변경, 삭제, 열거 가능 여부)를 가지고 있다. 상태가 가능일 때만 처리할 수 있으며 프로퍼티를 추가할 때 상태를 결정한다.

```jsx
const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false
});

object1.property1 = 77;
// throws an error in strict mode

console.log(object1.property1);
// expected output: 42
```

### 프로퍼티 디스크립터

```jsx
// 두 가지를 혼용할 수는 없음
Object.defineProperty(o, 'conflict', {
  value: 0x9f91102,
  get: function() { return 0xdeadbeef; }
});
```

### getter, setter

OOP 용어. 설명은 ES5 기준이나 ES6의 방법을 사용하는 것이 더 나음.

```jsx
var o = {};
var bValue = 38;
Object.defineProperty(o, 'b', {
  // ES2015 단축 메서드명 사용
  // 아래 코드와 같음
  // get: function() { return bValue; }
  // set: function(newValue) { bValue = newValue; },
  get() { return bValue; },
  set(newValue) { bValue = newValue; },
  enumerable: true,
  configurable: true
});
o.b; // 38
// 'b' 속성이 o 객체에 존재하고 값은 38
// o.b를 재정의하지 않는 이상
// o.b의 값은 항상 bValue와 동일함
```

> get() 함수로 호출하면 에러 발생.
> 

### getPrototypeOf()

파라미터의 prototype에 연결된 프로퍼티를 반환한다. (setPrototypeOf()은 ES5 스펙에 없고 ES6에 있음)

### keys()

열거 가능한 프로퍼티 이름을 반환한다.

## 프로퍼티 디스크립터 함수

### preventExtensions()

오브젝트에 프로퍼티 추가 금지 설정. 추가 금지를 설정한 후에는 추가 가능으로 변경 불가.

### seal()

오브젝트에 프로퍼티 추가, 삭제 금지 설정. 추가 금지는 오브젝트 단위로 설정하고 삭제 금지는 프로퍼티 단위. 추가 금지를 하더라도 변경은 가능하다.

### freeze()

오브젝트에 프로퍼티 추가, 삭제, 변경 금지 설정.
