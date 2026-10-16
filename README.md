# Online Shoppers Purchase Prediction

## 1. Giới thiệu đề tài

Đề tài xây dựng mô hình dự đoán khả năng mua hàng của một phiên truy cập trong môi trường thương mại điện tử dựa trên các đặc trưng hành vi của phiên truy cập.

Hệ thống sử dụng dữ liệu hành vi truy cập website để dự đoán liệu phiên truy cập đó có dẫn đến hành động mua hàng hay không.

Các mô hình được sử dụng gồm:
- Logistic Regression
- Decision Tree
- Random Forest

Ngoài kết quả dự đoán, đề tài sử dụng SHAP để giải thích các đặc trưng có ảnh hưởng đến kết quả dự đoán của từng phiên truy cập.

## 2. Mục tiêu

- Tiền xử lý và chuẩn hóa dữ liệu hành vi của các phiên truy cập.
- Xây dựng các mô hình dự đoán khả năng mua hàng.
- So sánh hiệu quả giữa các mô hình.
- Xác định ngưỡng quyết định phù hợp thay vì chỉ sử dụng ngưỡng mặc định 0.5.
- Sử dụng các chỉ số ROC-AUC, F1-score, Precision và Recall để đánh giá mô hình.
- Sử dụng SHAP để giải thích kết quả dự đoán.
- Xác định các đặc trưng hành vi có ảnh hưởng lớn đến khả năng mua hàng.

## 3. Dataset

Đề tài sử dụng bộ dữ liệu Online Shoppers Purchasing Intention Dataset.

Dữ liệu mô tả hành vi của các phiên truy cập trên website thương mại điện tử. Mỗi dòng dữ liệu tương ứng với một phiên truy cập, trong đó các đặc trưng thể hiện hành vi và thông tin của phiên truy cập.

Biến mục tiêu:

- Revenue: cho biết phiên truy cập có phát sinh mua hàng hay không.

Các đặc trưng chính gồm:

- Administrative
- Administrative_Duration
- Informational
- Informational_Duration
- ProductRelated
- ProductRelated_Duration
- BounceRates
- ExitRates
- PageValues
- SpecialDay
- Month
- OperatingSystems
- Browser
- Region
- TrafficType
- VisitorType
- Weekend

## 4. Tiền xử lý dữ liệu

Quá trình tiền xử lý gồm:

1. Kiểm tra dữ liệu ban đầu.
2. Kiểm tra và xử lý các bản ghi trùng lặp.
3. Kiểm tra kiểu dữ liệu của các đặc trưng.
4. Phân chia dữ liệu thành tập Train, Validation và Test.
5. Mã hóa các biến phân loại.
6. Chuẩn bị dữ liệu đầu vào cho các mô hình.
7. Sử dụng seed cố định để đảm bảo khả năng tái lập kết quả.

Sau khi mã hóa, dữ liệu có 28 đặc trưng.

Kích thước dữ liệu:

- Train: 7323 × 28
- Validation: 2441 × 28
- Test: 2441 × 28

## 5. Mô hình

Đề tài xây dựng và so sánh 3 mô hình:

### Logistic Regression

Mô hình hồi quy Logistic được sử dụng để dự đoán xác suất một phiên truy cập có khả năng mua hàng.

### Decision Tree

Mô hình cây quyết định được sử dụng để phân loại phiên truy cập dựa trên các đặc trưng hành vi.

### Random Forest

Random Forest kết hợp nhiều cây quyết định nhằm cải thiện khả năng dự đoán và hạn chế hiện tượng quá khớp.

## 6. Đánh giá mô hình

Các chỉ số được sử dụng gồm:

- ROC-AUC
- F1-score
- Precision
- Recall
- Confusion Matrix

Do dữ liệu có sự mất cân bằng giữa các lớp, đề tài không chỉ dựa vào Accuracy mà sử dụng thêm F1-score, Precision và Recall để đánh giá.

Ngưỡng quyết định được lựa chọn dựa trên F1-score trên tập Validation.

Kết quả trên tập Test:

| Model | Threshold | ROC-AUC | F1 | Precision | Recall |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.5608 | 0.9171 | 0.6619 | 0.6034 | 0.7330 |
| Decision Tree | 1.0000 | 0.7400 | 0.5624 | 0.5646 | 0.5602 |
| Random Forest | 0.4100 | 0.9259 | 0.6640 | 0.6739 | 0.6545 |

Trong ba mô hình, Random Forest đạt ROC-AUC và F1-score cao nhất trong kết quả thử nghiệm.

## 7. Giải thích kết quả bằng SHAP

SHAP được sử dụng để giải thích mức độ đóng góp của từng đặc trưng vào kết quả dự đoán.

Một số đặc trưng có mức độ quan trọng cao gồm:

- PageValues
- ProductRelated_Duration
- ExitRates
- BounceRates
- ProductRelated
- Administrative_Duration

Trong đó PageValues là đặc trưng có mức độ quan trọng cao nhất trong mô hình Random Forest.

SHAP cũng được sử dụng để giải thích kết quả dự đoán của từng phiên truy cập, giúp xác định đặc trưng nào làm tăng hoặc giảm khả năng mua hàng.

Ví dụ:

- PageValues có SHAP dương → góp phần làm tăng khả năng mua hàng.
- ExitRates có SHAP âm → góp phần làm giảm khả năng mua hàng.
- BounceRates có SHAP âm → góp phần làm giảm khả năng mua hàng.

## 8. Demo dự đoán

Hệ thống cho phép nhập thông tin của một phiên truy cập và sử dụng mô hình Random Forest để:

1. Tính xác suất mua hàng.
2. So sánh xác suất với ngưỡng quyết định.
3. Đưa ra kết quả có khả năng mua hàng hoặc không có khả năng mua hàng.
4. Hiển thị các đặc trưng đóng góp chính bằng SHAP.

Ví dụ kết quả:

============================================================
        DEMO DỰ ĐOÁN KHẢ NĂNG MUA HÀNG
============================================================

Xác suất mua hàng: 41.00%
Ngưỡng quyết định: 0.41
Kết quả: CÓ khả năng mua hàng

3 ĐẶC TRƯNG ĐÓNG GÓP CHÍNH:

- numeric__PageValues: SHAP = 0.2562
  → tăng khả năng mua hàng

- numeric__ExitRates: SHAP = -0.1102
  → giảm khả năng mua hàng

- numeric__BounceRates: SHAP = -0.0889
  → giảm khả năng mua hàng

## 9. Cấu trúc thư mục

Online-Shoppers-Purchase-Prediction/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   └── 01_data_preparation.ipynb
│
├── src/
│
├── results/
│
├── requirements.txt
└── README.md

## 10. Công nghệ sử dụng

- Python
- Pandas
- Scikit-learn
- SHAP
- Joblib
- Google Colab
- GitHub

## 11. Kết quả

Kết quả thử nghiệm cho thấy Random Forest là mô hình có hiệu quả tốt nhất trong ba mô hình được xây dựng.

Các kết quả của Random Forest trên tập Test:

- ROC-AUC: 0.9259
- F1-score: 0.6640
- Precision: 0.6739
- Recall: 0.6545
- Ngưỡng quyết định: 0.41

Mô hình Random Forest được lựa chọn để thực hiện phần demo dự đoán và giải thích kết quả bằng SHAP.
