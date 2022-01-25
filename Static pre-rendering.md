# Static pre-rendering
### 1. create react app → CSR(Client Side Rendering)
- root div(비어있음, 유일한 HTML) 제외하고는 전부 javascript
- javascript가 모든 UI 만듦, 브라우저 HTML 가져올 때 비어있는 root div 가져옴
- 그 후 모든 javascript와 react.js 실행하고 앱이 유저에게 보임(UI 만듦)

### 2. next.js → SSR(Server Side Rendering)
- 실제 소스코드에 실제 HTML 존재, 페이지 미리 렌더(Static pre-rendering)
- next.js가 초기 상태로 미리 렌더링함(count = 0)
- 이후에 react가 넘겨받아서 잘 작동

- #### hydration : react.js를 프론트엔드 안에서 실행하는 것
  - 생성된 각 HTML은 해당 페이지에 필요한 최소한의 JavaScript 코드와 연결됩니다. 
    브라우저에서 페이지를 로드하면 해당 JavaScript 코드가 실행되고 페이지가 완전히 대화식으로 만들어집니다.
  - Each generated HTML is associated with minimal JavaScript code necessary for that page. 
    When a page is loaded by the browser, its JavaScript code runs and makes the page fully interactive.

- next.js는 react.js를 백엔드에서 동작시켜서 페이지를 미리 만드는 데 이게 component를 render시킴
- component render 된 게 HTML 되고 next는 HTML을 데이터 소스코드에 넣어줌 
  → 그래서 유저는 javascript와 react가 로딩 x ⇒ 콘텐츠는 볼 수 o
- 이후에 react 돌아감!
