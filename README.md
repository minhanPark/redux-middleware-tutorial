# Redux-middleware-tutorial

## 리덕스에 미들웨어 적용시키기

```js
// index.js
import { createStore, applyMiddleware } from "redux";

const store = createStore(
  rootReducer,
  composeWithDevTools(applyMiddleware(logger, ReduxThunk, sagaMiddleware))
);
```
redux에서 applyMiddleware를 갖고와서 미들웨어들을 넣어주면 됨

## 제너레이터 함수

```js
// Generator function

function* idMaker(){
  var index = 0;
  while(index < 3)
    yield index++;
}

var gen = idMaker();
```

제너레이터 함수는 바로 호출되지 않고, 함수를 위한 이터레이터 객체가 반환됨.  
이 이터레이터에 **next()메서드를 이용하면 제너레이터함수가 실행되어 yield문을 만날때 까지 진행이됨.**  
계속 next 메서드를 통해서 멈췄던 부분에서 재실행하게 되고, next는 **yield값인 value**와 **모든 yield문의 실행여부를 표시하는 done(불린값)**을 가진 객체를 반환함. 

```js
console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // undefined
```

## redux-thunk와 redux-saga

비동기 작업을 처리할 때 redux-thunk는 일반함수로 이루어져 있기때문에 간단하다는 장점이 있음. redux-saga는 제너레이터 함수를 이용하기 때문에 진입장벽이 있지만 복잡한 상황에서 더욱 효울적으로 작업을 관리할 수 있음.