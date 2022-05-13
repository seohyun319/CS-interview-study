## Async/Await

- 비동기 코드를 작성하는 새로운 방법.
- promise기반
- function 키워드 앞에 async를, function 내부의 promise를 반환하는 비동기 처리 함수 앞에 await를 붙이면 됨.
  - async: promise를 return.
  - await: promise를 기다림. async로 정의된 함수 안에서만 사용 가능.
- Promise보다 비동기 코드의 겉모습이 깔끔하다는 장점

<br />

- 에러 핸들링

  - `promise`로 구현

        ```js
        const makeRequest = () => {
            try {
            getJSON().then((result) => {
                // this parse may fail
                const data = JSON.parse(result);
                console.log(data);
            });
            .catch((err) => {
                console.log(err)
            })
            } catch (err) {
            console.log(err);
            }
        };
        makeRequest();
        ```

  - `async/await` 구현

        ```js
        const makeRequest = async () => {
        try {
            // this parse may fail
            const data = JSON.parse(await getJSON());
            console.log(data);
        } catch (err) {
            console.log(err);
        }
        };

        makeRequest();
        ```

- 분기 (데이터를 fetch하고 결과를 return하거나 데이터 안의 값을 이용해 더 상세한 정보를 가져올지 결정)

  - `promise`로 구현

    ```js
    const makeRequest = () => {
      return getJSON().then((data) => {
        if (data.needsAnotherRequest) {
          return makeAnotherRequest(data).then((moreData) => {
            console.log(moreData);
            return moreData;
          });
        } else {
          console.log(data);
          return data;
        }
      });
    };
    ```

  - `async/await` 구현

    ```js
    const makeRequest = async () => {
      const data = await getJSON();
      if (data.needsAnotherRequest) {
        const moreData = await makeAnotherRequest(data);
        console.log(moreData);
        return moreData;
      } else {
        console.log(data);
        return data;
      }
    };
    ```

- 중간값 (promise1의 return값을 이용해 promise2를 호출, 두 promise의 결과 이용해 promise3 호출)

  - `promise`로 구현

    ```js
    const makeRequest = () => {
      return promise1().then((value1) => {
        // do something
        return promise2(value1).then((value2) => {
          // do something
          return promise3(value1, value2);
        });
      });
    };
    ```

  - `async/await` 구현

    ```js
    const makeRequest = async () => {
      const value1 = await promise1();
      const value2 = await promise2(value1);
      return promise3(value1, value2);
    };
    ```

참고 링크

- [링크](https://kiwanjung.medium.com/%EB%B2%88%EC%97%AD-async-await-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-promise%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-955dbac2c4a4)
- [링크](https://medium.com/@constell99/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-async-await-%EA%B0%80-promises%EB%A5%BC-%EC%82%AC%EB%9D%BC%EC%A7%80%EA%B2%8C-%EB%A7%8C%EB%93%A4-%EC%88%98-%EC%9E%88%EB%8A%94-6%EA%B0%80%EC%A7%80-%EC%9D%B4%EC%9C%A0-c5fe0add656c)
