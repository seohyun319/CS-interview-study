## Async/Await

- 비동기 코드를 작성하는 새로운 방법.
- promise기반
- function 키워드 앞에 async를, function 내부의 promise를 반환하는 비동기 처리 함수 앞에 await를 붙이면 됨.
- Promise보다 비동기 코드의 겉모습이 깔끔하다는 장점

<br />

- `promise`로 구현

```js
function makeRequest() {
  return getData()
    .then((data) => {
      if (data && data.needMoreRequest) {
        return makeMoreRequest(data)
          .then((moreData) => {
            console.log(moreData);
            return moreData;
          })
          .catch((error) => {
            console.log("Error while makeMoreRequest", error);
          });
      } else {
        console.log(data);
        return data;
      }
    })
    .catch((error) => {
      console.log("Error while getData", error);
    });
}
```

- `async/await` 구현

```js
async function makeRequest() {
  try {
    const data = await getData();
    if (data && data.needMoreRequest) {
      const moreData = await makeMoreRequest(data);
      console.log(moreData);
      return moreData;
    } else {
      console.log(data);
      return data;
    }
  } catch (error) {
    console.log("Error while getData", error);
  }
}
```
