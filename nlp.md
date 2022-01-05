
斷詞 Word segmentation, WS 
詞類標註 Part-of-speech tagging, POS 
實體命名識別 Name entity recognition, NER 
關係抽取 Relationship extraction 
抽取式摘要
生成式摘要 

## 分類任務
### 分類器參數, Activation Function
        linear: f(x) = x, -inf to inf 
        sigmoid: f(x) = 1/(1+e^x), 0 to 1 
        tanh: , -1 to 1 
        relu: max(0, x), 0 to inf 
        leaky relu:
  sigmoid: 0 to 1, 特性 1.單側抑制 2.相對寬闊的邊界(-6 to -6) 3.稀疏激活性 函式 f(x) = 1 / (1+exp(-x)) 導數 f'(x) = f(x)(1-f(x)) 
  tanh(TanHyperbolic): -1 to 1 函式 f(x) = (e^x - e^(-x)) / (e^x + e^(-x)) 導數 f'(x) = 1 - (f(x))^2 
  ReLU(Rectifield Linear Units): 0 to inf, 特性 1.無梯度消失的問題 2.歸0時cell死亡 函式 f(x) = max(0, x) 導數 f'(x) = {1, x>0; 0, x<=0} 
  softmax: 0 to 1 特性 逼進0與1 函式 f(x)i = e^x_i / sigma(k=1 to K) e^x_k 導數
### 配對任務













