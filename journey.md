
Control Flow
基本流程控制三個指令 pass, continue, break pass: 執行另一個區塊, 所以通常會搭配if...else, 所以在位置1.時無實質功能, 2.表示當i被2整除時, 會執行else continue: 當執行到這一行時, 開始下一個for迴圈, 所以3.表示i小於10時, 直接跳到for迴圈開始下一個i, 不會到達print break: 當執行到這一行時, 終止if/整個for迴圈, 因此當i大於10時, 會直接跳出for迴圈, 不會到達print

        print("start")
        for i in range(50):
            pass # 1.
            if i % 2 == 0: pass # 2.
            else:
                if i < 10: continue # 3.
                if i > 10: break # 4.
            print(i) # 注意縮排的位置
        print("end")
    
輸出結果:

                start
                0
                2
                4
                6
                8
                10
                end
Activation Function
linear: f(x) = x, -inf to inf 
sigmoid: f(x) = 1/(1+e^x), 0 to 1 
tanh: , -1 to 1 
relu: max(0, x), 0 to inf leak 
relu:
Variable Argument Functions
可變參數 Argument(*args): 將參數收蒐集到tuple中 Keyword Argument(**kwargs): 將參數收蒐集到dict中 順序問題 *args then **kwargs 因為在函式(df)中, 前頭要是開放參數, 而預設參數放在後面, 使得函式呼叫時可以直接丟數value而不用先定義key
Set
新增
                y= set(1) or x= {2} # 建立集合
                y.add(2) # 新增元素 
                x = y.copy() # 拷貝 
        
更新
                y.update(x) # 合併兩個集合
刪除
                y.remove(2) # 移除元素, 找不到則KeyError
                y.discard(2) # 移出元素
                y.pop() # 擲出一個隨機元素, 為空則KeyError
                y.clear() # 清空集合
關係
                x in y or x not in y: 元素包含判斷
                x | y : 聯集
                x & y : 交集
                x ^ y : 對稱差集, 包含x, y不重複的元素
                x.issubset(y): 子集判斷, x是否是y的子集
                y.issuperset(x): 超集判斷


魔術方法
                __new__
                __init__
                __call__







