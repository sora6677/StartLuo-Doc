# StartLuo-backend.md 活動後台

## 共用錯誤代碼
|回傳碼|說明|
|---|---|
|200|成功|
|1000|異常錯誤|
|1001|資料異常|
|1002|連線異常|
|1003|令牌失效|
|1004|更新失敗|

***
## ManagerLogin - 管理員登入
```
URL：api/manager/ManagerLogin.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  ManagerAccount(string)：管理員帳號
  ManagerPassword(string)：管理員密碼
傳入範例：
  data={"ManagerAccount":"xxx","ManagerPassword":"xxx"}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
    ManagerId(string)：管理員ID
    ManagerToken(string)：管理員令牌
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"ManagerId":"1","ManagerToken":"1bab341c06ca0d432e3d37adc892a4a1"}}
失敗範例：
  {"status":1101,"msg":"登入失敗","data":{}}
  {"status":1102,"msg":"密碼錯誤","data":{}}
```

## ManagerLogout - 管理員登出
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/manager/ManagerLogout.php
MetHod：GET
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  參考共用錯誤代碼
```

***
## 頁面說明
### 各頁面類型對應
|類型代碼|說明|
|---|---|
|101|官網主頁|
|102|發財開始囉|
|103|賺錢開始鑼|
|104|最新活動|
|105|音樂祭活動|
|106|沙漏活動|
|107|皂飛車活動|
|108|品牌與名人|
|109|服務條款|

### 頁面內容參考
[StartLuo 頁面內容文件](https://github.com/kd20220905/StartLuo_back/blob/main/back.md#startluo)

## SetPageContent - 寫入頁面訊息
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startpage/SetPageContent.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  pageType(int)：頁面類型代碼 **參考 各頁面類型對應
  pageContent(string)：頁面內容
傳入範例：
  data={"pageType":101,"pageContent":{......}}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  {"status":1103,"msg":"查無此頁面","data":{}}
```

## GetPageContent - 取得頁面訊息
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startpage/GetPageContent.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  pageType(int)：頁面類型代碼 **參考 各頁面類型對應
傳入範例：
  data={"pageType":101}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
    content(object)：頁面內容
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"content":{......}}}
失敗範例：
  {"status":1103,"msg":"查無此頁面","data":{}}
```

***
## StartLuoList - 沙漏期數列表
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/StartLuoList.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  RowCount(int)：取得筆數 範圍 10 ~ 100
  GetPage(int)：取得頁數 範圍 >1
傳入範例：
  data={"RowCount":10,"GetPage":1}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object array)：
    TotalPage(int)：總頁數
    TotalCount(int)：總筆數
    PeriodList(object array)：
      PeriodId(int)：期數ID
      StartDateTime(string)：活動開始時間
      EndDateTime(string)：活動結束時間
      BetEndDateTime(string)：下注結束時間
      HourClassStartTime(string)：沙漏開始時間
      HourClassEndTime(string)：沙漏結束時間
      IsNow(int)：期數進行中
      BetCount(int)：注單總量
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"TotalPage":1,"TotalCount":2,"PeriodList":[{"PeriodId":2,"StartDateTime":"2023-01-14 17:00:00","EndDateTime":"2023-01-21 16:59:59","BetEndDateTime":"2023-01-21 15:00:00","HourClassStartTime":"0000-00-00 00:00:00","HourClassEndTime":"00:00:00","IsNow":0,"BetCount":0},{"PeriodId":1,"StartDateTime":"2023-01-06 12:00:00","EndDateTime":"2023-01-14 16:59:59","BetEndDateTime":"2023-01-14 15:00:00","HourClassStartTime":"2023-01-04 00:00:00","HourClassEndTime":"00:00:00","IsNow":1,"BetCount":1}]}}
失敗範例：
  參考共用錯誤代碼
```

## StartLuoDefault - 取得期數預設時間
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/StartLuoDefault.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
傳入範例：
  data={"PeriodId":1}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object array)：
    DefaultStartDateTime(string)：預設-活動開始時間
    DefaultEndDateTime(string)：預設-活動結束時間
    DefaultBetEndDateTime(string)：預設-下注結束時間
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"DefaultStartDateTime":"2023-01-04 00:00:00","DefaultEndDateTime":"2023-01-06 00:00:00","DefaultBetEndDateTime":"2023-01-05 00:00:00"}}
失敗範例：
  參考共用錯誤代碼 或
  {"status":1104,"msg":"期數資料異常","data":{}}
```

## StartLuoStart - 活動開始
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/StartLuoStart.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
  StartDateTime(string)：開始時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
傳入範例：
  data={"PeriodId":1,"StartDateTime":"2022-12-30 13:00:00"}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  參考共用錯誤代碼 或
  {"status":1104,"msg":"期數資料異常","data":{}}
```

## StartLuoEnd - 活動結束
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/StartLuoEnd.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
  EndDateTime(string)：開始時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
傳入範例：
  data={"PeriodId":1,"EndDateTime":"2022-12-30 13:00:00"}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  參考共用錯誤代碼 或
  {"status":1104,"msg":"期數資料異常","data":{}}
```

## BetStop - 停止下注
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/BetStop.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
  StopDateTime(string)：下注停止時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
傳入範例：
  data={"PeriodId":1,"StopDateTime":"2022-12-30 16:00:00"}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  參考共用錯誤代碼 或
  {"status":1104,"msg":"期數資料異常","data":{}}
```

## HourglassStart - 沙漏開始
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/HourglassStart.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
傳入範例：
  data={"PeriodId":1}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  參考共用錯誤代碼 或
  {"status":1104,"msg":"期數資料異常","data":{}}
```

## HourglassEnd - 沙漏結束
```
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/HourglassEnd.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
  EndTime(string)：結束時間 格式:HH:ii:ss (24 小時制)
傳入範例：
  data={"PeriodId":1,"EndTime":"16:00:00"}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{}}
失敗範例：
  參考共用錯誤代碼 或
  {"status":1104,"msg":"期數資料異常","data":{}}
```

## WinList - 中獎列表
```
**目前僅列當期
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/WinList.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  RowCount(int)：取得筆數 範圍 10 ~ 100
  GetPage(int)：取得頁數 範圍 >1
  PeriodId(int)：期數ID
  StartDateTime(string)：最後修改注單時間-起始時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
  EndDateTime(string)：最後修改注單時間-結束時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
傳入範例：
  data={"RowCount":10,"GetPage":1,"PeriodId":1,"StartDateTime":"2023-01-03 15:00:00","EndDateTime":"2023-01-03 18:00:00"}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
    TotalPage(int)：總頁數
    TotalCount(int)：總筆數
    WinList(object array)：
      MemberId(string)：玩家的 memberID
      NickName(string)：玩家暱稱
      UserPhone(string)：玩家手機
      PeriodId(int)：期數Id
      BetNo(int)：玩家注單編號
      QuizTime(string)：競猜時間 格式:HH:ii:ss (24 小時制)
      UpdateDateTime(string)：最後修改注單時間
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"TotalPage":1,"TotalRows":1,"WinList":[{"MemberId":"LFtjoUck3CPDEWtkxfI77Csudfg2","NickName":"Daisy00001","UserPhone":"0988888888","PeriodId":1,"BetNo":1,"QuizTime":"15:36:00","UpdateDateTime":"2023-01-05 12:20:32"}]}}
失敗範例：
  參考共用錯誤代碼
```

## BetList - 注單列表
```
**目前僅列當期
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/BetList.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  RowCount(int)：取得筆數 範圍 10 ~ 1000
  GetPage(int)：取得頁數 範圍 >1
  PeriodId(int)：期數ID
  QuizStartTime(string)：競猜時間-起始 格式:HH:ii:ss (24 小時制) **當 IsAll = 0 時為必填
  QuizEndTime(string)：競猜時間-結束 格式:HH:ii:ss (24 小時制)  **當 IsAll = 0 時為必填
  StartDateTime(string)：最後修改注單時間-起始時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
  EndDateTime(string)：最後修改注單時間-結束時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
  IsAll(int)：是否查 StartDateTime ~ EndDateTime 內的全部注單 0:依競猜時間查詢 1:查全部
傳入範例：
  data={"RowCount":10,"GetPage":1,"PeriodId":1,"QuizStartTime":"01:00:00","QuizEndTime":"02:00:00","StartDateTime":"2023-01-07 00:00:00","EndDateTime":"2023-01-08 00:00:00","IsAll":0}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
    TotalPage(int)：總頁數
    TotalCount(int)：總筆數
    BetList(object array)：
      BetId(int)：注單唯一碼
      MemberId(string)：玩家的 memberID
      NickName(string)：玩家暱稱
      UserPhone(string)：玩家手機
      PeriodId(int)：期數
      BetNo(int)：玩家注單編號
      UseId(int)：票券交易ID
      QuizTime(string)：競猜時間 格式:HH:ii:ss (24 小時制)
      UpdateDateTime(string)：最後修改注單時間
      UseStatus(int)：票券狀態 是否已使用 0:處理中 1:成功 2:異常 3:餘額不足 4:失敗
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"TotalPage":1,"TotalRows":1,"BetList":[{"BetId":167281844214494,"MemberId":"LFtjoUck3CPDEWtkxfI77Csudfg2","NickName":"Daisy00001","UserPhone":"0988888888","PeriodId":0,"BetNo":1,"UseId":167299919212197,"QuizTime":"15:50:00","UpdateDateTime":"2023-01-06 18:00:02","UseStatus":1}]}}
失敗範例：
  參考共用錯誤代碼
```

## BetListAll - 注單列表不分頁
```
**目前僅列當期
Header：
  ManagerId(string)：管理員 (唯一碼)
  ManagerToken(string)：身分驗證令牌
```

```
URL：api/startluo/BetListAll.php
MetHod：POST
傳入參數：
  data：JSON
傳入JSON：
  PeriodId(int)：期數ID
  QuizStartTime(string)：競猜時間-起始 格式:HH:ii:ss (24 小時制) **當 IsAll = 0 時為必填
  QuizEndTime(string)：競猜時間-結束 格式:HH:ii:ss (24 小時制)  **當 IsAll = 0 時為必填
  StartDateTime(string)：最後修改注單時間-起始時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
  EndDateTime(string)：最後修改注單時間-結束時間 格式:yyyy-mm-dd HH:ii:ss (24 小時制)
  IsAll(int)：是否查 StartDateTime ~ EndDateTime 內的全部注單 0:依競猜時間查詢 1:查全部
傳入範例：
  data={"PeriodId":1,"QuizStartTime":"01:00:00","QuizEndTime":"02:00:00","StartDateTime":"2023-01-07 00:00:00","EndDateTime":"2023-01-08 00:00:00","IsAll":0}
```

```
回傳參數：
  status(int)：代碼
  msg(string)：訊息
  data(object)：
    BetList(object array)：
      BetId(int)：注單唯一碼
      MemberId(string)：玩家的 memberID
      NickName(string)：玩家暱稱
      UserPhone(string)：玩家手機
      PeriodId(int)：期數
      BetNo(int)：玩家注單編號
      UseId(int)：票券交易ID
      QuizTime(string)：競猜時間 格式:HH:ii:ss (24 小時制)
      UpdateDateTime(string)：最後修改注單時間
      UseStatus(int)：票券狀態 是否已使用 0:處理中 1:成功 2:異常 3:餘額不足 4:失敗
回傳方式：JSON
```

```
成功範例：
  {"status":200,"msg":"成功","data":{"BetList":[{"BetId":167281844214494,"MemberId":"LFtjoUck3CPDEWtkxfI77Csudfg2","NickName":"Daisy00001","UserPhone":"0988888888","PeriodId":0,"BetNo":1,"UseId":167299919212197,"QuizTime":"15:50:00","UpdateDateTime":"2023-01-06 18:00:02","UseStatus":1}]}}
失敗範例：
  參考共用錯誤代碼
```

