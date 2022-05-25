


### API

#### fetch()

response.ok > 2xx內的範圍為true

> 比較 $.ajax

> 比較 $.get, $.post

#### Server-Sent Events
long polling

#### WebSocket


`based on ES6`


### Prototype Pollution

``` js
let dict = Object.create(null) // 創造一個空的物件(沒任何方法), 物件裡沒有 __proto__ 這個key
let dict = new Object() // 創造一個新物件, 有物件方法但沒有內容, 可以汙染 __proto__
```

