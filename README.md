# ntut-project
independent study in drone

單樣本物件偵測系統開發 基於 os2d

# Paper Reference
- [1]  A. Osokin, et al., "OS2D: One-Stage One-Shot Object Detection by Matching 
Anchor Features," arXiv:2003.06800, 2020. [Online]. Available: 
https://arxiv.org/abs/2003.06800 
Github: https://github.com/aosokin/os2d
- [2]  K. He, et al., "Deep Residual Learning for Image Recognition," in Proceedings of 
the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016. 
[Online]. Available: https://arxiv.org/abs/1512.03385
- [3]  I. Goodfellow, et al., "Generative Adversarial Networks," arXiv:1406.2661, 2014. 
[Online]. Available: https://arxiv.org/abs/1406.2661
- [4] Song, Y., et al., "Denoising Diffusion Implicit Models," arXiv:2010.02502.
- [5]  B. Jacob, et al., "Quantization and Training of Neural Networks for Efficient 
Integer-Arithmetic-Only Inference," in Proceedings of the IEEE Conference on 
Computer Vision and Pattern Recognition (CVPR), 2018. [Online]. Available: 
https://arxiv.org/abs/1712.05877
- [6]  NVIDIA Developer, "Optimizing AI Inference with TensorRT," NVIDIA, 2023. 
[Online]. Available: https://developer.nvidia.com/tensorrt
- [7]  NVIDIA, "NVIDIA Jetson Orin Nano Super Developer Kit," [Online]. Available: 
https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-orin/
 nano-super-developer-kit/
- [8] H. Li, et al., "Pruning Filters for Efficient ConvNets," in Proceedings of the 
International Conference on Learning Representations (ICLR), 2017. [Online]. 
Available: https://arxiv.org/abs/1608.08710
- [9] M. Fordellone and M. Vichi, "Structural Equation Modeling and simultaneous 
clustering through the Partial Least Squares algorithm," Preprint submitted to Elsevier,2018. [Online]. Available: https://arxiv.org/abs/1810.07677


# Timeline for 18 weeks

## **第一階段（第 1 ~ 6 週）：OS2D 物件偵測系統開發**
**🔹 目標：**
- 建立 OS2D 環境，掌握 **單樣本物件偵測** 的核心概念。
- 透過 **旋轉數據增強（Rotation Augmentation）** 來微調模型，提高其泛化能力。

### **📅 第 1 週：環境建置與 OS2D 安裝**
✅ **目標**：
- 在 **Google Colab 或本機（Ubuntu + PyTorch）** 安裝 **OS2D**，建立開發環境。
- 測試 **官方 Demo**，確保預訓練模型可運行。

✅ **工作內容**：
1. 安裝 **PyTorch、OS2D 依賴套件**，確保環境相容。
2. 下載 **OS2D 官方模型與測試影像**。
3. 測試官方 `demo.py`，檢查是否能成功偵測範例影像。

✅ **驗證方式**：
- **成功載入 OS2D 模型**（檢查 `model.pth`）。
- **輸出 OS2D 物件偵測結果**（bounding box + 類別）。

---

### **📅 第 2 週：理解 OS2D 模型架構**
✅ **目標**：
- 深入理解 **OS2D Backbone（ResNet-50）** 如何提取影像特徵。
- 研究 **錨點特徵匹配（Anchor Feature Matching）**。

✅ **工作內容**：
1. 分析 **OS2D 物件偵測流程**（`os2d.py`）。
2. 研究 **OS2D 如何提取特徵圖（Feature Maps）**：
   - 使用 **Grad-CAM** 視覺化關鍵特徵。
   - **輸出 256 個通道的特徵圖**，找出最關鍵的通道。

✅ **驗證方式**：
- **成功輸出 256 通道的特徵圖**（PNG + `.npy`）。
- **比較不同輸入影像的 Grad-CAM 熱圖**。

---

### **📅 第 3 週：單樣本物件偵測測試**
✅ **目標**：
- 使用 **自訂影像** 測試 OS2D 的物件偵測效果。
- 設計 **旋轉、光照變化** 測試場景。

✅ **工作內容**：
1. **準備 5~10 張自訂影像**，並輸入 OS2D 測試。
2. 設計不同條件：
   - **旋轉 ±30°、±45°**
   - **改變亮度與對比度**
3. 記錄 OS2D 在這些條件下的偵測成功率（IoU）。

✅ **驗證方式**：
- **比較不同測試條件下的 IoU（交集並比）**。
- **輸出錯誤案例分析（False Positives / Negatives）**。

---

### **📅 第 4 週：微調 OS2D（Fine-Tuning）**
✅ **目標**：
- 對 **ResNet-50 Backbone** 進行微調，提升泛化能力。
- 使用 **旋轉數據增強（Rotation Augmentation）** 訓練新模型。

✅ **工作內容**：
1. **設定 OS2D 訓練流程**（使用 `train.py`）。
2. 設定：
   - **學習率：0.0001**
   - **Batch Size：8**
   - **旋轉增強範圍：±45°**
3. 訓練 10 個 Epochs，觀察 **mAP 變化**。

✅ **驗證方式**：
- **比較微調前後的 IoU、mAP**。
- **輸出新模型的偵測結果**（Bounding Box）。

---

## **第二階段（第 7 ~ 12 週）：生成式 AI 數據增強**
**🔹 目標：**
- 使用 **GAN 或 Diffusion Models** 生成 **探測影像（Probe Images）** 來幫助剪枝與量化。

### **📅 第 7 週：研究生成式 AI**
✅ **目標**：
- 了解 **GAN（StyleGAN、BigGAN）** 與 **Diffusion Models** 生成影像的原理。
- 測試 **基礎 GAN 影像生成**。

---

### **📅 第 8 週：生成探測影像**
✅ **目標**：
- 設計 **合成影像**，用於測試 OS2D 的特徵回應。

✅ **工作內容**：
1. 生成：
   - **隨機紋理**
   - **高頻 / 低頻影像**
2. 測試這些影像輸入 OS2D 的 **通道響應值**。

✅ **驗證方式**：
- 找出 **對特定通道影響最強的影像**。
- **視覺化通道響應變化**。

---

## **第三階段（第 13 ~ 18 週）：模型壓縮與優化**
**🔹 目標：**
- **剪枝（Pruning）+ 量化（Quantization）** 降低計算成本。

### **📅 第 13 週：深入通道剪枝**
✅ **目標**：
- **分析 OS2D 的 1024 個特徵通道**，找出 **低活性通道** 並進行剪枝。

✅ **工作內容**：
1. **計算每個通道的平均活性（Mean Activation）**。
2. **剪除影響最低的 30% 通道**。
3. 測試剪枝後的辨識率變化。

✅ **驗證方式**：
- **比較剪枝前後的 IoU、mAP、FPS**。

---

### **📅 第 14 週：量化感知訓練（QAT）**
✅ **目標**：
- **將 OS2D 模型量化至 FP16 / INT8**，降低記憶體需求。

✅ **工作內容**：
1. **使用 TensorRT** 進行 **FP16 量化**，測試推論速度。
2. **嘗試 INT8 量化**，並校準數據集。

✅ **驗證方式**：
- **比較原始模型 vs. 量化模型的 FPS、mAP**。

---

### **📅 第 15 ~ 16 週：剪枝 + 量化整合**
✅ **目標**：
- **剪枝（50%）+ 量化（FP16 / INT8）**，找到最佳配置。

✅ **驗證方式**：
- 記錄 **最終模型大小 vs. 準確率 vs. FPS**。

---

### **📅 第 17 ~ 18 週：成果驗證與報告**
✅ **目標**：
- 完成專題報告，整理 **測試數據 + 影像結果**。

