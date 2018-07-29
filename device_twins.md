# Azure iot hub Device Twin

## 裝置對應項

### 簡介
每有一個裝置連線到iot hub ，就會產生一個對應的裝置對應項，以JSON的資料格式來儲存裝置的相關資訊，包括metadata, configuration, condition 。裝置對應項是可以雙向溝通的(D2C,C2D)，在Azure IoT hub 的配置當中是屬於標準層才可以使用的。裝置對應項可以在雲端儲存特定的中繼資料、從裝置的應用程式中得知目前裝置的狀況、同步處理裝置端和後端的工作流程狀態(更新資料)、查詢裝置的資訊
### 文件內容
JSON文件中有四個部分
-  Tags:後端可以讀取和寫入的json部分，裝置端看不到
-  Desired properties:讓裝置端的應用程式可以接收後端的需求
-  Reported properties:讓後端了解裝置端的狀況還有可以讀取查詢
   *desired properties 和 reported properties 需互相搭配使用，來同步處理配置組態及狀況
-  Device identity properties:紀錄裝置的metadata

![alt tag](https://i.imgur.com/VKWL43U.png)

![alt tag](https://i.imgur.com/gpPIzpF.png)

標籤、所需屬性和報告屬性全都支援開放式並行存取
Etag是用來確保標籤資料的一致性，而version則會依照版本的不同有一個遞增直，更新端可以使用版本強制達到更新的一致性(避免裝置和雲端同時存取資料造成資訊不一致)
$ 代表該資料室唯讀屬性
標籤、所需屬性和報告屬性中所有 JSON 物件的深度上限為 5。
所有字串值的最大長度為 4 KB

## D2C
當資料從前端裝置到後端的解決方案的時候，可針對傳輸的型態提供三個方式
1. 裝置到雲端訊息
2. 裝置對應項的回報屬性
3. 上傳檔案

![alt tag](https://i.imgur.com/XxTlSGb.png)

*當我有需要傳送遙測資訊或是警示的時候，有兩種做法可以用D2C的方式傳送或是夾帶在標籤中，但是建議不要使用第二種，由於裝置到雲端訊息允許高於裝置對應項更新的輸送量，所以有時希望避免針對每則裝置到雲端訊息更新裝置對應項。

![alt tag](https://i.imgur.com/wkEghgS.png)

## C2D
Iot hub 提供3個從裝置端到雲端的功能
1. 直接方法:需要立即確認結果的通訊，通常用於裝置的互動式控制，例如開啟風扇。
2. 對應項的所需屬性，適用於可讓裝置進入特定所需狀態的長時間執行命令。 例如，將遙測傳送間隔設定為 30 分鐘。
3. 雲端到裝置訊息，適用於對裝置應用程式的單向通知。


![alt tag](https://i.imgur.com/QBTQtt9.png)

![alt tag](https://i.imgur.com/51qPOVM.png)

## 裝置與模組對應項、作業和訊息路由的 IoT 中樞查詢語言

Source: https://docs.microsoft.com/zh-tw/azure/iot-hub/iot-hub-devguide-query-language

每個「IoT 中樞」查詢都包含 SELECT 和 FROM 子句，以及選擇性的 WHERE 和 GROUP BY 子句。 每個查詢都會在 JSON 文件的集合上執行，例如裝置對應項。 FROM 子句會指出要在其上反覆運算的文件集合 (devices 或 devices.jobs)。 然後，會套用 WHERE 子句中的篩選。 使用彙總時，此步驟的結果會依照 GROUP BY 子句中所指定的方式進行分組。 針對每個群組，會依照 SELECT 子句中所指定的方式產生一個資料列。

### FROM 子句
FROM <from_specification> 子句只能採用兩個值︰FROM devices (用來查詢裝置對應項) 或 FROM devices.jobs (用來查詢每一裝置的作業詳細資料)。

### WHERE 子句
WHERE <filter_condition> 子句是選擇性的。 它會指定一或多個條件，而且 FROM 集合中的 JSON 文件必須滿足這些條件，才能納入為結果的一部分。 任何 JSON 文件都必須將指定的條件評估為 "true"，才能併入結果。
運算式和條件一節中會說明允許的條件。

### SELECT 子句
SELECT <select_list> 是必要子句，可指定要從查詢擷取的值。 它會指定用來產生新 JSON 物件的 JSON 值。 針對已篩選 (及視需要已分組) 之 FROM 集合子集的每個項目，投影階段會產生一個新的 JSON 物件。 此物件會以 SELECT 子句中所指定的值來建構。

### GROUP BY 子句
GROUP BY <group_specification> 子句是一個選擇性步驟，會在 WHERE 子句中指定的篩選之後、SELECT 中指定的投影之前執行。 它會根據屬性值來分組文件。 這些群組可用來產生 SELECT 子句中所指定的彙總值。
