# Server Side Rendering
### 1. Client Side Rendering
- 페이지의 내용을 브라우저에서 그림
### 2. Server Side Rendering
- 페이지의 내용을 서버에서 다 그려서 브라우저로 던져줌
- 아무것도 안보이다가 한번에 뜸!
- 사용 목적
  - 검색 엔진 최적화: 네이버와 같은 검색 사이트에서 검색했을 때 결과가 사용자에게 많이 노출될 수 있도록 최적화 하는 기법
    - 정보가 들어간 html이 쭉 뜨기 때문! 
  - og(Open Graph): sns에서 링크 공유 시 해당 웹 사이트의 정보를 이미지와 설명으로 표시, og에 효율적
  - 빠른 페이지 렌더링
   (서버에서 다 그려서 브라우저로 보내주기 때문에 사용자 입장에서는 화면에 유의미한 정보가 표시되는 시간이 빨라지는 것)
- 단점
  - api 속도 느리면 아무것도 안보임...계속 흰 화면

![image](https://user-images.githubusercontent.com/61729276/151116500-aa53ea73-76fa-4e73-bc43-eb8f4769053d.png)

### 3. getServerSideProps()
- 이 페이지가 오직 server side render만 할 수 있도록 선택가능
- 페이지가 유저에게 보여지기 전에 props를 받아오는 function을 만드는 것!
```javascript
// pages/index.js

export default function Home({results}){...}

export function getServerSideProps(){
  //여기 코드는 서버에서만(클라이언트x) 돌아간다, user에게 안보임, 여기에 api key 넣으면 숨길 수 있음!
  // 함수 이름 중요, export도 빼먹으면 안돼!
  const { results } = await (await fetch(`http://localhost:3000/api/movies`)).json();
  return {
    props: {
      results, //여기 results가 위의 Home에 props로 들어간다
    }
  }
}
```
### 4. 진행 순서 
1. _app.js에 pages/index.js 불려가고, Home이 _app.js의 `<Component>` 자리에 들어감
2. 그리고 getServerSideProps 호출, nextjs는 우리가 getServerSideProps를 사용할 거라는 걸 알게되고
3. api에서 뭔가 호출, 그 후에 이 props를 return
4. 그러면 next.js가 그 props를 `<Component {...pageProps} />`에서 `pageProps` 자리에 넣을 거임!
 
### 5. ERROR : Only absolute URLs are supported
- `fetch("/api/movies")`에서 이 주소는 front에서만 작동
- http://localhost:3000/api/movies 이렇게 써줘야함!

# 6. nextjs의 SSR, 완전 멋진 점!
> 서버에서 props로 result 받아오고, reactjs가 hydrate(흡수)해서 쓴다!   
> Home 함수에서 {results} 받아서 map 돌려서 사용한다!(reactjs가 hydrate해서 쓰는 부분)
