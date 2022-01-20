# 페이지 url 경로
- pages 폴더에 js파일 생성하기만 하면 파일의 경로가 url 경로가 된다.
- 중간에 폴더를 만들면 폴더까지 url 경로가 된다.
```javascript
// pages 폴더 -> posts폴더 -> first-post.js =>  http://localhost:3000/posts/first-post

export default function FirstPost(){
  return <h1>First Post</h1>
}
```

# Link 컴포넌트
```javascript
import Link from 'next/link

<h1 className="title">
  Read{' '}    // {' '} 여러 줄에 걸쳐 텍스트를 나누는 데 사용되는 빈 공간을 추가합니다.
  <Link href="/posts/first-post">
    <a>this page!</a>
  </Link>
</h1>
```
