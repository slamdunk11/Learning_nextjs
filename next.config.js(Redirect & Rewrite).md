# 본격적으로 들어가기 전에...
### 1. 기타 내용
- public폴더의 파일은 가져올 때 경로가 `/파일명.확장자` 이거면 된다
(..public/파일명 이런 거 안해도 됨)
```javascript
// public 폴더 안의 /vercel.svg
<img src="/vercel.svg" />
```

- next.js에서는 img 태그 x, a 태그 -> `<Link><a></a></Link>`였던 것처럼
- img태그 -> `<Image />` 로 써야한다??, 그런데 로컬이미지, 원격이미지를 사용할 때 복잡해질 수도 있다

# Redirect & Rewrite
### 1. Redirect
- next.config.js파일에 Redirect 넣어주면 가능!
- redirects는 return한다 배열 안의 오브젝트를...!
- redirects를 여러개 하고 싶으면 배열 안의 오브젝트를 여러개 만들면 됨!
  (지금 서버가 실행되고 있음...client and server)
  
```javascript
// next.config.js

module.exports = {
  reactStrictMode: true,
  //redirection에 필요한 건 이게 다
  async redirects() {
    return [
      {
        source: "/contact", // 유저가 contact주소를 친다면
        destination: "/form", // 우리는 유저를 form이라는 destination(어디든 가능)으로 보낸다
        // destination: "https://nomadcoders.co",
        permanent: false, 
        // 영구적인지 아닌지에 따라, 브라우저나 검색엔진이 이 정보를 기억하는 지 결정됨
        // localhost:3000/contact 치면 http://localhost:3000/form 여기로 간다!
      },
      {
        // source에 `:path`를 하면 destination에도 같은 `:path`로 간다
        source: '/old-blog/:path', // :path 부분에 id, 숫자 같은 것 넣는다
        // source: '/old-blog/:path*', destination: '/new-sexy-blog/:path*' 
        // *을 넣어주면 모든 걸 catch한다
        (:path일 때는 /1122 이거 하나만, :path*일 때는 /1122/comments/1245)
        destination: '/new-sexy-blog/:path', // 똑같은 :path 즉 id가 온다!!!!
        permanent: false, 
      },
    ]
  }
}
//  next.config.js 파일 변경해서 적용하려면 서버 재시작해야 효과 적용됨
    (ctrl c하면 나와짐...이거 하고 yarn dev하기)
```
### 2. Rewrite
- next.config.js파일에 Rewrite 넣어주면 가능!
- Rewrites는 return한다 배열 안의 오브젝트를...!
- request에 mask를 씌우는 것 같은 rewrite
- redirect가 url변화하는 게 다 보인다면 rewrite는 보이지 않는다!

### 3. API Key를 숨겨보자!
- api 숨기고 싶은 이유 
  - api키를 모두에게 공개하고 싶지 않아...돈 내고 api key 사는 경우도 있어...
  - api 사용량 제한되어있어서 예를 들어 1분에 100번밖에 못 불러와...사람들이 API Key 알게되서 남용할 경우, 모두 개인 목적으로 쓰게 될 경우 사용에 제한이 걸릴 수도 있어

#### 3-1. next.config.js 파일에 rewrite를 사용해서 API Key 숨겨보자!
```javascript
// next.config.js
const API_KEY = 'e35468655a42727015635393664';
module.exports = {
  reactStrictMode: true,
  async redirects() {
   ...
  },
  async rewrites() {
    return [{
      source: "/api/movies",
      destination: `https://api.themoviedb.org/3/movie/popular?api_key=${API_KEY}`
    }];
  },
};
```
```javascript
// pages.index.js
export default function Home() {
...
  useEffect(() => {
    (async () => {
      const { results } = await (await fetch(`/api/movies`)).json();
    })();
    // fetch부분의 url을 rewrites의 source로 바꿔준다!
    // 이러면 데이터도 잘 받아오고, network의Request URL이 http://localhost:3000/api/movies 이렇게 뜬다
    // 바로 next.js의 request masking!
    // API Key 노출되지 않는다!!!
    // 실제로 검색창에 http://localhost:3000/api/movies(우리 서버에 mask된 url)이라는 url에 방문하면 response 뜬다!
    ...
  }, []);
...
}
```
### 3-2. API Key를 숨겨주는 다른 방법! .env 파일을 이용한다!
- next.config.js에 const API_KEY = process.env.API_KEY; 
```javascript
// next.config.js
const API_KEY = process.env.API_KEY; 

module.exports = {
  reactStrictMode: true,
  async rewrites() {
    return [{
      source: "/api/movies",
      destination: `https://api.themoviedb.org/3/movie/popular?api_key=${API_KEY}`
    }];
  },
};
```
- .env 파일 작성
```javascript
// .env
API_KEY = e35468655a42727015635393664
```
- .gitignore 파일에 .env 추가 → git에 안 올라가도록!
```javascript
// .gitignore
.env
```
