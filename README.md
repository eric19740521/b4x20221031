# b4x20221031
B4X實驗:  NON-UI時,ResumableSub處理辦法??  Coroutine(輕量級的執行緒) ???實作工作排程APP(B4J)
B4X實驗:  NON-UI時,ResumableSub處理辦法??  Coroutine(輕量級的執行緒) ???實作工作排程APP(B4J)
Insider Tips:Because of the ability, there is no English document. But you can use google translate
參考資料:
Resumable Subs - Sleep / Wait For 用法
https://www.b4x.com/android/forum/threads/b4x-resumable-subs-sleep-wait-for.78601/

ResumableSub in Non-UI app
https://www.b4x.com/android/forum/threads/resumablesub-in-non-ui-app.106663/#content

Resumable Subs (wait for / sleep) in server handlers
https://www.b4x.com/android/forum/threads/resumable-subs-wait-for-sleep-in-server-handlers.81833/	


1.Resumable subs為何???

Resumable subs 是 B4J v5.50 / B4i v4.00 / B4A v7.00 中添加的新功能。它極大地簡化了異步任務的處理。
（這個特性是無堆棧協程
的一個變種。） 可恢復的子程序的特殊特性是它們可以被暫停，而不用暫停正在執行的線程，然後再被恢復。
 該程序不會等待可恢復的子程序繼續。其他事件將照常舉行。
 任何一次或多次調用睡眠或等待的潛艇都是可恢復的潛艇。IDE 在子聲明旁邊顯示一個指示器：
https://www.b4x.com/android/forum/threads/b4x-resumable-subs-sleep-wait-for.78601/


2.Resumable Subs 在Server用法
Handle sub 本身不能是可恢復的 sub。

為什麼？

- Wait For / Sleep 必須在調用 StartMessageLoop 之前調用，否則它們將永遠不會被執行。
- Wait For / Sleep 代碼流等效於 Return，因此如果它們出現在 StartMessageLoop 之前，則永遠不會創建消息循環，並且處理程序將在引發事件之前完成。

WebSocket 處理程序確實有一個消息循環，所以不應該在那裡做任何特別的事情。

提示：使用正確的庫。
OkHttpUtils2_NonUI 用於服務器應用程序，OkHttpUtils2 用於 UI 應用程序。
以上提示不再正確。由於 OkHttpUtils2 是一個 b4xlib，因此您應該始終使用 OkHttpUtils2。


3.NON-UI
t01展示..
   沒有使用StartMessageLoop ==> 看結果
   有使用StartMessageLoop   ==> 看結果

t02展示
   利用論壇上的範例 ==> 看結果

t03展示
   自己寫一個下載的範例,不加StartMessageLoop  ==> 看結果
			不加StopMessageLoop


   自己寫一個下載的範例,加StartMessageLoop  
			不加StopMessageLoop ==> 看結果	


   自己寫一個下載的範例,加StartMessageLoop  
			加StopMessageLoop ==> 看結果


4.自己動手寫一個有N個工作的工作排程APP
t04.jar
Sleep or Wait For is a resumable subs
此功能是 stackless 的變體
Coroutines 可看作是輕量級的執行緒
https://ithelp.ithome.com.tw/articles/10261501 參考此文章


執行緒
 


比如發訊息時,發到line(1),寄信到EMAIL(2)

程式碼
https://github.com/eric19740521/b4x20221031


	

   





