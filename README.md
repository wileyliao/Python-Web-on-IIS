# Python-Web-on-IIS
Build Python Web on IIS Step by Step

## Python app env
`pip install wfastcgi` <br>
運行：`wfastcgi-enable.exe` <br>
會回傳回應『已將設定變更套用......』 <br>
複製路徑供後續設置使用：`disk:\path\to\your\python.exe|disk:\path\to\your\wfastcgi.py`

## 1. 開啟CGI服務並新增站台
- 控制台 -> 程式集 -> 程式與功能 -> 開啟或關閉Windows功能 -> IIS -> WWW服務 -> 應用程式與開發功能 -> CGI <br>
- 右鍵站台 -> 新增網站 -> 設定站台名稱、實體路徑(專案根目錄)、連接阜(api呼叫的port號)

## 2. 在IIS中創建網站並新增Python APP
- 點選新站台 -> 處理常式對應 -> 新增模組對應： <br>
(要求路徑：*)、(模組：FastCgiModule)、(執行檔：wfastcgi-enable的回應)、(名稱：該專案名)、(要求限制：取消勾選)

## 3. 設定FastCGI執行位置與識別方式
- 本機IIS -> FastCGI設定 -> 剛新增的應用程式 -> 環境變數： <br>
  加入兩個：(1. Name = `PYTHONPATH`，Value = app的資料夾位置)、(2. Name = `WSGI_HANDLER`，Value = `appfile.app`)
- 應用程式集區 -> 剛新增的應用程式 -> 進階設定 -> 產生處理序模型事件紀錄項目 -> 識別：LocalSystem

## Repeat 2. & 3. 可以在同一站台下管理不同的專案
