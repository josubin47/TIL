# Global 오브젝트

모든 <script>를 통해 하나만 존재한다. new 연산자로 인스턴스 생성 불가. 단 하나만 존재하기 때문에 생성할 필요도 없음. 모든 코드에서 공유한다. 이름은 있지만 오브젝트 실체가 없다. 오브젝트를 작성(사용)할 수 없다.

- NaN, infinity, indefined
- 상수 개념으로 사용 (외부에서 프로퍼티 값 변경 불가)
- delete 연산자로 삭제 불가

## Global과 window의 관계

- 글로벌 : JS가 주체
- window : window가 주체

주체는 다르지만 글로벌 오브젝트의 프로퍼티와 함수가 window 오브젝트에 설정된다. 글로벌 오브젝트는 실체가 없으므로 함수와 프로퍼티가 어딘가에 저장되어 있어야 하기 때문에 window 오브젝트에 저장되어 있다. 따라서 글로벌 오브젝트의 프로퍼티를 window 오브젝트에서 가져올 수 있다. → Host 오브젝트 개념

> use strict 환경에서는 window.undefined처럼 오브젝트를 사용해야 하며 undefined처럼 프로퍼티 이름만 사용할 수 없습니다.
> 

### parseInt()

### parseFloat()

### isNaN()

숫자 값이 아니면 true, 숫자 값이면 false.

```jsx
log(null) //false
log(NaN === NaN) //false -> 설계 실수 (ES6의 Object.is() 사용)
```

> NaN 비교 시에는 ES6의 Object.is()를 사용하는 게 안전하다.
> 

### isFinite()

값이 infinity, NaN이면 false를 반환, 유한이면 true 반환. 값이 숫자로 변환되면 숫자로 인식한다.

### encodeURI()

### encodeURIComponent()

### decodeURI()

### decodeURIComponent()

### eval()

파라미터의 문자열을 JS 코드로 간주하여 실행한다. 실행 결과를 반환 값으로 사용한다. 값을 반환하지 않으면 undefined 반환. 보안에 문제가 있다고 알려져 있어 사용을 권장하지 않는다.