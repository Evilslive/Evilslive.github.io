## 學習筆記
### Control Flow
#### 流程控制
+ ___pass___ &emsp; 執行另一個區塊, 所以通常會搭配if...else；在位置1.時無實質功能, 2.表示當i被2整除時, 會執行else 
+ ___continue___ &emsp; 當執行到這一行時, 開始下一個for迴圈；3.表示i小於10時, 直接跳到for迴圈開始下一個i, 不會到達print 
+ ___break___ &emsp; 當執行到這一行時, 終止if/整個for迴圈；當i大於10時, 會直接跳出for迴圈, 不會到達print

```python
print("start")
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

### Variable Argument
#### 可變參數 
+ ___\*args___ &emsp; Arguments: 將參數收蒐集到tuple中 
+ ___\*\*kwargs___ &emsp; Keyword Arguments: 將參數收蒐集到dict中

>\*args then \*\*kwargs &emsp; 在 ___def___ 函式中, 需先放開放參數, 再接預設參數

### Copy
由append、extend所帶出的議題, 探討深拷貝、淺拷貝

### Set
#### 新增
```python
y= set(1) or x= {2} # 建立集合
y.add(2) # 新增元素 
x = y.copy() # 拷貝 
```
#### 更新
```python
y.update(x) # 合併兩個集合
```
#### 刪除
```python
y.remove(2) # 移除元素, 找不到則KeyError
y.discard(2) # 移出元素
y.pop() # 擲出一個隨機元素, 為空則KeyError
y.clear() # 清空集合
```
#### 關係
```python
x in y or x not in y: 元素包含判斷
x | y : 聯集
x & y : 交集
x ^ y : 對稱差集, 包含x, y不重複的元素
x.issubset(y): 子集判斷, x是否是y的子集
y.issuperset(x): 超集判斷
```
### List
```python
x = ['a','b']
y = ['Tom','Bill']
## 增加
x += ['c'] 
x.append('d')
x.extend(['e']) # x = ['a','b','c','d','e']
## 刪除
del x[0] # 'a'
del x[-2] # 'd'
x.pop(0) # 'b'
x.pop() # 'e'
x.remove('c') # []
x.clear() # 清空 []
## 查
y.index('Tom') # 0
y.index('Bill',3,4), # ValueError: 'Bill' is not in list
y.count('Bill') # 1
## 改

```
> 查找速度 dict > list

### Method
@classmethod, 類方法

@staticmethod, 靜態方法

### Magic Methods
#### Initialization and Construction
+ \_\_new\_\_(cls, other) &emsp; To get called in an object's instantiation.
+ \_\_init\_\_(self, other) &emsp; To get called by the __new__ method.
+ \_\_call\_\_(self, other) &emsp; 

<!--
        __del__(self)	Destructor method.
#### Unary operators and functions

        __pos__(self)	To get called for unary positive e.g. +someobject.
        __neg__(self)	To get called for unary negative e.g. -someobject.
        __abs__(self)	To get called by built-in abs() function.
        __invert__(self)	To get called for inversion using the ~ operator.
        __round__(self,n)	To get called by built-in round() function.
        __floor__(self)	To get called by built-in math.floor() function.
        __ceil__(self)	To get called by built-in math.ceil() function.
        __trunc__(self)	To get called by built-in math.trunc() function.
#### Augmented Assignment

        __iadd__(self, other)	To get called on addition with assignment e.g. a +=b.
        __isub__(self, other)	To get called on subtraction with assignment e.g. a -=b.
        __imul__(self, other)	To get called on multiplication with assignment e.g. a *=b.
        __ifloordiv__(self, other)	To get called on integer division with assignment e.g. a //=b.
        __idiv__(self, other)	To get called on division with assignment e.g. a /=b.
        __itruediv__(self, other)	To get called on true division with assignment
        __imod__(self, other)	To get called on modulo with assignment e.g. a%=b.
        __ipow__(self, other)	To get called on exponentswith assignment e.g. a **=b.
        __ilshift__(self, other)	To get called on left bitwise shift with assignment e.g. a<<=b.
        __irshift__(self, other)	To get called on right bitwise shift with assignment e.g. a >>=b.
        __iand__(self, other)	To get called on bitwise AND with assignment e.g. a&=b.
        __ior__(self, other)	To get called on bitwise OR with assignment e.g. a|=b.
        __ixor__(self, other)	To get called on bitwise XOR with assignment e.g. a ^=b.
#### Type Conversion Magic Methods

        __int__(self)	To get called by built-int int() method to convert a type to an int.
        __float__(self)	To get called by built-int float() method to convert a type to float.
        __complex__(self)	To get called by built-int complex() method to convert a type to complex.
        __oct__(self)	To get called by built-int oct() method to convert a type to octal.
        __hex__(self)	To get called by built-int hex() method to convert a type to hexadecimal.
        __index__(self)	To get called on type conversion to an int when the object is used in a slice expression.
        __trunc__(self)	To get called from math.trunc() method.
#### String Magic Methods

        __str__(self)	To get called by built-int str() method to return a string representation of a type.
        __repr__(self)	To get called by built-int repr() method to return a machine readable representation of a type.
        __unicode__(self)	To get called by built-int unicode() method to return an unicode string of a type.
        __format__(self, formatstr)	To get called by built-int string.format() method to return a new style of string.
        __hash__(self)	To get called by built-int hash() method to return an integer.
        __nonzero__(self)	To get called by built-int bool() method to return True or False.
        __dir__(self)	To get called by built-int dir() method to return a list of attributes of a class.
        __sizeof__(self)	To get called by built-int sys.getsizeof() method to return the size of an object.
#### Attribute Magic Methods

        __getattr__(self, name)	Is called when the accessing attribute of a class that does not exist.
        __setattr__(self, name, value)	Is called when assigning a value to the attribute of a class.
        __delattr__(self, name)	Is called when deleting an attribute of a class.
#### Operator Magic Methods

        __add__(self, other)	To get called on add operation using + operator
        __sub__(self, other)	To get called on subtraction operation using - operator.
        __mul__(self, other)	To get called on multiplication operation using * operator.
        __floordiv__(self, other)	To get called on floor division operation using // operator.
        __truediv__(self, other)	To get called on division operation using / operator.
        __mod__(self, other)	To get called on modulo operation using % operator.
        __pow__(self, other[, modulo])	To get called on calculating the power using ** operator.
        __lt__(self, other)	To get called on comparison using < operator.
        __le__(self, other)	To get called on comparison using <= operator.
        __eq__(self, other)	To get called on comparison using == operator.
        __ne__(self, other)	To get called on comparison using != operator.
        __ge__(self, other)	To get called on comparison using >= operator.
-->

### Decorator

前半段表現不一樣但後半段一樣, 用修飾(不同, 同)
```python

```

### Inheritance

前半段表現一樣但後半段不一樣, 用繼承(同, 不同)




