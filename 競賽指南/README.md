# 2024 AI Cup TW (Generative-AI Navigation Information Competition for UAV Reconnaissance) (4/128=3.1%) - Excellent Award

## 🎯 競賽目標：高分至上，不談新穎性

這次參與的比賽是 2024 年 AICUP 台灣場的無人機偵察任務，目標是從空拍影像中預測出 **河岸線** 和 **車道邊界**，也就是一種像素級的 **邊緣偵測任務**。

與研究領域追求創新方法不同，競賽最重要的是——**分數！分數！還是分數！**  
為了得分，我們可以捨棄 fancy 的模型創新，改用穩定、成熟且效果強的技術 —— **Ensemble Learning**。

---

## 🧠 常見的致勝法寶：Ensemble Learning

### 什麼是 Ensemble Learning？

Ensemble Learning（集成學習）是一種透過**結合多個模型的預測結果**來提高整體準確率的技巧。  
它的基本邏輯是：

- 單一模型容易出錯或有偏誤。
- 多個模型若能在同一像素達成共識，就可能代表「這是正確答案」。
- 常見的集成方法有：**平均（average）、投票（voting）、權重加總（weighted ensemble）**等。

### 為什麼這麼有效，卻很少見於 paper？

- Paper 通常追求方法新穎性，Ensemble 不是一個「新方法」，而是「組合策略」，很難被當作主要貢獻點。
- 但在競賽裡，Ensemble 是**壓分數的秘密武器**，尤其是當單一模型已經接近極限時，集成是往上突破的關鍵。

---

## 🔧 我的方法：從基礎做起，一步步強化

這次的實作流程，我從最簡單的 baseline 做起，並依序加入改進策略，直到最後透過 Ensemble 獲得顯著提升。

### Step 1: 建立 baseline 模型

- 使用簡單的 encoder-decoder 結構
- 每類別（河流 / 車道）各訓練 200 張圖測試效果  
➡️ 分數：約 **0.630**

---

### Step 2: 使用全訓練集

- 原本的 baseline 模型，擴大資料量至全部 2160 張圖  
➡️ 分數提升至 **0.672**

---

### Step 3: 更換模型為 UNet

- 換成 2015 年的 UNet（具 skip connection 的 segmentation 經典模型）  
➡️ 分數：**0.730**

---

### Step 4: 精修 UNet 結構

- 微調模型結構與訓練參數  
➡️ 分數：**0.739**

---

### Step 5: Ensemble Learning 導入

- 嘗試集成 UNet、Restormer（CVPR 2021）、ZoomNet（CVPR 2022）等多個模型
- 對每一個 pixel 進行 **投票（voting）**
- 多模型一致預測即為最終結果  
➡️ 最終分數：**0.797**

---

## 🧪 實驗分析與未來展望

- 進行 ablation study 分析每個策略的貢獻
- 未來可嘗試：
  - 測試時的資料增強（TTA）
  - 使用預訓練權重做 transfer learning
  - 更複雜的集成策略（如 stacking）

---

## ✅ 結語

這次比賽最大的收穫是：

- 不用追求 fancy 的方法，只要有效，**Ensemble Learning 一樣可以稱霸排行榜**
- 訓練資料品質與模型穩定性，是比賽關鍵
- 競賽最講究實作力與 debug 能力，不輸研究的思考深度

---

👨‍💻 Author: Sheng-An Wang (Andy 王聖安)