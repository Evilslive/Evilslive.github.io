

#### Array 
遍歷陣列
```javascript
let a = [1,2,3]

for (let i = 0; i < a.length; i++ ) {
  // for : 可設定 起始點、結束點、間隔
}
for ( const k in a) {
  // for-in : k為陣列的 keys , 無特別附屬則為 index > string(0,1,2)
  // 如果增加屬性則也會枚舉出來, 自身外也包含繼承的, ex: a.prop > 0,1,2,prop 
}
for (const e of a) {
  // for-of : e為元素 (1,2,3)
}

a.forEach( 
  element => {
  // forEach : callback型式, 也可以寫(element, index)
  // callback型式 > 不會影響到原本的陣列, 且不能中斷
});


```

#### Object
物件
```javascript
```


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

