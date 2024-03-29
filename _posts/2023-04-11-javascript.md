---
layout: post
title: "Javascript"
date: 2023-04-11 16:00:10 +0800
last_updated: 2023-04-11 16:00:10 +0800
---

### map() 和 forEach() 的區別

`map()`會回傳一個新的陣列，而`forEach()`只是單純的for操作

<br>

### push()、pop()、shift()、unshift()

- `push()`
```js
const a = [0, 1]
console.log(a.push(2)) // 3 -> 回傳陣列的新長度
console.log(a) // [0, 1, 2] -> 在陣列的最後增加一個新的元素
```

- `pop()`
```js
const a = [0, 1, 2]
console.log(a.pop()) // 2 -> 回傳被移除的元素
console.log(a) // [0, 1] -> 移除陣列的最後一個元素
```

- `shift()`
```js
const a = [0, 1, 2]
console.log(a.shift()) // 0 -> 回傳被移除的元素
console.log(a) // [1, 2] -> 移除陣列的第一個元素
```

- `unshift()`
```js
const a = [0, 1, 2]
console.log(a.unshift(3, 4)) // 5 -> 回傳陣列的新長度
console.log(a) // [3, 4, 0, 1, 2] -> 在陣列開頭的增加新的元素
```

<br>

### slice()、splice()、split()

- `slice()`可使用在 array 和 string 上
```js
const arrayA = ['a', 'b', 'c', 'd', 'e']
console.log(arrayA.slice(1, 3)) // ['b', 'c'] -> 回傳 [1]~[3](不含3) 之間的元素
console.log(arrayA) // ['a', 'b', 'c', 'd', 'e'] -> 不會改變 arrayA 的值
```
```js
const stringA = 'How Are You'
console.log(stringA.slice(1, 3)) // 'ow' -> 回傳 [1]~[3](不含3) 之間的字串
console.log(stringA) // 'How Are You' -> 不會改變 stringA 的值
```

- `splice(startIndex, removeCount, newItem1, ...)`
- 可以有多個 props
- startIndex(required): 從該元素開始要被移除
- removeCount(optional): 要被移除的元素數量
- newItem(optional): 取代掉被移除的元素，可以是多個
```js
const arrayB = ['a', 'b', 'c', 'd', 'e']
console.log(arrayB.splice(1, 2, 'f')) // ['b', 'c'] -> 回傳被移除的元素
console.log(arrayB) // ['a', 'f', 'd', 'e'] -> 會改變 arrayB 的值
```
```js
const arrayC = ['a', 'b', 'c', 'd', 'e']
console.log(arrayC.splice(1)) // -> ['b', 'c', 'd', 'e']
console.log(arrayC) // ['a']
```
```js
const arrayD = ['a', 'b', 'c', 'd', 'e']
console.log(arrayD.splice(1, 2)) // ['b', 'c']
console.log(arrayD) // ['a', 'd', 'e']
```

- `split()`
```js
const stringB = 'How Are You'
console.log(stringB.split(' ')) // ['How', 'Are', 'You'] -> 回傳一個新的陣列，以傳入的分割字串將原本的字串分割
console.log(stringB) // 'How Are You' -> 不會改變 stringB 的值
```

<br>

### sort()

演算法中的`sort()`，有非常多實作方式，有 stable 和 unstable 的區別。  
但是各個Browser執行`sort()`的方式並不一樣，所以需要注意使用時，有沒有必須要 stable 的需求。  
[各 Browser 的 sort() 是否為 stable 的參照](https://stackoverflow.com/a/16479342)

<br>

### Number() 和 parseInt() 的區別
  - Number() 較為嚴格，當轉換值中包含無法轉換的內容時，會直接回傳 NaN
  - parseInt() 遇到無法解析的字元，會停止解析於此字元，並回傳目前為止的結果

```js
console.log(parseInt('10px')) // 10
console.log(Number('10px')) // NaN
```
<br>

### Map 和 Set

對我來說，最簡單的總結就是，`Map`是各個 key 不會重複的`Object`，而`Set`是各個元素不會重複的`Array`。  

網路上有非常多資源，把這2者的區別和特性寫的非常清楚，這邊就不再贅述:  
- [javascript.info](https://javascript.info/map-set)  
- [漫築蘭格的 medium](https://medium.com/%E6%BC%AB%E7%AF%89%E8%98%AD%E6%A0%BC/js%E4%B8%AD%E7%9A%84-set-%E8%88%87-map-815a9157b3bf)  
- [pjchender 的筆記 map](https://pjchender.dev/javascript/js-map/)  
- [pjchender 的筆記 set](https://pjchender.dev/javascript/js-set/)  

<br>

### && 用法

>數字 0 會被判斷為 false

在使用`map()`時我們會習慣使用 list 的長度判斷是否 render，避免畫面上顯示 0，盡可能在`&&`運算子前確保條件為 boolean

```js
{list.length && list.map(...)} // avoid
{list.length > 0 && list.map(...)} // good
```
<br>

### ||和??的區別

`??`: 當左邊為`null`或`undefined`時回傳右邊

`||`: 當左邊被判定為 false 時回傳右邊 (ex: `null`, `undefined`, `NaN`, `''`, `0`)

<br>

### JSON.stringify()

當物件內的 value 為`undefined`時，在`JSON.stringify()`後 key+value 會一起消失，但是 value 為`null`時會留下 key+value

```js
console.log(JSON.stringify({ a: undefined })) // {}
console.log(JSON.stringify({ a: null })) // {"a":null}
```
<br>

### typeof

```js
typeof NaN // number
typeof null // object
typeof undefined // undefined
```

<br>

### try catch

出現錯誤時及時中斷，並避免後續程式碼被執行。

當`funcB`又被其他 function 呼叫到時，就需要在`catch`的地方再將錯誤`throw`出去

```js
const funcA = () => {
  const error = 'ERROR !'
  throw error
}

const funcB = () => {
  try {
    console.log('funcB start')
    funcA()
    console.log('funcB end') // 這一行不會觸發
  } catch (e) {
    console.warn(e) // 但是會觸發這一行
  }
}
```

<br>

### async function and Promise

>async await 語法算是取得 Promise 結果的一種更簡潔變形體

```js
const fetchFirst = () => {
  return new Promise((resolve, reject) => {
    resolve()
  })
}

const fetchSecond = () => {
  return new Promise((resolve, reject) => {
    resolve()
  })
}

fetchFirst()
  .then(res => {
    // 取得第一筆資料，但同時我必須在 then 這個巢狀程式碼中去做第二部分的處理
    console.log(res)
    return fetchSecond()
  })
  .then(res => {
    // 這時候我才能拿到第二筆資料然後處理
    console.log(res)
  })

const fetchData = async () => {
  const firstData = await fetchFirst() // 取得第一筆資料
  console.log(firstData)
  const secondData = await fetchSecond() // 取得第二筆資料
  console.log(secondData)
}

fetchData()
```

一個比較不常見的例子
```js
const funcA = async () => {
  console.log('funcA start')
  await funcB()
  console.log('funcA end')
}
const funcB = async () => {
  console.log('funcB')
}
funcA()
console.log('start')

// funcA start
// funcB
// start
// funcA end
```

- `Promise.all` -> 並行處理多個 Promise
- 當要執行的 Promise 數量較多時可以減少執行時間

```js
const a = await fetchA()
const b = await fetchB()
const c = await fetchC()

const [a, b, c] = await Promise.all([
  async () => {
    const a = await fetchA()
    return a
  },
  async () => {
    const b = await fetchB()
    return b
  },
  async () => {
    const c = await fetchC()
    return c
  }
])
```

<br>
