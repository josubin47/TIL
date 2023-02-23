
# SPA 라우팅 구현
리액트의 react-router-dom 라이브러리를 사용할 수 없는 VanillaJS 환경에서 SPA 라우팅을 구현하려면 어떻게 해야 할까?

## SPA 라우팅

사용자 관점에서는 URL과 페이지가 변경되고 있는 것처럼 보이나, index.html 안에서 모든 라우팅이 일어난다.

# History API

History API는 브라우저의 세션 기록에 대한 액세스를 제공한다. 사용자 기록을 앞뒤로 탐색하고 내용을 조작할 수 있는 메소드들을 담고 있다.

## history.pushState()
pushState()를 사용하면 갈아끼울 컴포넌트의 새로운 url과 제목, 데이터를 저장하고 지정할 수 있다. 주소 데이터는 history.state에 저장된다. 뒤로가기와 앞으로가기를 눌러도 새로고침 되지 않고 주소만 바뀐다. 다만 새로고침을 누르는 경우는 서버사이드 랜더링으로 해결해야 한다.

```jsx
// history.pushState(전달할 새 데이터 객체, 변경 제목, 변경 url)
history.pushState({page: 1}, "title 1", "?page=1")

```

## history.replaceState()

replaceState()는 pushState() 다르게 이전 주소로 돌아가는 기능(뒤로가기 활성화)을 제공하지 않는다. 이전 주소 기록을 없애고 바꿀 주소만 남기기 때문이다.

```jsx
// history.replaceState(전달할 새 데이터 객체, 변경 제목, 변경 url)
history.replaceState({page: 3}, "title 3", "?page=3")

```

## popstate 이벤트

브라우저에서 history 엔트리에 변경 사항이 생길 때 발생하는 이벤트.

pushState()와 replaceState() 실행 시에는 발생하지 않고, pushState()나 replaceState()로 주소를 바꾼 후 뒤로가기나 앞으로 가기를 눌렀을 때 발생한다. popstate 이벤트 발생 후 history.state에 접근하면 이전 state를 가져올 수 있다.

```jsx
window.onpopstate = (event) => {
  console.log(`location: ${document.location}, state: ${JSON.stringify(event.state)}`);
};
history.pushState({ page: 1 }, "title 1", "?page=1");
history.pushState({ page: 2 }, "title 2", "?page=2");
history.replaceState({ page: 3 }, "title 3", "?page=3");
history.back(); // Logs "location: <http://example.com/example.html?page=1>, state: {"page":1}"
history.back(); // Logs "location: <http://example.com/example.html>, state: null"
history.go(2);  // Logs "location: <http://example.com/example.html?page=3>, state: {"page":3}"

```


# 구현하기

## Router.js

### 1. url 정보를 담고 있는 routes 배열 생성

routes 배열을 생성하여 필요할 때마다 url을 하나씩 추가할 수 있게 하였다.

path에는 url을 정규표현식으로 작성하였고 view에는 이동할 페이지를 넣어주었다.

```jsx
const routes = [
    { path: /^\/$/, view: Home },
    { path: /\/test1/, view: Test1 },
    { path: /\/test2/, view: Test2 },
    { path: /^\/test\/(\d+)$/, view: TestA },
];
```

### 2. 현재 url과 일치하는 route 정보를 찾는 함수 작성

routes 배열에서 location.pathname과 일치하는 route 정보를 찾아 반환한다.

```jsx
const findMatchRoute = () => {
    return routes.find((route) => route.path.test(location.pathname));
};
```

### 3. render 함수 작성

뷰 인스턴스를 생성하고 뷰.js의 render 함수를 호출해 뷰를 렌더링하는 로직을 담고 있다. 각 뷰마다 공통적으로 render 함수를 가지도록 설계하였다.

매개변수는 필요시 로직을 추가 구현하여 사용한다.

```jsx
this.render = ($data) => {
    const $view = findMatchRoute().view;
    const app = new $view();
    document.querySelector("#app").innerHTML = app.render();
};
```

### 4. navigate 함수 작성

history.pushState()를 이용해 url 정보를 바꿔주는 함수이다. url 정보를 바꾸면서 3번에 작성한 render 함수를 호출하여 뷰를 렌더링한다.

```jsx
this.navigate = (url) => {
    history.pushState({ url: url }, "", url);
    this.render();
};
```

### 5. 라우터 초기화 함수 작성

app.js 초기화 시에 호출할 라우터 초기화 함수이다.

뒤로가기를 눌렀을 때 onpopstate를 통해 url과 맞는 뷰가 렌더링되도록 처리해준다.

```jsx
this.currentPage = "/";

this.init = () => {
    this.navigate(this.currentPage);

    window.onpopstate = (e) => {
      this.navigate(location.href);
    };
};
```

### [작성 중인 코드 ✏️✏️](https://github.com/josubin47/VanillaJS-study)


### 참고

- [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)

- [popstat event](https://developer.mozilla.org/en-US/docs/Web/API/Window/popstate_event)
