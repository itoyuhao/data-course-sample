## 實作「rule-based」& 「content-based」的推薦系統

### 一、專案目的：
根據使用者過去的商品購買紀錄/商品資訊，建立一個推薦系統，以推薦未來使用者合適的商品。


### 二、使用工具：
1. 資料：來自 2014 年 Amazon 發布的資料集
    * 購買記錄(All_Beauty)：2000-01-10 to 2018-10-02 (371345 筆)
      * 訓練資料：2000-01-10 to 2018-09-01 (370752 筆)
      * 測試資料：2018-09-01 to 2018-09-30 (590 筆)
    * 商品資訊(meta_All_Beauty)：32892 筆

2. 使用套件：pandas, numpy


### 三、推薦方法說明：

Week 1:
   1. 思考過程

     * 原先希望能透過使用者過去的購買紀錄，推薦其同品牌(brand)的高評價商品，或是推薦商品資訊中的其他相關商品(also_buy)；探索後發現在590筆測試資料中，發現僅38位使用者曾在訓練資料中出現，因此此方法可能不適用。
     * 衡量後採用兩種方法進行嘗試，兩種方法皆綜合過去的銷售或評分紀錄作為推薦規則

   2. 兩個推薦規則

     * 做法一：推薦熱門程度最高的前10項商品 (熱門程度定義：所有評分紀錄加總) 
     * 做法二：推薦最近一個月銷量排行前十名的商品


Week 2:
   1. 思考過程

     * 結合 Content-Based 與 Rule-Based兩種篩選方式進行推薦
     * 僅取最近一個月的購買紀錄作為訓練資料
     * 嘗試推薦相似的商品給曾購買過商品的使用者(Content-Based)；不足K個或是未曾購買的使用者則推薦熱銷和評分高的商品

   2. 兩個推薦規則

     * Rule-Based：以銷售數量與評分平均數為判斷依據，以銷售數量為主、評分平均數為輔排序) 
     * Content-Based：以相似程度(餘弦距離)排序

### 四、推薦結果：

Week 1:
   1. 評估分數(Recall)：
     * 做法一： 0.083051
     * 做法二： 0.154237

   2. 實作後想法：看起來比起考慮所有歷史銷量與評分的推薦規則，以近一個月的銷量排行來進行推薦會更準一些，但兩者皆仍有很大的優化空間。

Week 2:
   1. 評估分數(Recall)：
     * 0.157627

   2. 實作後想法：納入Content-Based的推薦方法後比起僅用Rule-Based的推薦方式又更準確一些，但皆仍有很大的優化空間。
