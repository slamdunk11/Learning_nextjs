# Custom App(_app.js)
### global styles 추가하는 법
- 1차적인 방법: 적용을 원하는 페이지에서 global `<styled jsx global></style>`(⇒ 이러면 이 페이지에만 적용되고 다른 페이지는 적용 x )  
  - 원래 style jsx는 component scoped(컴포넌트 내에서 한정되어 적용된다!, 다른 컴포넌트 스타일 설정 신경 안씀)
  - App Page의 개념
```javascript
export default function Home(){
  return(
  <div>
    <NavBar />  // global(전역) 기준으로 NavBar에 있는 a 태그는 흰색으로 표기된다!(NavBar에 style있다면 NavBar 스타일이 우선되긴 함)
    <h1>Hello</h1>
    <style jsx global>{`
      a{
        color: white;
      }
    `}</style>
    </div>
  )
}
```
- 말 그대로 모든 페이지들에 전역적으로 style 적용하고 싶을 때는? ⇒ Custom App(pages 폴더 안에 _app.js)
  - App Component의 개념(일종의 어떤 컴포넌트의 청사진)
  - 꼭 _app.js의 이름, Nextjs는 다른 한 페이지가 렌더링 되기 전에 App을 먼저 보기 때문, 그리고 나서 다른 페이지 내용물을 _app.js에서 rendering   
  - _app.js로 파일을 만드는 순간 위의 과정은 내가 뭘 할 것도 없이 자동적으로 물 밑에서 일어난다...!
  - 그리고 styles폴더의 globals.css를 _app.js에 import할 수 있다!(다른 파일에는 globals.css import 불가능, 에러남)
    (만약 css파일을 컴포넌트에 import하고 싶으면 ~.module.css 여야함)
```javascript
// pages폴더 안에 _app.js
// function 이름은 상관x, App, MyApp, CustomApp...기타 등등

// 만약 내가 index.js 페이지를 렌더하려고 한다면, index.js의 컴포넌트를 가져다가 App의 props인 Component로 App 함수에 전달해줌
import NavBar from "../components/NavBar"; 
import "../styles/globals.css";  // globals.css import 가능, import만 하면 적용됨

export default function App({Component, pageProps}){
  return (
    <>
      <NavBar /> // 여기에 NavBar 넣어주면 다른 페이지에서 NavBar를 추가하지 않아도 된다!, 모든 페이지는 NavBar 밑의 Component에서 렌더링 될 거니까!
      <Component {...pageProps}/> // _app.js의 App함수는 index.js 페이지를 렌더한다
      <span>hello</span> // 어느 페이지에서건 hello가 보임
      <style jsx global>{` // 여기서 전역적으로 a 태그 흰색!(NavBar에 style있다면 NavBar 스타일이 우선되긴 함)
            a{
                color: white;
            }
        `}</style>
    </>
);
}
```
