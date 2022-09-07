

### assembly
組件/元件, ex: exe、dll檔
> 具有語言無關性

What is manifest?

### class
類型

## Access Modifiers
存取修飾詞

|   呼叫組件     |   呼叫位置   | public | private | private protected | protected | protected internal | internal |
| -------------:| -----------:|:-------:|:-------:|:----------------:|:----------:|:------------------:|:--------:|
|               | this class  |:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|
| same assembly | child class |:heavy_check_mark:|:x:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|
|               | other class |:heavy_check_mark:|:x:|:x:|:x:|:heavy_check_mark:|:heavy_check_mark:|
| diff assembly | child class |:heavy_check_mark:|:x:|:x:|:heavy_check_mark:|:heavy_check_mark:|:x:|
|               | other class |:heavy_check_mark:|:x:|:x:|:x:|:x:|:x:|

+ protected : 只在**繼承**內使用, 保護繼承
+ internal : 只在**組件**內使用, 連接組件
+ protected + internal : **聯集**, 組件或繼承都可以使用
+ private + protected : **交集**, 同組件&繼承內使用 (所以不需要再有 private internal)

## 其他修飾詞

#### abstract vs virtual
抽象方法與虛擬方法

#### const vs static readonly


## value types

整數 (含零正: 範圍長度一樣, 但 中心位置=整數最大值, 故 max(整數)\*2 +1 == max(純正))
+ sbyte (byte) (-128, 127)
+ short (ushort) (-32768, 32767)
+ int	(uint) 9次方
+ long (ulong) 18次方
+ nint (nuint)

浮數點
+ float (F)
+ double (D)
+ decimal (M): 可以保留小數點後的0, 使得 ToString 時 1.1 跟 1.10 不一樣

> 有隱含的數字轉換規則

<br>
<br>
<hr>

## CommandLine
指令集

```cmd
dotnet run
dotnet test 
dotnet list package
dotnet add package <name>
```

<br>
<br>
<hr>
或許先由命名空間整理

## System

#### 陣列 []

```cs
String[] NList = new string[3]; // 需宣告長度, 速度
NList[0] = "a";
NList[1] = "b";
NList[2] = "c";
// 「增」時固定長度, 不好「插」、「改」
```


#### Array
+ 基型
+ 連續分配
+ 統一型別

```cs
```

## System.Collections

#### ArrayList
+ 非型別安全: 錯誤的資料增刪, 可能導致型別不匹配報錯
+ 連續分配
+ 不定長
+ 須裝箱拆箱: 物件化object後才放入或取出 (所以可以不同類混存)

```cs
ArrayList AList = new ArrayList(); // 可動態擴充, 長度可宣可不宣
AList.Add("a"); // 增
AList.InsertRange(0, new string[] {"x", "b", "u"}); // 插
AList.RemoveAt(0); // 刪, 縮減長度
AList[2] = "g"; // 改, 無法直接賦予長度外位置
// 查
```

#### Queue
+ 先進先出

```cs
Queue<int> queue = new Queue<int>();
queue.Enqueue(123); // 向對列新增元素
queue.Dequeue(); // 取出最前頭的元素, 並由對列中移除
queue.Peek(); // 複製(?)最前頭的元素, 但不移除
```

#### Stack
+ 先進後出

```cs
Stack<string> stack = new Stack<string>();
stack.Push("A計畫"); // 新增元素
stack.Push("B計畫");
stack.Pop(); // 獲取最後進入的元素, 並由對列中移除
stack.Peek(); // 獲取不移除
```

## System.Collections.Generic

#### List
+ ArrayList的泛型等化
+ 統一型別
+ 長度可變
+ 因先宣告型別, 不須裝拆箱

```cs
```

#### LinkedList
+分配不連續

```cs
```

#### HashSet

```cs
```

#### SortedSet

```cs
```

#### HashTable

```cs
```

#### Dictionary

```cs
```

#### SortedDictionary

```cs
```

#### SortedList

```cs
```









