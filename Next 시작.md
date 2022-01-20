# Next 시작
```
npx create-next-app@latest
# or
yarn create next-app
```
- TypeScript 프로젝트로 시작하려면 다음 --typescript플래그를 사용
```
npx create-next-app@latest --typescript
# or
yarn create next-app --typescript
```

```
code 프로젝트 명
// visual studio 새 창에서 프로젝트 열림
```

```
npm run dev // 시작
yarn dev
```

# Next.js 특징
- 사전 렌더링(pre-rendering)
  - 정적 생성(권장, 성능상의 이유로): HTML은 빌드 시 생성되며 각 요청에서 재사용됩니다.
  - 서버 측 렌더링(SSR): HTML은 각 요청에 대해 생성됩니다.
