# JSON 오브젝트

**J**ava**S**cript **O**bject **N**otation. 데이터 송수신의 변환 기준. 텍스트이므로 전송 속도가 빠르다. JS 데이터 타입을 지원하며 다른 언어도 사용하지만 완전하게 같지 않을 수 있기 때문에 필수적으로 확인이 필요하다.

### stringify()

JS → JSON 타입의 문자열.

```jsx
//특수한 값 변환
log(JSON.stringify([infinity, NaN, null])); //[null, null, null]
log(JSON.stringify([true, false])); //[true, false]

//undefined 변환
log(JSON.stringify(undefined)); //undefined
log(JSON.stringify([undefined])); //[null]
log(JSON.stringify({value: undefined})); //{} (프로퍼티 값과 이름 둘 다 제외됨)

//두 번째 파라미터에 함수 작성
//함수에서 리턴한 값을 변환 값으로 사용
//값을 리턴하지 않거나 undefined를 return하면 최종 데이터에서 제외
function replacer(key, value) {
  if (typeof value === "string") {
    return undefined;
  }
  return value;
}

var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
log(JSON.stringify(foo, replacer)); //{"week":45,"month":7}

//두 번째 파라미터에 배열 작성
//이름이 값은 것만 반환
log(JSON.stringify(foo, ['week'])); // {"week":45}

//세 번째 파라미터 : 가독성
```

### parse()

JSON → JS.

```jsx
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj);
// { result: true, count: 42 }

console.log(obj.count);
// expected output: 42

console.log(obj.result);
// expected output: true

//두 번째 파라미터 작성
//파싱한 오브젝트를 하나씩 읽어가면서 두 번째 파라미터의 함수를 실행하여 결과에 반영
//값을 리턴하지 않거나 undefined를 return하면 최종 데이터에서 제외
```

❗ 파싱 대상이 서버에서 받은 데이터일 때, try-catch문을 필수적으로 사용한다.
