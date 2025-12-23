# 一周穿搭管理系統設計與實現

**Weekly Outfit Planning System**

---

## 📋 目錄

* 需求說明書（Software Requirement Specification, SRS）
* 概要設計說明書（High-Level Design）
* 詳細設計說明書（Detailed Design）
* 測試計畫（Test Plan）
* 結論與未來展望

---

## 一、需求說明書（Software Requirement Specification, SRS）

### 1.1 系統目的

現代使用者在日常生活中需頻繁思考每日穿搭，往往需同時考量天氣、場合與衣物重複率，容易造成決策負擔。本系統旨在提供一套完整的一周穿搭管理解決方案，協助使用者：

* 系統化管理個人衣櫃資料
* 根據天氣與使用者偏好自動產生每日穿搭
* 提前規劃一周穿搭，降低日常選擇成本
* 提升穿搭一致性與生活效率

---

### 1.2 使用者角色（User Roles）

#### 1. 一般使用者（User）

* 建立與管理個人衣櫃
* 設定穿搭偏好（顏色、場合、季節）
* 查看每日／一周穿搭建議
* 手動調整穿搭結果

（UML：Use Case Diagram）

---

#### 2. 系統管理者（Administrator）

* 管理衣物分類與穿搭規則
* 維護系統基本資料
* 檢視穿搭統計資料

（UML：Use Case Diagram）

---

### 1.3 功能性需求（Functional Requirements）

* FR1：使用者登入／登出系統
* FR2：使用者新增、修改與刪除衣物資料
* FR3：系統可整合天氣資料來源
* FR4：系統自動產生每日與一周穿搭建議
* FR5：使用者可手動調整穿搭內容並儲存

---

### 1.4 非功能性需求（Non-Functional Requirements）

* 效能需求：穿搭建議產生時間 ≤ 3 秒
* 安全性需求：使用者資料需安全儲存
* 可用性需求：介面操作簡單直覺
* 擴充性需求：未來可加入 AI 穿搭推薦

---

### 1.5 介面需求

系統提供圖形化使用者介面（GUI），包含：

* 登入畫面
* 衣櫃管理頁面
* 一周穿搭日曆頁面
* 穿搭調整介面

  
###1.6 UML：使用案例圖（Use Case Diagram）


<img width="486" height="630" alt="3" src="https://github.com/user-attachments/assets/9413d63f-d563-4865-81a6-fc8cf14d5e53" />

## 二、概要設計說明書（High-Level Design）

### 2.1 系統架構

本系統採用**三層式架構（Three-Tier Architecture）**：

1. **表現層（UI Layer）**

   * 提供使用者操作介面
2. **穿搭邏輯層（Logic / Service Layer）**

   * 處理穿搭推薦與業務邏輯
3. **資料層（Data Layer）**

   * 儲存衣物、穿搭與使用者資料

### 2.2 系統模組劃分

系統主要模組如下：

* 使用者管理模組（User Module）
* 衣櫃管理模組（Closet Module）
* 穿搭推薦模組（Outfit Recommendation Module）
* 天氣整合模組（Weather Integration Module）
* 行事曆顯示模組（Calendar Module）

---

### 2.3 模組關係（Component Diagram）

各模組透過穿搭邏輯層進行協作，UI 層不直接存取資料層，以確保系統模組間低耦合、高內聚。

<img width="734" height="391" alt="2" src="https://github.com/user-attachments/assets/1c7d1bdc-a571-4d20-b43d-035d54065ed6" />

---

### 2.4 類別設計（Class Diagram）

主要類別包含：

* User
* Clothes
* Outfit
* WeatherInfo

（UML：Class Diagram）

---

## 三、詳細設計說明書（Detailed Design）

### 3.1 一周穿搭產生流程（Sequence Diagram）

當使用者請求一周穿搭時，系統執行以下互動流程：

1. User 透過 App 發出請求
2. App 呼叫穿搭邏輯層
3. 邏輯層存取衣櫃資料
4. 邏輯層呼叫 Weather API
5. 整合結果後回傳給 App

<img width="408" height="622" alt="4" src="https://github.com/user-attachments/assets/9a6a7f6a-946e-41f6-a044-b59491f656b2" />

---

### 3.2 穿搭推薦流程（Pseudo Flow）

1. 使用者進入一周穿搭頁面
2. 系統取得未來一周天氣資料
3. 系統讀取使用者衣櫃資料
4. 依季節與場合篩選可用衣物
5. 組合每日穿搭
6. 檢查並避免重複穿搭
7. 輸出一周穿搭結果

---

### 3.3 UML：活動圖（Activity Diagram）

活動圖描述穿搭流程中的決策與分支，例如：

* 天氣是否適合
* 是否有可用衣物
* 是否需重新產生穿搭

（UML：Activity Diagram）

---

## 四、測試計畫（Test Plan）

### 4.1 測試目標

本測試計畫旨在驗證一周穿搭管理系統是否符合需求說明書中定義之功能與非功能需求，確保系統在三層式架構下能正確運作。

---

### 4.2 測試策略與方法

測試採分層策略，包含：

* 功能測試
* 系統整合測試
* 流程與例外測試

測試設計以 UML 圖作為依據，以提升測試覆蓋率與可追蹤性。

---

### 4.3 功能測試（Functional Testing）

* 衣櫃管理功能測試：驗證衣物新增、修改與刪除功能正確性
* 每日穿搭產生功能測試：驗證系統依天氣與衣櫃資料自動生成每日穿搭的正確性
* 一周穿搭顯示功能測試：驗證系統將每日穿搭整合並正確顯示於一周行事曆
* 手動調整穿搭功能測試：驗證使用者手動調整穿搭後，系統能正確儲存與更新顯示結果

<img width="382" height="301" alt="7" src="https://github.com/user-attachments/assets/186504c5-90d4-4e57-8bf9-c08a455a78af" />


---

### 4.4 系統整合測試（Integration Testing）

驗證 UI、Logic 與 Data Layer 間的互動是否正確，確保資料流與呼叫順序符合設計。

（UML：Sequence Diagram）

---

### 4.5 流程與例外測試（Process and Exception Testing）

測試以下情境：

* 衣櫃資料不足
* 天氣資料取得失敗
* 使用者手動調整穿搭

（UML：Activity Diagram）

---

### 4.6 測試完成準則

當所有測試案例皆通過，且未發現重大流程或功能錯誤，即視為測試完成。

---

### 4.7 測試資源

* 測試人員：2 人
* 測試環境：Web / Mobile
* 測試資料：模擬衣物與穿搭資料

---

## 五、結論與未來展望

### 5.1 結論

本專題完成一套具備完整系統架構與流程設計的一周穿搭管理系統，並依循軟體工程方法進行需求分析、系統設計與測試規劃。透過 UML 圖輔助說明，使系統結構與行為具備良好可讀性與一致性。

---

### 5.2 未來展望

未來可導入：

* AI 圖像辨識自動分類衣物
* 使用者穿搭偏好學習
* 跨平台行動應用整合

以提升系統智慧化與實用性。

---
<img width="777" height="441" alt="1" src="https://github.com/user-attachments/assets/2171f738-6a41-4a00-96e8-d04df3cfbb48" />
<img width="734" height="391" alt="2" src="https://github.com/user-attachments/assets/1c7d1bdc-a571-4d20-b43d-035d54065ed6" />
<img width="486" height="630" alt="3" src="https://github.com/user-attachments/assets/9413d63f-d563-4865-81a6-fc8cf14d5e53" />
<img width="408" height="622" alt="4" src="https://github.com/user-attachments/assets/9a6a7f6a-946e-41f6-a044-b59491f656b2" />
<img width="754" height="446" alt="5" src="https://github.com/user-attachments/assets/cbd9c83e-6ea5-4d3d-9e48-cacab9411c00" />
<img width="762" height="262" alt="6" src="https://github.com/user-attachments/assets/afd81c4e-6baa-440e-a5b6-2af43e4c8478" />
<img width="382" height="301" alt="7" src="https://github.com/user-attachments/assets/186504c5-90d4-4e57-8bf9-c08a455a78af" />
