# 1. 그냥 css 추가하는 법
```javascript
<Link href="/about">
  <a style={{}}>About</a>
</Link>
```

# 2. CSS modules
### 2-1. CSS modules 사용하는 법
- 파일명: NavBar.module.css
- 이 파일에서 쓴 클래스명 다른 파일에서 써도 문제 안생김! 독립적임!
- 나중에 작성후 개발자 도구로 살펴보면 nav라는 클래스 뒤에 랜덤 문자들이 덧붙여져 생성됨-> 완전 다른 클래스명이 되어버려서 괜찮!
```css
/* NavBar.module.css*/
.nav{
  display: flex;
  ...
}
.active{
  color: tomato;
}
.link{
  text-decoration: none;
}
```
- 위의 NavBar.module.css파일을 Navbar.js에 import 시켜서 사용

```javascript
// Navbar.js
import styles from "./NavBar.module.css";
...
<nav className={styles.nav}>
...
</nav>
```
```javascript
// Navbar.js 조건부로 class적용도 가능
import styles from "./NavBar.module.css";
<nav>
  <Link href="/">
    <a className={router.pathname === "/" ? styles.active : ""}>home</a>
  </Link>
  <Link href="/about">
    <a className={router.pathname === "/about" ? styles.active : ""}>about</a>
  </Link>
</nav>
```

### 2-2. CSS modules에서 class 2개 적용하고 싶을 때
```javascript
import styles from "./NavBar.module.css";
<nav>
  <Link href="/">
    <a className={`${styles.link} ${router.pathname === "/" ? styles.active : ""}`}>home</a>
  </Link>
  <Link href="/about">
    <a className={[styles.link, router.pathname === "/about" ? styles.active : ""].join(" ")}>about</a>
  </Link>
</nav>
```
# 3. Styles JSX
### 3-1. Styles JSX 사용법
- style 태그에 jsx라는 props 추가
- style 태그 중괄호({}), 백틱(``)안에 클래스 추가
- 여기도 클래스명 독립적임, 다른 데(부모 컴포넌트)서 같은 클래스명 써도 개발자도구로 확인해보면 jsx-dkdk88 이런 클래스명임 
- 오직 이 컴포넌트 안에서만 쓰임
```javascript
<nav>
  <Link href="/">
    <a>home</a>
  </Link>
  <Link href="/about">
    <a>about</a>
  </Link>
  <style jsx>{`
    nav {
      background-color: tomato;
    }
    a{
        text-decoration: none;
      }
  `}</style>
</nav>
```
### 3-2. Styles JSX 조건부 사용법
```javascript
<nav>
  <Link href="/">
    <a className={router.pathname === "/" ? "active" : ""}>home</a>
  </Link>
  <Link href="/about">
    <a className={router.pathname === "/about" ? "active" : ""}>about</a>
  </Link>
  <style jsx>{`
    nav {
      background-color: tomato;
    }
    a{
        text-decoration: none;
      }
    .active {
      color: blue;
      // color: ${props.color}; props를 받고 싶을 때
    }
  `}</style>
</nav>
```

# 4. Global Styles
- App Page와 App Component(_app.js라는 파일로 전역 스타일 설정 가능!)의 개념 이해 필요
### 4-1. Global Styles 약간 부족한 방법
- index.js페이지 파일에서 style 태그에 global이라는 prop 추가
```javascript
 <div>
  <NavBar />
  <h1>Hello</h1>
  <style jsx global>
    a{
      color: white;
    }
  </style>
 </div>
 
 // 이렇게만 하면 about페이지로 넘어갔을 때 color: white 작동 x, 페이지별로 작동되는 next의 속성 때문
```

### 4-2. Global Styles 진짜 방법(App Component(_app.js)이용해서)
- pages폴더 안에 _app.js 라는 파일 만들기(꼭 이 이름이어야 함)
- next는 _app.js 를 먼저 확인하고 다른 페이지를 렌더링한다!
- 스타일뿐만 아니라 전역으로 쓸 컴포넌트도 추가 가능!
- _app.js에서 style 태그에 global이라는 prop 추가하면 전역 스타일
- 혹은 styles폴더에 globals.css파일을 import할 수 있다.(custom App 컴포넌트인 _app.js에만 import가능)
- `import "../styles/globals.css"` 이렇게 삽입 가능

```javascript
//_app.js
// 밑의 함수 App 말고도 CustomApp, MyApp...등 이름 자유롭게 가능
// 프레임워크(next.js)는 내 코드를 불러낸다->props로 내가 작성한 Component, pageProps를 받음
// about 페이지를 렌더하기 전에 about페이지에 있는 About이라는 함수 컴포넌트를 받아내는 것
import NavBar from "../components/NavBar";
export default function App({Component, pageProps}){
  return (
    <>
      <NavBar /> // 페이지마다 써줬던 NavBar컴포넌트 지워줘도 됨
      <Component {...pageProps} /> // 모든 페이지는 NavBar 밑인 여기에 렌더링 될 예정
      <span>hello</span>
      <style jsx global>
        a{
         color: white;
        }
      </style>
      // 이렇게 하면 a태그는 어딜가든 흰색
    </>
  )
}
```
