---
title: "\U0001F4CD流程圖（ Flow Chart ）"
tags: [流程圖]

---

# 📍流程圖（ Flow Chart ）
###### tags: `流程圖`
將瑣碎且複雜的資料整理、歸納，讓其他人對你的程式內容一目了然。
不同人對不同圖像也會有不一樣的差異，為了減少此問題，我們必需要統一流程圖的圖像。

+ 線上繪製流程圖：[Draw.io](https://www.draw.io/)
+ Draw.io教學：[免費流程圖線上繪製軟體 Draw.io簡介](http://newsletter.ascc.sinica.edu.tw/news/read_news.php?nid=3547)

### 圖示說明
|名稱|圖示|用途|
|:---:|:---:|---|
|開始端 / 結束端|![](https://i.imgur.com/QN4tbEI.png)|第一個步驟和最後一個步驟，會用橢圓形的符號來代表。|
|輸入|![](https://i.imgur.com/h8mJAcD.png)|輸入內容。
|副程式 / 一堆程式步驟|![](https://i.imgur.com/sHTBS67.png)|可視為另一份流程。
|單一程式步驟|![](https://i.imgur.com/3xKUkpm.png)|代表中間的步驟，用箭頭做連接。|
|條件判斷|![](https://i.imgur.com/hevrEW5.png)|會因為不同選擇走向不同的流程。|
|文黨 / 文案|![](https://i.imgur.com/X2dV3Ci.png)|若有產出文件檔，或者是有需要參閱文件時使用|

### 流程圖規則
1. 表示相應操作的框。
2. 帶箭頭的流程線。
3. 框內外必要的文字說明。
4. 結構內的每一部分都有機會被執行到。
5. 結構內不存在“閉環”。
### 範例
![](https://i.imgur.com/h6EPKXf.png)
:::info
先把流程圖規定好，考慮可行性、邏輯性...第二步才撰寫程式。
:::
###### 資料來源：[流程圖（Flow Chart）常用符號說明](https://free.com.tw/flow-chart-symbols-and-usage/)、[從零開始：流程圖[1]](https://ithelp.ithome.com.tw/articles/10196068)、[流程圖說明](http://www2.lssh.tp.edu.tw/~hlf/class-1/lang-c/flow/flow-chat.htm)


## 📍循序流程圖（ Sequence Diagram ）
清楚地傳遞各物件在時間軸上的互動情境，因此透過圖來標示參與的所有物件有哪些，以及在各時間點彼此互動的情況，幫助閱讀的人可以快速及清晰地掌握細節。

### 圖示說明
![](https://i.imgur.com/3YkTKuI.png)
1. **參與者(Participants)**：參與互動的物件，內文格式為 名稱 : 類別名稱
2. **生命線(Lifeline)**：表示互動發生的時間軸
3. **執行發起(Execution Occurrence)**：描繪生命線內某個執行單元
4. **訊息(Message)**：呼叫目標物件的實際作為
5. **合併片段(Combined Fragment)**：描述不同情況下可能發生的變化(opt=option)
6. **回傳訊息(Reply Message)**：非必須符號，因為執行發起的結束點就隱含此意了

### 合併片段(Combined Fragment)
+ **alt (Alternatives)**：任何情況只有一個序列發生，是互斥的條件。
   **範例**：電腦寫程式，不然就用電腦聽音樂
    ![](https://i.imgur.com/rO8L5B2.png)

+ **par (Parallel)**：平行處理，片段中的事件可以交錯執行。
    **範例**：平行處理，片段中的事件可以交錯執行。
    ![](https://i.imgur.com/6I2NJbY.png)
+ **opt (Option)**：選擇項，不一定會發生的序列(要符合條件)。
    **範例**：工程師卡關的時候會查詢點部落求解答。
    ![](https://i.imgur.com/t2Vmq6c.png)
+ **loop**：重複片段。可以設立重複的條件，若未設定最小級最大重複次數，預設表示無限制。
    **範例**：工程師只要卡關，直接無窮盡地使用電腦進行Google搜尋，直到找到解決方案才會罷休。
    ![](https://i.imgur.com/3OzEEfN.png)
+ **ref(Reference)**：表示參考另一個互動循序圖，屬於Interaction Use範疇。
    **範例**：顧客在使用網站時都需要登入，而登入細節於此不贅述(直接參考到登入循序圖即可)。
    ![](https://i.imgur.com/m1J1P4F.png)


###### 資料來源：[[UML] 使用循序圖傳達各物件互動及時序關係](https://dotblogs.com.tw/wasichris/2016/03/17/232341)
