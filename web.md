
## Web Server Gateway Interface,  WSGI

#### Gunicorn 

```shell
gunicorn wsgi:app
gunicorn --workers=4 wsgi:app
gunicorn --bind=10.1.0.0:8080 wsgi:app
```

#### Werkzeug

```
```

#### FastCGI
Fast Common Gateway Interface

> Flask vs IIS 10

###### python設定
2. pip install wfastcgi
   * 於安裝的位置啟用功能cmd輸入 `wfastcgi-enable`, 通常是 C:\xxx\pythonXXX\lib\site-packages\
   * 將 site-package 裡的 `wfastcgi.py` 複製到 `PYTHONPATH` 路徑內 (項6)
3. 在 ```PYTHONPATH``` 路徑下, 輸入下列指令開啟IIS用戶可以訪問網站腳本的權限
   ```shell
        icacls . /grant "NT AUTHORITY\IUSR:(OI)(CI)(RX)"
        icacls . /grant "Builtin\IIS_IUSRS:(OI)(CI)(RX)" 
   ``` 
     
     <details>
     <summary>關於 icacls </summary>
      Windows Server 上的指令
  
      取代 cacls: 主要進行DACL, 顯示或修改指定目錄中檔案的存取控制清單
  
      /grant : 授予存取權限(取代), /grant[:-r]則新增
      
      中間的IUSR為預設路徑 (可以網頁右鍵編輯權限?)
      
      (OI) : 物件繼承, 套用在目錄上
  
      (CI) : 容器繼承, 套用在目錄上
  
      (RX) : 讀取和執行存取權
  
     </details>

flask `app.config` key的設定:
    + PERMANENT_SESSION_LIFETIME：設置 session 的效期，單位是秒。默認 Session 是永久，當 session.permanent 為 True 時才會套用。
    + SESSION_COOKIE_SECURE: True時只在 HTTPS 發送，默認為 False。

###### windows設定
1. 啟用Server CGI 功能
   * 程式集 > 開啟或關閉Windows功能 > Internet Information Servers > World Wide Web 服務 > 應用程式開發功能 > CGI
2.
3.
4. 由 window server 開啟 IIS管理員 > 站台 > 新增網站 > 輸入網站資料夾的 *實體路徑*、設定 *連接阜* (iponfig 避免重複)
5. 在站台內新增的網站 開啟 處理常式對應 > 新增對應模組, 要求路徑 * (表示本地路徑)、模組選 FastCgiModule, 要求限制 > 對應 > 取消 只有當要求對應到下列項目時才啟動處理常式
6. 回到 本機IIS > FastCGI設定 > 剛剛設定的站台名 > 環境變數, 新增名稱與變數
   * `PYTHONPATH`: 入口網站資料夾位置, 含有wfastcgi.py的位置(注意不是安裝路徑C)
   * `WSGI_HANDLER`: 啟動程式名稱, 以flask為例通常是 程式名xxxx.app, 也就是 app=Flask(__name__)的路徑
7. 在 應用程式區集 中, 找到對應的處理序 > 進階設定, 將 識別 修改為 LocalSystem
8. HTTP回應標頭 新增  名稱 `X-Frame-Options`: 值 `SAMEORIGIN`, 用以防Clickjacking(?)
9. 防火牆新增輸入規則, 開放連接阜即可外部連線


```shell
netsh http # 可以進行 URL 保留專案和註冊, 實質上還未使用到(待研究)
```

## IIS

### Warm Up
1. 新增角色:應用程式初始化
2. 網站/進階設定/{預先載入已啟用: True, 閒置逾時動作: Suspend}
3. 對應的應用程式區集/啟動模式: AlwaysRunning

## NETWORK 網路

<details>
<summary> 網路相關指令 </summary>

#### *ipconfig*

查詢系統的網路卡資訊

#### *route*

封包傳送的路由指令 ?

#### *netstat*

觀看網路狀況與統計分析

#### *ping*

測試目標主機

#### *nslookup*

使用不同的server可以透過中華電信、Google查詢ip的Domain Name(DNS)
```bash
> server 168.95.1.1
Default Server:  dns.hinet.net
Address:  168.95.1.1
> server 8.8.8.8
Default Server:  dns.google
Address:  8.8.8.8
```

</details>

<details>
<summary> Port 埠 (是ㄅ不是ㄆ) </summary>
  
+ 0
+ 1
+ 7
+ 19
+ 21 > File Transfer Protocol, FTP 檔案傳輸協議
+ 22
+ 23 > Telnet 遠端登錄服務
+ 25  
+ 31
+ 42
+ 53 > Domain Name Server, DNS 網域名稱服務
+ 67
+ 69
+ 79
+ 80 > HTTP
+ 88
+ 99
+ ...
+ 443 > HTTPS
+ 1433 > SQL預設通道
+ ...
+ 3389 > WIN 2000 終端開啟
+ ...
+ 8080 > WWW
+ ...

</details>


## HTTP 請求方式

#### GET >     請求展示指定資源。只應用於取得資料。
#### HEAD >    請求與 GET 方法相同的回應，但它沒有回應主體(response body)。
#### POST >    用於提交指定資源的實體，通常會改變伺服器的狀態或副作用(side effect)。
#### PUT >     取代指定資源所酬載請求（request payload）的所有表現。
#### DELETE >  刪除指定資源.
#### CONNECT > 和指定資源標明的伺服器之間，建立隧道（tunnel）。
#### OPTIONS > 描述指定資源的溝通方法（communication option）。
#### TRACE >   與指定資源標明的伺服器之間，執行迴路返回測試（loop-back test）。
#### PATCH >   用指定資源的部份修改。

#### 發送

python
```python
import json
import requests
url = 'http://127.0.0.1:5000'
data = {"Q":"A"}
data = json.dumps(data)
reqs = requests.post(url, data=data)

```

js
```js
$.ajax({
    type: 'POST',
    url: 'http://127.0.0.1:5000',
    contentType: 'application/json;charset=UTF-8',
    data: JSON.stringify({ "Q": "A" }),
})
  .then(
    function(){
  })
  .fail(
    function(){
  });

fetch(url, 
  {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ "Q": "A" }),
  })
  .then(response => {
    // 先回傳資料或進行status判斷
    return response.json()
  })
  .then(data =>{
  })
  .catch(error=>{
  });
```

#### 接收

```python
```

### HTTP 狀態碼

<details>
<summary> 1xx 資訊回應 </summary>
  
> 100 Continue
此臨時回應表明，目前為止的一切完好，而用戶端應當繼續完成請求、或是在已完成請求的情況下，忽略此資訊。

> 101 Switching Protocol
此狀態碼乃為用戶端 Upgrade (en-US) 請求標頭發送之回應、且表明伺服器亦切換中。

> 102 Processing (WebDAV (en-US))
此狀態碼表明伺服器收到並處理請求中，但目前未有回應。

> 103 Early Hints (en-US)
此狀態碼主要與 Link (en-US) 標頭有關：它能讓用戶代理（user agent）能在伺服器準備回應前能 preloading (en-US) 資源。

</details>

<details> 
<summary> 2xx 成功回應 </summary>

> 200 OK
請求成功。

> 201 Created
請求成功且新的資源成功被創建，通常用於 POST 或一些 PUT 請求後的回應。

> 202 Accepted
此請求已經被接受但尚未處理。此狀態為非承諾性，代表 HTTP 無法在之後傳送一個非同步的回應告知請求的處理結果。最初目的為外部程序或其他伺服器處理請求的情況，或用於批次處理中。

> 203 Non-Authoritative Information
此回應碼表示回傳的中介資料集與並非與原始伺服器上的有效確定集合完全相同，而是來自本地或第三方的副本。除此情況外，200 OK 回應碼應該被優先使用。

> 204 No Content
傳送的請求沒有內容, 但headers內有資訊.

> 205 Reset Content
請求刷新頁面

> 206 Partial Content
分流下載?

> 207 Multi-Status (WebDAV (en-US))
多狀態響應?

> 208 Multi-Status (WebDAV (en-US))
用以避免多狀態響應時, 反覆請求?

> 226 IM Used (HTTP Delta encoding)
已完成GET請求?

</details>
 
<details>
<summary> 3xx 重定向訊息 </summary>

> 300 Multiple Choice
請求擁有一個以上的回應。用戶代理或使用者應該從中選一。不過，並沒有標準的選擇方案。

> 301 Moved Permanently
此回應碼的意思是，請求資源的 URI 已被改變。有時候，會在回應內給予新的 URI。
>> 永久轉址

> 302 Found (en-US)
請求的URI已暫時改變了, 正在等待完成?
>> 暫時轉址

> 303 See Other (en-US)
伺服器傳送請求到其他位址, 以取得URI與GET資源

> 304 Not Modified (en-US)
暫存未被修改, 告知可繼續使用.

> 305 Use Proxy 
在舊版本的 HTTP 規範中，表示請求資源必須透過代理存取。基於對代理的頻內設置 (in-band configuration) 相關的安全考量，該狀態碼已棄用。

> 306 unused
該狀態碼已不再被使用，僅被保留。該狀態碼曾在先前得的 HTTP 1.1 規範中被使用。

> 307 Temporary Redirect (en-US)
伺服器發送此回應來使客戶端保持請求方法不變向新的地址發出請求。 與 302 Found 相同，差別在於客戶端不許變更請求方法。例如，應使用另一個 POST 請求來重複發送 POST 請求。

> 308 Permanent Redirect (en-US)
URI以永久更改, 請求方法將延續使用?

</details>
  
<details> 
<summary> 4xx 用戶端錯誤回應 </summary>

> 400 Bad Request (en-US)
此回應意味伺服器因為收到無效語法，而無法理解請求。

> 401 Unauthorized (en-US)
需要授權以回應請求。它有點像 403，但這裡的授權，是有可能辦到的。

> 402 Payment Required (en-US) 
此回應碼留作未來使用。一開始此碼旨在用於數位交易系統，然而，目前極少被使用，且不存在標準或慣例。

> 403 Forbidden
用戶端並無訪問權限，例如未被授權，所以伺服器拒絕給予應有的回應。不同於 401，伺服端知道用戶端的身份。
>> .14 伺服器已設為不列出此目錄的內容

> 404 Not Found
伺服器找不到請求的資源。因為在網路上它很常出現，這回應碼也許最為人所悉。
>> .11 要求包含雙重逸出序列。
>> 
>> .12 要求包含高位元字元。
>> 
>> 在設定`IIS 10`時遇到的問題, 當 內容/url/src 包含 % # 等高位字元時, 可在要求過濾 `Requests Filter` 進行設定, 但須顧慮安全性(?)

> 405 Method Not Allowed (en-US)
伺服器理解此請求方法，但它被禁用或不可用。有兩個強制性方法：GET 與 HEAD，永遠不該被禁止、也不該回傳此錯誤碼。

> 406 Not Acceptable (en-US)
伺服器根據請求找不到資源?

> 407 Proxy Authentication Required (en-US)
類似401, 但須透過Proxy完成身分驗證

> 408 Request Timeout (en-US)
伺服器回應超過設定時間?

> 409 Conflict
表示請求與伺服器目前狀態衝突

> 410 Gone (en-US)
請求的資源已經不在.

> 411 Length Required
伺服器拒絕該請求，因為 Content-Length 頭沒有被定義，然而伺服器要求。

> 412 Precondition Failed (en-US)
用戶端的header不符合要求

> 413 Payload Too Large (en-US)
請求的實體資料大小超過了伺服器定義的上限，伺服器會關閉連接或返回一個 Retry-After 回應頭。

> 414 URI Too Long (en-US)
客戶端的 URI 請求超過伺服器願意解析的長度。

> 415 Unsupported Media Type
被請求資源的多媒體類型不被伺服器支援，因此該請求被拒絕。

> 416 Requested Range Not Satisfiable (en-US)
數據太大?

> 417 Expectation Failed (en-US)
伺服器無此請求方式?

> 418 I'm a teapot
伺服器拒絕用茶壺泡咖啡... XDD

> 421 Misdirected Request
新的定向失敗

> 422 Unprocessable Entity (en-US) (WebDAV (en-US))
請求格式正確, 但"語意"錯誤?

> 423 Locked (WebDAV (en-US))
被訪問的資源被鎖定。

> 424 Failed Dependency (WebDAV (en-US))
由於先前的請求失敗導致此請求失敗。

> 426 Upgrade Required (en-US)
請用戶端升級

> 428 Precondition Required (en-US)
有條件的接受請求, 避免遺失更新, 如用戶端GET資源並修改後, PUT回來時.

> 429 Too Many Requests (en-US)
用戶在給定的時間內 ("rate limiting") 發送了過多的請求。

> 431 Request Header Fields Too Large (en-US)
伺服器不願意處理該請求，因為標頭欄位過大。該請求可能可以在減少請求標頭欄位大小後重新提交。

> 451 Unavailable For Legal Reasons
用戶端請求違法的資源，例如受政府審查的網頁。
  
</details>
  
<details>
<summary> 5xx 伺服器端錯誤回應 </summary>

> 500 Internal Server Error
伺服器端發生未知或無法處理的錯誤。
>> .19 Internal Server Error. 可能是 ApplicationHost.config 或 Web.config 格式不正確或有未識別的XML元素; 或IIS上子父有重複的定義
>>
>> .52 URL Rewrite Module Error. 也是父層級被鎖定的原因, 釋放資源或重啟IIS
>>
  
> 501 Not Implemented (en-US)
請求方法不支持 (GET, HEAD)?

> 502 Bad Gateway
伺服器關閉或離線?

> 503 Service Unavailable
伺服器開著, 但停止運作或過載?

> 504 Gateway Timeout
伺服器無法及時回應

> 505 HTTP Version Not Supported (en-US)
請求使用的 HTTP 版本不被伺服器支援。

> 506 Variant Also Negotiates (en-US)
伺服器內部配置錯誤: 循環引用?

> 507 Insufficient Storage (en-US)
伺服器內部配置錯誤: 存取變動的資源?

> 508 Loop Detected (en-US) (WebDAV (en-US))
無限循環/死結

> 510 Not Extended (en-US)
請求是未來更新才能處裡的

> 511 Network Authentication Required (en-US)
用戶端需獲得權限才能訪問

[以上由MDN頁面修改](https://developer.mozilla.org/zh-TW/)
  
</details>
