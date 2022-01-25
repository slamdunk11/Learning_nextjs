# Layout
- custom app component를 사용할 때 흔히 쓰는 패턴 ⇒ layout 패턴
- components폴더에 Layout.js라는 react component
```javascript
// components/Layout.js
  import Navbar from './navbar'
  import Footer from './footer'
  
  export default function Layout({children}){ 
  // children은 react.js가 제공하는 prop, 하나의 component를 다른 component에 넣을 때 쓸 수 있다
    return(
      <>
        <Navbar />
        <main>{children}</main>
        <Footer />
      </>
    )
  }
```
```javascript
// pages/_app.js(Custom App)

import Layout from '../components/layout'

export default function Myapp({component, pageProps}){
  return(
    <Layout>  // _app.js에 Layout 추가
      <Component {...pageProps} />  // Layout의 children이 이 Component
    </Layout>
  )
}
```
- 이런 Layout패턴을 쓰는 이유?
  -  너무 큰 _app.js를 원하지 않아서, 여기는 global로 import해야할 것들이 많기 때문에 (Google Analytics, 검색엔진, 스크립트 분석)
     _app.js에 NavBar, Footer를 넣기 보다는 Layout.js에 넣는다!

# 페이지 하나에 여러 레이아웃이 필요한 경우?
```javascript
import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'

export default function Page(){
  return{}
}

Page.getLayout = function getLayout(page){
  return(
    <Layout>
      <NestedLayout>{page}</NestedLayout>
    </Layout>
  )
}
```
```javascript
// pages/_app.js
export default function MyApp({Component, pageProps}){
  const getLayout = Component.getLayout || ((page) => page)
  
  return getLayout(<Component {...pageProps} />)
}
```
