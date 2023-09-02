---
layout: post
title: "Typescript"
date: 2023-04-11 16:00:00 +0800
last_updated: 2023-09-02 16:00:10 +0800
---

### 一些比較特殊不常見的型別

<br>

> 目前已經有相當大一部分的第三方 module 都已經使用 Typescript  
> 所以有很多繼承自 module 的 props 都可以在 source code 中直接找到它的型別  
> 或是直接將 component 的型別 import 進程式碼的作法

- extends 型別
```js
import { IconProps as defaultIconProps } from '@material-ui/core'
...
export interface IconProps extends defaultIconProps {
  ...
}
```

- `style` for styled-components
```js
import { CSSProperties } from 'react'
...
style?: CSSProperties
```

- `children` & `element`
- `ReactNode`, `ReactElement`, `ReactChildren`
  - 我的理解是要根據不同的 props 需要去選擇上述的型別
  - `ReactElement`基本上只包含 type、props、key 三個屬性，在 React 中幾乎和`JSX.Element`等價
  - `ReactNode`則是一個聯合型別，當中包含`ReactElement`
  - `ReactChildren`比較少見，但我尚未釐清它的定義就不贅述

<br>

- React ref
```js
import { LegacyRef } from 'react'
...
refs?: LegacyRef<Element>
```

- React event
  - `FocusEvent`, `KeyboardEvent`, `MouseEvent`, `SyntheticEvent` ...
  - 根據需求選擇

<br>

- `setTimeout()` & `setInterval()`
```js
let timer: NodeJS.Timeout
```

- `response` from `Promise`
```js
const tplResponse = new Response()
...
response: typeof tplResponse
```

<br>

在學習 Typescript 的過程中曾經聽到一個觀念:
> 在使用 Typescript 時要盡可能避免`any`型別的出現，否則使用 Typescript 是毫無意義的

但是在專案中其實存在很大量的物件，它的資料結構可能非常複雜  
或是它是透過 fetch http request 得來的資料，有的時候並沒有辦法完全的剖析它的資料型別和結構  
但為了避免使用`any`我可能會定義一個全域的型別去賦予這樣的物件。
```js
export interface Prop {
  [key: string]: any
}
// or
Record<string, any>
```

<br>

### intellisense

在使用 vs code 開發 Typescript 時，export 的變數或是物件在賦予型別的時候，可以加上註解說明  
但是需要遵照 JSDoc 的規則，使用前綴 2 個`*`的多行註解  
範例如下:  
```js
export interface Type {
  /** 正確 */
  correctType: string
  /* 錯誤 */
  wrongType: string
}
```
![intellisense_correctType.png](/assets/intellisense_correctType.png)  
![intellisense_wrongType.png](/assets/intellisense_wrongType.png)

<br>

### Utility Types

一些特殊功能的 Types

- `Partial`把 interface 中**必填**的屬性改為**非必填**
- `Required`把 interface 中**非必填**的屬性改為**必填**
- `Pick`在 interface 中**選擇**屬性
- `Omit`在 interface 中**剔除**屬性

<br>