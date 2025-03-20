# 圖片道路遮罩轉換

## 簡介
本程式用於批量處理圖片，將圖片中紫色道路區域轉換為黑色 (0)，其餘區域保持為白色 (255)，以生成二值化道路標註圖。適用於需要標記道路區域的影像處理任務。
由於CamVid(Cambridge-Driving Labeled Video Database)有32個類別，為了只求出路面範圍而將其他類別的物件設為白色，目標路線設為黑色。

## 環境需求
- Python 3.x
- OpenCV (`cv2`)
- NumPy (`numpy`)
- OS (`os`)
- Shutil (`shutil`)
- Google Colab (`google.colab.files`，若在 Colab 上執行)

## 使用方式
### 1. 執行主要腳本
請確保您的 Python 腳本與輸入圖片資料夾位於相同的目錄下，然後執行以下程式碼。

#### **函數介紹**
- `convert_to_binary_road(input_path, output_path)`:
  - 讀取輸入圖片，將紫色區域 (RGB: 100,0,100 ~ 255,100,255) 轉換為黑色，其餘部分保持白色。
  - 儲存處理後的圖片。
  - Cambridge-Driving Labeled Video Database 中路面顏色為紫色

- `process_directory(input_dir, output_dir)`:
  - 處理整個資料夾內的圖片，產生標註圖片。
  - 支援格式：PNG、JPG、JPEG、BMP。

- `shutil.make_archive(output_filename, 'zip', folder_path)`:
  - 將輸出的標註圖片壓縮為 ZIP 檔。

- `files.download(output_filename)`:
  - 下載壓縮後的 ZIP 檔案（僅適用於 Google Colab）。

#### **範例執行方式**
```python
input_directory = "/content/1"  # 請替換成你的輸入資料夾路徑
output_directory = "/content/output1"  # 請替換成你的輸出資料夾路徑

result = process_directory(input_directory, output_directory)
print(result)

# 壓縮輸出資料夾
import shutil
output_filename = "/content/output.zip"
shutil.make_archive(output_filename.replace(".zip", ""), 'zip', output_directory)
print(f"{output_directory} 已壓縮為 {output_filename}")

# 下載壓縮檔案（僅適用於 Google Colab）
from google.colab import files
files.download(output_filename)
```

## 注意事項
1. **輸入圖片必須包含紫色道路區域，否則結果可能不準確。**
2. **程式執行時，請確保 `input_directory` 和 `output_directory` 的路徑正確。**
3. **若要在本機執行，請移除 `files.download()` 相關的 Colab 下載部分。**

