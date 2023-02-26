# 기본값 매개변수 (default parameter)

매개변수 기본값 설정은 함수를 훨씬 안전하게 만들어 준다.

여러 방법이 있지만 기본값 매개변수(default parameter)를 사용하면 함수를 더욱더 명시적이고 안전하게 초기화 시킬 수 있다. 특히 매개변수를 객체로 받는 경우의 에러 발생 확률을 더욱 낮춰준다.

```jsx
function createCarousel({
  margin = 0,
  center = false,
  navElement = "div",
} = {}) {
  // ..some code
  return {
    margin,
    center,
    navElement,
  };
}

createCarousel();
```

에러 처리 함수를 만들어 같이 사용한다면 훨씬 안전하게 쓸 수 있다.

```jsx
const required = (argName) => {
  throw new Error("required is " + argName);
};

function createCarousel({
  items = required("items"),
  margin = 0,
  center = false,
  navElement = "div",
} = {}) {
  // ... some code

  return {
    margin,
    center,
    navElement,
  };
}
```
