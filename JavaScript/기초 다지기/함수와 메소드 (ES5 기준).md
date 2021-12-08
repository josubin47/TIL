# 함수와 메소드 (ES5 기준)

## 함수

오브젝트에 연결한다.

**ex) Object.create()**

## 메소드

오브젝트의 prototype에 연결한다.
**ex) Object.prototype.toString()**

## 왜 둘을 구분해야하는가?

JS 코드 작성 방법이 다르기 때문. 함수는 파라미터에 값을 작성하고 메소드는 메소드 앞에 값을 작성한다.

```jsx
String.fromCharCode(49, 65); //함수
"abc".toString(); //메소드
```