

## Linux 學習紀錄: ubuntu 20.04 mainly 

### 開機引導修復

在grub 2環境下, 一一測試每個分隔槽, 直到找到含有路徑 /boot/grub 的磁區, 表示系統安裝在此
```grub
> ls
（hd0） （hd0，msdos9） （hd0，msdos8） （hd0，msdos7） （hd0，msdos6） ...
> ls (hd0) /boot/grub
ERROR MSG NOT FOUND ! 
> ls (hd0, msdos9) /boot/grub 
...
```
找到後重新指向, 並啟動(normal)

```grub
> set root =（hd0，msdos8）
> set prefix=（hd0，msdos8）/boot/grub
> insmod normal
> normal
```
> insmod: install module

啟動後, 再到系統內更新grub

### 網路相關指令

#### *ifconfig*

查詢系統的網路卡資訊

#### *route*

封包傳送的路由指令 ?

#### *netstat*

觀看網路狀況與統計分析

#### *ping*

測試目標主機

#### *nslookup*

查詢DNS









