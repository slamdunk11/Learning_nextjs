# Layout
```javascript
  import Navbar from './navbar'
  import Footer from './footer'
  
  export default function Layout({children}){
    return(
      <>
        <Navbar />
        <main>{children}</main>
        <Footer />
      </>
    )
  }
```

# Custom App
```javascript
// pages/_app.js

import Layout from '../components/layout'

export default function Myapp({component, pageProps}){
  return(
    <Layout>
      <Component {...pageProps} />
    </Layout>
  )
}
```

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
