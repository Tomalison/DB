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
- 範例 :
建資料表的主key是customers_id
``` sh
Create table `orders`, `customers` (
  `customers_id` INT NOT NULL,
  Primary key(`customers_id`));
```
在主key後面塞入customer_name欄位
``` sh
Alter Table `orders`, `customers`
Add Column `customer_name` Varchar(45) Not Null After `customers_id`;
```
把建的欄位砍掉
``` sh
Alter Table `orders`, `customers`
Drop Column `customer_name`;
```
把這表刪除掉
``` sh
Drop Table `orders`, `customers`;
```
把表的欄位資料刪除掉
``` sh
Truncate `orders`, `customers`;
```
#### 欄位
- data type : INT(2)=整數2個位  Varchar(5)=字串5個字元 Decimal()=浮點數 Datetime()=時間 BLOB=二進位的資料型態(例如音樂檔、圖片)  這些都會對應到你程式的物件
- /* PK :primary key，功用是串連其他Table / NN :not null不能為空值 / UQ :unique唯一索引值 / BIN :binary二進位的資料 / UN :unsigned沒有符號(非負數) ZF :zero fill 填充0 例如欄位資料是int(4)，則內容是0001 /  AI :auto increment自動增加 / G :這一列由其他列計算出來的 */
- comment 可以去寫一些註解 表達該欄位是在做啥
#### 資料匯入與匯出
- data export 資料備份或傳給其他人 : 選資料庫與表，選要匯出的位置(匯出.sql)
- inport 到對應的資料庫，匯入進來
  
## 資料庫設計
#### 首先，要先知道一些關鍵欄位的用法
- 關聯式資料庫是將資料間的關係，以表單(Table)的形式表達，並將資料儲存於表中；設計Table與屬性(欄位)來儲存資料；可以透過SQL語法查詢多個Table資料。
- 主鍵 : 用來識別表中資料的唯一值；不能重複；提供資料索引(index)
- 外來鍵 : 這個欄位會存放其他表的主key；只有經過確認的資料才能夠輸入存放進表中。
- 表格連結 : 
- ![image](https://github.com/Tomalison/DB/assets/96727036/71108b49-8721-4d55-83a2-1406ed94140f)

#### 使用者需求分析的方法與流程
- 資料庫是系統的底層，系統開發人員與使用者討論需求時，如何引導，例如問 _訂單系統要不要跟物流業者系統串接(這問題就不重要X因為他是細部問題) 建議從角色開始下手 : _有哪些角色人員要使用這個系統? _在從角色人員的面向去了解，他們要做甚麼? _進而深談理解他們需要甚麼功能?
- ![image](https://github.com/Tomalison/DB/assets/96727036/7ee3b913-9952-4f33-a265-0ef2eee1c15f)
- 將剛剛需求分析，做成UML，是一種開放的方法，用於說明、可視化、構建一個正在開發的軟體系統方法(drowio)
- ![image](https://github.com/Tomalison/DB/assets/96727036/63bef09e-77ba-4ca4-ace7-8ec4497c81d0)
- 初步整理歸納
- ![image](https://github.com/Tomalison/DB/assets/96727036/908fc391-e99c-4a9d-9ce8-16e367b9a74b)
- 製作出使用者介面雛形，看的到形體有助於討論分析，不用管外觀是否好看，方便快速調整 (https://balsamiq.com/)
- ![image](https://github.com/Tomalison/DB/assets/96727036/6e3e4884-9185-400f-b758-58034b51de2d)
- 用上面那個範例，在資料庫要怎麼設計: 要先建立一對多的表 例如order跟orderdetail
- 資料庫設計>>前端介面設計>>後端程式架構設計>>子系統interface與外部系統API設計>>整合測試案例設計
- 資料庫設計:ER Diagram (http://www.vertabelo.com/) (drowio)
- ![image](https://github.com/Tomalison/DB/assets/96727036/6ed452f4-cb2b-4e37-8b77-fbb6971b21b8)
- 像是客戶端>城市>國家 是一個多對一的資料。我們盡量會讓我們資料庫設計都是多對一或是一對多，而不是多對多的設計
- 欄位設計 : 名稱若有分隔用底線區分；關鍵欄位請加入註解；像常見的這幾個都可以建立create_by,create_date,update_by,update_date
- 開發文件撰寫(請見軟體開發篇)

#### 工作實際案例分析
- 範例 :帳務管理系統
- ![image](https://github.com/Tomalison/DB/assets/96727036/6ff759f0-6c38-4085-b4e8-a895f46b973e)
- 假設上面的幾個內容，要想出一個結構化的table藍圖(如下)
- ![image](https://github.com/Tomalison/DB/assets/96727036/2b06049a-356b-4e29-9251-76aaa218c14e)

#### 設計資料庫的重要觀念
- 正規化 : 避免資料重複浪費空間和矛盾的情形；使用資料庫時能更有效率更容易維護；正規化有七個階段，但一般來說做到三個就夠了(1NF,2NF,3NF)；每一個階段在進行之前須確認前一個階段已完成；正規化需要在資料庫設計階段就進行
- 1NF : 確認主鍵；每一個欄位只能有一個資料(2013/7/5~2014/7/6 這樣就是要分兩個欄位)；資料表中沒有意義相同的多個欄位 (例如:一階主管、二階主管，這樣要改成階層)
- 2NF : 完成第一正規化；每一個欄位和主鍵沒有部分相依的關係，向下圖範例產品ID跟OrderID沒有直接相依，是部分相依要避免。拆開成orderdetail這張表
- ![image](https://github.com/Tomalison/DB/assets/96727036/1d2ad816-118a-4b88-99bf-505252f4b1c1)
- 3NF : 完成第二正規化；非主鍵之間不能有依賴關係，清單中有數量跟價格，那我們就不需要在建一個total來浪費這兩個計算出來的內容，浪費空間
- ![image](https://github.com/Tomalison/DB/assets/96727036/d4a58646-2677-408a-a712-c66a9b31ec89)

## SQL語法
#### 撈取資料庫資料的關鍵字Select
- select : sql的搜尋敘述從select開始>from資料庫.table名稱>where條件子句
- 若是沒from則是單純列印
- 資料量大時盡量避免
- 搜尋資料請假入條件增加搜尋效率
- 假設資料庫有多個資料庫，select * from orders.orders; 表前面指定資料庫
- 如何限制資料數量 limit 10; 就是限制資料只要10筆
- where customerid = 87 and employeeid = 3; 用and(且)增加篩選條件
#### 多個表格連接在一起的作法
- Join方法 : 將兩個table結合再一起；在where設定結合條件來執行
- 例如 select *  from orders, orderdetails where orders.orderid = orderdetails.orderid
#### 排序
- order by :排序；asc由小到大；desc由大到小
- select * from A order by price desc;
#### 將特定欄位中相同的資料作為分組
- group by : 資料分組；當我們搜尋的欄位中，包含函數的運算時，我們就會使用group by
- select item, sum(price) from list group by item; 他的price就會依照item做加總
#### 資料分組後加入條件，過濾出你想要的資料
- having: 子句能夠過濾條件，控制那些組可以出現在最後結果中，有點像是第二層過濾
- select item, sum(price) from list group by item having sum(price) > 50;  就會抓出大於50的資料；having要加在order by之上，但其他子句之下。
#### 欄位名字過長?表單名字太複雜?暫時取個暱稱來使用
- as : 用來指定欄位別名或是表格別名
- select o.orderid ad order_id  from orders as o, orderdetails as d where o.orderid = d.orderid
#### 不曉得完整、精確的資料內容，也可以找出大概可能的結果
- like：可以找出相同模式的資料　％
- select * from Table where name like 'C%'; %也可前後都放
#### 搜尋出特定範圍的日期或數字資料
- between ...and : 可以找出一個範圍內的資料
- select * from Table where numbers between 1 and 10; 可以介於1~10的資料(包含)
#### 元素比較
- in : 找出符合在in元素中的資料
- not in : 找出不符合在這元素中的資料
- select * from Table where numbers in (5,8); 找出 5跟8的資料 如果是用not in 就會找出除了5跟8以外的資料
#### 子查詢
- 在一個SQL查詢敘述之中，在放入一個SQL查詢
- 子查詢要用刮弧包起來
- 在使用子查詢的時候也可以使用外部SQL的Table與欄位
- ![image](https://github.com/Tomalison/DB/assets/96727036/63f1df8f-14f0-4dfa-8cd7-e1602002d0fe)
- 例如 select * from orders o where o.OrderID in ( select d.OrderID from orderdetails d where o.OrderID = d.OrderID and d.productID = 12); 外層只放了orders這張表，因為我要找出有哪些訂單，然後我要查詢在這OrderID之中 他有哪些訂單是包含產品ID是12的訂單明細
#### 搜尋資料時，用exits會更有效率
- exists : 用來判斷子查詢有沒有查詢的結果
- select * from orders where exists (select d.OrderID from orderdetails d where o.OrderID = d.OrderID and d.productID = 12);
#### 新增資料
- insert : 將資料塞入資料庫當中
- insert into Table(Col_1, Col_2) values (1, 'data'); 將值寫入到各自這兩個欄位
- 將某表資料塞入到另一張表中
```sh
insert into shippers(shipperid, shippername, phone)
select 5, suppliername, phone
from suppliers
where SupplierID = 2;
```
#### 修改資料
- update : 更新資料庫中的資料
- update Table set name = 'Ryan' where id = 1;
``` sh
update shippers
set shippername = 'ABC'
where shipperid = 5;
```
#### 刪除資料
- delete : 將資料庫中的資料刪除
- delete from Table where id = 1;
``` sh
delete from shippers
where shipperid = 5 ;
```
## Mysql函式庫與運算子
#### 數學運算子
- 加減乘除(+-*/)
- select 3 mod 2; 這就是餘數=1
- select 3 div 2; 相除之後的整數
#### 比較運算子
- 大於,小於,等於,不等於(> ,< ,= ,!=)
- select * from products where productid != 1 ; 向這個會把不等於1的全部列出來
#### 邏輯運算子
- ![image](https://github.com/Tomalison/DB/assets/96727036/33a81c05-a13b-42b0-892e-56520d05d976)
- and , or , not(將邏輯運算反過來)
- select * from Table where (name='amy' or name='john'); 找這張表中符合其中一項就可以列出來
- select * from Table where not name = 'cindy'; 找這表不是cindy的所有資料
#### 計算資料的數量
- count : 計算資料的數量
- distinct 呈現不重複的資料
- ![image](https://github.com/Tomalison/DB/assets/96727036/558ceb4c-261b-469a-ba60-0148b0379d91)
- 以上面的範例來說，就是算name有4筆資料；如果是用distinct 他就只會呈現ABC三個資料
- select count(distinct productid) from orderdetails; 可以利用這個結合技巧去計算不重複資料有幾筆
#### 數學運算函式庫
- sum(col):欄位數值的總和
- abs(num):num的絕對值
- round(num,n):num小數點後第n位四捨五入
- truncate(num,n):num值小數點後第n位,無條件捨去
- pow(x,y):x的y次方
- sqrt(num):num的平方根
#### 處理文字的函式庫
- Substring(str,pos):擷取字串從pos位置開始到最後一個 ； select  substring('abcdef',2); 這個範例就會印出bcdef
- Substring(str,pos,len):從pos位置開始，擷取長度len的字串 ； select  substring('abcdef',2,3); 這個範例就會印出bcd
- Concat(A,B):將A字串與B字串結合 ; select concat(lastname,' ',firstname) from employees; 就可以合成像是 Tom SU的名字
- Replace(A,'cde','fgh'):將A欄位或字串中的cdf文字換成fgh文字 

## 資料庫進階功能
#### 建立索引，加快搜尋資料的速度
- index : 提升資料庫搜尋資料的效率
- ![image](https://github.com/Tomalison/DB/assets/96727036/81f827f7-887a-48db-ab82-df9fe0b04e73)
- 如何建立 select * from orders.employees; 假設我們要針對lastname增加索引，找到該表然後找到"索引"功能
- 這個索引觀念要謹記，未來在資料量大時可以使用
#### 當事件發生時，建立一個觸發程序能幫你啟動自動化的程式
- trigger(觸發器_Navicat) 是跟著table去操作的，在insert、update、delete之前或之後扣下扳機
- ![image](https://github.com/Tomalison/DB/assets/96727036/c3d3a049-17a3-4f5c-9512-6d69d3ae4c3b)
- 假設我要在員工after insert後，新增一個trigger。 new.欄位名稱，是要用該欄位的值；sysdate()目前現在的時間(時分秒)
```sh
create definer = current_user trigger 'orders'.'employees_after_insert' after insert on 'employees' for each row
begin
insert into employees_log(name, date) values(new.lastname, sysdate());
end
```
#### 虛擬表格能幫你在應用層少寫一些SQL語法和程式碼，是一個實用技能
- views(檢視功能_Navicat) : 她是像是TABLE但是是由SQL組成的，有時候我們會寫一長串的SQL像是出報表或搜尋資料的SQL，我們就把它包起來變成view，另外開帳號權限給別人使用不用看到原始資料
- ![image](https://github.com/Tomalison/DB/assets/96727036/1a470d95-d646-416d-a9aa-fb9caadb4bdb)

#### 在資料庫中撰寫自己的函式，將流程和邏輯包起來，隨時可使用
- stored procedures(事件) : 我們可能在固定的時間，例如每日或是每週期去產生一些報表給主管去看，或是要匯入到另一張TABLE，就會去儲存這個
```sh
Delimiter $$

create procedure 'add_summary' (sum int, add_time datetime)
begin

if add_time < now() then
  insert into summary(sum, date) values(sum, add_time):
else
  select 'error':
end if:

end
```
- 使用這個procedures方式 : call add_summary(200, str_to_date('2017/10/30','%Y/%m/%d')):
- select * from summary: 就可以看到呼叫這程式的資料
#### 教你如何使用資料庫中內建的函式和常用的函式
- functions(函式_Navicat) 製作自己的函式 例如做一個BMI函式 ；decimal小數點長度是3，到小數點第1位
```sh
Delimiter $$

create function 'bmi' (w decimal(3,1), h decimal(3,1))  
returns decimal(3,1)
begin
return w/pow(h,2):
end
```
- 試看看這函式 : select bmi(55, 1.6);

## 程式語言串連資料庫的設計與實作
#### 安裝Python學習環境for Windows
- 個人使用pycharm
#### Python串接Mysql資料庫
- 在terminal安裝mysql : pip install mysql-connector-python
```sh
from mysql import connector

connection = connector.connect(host='localhost', database='pet100', user='root', password='123') # 連接資料庫
cursor = connection.cursor() # 建立游標物件
cursor.execute('select database()') # 執行SQL指令
result = cursor.fetchall() # 取得所有資料
print(result) # 輸出結果
connection.close() # 要注意關閉，不然常常佔據資源
```
- try 連線資料庫
- except 發生錯誤後的動作
- finally 中斷連線
``` sh
from mysql import connector
try:
    connection = connector.connect(host='localhost', database='pet100', user='root', password='123') # 連接資料庫
    cursor = connection.cursor() # 建立游標物件
    cursor.execute('select database()') # 執行SQL指令
    result = cursor.fetchone() # 取得
    print('目前使用資料庫',result) # 輸出結果
except connector.Error as e:
    print('連線失敗',e)
finally:
    connection.close()
    print('資料庫連線已經關閉')
```
#### 使用參數撰寫SQL語法，避免SQL注入攻擊(SQL INJECTION)
#### Tomcat安裝與說明
#### Tomcat目錄價購與web.xml設定
#### Web系統架構
#### 物件關係對應(ORM)實作

## Mysql資料庫維護
## Nosql資料庫
## SQL語法判斷資料的方式
