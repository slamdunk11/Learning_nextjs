# Seo
```javascript
// components/Seo.js
import Head from "next/head";

export default function Seo({title}){ // title이라는 props받아서 페이지별로 쓸 수 있다
    return <Head><title>{title} | Next Movies</title></Head>
}
```
```javascript
// index.js home페이지
import Seo from "../components/Seo";

export default function Home(){
    return (
    <div>
        <Seo title="Home"></Seo> //이렇게 props!
        <h1>Hello</h1>
        
    </div>);
}
```

이걸 Layout에 적용할 수도 있다!

