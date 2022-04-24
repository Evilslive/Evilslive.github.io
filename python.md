## Python Notes

### Control Flow
流程控制
+ ___pass___ &emsp; 執行這一行時不動作, 所以通常會搭配if...else, 一個條件動作、另一個pass；在位置1.時無實質功能, 2.表示當i被2整除時, 不做任何事 </li>
+ ___continue___ &emsp; 當執行到這一行時, 開始下一個for迴圈；3.表示i小於10時, 直接跳到for迴圈開始下一個i, 不會到達print </li>
+ ___break___ &emsp; 當執行到這一行時, 終止if/整個for迴圈；當i大於10時, 會直接跳出for迴圈, 不會到達print </li>

```python
print("start", end=" > ")
for i in range(50):
    pass # 1.
    if i % 2 == 0: pass # 2.
    else:
        if i < 10: continue # 3.
        if i > 10: break # 4.
    print(i, end=' > ') # 注意縮排的位置
print("end")
```
   
output：

    start > 0 > 2 > 4 > 6 > 8 > 10 > end

### Short Circut

> 就直接用 and or 就好了, why & | ?

### Variable Argument
可變參數 
    
+ ___\*args___ &emsp; Arguments: 將參數收蒐集到tuple中 
+ ___\*\*kwargs___ &emsp; Keyword Arguments: 將參數收蒐集到dict中

>\*args then \*\*kwargs &emsp; 在 ___def___ 函式中, 需先放開放參數, 再接預設參數

### Copy

由append、extend所帶出的議題, 探討深拷貝、淺拷貝

### Data type

##### \_\_init__
```python
x = ['a','b']
y = ['Tom','Bill']
```

##### 增
```python
# set
y= set(1) or x= {2} # 建立集合
y.add(2) # 新增元素 
x = y.copy() # 拷貝 

# dict
y.setdefault("k", "v") # 將key, value新增到字典
y.update({"k":"v"}) # 合併字典, 後蓋前
z = {**x, **y} # 合併字典, ver3.5-

# list
x += ['c'] 
x.append('d')
x.extend(['e']) # x = ['a','b','c','d','e']

```

##### 刪
```python
# set
y.remove(2) # 移除元素, 找不到則KeyError
y.discard(2) # 移出元素
y.pop() # 擲出一個隨機元素, 為空則KeyError
y.clear() # 清空集合

# dict
y.pop("k","v")
y.popitem()
y.clear()

# list
del x[0] # 'a'
del x[-2] # 'd'
x.pop(0) # 'b'
x.pop() # 'e'
x.remove('c') # []
x.clear() # 清空 []

```

##### 查

```python
# set

# dict
y.get()

# list
y.index('Tom') # 0
y.index('Bill',3,4), # ValueError: 'Bill' is not in list
y.count('Bill') # 1

```

##### 改
```python
# set
y.update(x) # 合併兩個集合

# dict

# list

```

##### 關係
```python
x in y or x not in y: 元素包含判斷
x | y : 聯集
x & y : 交集
x ^ y : 對稱差集, 包含x, y不重複的元素
x.issubset(y): 子集判斷, x是否是y的子集
y.issuperset(x): 超集判斷
```


### Type conversion
    
#### 格式轉換

***list***
```python
list_a = other_type.tolist()
list_a = list(other_type)
```

***numpy***
```python
array_a = np.array(other_type)

array_a = series_a.to_numpy()
array_a = series_a.values
```

***pandas***
```python
series_a = pd.Series(other_type)
```

***tensorflow***
```python
constant_a = tf.constant(other_type)
```

> 可以加入 isdigit()、isnumerial()、isdecimal() # 但無法判斷float

> 查找速度 dict > list

### Method

@property, 將方法當作參數、屬性調用(類裡須宣告__init__)

不須實例化即可調用的修飾方法, 所在的類不須實例化即可使用

@classmethod, 類方法(不需要self參數, 但需要指向自身類的cls參數)

@staticmethod, 靜態方法(不需要self、cls參數)

### Magic Methods

#### Initialization and Construction
*\_\_new__(cls, other)* &emsp; 當對象實例化時調用
*\_\_init__(self, other)* &emsp; 被*\_\_new__*方法調用
*\_\_call__(self, other)* &emsp; 呼叫實例化對象時調用

*\_\_dir__(self)*  &emsp; 列出對象的所有屬性、方法, 如:dir()

```python
class Cola:
    PRICE = 1.01
    def __init__(self):
        pass
    def promotion1(self):
        print('50% off second item !')
    def promotion2(self):
        print('Buy one get one free !')

can = Cola()
print(can.__dir__())
```
output:
```python
['__module__', 'PRICE', '__init__', 'promotion1', 'promotion2', ... ] # 其他魔術方法
```
*\_\_getitem__(self, key)* &emsp; 實例化為*dict*對象

```python
class CountingStars:
    def __init__(self, count:str):
        self.pages = {}
        for s,t in enumerate(count):
            self.pages[t] = self.pages.get(t, []) + [s+1]
    def __getitem__(self, key):
        return self.pages[key]


where_is = CountingStars('Hello, world !!')
print(where_is['o'])
```
*\_\_iter__* &emsp; 迭代

*\_\_all__* &emsp; 
雖然使用 "all" ,但真正的用意是「只有這些」; 
當使用 <code> from module import * </code> 時, 寫有此方法的模組將只會導入all內寫明的類與方法
, 限制list類型

#### Descirptor

描述器

*\_\_get__(self, __obj: Any, __type: type | None)* &emsp;

*\_\_set__(self, __obj: Any, __value: Any)* &emsp;

*\_\_delete__(self, __obj: Any)* &emsp; 回收機制

### Decorator

前半段表現不一樣但後半段一樣, 用修飾(不同, 同)
```python
    還沒什麼心得
```

### Inheritance

前半段表現一樣但後半段不一樣, 用繼承(同, 不同)
```python
    還沒什麼心得
```

### Path

相對路徑 與 絕對路徑, module 與 package



