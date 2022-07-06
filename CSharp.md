

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


