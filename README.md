# U-Net 影像分割專案

## 簡介

此專案使用 U-Net 模型進行影像分割，並可應用於影片處理。程式碼主要分為以下幾個部分：

1. **模型定義 (`UNet`)**: 定義 U-Net 模型架構，包含編碼器、瓶頸層和解碼器，用於提取影像特徵並進行像素級別的分類。
2. **資料集 (`CustomDataset`)**: 定義自定義資料集類別，用於載入訓練影像和對應的遮罩。
3. **訓練 (`train_model`)**: 訓練 U-Net 模型，使用二元交叉熵損失函數和 Adam 優化器。
4. **預測 (`UNetPredictor`)**: 使用訓練好的模型對單張圖片或影片進行預測，生成分割遮罩。
5. **影片處理 (`process_video`)**: 針對影片進行處理，每隔一定幀數進行預測，並根據黑色像素的出現次數決定最終遮罩。

## 使用方法

### 訓練模型

1. 將訓練影像放置於 `/content/1` 資料夾，遮罩放置於 `/content/2` 資料夾。
2. 執行 `main()` 函數開始訓練。
3. 訓練好的模型會儲存為 `unet_model.pth`。

### 預測單張圖片

1. 使用 `UNetPredictor` 類別載入訓練好的模型。
2. 使用 `predict()` 方法進行預測，並指定輸入圖片路徑和輸出遮罩路徑。

### 預測影片

1. 使用 `process_video()` 函數，並指定模型路徑、影片路徑、最終遮罩路徑、幀間隔和黑色像素閾值。
2. 程式會每隔一定幀數進行預測，並根據黑色像素的出現次數決定最終遮罩。

## 注意事項

- 訓練影像和遮罩應為 PNG 格式，且遮罩應為單通道灰階影像。
- 影片處理時，幀間隔和黑色像素閾值可根據實際情況調整。
- 確保已安裝必要的套件，如 PyTorch、OpenCV 等。
- 本程式初始運作環境是在google colab上。
  
## 參考資料

- [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://arxiv.org/abs/1505.04597)
- [Day 20：使用 U-Net 作影像分割(Image Segmentation)](https://ithelp.ithome.com.tw/articles/10240314)
- [深度學習Paper系列(05)：U-Net](https://tomohiroliu22.medium.com/%E6%B7%B1%E5%BA%A6%E5%AD%B8%E7%BF%92paper%E7%B3%BB%E5%88%97-05-u-net-41be7533c934)
- [教學影片] U-Net 影像分割演算法實作]([https://youtu.be/Er_UmH9qADE?si=wU1IQWH7xLO-To8U](https://www.youtube.com/watch?v=Er_UmH9qADE))

## 資料集

- [CamVid (Cambridge-Driving Labeled Video Database)](https://www.kaggle.com/datasets/carlolepelaars/camvid)
