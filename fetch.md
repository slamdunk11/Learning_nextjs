# 1. fetch 사용방법
```javascript
(async() => {
  const {results} = await (await fetch(`api주소`)).json();
})()
```
