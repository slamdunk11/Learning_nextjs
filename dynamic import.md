# 1. dynamic import 사용법
```javascript
  import dynamic from 'next/dynamic'
  
  const Dynamiccomponent = dynamic(() => import('../components/hello')) // 경로 명시적으로! 템플릿 문자열이나 변수 x
  // dynamic()은 React.lazy와 유사하게 사전 로드가 작동하도록 모듈의 최상위 수준에 표시되어야 하므로 React 렌더링 내부에서 사용 x
  function Home(){
    return (
      <div>
        <Header />
        <DynamicComponent />
        <p>HOME PAGE is here!</p>
      </div>
    )
  }
  
export default Home
```

# 2. custom loading componet
- 동적 구성 요소가 로드되는 동안 로드 상태를 렌더링하기 위해 선택적 로드 구성 요소를 추가할 수 있습니다.
```javascript
import dynamic from 'next/dynamic'
  
const DynamicComponentWithCustomLoading = dynamic(() => import('../components/hello'),
{loading: () => <p>...</p>}
)

function Home() {
  return (
    <div>
      <Header />
      <DynamicComponentWithCustomLoading />
      <p>HOME PAGE is here!</p>
      </div>
    </div>
  )
}

export default Home
```

# 3. With no SSR
- 항상 서버 측에 모듈을 포함하고 싶지는 않을 수 있습니다. 
- 예를 들어 모듈에 브라우저에서만 작동하는 라이브러리가 포함된 경우입니다.

```javascript
import dynamic from 'next/dynamic'

const DynamicComponentWithNoSSR = dynamic(() => import('../components/hello3'),
{ ssr : false }
)

function Home(){
  return(
    <div>
      <Header />
      <DynamicComponentWithNoSSR />
      <p>HOME PAGE is here!</p>
    </div>
  )
}

export default Home
```
