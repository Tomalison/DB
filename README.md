# 資料庫學習紀錄

## 系統安裝與介面操作

#### 前言
- 常用的有Mysql、Oracle、Microsoft sql
- mysql是開放原始碼資料庫管理系統，原本是SUN旗下的資料庫管理系統、2009年Oracle將之買下、效能高、成本低與可靠度高。
- 這是一種結構化(Structured Query Language)、SQL是關聯式資料庫的程式語言標準語言
- 允許用戶撈取關連式資料庫的數據、允許用戶定義資料庫的數據、新增、修改、刪除資料庫中的表單，設定table,procedure,views...的權限。
- ![image](https://github.com/Tomalison/DB/assets/96727036/6d517a34-2dce-4682-87c5-6291c522fff6)
- ![image](https://github.com/Tomalison/DB/assets/96727036/83362f2a-3cb5-4559-962e-e2cfc4a9d7b4)
- 資料庫管理:直接指令連到資料庫、使用工具介面、Workbench、PHPMyadmin、TOAD / 我個人是使用Navicat
- 程式語言與資料庫的串接 範例
- ![image](https://github.com/Tomalison/DB/assets/96727036/6616bd21-a02f-4260-b91b-08098be5882a)

#### 系統操作與環境介面
- 個人使用Navicat16 [navicat_ct.pdf](https://github.com/Tomalison/DB/files/12157858/navicat_ct.pdf)
- Mysql community Server 下載 https://dev.mysql.com/downloads/ 選作業系統版本 安裝。
- Win Mysql server + Applications_workbench  要開3306port

## 資料庫基本架構
#### 什麼是資料庫/基本觀念說明
- create database if not exists orders; 建立orders資料庫(如果他不存在的話)
- drop database orders; 刪除資料庫(謹慎使用)
- UTF-8 預設用這個編碼方式
#### 儲存資料的表格
- Tabel如何建立與設定
- 建table之前Column一定要先建一個ID的欄位
- INDEX 資料越多 索引可以幫我們更快找到資料並增加資料庫效能
- Trigger當我們對table做塞入/編輯資料時後做一些動作(例如發通知、或紀錄)
- Partition當資料很多時可以做一個切割，可以讓我們快速去找到我們要的東西
- drop table就可以砍掉這張表/Truncate table則是把資料刪除 但表還是保留。(謹慎)
``` sh
Create table `orders`, `customers` (
  `customers_id` INT NOT NULL,
  Primary key(`customers_id`));
```

#### 欄位
#### 課程資料匯入與匯出

## 資料庫設計
#### 首先，要先知道一些關鍵欄位的用法
#### 使用者需求分析的方法與流程
#### 工作實際案例分析
#### 設計資料庫的重要觀念

## SQL語法
#### 撈取資料庫資料的關鍵字Select
#### 多個表格連接在一起的作法
#### 排序
#### 將特定欄位中相同的資料作為分組
#### 資料分組後加入條件，過濾出你想要的資料
#### 欄位名字過長?表單名字太複雜?暫時取個暱稱來使用
#### 不曉得完整、精確的資料內容，也可以找出大概可能的結果
#### 搜尋出特定範圍的日期或數字資料
#### 元素比較
#### 子查詢
#### 搜尋資料時，用exits會更有效率
#### 新增資料
#### 修改資料
#### 刪除資料

## Mysql函式庫與運算子
#### 數學運算子
#### 比較運算子
#### 邏輯運算子
#### 計算資料的數量
#### 數學運算函式庫
#### 處理文字的函式庫

## 資料庫進階功能
#### 建立索引，加快搜尋資料的速度
#### 當事件發生時，建立一個觸發程序能幫你啟動自動化的程式
#### 虛擬表格能幫你在應用層少寫一些SQL語法和程式碼，是一個實用技能
#### 在資料庫中撰寫自己的函式，將流程和邏輯包起來，隨時可使用
#### 教你如何使用資料庫中內建的函式和常用的函式

## 程式語言串連資料庫的設計與實作
#### 安裝Python學習環境for Windows

#### 使用參數撰寫SQL語法，避免SQL注入攻擊(SQL INJECTION)
#### Tomcat安裝與說明
#### Tomcat目錄價購與web.xml設定
#### Web系統架構
#### 物件關係對應(ORM)實作

## Mysql資料庫維護
## Nosql資料庫
## SQL語法判斷資料的方式
