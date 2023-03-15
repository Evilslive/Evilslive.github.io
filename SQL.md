

### 正規化

#### 1NF
無重複資料群: 一筆資料不會有重複的資料群. 以欄位來看, 每個欄位在資料表中的訊息是獨特的且唯一的, 也就是表中的欄與欄維持在二維對應, 不會超出到三維.

#### 2NF
消除多餘: 透過參照值分隔資料, 以減少重複資料與多餘資料

#### 3NF
找到主要依賴者: 回到值得依賴的鍵值

#### BCNF (Boyce Codd Norm Form)
#### 4NF 
#### 5NF


```sql
TRUNCATE TABLE 表單名; /*清空表單*/
```

## SQL連線障礙排除

### SSCM
服務啟用
Configuration Tools 》Sql Server Configuration Manager 》SQL Server 》Running

TCP/IP開啟
Sql Server Configuration Manager 》 Sql Server Network Configuration 》TCP/IP 》Enabled

TCP/IP上按右鍵, 在IP ADRESS 最下面一項 IP ALL 0為動態, 設定完成後重啟可以看的取得的值

### SSMS
選資料庫的Management 》SQL Server Log, 查詢連線狀況

如果出現Sql Error 18456，表示沒有開啟Mixed Mode（混合驗證模式）

選擇資料庫》Properties 》Security 》Sql Server and Windows Authentication Mode , 重新啟動

